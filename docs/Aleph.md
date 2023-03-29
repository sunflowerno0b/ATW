# Intro to Aleph
My organization needed to have a database repository in which journalist around the world could access and share documents surrounding findings about environmental matters. After a few discussions the service [Aleph](https://docs.alephdata.org/) was decided to be the option that we went with. I will detail the steps below- this will be long so sit back, and prepare to read.

In order to run Aleph it would be easiest to manage via an AWS EC2 instance. To perform the creation of the EC2 I did the following steps:

1) https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard: and select the server that you wanted- for this case I selected Ubuntu 20.05 LTS Server with the 64 bit x86. 

From there you are taking to step 2 out of 7 which is selecting the instance type. Here we have to see how many CPuS, RAM memory (GiB) would be need. I was confused about price so my friend mentioned that I can gather estimates from: https://calculator.aws/#/createCalculator/EC2 when using that page its easier to just type EC2 rather than the drop down menu because the services to get estimates on was endless. I selected the region to be US E. N Virginia - for no particular reason that a) at my old organization thats what they used b) we had another instance running there already and I wanted everything to be accessed at once. I then selected linux then ticked the search by instances by name - in this case `t3.medium`. I kept the utilization at 100% and the number of EC2 at 1. 

My friend explained that we have options for this, we could have auto scaling which means that there would be 3 instances so should one fail the other two could still keep the service running. But since this is just staging 1 would be enough for now. Total estimated cost per year would be 288USD.

Note: t2 and t3 medium offered the same options at the same price (or not that much difference in price) so I opted for t3 as it was newer.

I spoke to the Data person at my organization and he states that currently there is 25GB of data with room for plenty more. 

The next step (3) was configuring the instance details, at the juncture since its only 1 instance we need I left 1 as the instance count. I kept the network the same but made the subnet be subnet 1a, the reason for this is should this fail the subnet will provide redundancy.

I enabled auto-assign public IP, and I kept the rest f the configurations at defaults. 

Things to note:
- the IAM role used to give permissions to edit or modify was resources from within the instance.



-Shutdown behavior I left it at stop, not terminate because I don’t want anything deleted/
I also added protect against accidental termination because since I am a no0b- in the event I mess up, I don’t want all my work to be erased.
-For monitoring through Cloudwatch, I left this unchecked as most of the moniotorizat ion options that come basic are enough for this staging. 

Adding storage:
Here I needed to create thee volumes, by default AWS will create the root being dev/sda1 with a 8GB  not encrypted. I added encryption and kept things as is. I then added two new volumes, 1 for 8 GB which would be where Docker lives and another with 100gb where the data would live. All were encrypted.

For tags I created one which everyone should have at minimum which was NAME Aleph Staging.

The configuration of security groups is where you add your rules. We added three 1 ssh (port 22), 1 http port (80) and 1 for HTTPS(443). Once the instance is up, I will want to change the port that SSH listens on to reduce attack zone. I will also want to make custom changes to the IP here so that again the attack zone is minimized. Once I reviewed everything, I was able to launch the instance. AWS asked if I wanted to store my key or create a new one. AWS charges 10$/key (which is crazy) so I used the Pem file that was created in a previous issue from that contractor. Once I login, I can add my own key so that I do not have to use the generic key that we have for the other instance. On my instances page I was able to see the public IPV4 address, this allowed me to 

Now that the instance is up and running, I have to ssh into the system, format the disks, mount them permanently, download docker and follow the installation instructions for Aleph.

Formatting the disks:

I used the `fdisk -l` command to list all the disks that I have within my server. From there I was able to get the names of each of the disks, most online blogs and tutorials will have /dev/sdb1 as the default- but that was not the case for me. It was `nvme1n1` or some vacation of that for the three disks that I had. 

i ran `sudo mkfs -t ext4 [NAME OF THE PARTITION OR DISK]` then I verified that the file system was changed by running `lsblk -f` , my output was updated to ext4. 

https://phoenixnap.com/kb/linux-format-disk



Mounting permanently:

When mounting the disks that I created, as a refresher I have one of 8GiB and one of 10GiB- I have to select a mount point but this will roll out in several instances.

The mount point can be of any name. Most of the examples I found had weird names or led me down understanding the linux file system. I did have to understand the linux file system but I will explain that later.

To keep things simple I decided that I will create a mount point /data for the 100GiB. The command I ran to mount is `mount /dev/[VOLUME NAME] /data`. This will mount that disk to the mount point /data. To get the name of the volume data, I ran both `lsblk -l` & `df -h`. here I was able to read the output and ID each volume. 

