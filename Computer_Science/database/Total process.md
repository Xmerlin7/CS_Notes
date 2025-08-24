```bash
mysql -u root -p
--enter the password
mysql> CREATE DATABASE IF NOT EXISTS quickric;
mysql> CREATE USER IF NOT EXISTS 'quickric_user'@'%' IDENTIFIED BY 'QuickRicK_123!';
mysql> GRANT ALL PRIVILEGES ON quickric.* TO 'quickric_user'@'%';
mysql> FLUSH PRIVILEGES;  -- Refresh privileges
mysql -u quickric_user -p quickric < setup-database.sql
TRUNCATE TABLE SENSORS;


```
![[Pasted image 20241007032425.png]]
```  MYSQL
INSERT INTO SENSORS (bpm, gps, emergency)
VALUES 
(85, '40.7128, -74.0060', stable),
(92, '34.0522, -118.2437', stable),
(78, '51.5074, -0.1278', emergency);

-- updated
UPDATE SENSORS
SET emergency = emergency 
WHERE bpm = 80;

-- delete
DELETE FROM SENSORS
WHERE bpm = 85;

--  filter 
SELECT * FROM SENSORS
WHERE bpm > 90;

-- ORDER
SELECT * FROM SENSORS
ORDER BY bpm DESC;

-- LIMIT
SELECT * FROM SENSORS
LIMIT 5;

-- Count 
SELECT COUNT(*) AS total_rows FROM SENSORS;

-- Min & Max
SELECT MAX(bpm) AS max_bpm FROM SENSORS;

SELECT MIN(bpm) AS min_bpm FROM SENSORS;

-- Group and Average Data
SELECT emergency, AVG(bpm) AS avg_bpm
FROM SENSORS
GROUP BY emergency;

```