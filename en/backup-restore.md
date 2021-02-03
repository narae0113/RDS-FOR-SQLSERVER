## Database > RDS for SQL Server > Backup and Restoration

## Backups

It is available to prepare for restoring database of a database instance. RDS for SQL Servers execute backups in the consecutive order.  
Backups can be manually created at a time of choice or automatically created by setting backup retention period. 
Restoration is available to a particular time by using manually created backups, or to a point of time during backup retention period. 

> [Caution]
> While backup is underway, performance may be degraded due to such backup.  
> To minimize the impact on service, backup is recommened while service workload is low.

### Backup Storage 

RDS for SQL Server helps to store all backup files at a backup storage. Backup storage is provided free of charges, as much as the sum of storage size of all database instances of a region, while the exceeding part shall be charged.  
Auto backup files are deleted along with database instance deletion, while manual backup files are permanently saved at a backup storage, unless specified otherwise by user.  

### Auto Backup

By setting up the backup retention period for more than a day, auto backup is enabled and executed during specified backup execution period. Unless the backup execution time is specified, daily auto backup shall be executed when there is the minimum workload. By specifying backup time, auto backup is executed within 15 minutes from the specified time. Auto backups can be saved for up to 30 days. When the backup retention period setting is N/A, auto backup is disabled, deleting all auto backup files saved from backup storage. With the auto backup disabled, restoration to a point of time during backup retention period becomes unavailable, while restoration to a particular time with manual backup only is available.   

> [Caution]
> If auto backup is enabled, make sure to use the `Full` database recovery model.
> If the `Simple` or `Bulk logged` model is used, it will be forced to use the `Full` recovery model and perform a full backup again from the beginning.

### Manual Backup

Regardless of auto backup enabling, a backup to a time of choice can be manually executed. To create a manual backup, it must be named to meet the following rules:   

* Must be unique for each region.
* Must be comprised of alphabets, numbers, -, _ , and . only, between 4 and 100 characters. 
* Must start with a letter. 

## Restoration

RDS for SQL Server helps to restore to a backup moment by using backup files, or to a point in time. With restoration, a new database instance is created, which is irrelevant to an existing database instance. Since restored database instance regards to database only, a new setting of a parameter and a security group is required. Setting of a new parameter group is available, but it is recommended to restore with the parameter group from the backup time.    

### Restoration with Backup

With manual or auto backups, database instance can be restored. Restoration time depends on the backup size, from a few minutes, up to dozones of minutes. It is recommended to apply the same type of backup database instance and parameter group for restoration. 

> [Caution]
> If a database instance has many databases, each in big size, backup time might be different for each.  
> Since backup is executed for each database one by one, recovery is not ensured for all databases from a certain backup time.   

### Point-in-Time Restoration during Backup Retention Period 

If auto backup is enabled for a database instance, it is available to restore data to a time point during retention period. To enable a point-in-time restoration, log backup is required. RDS for SQL Server executes auto log backups at every 5 minutes, and stores them at a backup storage. If the auto backup is enabled, it detects the database created by user every 5 minutes and performs a full backup separately. Therefore, if users try to roll back to the time the database was just created, the newly created database won't be recovered properly. Using a reliable DB instance without separate modification, a point in time which as at least 5 minutes after the time of creation must be selected.

