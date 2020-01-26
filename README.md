qubinode-usb-imager
=========

The qubinode-usb-imager Ansible role builds a bootable usb disk to be used to a qubinode hosts

Requirements
------------

- RHEL Server ISO


Download ISO
------------
* [Red Hat Enterprise Linux 7.6 Binary DVD](https://access.redhat.com/downloads/content/69/ver=/rhel---7/7.6/x86_64/product-software)
* [Red Hat Enterprise Linux 7.7 Binary DVD](https://access.redhat.com/downloads/content/69/ver=/rhel---7/7.7/x86_64/product-software)
* [Red Hat Enterprise Linux 7.8 Beta Binary DVD](https://access.redhat.com/downloads/content/69/ver=/rhel---7/7.8%20Beta/x86_64/product-software)

Creating SHA-512 password for qubinode_user_pw and root_pw
------------
```
mkpasswd --method=SHA-512
```

Role Variables
--------------

| Parameter | Default value | Description |
| --- | --- | --- |
| iso_grub_dir  | default = [ '/rhel-server-7.7-x86_64-dvd.iso' ]  | set ISO variable in qubinode kickstart file  |
| rhel_version  | default = 7.7 | set RHEL Version  |
| ks_file | default = 'qubinode_rhel77.ks' | set KS variable in qubinode kickstart file |
| ks_file_dir   | default = '/{{ ks_file }}'   |  set KS variable directory  |
| packages | default = [ 'grub2-efi', 'shim', 'gdisk', 'grub2-efi-modules', 'grub2-efi-x64-modules' ] | required packages |
| qubinode_hostname | default = 'qubinode-box.example.com' | hostname for qubinode server |
| set_static_ip  | true  | Configures machine with static ip  |
| qubinode_ip_addr | | qubinode host default network ip address |
| qubinode_gw | | qubinode host default network gateway
| qubinode_nameserver_ip | default = '1.1.1.1' | DNS server for qubinode server |
| qubinode_net_dev | | qubinode network device(exanple: 'eno1')
| qubinode_netmask | | qubinode host default network netmask(example: '255.255.255.0) |
| root_pw | | root password for qubinode box
| usb_device | | example: '/dev/sdc' |
| enable_gnome_desktop  | false  |  Set to true if you would like to install gnome desktop.  |
| qubinode_user_pw | | qubinode host default qubi user password |
| qubinode_username | default = 'qubi'| qubinode admin user username |
| qubinode_user_fullname | default = 'Qubi Admin'| qubinode admin user full name |
| ok_to_reboot | default = 'no' | reboot your workstation/host if partprobe fails |
| os_disk | default = 'sda' | the name of the first disk on your device where the os gets installed |

Example Playbook for Generic Server
----------------
```
- hosts: localhost
  remote_user: root
  roles:
    - name: qubinode-usb-imager
      vars:
        rhel_version: 7.7
        os_disk: sda
        usb_device: '/dev/sdb'
        root_pw: "$6$lzcUgJ886.GHT1IM$BtYRQltzadzbHtubxHC1li5yFbdvdkTeGnD2ex1H4VHwQoUGTz22UHyUondkHu/wG515sFuztuesrwC7s.Xkd/"
        qubinode_user_pw: "$6$hDS1K0FLywm2VIHm$c3PP8Ko9eHxYS.Lk/gRtwYzQCBlm0otDpx7UlJDuTYeK0EtUG40kS/gXKgMAaZ71NavoEsCHTnamQVCuofQh1/"
        set_static_ip: true
        qubinode_username: 'qubi'
        qubinode_net_dev: 'eno1'
        qubinode_ip_addr: '192.168.1.45'
        qubinode_nameserver_ip: '1.1.1.1'
        qubinode_netmask: '255.255.255.0'
        qubinode_hostname: 'qubinode-box.example.com'
        qubinode_gw: '192.168.1.1'
        iso_grub_dir: '/rhel-server-7.7-x86_64-dvd.iso'
        ks_file: 'qubinode-rhel77.ks'
        ok_to_reboot: no
```

Playbook for Super Micro Server with X11SDV-8C-TP8F motherboard
----------------
```
- hosts: localhost
  remote_user: root
  roles:
    - name: qubinode-usb-imager
      vars:
        rhel_version: 7.7
        usb_device: '/dev/sdb'
        os_disk: sda
        root_pw: "$6$lzcUgJ886.GHT1IM$BtYRQltzadzbHtubxHC1li5yFbdvdkTeGnD2ex1H4VHwQoUGTz22UHyUondkHu/wG515sFuztuesrwC7s.Xkd/"
        qubinode_user_pw: "$6$hDS1K0FLywm2VIHm$c3PP8Ko9eHxYS.Lk/gRtwYzQCBlm0otDpx7UlJDuTYeK0EtUG40kS/gXKgMAaZ71NavoEsCHTnamQVCuofQh1/"
        set_static_ip: false
        qubinode_username: 'qubi'
        qubinode_net_dev: 'eno1'
        qubinode_ip_addr: ''
        qubinode_nameserver_ip: ''
        qubinode_netmask: ''
        qubinode_hostname: 'qubinode-box.example.com'
        qubinode_gw: ''
        iso_grub_dir: '/rhel-server-7.7-x86_64-dvd.iso'
        enable_gnome_desktop: false
        ks_file: 'x11sdv-8c-tp8f.ks'
        ok_to_reboot: no
```

Known Issues
------------

If you try to mount the data volume and encounter an error like this.

```
mount: wrong fs type, bad option, bad superblock on /dev/xxx
```

Using the device sdb2 as an example, run the following commands to resolve.

```
xfs_repair -L /dev/sdb2
xfs_admin -U generate /dev/sdb2
```

License
-------

BSD

Author Information
------------------
Abner Malivert
