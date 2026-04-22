# CUSTOMER BANKING APP : A FULL JOURNEY 

### LAB 1 : EXECUTING BASIC SPRING BOOT APPLICATION

**Description** : Configuring and adding dependencies to create a simple spring boot project with the help of spring initializer(https://start.spring.io)


<img width="1440" height="819" alt="Screenshot 2026-04-22 at 11 26 55 AM" src="https://github.com/user-attachments/assets/4271fd36-6e53-4045-8fa2-104a55a5cd9f" />

</br> 

After generating(for the first one, I just added *Spring web* dependency:

<img width="758" height="167" alt="Screenshot 2026-04-22 at 11 28 48 AM" src="https://github.com/user-attachments/assets/d916ffcb-9e2d-4c35-b2c7-c367d63e207f" />

</br> 

After opening the project in vscode(Already had maven build tool installed in system). Then in terminal I ran `mvn spring-boot:run`. 
</br>
Running in `localhost:8080` ( TOMCAT runs in port 8080), a **whitelabel error page** is encountered. This is because no `@GetMapping` means no method is used to handle any URL, so all requests fail.

<img width="1440" height="819" alt="Screenshot 2026-04-22 at 11 41 04 AM" src="https://github.com/user-attachments/assets/73838dbb-f8bd-401b-bf46-75b2d0a473a3" />

</br>
Adding a controller class to show an actual message:

```java
/*Class name : Hello.java */


package com.firstproject.myFirstproject;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class Hello {

    @GetMapping("/blah")
        public String hello(){
            return "Hello! I am Srinidhi";
        }
    
}
```

<img width="1440" height="900" alt="Screenshot 2026-04-22 at 11 47 00 AM" src="https://github.com/user-attachments/assets/ebcf4575-5796-4f01-9938-23dd2db7377b" />
</br>
Testing in POSTMAN:

<img width="1266" height="743" alt="Screenshot 2026-04-22 at 11 58 13 AM" src="https://github.com/user-attachments/assets/f8e1821c-49d2-4fd1-bf9a-06ac5d7d4cc8" />

### LAB 2 & 3 : DATABASE & DATABASE STRUCTURE 

**Description** : Creating ERDs from physical tables using MySQL Workbench. 

```sql
>mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 19
Server version: 9.4.0 Homebrew

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database 2_primary_database;
Query OK, 1 row affected (0.009 sec)

mysql> use 2_primary_database;
Database changed
mysql> CREATE TABLE customer_classification (
    ->   cstcl_id BIGINT PRIMARY KEY,
    ->   cstcl_type VARCHAR(100),
    ->   cstcl_type_value VARCHAR(100),
    ->   cstcl_effective_date DATE,
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36)
    -> );
Query OK, 0 rows affected (0.017 sec)

mysql> CREATE TABLE customer_details (
    ->   customer_id BIGINT PRIMARY KEY,
    ->   customer_type BIGINT,
    ->   full_name VARCHAR(150),
    ->   dob DATE,
    ->   status VARCHAR(50),
    ->   mobile_number VARCHAR(15),
    ->   email VARCHAR(100),
    ->   country VARCHAR(50),
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36),
    ->   FOREIGN KEY (customer_type) REFERENCES customer_classification(cstcl_id)
    -> );
Query OK, 0 rows affected (0.122 sec)

mysql> CREATE TABLE customer_identification (
    ->   cust_ident_id BIGINT PRIMARY KEY,
    ->   customer_id BIGINT,
    ->   id_type BIGINT,
    ->   id_value VARCHAR(100),
    ->   effective_date DATE,
    ->
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36),
    ->
    ->   FOREIGN KEY (customer_id) REFERENCES customer_details(customer_id),
    ->   FOREIGN KEY (id_type) REFERENCES customer_classification(cstcl_id)
    -> );
Query OK, 0 rows affected (0.018 sec)

mysql> CREATE TABLE customer_name (
    ->   cust_name_id BIGINT PRIMARY KEY,
    ->   customer_id BIGINT,
    ->   name_type BIGINT,
    ->   name_value VARCHAR(100),
    ->   effective_date DATE,
    ->
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36),
    ->
    ->   FOREIGN KEY (customer_id) REFERENCES customer_details(customer_id),
    ->   FOREIGN KEY (name_type) REFERENCES customer_classification(cstcl_id)
    -> );
Query OK, 0 rows affected (0.014 sec)

mysql> CREATE TABLE customer_proof_of_identity (
    ->   cust_proof_id BIGINT PRIMARY KEY,
    ->   customer_id BIGINT,
    ->   proof_type BIGINT,
    ->   proof_value VARCHAR(100),
    ->   start_date DATE,
    ->   end_date DATE,
    ->
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36),
    ->
    ->   FOREIGN KEY (customer_id) REFERENCES customer_details(customer_id),
    ->   FOREIGN KEY (proof_type) REFERENCES customer_classification(cstcl_id)
    -> );
Query OK, 0 rows affected (0.012 sec)

mysql> CREATE TABLE customer_address (
    ->   cust_address_id BIGINT PRIMARY KEY,
    ->   customer_id BIGINT,
    ->   address_type BIGINT,
    ->   address_value VARCHAR(200),
    ->   effective_date DATE,
    ->
    ->   created_by VARCHAR(50),
    ->   created_ts TIMESTAMP,
    ->   updated_ts TIMESTAMP,
    ->   uuid VARCHAR(36),
    ->
    ->   FOREIGN KEY (customer_id) REFERENCES customer_details(customer_id),
    ->   FOREIGN KEY (address_type) REFERENCES customer_classification(cstcl_id)
    -> );
Query OK, 0 rows affected (0.018 sec)

mysql> INSERT INTO customer_classification VALUES
    -> (1, 'CUSTOMER_TYPE', 'INDIVIDUAL', CURDATE(), 'admin', NOW(), NOW(), 'uuid-1'),
    -> (2, 'ID_TYPE', 'AADHAR', CURDATE(), 'admin', NOW(), NOW(), 'uuid-2'),
    -> (3, 'NAME_TYPE', 'FIRST_NAME', CURDATE(), 'admin', NOW(), NOW(), 'uuid-3'),
    -> (4, 'ADDRESS_TYPE', 'HOME', CURDATE(), 'admin', NOW(), NOW(), 'uuid-4');
Query OK, 4 rows affected (0.005 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> INSERT INTO customer_details VALUES
    -> (101, 1, 'Srinidhi', '2005-01-01', 'ACTIVE', '9876543210',
    ->  'mail@gmail.com', 'India', 'admin', NOW(), NOW(), 'uuid-5');
Query OK, 1 row affected (0.003 sec)

mysql> INSERT INTO customer_identification VALUES
    -> (201, 101, 2, '1234-5678-9012', CURDATE(), 'admin', NOW(), NOW(), 'uuid-6');
Query OK, 1 row affected (0.002 sec)

mysql> INSERT INTO customer_name VALUES
    -> (301, 101, 3, 'Srinidhi', CURDATE(), 'admin', NOW(), NOW(), 'uuid-7');
Query OK, 1 row affected (0.003 sec)

mysql> INSERT INTO customer_address VALUES
    -> (401, 101, 4, 'Manipal, Karnataka', CURDATE(), 'admin', NOW(), NOW(), 'uuid-8');
Query OK, 1 row affected (0.003 sec)

mysql> INSERT INTO customer_proof_of_identity VALUES
    -> (501, 101, 2, '1234-5678-9012', '2020-01-01', '2030-01-01',
    ->  'admin', NOW(), NOW(), 'uuid-9');
Query OK, 1 row affected (0.004 sec)
```

<img width="1440" height="900" alt="Screenshot 2026-04-22 at 12 23 17 PM" src="https://github.com/user-attachments/assets/8fe91ef9-4283-4604-b85b-b2a3eae0e641" />

</br>
Add a new diagram

<img width="1440" height="900" alt="Screenshot 2026-04-22 at 12 24 15 PM" src="https://github.com/user-attachments/assets/3ecf5570-5122-4835-939f-c20640501e30" />

</br> Proceed with a few more steps and click on the database you want o reverse engineer:

<img width="894" height="695" alt="Screenshot 2026-04-22 at 12 24 38 PM" src="https://github.com/user-attachments/assets/e2e6a229-9917-4271-b6df-4043cb3cafb3" />

</br> Finish up and you will get the completed LDM(Logical data model) -> This we get by **Reverse engineering**
<img width="495" height="690" alt="Screenshot 2026-04-22 at 12 26 04 PM" src="https://github.com/user-attachments/assets/6a51e8ea-6119-483b-8ae6-8fb043f83fe0" />

Now we also have the possibility of getting the physical tables from LDM using **Forward engineering**

<img width="1439" height="875" alt="Screenshot 2026-04-22 at 12 36 02 PM" src="https://github.com/user-attachments/assets/5e0448e8-25cd-4b1f-a97a-ce68c8e26729" />

<img width="891" height="692" alt="Screenshot 2026-04-22 at 12 36 22 PM" src="https://github.com/user-attachments/assets/31d8e694-ffdc-4c26-afc7-f4a2de6c16fe" />

Some important points:
Audit columns : Used for tracking
</br></br>

* UserID : Who performed the action.
* Workstation/SystemID : IP Address, Device, Channel
* Local Timestamp : When the user started action; recorded in user's device timezone.
* Host Timestamp : When the database recorded the action; recorded in UTC
* Acceptance Timestamp : When the system accepts the request(something like API request); recorded in UTC
* Timezone offset : Helps convert Local TS --> UTC
* System/Module ID : Which module created data
* UUID : Unique ID for entire transaction/process

*Insert-only Paradigm* is where DELETION AND UPDATION never takes place but only INSERTING as new rows happens. This to maintain proper history without losing past information.


### LAB 3 : RestAPI

**Description** : Building my very own RestAPI

After setting up mysql server, we configure a new spring boot project using spring initializr(https://start.spring.io)

<img width="1440" height="817" alt="Screenshot 2026-04-22 at 6 20 36 PM" src="https://github.com/user-attachments/assets/8d39769d-5cad-4364-8b5f-fe0fc65fae6a" />

</br> Once this is downloaded, we configure the *application.properties* file. 

</br>
Layered architecture :

* The presentation layer: It contains all categories related to the presentation layer.
* The business layer: It contains business logic.
* The persistence layer: It’s used for handling functions like object-relational mapping
* The database layer: This is where all the data is stored.

Spring-boot flow architecture:

* Controller layer : Handles incoming API requests
* Service layer : Handles the business logic
* Repository layer : Talks to the database
* Database layer : The layer where data is stored

</br> 

We make 4 packages and 4 java classes(in each package) - entity ,repository ,service , controller.

</br>

One API was built which established a connection between mysql and **Customer Details** table(one of the tables we created, refer LDM)

</br>

Running on localhost:8080/api/users

<img width="1440" height="373" alt="Screenshot 2026-04-22 at 7 39 44 PM" src="https://github.com/user-attachments/assets/02d7d52a-0845-4a4a-bf15-1aa7f43cda0a" />

POST:

<img width="1272" height="791" alt="Screenshot 2026-04-22 at 7 40 44 PM" src="https://github.com/user-attachments/assets/b09a5622-aff8-49b7-b875-26c1f054095c" />

GET:

<img width="1272" height="792" alt="Screenshot 2026-04-22 at 7 41 19 PM" src="https://github.com/user-attachments/assets/b158be7a-a5df-4765-a77f-3d1faa8b06ae" />

The database itself:

<img width="1259" height="208" alt="Screenshot 2026-04-22 at 7 44 09 PM" src="https://github.com/user-attachments/assets/3ec1e12c-43a6-48c9-98ef-6c04e1f9537a" />








































