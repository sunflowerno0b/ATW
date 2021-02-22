## Docker
On my journey, I learned that my organization makes use of Docker often. Here are my notes on the tool.

## Why use it ?
Sometimes OS’s and services are not compatible which leads to issues libraries , OS, & dependencies will not work.  

Docker runs components, dependencies in its own containers. Just had to build the docker configuration once. 

Containers are completed isolated environments, they can have their own network interfaces, etc but they all share the same OS kernel. 

Docker uses LX C containers. 

OS have two things, an OS kernel and a set of software. the OS kernel interacts with the underlying hardware. Its the software above the OS kernel that makes them different. 

Sharing the kernel, what does that mean? Docker can run any OS so long as they are on the same kernel. 

Each docker container has the additional software that makes these OSs different. 

You will not be able to run a window based container with an OS kernel. 

When you install Docker on windows you work linux on linux vrutal machine on windows. 

Unlike hypervisors, its not meant to run different OSs, dockers package and ship them anywhere any time as many times as we want.

Docker installs on the OS. 

Utilization is used higher disk space, CPU space when you use a virtual machine. Docker allows it to boot up in seconds.

Docker has less isolation as more resources are shared. 


You can see Docker hosted on virtual docker.

Products are containerized. ‘

If you need to run multiple you could, you just need to remember to add a front load balancer. If one fails you can delete it and redownload it.


