# postgreSQL-assignment-3

# Vehicle Rental Database – SQL Project

## 📌 Overview
This project represents a **Vehicle Rental Management System** database built using PostgreSQL.  
It works with three main tables:

- **users** — stores customer & admin details  
- **vehicles** — stores vehicle information  
- **bookings** — stores rental booking records  

This project demonstrates:
- JOIN operations  
- Filtering using WHERE  
- Checking existence using NOT EXISTS  
- Aggregation using GROUP BY + HAVING  

---

## 📂 Database Tables

### 🧍‍♂️ Users Table
Stores customer/admin information.

| Column  | Type |
|--------|------|
| user_id | SERIAL (PK) |
| name | VARCHAR |
| email | VARCHAR |
| phone | VARCHAR |
| role | VARCHAR |

---

### 🚗 Vehicles Table
Stores vehicle details.

| Column | Type |
|--------|------|
| vehicle_id | SERIAL (PK) |
| name | VARCHAR |
| type | VARCHAR |
| model | INT |
| registration_number | VARCHAR |
| rental_price | NUMERIC |
| status | VARCHAR |

---

### 📑 Bookings Table
Stores customer booking details.

| Column | Type |
|--------|------|
| booking_id | SERIAL (PK) |
| user_id | INT (FK) |
| vehicle_id | INT (FK) |
| start_date | DATE |
| end_date | DATE |
| status | VARCHAR |
| total_cost | NUMERIC |

---

## 📌 SQL Queries

All required project queries are provided below in a single SQL file format.

```sql
-- Query 1: JOIN
-- Retrieve booking information with customer name and vehicle name
SELECT
  b.booking_id,
  u.name AS customer_name,
  v.name AS vehicle_name,
  b.start_date,
  b.end_date,
  b.status
FROM bookings b
INNER JOIN users u ON b.user_id = u.user_id
INNER JOIN vehicles v ON b.vehicle_id = v.vehicle_id;


-- Query 2: EXISTS
-- Find vehicles that have never been booked
SELECT
  *
FROM vehicles v
WHERE NOT EXISTS (
  SELECT 1
  FROM bookings b
  WHERE b.vehicle_id = v.vehicle_id
);


-- Query 3: WHERE
-- Retrieve all available vehicles of type 'car'
SELECT
  *
FROM vehicles
WHERE type = 'car'
AND status = 'available';


-- Query 4: GROUP BY + HAVING
-- Find vehicles with more than 2 bookings
SELECT
  v.name AS vehicle_name,
  COUNT(*) AS total_bookings
FROM bookings b
INNER JOIN vehicles v
ON b.vehicle_id = v.vehicle_id
GROUP BY v.vehicle_id, v.name
HAVING COUNT(*) > 2;
```
