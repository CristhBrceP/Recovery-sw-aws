# Recovery-sw---aws
Configuration and Installation Manual of a Multicast Solution with AWS for Software Restoration in Computer Labs.

1. Materials:
The high-performance hardware provides the necessary resources to achieve efficient performance and fast response of the multicast platform, therefore a workstation computer equipped with an Intel® Xeon® processor E-2224G, 8 (4P+4E) cores up to 4.7 GHz Chipset FCLGA1151, accompanied by 32GB of RAM 2666 MHz DDR4 and a 2TB SSD M.2 2280 PCIe Gen4x4 M.2 NVMe solid disk was used.

2. Operating Platform:
   
Linux Ubuntu versión22.04.4 LTS (Jammy Jellyfish)
Download link: https://releases.ubuntu.com/jammy/

4. Minimum requirements:
   
* Processor: Intel or AMD at 1 Ghz
* RAM: 384 MB
* Hard disk: 5 GB
* VGA graphics card
* CDROM drive or network card.

4. How to install ubuntu linux?

Step 1: Select Try or Install Ubuntu

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/26a79867-0ab7-4c70-9935-234905425c1d)

Step 2: Once you select it, you will be prompted to proceed with “Try Ubuntu” or install it.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/234cb2d9-b784-49b4-9a8e-b27aa7ed7afa)

Try or Install Ubuntu

Step 3: Alternatively, you can click the installation icon on the desktop to initiate the installation if you dismiss the above window.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/fe9a149f-3235-49ef-81f6-bc722286d4c4)

Start the Installer in Live Environment

Step 4: It will ask you to choose some basic configurations like language and keyboard layout. Select the most appropriate ones for your system.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/3d3e0b5c-b09a-4a0f-9cc9-59a7150395dd)

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/18927a46-3a44-4d26-ae7c-f003b362950f)

Select Language and Keyboard Layout

Step 5: You should go for the normal installation here because it will install some software like a music player, video players and a few games.
If you are connected to the internet, you’ll get the option to download updates while installing Ubuntu. You may uncheck it because it may increase the installation time if you have a slow internet. You can update Ubuntu later as well without any issues.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/a979658e-e7e5-4e2c-9ad2-e819673fcf1f)

Normal Installation Mode

Step 6: The most important screen comes currently. If there are other operating systems installed, you may get the option to install Ubuntu along with them in dual boot.
But since your goal is to only have Ubuntu Linux on your entire system, you should go for the Erase disk and install Ubuntu option.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/f5ed0c92-2e0e-4467-8be0-d4632546be00)

Erase Disk and Install Ubuntu

Step 7: When you hit the “Install Now” button, you’ll see a warning that you are about to delete the data. You already know it, don’t you?
![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/72af27f4-cf3a-43a2-8a89-ba04e31470b9)

Usual warning about formatting the disk

Step 8: Things are straightforward from here. You’ll be asked to choose a time zone.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/ba225e74-ef1e-4dd0-96cd-267572c525f1)

Select Time zone

Step 9: And then you’ll be asked to create a username, computer’s name (also known as hostname) and set a password.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/4cb61374-6967-4f41-b542-226fa58ddc58)

Set username and password

Step 10: Once you do that, you just must wait and watch for like 5–10 minutes. You’ll see a slideshow of Ubuntu features in this time.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/cb02ca00-518c-4ef9-940f-e9aa683e9cf1)

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/9f6f68e1-0c1a-4968-a2d7-23cfe4708f15)

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/37eac7d3-9885-4f2a-9fda-4cddaa1b44ca)

Installer executes various stages of Installation of Ubuntu

Step 11: Once the process finishes, you will be asked to restart the system.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/3f6950c2-2d6f-4342-adfd-c7168932264b)

Restart your system

Step 12: When you restart the system, you might encounter a shutdown screen that asks you to remove the installation media and press enter.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/f88a4bfb-c8f7-4916-a46d-45abbeb9166b)

Remove installation medium

Step 13: Remove the USB disk and press enter. Your system will reboot and this time, you’ll boot into Ubuntu.
That’s it. See, how easy it is to install Ubuntu. You can use this method to replace Windows with Ubuntu.

