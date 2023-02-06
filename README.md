# RaspberryPi_Travel_Router
Ansible playbook for configuring a rasberry pi as a travel router that auto connects to VPN on boot.


# Introduction #
In this document we’ll show you how to edit the ansible playbooks to configure a Raspberry Pi as a travel router that auto connects to an OpenVPN Access Server. This guide was written with the assumption of living in the USA. Playbooks were developed and tested from an ansible control node running ansible [core 2.12.2] at the time of writing.
  # What's covered
    • How to create a bootable microSD card with Raspberry Pi OS.
    • How to configure and run these playbooks with your settings.
  # What's Not covered
    • How to setup an OpenVPN Server’s
    • How to setup your ansible control server (It just needs ansible & git installed)
  # You’ll need:
    • A Raspberry Pi (I used a Pi 3B+ and a 4b for testing)
    • A microSD card (8 GB or more recommended).
    • A USB dongle for your Pi (I’v used this one for a few years https://www.amazon.com/dp/B003MTTJOY)
    • A computer with a microSD card drive, or an SD card drive and a microSD card adapter. This computer will also need Raspberry Pi Imager installed.
    • Access to a server/service running OpenVPN & a downloaded copy of your client.ovpn file.
      ## This doc assumes you use username/password to auth to your VPN server. ##
    • An ansible “control node” (the machine that runs Ansible). To avoid issues following along with this, I would make sure you are running ansible core 2.12.2 or higher.
    • The Ansible community module installed on your control node.
      ansible-galaxy collection install community.general

# Install Raspberry Pi OS Lite SD card
The first step is to install Raspberry Pi OS Lite on your Raspberry Pi and connect it to the network. Since I don't like to disable host_key_checking in my ansible.conf file I add my ansible control server’s public key to my Pi OS when I image the SD card with pi imager.
Note: The steps given in this section will erase all existing content on your microSD card. If you already have Pi OS running on your Raspberry Pi you can skip the next section


1. Open Raspberry Pi imager
2. Select “Choose OS”
3. Select Raspberry Pi OS (Other)
4. Select “Raspberry Pi OS Lite”
5. Now Select “Choose Storage”
6. Select your SD card.
7. Now back at the main imager screen. Press “CTRL+SHIFT+X” to open the advanced menu
8. Enable SSH, Add the public key from your ansible control server and set your location. And click Save.
9. Select “Write” to write Pi OS to your SD card.
10. Wait for image to complete
11. Once complete,  un-mount the SD card and put in it your Raspberry Pi.


# Boot the Raspberry Pi
1. Hard wire your pi into your router.
2. Get its IP address from your DHCP server(or you can connect a monitor to it and see it at the login screen)
3. From your ansible control server try and ssh into the Pi (ssh pi@IP_ADDRESS). This will ensure you can connect to the pi from your control server as well as add its public key to your ansible server key store.
4.  Close the ssh connect to the pi (exit)
    1.  Clone down this repository and edit the playbooks.
    2.  Clone down this repository into a directory on your control server.
    3.  Update the inventory file with your raspberry pi’s IP to it.
    4.  Next copy your client.ovpn file to the “files” folder
        1.  rename this file to client.ovpn if its not called client.ovpn
        2.  I highly recommend you add your client.ovpn to your .gitignore file before you ever push this repo to your own repo
5. Update the tasks in roles/initial_setup/tasks to match your country & timezone.
   1. Verify you locale. vim roles/initial_setup/tasks/set_locale.yml.
   2. Verify your wifi country. vim roles/initial_setup/tasks/set_wifi_country.yml
   3. Set/Verify your timezone(optional). vim roles/initial_setup/tasks/set_timezone

# Running Ansible
1. From your control node and within the root folder of the cloned repo run the following command.
   1. ansible-playbook install_vpn -K --user pi -i inventory
2. Enter the default password for the pi user (raspberry)
3. Enter the desired username and password for your new user (this will replace the pi user)
4. Enter the username and password of the account you use to log into your VPN (this is to setup auto vpn login on boot)
5. Enter the ssid and passphrase for the wifi network you want your external devices connect to when you travel.
6. Enter the ssid and passphrase of the wifi network you want your Pi to connect to for internet.
   1. I'm using my old iphone7 hot spot in this example. You would just need to update /etc/wpa_supplicant/wpa_supplicant-wlan0.conf file when ever you need to connect to new wifi networks when you travel. I usually just do this via ssh since its quick.
        1. *wpa_passphrase {{ wan_ssid }} {{ wan_pass_phrase }} >> /etc/wpa_supplicant/wpa_supplicant-wlan0.conf*
 7. The playbooks take a 10-15 minutes to run though depending on how many OS updates there are.

# Helpful resources
1. https://docs.ansible.com/ansible/latest/index.html
2. https://www.raspberrypi.org/

# TODO
1. Add screenshots
2. Add TOC
3. Add more links to helpful resources
4. Refactor roles with handlers with 'block' blocks