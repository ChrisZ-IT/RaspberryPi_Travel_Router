Role Name
=========

Inital raspberry pi travel router OS baseline setup.

Requirements
------------
None

Role Variables
--------------

None

Dependencies
------------

Designed to work with the other roles on this repo

Example Playbook
----------------

    - hosts: raspberry_pis
      vars_prompt:
      - name: new_user_username
        prompt: Enter new user's Username
        private: no

      - name: new_user_password
        prompt: Enter new user's Password
        private: yes
        encrypt: sha512_crypt
        confirm: yes
        salt_size: 7
      roles:
         - inital_setup

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
