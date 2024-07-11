# nsclient-_dh-key-updater
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

## Usage

### Installation

1. Place the `NSClientPP_DHKey_Updater.ps1` script in a suitable directory.
2. Ensure the script has the appropriate permissions to run.

### Configuration

1. Modify the script to set the path for your log file:
   ```powershell
   $logFilePath = "PATH/TO/YOUR/LOGFILE.log"
   ```
2. Ensure the Active Directory PowerShell module is installed and imported.

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

## Note
Ensure you generate your own DH key. The one provided in the script is a placeholder.

This script is a tool to help automate the configuration of NSClient++ on your domain controllers. Ensure you review and test the script in a controlled environment before deploying it in production.
