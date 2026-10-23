# Lab 04: Simple Python Database Connections

## Objective
The objective of this lab is to connect Python applications with MySQL and MongoDB, configure database connections using environment variables, and manage credentials through a configuration file.

## Tools and Technologies
- Ubuntu Linux
- Python 3
- MySQL
- MongoDB
- Docker and Docker Compose
- Git and GitHub

## Tasks Completed

### Task 1: MySQL Connection
Connected Python to the MySQL database using `mysql.connector` and verified the connection by retrieving the database environment.

### Task 2: MongoDB Connection
Connected Python to MongoDB using `pymongo` with hardcoded connection credentials and verified the connection using a ping command.

### Task 3: Environment Variables
Configured MongoDB connection details using environment variables to connect to the development, testing, and production databases.

### Task 4: Configuration File
Created a local `credentials.ini` file to store database credentials and used Python's `configparser` module to select the required database environment.

### Task 5: Credential File Permissions
Restricted access to the local credentials file using Linux file permissions.

## Verification
The database connections were tested by checking the selected database, server address, and environment information.

## Screenshots
The `screenshots/` directory contains evidence of the setup, database connections, environment configurations, credential file permissions, and required verification tasks.

## Conclusion
This lab demonstrates how Python connects to MySQL and MongoDB. It also explains how environment variables and configuration files can be used to manage database connection settings for different environments.
