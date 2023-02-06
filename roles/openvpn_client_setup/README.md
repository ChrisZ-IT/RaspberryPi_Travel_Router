Role Name
=========

Configures rasbery pi's VPN client access to auto login on boot.

Requirements
------------

Need a VPN server, and a copy of your client.ovpn config file.

Role Variables
--------------

Copy the contents of your client's ovpn config file into the vpn_home.yml vars file.

Dependencies
------------

client.ovpn

Example Playbook
----------------

    - hosts: raspberry_pis
      vars_prompt:
      - name: vpn_username
        prompt: Enter your VPN's username 
        private: no

      - name: vpn_password
        prompt: Enter your VPN's Password
        private: yes
        confirm: yes
      roles:
         - openvpn_client_setup

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
 