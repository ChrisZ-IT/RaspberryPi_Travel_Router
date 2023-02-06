Role Name
=========

Removes the default 'pi' user on your raspberry pi travel router.

Requirements
------------

A new sudo user on the pi

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

    - hosts: raspberry_pis
      become: yes
      roles:
         - remove_default_user

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
