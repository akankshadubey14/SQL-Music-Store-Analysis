
# 🎵 Music Store Database Project  

## 📌 Overview  
The **Music Store Database** is designed to manage and analyze sales data of a music store. The project involves database creation, data insertion, and running SQL queries to extract meaningful insights. This dataset contains information about **customers, invoices, artists, albums, tracks, genres, and employees**.  

The goal of this project is to **analyze business performance** by extracting insights such as:  
✔ Best-selling tracks, albums, and genres  
✔ Customer purchasing behavior and trends  
✔ Monthly and yearly revenue analysis  
✔ Employee sales performance  

## 🚀 Features  
- **Database Schema Creation & Population**  
- **SQL Queries for Business Intelligence**  
- **Data Analysis on Sales Trends**  
- **Optimization of Queries for Performance Enhancement**  

## 🛠️ Tech Stack  
| Technology  | Description |
|------------|-------------|
| **SQL** (MySQL / PostgreSQL) | For database management & querying |
| **PL/SQL** | Advanced queries and stored procedures |
| **Power BI / Tableau (Optional)** | Data visualization for insights |

## 📂 Project Structure  
```
📦 Music_Store_Database
 ┣ 📜 Music_Store_database.sql      # SQL script to create and populate the database
 ┣ 📜 Music_Store_Query.sql         # SQL queries for analysis and insights
 ┣ 📜 README.md                     # Project documentation
```

## 📊 Database Schema  
The database consists of multiple tables. Below are the primary tables and their key columns:  

### **1. Customers** (`customer_id`, `first_name`, `last_name`, `email`, `city`, `state`, `country`)  
- Stores customer details, including location and contact information.  

### **2. Invoices** (`invoice_id`, `customer_id`, `invoice_date`, `total`)  
- Contains customer purchase transactions.  

### **3. Invoice_Items** (`invoice_item_id`, `invoice_id`, `track_id`, `unit_price`, `quantity`)  
- Tracks the individual items purchased in each invoice.  

### **4. Tracks** (`track_id`, `name`, `album_id`, `genre_id`, `composer`, `milliseconds`, `unit_price`)  
- Stores information about individual music tracks.  

### **5. Albums** (`album_id`, `title`, `artist_id`)  
- Represents music albums and their respective artists.  

### **6. Artists** (`artist_id`, `name`)  
- Contains artist names associated with albums.  

### **7. Genres** (`genre_id`, `name`)  
- Stores different music genres (e.g., Rock, Jazz, Pop, Classical).  

### **8. Employees** (`employee_id`, `first_name`, `last_name`, `title`, `reports_to`)  
- Manages store employees and their reporting hierarchy.  

## 🔍 Key Analyses & Queries  

Here are some **important SQL queries** included in the project:  

### 📈 **1. Sales Analysis**  
#### 🔹 Find the **Total Revenue** of the Store  
```sql
SELECT SUM(total) AS total_revenue 
FROM invoices;
```

#### 🔹 Find the **Monthly Sales Trend**  
```sql
SELECT 
    strftime('%Y-%m', invoice_date) AS month, 
    SUM(total) AS monthly_revenue
FROM invoices
GROUP BY month
ORDER BY month;
```

### 🏆 **2. Best-Selling Tracks & Genres**  
#### 🔹 Top 5 Best-Selling Tracks  
```sql
SELECT t.name, COUNT(ii.track_id) AS total_sold
FROM invoice_items ii
JOIN tracks t ON ii.track_id = t.track_id
GROUP BY ii.track_id
ORDER BY total_sold DESC
LIMIT 5;
```

#### 🔹 Most Popular Music Genre  
```sql
SELECT g.name AS genre, COUNT(ii.invoice_item_id) AS total_sold
FROM invoice_items ii
JOIN tracks t ON ii.track_id = t.track_id
JOIN genres g ON t.genre_id = g.genre_id
GROUP BY g.genre_id
ORDER BY total_sold DESC
LIMIT 1;
```

### 🛍️ **3. Customer Purchase Behavior**  
#### 🔹 Top 5 Customers by Total Spending  
```sql
SELECT c.first_name, c.last_name, SUM(i.total) AS total_spent
FROM customers c
JOIN invoices i ON c.customer_id = i.customer_id
GROUP BY c.customer_id
ORDER BY total_spent DESC
LIMIT 5;
```

### 🏢 **4. Employee Performance**  
#### 🔹 Sales Performance of Each Employee  
```sql
SELECT e.first_name, e.last_name, COUNT(i.invoice_id) AS total_sales
FROM employees e
JOIN customers c ON e.employee_id = c.support_rep_id
JOIN invoices i ON c.customer_id = i.customer_id
GROUP BY e.employee_id
ORDER BY total_sales DESC;
```

## 🔧 Setup Instructions  
Follow these steps to set up the database and run queries:  

### **Step 1: Install SQL Database**  
- If using **MySQL**, download it from [MySQL Official Website](https://dev.mysql.com/downloads/).  
- If using **PostgreSQL**, download from [PostgreSQL Official Site](https://www.postgresql.org/download/).  

### **Step 2: Import the Database**  
- Open your database tool (MySQL Workbench / pgAdmin / SQLite Browser).  
- Run the script **`Music_Store_database.sql`** to create the database and insert data.  

### **Step 3: Run Queries**  
- Open the **`Music_Store_Query.sql`** file and execute queries for analysis.  

## 🎯 Insights & Takeaways  
🔸 The **Rock** genre generates the highest revenue.  
🔸 The **top-selling artist** is *[Artist Name]* (based on invoice data).  
🔸 Customers from *[City Name]* spend the most per transaction.  
🔸 The **best-performing employee** in terms of sales is *[Employee Name]*.  

## 📜 License  
This project is intended for educational purposes. You are free to modify and use it as needed.  



---
