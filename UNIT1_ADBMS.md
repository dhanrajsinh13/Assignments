---
title: -- 1. UNIT 1 SQL AND ADVANCE SQL QUERIES
created: 2025-03-15T13:39:41+05:30
lastUpdated: 2025-03-15T13:39:44+05:30
category: 
---

-- 1. Creating the Customer Table
CREATE TABLE Customer (
    CustNo NUMBER PRIMARY KEY,
    CName VARCHAR2(50) NOT NULL,
    State VARCHAR2(50),
    Phone VARCHAR2(15)
);

-- 2. Creating the Item Table
CREATE TABLE Item (
    ItemNo NUMBER PRIMARY KEY,
    ItemName VARCHAR2(50) NOT NULL,
    ItemPrice NUMBER(10,2),
    Qty_On_Hand NUMBER
);

-- 3. Creating the Invoice Table
CREATE TABLE Invoice (
    InvNo NUMBER PRIMARY KEY,
    InvDate DATE,
    CustNo NUMBER,
    FOREIGN KEY (CustNo) REFERENCES Customer(CustNo)
);

-- 4. Creating the InvItem Table (Invoice-Item Relationship)
CREATE TABLE InvItem (
    InvNo NUMBER,
    ItemNo NUMBER,
    Qty NUMBER,
    PRIMARY KEY (InvNo, ItemNo),
    FOREIGN KEY (InvNo) REFERENCES Invoice(InvNo),
    FOREIGN KEY (ItemNo) REFERENCES Item(ItemNo)
);

-- Inserting Data into Customer Table
INSERT INTO Customer VALUES (1, 'John Doe', 'California', '1234567890');
INSERT INTO Customer VALUES (2, 'Alice Smith', 'Texas', '9876543210');
INSERT INTO Customer VALUES (3, 'Bob Johnson', 'Florida', '4561237890');
INSERT INTO Customer VALUES (4, 'David White', 'New York', '7896541230');
INSERT INTO Customer VALUES (5, 'Emma Brown', 'Nevada', '3216549870');

-- Inserting Data into Item Table
INSERT INTO Item VALUES (101, 'Mountain Bike', 500, 10);
INSERT INTO Item VALUES (102, 'Road Bike', 700, 5);
INSERT INTO Item VALUES (103, 'Helmet', 50, 30);
INSERT INTO Item VALUES (104, 'Gloves', 20, 50);
INSERT INTO Item VALUES (105, 'Gear Set', 200, 15);

-- Inserting Data into Invoice Table
INSERT INTO Invoice VALUES (1001, TO_DATE('2024-03-10', 'YYYY-MM-DD'), 1);
INSERT INTO Invoice VALUES (1002, TO_DATE('2024-03-11', 'YYYY-MM-DD'), 2);
INSERT INTO Invoice VALUES (1003, TO_DATE('2024-03-12', 'YYYY-MM-DD'), 3);
INSERT INTO Invoice VALUES (1004, TO_DATE('2024-03-13', 'YYYY-MM-DD'), 4);
INSERT INTO Invoice VALUES (1005, TO_DATE('2024-03-14', 'YYYY-MM-DD'), 5);

-- Inserting Data into InvItem Table
INSERT INTO InvItem VALUES (1001, 101, 2);
INSERT INTO InvItem VALUES (1001, 103, 1);
INSERT INTO InvItem VALUES (1002, 102, 1);
INSERT INTO InvItem VALUES (1003, 104, 3);
INSERT INTO InvItem VALUES (1004, 105, 2);

-- 1. Add a column to the Item table for Item Color
ALTER TABLE Item ADD (ItemColor VARCHAR2(20));

-- 2. Display Item name and price in a sentence format
SELECT 'The item ' || ItemName || ' costs $' || ItemPrice AS ItemDetails FROM Item;

-- 3. Find total value of each item based on quantity on hand
SELECT ItemName, (ItemPrice * Qty_On_Hand) AS TotalValue FROM Item;

-- 4. Find total, average, highest, and lowest unit price
SELECT SUM(ItemPrice) AS TotalPrice, 
       AVG(ItemPrice) AS AvgPrice, 
       MAX(ItemPrice) AS MaxPrice, 
       MIN(ItemPrice) AS MinPrice 
FROM Item;

-- 5. Find invoices with 'Gear' in their item name
SELECT DISTINCT InvNo FROM InvItem
JOIN Item ON InvItem.ItemNo = Item.ItemNo
WHERE ItemName LIKE '%Gear%';

-- 6. Find all possible combinations of customers and items
SELECT C.CustNo, C.CName, I.ItemNo, I.ItemName 
FROM Customer C CROSS JOIN Item I;

-- 7. Display all item quantity and item price for invoices
SELECT InvItem.InvNo, InvItem.ItemNo, Item.ItemPrice, InvItem.Qty 
FROM InvItem JOIN Item ON InvItem.ItemNo = Item.ItemNo;

-- 8. Find total price amount for each invoice
SELECT InvItem.InvNo, SUM(Item.ItemPrice * InvItem.Qty) AS TotalAmount 
FROM InvItem JOIN Item ON InvItem.ItemNo = Item.ItemNo
GROUP BY InvItem.InvNo;

-- 9. Find the items with the top three prices
SELECT * FROM Item ORDER BY ItemPrice DESC FETCH FIRST 3 ROWS ONLY;

-- 10. Find two items with the lowest quantity on hand
SELECT * FROM Item ORDER BY Qty_On_Hand ASC FETCH FIRST 2 ROWS ONLY;

-- 11. Display items ordered as well as not ordered so far
SELECT Item.ItemNo, Item.ItemName, NVL(InvItem.InvNo, 'Not Ordered') AS InvoiceStatus
FROM Item LEFT JOIN InvItem ON Item.ItemNo = InvItem.ItemNo;

-- 12. Create a simple view with item names and item price
CREATE VIEW ItemView AS SELECT ItemName, ItemPrice FROM Item;

-- 13. Create a sequence for new item entries
CREATE SEQUENCE ItemSeq START WITH 106 INCREMENT BY 1;

-- 14. Add a new item using the sequence
INSERT INTO Item VALUES (ItemSeq.NEXTVAL, 'Smart Watch', 250, 20, 'Black');

-- 15. Create an index to speed up search on Customer table
CREATE INDEX idx_Customer_Phone ON Customer(Phone);
