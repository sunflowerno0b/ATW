## RSA & CONFIG

In systems administration much of the work performed requires the sysadmin to ssh into a machine. Organizations, if prudent will need the users RSA keys in order to provide secure authentication. RSA works under asymmetric encryption with the user generating a private & a public key pair. These keys are later stored in locations such as github, gitea etc. 

## Generating an RSA key 

Reading material [here](https://piechowski.io/post/how-to-use-openssl-genpkey-rsa/)

## .ssh/ Config

The .ssh directory includes files used for secure shell protocol. It's a cryptographic network protocol for operating network services securely over an unsecured network.

There will be times where the systems team makes changes to the security infrastructure. Changes can include but are not limited to:

* changing HA Proxy rules 
* updates to the bastion
* VPN updates 
* IP address changes 

