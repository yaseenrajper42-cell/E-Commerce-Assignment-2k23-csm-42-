#Sprint 1 â€” System Architecture & Scope

## 1. Target Audience & Market Focus

### Primary Persona

The main users of this e-commerce website will be **young retail customers and university students** who usually shop online for everyday fashion items such as shirts, trousers, shoes, and accessories. The website is mainly aimed at users who want a simple way to browse products, compare prices, add items to a cart, and place an order without going through a complicated process.

A typical user can be considered a student or young working person who uses a mobile phone regularly and is comfortable with online shopping.

### Core Pain Point

A common problem with small online stores is that product information, stock availability, and the ordering process are not always organized in one place. Customers may have difficulty finding the right product or keeping track of the items they want to buy.

The proposed system will provide a single platform where customers can browse products, search and filter the catalog, manage their cart, and place orders. For the store side, basic product and inventory management will also be included.

### Domain Scope

The project will focus on the **Consumer Apparel / Fashion E-Commerce** market.

The initial product catalog will include categories such as clothing, footwear, and accessories. The MVP will focus on the basic shopping process rather than advanced features such as recommendations, live chat, loyalty programs, or multiple-vendor support.

---

## 2. MVP Feature Scope

The MVP will contain the following core workflows. The scope is intentionally kept small so that the main shopping flow can be completed within the semester.

| Category | Feature | Description | Priority |
|---|---|---|---|
| Authentication | User Registration & Login | Users can create an account and log in securely. Passwords will be stored using hashing and authentication will use JWT. | High (MVP) |
| Catalog | Product List & Search | Users can browse available products and search for products by name. Products can also be filtered using categories. | High (MVP) |
| Cart | Cart Management | Users can add products to their cart, change quantities, and remove items before checkout. | High (MVP) |
| Checkout | Order Processing | Users can confirm their cart and place an order. A mock payment flow will be used initially instead of depending on a real payment service. | High (MVP) |
| Orders | Order History | Logged-in users can view their previous orders and basic order details such as total amount and status. | Medium (MVP) |
| Admin | Product & Inventory Management | An admin can add, edit, delete, and update stock quantities for products. | Medium |

### Out of Scope for Sprint 1 / MVP

The following features are not required for the initial MVP:

- Product reviews and ratings
- Wishlist
- Discount/coupon system
- Recommendation system
- Multiple sellers/vendors
- Advanced analytics
- Real payment settlement
- Delivery tracking integration

These can be considered later if there is enough time after the required features are completed.

---

## 3. Tech Stack Selection & Justification

### Frontend Framework: Next.js (React)

I plan to use **Next.js with React** for the frontend. It provides a component-based structure that is suitable for building product pages, the shopping cart, checkout, and admin screens. Compared with using plain React alone, Next.js also gives a clear project structure and useful features for routing and web performance, while still being relatively easy to work with for a semester project.

### Backend Infrastructure: Node.js + Express.js

The backend will use **Node.js with Express.js**. Express is lightweight and has a large ecosystem, which makes it practical for creating REST APIs for users, products, carts, and orders. Node.js also allows the frontend and backend project to use JavaScript/TypeScript, which should make development and debugging easier for an individual project.

### Database Management System: PostgreSQL

I will use **PostgreSQL** as the main database because the project has several related entities such as users, products, orders, and order items. A relational database makes the relationships and foreign-key constraints easier to enforce compared with a document database such as MongoDB. PostgreSQL also supports suitable data types for prices, timestamps, and IDs and provides good data integrity for order records.

### Caching: Redis (Optional)

**Redis** may be added later if caching or session-related performance becomes necessary. For the first version, PostgreSQL will handle the main persistent data, so Redis is not considered a required MVP dependency.

### Proposed Architecture

The basic architecture will follow a simple client-server approach:

**Next.js Frontend â†’ Express REST API â†’ PostgreSQL Database**

The frontend will send requests to the backend API. The backend will handle authentication, business logic, validation, and database operations. This keeps the database separate from the user interface and makes the application easier to extend in later sprints.

---

## 4. Entity-Relationship Diagram (ERD)

The database is designed around the main shopping workflow. A user can place multiple orders and have a cart. An order contains one or more order items, while each order item refers to a product. Products belong to categories.

The `ORDER_ITEMS` table is used as the associative entity between `ORDERS` and `PRODUCTS`. This also allows the quantity and purchase-time unit price to be stored for every product in an order.

```mermaid
erDiagram