Once it was mounted, if I reboot the volume would not be mounted and that would be a problem. So I need to mount permanently. To do that, I had to edit the `etc/fstab` file. The contents of the fstab file were minimal. Note: you have to run this as sudo. 

What you need to enter is something similar to the following:

`UUID=847bc509-b856-4a1e-9a01-c902bec56801       /scripts        ext4    defaults,ro     0       0`



To get the UUID for the disk I ran `sudo blkid /dev/[DISK NAME]`
for me I added the nofail rule. This will prevent the instance from starting if the disks cannot mount. Once that file was edited, I saved it and then I reboot the system. To check that it was mounted in the `/data` point I ran yet again `lsblk -l` and I saw the disk in question was mounted. I performed the same for the other disk but this should be discussed in depth as it relates with Docker. 

Docker by default writes to the /var/lib/docker. I created the mount point as /Docker by default docker would not see this and not write here. It would perhaps break. I had to unmount the disK I had mounted to point `/var/lib/Docker` then I ran `mv /var/lib/Docker/ /var/lib/docker`. I had already installed Docker within that mount point. I was scared that the docker config files did not cary over with the name change. I ran `sudo docker ps` and I had output that indicated the information carried over. 

Now to explain Docker. Since docker will write to /var/lib/docker , in the linux file system, that path is connected to the root /. When I created the instance, I had three volumes:
-root
-data
-docker 

so I had to make sure that the docker mount point was in the correct location so docker could run to the 10GB rather than the /file which was 8GB. The mount point in the `fstab` file pointed to /var/lib/docker. This ensures that my root stays clean and the 10GiB mounted to the path `/var/lib/docker` is what gets written to.


https://stackoverflow.com/questions/40118442/how-to-change-mountpoint-name


https://phoenixnap.com/kb/install-docker-on-ubuntu-20-04

Now that the disks were permanently mounted, docker installed I needed to look at the documentation to install Aleph. But on concern came to mind- what happens when our team exceeds the 100GiB, how do I increase the size of the volume. To increase the volume I went to my EC2 list, then clicked my instance ID, from there I went to storage. In storage I saw the volume size that I would be working with, this was the 100GiB. My friend said, as a test, let’s increase it to 101. I clicked the Volume ID, then on the new page I clicked actions and I saw Modify volume. Here I could change the size. I entered 101 and clicked modify. I needed to verify that this change was made via terminal. 


I left my current session nd re ssh’d into the machine. I ran `df -hT` as the documentation said- this did not help me. I ran `lsblk -l` and here I was able to see that it was 101 which is what I needed. 
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html?icmpid=docs_ec2_console



CHANGING PORT ON AWS

To change the port on aws, I needed to go into the instance `/etc/sshd_config` file. From there I needed to comment out the Port that I wanted to change it to. Afterwards, I needed to add the INBOUND rule to the security groups that I had for my instance. To do that, I went to my instance, clicked security group, deleted the default ssh 22 and added CUSTOM TCP, added my port number. Now I could run ssh -pXXXX [HOST NAME] but typing the port number each time would be annoying. So I had to edit my `/etc/hosts` file to add PORT XXXX. Once I saved my host file I was able to run `service sshd restart` and I opened a new terminal and I was able to ssh in. 

https://gist.github.com/tusharf5/89a094de01321880fdf44bf1d4e4ea4c


https://serverfault.com/questions/338077/basic-ssh-port-change-not-working-on-ec2-instance

ALEPH CONFIGURATION FILE:

working within the aleph.ev file one of the first configuration options was to set the secret key. I ran `openssl rand -hex 24` and pasted the output into the aleph.env configuration file. I then edited ALEPH APP tote to RIN Data and the slug to be rin_data. 

ELASTIC IP:
as it stands now if i stop and restart the service the IP assigned to the instance will change. This is an issue because I created an A/AAA record with a set IP. If the IP is always changing I will have to go into Linode and change the IP address in the A/AAAA record. To prevent this it would be easier to assign a static IP or in aws world whats called an elastic IP. To do this I went to the Networking & Security portion of my ec2 dashboard.
There I selected allocate Elastic UP address, I selected Amazons Pool of IPv4 addresses and added the tag for staging. After that I selected Allocate. Once the IP was addressed it had no name, I added the name Aleph staging. Then I clicked it and selected associate Elastic UP address. There was already one in use so I had to select the recently created one. After that the elastic IP was added. I then edited my `/etc/hosts` file because the IP was an old one, I changed it to the elastic IP address that I just generated. From there I also went into Linode and changed the A/AAA record to reflect the elastic IP address.

