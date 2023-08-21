# Database Migration Guide
MongoDB Atlas to MongoDB Production Servers

Migrating a database from MongoDB Atlas to your own production servers involves several steps to ensure a smooth transition. The following guide provides a detailed walkthrough of the process, ensuring you can complete the migration successfully.

## Clone External Database using `mongodump`

1. Connect to your MongoDB Atlas database using the appropriate credentials.
2. Open a terminal or command prompt.
3. Navigate to the directory where you want to save the backup.
4. Run the following command to perform a backup:
   ```
   mongodump --uri="<Atlas Connection String>"
   ```
   This command will create a backup of your Atlas database in BSON format.

## Establish VPN Connection for Production

1. Ensure you have the necessary VPN client software installed.
2. Connect to your production environment via VPN to establish a secure connection.

## Connect to Production MongoDB Server

1. Open a terminal or command prompt on your local machine.
2. Connect to your production MongoDB server using the following command:
   ```
   mongo --host <production_host> --port <production_port> -u <username> -p
   ```

## Backup Existing Production Server Database

1. Once connected to the production MongoDB server, initiate a backup using the following command:
   ```
   mongodump --db <production_db_name> --out <backup_directory>
   ```

## Remove the Existing Production Database

1. Still connected to the production MongoDB server, drop the existing database:
   ```
   use <production_db_name>
   db.dropDatabase()
   ```

## Restore Cloned Database to Production Server

1. In the same terminal, navigate to the directory where you saved the backup created from Atlas.
2. Run the following command to restore the backup to the production server:
   ```
   mongorestore --db <production_db_name> <backup_directory>/<atlas_db_name>
   ```

## Update URLs and Production Settings

1. In the application code or configuration files, update any URLs and settings that point to the MongoDB Atlas instance. Replace them with the appropriate details for your production server.

## Test Everything

1. Run thorough testing on your application to ensure that it is functioning as expected with the new production MongoDB server.
2. Test various functionalities, endpoints, and queries to verify the integrity of the migrated data and the application's behavior.

