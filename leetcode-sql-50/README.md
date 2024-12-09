# Leetcode SQL 50 Solutions
![LC](/src/lc-sql-50.png)
## [Problem List](https://leetcode.com/studyplan/top-sql-50/)
**SELECT**
1. [Recycleable and Low Fat Product](#recycleable-and-low-fat-product)
2. [Find Customer Referee](#find-customer-referee)
3. [Big Countries](#big-countries)
4. [Article View 1](#article-view-1)
5. [Invalid Tweets](#invalid-tweets)

**Basic Joins**

6. [Replace Employee ID With The Unique Identifyer](#replace-employee-id-with-the-unique-identifyer)
7. [Product Sales Analysis 1](#product-sales-analysis-1)
8. [Customer Who Visited but Did Not Make Any Transaction](#customer-who-visited-but-did-not-make-any-transaction)
9. [Average Time of Process per Machine](#average-time-of-process-per-machine)

> I'll add new things I'm learning while solving the problem as a note here that was not in the Main note section.

### Recycleable and Low Fat Product
```sql
SELECT product_id FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```
### Find Customer Referee
```sql
SELECT name FROM Customer
WHERE
referee_id != 2
OR referee_id is null;
```
### Big Countries
```sql
SELECT name, population, area FROM World
WHERE 
area >= 3000000 OR population >= 25000000;
```

### Article View 1
```sql
SELECT DISTINCT author_id AS id from Views 
WHERE author_id = viewer_id; 
```
### Invalid Tweets
- The `LENGTH()` function is used to count number of characters in a string including white spaces.
```sql
SELECT tweet_id FROM Tweets
WHERE length(content) > 15;
```
### Replace Employee ID With The Unique Identifyer
```sql
SELECT unique_id, name FROM Employees
LEFT OUTER JOIN EmployeeUNI
ON Employees.id = EmployeeUNI.id
ORDER BY name;
```
### Product Sales Analysis 1
```sql
SELECT product_name, year, price FROM Sales
FULL OUTER JOIN Product
ON Sales.product_id = Product.product_id
WHERE Sales.sale_id IS not null;
```
### Customer Who Visited but Did Not Make Any Transaction
```sql
SELECT customer_id, COUNT(customer_id) as count_no_trans FROM Visits
LEFT OUTER JOIN Transactions
ON Transactions.visit_id = Visits.visit_id
WHERE Transactions.visit_id is null
GROUP BY customer_id;
```
### Raising Temperature
- Using self join:
```sql
SELECT w1.id FROM Weather w1
JOIN Weather w2
ON w1.recordDate = w2.recordDate + 1
WHERE w1.temperature > w2.temperature;
```
- Using [Cross Join](https://learn.microsoft.com/en-us/power-query/cross-join):
```sql
SELECT today.id 
FROM Weather yesterday
CROSS JOIN Weather today
WHERE today.recorddate - yesterday.recorddate = 1
AND today.temperature > yesterday.temperature;
```

### Average Time of Process per Machine 
- This rounding needs typecasting, else it's screaming error.
```sql
SELECT s.machine_id, ROUND(AVG(e.timestamp - s.timestamp)::NUMERIC,3) AS processing_time
FROM Activity AS s JOIN Activity AS e
ON s.machine_id = e.machine_id
AND s.process_id = e.process_id
AND s.activity_type = 'start'
AND e.activity_type = 'end'
GROUP BY s.machine_id;
```