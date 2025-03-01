# Nextcloud Setup Guide
A comprehensive guide to setting up Nextcloud, including the initial Raspberry Pi setup.

## Hardware Requirements
1. Raspberry Pi
2. Computer
3. SD Card / USB / Hard Disk / SSD (referred to as storage)

## Initial Setup for Raspberry Pi

### Installing Raspberry Pi OS on External Storage
1. Download and install the [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
2. Open Raspberry Pi Imager, choose your device, OS, and storage, then click "Next".
3. Select "Edit settings" from the pop-up window to configure your OS settings.
4. In the "General" tab, set your username, password, and Wi-Fi settings.
5. In the "Services" tab, enable SSH and select "Use password authentication".
6. Apply the OS customization and confirm to erase data on the external storage.
7. Eject the drive and connect it to your Raspberry Pi.

### Accessing the Raspberry Pi via SSH
1. Find the IP address of the Raspberry Pi from your router settings.
2. Use a terminal to access the Raspberry Pi using SSH and its IP address.
3. Terminal command: `ssh pi_name@pi_ip_address`
4. Confirm the connection by typing "yes" when prompted.
5. Enter the password you created during the Raspberry Pi OS installation.
6. Update the OS using the command: `sudo apt update && sudo apt upgrade`.

### Optional - Setting Up Portainer, Docker, and Shell in a Box
1. Install Docker: `curl -sSL https://get.docker.com | sh`
2. Add user to the Docker group: `sudo usermod -aG docker {username}`
3. Install Portainer by following the [deployment steps](https://docs.portainer.io/start/install-ce/server/docker/linux).
4. Install Shell in a Box: `sudo apt install shellinabox`
