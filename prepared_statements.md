# Using data that can change in a sql query
Each time a page is requested, it can use different values in the SQL query to get different data from the database. In such cases, the SQL query must be **prepared** first, then **executed**.

## Step 1: Prepare
SQL statements use placeholders to represent values that can change each time the SQL statement is run. A SQL placeholder acts like a variable, but its name starts with a colon **:** , not a $ symbol.

When a SQL query contains a placeholder, instead of calling the PDO object's **query(**) method to run the query, the PDO object's **prepare()** method is called.

The prepare() method also returns a PDOStatement object but, at this point, the PDOStatement object just represents the SQL statement (not the result set).
## Step 2: Execute
Next, the SQL statement is executed by calling the PDOStatement object's **execute()** method. It requires one argument: an array holding the values that should be used to replace the placeholder.

The placeholder's name and the value to use can be supplied as an associative array, where the:

- **key** is the placeholder name in the SQL query (it can have a colon before it, but it is not required)
- **value** is the value used to replace the placeholder (the value is often already stored in a variable)

```php                                
                                                    //placeholder
$sql = "SELECT forename, surname FROM member WHERE id = :id;"
$statement = $pdo->prepare($sql);
                        //passing the actual value
$statement->execute(['id'] => $id);
```
The SQL query above has a placeholder called :id. The execute() method replaces: id with the value stored in the $id variable. Programmers call this a **prepared statement**.

NEVER add values from a query string or form string to create a SQL statement. This exposes your site to a hack known as a SQL injection attack. Prepared statements stop this risk.

### Don't do:
```php
$sql = 'SELECT forename, surname FROM member WHERE id=' . $id;
$sql = 'SELECT forename, surname FROM member WHERE id=' . $_GET['id'];
```

