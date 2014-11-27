# Checklist Samba
---
1.  In the directory in which you store your `smb.conf` file, run the command `testparm smb.conf`. If it reports any errors, then your smb.conf configuration file is faulty:
    1. /etc/samba or in /usr/local/samba/lib
1. Check firewall
    1. iptables -L -v, ipchains -L -v
1. Run the command `smbclient -L hostname` on the UNIX box. You should get back a list of available shares
	1. Error with: `"bad password"`
    	- either an incorrect hosts allow, hosts deny, or valid users line in your smb.conf
        - or your guest account is not valid
        	- Check what your guest account is using testparm,temporarily remove any hosts allow, hosts deny, valid users, or invalid users lines
    1. Error with: `"connection refused"`
    	- then the smbd server may not be running
        	- If you installed it in inetd.conf, then you probably edited that file incorrectly
            - If you installed it as a daemon, then check that it is running and check that the `netbios-ssn port` is in a `LISTEN` state using `netstat -a`
    1. Error with: `session request failed`
    	- the server refused the connection
        - If it says `“Your server software is being unfriendly,”` -> probably invalid command line parameters to smbd, or  problem with startup of smbd. Check your config file (`smb.conf`) for syntax errors with testparm and that the various directories where Samba keeps its log and lock files exist
    1. Possible cause for failure of this test  -> subnet mask and/or broadcast address settings incorrect.
    	- Check that the network interface IP address/broadcast address/subnet mask settings are correct and that Samba has correctly noted these in the `log.nmbd` file
1. Run the command nmblookup -B hostname `__SAMBA__`. You should get back the IP address of your Samba server.
	- If you do not, then nmbd is incorrectly installed. Check your `inetd.conf` if you run it from there, or that the daemon is running and listening to UDP port 137
1. Run the command `nmblookup -B CLIENTname '*'`
	- You should get the PC's IP address back
1. Run the command `nmblookup -d 2 '*'`
1. Run the command `smbclient //Servername/TMP`. You should then be prompted for a password: password unixbox. If you want to test with another account, then add the -U accountname option to the end of the command line for example, smbclient //bigserver/tmp -Ujohndoe.
1. On the PC, type the command net view \\BIGSERVER. You should get back a list of shares available on the server. If you get a message network name not found or similar error, then NetBIOS name resolution is not working. This is usually caused by a problem in nmbd
1. Run the command net use x: \\BIGSERVER\TMP. You should be prompted for a password, then you should get a command completed successfully message. If not, then your PC software is incorrectly installed or your smb.conf is incorrect. Make sure your hosts allow and other config lines in smb.conf are correct
1.Run the command nmblookup -M testgroup where testgroup is the name of the workgroup that your Samba server and Windows PCs belong to. You should get back the IP address of the master browser for that workgroup
1. Browse to your server
