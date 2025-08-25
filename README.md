# Nextcloud Setup Guide
A comprehensive guide to setting up Nextcloud, including the initial Raspberry Pi setup.

## Hardware Requirements
1. Raspberry Pi
2. Computer
3. SD Card / USB / Hard Disk / SSD (willl refer to it as storage moving forward)

## Initial Setup for Raspberry Pi

### Installing Raspberry Pi OS on External Storage
1. Download and install the [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
2. Open Raspberry Pi Imager, choose your device, OS, and storage, then click "Next".
3. Select "Edit settings" from the pop-up window to configure your OS settings.
4. In the "General" tab, set your username, password, and Wi-Fi settings.
5. In the "Services" tab, enable SSH and select "Use password authentication" since we will be using Shell in a Box(incompatible with passkey).
6. Apply the OS customization and confirm to erase data on the external storage.
7. Eject the drive and connect it to your Raspberry Pi.

### Accessing the Raspberry Pi via SSH
1. Find the IP address of the Raspberry Pi from your router settings.
2. Use a terminal to access the Raspberry Pi using SSH and its IP address.
3. Terminal command: `ssh pi_name@pi_ip_address`
4. Confirm the connection by typing "yes" when prompted.
5. Enter the password you created during the Raspberry Pi OS installation.
6. Update the OS using the command: `sudo apt update && sudo apt upgrade -y`.

## Secure your Raspberry Pi

Since we are keeping this raspberry pi only on local network, the following should be enough to keep it secure:
### Disable unnecessary services
1. List all the services using the command: `systemctl list-unit-files --type=service`.
2. Disable the services you will not be using, command: `sudo systemctl disable --now <service_name>`.
### Install Fail2Ban
1. Install Fail2ban with the command: `sudo apt install fail2ban -y`.
2. Setup the config file for Fail2ban to block brut force attempts to three (or more if you want).
3. Navigate to the directory /etc/fail2ban/ using command: `cd /etc/fail2ban/jail.d`.
4. You will find only one file inside this folder, named: `defeault-debians.conf`, we can edit this file with: `bantime=36000` and in next line write `maxretry=3`. You can change this numbers according to your requirement.
5. Check if Fail2ban is running using command: `systemctl status fail2ban`.
6. If you get server ready and active, you are good.
7. Otherwise if you get an error: `Failed during configuration: Have not found any log file for sshd jail`, you need to install and rsyslog to create logs required for the Fail2ban.
8. Use the command: `sudo apt install rsyslog -y` to intall rsyslog.
9. Now enable this service using the command: `sudo systemctl enable rsyslog`.
10. Now restart the Fail2ban using the command: `sudo systemctl restart fail2ban`.
11. Try checking the status of Fail2Ban again and it should be running now and now your raspberry pi is secure against brut force attacks.
### Install UFW Firewall
1. Use the command: `sudo apt-get install ufw-y`, to install ufw firewall.
2. Block all incoming traffic using command: `sudo ufw defeault deny incoming`.
3. Allow all outgoing traffic(letting pi connect to internet and download updates etc) using command: `sudo ufw default allow outgoing`.
4. Allow connections using ssh through command: `sudo ufw allow ssh`.
5. Finally, enable the firewall using command: `sudo ufw enable`.

## Additional setup

### Set Up Docker, and Shell in a Box
1. Install Docker: `curl -sSL https://get.docker.com | sh`
2. Add user to the Docker group: `sudo usermod -aG docker <username>`
3. Install Shell in a Box: `sudo apt install shellinabox`.
4. Use the command: `sudo ufw allow from <subnet> to any port 4200 proto tcp` to enable shellinabox access from your subnet. By default ssh uses port 4200, to confirm use command: `sudo ss -tlnp | grep shellinabox`.
   
### Intall and setup portainer
1. Install Portainer by following the [deployment steps](https://docs.portainer.io/start/install-ce/server/docker/linux).
2. Open portainer using ip address of raspberry pi and port number that you used during earlier command.
3. Go to Setting > App templates > URL and add the url : https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v3-arm64.json

## Nextcloud Setup
1. After adding this template url, go to templates and search for Nextcloud and select it.
2. Create database password and MYSQL_ROOT_PASSWORD and select port number as 5443(can use some other port as well)
3. Enter url as https:<ip_Address>:<port_number> to access nextcloud.
4. Create a username and password of your choice.
5. Select MySQL/MariaDB from storage and database, add nextcloud as database user and password same as step 2 database password, database name should be nextcloud_db and databasehost should be nextcloud_db:3306 (you can confirm port number from your portainer- got to containers and for nextcloud_db go to quick actions first option adn read through the page to find the port number)
6. It is ready to use and you can go to files and create your own separate folder - to backup your computer files for example.
7. Install nextcloud on your laptop and run it and add server address of the pi same url as step 3.
8. You have to login using username and password you created during step 4.
9. Now you can choose the folder/drive of your laptop you want to backup in nextcloud. All the contents of the selected folder will be in sync with nextcloud.
10. You have succesffuly created your own private cloud storage to backup files from your laptop.

### Use the following commands to remove docker and volume:
1.`sudo docker stop nextcloud` - stop docker container. Replace nextcloud with your container name.
2.`sudo docker rm nextcloud` - remove docker container.
3.`sudo docker volume rm nextcloud` - remove volume.
4. `sudo docker volume ls` - check if volume is removed.

