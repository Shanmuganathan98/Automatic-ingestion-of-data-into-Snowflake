**Automatic ingestion of data from local to snowflake tables**

**Table of Contents**

1\. Introduction

2\. Purpose

3\. Requirements

4\. Installation

5\. Configuration

6\. Usage

7\. Workflow

8\. Features

9\. Limitations

10\. Conclusion

**1\. Introduction:**

The CSV File Loader to Snowflake script is a Python application designed to automate the process of loading CSV files into Snowflake tables. It utilizes the Snowflake Python Connector and the Watchdog library to monitor a specified directory for the creation of CSV files. Upon detecting a new CSV file, the script connects to a Snowflake account, creates or updates corresponding tables, and loads the data into Snowflake.

**2\. Purpose:**

The purpose of this script is to streamline data ingestion workflows by eliminating manual intervention in the process of loading CSV files into Snowflake. By automating file monitoring, table creation, and data loading tasks, it helps improve efficiency, reduce errors, and accelerate data processing pipelines.

**3\. Requirements:**

To use the CSV File Loader to Snowflake script, the following requirements must be met:

- Python 3.x installed on the system.
- Snowflake Python Connector (\`snowflake-connector-python\`) installed.
- Watchdog library (\`watchdog\`) installed.
- Access to a Snowflake account with necessary privileges for data loading operations.

**4\. Installation:**

To install the required Python libraries, use the following command:

pip install snowflake-connector-python watchdog

**5\. Configuration:**

Before running the script, configure the following parameters:

- Snowflake Account: The name of the Snowflake account where data will be loaded.
- Snowflake User: The username used to connect to the Snowflake account.
- Snowflake Password: The password associated with the Snowflake user.
- Snowflake Database: The name of the Snowflake database where tables will be created or updated.
- Snowflake Warehouse: The Snowflake warehouse to be used for data loading operations.
- Snowflake Schema: The name of the Snowflake schema where tables will be created or updated.
- Directory Path: The absolute path to the directory containing CSV files to be monitored.

**6\. Usage:**

To use the script:

1\. Run the script using Python:

python csv_loader_to_snowflake.py

2\. Follow the prompts to provide the required Snowflake account information, directory path, and other configuration parameters.

3\. The script will start monitoring the specified directory for newly created CSV files. When a new CSV file is detected, it will be automatically loaded into a corresponding Snowflake table.

4.Libraries Used:

- snowflake.connector: This library is used to establish a connection with Snowflake and execute SQL queries.
- Time: Used for handling time-related operations.
- os: Provides a portable way of using operating system-dependent functionality.
- csv: Helps in parsing CSV files.
- watchdog: A Python library that monitors filesystem events.
- getpass: Used for securely entering passwords without displaying them on the screen.
- MyHandler Class:
- This class is a subclass of FileSystemEventHandler and contains methods to handle file system events.
- Methods:
- \__init_\_(...): Initializes the handler with Snowflake connection details and the directory path to monitor.
- on_created(...): Overrides the method to handle file creation events. It checks if a CSV file is created and calls load_to_snowflake method.
- load_to_snowflake(...): Loads data from a CSV file into Snowflake. It establishes a connection, determines the table name from the file name, and executes SQL queries to load data.
- create_new_table(...): Creates a new Snowflake table based on the CSV file's structure.
- detect_delimiter(...): Detects the delimiter used in the CSV file.

**7.Workflow:**

- Initialization: The script prompts the user to input Snowflake account details (account, user, password), database, warehouse, schema, and the directory path containing CSV files. Snowflake account credentials and directory path are provided by the user.
- Directory Monitoring Setup: An instance of the ‘MyHandler’ class is created, which handles filesystem events such as file creations. An observer object is instantiated, which monitors the specified directory (provided by the user) for filesystem events. The observer is configured to use the ‘MyHandler’ instance for event handling.
- Observer Start: The observer starts monitoring the specified directory for filesystem events, such as file creations.
- File Creation Event Detection: As CSV files are created in the monitored directory, filesystem events are detected by the observer.
- ‘on_created’ Method Execution: Upon detecting a file creation event, the ‘on_created’ method of the ‘MyHandler’ class is invoked.
- CSV File Detection: The ‘on_created’ method checks if the newly created file is a CSV file. If the file is a CSV file, the script proceeds with the data loading process. Otherwise, it ignores the event.
- Data Loading to Snowflake: The script establishes a connection with Snowflake using the provided account details (account, user, password). SQL commands are executed to load the data from the CSV file into Snowflake. If a table already exists with a similar name to the CSV file, the data is appended to the existing table. Otherwise, a new table is dynamically created based on the CSV file's structure.
- File Staging: Before loading data into Snowflake, the CSV file is staged in Snowflake using the PUT command. The file is placed in a temporary staging area within Snowflake for efficient data transfer.
- Data Loading Process: Snowflake's COPY INTO command is used to load data from the staged CSV file into the Snowflake table. The COPY INTO command specifies the source file format and the destination table where the data will be loaded.
- Error Handling: Throughout the data loading process, robust error handling mechanisms are implemented to handle exceptions gracefully. Any errors encountered during the data loading process are logged and reported to ensure data integrity and reliability.
- Observer Continues Monitoring: After processing the file creation event, the observer continues to monitor the directory for further filesystem events.
- Repeat Process: The script remains in a loop, continuously monitoring the directory for new CSV files and initiating the data loading process as new files are created. This process continues until the user interrupts the script or stops the observer.

**8\. Features:**

- File System Monitoring: Utilize the watchdog library to monitor a specified directory for CSV file creations.
- Snowflake Connectivity: Establish connections with Snowflake using the snowflake.connector library to execute SQL queries for data loading.
- Dynamic Table Creation: Dynamically create Snowflake tables based on the structure of CSV files, ensuring flexibility and adaptability.
- Error Handling: Implement robust error handling mechanisms to gracefully handle exceptions and ensure data integrity.
- Logging: Incorporate logging functionality to track events, errors, and data loading activities for monitoring and troubleshooting purposes.

**9\. Limitations:**

- The script assumes that CSV files have a consistent structure and format.
- It does not handle complex CSV file structures or transformations.
- Error handling is limited to basic exception catching and logging.

**10\. Conclusion:**

The Automatic CSV to Snowflake Loader project offers a comprehensive solution for automating data loading processes into Snowflake, enhancing efficiently, and enabling real-time data integration and analysis. With its robust features and potential for future enhancements, the project aims to provide organizations with a reliable and scalable solution for their data integration needs.