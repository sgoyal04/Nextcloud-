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

### Set Up Docker, and Shell in a Box
1. Install Docker: `curl -sSL https://get.docker.com | sh`
2. Add user to the Docker group: `sudo usermod -aG docker {username}`
3. Install Shell in a Box: `sudo apt install shellinabox`
   
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
