# Delivery Order System SQL Schema

## Overview

This document outlines the SQL Data Definition Language (DDL) to create a table for a delivery order system, along with SQL Data Manipulation Language (DML) statements to insert sample data and update records in the table. Each column in the table is explained in detail.

## SQL DDL to Create Table

Below is the SQL code snippet used to create the `delivery_orders` table:

```sql
CREATE TABLE delivery_orders (
    order_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    delivery_address VARCHAR(255) NOT NULL,
    contact_number VARCHAR(15) NOT NULL,
    order_date DATE NOT NULL,
    delivery_date DATE,
    item_description VARCHAR(255) NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    total_price DECIMAL(10, 2) NOT NULL CHECK (total_price >= 0),
    status VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Explanation of Columns

Each column in the `delivery_orders` table has specific constraints and descriptions as follows:

1. **order_id**
   - **Description:** A unique identifier for each delivery order.
   - **Constraints:** This is the primary key of the table, ensuring that each order can be uniquely identified.

2. **customer_name**
   - **Description:** The name of the customer placing the order.
   - **Constraints:** This field cannot be null.

3. **delivery_address**
   - **Description:** The address where the order should be delivered.
   - **Constraints:** This field cannot be null.

4. **contact_number**
   - **Description:** The phone number of the customer for contact purposes.
   - **Constraints:** This field cannot be null.

5. **order_date**
   - **Description:** The date when the order was placed.
   - **Constraints:** This field cannot be null.

6. **delivery_date**
   - **Description:** The expected or actual date when the order will be delivered.
   - **Constraints:** This field can be null if the delivery date is not yet determined.

7. **item_description**
   - **Description:** A description of the item(s) ordered.
   - **Constraints:** This field cannot be null.

8. **quantity**
   - **Description:** The number of items ordered.
   - **Constraints:** This field cannot be null and must be greater than zero.

9. **total_price**
   - **Description:** The total price of the order, calculated based on quantity and item price.
   - **Constraints:** This field cannot be null and must be zero or greater.

10. **status**
    - **Description:** The current status of the order (e.g., Pending, Delivered, In Transit).
    - **Constraints:** This field cannot be null.

11. **created_at**
    - **Description:** Timestamp indicating when the entry was added into this database.
    - **Default Value:** Automatically set by default timestamp function provided by MySQL server at time point it gets inserted into DBMS environment.

## SQL DML to Insert Sample Data

Below are some examples demonstrating how one might go about inserting various types of entries within our newly defined structure:

```sql
INSERT INTO delivery_orders (order_id, customer_name, delivery_address, contact_number, order_date, delivery_date, item_description, quantity, total_price, status) VALUES
(1, 'John Doe', '123 Elm St, Cityville', '123-456-7890', '2024-11-01', '2024-11-03', 'Wireless Mouse', 2, 40.00, 'Delivered'),
(2, 'Jane Smith', '456 Oak St, Townsville', '987-654-3210', '2024-11-02', '2024-11-04', 'Bluetooth Headphones', 1, 60.00, 'In Transit'),
(3, 'Alice Johnson', '789 Pine St, Villagetown', '555-123-4567', '2024-11-03', '2024-11-05', 'USB-C Charger', 3, 30.00, 'Pending'),
(4, 'Bob Brown', '321 Maple Ave, Citytown', '444-987-6543', '2024-11-04', '2024-11-06', 'Laptop Stand', 1, 25.00, 'Delivered'),
(5, 'Carol White', '654 Cedar Blvd, Metropolis', '222-333-4444', '2024-11-05', '2024-11-07', 'Ergonomic Keyboard', 1, 50.00, 'In Transit');
```

## SQL DML to Update Existing Records

To update an existing record in the `delivery_orders` table (for example: changing the status of an order), you can use the following SQL statement:

```sql
UPDATE delivery_orders
SET status = 'Delivered',
    delivery_date = CURRENT_DATE
WHERE order_id = 3;
```

### Explanation of Update Statement

1. **SET Clause**:
   - `status`: Changes the status of the order to "Delivered".
   - `delivery_date`: Sets the delivery date to today's date using `CURRENT_DATE`.

2. **WHERE Clause**:
   - Identifies which record(s) to update based on `order_id`.
