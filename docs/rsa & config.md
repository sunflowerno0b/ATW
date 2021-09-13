## RSA & CONFIG

In systems administration much of the work performed requires the sysadmin to ssh into a machine. Organizations, if prudent will need the users RSA keys in order to provide secure authentication. RSA works under asymmetric encryption with the user generating a private & a public key pair. These keys are later stored in locations such as GitHub, gitea etc. 

## Generating an RSA key 

Reading material [here](https://piechowski.io/post/how-to-use-openssl-genpkey-rsa/)

## .ssh/ Config

The .ssh directory includes files used for secure shell protocol. It's a cryptographic network protocol for operating network services securely over an unsecured network.

There will be times where the systems team makes changes to the security infrastructure. Changes can include but are not limited to:

* changing HA Proxy rules 
* updates to the bastion
* VPN updates 
* IP address changes 

## Potential Problem

User at my org was attempting to ssh into a machine but was getting an
`UNREACHABLE! => {"changed"}: false, "msg": "Failed to connect to the host via ssh: ssh: connect to host XXX.XX.X.XXX port 22: COnnection timed out", "unreachable": true}` 

## Solution Thought Process
First, I realized this user had been out for about two weeks, perhaps their key expired & needed updating. This was not the case; they key the user was using was the team key for a generic user, not specific. 

I had to attempt to recreate the issue (note my friend guided my hand through all this, always grateful for you♡).

I asked user to attempt connecting but directing ssh to the user key with the following command:

`ssh -i ~/.ssh/KEYFILE` 

User states that this did not work either. I next asked for user to print out the debug report with the command:

`ssh -vv -i ~/.ssh/KEYFILE`

The debug report stated that user was trying to connect with there ssh config but 

`.*.conf matched no files` 

User states that config file was up to date. But the systeam just made changes to the bastion within the time frame that the user was out. User pasted their config file. Here is where I compared it to my config file and noticed they were missing a line which included our internal IP Range for host, user, identity file for the `proxyJump bastion`. Once they added the file, it worked.



