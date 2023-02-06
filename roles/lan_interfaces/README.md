Role Name
=========

Configures the LAN side WLAN interface on your raspberry pi travel router.

Requirements
------------

None

Role Variables
--------------
# The SSID and Passphrase of the WLAN you connect your devices to for internet access when you travel.
lan_ssid:
lan_pass_phrase:

Dependencies
------------

None

Example Playbook
----------------

    - hosts: raspberry_pis
      vars_prompt:
      - name: lan_ssid
        prompt: Enter ssid of lan wifi (the ssid the pi hosts for devices to connect to)
        private: no

      - name: lan_pass_phrase
        prompt: Enter the passphrase of the lan wifi (Passphrase you enter to connect TO THE raspberry pi)
        private: yes
        confirm: yes
      become: yes
      roles:
         - lan_interfaces

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
