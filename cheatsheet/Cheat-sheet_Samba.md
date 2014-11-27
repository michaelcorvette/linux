#Samba on CentOs 7.0 - Michaël Corvette
[bron](http://www.howtoforge.com/samba-server-installation-and-configuration-on-centos-7)

| Command | Explanation |
|--------|--------|
|yum install samba samba-client samba-common| Installation|
|vi /etc/samba/smb.conf| Change configuration|
|mkdir -p /samba/anonymous| make directory for anonymous share|
|systemctl enable smb.service| enable smb |
|systemctl enable nmb.service| enable nmb |
|systemctl restart smb.service| restart smb|
|systemctl restart nmb.service| restart nmb|
|firewall-cmd --permanent --zone=public --add-service=samba| set the firewall|
|firewall-cmd --reload| restart firewall|
|groupadd smbgrp| add the group for secure share|
|useradd srijan -G smbgrp| add the user|
|smbpasswd -a srijan| set password|
|mkdir -p /samba/secured| create folder for secure share|
|cd /samba| change directory|
|chmod -R 0777 secured/| set permissions|
|chcon -t samba_share_t secured/| set security context|
|vi /etc/samba/smb.conf| edit configuration|
|systemctl restart smb.service| restart smb|
|systemctl restart nmb.service| restart nmb|
|testparm| check an smb.conf configuration file for internal correctness|


