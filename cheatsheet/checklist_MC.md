# Labo 3: Troubleshooting checklist
---


- `systemctl list-units --type service|grep 'httpd\|mariadb\|firewalld'`

- `systemctl list-units --type service`

- `ip a`, `https://'IP-Address'`

- `gedit /etc/sysconfig/network-scripts/ifcfg-enp0s3`
- Change these settings:
          - BOOTPROTO="static"
          - IPADRR=192.168.56.14
          - NETMASK=255.255.255.0
          - NM_CONTROLLED=no
          - ONBOOT="yes"
- `systemctl restart network.service`
- `ip a`

- firewall-cmd --permanent --zone=public --add-service=http 
- firewall-cmd --permanent --zone=public --add-service=https
- firewall-cmd --reload

- `sudo gedit /var/www/html/test.php`
- `<?php phpinfo(); ?>`
- Save and close `test.php`
- `http://IP-Address/test.php`
- `sudo rm /var/www/html/test.php`

- `sudo yum install httpd` (install service)
- `sudo systemctl start httpd.service` (start service)
- `sudo systemctl enable httpd.service` (start service at boot of machine)

- `sudo yum install php php-mysql` (install service)
- `sudo systemctl restart httpd.service` (restart service)

- `sudo yum install mariadb mariadb-server` (install service)
- `sudo systemctl start mariadb` (start service)
- `sudo mysql_secure_installation` > `Enter` > <br>
              `Enter password` > `Re-enter password` > `Enter`
- `sudo systemctl enable mariadb` (start service at boot of machine)



