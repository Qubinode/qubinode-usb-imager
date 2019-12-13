Role Name
=========

qubinode-usb-imager builds bootable usb used to install RHEL 7 on a qubinode hosts

Requirements
------------

You will need to download the rhel-server-7.6-x86_64-dvd.iso from access.redhat.com

Role Variables
--------------

| Parameter | Choices/<span style="color: blue;">Default</span> | Comments |
| --- | --- | --- |
| Content Cell  | Content Cell  | |
| Content Cell  | Content Cell  | |


Example Playbook
----------------

always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------
Abner Malivert (idtff)