![image](https://github.com/CristhBrceP/Recovery-sw-aws/assets/171496937/ceda4f1b-42ea-4b67-95fb-f163a9adf958)

Finished installation

5. How to install ZabbiX for Ubuntu?

5.1 Install and configure Zabbix for your platform

Run the following cmds:

sudo wget https://repo.zabbix.com/zabbix/6.3/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.3-3%2Bubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.3-3+ubuntu22.04_all.deb
sudo apt update 
sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent

5.2 Install sql server

sudo apt-get install mysql-server
sudo systemctl start mysql

5.5 Create initial database

sudo mysql
create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'password';
grant all privileges on zabbix.* to zabbix@localhost;
set global log_bin_trust_function_creators = 1;
quit;

5.6 On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.

sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix

5.7 Disable log_bin_trust_function_creators option after importing database schema.

sudo mysql
set global log_bin_trust_function_creators = 0;
quit;

5.8 Configure the database for Zabbix server

Edit file /etc/zabbix/zabbix_server.conf and set the DB password with ->
sudo vim /etc/zabbix/zabbix_server.conf

5.9 Start Zabbix server and agent processes

systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2

5.10 Open Zabbix UI web page and proceed with web ui config (should be self explanatory)
The default URL for Zabbix UI when using Apache web server is http://host/zabbix

6 How to install zabbix for Ubuntu?

#this guide is used for configure ZabbiX monitor of process in plataform linux.
header: | this "open guide" is a collaborative effort. It was begun and is led by [CristhBrceP (https://github.com/CristhBrceP)].

Install and configure ZabbiX for plataform Linux version 22.04 Jammy

#open terminal
#use commnand for install
  wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_7.0-1+ubuntu22.04_all.deb
  dpkg -i zabbix-release_7.0-1+ubuntu22.04_all.deb
  apt update

#use this command for install server, interfaz and agent ZabbiX
  apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent

#use this command for install Mysql server
  sudo apt-get install mysql-server
  sudo systemctl start mysql

#use command for create initial database
#define own password for mysql line 26
  mysql -uroot -p
  password
  mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
  mysql> create user zabbix@localhost identified by 'password';                 
  mysql> grant all privileges on zabbix.* to zabbix@localhost;
  mysql> set global log_bin_trust_function_creators = 1;
  mysql> quit;

#On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.
 sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix

#use this command for Disable log_bin_trust_function_creators option after importing database schema.
  mysql -uroot -p
  password
  mysql> set global log_bin_trust_function_creators = 0;
  mysql> quit;

#Configure the database for Zabbix server
#Edit file /etc/zabbix/zabbix_server.conf and set the DB password with
  sudo vim /etc/zabbix/zabbix_server.conf
    DBPassword=password

#Start Zabbix server and agent processes
  systemctl restart zabbix-server zabbix-agent apache2
  systemctl enable zabbix-server zabbix-agent apache2

#Open Zabbix UI web page and proceed with web ui config
#The default URL for Zabbix UI when using Apache web server is http://host/zabbix
#this guide is used for configure DRBL server of process in plataform linux.
header: |
  this "open guide" is a collaborative effort. It was begun and is led by [CristhBrceP (https://github.com/CristhBrceP)].

How to install DRBL on Linux?

Install and configure DRBL server for plataform Linux version 22.04 Jammy

#Prepare ubuntu
#open terminal
#use commnand for install DRBL server. Open the sources.list file to add the Clonezilla repository with this command:
  sudo nano /etc/apt/sources.list

#Add this line to the end of the file
  deb http://drbl.sourceforge.net/drbl-core drbl stable

#donwload GPG Key for unbuntu version Jammy
  deb http://archive.ubuntu.com/ubuntu jammy main restricted universe multiverse # (Or any Ubuntu mirror site near you)
  deb http://free.nchc.org.tw/drbl-core drbl stable

#Make sure the system is up to date:
  sudo apt-get update

#Configure network (optional)
  sudo apt-get remove network-manager

#Edit the interfaces file
  sudo nano /etc/network/interfaces

  #Loopback
  auto lo
  iface lo inet loopback
  #Network interface, must match your network
  auto eth0
  iface eth0 inet static
  address 192.168.1.53
  netmask 255.255.255.0
  gateway 192.168.1.1
  #Virtual Interface for Conezilla, make sure it is “class C” IP (192.168.x.x)
  auto eth0:0
  iface eth0:0 inet static
  address 192.168.100.100
  netmask 255.255.255.0

#use command for install DRBL
sudo /usr/sbin/drblsrv -i

#It asks us if we want to set a password for each time we clone a client, we say “N”.

#Do you want to set the pxelinux password for the clients so that when the client boots, a password must be entered to boot.
client boots, a password must be entered to boot (For more security)
[y/N] N

#I recommend choosing “Y” in the following question:
Do you want to use a graphical background for the PXE menu when the client boots?
Note.

#If you use the PXELinux graphical menu, but the client does not boot, you can switch to text mode by running
you can switch to text mode by running “/opt/drbl/sbin/switch-pxe-bg-mode -m text".
[y/N] Y

#Choose “N” at the next prompt:
#Do you want to use the DRBL server as a NAT server? If not, your DRBL client will not be able to access the Internet.
[y/N] Y

#Finally choose “Y”:
#We are now ready to deploy the files on the system!
#Attention! If you continue, your firewall rules will be overwritten during the installation...
[Y/N] Y

#Start Clonezilla Server
Now that we have finished configuring Clonezilla let's start it to begin cloning. Type this command:
  sudo /usr/sbin/dcs

#On the first screen choose “Select all the clients”.