Something to know about elastic ip’s within AWS, so long as they are associated with an instance they are free. when they are not associated with on that is when you are charged. So if the service is no longer needed and has to be cut, a sysadmin must remember to disassociate the elastic ip. 

Also-since we have the name pulitzercenter.org that we pay for, it made no sense to pay 12 dollars a month to AWS to create the route53 record through their R53 wizard. This is why we went through A/AAA record as a subdomain, it would be cheaper to do.




ADDING MY SSH KEY TO THE AWS SERVER:
As of right now there was a pem file that I was using created by the contractor from other problems within aws to ssh in. What I wanted to do is to make sure that my set of keys could ssh in. So what I did:

ran `ssh-keygen -t rsa` 
entered the password and the name 
then i ran chmod 600 on the .pub file , I then opened vim to copy the information of the new key. I ssh’d into the server and I went to .ssh/authorized_keys, I opened the file and pasted the contents of my key there. I hit save. 

I then went back to my local machine and edited my /etc/hosts files to point my key instead of the generic ubuntu key on file. Then I was able to ssh in. 


ALEPH CONTINUED:
After associating the elastic IP on AWS- I made the change to the `/.ssh/config` file but my friend said that I could just now point it to the staging website. So I attempted to change the config file but when I ran the ssh command it still did not work. we wanted to make sure that the dns record was updated and pointing correctly. we went to https://dnspropagation.net, i entered the staging website and I was able to see where it was available. 

Then I attempted to SSH once more. It did not work and this is still a mystery to be solved.

install docker compose:
https://docs.docker.com/compose/install/
 


INSTALLING SWAG ON SEVER FOR ALEPH:

https://www.the-digital-life.com/webserver-linux/

The way I understand this at time of writing is that once we had the EC2 instance up, we had volumes / disks mounted to it and there was a CNAME attached to our server but there is essentially nothing on the server. In order to host the website we needed to install a web server within the server to support the docker compose images that we were installing. Thats when my friend showed me linuxserver/swag. It’s an all in one web server that provides items like fail2ban, ssl certsmand ngnix all in one docker image. With my lack of know how this seems to be the best idea as it would do what I needed and then some. I followed the video https://www.the-digital-life.com/webserver-linux/ to run the simple docker compose file. I made edits to the `PUID, TZ, URL & SUBDOMAINS` of my docker-compose.yml file. When I ran it it failed. I checked my ec2, it was up. I checked linode to make sure that the CNAME information was correct. I circled back to DNS propagate to ensure that was right.

In my local computer I ran `  nmap -Pn -p 80,443 rindata-staging.pulitzercenter.org` to check if the ports were open. They were. In my configuration file my friend realized that I had my URL as my subdomain and my subdomain as www, dont ask me why- it’s what the kind gentlemen in the video did so I copied. Additionally, the video only showed basic .yml file, I needed to add an additional option here `ONLY_SUBDOMINAS=true` to make sure that it did not generate a cert for the already certified domain. Once I made the URL my organizations main domain and the subdomain the staging url that I needed I ran `docker-compose up` and I was able to see that it was now working for the website. Granted it was just the swag landing page but this allowed me to see that everything was configured and I was now able to take that docker file and move it into the the service section of the Aleph docker file. 


https://docs.linuxserver.io/images/docker-swag here I could see all the other options that I could include, granted this is not so straight forward so I hope that this all makes sense. 


Side bar knowledge:
A proxy server speaks to the client to determine what site they want to visit. Here the credentials for HTTPS access are secured and the location of where the user wants to visit is made. Once the information is exchanged with the proxy server- the sever then talks to the web via HTTP (its assumed that this is secure) and obtains the information needed to redirect the client to the website that they want to visit.

NOTES ON CONFIGURATION OF THE NGINX, I was working within the default.conf

I had to add to the `server_name _.*;` to reflect the subdomain of my instance.

