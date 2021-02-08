## Database > RDS for SQL Server > Database Instance

Database instance encompasses virtual equipment and installed Microsoft SQL Server, serving as the unit of Microsoft SQL Server provided by RDS for SQL Server. 
Direct access to a database instance is not allowed, but access is enabled only through the port entered when creating the database instance. 
Database instances can be identified by user-specified name or automatically assigned 32-bit ID. 
A database instance must be named, considering the following constraints: 

* Must be unique for each region. 
* Must be comprised of alphabets, numbers, -, _ ,and .only, between 4 and 100 characters.
* Must start with a letter. 

To create a database instance, user account and password setting is required, considering the following constraints: 

* User account must be between 4 and 16 characters, comprised of alphabets and numbers only, starting with a letter. 
* Password must be between 8 and 128, comprised of alphabets, numbers, !, $, #, and % only. 
* Password cannot include user's account name. 
* Password must include at least three categories out of capital letters, small-case letters, numbers, and special characters. 

### Availability Area

RDS for SQL Server has many availability areas under one system so as to prepare against failure in physical hardware. A failure occurred within an availability area does not affect other availability areas, raising availability of the entire service. Database instances that are dispersed and created in different areas can communicate via network, with no charges.   

> [Caution]
> The availability area of already-created database instance cannot be changed. 

### Version of Microsoft SQL Server

Only the SQL Server 2016 Standard version is supported.   

### Database Instance Type

Each type of database instance has different CPU core count and memory volume. 
To create a database instance, an appropriate type must be selected depending on the database workload. 

| Type    | Description |
| ------- | -------------------------------------------------|
| m2 | Configures balance between CPU and memory.   |
| c2 | Has higher performance setting for CPU. |
| r2 | Available when momory takes more volume than other reources|
| x1 | A type that supports high performance CPUs and memory. Used for services and applications that require high performance. |

It is easy to change the type of already-created database instance via web console.

> [Caution]
> Changing already-created database instance type requires minutes of downtime since database instance must be closed. 

### Storage Type

Database instances support two storage types: HDD or SSD. 
Since each storage type provides different performance and pricing, an appropriate storage type must be selected depending on the database workload.  
A storage type can be created from 20GB up to 2,000 GB. 
It is easy to change the size of already-created storage via web console. 

> [Caution]
> Changing already-created storage size requires minutes of downtime since database instance must be closed. 
> The type of already-created storage cannot be changed. 
