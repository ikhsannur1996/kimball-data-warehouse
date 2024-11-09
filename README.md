# Delivery Order System SQL Schema

This document outlines the SQL Data Definition Language (DDL) to create a table for a delivery order system, along with SQL Data Manipulation Language (DML) statements to insert sample data into the table.

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
    Status VARCHAR(50) NOT NULL,
    PaymentMethod VARCHAR(50) NOT NULL, -- New column for payment method
    PaymentStatus VARCHAR(50) NOT NULL, -- New column for payment status
    DeliveryMethod VARCHAR(50),          -- New column for delivery method
    TrackingNumber VARCHAR(100),         -- New column for tracking number
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- New column for creation timestamp
    UpdatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP -- New column for update timestamp
);
```

## SQL DML to Insert Sample Data

```sql
INSERT INTO DeliveryOrders (OrderID, CustomerName, DeliveryAddress, ContactNumber, OrderDate, DeliveryDate, ItemDescription, Quantity, TotalPrice, Status, PaymentMethod, PaymentStatus, DeliveryMethod, TrackingNumber) VALUES
(1, 'John Doe', '123 Elm St, Cityville', '123-456-7890', '2024-11-01', '2024-11-03', 'Wireless Mouse', 2, 40.00, 'Delivered', 'Credit Card', 'Paid', 'Standard', 'TRACK123456'),
(2, 'Jane Smith', '456 Oak St, Townsville', '987-654-3210', '2024-11-02', '2024-11-04', 'Bluetooth Headphones', 1, 60.00, 'In Transit', 'PayPal', 'Paid', 'Express', 'TRACK987654'),
(3, 'Alice Johnson', '789 Pine St, Villagetown', '555-123-4567', '2024-11-03', '2024-11-05', 'USB-C Charger', 3, 30.00, 'Pending', 'Debit Card', 'Pending', 'Standard', NULL),
(4, 'Bob Brown', '321 Maple Ave, Citytown', '444-987-6543', '2024-11-04', '2024-11-06', 'Laptop Stand', 1, 25.00, 'Delivered', 'Credit Card', 'Paid', 'Standard', 'TRACK111222'),
(5, 'Carol White', '654 Cedar Blvd, Metropolis', '222-333-4444', '2024-11-05', '2024-11-07', 'Ergonomic Keyboard', 1, 50.00, 'In Transit', 'Bank Transfer', 'Pending', 'Express', NULL),
(6, 'David Green', '987 Birch St, Urbania', '111-222-3333', '2024-11-06', '2024-11-08', 'Gaming Mouse', 2, 70.00, 'Pending', 'Credit Card', 'Pending', NULL),
(7, 'Eva Black', '135 Spruce Rd, Suburbia', '333-444-5555', '2024-11-07', '2024-11-09', 'Monitor Stand', 1, 35.00, 'Delivered', 'PayPal', 'Paid', NULL),
(8, 'Frank Blue', '246 Willow Way, Countryside','666-777-8888','2024-11-08','NULL','Desk Organizer','3','15.00','Pending','Debit Card','Pending','Standard','TRACK333444'),
(9,'Grace Yellow','369 Fir St,Riverside','999-888-7777','2024-11-09','NULL','Phone Case','2','20.00','In Transit','Credit Card','Paid','Express','TRACK555666'),
(10,'Henry Purple','159 Chestnut Ln,Hilltown','888-999-0000','NULL','NULL','Smartwatch','1','200.00','Pending','Bank Transfer','Pending','Standard','TRACK777888');
```

## Explanation of New Columns

1. **PaymentMethod**: Specifies how the customer paid for the order (e.g., Credit Card, PayPal).
2. **PaymentStatus**: Indicates whether the payment has been completed or is still pending.
3. **DeliveryMethod**: Describes the type of delivery service used (e.g., Standard or Express).
4. **TrackingNumber**: A unique identifier used to track the shipment.
5. **CreatedAt**: Timestamp indicating when the order was created.
6. **UpdatedAt**: Timestamp indicating when the order was last updated.
