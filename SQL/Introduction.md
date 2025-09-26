# Database Management Systems (DBMS)

## Topics

  -   [Fundamental Concepts](./Introduction.md#-fundamental-concepts)
  -   [Evolution of DBMS](./Introduction.md#️-evolution-of-dbms)
  -   [File-Based Systems](./Introduction.md#-file-based-systems)
  -   [Relational DBMS (RDBMS)](./Introduction.md#-relational-dbms-rdbms)
  -   [NoSQL Databases](./Introduction.md#-nosql-databases)
  -   [User Administration](./Introduction.md#-user-administration)
  -   [Advantages of DBMS](./Introduction.md#advantages-of-dbms)

## 📖 Fundamental Concepts

* **Data:** A collection of raw facts (characters, quantities like `int`, `float`, `double`, and symbols).
* **Database:** An organized collection of data that can be easily accessed, managed, and updated. It is structured to allow efficient storage, retrieval, and manipulation of information, typically using tables, fields, and records.
* **DBMS:** A collection of software (S/W) that provides a quick way to access and modify data. This S/W is used to manage the database.
    * **Examples:** Oracle, MySQL

---

## 🕰️ Evolution of DBMS

The evolution of database systems can be categorized into three main types:

1.  **File-Based Systems**
2.  **Relational DBMS (RDBMS)**
3.  **NoSQL Databases**

---

## 📂 File-Based Systems

In a file-based system, users must write custom code to handle all data access and modification.

<img width="405" height="288" alt="file based" src="https://github.com/user-attachments/assets/c73f882f-7e82-4ad0-90c5-4ebd540d4a05" />

* **Issues with File-Based Systems:**
    * **Redundancy:** Data is often duplicated.
    * **Security:** Lacks centralized security controls.
    * **Consistency:** Difficult to maintain consistent data across multiple files.
    * **Concurrency:** Multiple users can't easily access the same data simultaneously.
    * **Difficult Data Access:** Requires specific programming for each task.
    * **No Backup & Recovery:** Lacks built-in mechanisms for data backup and recovery.

---

## 💾 Relational DBMS (RDBMS)

<img width="743" height="292" alt="rdbms" src="https://github.com/user-attachments/assets/dd911ee0-27b2-4d27-af2d-4afafb9dbade" />

A database is called a **Relational Database** if it stores data in the form of tables, which contain rows and columns. It's a software system that provides **SQL** (Structured Query Language) and solves the issues found in file-based systems.

* **Key Characteristics:**
    * Data is stored in tables with rows and columns.
    * It provides library functions that make data management easy.
    * It provides SQL for data manipulation.
    * It focuses on enforcing business logic and data integrity.
    * **Schema:** Defines the overall design of a database and specifies what data should be in each column. In RDBMS, every table has a schema that defines how each row should be structured.
    * **Administrative Panel:** Provides an administrative panel for managing user roles and permissions.

* **Problems with RDBMS:**
    * **Scalability:** Can be difficult to scale regularly.
    * **Rigid Structure:** Requires a proper structure, and `NULL` values are used when there is no data to enter in a row.

---

## 🚀 NoSQL Databases

NoSQL databases were developed to address the scalability and structure issues of RDBMS. They are used for handling large, unstructured data.

* **Key Characteristics:**
    * Designed for high scalability.
    * Handles unstructured data efficiently.
    * Data can be stored as documents, key-value pairs, or objects, not just tables.
    * **Examples:** MongoDB, DynamoDB (Amazon), Cassandra

* **Problems with NoSQL:**
    * **No Consistency in Transactions:** It doesn't guarantee that the data a user reads is the absolute latest version.

---

## 👨‍💼 User Administration

User administration within a DBMS involves tasks that help manage users and maintain the health of the system.

* **Helps in:**
    * Registering and monitoring users.
    * Enforcing data security.
    * Monitoring performance.
    * Maintaining data integrity.
    * Dealing with concurrency control.
    * Recovering information corrupted by unexpected failures.

---

## Advantages of DBMS

* minimized redundancy and data consistency
* simplified data access
* multiple data views
* Data security
* Concurrent access to data
* Backup and recovery mechanism

---