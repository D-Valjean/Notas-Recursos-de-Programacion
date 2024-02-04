

The **`ifconfig`** command is part of the **net-tools** package, a Linux network utility deprecated because of a lack of maintenance and IPv6 support. 

While certain distributions still have net-tools preinstalled, others, like Debian, don't. Therefore, when Debian users try to run **`ifconfig`**, the output prints an error.

![ifconfig Debian terminal output](https://phoenixnap.com/kb/wp-content/uploads/2022/11/ifconfig-debian-terminal-output.png)

The error occurs either because the system does not have **net-tools** or because the **`ifconfig`** directory is not added to the standard **PATH** variable.

The following sections explain how to fix the ifconfig "_command not found"_ issue.

### Method 1: Install net-tools

The first step to fixing the _"command not found"_ error is to install **net-tools**. Do the following:

1. Update Debian repositories.

```
sudo apt update
```

![sudo apt update terminal output](https://phoenixnap.com/kb/wp-content/uploads/2022/12/sudo-apt-update-terminal-output.png)

2. Install **net-tools** with **[apt](https://phoenixnap.com/kb/apt-linux)**.

```
sudo apt install net-tools
```

![sudo apt install net-tools terminal output](https://phoenixnap.com/kb/wp-content/uploads/2022/12/sudo-apt-install-net-tools.png)

3. Run **`ifconfig`** to confirm the installation.

```
ifconfig
```

![ifconfig Debian terminal output](https://phoenixnap.com/kb/wp-content/uploads/2022/12/ifconfig-debian-terminal-output.png)

The output above verifies the installation. However, in some cases, Debian won't execute **`ifconfig`** even after the user installs **`net-tools`**. The command prints the same error as before the installation: 

![bash: ifconfig: command not found](https://phoenixnap.com/kb/wp-content/uploads/2022/12/ifconfig-debian-command-not-found.png)

This happens because the system installs **`ifconfig`** in _**/sbin/**_, which is not a part of the standard user **PATH** variable. By default, regular users cannot invoke **`ifconfig`** unless they add the command to **PATH.** However, workaround methods exist.