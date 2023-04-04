# VPN
VPN and servers can be confusing, I am still confused by them today. Below are some notes that I have gathered.


## VPN
If you ever have an issue with a connection one of the 
common places to check is your `resolv.conf` file. 

### How?
In your terminal with your editor of choice open `resolv.conf`, if you do not have this file the editor will automatically create it. 

You will want to add the name-server of the site you're trying to reach. Example:
`nameserver 172.X.XX.X.X`

When not needed feel free to comment it out. Example:
`#nameserver 172.X.XX.X.X`


The system wont read it. Once you have made this change, 
you will want  to make sure that in your VPN client you 
go to the configuration settings and select something
 manual along the lines of "allow changes manually to
 network changes".

 ## External HardDrive 
 When you have to move files, for example a tarball you
 need to execute the following command:
 `tar -cvfz [NAME OF TARBALL].tar.gz [DESIRED LOCATION OF FILE]`

## Connecting To Servers 
Working on systems will have you ssh'ing into several 
machines. At times you will have to copy over tarballs
from one machine into yours or your desired external
storage device.

For this you will use the `scp` command. In some cases 
your machine will not have a direct path to your key when
you must list it out the command is as follows:
`scp -p 443 -i [PATH TO KEY]` This command lists the port 
also to copy and where the key is to connect to the server.

An example of copying contents from one server to an 
external hard drive would be:
`scp -p 443 -i ~/.ssh/[CERTIFICATE LOCATION] USERNAME@SEVERNAME:[LOCATION OF TARBALL][LOCATION WHERE YOU WANT IT COPIED]`

If you're lost on where to find the file path to your 
external drive (if thats where you want to push documents)

Mac: Open the Disk Utility in the /Applications/Utilities/ folder, click on the partition, choose Info, and look at the disk identifier. Example: `Volumes/"My Passport for Mac"

Linux: To be continued 

Windows: if you click on computer, then click the external
drive in question, at the top of the window it will show
you the path. Example: `C: Users\sunflowerno0b\USB


Yes, this is very unique and its not commonly found, 
normally you indicate the `scp` command connect to the 
server and location of where you want to contents copied. 

## 2FA Reset for OpenVPN
VPNs allow for secure access to certain sites for your 
systems team. For example some teams may need only 
internal members to access your git. Authentication to 
these VPN protected sites normally include: 

+ ssl certificate 
+ username & password
+ MFA

When MFA needs to be rest, you should always look at the 
documentation.  To rest the 2FA for a specific user using OpenVPN:

+ ssh into the VPN (1XX.XX.XXX.XX)
+ go into the root directory `cd /`
+ run `find / | grep sacli `
+  `cd` into the scripts folder
+ run `sudo ./scali -- user [USERNAME] --KEY "prop_google_auth" -- value "false" UserProPut`


Note that this will disable the google authenticator for 
the specific user.


+ run `sudo ./sacli -- user[USERNAME] -- lock 0 Google AuthLock` this will reset the Google Authenticator for the user to rescan upon signing in again. 


Further options can be explored [here](https://openvpn.net/vpn-server-resources/google-authenticator-multi-factor-authentication/)
## VPN & LDAP
When configuring VPN that will use your teams LDAP it is best practices for the username to match the LDAP profile 
when creating the user in admin. 

Should a user 
lose or replace phone
