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

```