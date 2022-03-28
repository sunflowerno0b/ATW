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

To check if my apple mini came with a NIC I ran `ip a` and this listed out a ton of jibberish on what my server had. I saw that it had an eth0 but nothing starting with a `w` which is what would indicate something relating to wifi. 