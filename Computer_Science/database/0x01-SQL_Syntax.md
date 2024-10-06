1. <span style="color:#00b050">Connecting to database</span>
	- `mysql -u username -p`

> [!NOTE]
> 	- Enter the command above to connect to a MySQL database. You'll be prompted to enter your password.

2. <span style="color:#00b050"> Basic SQL Commands</span>
	- Database Operations
		- **<span style="color:#00b0f0">Show Databases:</span>**
			`SHOW DATABASES;`
		- <span style="color:#00b0f0">Create a New Database:</span>
			- `CREATE DATABASE database_name;`
		- <span style="color:#00b0f0">Select a Database to Use:</span>
			- `USE database_name;`
		- <span style="color:#00b0f0">Drop (Delete) a Database:</span>
			- `DROP DATABASE database_name;`
	- Table Operations
		- <span style="color:#00b0f0">Show Tables in a Database:</span>
			- `SHOW TABLES;`
		- Create a New Table:
```sql
		CREATE TABLE table_name (column1 datatype constraints,column2 datatype      constraints,);
```

	- **Drop (Delete) a Table:**
    
    sql
    
    Copy code
    
    `DROP TABLE table_name;`
    
- **Describe Table Structure:**
    
    sql
    
    Copy code
    
    `DESCRIBE table_name;`
    

#### **Data Operations**

- **Insert Data into a Table:**
    
    sql
    
    Copy code
    
    `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`
    
- **Select Data from a Table:**
    
    sql
    
    Copy code
    
    `SELECT column1, column2, ... FROM table_name WHERE condition;`
    
    _To select all columns:_
    
    sql
    
    Copy code
    
    `SELECT * FROM table_name;`
    
- **Update Existing Data in a Table:**
    
    sql
    
    Copy code
    
    `UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;`
    
- **Delete Data from a Table:**
    
    sql
    
    Copy code
    
    `DELETE FROM table_name WHERE condition;`
    

#### **Table Modification**

- **Add a New Column to a Table:**
    
    sql
    
    Copy code
    
    `ALTER TABLE table_name ADD column_name datatype constraints;`
    
- **Modify an Existing Column:**
    
    sql
    
    Copy code
    
    `ALTER TABLE table_name MODIFY column_name new_datatype constraints;`
    
- **Drop a Column from a Table:**
    
    sql
    
    Copy code
    
    `ALTER TABLE table_name DROP COLUMN column_name;`
    

---

### **3. Indexes and Keys**

- **Create an Index on a Table:**
    
    sql
    
    Copy code
    
    `CREATE INDEX index_name ON table_name (column_name);`
    
- **Create a Primary Key:**
    
    sql
    
    Copy code
    
    `ALTER TABLE table_name ADD PRIMARY KEY (column_name);`
    
- **Create a Foreign Key:**
    
    sql
    
    Copy code
    
    `ALTER TABLE table_name ADD CONSTRAINT fk_name FOREIGN KEY (column_name) REFERENCES other_table (other_column);`
    

---

### **4. Data Retrieval and Filtering**

- **Use WHERE Clause to Filter Results:**
    
    sql
    
    Copy code
    
    `SELECT column1, column2 FROM table_name WHERE condition;`
    
- **Order Results:**
    
    sql
    
    Copy code
    
    `SELECT column1, column2 FROM table_name ORDER BY column1 [ASC|DESC];`
    
- **Limit Number of Results:**
    
    sql
    
    Copy code
    
    `SELECT column1, column2 FROM table_name LIMIT number;`
    
- **Aggregate Functions:**
    
    sql
    
    Copy code
    
    `SELECT COUNT(*) FROM table_name;  SELECT AVG(column_name) FROM table_name;  SELECT SUM(column_name) FROM table_name;  SELECT MAX(column_name) FROM table_name;  SELECT MIN(column_name) FROM table_name;`
    

---

### **5. Advanced Queries**

- **Join Tables:**
    
    sql
    
    Copy code
    
    `SELECT column1, column2 FROM table1 INNER JOIN table2 ON table1.common_column = table2.common_column;`
    
- **Group Results:**
    
    sql
    
    Copy code
    
    `SELECT column1, COUNT(*) FROM table_name GROUP BY column1;`
    
- **Having Clause (for aggregated data):**
    
    sql
    
    Copy code
    
    `SELECT column1, COUNT(*) FROM table_name GROUP BY column1 HAVING COUNT(*) > 1;`
    

---

### **6. Transactions**

- **Begin a Transaction:**
    
    sql
    
    Copy code
    
    `START TRANSACTION;`
    
- **Commit a Transaction:**
    
    sql
    
    Copy code
    
    `COMMIT;`
    
- **Rollback a Transaction:**
    
    sql
    
    Copy code
    
    `ROLLBACK;`
