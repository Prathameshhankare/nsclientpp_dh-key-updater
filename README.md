# nsclient-_dh-key-updater
A PowerShell script to manage NSClient++ configuration on domain controllers. It checks if the domain controller is up, verifies the presence of the NSClient++ service, creates a DH key file with 2048 bit if it doesn't exist, updates the `nsclient.ini` configuration file, and restarts the NSClient++ service.
