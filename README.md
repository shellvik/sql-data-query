# SQL - Structured Query Language
- Notes.
- Resouces.
- Leetcode SQL 50 solutions.
## Repository Structure
```bash
sql-data-query
├── leetcode-sql-50
│   └── README.md
├── README.md
├── resources
│   └── DBMS_Full_Notes.pdf
└── src
    ├── dvdrental.tar
    └── sql-cheat-sheet.png
```
# PostgresSQL Environment Setup
## Command Line Approach
- OS: Ubuntu Linux.
- Install PostgreSQL
```bash
sudo apt install postgresql
```
- Check status and version:
```bash
/etc/init.d/postgresql status && psql --version
```
- Restarting PostgreSQL with service commnand:
```bash
sudo service postgresql restart
```
- Alternatively restarting PostgreSQL with pg_ctl command:
```bash
sudo ln -s /usr/lib/postgresql/$(psql --version | cut -d" " -f 3 | cut -d"." -f1)/bin/pg_ctl /usr/bin/pg_ctl

sudo -u postgres pg_ctl restart -D /var/lib/postgresql/$(psql --version | cut -d" " -f 3 | cut -d"." -f1)/main
```
- Restore example database for practice:
- Downlaod [dvdrental.tar](src/dvdrental.tar)
#### Create a new empty `dvdrental` database:
```bash
psql -U postgres
```
 - psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  Peer authentication failed for user "postgres"
 - To fix the above error, need to enable peer auth.
```bash
sudo vim /etc/postgresql/$(psql --version | cut -d" " -f 3 | cut -d"." -f1)/main/pg_hba.conf
```
- In the above file change the line:  
`local   all   postgres   peer` -> `local   all   postgres   md5`
- Restart service
```bash
sudo systemctl restart postgresql
```
- Create a password for user postgres:
```bash
sudo -i -u postgres
psql -c "ALTER USER postgres WITH PASSWORD 'pgpass123';"
```
- Now log in with:
```bash
sudo psql -U postgres -W
```
- Create an empty database named `dvdrental`:
```sql
create database dvdrental;
```
- Exit and restore the dvdrental database form backup file using `pg_restore`:
```bash
pg_restore -U postgres -d dvdrental /path/to/dvdrental.tar
```
- **Connect to `dvdrental` database**:
```bash
psql -U postgres -d dvdrental
```
- *List available commands in psql prompt:*
```psql
\?
```
- *List tables:*
```psql
\dt
```
## GUI Approach
- Downlaoad DBeaver Community(Debian package):
[Download Link](https://dbeaver.io/download/2/)
- Install DBeaver Community:
```bash
sudo dpkg -i dbeaver-ce_<version>_amd64.deb && dbeaver
```
- Create a database: `Ctrl+Shift+N` -> PostgrSQL -> Driver Properties(Install drivers) -> Finish.
- Restore database tar file: postgres-> Databases -> postgres -> tools -> restore.

# SQL Fundamantals
## Cheat Sheet
![sql-cs](src/sql-cheat-sheet.png)
## SELECT Statement
- `SELECT`  is the most common statement used, and it allows us to retrieve information form a table.
- `SELECT` statement general syntax:
```psql
SELECT column_name FROM table_name;
```
- In order to select multiple columns, use `,` in between column names:
```psql
SELECT col1,col2,col3 FROM table_name;
```
- Select every column form table:
```psql
SELECT * FROM table_name;
```
- In general it is not a good practice to use an astrisk(`*`) in SELECT statement if you don't really need all the columns.
    - Why? It will automatically query everything, which will increase the traffic between the database server and the application, which can slow down the retrieval of results.
- SQL is not case-sensitive, but capitalizing keywords can enhance readability.


