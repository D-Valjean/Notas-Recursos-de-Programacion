

To resolve the “sudo command not found” error on a Debian-based system, follow these steps:

1. Install the `sudo` package:
    
     
    
    Since you’re on a Debian-based system, you can use the `apt` package manager to install the `sudo` package. Open a terminal and run the following command:
    
    ```
    su -
    apt update
    apt install sudo
    ```
    
    The `su -` command is used to switch to the root user, which is necessary to install the `sudo` package. You will be prompted to enter the root password.
    
2. Add the user to the `sudo` group:
    
     
    
    After installing the `sudo` package, you need to add the user to the `sudo` group. Replace `username` with the actual username:
    
    ```
    usermod -aG sudo username
    ```
    
    You can then log out and log back in for the group change to take effect, or apply the group change immediately with:
    
    ```
    su - username
    newgrp sudo
    ```
    

Now, you should be able to use the `sudo` command without any issues.