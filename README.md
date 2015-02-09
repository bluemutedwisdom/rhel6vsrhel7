## Difference between RHEL6 and RHEL7

*Feature* | *RHEL 6* | *RHEL 7*
--- | --- | ---
First process | upstart (init) | systemd
Default filesystem | ext4 | xfs
Kernel version | 2.6.* | 3.10.*
Bootloader | Grub 0.97 | Grub 2
Firewall | iptables | firewalld
Network bonding | Bonding | Teaming
NTP | ntpd | chrony

### Recover lost root password
    - press in grub menu (e)
    - goto the line that starts with linux16 and append
    rd.break console=tty0
    - press ctrl+x to boot
    mount -o remount,rw /sysroot
    chroot /sysroot
    passwd root
    touch /.autolabel
    exit
    exit
### SystemD
Starting and stopping services

    - systemctl start httpd.service
    - systemctl stop httpd.service

Enabeling and disableing services

    - systemctl enable mariadb.service
    - systemctl disable mariadb.service

Masking and unmasking services. After masking a service you cannot enable it. if you need to enable a masked services you need to unmask it first.

    - systemctl mask iptables
    - systemctl unmask iptables

Change target in userspace. A target is something like runlevel

    - systemctl isolate multiuser.target # this will give a console
    - systemctl isolate graphical.target # this will give a gui

Change target persistant.

    - systemctl set-default multiuser.target
    - systemctl set-default graphical.target
