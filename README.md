# NSClientpp_dh-key-updater
A PowerShell script to manage NSClient++ configuration on domain controllers. It checks if the domain controller is up, verifies the presence of the NSClient++ service, creates a DH key file with 2048 bit if it doesn't exist, updates the `nsclient.ini` configuration file, and restarts the NSClient++ service.

# NSClient++ DH Key Updater

A PowerShell script to configure the DH key for NSClient++ on domain controllers.

## Overview

This script is designed to automate the process of adding a Diffie-Hellman (DH) key to the NSClient++ configuration on Windows domain controllers. It checks if the NSClient++ service is running on each domain controller, and if the DH key file is already present. If the file is not present, it creates the file, updates the configuration, and restarts the NSClient++ service.

## Features

- **Domain Controller Detection**: Fetches the list of domain controllers in the Active Directory domain.
- **Service Check**: Verifies if the NSClient++ service is running.
- **DH Key Management**: Creates the DH key file if it does not exist and updates the NSClient++ configuration.
- **Logging**: Logs all actions and results to a specified log file.
- **Error Handling**: Skips servers that are unreachable or already have the DH key file.
- **CSV Export**: Results are exported to a specified CSV file.

## Usage

### Installation

1. Place the `NSClientPP_DHKey_Updater.ps1` script in a suitable directory.
2. Ensure the script has the appropriate permissions to run.

### Configuration

1. Modify the script to set the path for your log file:
   ```powershell
   $logFilePath = "PATH/TO/YOUR/LOGFILE.log"
   ```
2. Modify the script to set the path for your CSV file:
   ```powershell
   $logFilePath = "PATH/TO/YOUR/output.csv"
   ```
3. Ensure the Active Directory PowerShell module is installed and imported.

### Execution

Run the script in a PowerShell session with administrative privileges.

#### Example:

To run the script manually:

  ```powershell
  .\NSClientPP_DHKey_Updater.ps1
  ```

### Cron Job Setup

To run the script periodically, you can set up a scheduled task in Windows Task Scheduler. Configure the task to run with the highest privileges.

### Logging

Check the specified log file for detailed logs of the script's execution.

#### Example

Suppose your log file path is C:\Logs\nsclientpp.log:

Set the log file path in the script:

```powershell
$logFilePath = "C:\Logs\nsclientpp.log"
```

Run the script manually:

```powershell
.\NSClientPP_DHKey_Updater.ps1
```

## Log File Content Example

The log file will contain similar entries as shown in the log output example. Here is a snippet of what the log file content may look like:

```
2024-07-11 10:00:00 - Processing DC01
2024-07-11 10:00:01 - DC01 is up.
2024-07-11 10:00:02 - NSClient++ service found on DC01.
2024-07-11 10:00:03 - DH key file created on DC01 at \\DC01\C$\Program Files\NSClient++\security\nrpe_dh_2048.pem.
2024-07-11 10:00:04 - nsclient.ini file updated on DC01.
2024-07-11 10:00:05 - NSClient++ service restarted on DC01.
2024-07-11 10:00:06 - Processing DC02
2024-07-11 10:00:07 - DC02 is up.
2024-07-11 10:00:08 - NSClient++ service found on DC02.
2024-07-11 10:00:09 - DH key file already exists on DC02. Skipping...
```

These log entries provide a step-by-step record of what the script is doing, which can be helpful for debugging and auditing purposes.

## CSV File Content Example

Exporting the data to a CSV file provides a streamlined and efficient way to manage and analyze information from a large number of Domain Controllers, allowing for easy tracking of server statuses and configuration changes in a structured format that is compatible with various data analysis tools. Here is a snippet of what the log file content may look like:

```
Date,Time,Server,Server Status,NSClient++ Service,DH Key Created?,Config file updated,Restarted NSClient++?
2024-08-22,18:16:14,DC01,UP,Yes,Already Exists,NA,NA
2024-08-22,18:16:15,DC02,UP,No,No,No,No
2024-08-22,18:16:17,DC03,UP,Yes,Already Exists,NA,NA
2024-08-22,18:16:18,DC04,UP,Yes,Already Exists,NA,NA
2024-08-22,18:16:18,DC05,UP,Yes,Already Exists,NA,NA
2024-08-22,18:16:19,DC06,UP,No,No,No,No
```

## Note
Ensure you generate your own DH key. The one provided in the script is a placeholder.

This script is a tool to help automate the configuration of NSClient++ on your domain controllers. Ensure you review and test the script in a controlled environment before deploying it in production.
