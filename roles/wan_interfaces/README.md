Role Name
=========

Configures the WAN side WLAN interface on your raspberry pi travel router.

Requirements
------------

a USB wlan device.

Role Variables
--------------
# SSID & passphrase of the wlan network you connect your pi to
wan_ssid:
wan_pass_phrase:

# The MAC address of your usb wlan adapter
ansible_facts.wlan0.macaddress:

Dependencies
------------

None

Example Playbook
----------------

    - hosts: raspberry_pis
      vars_prompt:
      - name: wan_ssid
        prompt: Enter ssid of wan wifi (the ssid the pi connects to for internet)
        private: no

      - name: wan_pass_phrase
        prompt: Enter the passphrase of the wan wifi (the passphrase of the wifi your pi connects to for internet)
        private: yes
        confirm: yes
      gather_facts: true
      become: yes
      roles:
         - wan_interfaces

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
