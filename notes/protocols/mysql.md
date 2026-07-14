# Tool 

# Connecting 


```bash
mysql -u root -p

```

```bash
mysql -u user -ppass

```

```bash
mysql -u user -h remote.host.htb -P 3306 -p 

```


```bash 
mysql -u user -h remote.host.htb -P 3306 -p --ssl=DISABLE
```

# Enumeration 

## External
```
nuclei -u http://url -tag mysql 

sudo nmap -sV -sC 3306 
```

## Internal 

### Table Manipulation
```mysql
INSERT INTO table_name VALUES (column1_value, column2_value, column3_value); 
```
```mysql
INSERT INTO logins VALUES(1, 'admin', 'p@ssw0rd', '2020-07-02');
```



```mysql
ALTER TABLE logins ADD newcolumn INT: 
```
```
ALTER TABLE logins MODIFY newerColumn DATE;

```



```mysql
UPDATE logins SET password = 'change_password' WHERE id > 1;
```

### ***Database Version***

```sql
SELECT @@version
```

```sql
SELECT POW(1,1)
```


```sql
SELECT SLEEP(5) 
```

### ***Table Selection***

```mysql
SELECT * FROM table_name; *

```

```mysql
SELECT * FROM logins ORDER BY password;
```

```mysql
SELECT * FROM logins ORDER BY password DESC, id ASC;

```


**Limiting Results**

```
SELECT * FROM logins LIMIT 2;
```
```
SELECT * FROM logins LIMIT 1, 2;
```

**Where Results**

```
SELECT * FROM table_name WHERE <condition>;
```

```
SELECT * FROM logins WHERE id > 1;
```

```
SELECT * FROM logins where username = 'admin'
```

**Like**

```
SELECT * FROM logins WHERE username LIKE 'admin%';
```


```
SELECT * FROM logins WHERE username like '___';
```


```
SELECT * FROM logins WHERE username != 'john' AND id > 1;
```

### Column Selection 

```
SELECT * from information_schema.columns

```

### Other Database Values 

```
UNION select 1, 

```

# Injections
```
** In Band - > Union Based : Must specify exact column we can read to suqery will direct output to be printed there
           - > Error Based : Used when we can get php or sql errors in front end and may intentionally cause error that returns
output of query
** Blind  - > Boolean Based: Can use SQL conditional statements to control whether the page returns any output at all, 'i.e., original query response,' if our conditional statement returns true
          - > Time Based: We use SQL conditional statements that delay the page response if the conditional statement returns true using the Sleep() function.
```

## Logic Suberversion 

### Comments 
- Comments can be added to prevent certain logic from being executed. Anything found after a ``--`` or `##` is not executed 
- Parentheses can also be used to ensure certain conditions are checked before others  
### Union Clause & Injection
- Union clauses combine results from SELECT statements 
- Data types from each column MUST be the same, and the number of columns in each table MUST also match 
`SELECT a, b FROM table1 UNION SELECT c, d FROM table2



```
SELECT * FROM ports UNION SELECT * FROM ships`

ports: table 
ships: another table 
```

**Determining Column Number**

- ORDER BY 
- UNION 
- The last successful column sorted determines what the number of columns are 

**Determining  Where To Place Injection **

```
cn' UNION select 1,@@version,3,4-- -
```



# Exploitations

## Database Enumeration 

## Reading Files

## Writing Files
