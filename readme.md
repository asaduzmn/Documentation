# Table of Contents
- [VMWare Installation Guide](#vmware-installation-guide)
    - [Download VMWare work station](#download-vmware-work-station)
    - [VMWare Installation](#vmware-installation)
- [Ubuntu Installation Guide](#ubuntu-installation-guide)
    - [Requirements](#requirements)
    - [Install Ubuntu](#install-ubuntu)
- [MySQL Installation](#mysql-installation)
    - [Install](#install)
    - [Configure MySQL](#configure-mysql)
    - [Secure Installation MySQL](#secure-installation-mysql)
- [Install PostgreSQL](#install-postgresql)
- [Install Oracle 19c Database](#install-oracle-19c-database)
    - [Requirements for oracle database](#requirements-for-oracle-database)
    - [Install Oracle Linux](#install-oracle-linux)
    - [Install Oracle Database 19c](#install-oracle-database-19c)
    - [Oracle DB 19c Prerequisites](#oracle-db-19c-prerequisites)
    - [Oracle 19c Software Installation](#oracle-19c-software-installation)
    - [Configuring the Oracle database listener](#configuring-the-oracle-database-listener)
- [Conclusion](#conclusion)

# VMWare Installation Guide
This section guide how to install vmware on windows

---
<!-- Download VMWare section -->
## Download VMWare work station
1. Navigate to [**Broadcom Support**][broadcom-support]. Log in on Broadcom or resgister if do not have an account. 
2. From the **Software** menu section, select **VMware Cloud Foundation** and then **My Downloads**.
3. Click on **VMware Workstation Pro**.  
4. Click on your desired **release**.  
5. Click **Download**.
---

<!-- Install VMWare section -->
## VMWare Installation
### Step 1:
After efficiently downloading the setup file, right-click and select Run as administrator.
### Step 2:
Please wait while it gets the necessary files to install the newest version of VMware Pro.
### Step 3:
To keep installing Workstation Pro, click the Next button in the Setup window.
### Step 4:
You must agree to the license agreement to ensure a hassle-free Workstation software setup. After accepting it, hit the Next button in the End-User License Agreement window.
### Step 5:
Installing the Enhanced Keyboard Driver when using a virtual machine in the program is a good idea. Check the confirm box and click Next to install the advanced option.
### Step 6:
You can enable automatic updates at startup for getting smooth user experience and press next button.
### Step 7:
To put shortcuts on your Windows desktop and start the menu, check both options in the Shortcuts window and click the Next button.
### Step 8:
Next, click the Install button to build the virtual OS program on Windows.
### Step 9:
Wait as the program copies the files it needs onto your system for Workstation Pro and sets up the system settings.
### Step 10:
Once you’ve completed the intricate steps, click the Finish button precisely.
### Step 11:
Click the Yes button to restart computer for taking workstation effect.
### Step 12:
Once the PC restarts, promptly double-click the VMware shortcut to open it. <br>
If you have purchased VMware software, enter the license key in the space provided below. Or, if you want to enjoy it free for personal use, select the option and continue.
### Step 13:
Now you have successfully installed VMware Pro, you can create or open virtual machine from VMWare, and final look will be this.

![VMware Workstation Pro Screenshot][workstation-image]

---

<br>
<br>

<!-- Ubuntu Installation Section -->
# Ubuntu Installation Guide

This section guide how to install Ubuntu on VMWare.

---
## Requirements
- [x] VMware installed
- [ ] Ubuntu ISO downloaded. Get Ubuntu from [Official website][ubuntu-download].
---


## Install Ubuntu
### Step 1: Create a new virtual machine.
1. After Downloading ubuntu iso file. Double click VMWare app and click on **Create a new virtual machine**.
2. Select **custom** type configuration and click on next.
3. You can choose different hardware compatibility or default and then press next button.
4. On guest Installation window select I will install operating system later and press next button.
5. Now select **ubuntu** version from drop down menu and press next button. 
6. Now you can choose virtual machine name and location for storing this virtual machine. For example:
    ```
    Virtual machine name: Ubuntu-64-bit and
    Location: I selected on D:// with name ubuntu-22.04 LTS
    ```
7. Select **processor** at least two and **cores** two and press next button.
8. Now select **memory** at least select **4GB** memory and press next button.
9. For network configuration select **NAT** and press next button
10. For **I/O controller type** keep default and press next button.
11. Keep default for **disk type** and press next button
12. Select **Create new Virtual disk** and press next button
13. Now choose **maximum disk capacity** at least **50GB** recommended, and you can select store virtual file as either **as single file** or **multiple**. And then press next button.
14. Specify disk file. Keep default is recommended.
15. Now press finish button and a virtual machine is created and final output will look like this photo.

    ![Virtual machine for ubuntu Screenshot][ubuntu-virtual-image]

---
### Step 2: Load a ubuntu iso and Install
1. Press on **edit virtual machine** settings on created virtual machine
2. You can see all the hardware configuration here, and press **CD/DVD** and browse for the ubuntu iso file and don't forget to select **connect at power on**.
3. Your set up is complete now power this virtual machine to start the installation process.
4. Upon booting from the ".iso" or "bootable media kit, you will be welcomed with a screen presenting multiple options. To initiate the installation process of Ubuntu 24.04, you must select the "Try or Install Ubuntu" option and hit the Enter key.
5. Now choose language for ubuntu. For me it is english.
6. Now accessibility you can leave what is default and press next button.
7. Choose keyboard layout for me it is **English(US)** and press next button.
8. In connect to the internet section choose **wired connection** and press next button.
9. Then choose **Install ubuntu** option and press next.
10. And then select interactive installation and press next button.
11. Here select default selection and press next button.
12. Select propriety software if you needed. 
13. And then we select erase disk and install ubuntu as it will not affect the host computer and go for next.
14. Now for **Account window** you choose your computer name, username and password.
15. Select **Time Zone**. If you are connected with internet it will automatically selected according to your location and go for the next button.
16. Now you for the final step you press the **Install** button and wait until it finish it's process.
17. After installation complete it will show a restart dialog box press the **restart** button and you have successfully completed installation.
18. Now log in into computer with your username password, and final output will like this.

    ![Ubuntu Landing Page][ubuntu-image]



<!-- MySQL installation on ubuntu -->
# MySQL Installation
This section guide how to install MySQL on Ubuntu.

## Install
### Step 1:
To install it, update the package index on your server if you’ve not done so recently:
```
sudo apt update
```

### Step 2:
Then install the ```mysql-server``` package:
```
sudo apt install mysql-server
```
### Step 3:
Ensure that the server is running using the ```systemctl start``` command:
```
sudo systemctl start mysql.service
```
These commands will install and start MySQL, but will not prompt you to set a password or make any other configuration changes. Because this leaves your installation of MySQL insecure, we will address this next.

## Configure MySQL
### Step 1: Adjust mysql root
By default root do not have any password. To set password for root use:
```
sudo mysql
```

This will allow you to enter mysql server then need to ```alter``` the user.

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
choose your password in ```password``` place.
### Step 2: 
After making this change, exit the MySQL prompt:
```
mysql> exit
```


## Secure Installation MySQL
### Step 1: 
Run the security script with ```sudo```:
```
sudo mysql_secure_installation
```
This will take you through a series of prompts where you can make some changes to your MySQL installation’s security options. The first prompt will ask whether you’d like to set up the Validate Password Plugin, which can be used to test the password strength of new MySQL users before deeming them valid.
<br>
If you elect to set up the Validate Password Plugin, any MySQL user you create that authenticates with a password will be required to have a password that satisfies the policy you select. The strongest policy level — which you can select by entering ```2``` — will require passwords to be at least eight characters long and include a mix of uppercase, lowercase, numeric, and special characters:

```
Output
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
 2
```


### Step 2:
Regardless of whether you choose to set up the Validate Password Plugin, the next prompt will be to set a password for the MySQL root user. Enter and then confirm a secure password of your choice:
```
Output
Please set the password for root here.


New password:

Re-enter new password:
```
You installed MySQL. If you want to enter mysql prompt just use:
```
mysql -u root -p
```
And enter password for ```root```

---
<br>

# Install PostgreSQL
This section guide how to install and configure PostgreSQL on Ubuntu.

### Step 1:
To install PostgreSQL, run the following command in the command prompt:
```
sudo apt install postgresql 
```



### Step 2: Verify Installation
Once the installation is complete, check the PostgreSQL service status:
```
sudo systemctl status postgresql
```
- If it’s running, you will see a green "active (running)" status.
- To start or enable PostgreSQL manually, use the following commands:
  ```
  sudo systemctl start postgresql
  sudo systemctl enable postgresql
  ```

### Step 3: 
To enter PostgreSQL user use this command:
```
sudo -i -u postgres 
```
### Step 4:
You can now access the PostgreSQL prompt immediately by typing:
```
psql
```
###  Step 5:
You can change/choose password for ```psql```:
```
ALTER USER postgres PASSWORD 'your_secure_password';
```
### Step 6:
Exit shell use 
```
\q
```
---
<br>

# Install Oracle 19c Database
This section guide how to install Oracle 19c database on VMWare.

---
## Requirements For Oracle Database
- [x] VMware installed
- [ ] OS(Oracle Linux). [Download][oracle-linux]
- [ ] Oracle Database 19c for Linux x86-64. [Download ZIP File][oracle-database].
---

## Install Oracle Linux
### Step 1: Make a virtual machine
Follow the step same as [Step 1: Create a new virtual machine.](#step-1-create-a-new-virtual-machine) on [install ubuntu](#install-ubuntu) section. 
A minor changes here on point ```5``` select version ***oracle linux***.
### Step 2:
From **edit virtual machine settings** on **CD/DVD** choose the downloaded iso oracle linux file location.
And then power the virtual machine.
### Step 3:
Upon booting from the ".iso" or "bootable media kit, you will be welcomed with a screen presenting multiple options. 
To initiate the installation process of Linux 8, you must select the "Try or Install Linux" option and hit the Enter key.
### Step 4:
Select Language for your operating system. For me it is **english**.
### Step 5:
On **Installation summary window** need to choose some softwares tool to make the os user friendly. Such as:
- Performance tool.
- Remote management for linux.
- Development tools.
- Graphical administration tools.
- Security tools.
- System tools.

and press **Done**.
### Step 6:
On the same window select installation destination. For VMWare no need to change.
### Step 7:
Now press on Network and Hostname. Turn on ethernet connection and choose hostname.For me it is **orahost**.
And now press **Done**.
### Step 8:
Now press on root password and choose root password. and press **Done**
### Step 9:
Select user creation option and create a user for this os.
### Step 10:
Now you are all set to begin installation and press **Begin Installation**. Wait until it is completed and reboot the system.
### Step 11:
Now it will show license information press on it and accept on the agreement. Then finish the configuration.
You are ready to use the os. Now move to the next section for install oracle database 19c.

---

## Install Oracle Database 19c
### Configure Hosts File
The "/etc/hosts" file must contain a fully qualified name for the server.
```
<IP-address>  <fully-qualified-machine-name>  <machine-name>
```
To know Check the IP address of the VM using ```ifconfig```. My ip address is ```192.168.40.131```.

For example in my case:
```
192.168.40.131  ol8-19.localdomain  ol8-19
```
Set the correct hostname in the "/etc/hostname" file.
```
ol8-19.localdomain
```



## Oracle DB 19c Prerequisites 

### Automatic setup 

If you plan to use the "oracle-database-preinstall-19c" package to  perform all your prerequisite setup, issue the following command.

```
# dnf install -y oracle-database-preinstall-19c
```

Update it:

```
# dnf update -y
```


Create the new groups and users.
```
# groupadd -g 54321 oinstall
# groupadd -g 54322 dba
# groupadd -g 54323 oper 
# useradd -u 54321 -g oinstall -G dba,oper oracle
```



### Additional Setup
Set the password for the "oracle" user.

```
passwd oracle
```

Set secure Linux to permissive by editing the "/etc/selinux/config" file, making sure the SELINUX flag is set as follows.

```
SELINUX=permissive
```

Once the change is complete, restart the server or run the following command.

```
# setenforce Permissive
```

If you have the Linux firewall enabled, you will need to disable or configure it, To disable it, do the following.

```
# systemctl stop firewalld
# systemctl disable firewalld
```

I created these directories in which the Oracle software will be installed.

```
mkdir -p /u01/app/oracle/product/19.3/dbhome_1
mkdir -p /u02/oradata
chown -R oracle:oinstall /u01 /u02
chmod -R 775 /u01 /u02
```

Create a "scripts" directory.

```
mkdir /home/oracle/scripts
```

Create an environment file called "setEnv.sh". The "$" characters are escaped using "\". If you are not creating the file with the `cat` command, you will need to remove the escape characters.

```

## copy this script to your terminal

cat > /home/oracle/scripts/setEnv.sh <<EOF

# Oracle Settings
export TMP=/tmp
export TMPDIR=\$TMP

export ORACLE_HOSTNAME=mydb.localdomain
export ORACLE_UNQNAME=orcl
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=\$ORACLE_BASE/product/19.3/dbhome_1
export ORA_INVENTORY=/u01/app/oraInventory
export ORACLE_SID=orcl
export PDB_NAME=orclpdb
export DATA_DIR=/u02/oradata

export PATH=/usr/sbin:/usr/local/bin:\$PATH
export PATH=\$ORACLE_HOME/bin:\$PATH

export LD_LIBRARY_PATH=\$ORACLE_HOME/lib:/lib:/usr/lib
export CLASSPATH=\$ORACLE_HOME/jlib:\$ORACLE_HOME/rdbms/jlib

EOF
```

Add a reference to the "setEnv.sh" file at the end of the "/home/oracle/.bash_profile" file.

```
echo ". /home/oracle/scripts/setEnv.sh" >> /home/oracle/.bash_profile
```

Create a "start_all.sh" and "stop_all.sh" script that can be called from a startup/shutdown service. Make sure the ownership and permissions are correct.
```
cat > /home/oracle/scripts/start_all.sh <<EOF
#!/bin/bash
. /home/oracle/scripts/setEnv.sh

export ORAENV_ASK=NO
. oraenv
export ORAENV_ASK=YES

dbstart \$ORACLE_HOME
EOF


cat > /home/oracle/scripts/stop_all.sh <<EOF
#!/bin/bash
. /home/oracle/scripts/setEnv.sh

export ORAENV_ASK=NO
. oraenv
export ORAENV_ASK=YES

dbshut \$ORACLE_HOME
EOF

chown -R oracle:oinstall /home/oracle/scripts
chmod u+x /home/oracle/scripts/*.sh
```

Once the installation is complete and you've edited the "/etc/oratab", you should be able to start/stop the database with the following scripts run from the "oracle" user.
```
~/scripts/start_all.sh
~/scripts/stop_all.sh
```

## Oracle 19c Software Installation 

**Oracle DB software**

Download from host to vm oracle Linux 8 using winscp. First switch the user to oracle then. Then use WinSCP from host machine to configure session like this:
![WinSCP session log in][winscp-session-image]

Then just drag the **Oracle database19c** to the vmware oracle linux in "/home/oracle/Downloads".
Then switch to the ```ORACLE_HOME``` directory. and use this command to unzip the downloaded file:
```
unzip -oq /home/oracle/Downloads/LINUX.X64_193000_db_home.zip
```

Now runt this command:
```
# Fake Oracle Linux 7.
export CV_ASSUME_DISTID=OEL7.6

# Interactive mode.
./runInstaller
```

Now it will pop up an interactive window for oracle installer.

### Step 1:
The **Select Configuration Option** page opens and **Select Create and configure a single instance database** and click Next.
### Step 2:
The **Select System Class** page opens and select **Server class** and click Next.
### Step 3:
The **Select Database Edition** page opens and select **Enterprise Edition** and click Next.
### Step 4:
The **Specify Installation Location** page opens and click Next, with the default settings unchanged.
### Step 5:
The **Create Inventory** page opens and click Next, with the default settings unchanged.
### Step 6:
The **Select Configuration Type** page opens and select **General Purpose / Transaction Processing** and click Next.
### Step 7:
The **Specify Database Identifiers** page opens and <br>
Configure the following parameters:
- Enter the global database name: I used ```orcl```.
- Enter the oracle system identifier (SID), which must be consistent with the ORACLE_SID variable setting in the profile file. I used ```orcl```.
- For container ```orclpdb``` is used for pluggable database.

Click Next.

### Step 8:
The **Specify Configuration Options** page open and use default settings on the Memory tab and click next.
### Step 9:
The **Specify Database Storage Options** page opens and Select **File system**, use the default database file location, and click Next. I used different location "u02/oradata/"
### Step 10:
The **Specify Management Options** page opens and click Next, with the default settings unchanged.
### Step 11:
The **Specify Recovery Options** page opens and click Next, with the default settings unchanged. For storage problem I did not select recovery option.
### Step 12:
The **Specify Schema Passwords** page opens and used same passwords for all accounts and Click Next.
### Step 13:
The **Privileged Operating System groups** page opens and click Next, with the default settings unchanged.
### Step 14:
The **Root script execution configuration page** opens and choose password for root, click Next.
### Step 15:
The **Perform Prerequisite Checks** page opens and automatically checks all prerequisites and opens to **Summary** page. 
### Step 16:
Click Install and the **Install Product** page opens and the installation program starts to install the database and displays the installation progress.
In the **Execute Configuration Scripts** dialog box, click OK.

## Configuring the Oracle database listener
### Step 1: 
Go to "/u01/app/oracle/product/19.0.0/dbhome_1/network/admin/" add this to ```tnsnames.ora```:
```
ORCLPDB = 
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP) (HOST = 018-19.localdomain) (PORT = 1521))
  (CONNECT DATA =
    (SERVER DEDICATED)
    (SERVICE NAME = orclpdb)
  )
)

```

### Step 2:
Now go to oracle home directory using this command:
```
cd $ORACLE_HOME
```
then run this command
```
netmgr
```

### Step 3:
From the navigation tree, select **Oracle Net Configuration > Local > Listeners > LISTENER**.

### Step 4:
In the right pane, select **Database Services** from the list, and then click **Add Database**.
A new database tab opens.

### Step 5:
Configure the global database name, location of the Oracle database home directory, and the SID of the database instance. The global database name and SID must be the same as the global database name and SID specified during database installation. For me it is ```orcl``` then save it.

### Step 6:
Check whether listener working or not by checking the listener status:
```
lsnrctl status
```
if it refused then you may need to start the listener using
```
lsnrctl start
```

### Step 7:
Then we check ```tnsping``` for ```ocl``` and ```oclpdb``` using:
```
tnsping ocl
tnsping oclpdb
```
### Step 8:
Now run this command to make sure oracle installed and ready to use and the output should be like this:
```
sqlplus / as sysdba
```
![Oracle SQL][oracle-sql-image]

## Post Installation
Edit the "/etc/oratab" file setting the restart flag for each instance to 'Y'.
```
cdb1:/u01/app/oracle/product/19.0.0/dbhome_1:Y
```

Enable Oracle Managed Files (OMF) and make sure the PDB starts when the instance starts.
```
sqlplus / as sysdba <<EOF
alter system set db_create_file_dest='${DATA_DIR}';
alter pluggable database ${PDB_NAME} save state;
exit;
EOF
```

# Conclusion
Throughout this documentation a brief guideline is given for installing:
- [x] VMware 
- [x] Ubuntu
- [x] MySQL
- [x] PostgreSQL
- [x] Oracle Linux 8
- [x] Oracle database 19c





<!-- RESOURCES -->

<!-- Website Links -->
[broadcom-support]: https://support.broadcom.com/
[ubuntu-download]: https://ubuntu.com/download
[oracle-linux]: https://yum.oracle.com/oracle-linux-isos.html
[oracle-database]: https://www.oracle.com/database/technologies/oracle-database-software-downloads.html#19c


<!-- Image Links -->
[workstation-image]: ./img/workstation-img.png "VMware Worstation Pro Screenshot"
[ubuntu-virtual-image]: ./img/ubuntu-64-virtual.png "A virtual machine for ubuntu"
[ubuntu-image]: ./img/ubuntu.png "Landing page of ubuntu"
[winscp-session-image]: ./img/winscp-session.png "WinSCP session log in"
[oracle-sql-image]: ./img/oracl-sql.png "Oracle SQL"