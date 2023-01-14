# Awesome-SQL


These 75+ queries will help to learn sql.

---

- Oracle 
- MySQL 
- SQL Server 
- PostgreSQL 
- SQLite


---

 - Table
   - Create a Table with a few fields by specifying their data types.
    ``` sql
      CREATE TABLE user (
        user_id INT PRIMARY KEY,
        first_name VARCHAR(255),
        last_name VARCHAR(255),
        email VARCHAR(255) UNIQUE,
        password VARCHAR(255),
        date_created DATETIME
      );
    ```
   - Add a field to an existing table.
    ```sql
      ALTER TABLE user ADD gender VARCHAR(25);
   ```
   - Modify a field's data type of a table.
    ```sql
      ALTER TABLE user MODIFY COLUMN date_created VARCHAR(255);
    ```
   - Rename a field's name.
    ```sql
      ALTER TABLE user RENAME COLUMN email TO email_id;
    ```
   - Remove a field from a table.
    ```sql
      ALTER TABLE user DROP COLUMN gender;
    ```
   - Rename a table's name.
    ```sql
      ALTER TABLE user RENAME TO user_detail;
    ```
   - Drop a table.
    ```sql
      DROP TABLE user_detail;
    ```

 - Constraints 
   - Primary Key
     - Create a Table with
       - a single field as the primary key
       - 2 or, more fields as the primary key 

      ``` sql
        CREATE TABLE one_primary_key (user_id INT PRIMARY KEY,
          first_name VARCHAR(255),
          last_name VARCHAR(255)
        );
        
        CREATE TABLE two_primary_keys (id int,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          CONSTRAINT PK_primary_keys PRIMARY KEY (id, first_name)
        );
      ```

     - Add a primary key to an existing table
       - for a single field
       - for 2 or, more fields 
      ``` sql
        CREATE TABLE no_primary_key (id INT,
          first_name VARCHAR(255),
          last_name VARCHAR(255)
        );
        
        ALTER TABLE no_primary_key ADD PRIMARY KEY (id);

        ALTER TABLE no_primary_key ADD CONSTRAINT PK_primary_keys PRIMARY KEY (id, first_name);
      ```
   - Unique
     - Create a Table with 
       - a single field unique 
       - 2 or, more fields combining unique 
       - multiple unique fields
      ``` sql
        CREATE TABLE one_unique (
          id INT,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          email VARCHAR(255) UNIQUE
        );

        CREATE TABLE two_unique (id int,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          CONSTRAINT UQ_two_unique UNIQUE (first_name, last_name)
        );
      ```
           
     - Add a unique constraint to an existing table 
       - for a single field 
       - for 2 or, more fields combining 
     - Drop a unique constraint
      ``` sql
        CREATE TABLE no_unique (id INT,
          first_name VARCHAR(255),
          last_name VARCHAR(255)
        );

        ALTER TABLE no_unique ADD UNIQUE (id);
        ALTER TABLE no_unique DROP INDEX id;

        ALTER TABLE no_unique ADD CONSTRAINT UQ_no_unique UNIQUE (id, first_name);
        ALTER TABLE no_unique DROP INDEX UQ_no_unique;
      ```

   - Not Null
      - Create a Table with 
        - one NOT NULL field 
        - multiple NOT NULL fields 
        - Add NOT NULL constraint to an existing field 
        - Remove NOT NULL constraint from an existing field
      ``` sql
        CREATE TABLE one_not_null (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255)
        );

        CREATE TABLE two_not_null (id INT NOT NULL,
          first_name VARCHAR(255) NOT NULL,
          last_name VARCHAR(255)
        );

        ALTER TABLE one_not_null MODIFY COLUMN first_name VARCHAR(255) NOT NULL;
        ALTER TABLE two_not_null MODIFY COLUMN first_name VARCHAR(255);
      ```

   - Default 
     - Create a Table with DEFAULT value(s)
       - for one field 
       - multiple fields 
       - Add a DEFAULT value constraint to an existing field 
       - Remove DEFAULT value constraint from an existing field
      ``` sql
        CREATE TABLE one_default (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          gender VARCHAR(255) DEFAULT 'unknown'
        );

        CREATE TABLE two_default (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          gender VARCHAR(255) DEFAULT 'unknown',
          bio VARCHAR(255) DEFAULT '...'
        );

        ALTER TABLE one_default ALTER first_name SET DEFAULT 'Goodie';
        ALTER TABLE one_default ALTER first_name DROP DEFAULT;
      ```

   - Check 
     - Create a Table with CHECK constraint for 
       - a single field 
       - 2 or, more fields combining 
       - multiple separated fields
        ``` sql
        CREATE TABLE one_check (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          age int CHECK (age>=18)
        );

        CREATE TABLE combined_check (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          age int, 
          cgpa DOUBLE,
          CONSTRAINT CHK_combined_check CHECK (age>=18 and cgpa>=7.5)
        );

        CREATE TABLE two_check (id INT NOT NULL,
          first_name VARCHAR(255),
          last_name VARCHAR(255),
          age int CHECK (age>=18),
          cgpa DOUBLE CHECK (cgpa>=7.5)
        );
        ```

      - Add a CHECK constraint to an existing table
          - a single field 
          - 2 or, more fields combining
          ``` sql
          CREATE TABLE one_check (id INT NOT NULL,
            first_name VARCHAR(255),
            last_name VARCHAR(255),
            age int,
            cgpa DOUBLE
          );

          ALTER TABLE one_check ADD CHECK (age>=18);
          ALTER TABLE one_check ADD CONSTRAINT CHK_one_check CHECK (age>=18 AND cgpa>=7.5);
          ```

      -  Drop a  CHECK constraint
          ``` sql

          SHOW CREATE TABLE one_check;
          + -----------
          CREATE TABLE `one_check` (
            `id` int NOT NULL,
            `first_name` varchar(255) DEFAULT NULL,
            `last_name` varchar(255) DEFAULT NULL,
            `age` int DEFAULT NULL,
            CONSTRAINT `one_check_chk_1` CHECK ((`age` >= 18))
          ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
          + -----------
          
          `user the conatra`
          ALTER TABLE one_check DROP CHECK one_check_chk_1;
          ```

   - Foreign Key 
     - Create a Table with 
       - a single foreign key field 
        ``` sql
        CREATE TABLE Persons (
          ID int NOT NULL,
          LastName varchar(255) NOT NULL,
          FirstName varchar(255),
          Age int,
          PRIMARY KEY (ID)
        );

        CREATE TABLE Orders (
          OrderID int NOT NULL,
          OrderNumber int NOT NULL,
          PersonID int,
          PRIMARY KEY (OrderID),
          FOREIGN KEY (PersonID) REFERENCES Persons(ID)
        );
        ```

      - multiple foreign key fields 

        ``` sql
        CREATE TABLE Persons (
          ID int NOT NULL,
          LastName varchar(255) NOT NULL,
          FirstName varchar(255),
          Age int,
          PRIMARY KEY (ID)
        );

        CREATE TABLE Address (
          AddressID int NOT NULL,
          Address_1 varchar(255) NOT NULL,
          Address_2 varchar(255),
          city varchar(255),
          country varchar(255),
          pincode varchar(255),
          PRIMARY KEY (AddressID)
        );

        CREATE TABLE Orders (
          OrderID int NOT NULL,
          OrderNumber int NOT NULL,
          PersonID int,
          AddressID int,
          PRIMARY KEY (OrderID),
          FOREIGN KEY (PersonID) REFERENCES Persons(ID),
          FOREIGN KEY (AddressID) REFERENCES Address(AddressID)
        );
        ```

     - Add a foreign key constraint to existing table 
       - a single field
        ``` sql
        CREATE TABLE Persons (
          ID int NOT NULL,
          LastName varchar(255) NOT NULL,
          FirstName varchar(255),
          Age int,
          PRIMARY KEY (ID)
        );

        CREATE TABLE Orders (
            OrderID int NOT NULL,
            OrderNumber int NOT NULL,
            PersonID int,
            PRIMARY KEY (OrderID)
        );

        ALTER TABLE Orders ADD FOREIGN KEY (PersonID) REFERENCES Persons(ID);
        ```

     - Drop a foreign key
        ``` sql
        ALTER TABLE Orders DROP CONSTRAINT orders_ibfk_1;
        ```
        

 - Insert, Update, Delete
   - Insert a row into a table. 
   - Insert a row into a table by providing data for a few fields. 
   - Insert multiple rows at a time into a table. 
   - Insert into a table by selecting needed data from another table.
   - Update a specific field's data in a table.
   - Update a field's data for multiple rows at a time.
   - Delete a row from a table.
   - Delete multiple rows from a table.

 - Select
   - Fetch all rows from a table.
   - Fetch only specific fields' data from a table.
   - Fetch only those rows that match a condition.
   - Apply multiple conditions.
   - Check if a field's data is NULL.
   - Check if a field's data is not NULL.
   - Check if a field's data starts with "NewY"
   - Check if a field's data ends with "don"
   - Check if a field's data contains "ijin"
   - Check if a field's data has "a" at 2nd position 
   - Check if a field's data starts with "B" and, has at least 5 characters.
   - Check if a field's data starts with "B" and, ends with "a".
   - Check if a field's data starts with "a" or, "o".
   - Check if a field's data doesn't contain "a" or, "o" at the 2nd position.
   - Check if a field's data ends with any character from "m" to "t".
   - Check if a field's data is 1 or, 2 or, 3 or, 4 or, 5.
   - Check if a field's data is in the range of 10 to 30.
   - Check if a field's data is not in the range of 10 to 50.
   - Fetch only distinct data contained in a field.
   - Fetch only the first 10 rows.
   - Fetch rows from 21 to 40.
   - Find the minimum value of a field.
   - Find the maximum value of a field.
   - Find the average value of a field.
   - Find the sum of all values contained in a field.

# References

- (Swapna Kumar) - https://twitter.com/swapnakpanda/status/1554435629886218240
- (W3 Schools) - https://www.w3schools.com/sql/