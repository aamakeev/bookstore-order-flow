# Integration and Interfaces

## Overview
This system follows a **modular, event-driven architecture** with REST APIs and asynchronous communication through **Apache Kafka**. The design adheres to the principles of Domain-Driven Design (DDD), focusing on aligning the software closely with the underlying business context and its domain logic. This approach facilitates a more intuitive and business-relevant development process, enhancing both scalability and maintainability.

---

## Synchronous Interactions (REST)

| From       | To                | Endpoint                    | Purpose                          |
|------------|-------------------|-----------------------------|----------------------------------|
| Frontend   | Cart Service      | `GET /cart/{userId}`        | Retrieve user's cart             |
| Frontend   | Checkout Service  | `POST /checkout`            | Process checkout details         |
| Frontend   | Order Service     | `POST /orders`              | Create a new order               |
| Frontend   | Payment Service   | `POST /payments`            | Start payment process            |
| PaymentSvc | Payment Gateway   | External redirect           | Collect payment details          |
| Gateway    | Payment Service   | `POST /payment-callback`    | Notify of payment status         |

---

## Asynchronous Interactions (Kafka)

| Kafka Topic         | Producer        | Consumers                     | Triggered On                           |
|---------------------|-----------------|-------------------------------|----------------------------------------|
| `order.created`     | Order Service   | Notification, Payment Service | When a user confirms the order         |
| `payment.success`   | Payment Service | Notification, Order Service   | When payment is successfully processed |
| `payment.failed`    | Payment Service | Notification, Order Service   | When payment fails                     |

---

## Authentication
- All frontend calls use **JWT tokens**.
- Internal services use **mutual TLS** or internal API keys.

---

## Error Handling
- Gateway callbacks are idempotent.
- Timeout fallback: if callback doesn’t arrive, system polls status or expires.
- Retries with backoff are implemented for webhook failures.

---

## Monitoring
- All services emit logs and metrics.
- Alerting set up on key failures: payment fails, refund rejected, callback delays.
- Each user actions trigger specific business metrics in Analytics system.