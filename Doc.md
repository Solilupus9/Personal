# Create Dir LLD

## Overview
The CreateDir project is designed to create a new folder at a specified path, validate the path and folder name, and log the process. It also handles errors by logging them and creating error reports.  
### Functions:
1. ***create.py***:
    1. **validate(path, folder_name):**  
        * Purpose: Validates the provided path and folder name.
        * Parameters:
            - path (str): The directory path where the folder will be created.
            - folder_name (str): The name of the folder to be created.
        * Exceptions:
            - Raises ValueError if the path or folder name contains invalid characters.
            - Raises FileExistsError if the folder already exists.
            - Raises FileNotFoundError if the path does not exist.
            - Raises PermissionError if the path is not writable.
            - Raises NotADirectoryError if the path is not a directory.
    <br></br>
    2. **create(BASE_DIR, path='.', folder_name='New folder'):**  
        * Purpose: Creates a new folder at the specified path and logs the process.
        * Parameters:
            - BASE_DIR (str): The base directory for configuration and logs.
            - path (str): The directory path where the folder will be created. Defaults to the current directory.
            - folder_name (str): The name of the folder to be created. Defaults to 'New folder'.
        * Exceptions:
            - Raises FileNotFoundError if the configuration file is not found.
        * Process:
            1. Checks for the existence of the configuration file.
            2. Creates required directories if they do not exist.
            3. Initializes the logger.
            4. Logs the start time, path, and folder name.
            5. Validates the path and folder name.
            6. Creates the folder.
            7. Logs the success or error.
            8. Calls create_backup to create a backup.
<br></br>
2. ***audit_log.py***:
   1. **audit_log(BASE_DIR):**  
        * Purpose: Initializes and returns a logger for audit logging.
        * Parameters:
            - BASE_DIR (str): The base directory for configuration and logs.
            - Returns: A configured logger instance.
        * Process:
            1. Loads configuration from Config.json.
            2. Determines the log interval and format.
            3. Creates or appends to the audit log file.
            4. Configures the logger with the appropriate level and format.
            5. Logs the creation of the log file and debug mode status.
    <br></br>
3. ***backup.py***:
   1. **create_backup(logger, BASE_DIR):**  
        * Purpose: Creates a backup of specified folders.
        * Parameters:
            - logger: The logger instance for logging the backup process.
            - BASE_DIR (str): The base directory for configuration and logs.
        * Process:
            1. Creates the backup directory if it does not exist.
            2. Loads configuration from Config.json.
            3. Copies specified folders to the backup directory.
            4. Logs the backup process.
    <br></br>
4. ***error_log.py***:
    1. **error_log(logger, e, time, BASE_DIR):**
        * Purpose: Logs error details and creates an error report.
        * Parameters:
            - logger: The logger instance for logging errors.
            - e (Exception): The exception that occurred.
            - time (str): The start time of the process.
            - BASE_DIR (str): The base directory for configuration and logs.
        * Process:
            1. Loads configuration from Config.json.
            2. Takes a screenshot if configured to do so.
            3. Reads the error template.
            4. Formats the error details into the template.
            5. Writes the error details to an error log file.
            6. Logs the creation of the error log.

### Dependencies
* os: For file and directory operations.
* re: For regular expression operations.
* datetime: For date and time operations.
* json: For reading configuration files.
* logging: For logging operations.
* shutil: For file operations.
* psutil: For system information.
* socket: For network information.
* traceback: For exception traceback.
* mss: For taking screenshots.

### Configuration
* Config File: Config.json
    - Contains settings like log interval, debug mode, audit log format, and backup folders.

### Error Handling
* Errors are caught and logged using the error_log function.
Error details are written to a template-based error log file.

### Logging
* Uses the audit_log function to log the process.
Logs include debug information, errors, and process completion status.