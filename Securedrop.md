# SecureDrop
At my current role, I am a SecureDrop (SD) admin. It was not known to me how intense this role would be and all the terminal jargon I would have to know.
Because of this, I will also store here and share tips and tricks that I have learned throughout my 3 years working with the tool. 

## What is it?
SecureDrop is an open source whistleblower submission system that media organizations and NGOs can install to securely accept documents from anonymous sources. It was originally created by the late Aaron Swartz and is now managed by Freedom of the Press Foundation. SecureDrop is available in 20 languages. More info can be found 
[here](https://securedrop.org/).

For my day-to-day I check SD for anonymous submissions of potential news story leads. 

## How does it work? 
### Tails
I will be limiting this section for security reasons. SecureDrop works with the 
The Amnesic Incognito Live System (tails). It’s an OS system, similar to Linux, MacOS & windows. The beauty of it is that it boots from a USB, and wipes itself clean after each use. It works only with TOR browsers. Arguably considered the most way to secure yourself on the internet. Check out more on tails 
[here](https://tails.boum.org/index.en.html).
Tails works in conjunction with tor browsers that use .onion websites. Info on tor [here](https://www.torproject.org/)

### The Computers
There is an **Admin Station** & there is a **Secure Viewing Station (svs)**. The admin station has access to the internet, where I use tor to access ".onion" sites. I pull attachments from said sites, load them to an encrypted USB. This USB is then taken to the SVS. Both machines utilize tails exclusively. 

The SVS is not connected to the internet. With the encrypted USB drive and another tails USB, the system boots. From there the contents of submissions and such are able to be viewed. The backbone of security for viewing submissions relies on long pass-phrases & PGP, check out the PGP documentation in my git for more on that. 

# Maintenance of SD
Being a sysadmin for SD requires understanding of the command line, SSH with sever(s), and the role of each USB. FPF attempts to make it easy with GUI options but I can attest that this does not always work.
## Command line
When updating and you don’t see it working with the gui

## V2 & V3 Upgrade
Recently it was announced that the support for V2 onions would cease. Earlier I mentioned onion (tor browsers). Check back there in case you need a refresher. This leaves V2 running instances vulnerable, eliminate the vulnerability by switching to V3. 

## Steps
### Verify ssh config files for Mon and App (your servers)
Every securedrop instance will have the Admin USB and the Journalist USB, for any major configurations to SD, it will run from the admin USB only. 

First, open the terminal navigate to the SD directory- enter `cd ~/Persistent/securedrop`  then verify that 
in servers (app & mon) have the files for ssh, they are titled `app-ssh-ths` & `mon-ssh-ths`. If they are there, excellent. If not, contact FPF support **ASAP**.

### Check your git status
Within the same `cd ~/Persistent/securedrop`, enter `git status`. This will have the output of where the `head detached at x.x.x`. You want to make sure that its at the lastest version. 


### Verify what servers app & mon are connected to
Again, within the same directory type this command `cat ~/Persistent/securedrop/install_files/ansible-base/app-source-ths`. After this command is run there is a secret URL that should be displayed here. When I say secret its a URL made of tons of letters- this is **not** to be shared. In my case there was not a secret URL it was a plain IP address not good. What to do? Reconfigure the servers.

Run `ssh -vvv app` `ssh -vvv mon`. This will produce a verbose output of the debug as its attempting to connect with the servers. Note that this point for me nothing was really showing beyond it not connecting. After that  you have to reconfigure your admin USB stick. 

To reconfigure type `./securedrop-admin sdconfig`. As a reminder this is all within the `~Persistent/securedrop` directory. The sdconfig gets all the configurations ready to send to the servers. It will provide with an interactive CL prompt where you will go through a series of questions. In this section, we also pay close attention to the questions on enabling or disabling V2, V3. Be sure to click yes for V3. Keeping V2 on is optional, but less secure. After that completes, you can type `cat ~/.ssh/config`. This will show the ssh configuration file, and we ***should*** see the private onion URL rather than the plain IP address we were seeing earlier. 

### Test ssh Connection 
To test your ssh connection to the severs enter `ssh app` & `ssh mon`. If your terminal switches to app@XXXX then you've successfully SSH'd. 

### Back up the admin stick
It's good practice to create back ups of the admin stick/ journalist stick(s) in case something goes wrong during an upgrade you can always roll back. To do that enter `./securedrop-admin backup`. This command creates a tarball for the current settings. This will take a while, do not fret. 

### Pushing the Configurations to the Servers
So everything that was done so far was only done locally within the tails/admin USB. The severs have no idea, and they are still operating under the old configurations. To make sure the servers have the correct configurations installed you should do the following. 

Run `./securedrop-admin sdconfig` <-- applies the changes locally once more 
Run `./securedrop-admin install` <-- this will send the configurations made in the step above to the servers. 

### End
I would ensure that you still have ssh capabilities. See above. And finally I would make sure that you have access to both of your instances. If you enabled V3, there should be a new link you should take note of which will appear as you access the source and journalists interface on the tor browser!


