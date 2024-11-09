# Delivery Order System SQL Schema

This document outlines the SQL Data Definition Language (DDL) to create a table for a delivery order system, along with SQL Data Manipulation Language (DML) statements to insert sample data and update records in the table. Each column in the table is explained in detail.

## SQL DDL to Create Table

```sql
CREATE TABLE DeliveryOrders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL,
    DeliveryAddress VARCHAR(255) NOT NULL,
    ContactNumber VARCHAR(15) NOT NULL,
    OrderDate DATE NOT NULL,
    DeliveryDate DATE,
    ItemDescription VARCHAR(255) NOT NULL,
    Quantity INT NOT NULL CHECK (Quantity > 0),
    TotalPrice DECIMAL(10, 2) NOT NULL CHECK (TotalPrice >= 0),
    Status VARCHAR(50) NOT NULL
);
```

## Explanation of Columns

1. **OrderID** (`INT`):
   - **Description**: A unique identifier for each delivery order.
   - **Constraints**: This is the primary key of the table, ensuring that each order can be uniquely identified.

2. **CustomerName** (`VARCHAR(100)`):
   - **Description**: The name of the customer placing the order.
   - **Constraints**: This field cannot be null.

3. **DeliveryAddress** (`VARCHAR(255)`):
   - **Description**: The address where the order should be delivered.
   - **Constraints**: This field cannot be null.

4. **ContactNumber** (`VARCHAR(15)`):
   - **Description**: The phone number of the customer for contact purposes.
   - **Constraints**: This field cannot be null.

5. **OrderDate** (`DATE`):
   - **Description**: The date when the order was placed.
   - **Constraints**: This field cannot be null.

6. **DeliveryDate** (`DATE`):
   - **Description**: The expected or actual date when the order will be delivered.
   - **Constraints**: This field can be null if the delivery date is not yet determined.

7. **ItemDescription** (`VARCHAR(255)`):
   - **Description**: A description of the item(s) ordered.
   - **Constraints**: This field cannot be null.

8. **Quantity** (`INT`):
   - **Description**: The number of items ordered.
   - **Constraints**: This field cannot be null and must be greater than zero.

9. **TotalPrice** (`DECIMAL(10, 2)`):
   - **Description**: The total price of the order, calculated based on quantity and item price.
   - **Constraints**: This field cannot be null and must be zero or greater.

10. **Status** (`VARCHAR(50)`):
    - **Description**: The current status of the order (e.g., Pending, Delivered, In Transit).
    - **Constraints**: This field cannot be null.

## SQL DML to Insert Sample Data

```sql
INSERT INTO DeliveryOrders (OrderID, CustomerName, DeliveryAddress, ContactNumber, OrderDate, DeliveryDate, ItemDescription, Quantity, TotalPrice, Status) VALUES
(1, 'John Doe', '123 Elm St, Cityville', '123-456-7890', '2024-11-01', '2024-11-03', 'Wireless Mouse', 2, 40.00, 'Delivered'),
(2, 'Jane Smith', '456 Oak St, Townsville', '987-654-3210', '2024-11-02', '2024-11-04', 'Bluetooth Headphones', 1, 60.00, 'In Transit'),
(3, 'Alice Johnson', '789 Pine St, Villagetown', '555-123-4567', '2024-11-03', '2024-11-05', 'USB-C Charger', 3, 30.00, 'Pending'),
(4, 'Bob Brown', '321 Maple Ave, Citytown', '444-987-6543', '2024-11-04', '2024-11-06', 'Laptop Stand', 1, 25.00, 'Delivered'),
(5, 'Carol White', '654 Cedar Blvd, Metropolis', '222-333-4444', '2024-11-05', '2024-11-07', 'Ergonomic Keyboard', 1, 50.00, 'In Transit');
```

## SQL DML to Update Existing Records

To update an existing record in the `DeliveryOrders` table (for example: changing the status of an order), you can use the following SQL statement:

```sql
UPDATE DeliveryOrders
SET Status = 'Delivered',
    DeliveryDate = CURRENT_DATE
WHERE OrderID = 3;
```

### Explanation of Update Statement

1. **SET Clause**:
   - `Status`: Changes the status of the order to "Delivered".
   - `DeliveryDate`: Sets the delivery date to today's date using `CURRENT_DATE`.

2. **WHERE Clause**:
   - Identifies which record(s) to update based on `OrderID`.
