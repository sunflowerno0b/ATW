## Server Relocation
I found myself having to relocate. This means the current DHCP settings that I had in the router that I could control are going out the window. To break that down I was able to log into my parents router and assign myself a specific IP so that when I SSH into my server I do not have to worry about the IP address changing. 

#### What is SSH?
SSH stands for secure shell or secure socket. Its a cryptographic network protocol that allows two computers to communicate and share data. When SSHing into a server the command syntax will typically follow this structure:

`ssh [username]@[IP Address or hostname] `

The default port for SSH is normally 22, because this is common knowledge for security reasons its better to change the open port to another number so that it restricts access. If you opt to change the port number there is an argument that you have to include within your command.

`ssh -p [port number] [username]@[IP Address or hostname]`

Finally, sshing to a port for the first time (or more) will ask you for a key, you can refer to my post [rsa$config](https://sunflowerno0b.github.io/ATW/rsa%20%26%20config/). If you need to specify a specific key the command will change to:

`ssh -p [port number] -i [path/to/key] [username]@IP Address or hostname]`

### Sever VS Wifi
The servers that I have worked with have always been either 
- connected via ethernet
- cloud based (in which the service provider handles the connection)

With my current living situation I could not connect an RJ45 from the router to my server :( so I had to do it via wifi. I will go through the steps that I took to get there. I asked around my network of folks and no one knew how to connect a server to Wifi. 

My first steps from some reading:
- determine if my apple mini came with a NIC (network interface card). This would speak to the router in the house and get me connected 
- if it didn't, purchase a network adapter

To check if my apple mini came with a NIC I ran `ip a` and this listed out a ton of jibberish on what my server had. I saw that it had an eth0 but nothing starting with a `w` which is what would indicate something relating to wifi. I saw nonthing that looked close to that. That meant I had to by my adapter.

Pro tip: ensure that the adapter is Linux compatible. I purchased [this](https://www.amazon.com/dp/B01GC8XH0S/ref=cm_sw_r_cp_api_i_RBWCZH5X5KAMB2PYKH91?_encoding=UTF8&psc=1). 

## Setting up the Server
Warning: you will need to connect the server  to LAN before you can connect to via the adapter. I asked if I could use a port on the router for a few hours. With that I was able to install `NetworkManager`. I found out later that network manager is older than netplan and I ended up using netplan anyway. 

I connected to LAN and then while in `root` I executed the command that came with the adapter from the vendor.

`sh -c 'wget deb.trendtechcn.com/install -O /tmp/install && sh /tmp/install'`

From there I went into the `/etc/netplan/` folder and then created `test.yaml`. From there I made the following configurations:


```
network: 
   vesion: 2
   renderer: NetworkManager
   wifis:
     w1x0ccf896ddf26:
     dhcp4: no
     addresses: []
     gateway4: []
     nameservers:
       addresses: []
       access-points:
         SSID:
          password:

```

That's a lot, let me break it down. The first three lines are there because they have to be - it sets the stage for `netplan` to read it.

For wifis the `w1x0cc...` that was the name of the adapter I had plugged in. I got this ID by running `ip a`. If you're lost, you can unplug and run the command, then plug the adapter and replug it in. You will see the different item and use that as your ID. 

For `dhcp4:` you can keep it as yes, but because this is a sever I wanted a static IP so that I could always access it because I like to use an alias for ease of use (this is configured in the `hosts` file)

In the `addresses` field I put the DHCP static IP followed by the /24. Including the brackets.
`Gateway` was the LAN IP of the router, probably going to be` 192.168.1.1`

For the `nameservers` I used cloud flare as that is reliable but you can use anything you like - so long as its reliable.

Under `access-points` I changed the SSID variable to my wifi name. Note: if you have spaces in your wifi name, wrap it with "  ` ". Then I entered the WPA2 credentials. 

After that I ran `netplan generate` this would pull up any errors. I had to run this a few times as I had some syntax issues. I then ran `netplan apply` to have the `test.yaml` settings apply. 

Note: it has to be `.yaml` not `.yml`. 

After that I had ***zero*** idea if it would work. I ran a `ping google.com` and started seeing packet transfers and I knew I was connected. 

I then went into my machine and attempted to SSH in, after changing my `/etc/hosts` file to the new IP. And I was able to get in. 

I used this [video](https://www.youtube.com/watch?v=Dacn58kgMXA) for reference. I hope you found this helpful. 


