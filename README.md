# Bookstore Order Flow — System Analysis

This repository presents a **complete system analysis** of the process of purchasing a book in an online bookstore.  
The analysis begins from the moment the user initiates the checkout (with the book already in the cart) and ends at the payment confirmation stage.

## Initial task description:  
Покупка Книги в интернет магазине  
  
Разложите на бизнес и системную составляющую, процесс покупки книги в интернет-магазине, начиная с момента оформления заказа и заканчивая подтверждением платежа (вы давний пользователь данного магазина и нужная вам книга уже у вас в корзине, и когда вы совершите оплату, то заветную книгу вам каким-то волшебным образом доставят эльфы, не раскрывайте их процессных тайн).  
Кратко опишите -ключевые сущности (их функциональность) и определите этапы их взаимодействия, придумайте каким образом можно простроить межсистемную интеграцию для данного процесса (укажите что и где будет выполняться, как и кем будет использоваться).  
Постройте схему, отразите в вашем workflow - все этапы, все кейсы, возможные альтернативы.  
Для построение схемы можете использовать любой софт, позволяющий просмотреть вашу работу внешним пользователям.

---

## Repository Structure
<pre>├── README.md - provides an overview of the project and general information
└── docs
    ├── api-description.yaml - details the specifications and endpoints of the APIs used in the system
    ├── entities.md - describes the key entities involved in the system and their attributes
    ├── integration.md - outlines the process of integrating the various system components and external services
    ├── plantuml - contains various UML diagrams that visually represent different aspects of the system architecture and processes
    │   ├── 01_ComponentDiagram
    │   │   ├── ComponentDiagram.puml
    │   │   ├── ComponentDiagram.png
    │   │   └── ComponentDiagram.svg
    │   ├── 02_UseCaseDiagram
    │   │   ├── UseCaseDiagram.puml
    │   │   ├── UseCaseDiagram.png
    │   │   └── UseCaseDiagram.svg
    │   ├── 03_ActivityDiagram
    │   │   ├── ActivityDiagram.puml
    │   │   ├── ActivityDiagram.png
    │   │   └── ActivityDiagram.svg
    │   ├── 04_SequenceDiagram
    │   │   ├── SequenceDiagram.puml
    │   │   ├── SequenceDiagram.png
    │   │   └── SequenceDiagram.svg
    │   ├── 05_ERDiagram
    │   │   ├── ERDiagram.puml
    │   │   ├── ERDiagram.png
    │   │   └── ERDiagram.svg
    │   ├── 06_BookStateDiagram
    │   │   ├── BookStateDiagram.puml
    │   │   ├── BookStateDiagram.png
    │   │   └── BookStateDiagram.svg
    │   ├── 07_OrderStateDiagram
    │   │   ├── OrderStateDiagram.puml
    │   │   ├── OrderStateDiagram.png
    │   │   └── OrderStateDiagram.svg
    │   └── 08_PaymentStateDiagram
    │       ├── PaymentStateDiagram.puml
    │       ├── PaymentStateDiagram.png
    │       └── PaymentStateDiagram.svg
    └── workflow.md - text description of the order process flow</pre>

## Technologies Used

- **PlantUML** — for architecture diagrams
- **Markdown** — for documentation
- **Git** - for storing the documentation

## Core Entities

- `User` — customer of the bookstore
- `Cart` — container for selected books
- `Order` — represents a confirmed intention to purchase
- `Payment` — stores transaction details and status
- `Payment Gateway` — external payment processor

---

## Covered Scenarios

- Successful checkout and payment
- Payment failure
- User cancels payment
- Payment timeout
- Refund request (e.g. book unavailable)