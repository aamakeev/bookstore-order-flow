# Workflow: Book Purchase in Online Store

## Main Scenario (Happy Path)
1. **User opens the cart**
   - System fetches cart items.
   - Cart UI shows book(s) ready for checkout.

2. **User confirms order**
   - Backend creates a new `Order` with status `created`.
   - Emits event `OrderCreated`.

3. **User proceeds to payment**
   - System creates a `Payment` record with status `pending`.
   - Payment Service provides URL to finalize payment.
   - Frontend displays payment page to user.
   - Redirects to Payment Gateway page.

4. **User completes payment**
   - Gateway sends callback with `success` status.
   - System updates `Payment` and `Order` status to `paid`.
   - Emits event `OrderPaid`.

5. **Confirmation screen**
   - User is shown success message and order summary.

---

## Alternative Scenarios

### Payment Failure
- Gateway callback returns `failed` status.
- System updates `Payment` to `failed`.
- User sees error message with retry option.

### User Cancels Payment
- User clicks cancel on web payment page.
- System updates `Payment` to `cancelled`.
- User sees cancellation message with retry option if payment timeout didn't happen.

### Payment Timeout
- User inactive for configured duration.
- System marks `Payment` as `timeout`.
- System marks `Order` as `cancelled`.
- User is informed about the cancellation of the order due to timeout.

### Refund Requested
- Triggered automatically if the order cannot be fulfilled (e.g., book out of stock) or can be initiated by the User via UI if this action is allowed by the system according to policy.
- System initiates refund via Payment Gateway.
- Updates `Payment` status to `refunded`.
- Emits event `PaymentRefunded`.
- User is informed about the successful refund.

---

## Edge Case Handling
| Case                         | Action Taken                               |
|------------------------------|--------------------------------------------|
| Gateway unresponsive         | Retry on callback, log alert               |
| Double callback              | Idempotency enforced via payment ID        |
| No stock after pay           | Trigger refund process                     |
| Unauthorised users' attempts | Require login                              |