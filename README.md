# Nextcloud 
A file sharing server for personal cloud solution.

# Hardware requirement:
1. Raspberry Pi
3. Computer
5. SD Card / USB / Hard disk / SSD ( will refer as storage )

# Initial setup for Pi:
# Installing Raspberry OS on external storage using computer:
1. Download and install Raspberry Pi Imager from: https://www.raspberrypi.com/software/ 
2. Open Raspberry pi imager and choose your device, OS and storage and click next.
3. Select edit settings from the pop up window. (If you would like to configure your OS settings)
4. In general, set username and password and wifi.
5. In services, enable ssh and select use password authentication.
6. Apply the OS customization and select yes to erase data on the external storage.
7. eject the drive and connect your drive to the Raspberry Pi.

# Access the Raspberry Pi using SSH:
1. You can find the IP address of the pi from router settings.
2. Now use terminal to access raspberry using ssh and Ip address of the Pi
3. Terminal command: ssh pi_name@pi_ip_address
4. Say yes to want to continue connecting.
5. Enter the password you created during Raspberry Pi OS installation.
6. Update the OS using command: sudo apt update && apt upgrade.
   