Then 

    location / {
        include /config/nginx/proxy.conf;
        include /config/nginx/resolver.conf;
        set $upstream_app ui;
        set $upstream_port 8080;
        set $upstream_proto http;
        proxy_pass $upstream_proto://$upstream_app:$upstream_port;

I had to make sure that these defaults stayed the same but I had to set the definition for $upstream_app to include the name of the service that was in my docker-compose.yml (The main one with all the services). To be ui, as listed in that docker file. I also had to see what port it was listening on and change the port number to reflect the same as that docker compose file. Additionally, I wanted to change the http to https but as we know that the proxy will talk to the web in unencrypted (we assume its secure) there was no need to change this. The last line uses the defined values in the line above to create the definition so nothing was needed to change. As we are only working with the ui for now I removed the other portions of the sample document. 

The same document that i pulled was from the nginx proxy-sites, there were loaded subdomain files which i used the structure for to create. 

When we ran docker-compose up, the site was running but it gave us a 500 error. When we looked at the logs, we were able to see that this was within the api and not the UI so this let us know that we have the UI working well. When i typed the staging website followed by /api I was able to get to the JSON file even though there was an internal server error.

Adding a user to Aleph:
I had to run docker-compose up in one terminal window, open another and dun docker pc to see the running container. As the docker was running I then ran docker exec -it [CONTAINER ID] bash. I wont lie, i went down all the services until the command `aleph create user ` worked. I had to run aleph —- help to see the options that I had for creating other users, once i did that- I was able to sign into Docker.

https://geekflare.com/run-commands-inside-docker/ 


After adding a user I needed to make sure that the service would not go down and would restart automatically without me having to run the `docker-compose up` to run the service aleph. In order to do that I needed to create a document within the `/etc/systemd/system` Once I created the `alpeh.service` file I needed to reload the systemctl with `systemctl daemon-reload`so that I could run the following commands 
`service aleph start` & `service aleph stop`. 



### Debugging why the notifications and alerts are not working for Aleph:
I created a new email account for the staging so that the `aleph.env` file would have the correct input within the alerts and notification section of the document. 

The first issue was that I made changes to the `aleph.env` file but I did not restart the service for those changes to take effect. In the previous section because I made changes to the `systemctl` I could now run `service aleph stop` & `service aleph start` to restart the Aleph. After doing that, I visited my staging website & tried to trigger an alert. Nothing happened. Went back to the `aleph.env` file & we saw that the TTLS & SSL set to `true` but the port that I had listed was 25. This creates conflict because port 25 by default is not encrypted. Yet, I had the encrypted variables set. I changed the port to 587 (a quick google search helped me for this: https://www.gmass.co/blog/gmail-smtp/) and restarted the service once more. Attempted and no luck. 

The logs needed to be looked at, to do this:

`docker logs -f config_api_1` & `docker logs -f config_ui_1`and also `docker logs -f config_worker_1`

These were the services that run with aleph, so I loaded up the browser- triggered the event and we saw nothing. I saw a prompt of the email that should have sent but it did not work.

*Learning point*:
when I was looking at the logs, I saw some components that are important to understand.
`POST` is an HTTP method
`GET` is what shows when you're getting information/data from the web, like when using a form.
HTTP 499, 200 these could be error codes or letting you know things are ok.
Then there will be numbers which show the size of the content.
After that, components of the web page like `svg` files, images etc.


I then went to Aleph's git page to see if similar issues had been faced and nothing matched exactly what I had. On the web, I went to settings ---> More Tools ---> web developer tools ---> Network Inspector. Once this was loaded I performed the same action of trying to get an alert or notification from the UI and I saw that it was a 502 bad gateway. 

 Next step is to reach out to Aleph directly. 

I heard back and they asked me if I had a mail sever set up. I checked it out and I realized that yet again I had conflicting information for my `alpeh.env` file. I changed my port to 465, tested the notification and checked the logs. There I saw that it was an TTLS was not configured. I changed that to `false` in my `.env` file and ran it again. I had an error on username and password, I amended my username to include the @[ORGNAME] and from there it worked! 

I also found this [link](https://docs.joomla.org/How_do_I_use_Gmail_as_my_mail_server%3F) to be more helpful. 

Once I was able to create my user and log into the system, I wanted to test out the notification settings to register a new user on the site. 

The registration email would come in but the link associated with the email pointed to an error / non existing page. I searched the github and checked for potential issues that another person may have faced. I found nothing. I reached out to the developers and at the moment they did not know how to configure it to stop giving the error. The issue was that the link was generating in one string that made no sense. Finally, a developer said that a `/` was missing. I needed to edit the `aleph.env` file. 

[INSERT PHOTO OF THE LINK]
I went into the .env file and edited the `ALEPH_UI_URL` variable and added the `/` at the end of my custom URL. From there, I restarted the aleph service so that these changes could reflect.
That resolved the link issue - a user could now register. 

Something to consider at this juncture:
With the registration link just open to anyone who has access to the link this poses a vulnerability to unwanted users registered & access to our data. 

## Setting up KeyCloak 
Looking at the statement above this is what lead me to keycloak. I wrote the developers asking about the cli command `aleph createuser`. I asked because the man page `aleph --help` showed only three commands but did not allow me to see all users or amend users. I wanted to control user access via the command line. When I wrote the developers, they admitted that the CLI tool is very bare bones and that [Keycloak](https://www.keycloak.org/) is what they used internally and what is recommend. 

First issue with this: I was reading Keycloak documentation it states that they use quay.io powered by RedHat. When I went to their github (yes,i am learning always go to the damn github) they listed jboss as the docker image to use. My friend suggested that we look at the last updates on each:

| Service | Last Updated                      |
|---------|-----------------------------------|
| Quay | 2 months ago                      |
| Jboss   | 3 months ago                      |
| bitnami | 11 hrs ago (from time of writing) |


Based on the figured above I am going to go with Bitnami. But I am jumping ahead, true to form thee was another issue. Apologies for this going back and forth. 

## Docker Space

Prior to speaking to my friend, I hadn't considered the update times. So I was going with the github and trying to install the image by running:

`docker run jboss/keycloak` this lead to a not enough space error 
[INSERT DOCKER NOT ENOUGH SPACE IMAGE]

My first thought was that I need to increase the size of the disk. I went into amazon and clicked on my EC2 instance. From there clicked on storage - selected the drive in question (after confirming the name within the server)and I updated the storage from 8GB to 10GB. To do that, click on the drive in question, then select actions, from there select modify storage.

I restarted the entire server with `sudo restart`. When it was up again, I restarted my docker `service docker start` & the aleph `service aleph start`. 

When I ran `df -hT` I saw that I was still at 8GB. I ran `lsblk` and I saw 10GB..confusion. My friend explained that I needed to update the partition because while I made the disk bigger, the partition still remained the same. 

I ran `docker system prune` this freed up a whopping 215 bytes of data. Not enough. 

I ran `service docker stop` & `service docker status` to verify that the service was inactive. Once confirmed I can now unmount the disk. I ran `umount /dev/nvme2n1` then `df -h` to make sure it was truly unmounted. Then I ran ` resize2fs /dev/nvme2n1` but I got the error that the server wanted me to check the fs with `e2fsck -f /dev/nvme2n1`. Finally, I ran `resize2fs /dev/nvme2n1` & `mount -a` to mount it back up and I saw with `df -h` that size was changed. I restarted docker & aleph. Now I can move to adding keycloak. 

## KeyCloak NGNIX File 
Right now Aleph is using port 8080. I cannot test keycloak within that port as its already in use. Once I amend my docker-compose.yml to add the keycloak components it will work.

On the back end I had to log into linode and duplicate the A/AAA record to match that of the staging record that we already had. That way that server understands when you reach that IP it can be pointing either to data staging or the keycloak staging. 

I created a keycloak .conf file that matches the aleph.conf file within the `site-conf` folder in `ngnix`. I ran `service aleph stop` and restarted - I went to my keycloak address only to see that there was a 502 error (my aleph service was working). I needed to add the subdomain to the `docker-compose.yml`Next, I decided to keep the postgres service for aleph and the postgres service for keycloak as two separate services within the docker-compose file.

I had to add several configurations after reading the bitnami documentation. At first I totally left out the post-gres information and the additional keycloak information.
```
postgres-keycloak:
    image: docker.io/bitnami/postgresql:11
    environment:
      # ALLOW_EMPTY_PASSWORD is recommended only for development.
      - ALLOW_EMPTY_PASSWORD=yes
      - POSTGRESQL_USERNAME=bn_keycloak
      - POSTGRESQL_DATABASE=bitnami_keycloak
    volumes:
      - 'postgres-keycloak-data:/bitnami/postgresql'

  keycloak:
    image: docker.io/bitnami/keycloak:15
    depends_on:
      - postgres-keycloak
    environment:
      #ADMIN_CREDENTIALS
      - KEYCLOAK_CREATE_ADMIN_USER=true
      - KEYCLOAK_ADMIN_USER=systems
      - KEYCLOAK_ADMIN_PASSWORD=[PASSWORD]
      - KEYCLOAK_MANAGEMENT_USER=manager
      - KEYCLOAK_MANAGEMENT_PASSWORD=bitnami1
      - KEYCLOAK_DATABASE_HOST=postgres-keycloak
      - KEYCLOAK_DATABASE_PORT=5432
      - KEYCLOAK_DATABASE_NAME=bitnami_keycloak
      - KEYCLOAK_DATABASE_USER=bn_keycloak
      - KEYCLOAK_DATABASE_PASSWORD=[PASSWORD]
      - KEYCLOAK_DATABASE_SCHEMA=public
      - KEYCLOAK_JDBC_PARAMS=sslmode=verify-full&connectTimeout=30000
```

Once I added these configurations I restarted aleph and I was able to access key-cloak.

Notes to add:
when testing the local docker you need to run `docker-compose  up` 

This was long & I will organize it better soon.