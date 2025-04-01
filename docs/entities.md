# Key Entities in Book Purchase Flow

## User
- Authenticated customer.
- Has profile info, saved addresses, and order history.
- **Fields**: id (INT), email (VARCHAR), name (VARCHAR).

## Cart
- Temporary storage of items user intends to buy.
- Tied to user session or account.
- Editable until order confirmation.
- **Fields**: user_id (INT), item_ids (TEXT).

## Order
- Represents user's confirmed intent to buy.
- States: `created`, `paid`, `cancelled`, `refunded`.
- Links to user, items, and payment.
- **Fields**: id (INT), user_id (INT), status (VARCHAR), created_at (DATETIME).

## Payment
- Contains transaction metadata.
- Tracks status: `pending`, `success`, `failed`, `cancelled`, `timeout`, `refunded`.
- Includes reference to external gateway and internal order.
- **Fields**: id (INT), user_id (INT), order_id (INT), gateway_id (VARCHAR), status (VARCHAR).

## Book (Product)
- Includes title, author, stock count, price.
- May become `unavailable` or `out_of_stock`.
- **Fields**: id (INT), title (VARCHAR), price (DECIMAL).

## Stock
- Tracks the quantity of each book available.
- **Fields**: book_id (INT), quantity (INT).

## Payment Gateway (External)
- Handles real-time payment authorization and processing.
- Returns callbacks to backend on status change.
- Can trigger retry or cancellation flows.
- **Directly interacts with the Payment Service to facilitate transactions.**

## Kafka
- Enables asynchronous communication between services.
Sample topics:
- `order.created`
- `order.paid`
- `payment.refunded`

---

## Database Tables (Logical)
| Table       | Key Columns                               |
|-------------|-------------------------------------------|
| `users`     | id, email, name                           |
| `carts`     | user_id, item_ids                         |
| `orders`    | id, user_id, status, created_at           |
| `payments`  | id, user_id, order_id, gateway_id, status |
| `products`  | id, title, price, stock                   |
| `stocks`    | book_id, quantity                         |
