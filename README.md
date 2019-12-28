qubinode-usb-imager
=========

The qubinode-usb-imager Ansible role builds a bootable usb disk to be used to a qubinode hosts

Requirements
------------

- rhel-server-7.6-x86_64-dvd.iso 

Role Variables
--------------

| Parameter | Default value | Description |
| --- | --- | --- |
| iso_name  | default = [ 'rhel-server-7.6-x86_64-dvd' ]  | name of the iso file with the iso extention  |
| ks_file | default = 'qubinode-rhel7.6.ks' | what do you want to name the kickstart file |
| packages | default = [ 'grub2-efi', 'shim', 'gdisk', 'grub2-efi-modules', 'grub2-efi-x64-modules' ] | required packages |
| qubinode_hostname | default = 'qubinode-box.example.com' | hostname for qubinode server |
| qubinode_ip_addr | | qubinode host default network ip address |
| qubinode_gw | | qubinode host default network gateway
| qubinode_nameserver_ip | default = '1.1.1.1' | DNS server for qubinode server |
| qubinode_net_dev | | qubinode network device(exanple: 'eno1')
| qubinode_user_pw | | qubinode host default qubi user password |
| qubinode_username | default = 'qubi'| qubinode admin user username |
| qubinode_user_fullname | default = 'Qubi Admin'| qubinode admin user full name |
| qubinode_netmask | | qubinode host default network netmask(example: '255.255.255.0) |
| iso_local_path | | location  of rhel-server-7.6-x86_64-dvd.iso (example: '/home/qubiuser') |
| root_pw | | root password for qubinode box
| usb_device | | example: '/dev/sdc' |
| ok_to_reboot | default = 'no' | reboot your workstation/host if partprobe fails |
| os_disk | default = 'sda' | the name of the first disk on your device where the os gets installed |

Example Playbook
----------------
```yaml
- hosts: localhost
  remote_user: root
  roles:
    - name: qubinode-usb-imager
      vars:
        rhel_release: '7.6'
        iso_name: 'rhel-server-7.6-x86_64-dvd
        iso_local_path: '/home'
        os_disk: sda
        usb_device: '/dev/sdb'
        root_pw: "$6$lzcUgJ886.GHT1IM$BtYRQltzadzbHtubxHC1li5yFbdvdkTeGnD2ex1H4VHwQoUGTz22UHyUondkHu/wG515sFuztuesrwC7s.Xkd/"
        qubi_pw: "$6$hDS1K0FLywm2VIHm$c3PP8Ko9eHxYS.Lk/gRtwYzQCBlm0otDpx7UlJDuTYeK0EtUG40kS/gXKgMAaZ71NavoEsCHTnamQVCuofQh1/"
        qubinode_net_dev: 'eno1'
        qubinode_ip_addr: '192.168.1.45'
        qubinode_nameserver_ip: '1.1.1.1'
        qubinode_netmask: '255.255.255.0'
        qubinode_hostname: 'qubinode-box.example.com'
        qubinode_gw: '192.168.1.1'
        ks_file: 'qubinode-rhel7.6.ks' 
        ok_to_reboot: no
```
License
-------

BSD

Author Information
------------------
Abner Malivert 
