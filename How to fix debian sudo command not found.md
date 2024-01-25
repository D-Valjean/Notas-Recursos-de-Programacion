
Before discussing how to fix sudo commands not found in Debian we will first discuss what Sudo is. Sudo means the superuser; as a superuser you have all the privileges which a root user can enjoy. Different distributions of Linux are such as Ubuntu, Fedora, and Mageia. Similarly, Debian is also an example of Linux general distribution. Ubuntu distribution is used for beginners whereas Debian is an advanced distribution that is used on an expert level. While working on Debian sometimes we found an error using the “sudo” command. It may be something like “sudo command not found”, “[user name] is not in the sudoers list” or maybe some other error that means the same.

This write-up is associated with the solution with which we can resolve this error. We will discuss both errors separately which are related to the sudo package, when we face them and how we can resolve these issues.

## How to FIX: Debian sudo command not found

By default in Debian, the sudo command is installed but sometimes it happens that we use the sudo command and it generates the following error.

We simply enter the root user mode as:

$ sudo -s

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20723%20122'%3E%3C/svg%3E)

So it means that the sudo package is not installed by default so to resolve this issue we simply go to the user mode and install the package. First, we will go to the root user mode.

$ su -

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20722%20116'%3E%3C/svg%3E)

Update the repository first.

# apt update

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20726%20198'%3E%3C/svg%3E)

Install the sudo package.

# apt install sudo -y

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20725%20344'%3E%3C/svg%3E)

Exit the root mode.

# exit

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20720%20120'%3E%3C/svg%3E)

To verify the installation of the error we will again enter the root by using sudo command.

$ sudo -s

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-6.png)

The issue which has been discussed at the start is now resolved.

## How to add user to sudoers file to resolve the error

We simply run the command of the list of disks on Debian.

$ sudo fdisk -l

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-7.png)

We have the output, “zhammad is not in the sudoers file . This incident will be reported.”, this is an error which means we cannot use the sudo command. Sudo command is an administrative command which is used with those commands which need administrative permissions. Now it means the user “zhammad” does not have the administrative rights so to access those permissions we have to install the “sudo command” manually and give the administrative privileges to this user.

We will switch the user to administrative user which is “hammad” in our case. So by using the “su command” we switch to hammad from zhammad.

$ su hammad

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-8.png)

Now as we switch the user to hammad, we will go to the root mode.

$ sudo -s

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-9.png)

Update the repository of Debian by using the update command.

# apt-get update

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-10.png)

As we can see in the output, the repository is updated and all the packages are up to date so no need to upgrade the repository. Now we add the new user in the list of sudoers file by using the command.

# usermod -aG sudo zhammad

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-11.png)

The user has been added to the list of sudoers and for the verification of this we used the command of “id”.

# id zhammad

![](https://linuxhint.com/wp-content/uploads/2021/10/How-to-fix-debian-sudo-command-not-found-12.png)

In the above output, we see the zhammad user is also added to the list of sudo. After verifying this we will exit the root mode by typing “exit”.

# exit

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20724%20125'%3E%3C/svg%3E)

For switching back to the zhammad from hammad.

$ su zhammad

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20724%20140'%3E%3C/svg%3E)

Again run the command of fdisk and confirm that the issue has been solved.

$ sudo fdisk -l

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20727%20390'%3E%3C/svg%3E)

The command runs successfully and displays the list of disks. So our issue has been resolved.

## Conclusion

Sudo is used for the commands which are making the changes in the root folder and administrative things. For a secure purpose, these permissions are only given either to the root user or the user which are allowed by the root user. We have discussed the solution of the issue in this write-up which is to resolve it by installing the sudo manually (if it is not installed so can be installed by this command else it is installed in Debian by default) and adding the user to the list of sudoers by switching to the administrative user account. I tried to assist you with the solution of “sudo command not found” in this write-up and hope this will help you in resolving the issue.

### ABOUT THE AUTHOR

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20112%20112'%3E%3C/svg%3E)

#### Hammad Zahid

I'm an Engineering graduate and my passion for IT has brought me to Linux. Now here I'm learning and sharing my knowledge with the world.

[View all posts](https://linuxhint.com/author/hzahid/)

#### RELATED LINUX HINT POSTS

- [How to Install Discord on Debian 12](https://linuxhint.com/install-discord-debian/ "How to Install Discord on Debian 12")
- [How to Install wget on Debian 12](https://linuxhint.com/install-wget-debian/ "How to Install wget on Debian 12")
- [How to Install Rust on Debian 12 Bookworm](https://linuxhint.com/install-rust-debian/ "How to Install Rust on Debian 12 Bookworm")
- [How to Install KDE Plasma Desktop Environment on Debian 12](https://linuxhint.com/install-kde-debian/ "How to Install KDE Plasma Desktop Environment on Debian 12")
- [How to Install NVM on Debian 12- Installing Multiple Node.js Versions](https://linuxhint.com/install-nvm-debian/ "How to Install NVM on Debian 12- Installing Multiple Node.js Versions")
- [How to Install Golang (Go) on Debian 12](https://linuxhint.com/install-go-debian/ "How to Install Golang (Go) on Debian 12")
- [How to Install Docker Compose on Debian 12 Bookworm](https://linuxhint.com/install-docker-compose-debian/ "How to Install Docker Compose on Debian 12 Bookworm")

**Linux Hint LLC, editor@linuxhint.com  
1309 S Mary Ave Suite 210, Sunnyvale, CA 94087  
**[Privacy Policy](https://linuxhint.com/policies-and-privacy/) and [Terms of Use](https://linuxhint.com/terms-of-use/)

32

0

Added to Favorites

Saved to Favorites! Sign in to ensure your favorites are not lost.

SIGN IN

Remove from FavoritesMy Favorite PagesSign in to ensure your favorites are not lost

0

SIGN IN

Powered by Slickstream