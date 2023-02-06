Role Name
=========

Configures the DHCP server for guest access on your raspberry pi travel router.

Requirements
------------

None

Role Variables
--------------

to prevent possable DNS leaking, replace 1.1.1.1 in the set_dhcp_config.yml file to the IP of your VPN server.

Dependencies
------------

None

Example Playbook
----------------

    - hosts: raspberry_pis
      roles:
         - dhcpd_setup

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
