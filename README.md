# CourseraProj1_30165
RDBMS Projects



What is the project about?
The project is about designing and building a centralized relational database system for a New York-based coffee shop chain that is planning to expand nationally through franchises.



Mission Statement:
“The purpose of the New York Coffee Co. DB system is to maintain the data that is used and generated to support the specialty coffee retail and franchise expansion business for our customers and suppliers and to facilitate the cooperation and sharing of information between corporate headquarters, franchise outlets, supply chain, and sales operations.”



Mission Objectives:

    To Maintain (Enter, Update and Delete) data on:
    Inventory levels, Supplier deliveries, Outlet equipment logs, Maintenance schedules, Workforce shift assignments

    To Perform searches on:
    Daily stock movements, Machine maintenance history, Franchise supply requests, Delivery discrepancies

    To Track the status of:
    Store operational readiness, Inventory reorder thresholds, Equipment downtime, Supply chain disruptions

    To Report on:
    Daily operations KPIs, Outlet-level inventory usage, Supplier delivery performance, Workforce productivity metrics



System Definition:
Business Unit	- Entities (This is the format followed below)
Operations -	Inventory, Suppliers, Equipment, Maintenance Logs, Shift Assignments
Sales & Marketing -	Sales Transactions, Products, Campaigns, Loyalty Program, Promotions
Human Resources (HR) -	Staff, Roles, Attendance, Payroll, Training Records
Finance & Accounting -	Invoices, Payments, Budget Allocations, Revenue Reports
Supply Chain	- Purchase Orders, Shipment Schedules, Supplier Contracts
Customer Service -	Customer Records, Feedback, Issue Tickets, Service History
Franchise Development -	Franchise Agreements, Locations, Onboarding Documents, Compliance Checklists



Code:

-- Table: staff
CREATE TABLE staff (
    staff_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    position VARCHAR(50),
    start_date DATE,
    location VARCHAR(50)
);

-- Table: sales_outlet
CREATE TABLE sales_outlet (
    sales_outlet_id INT PRIMARY KEY,
    sales_outlet_type VARCHAR(50),
    address VARCHAR(100),
    city VARCHAR(50),
    telephone VARCHAR(20),
    postal_code VARCHAR(10),
    manager INT,
    FOREIGN KEY (manager) REFERENCES staff(staff_id)
);

-- Table: customer
CREATE TABLE customer (
    customer_id INT PRIMARY KEY,
    customer_key VARCHAR(100), -- Assuming this is unique or important identifier
    customer_email VARCHAR(100),
    customer_since DATE,
    customer_card_number VARCHAR(20),
    birthdate DATE,
    gender VARCHAR(10)
);

-- Table: product
CREATE TABLE product (
    product_id INT PRIMARY KEY,
    product_category VARCHAR(50),
    product_type VARCHAR(50),
    product_name VARCHAR(100),
    description TEXT,
    price DECIMAL(10, 2)
);

-- Table: sales_transaction
CREATE TABLE sales_transaction (
    transaction_id INT PRIMARY KEY,
    transaction_date DATE,
    transaction_time TIME,
    sales_outlet_id INT,
    staff_id INT,
    customer_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2), -- This 'price' seems to be the price at the time of transaction, distinct from product.price
    FOREIGN KEY (sales_outlet_id) REFERENCES sales_outlet(sales_outlet_id),
    FOREIGN KEY (staff_id) REFERENCES staff(staff_id),
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
    FOREIGN KEY (product_id) REFERENCES product(product_id)
);
