#Clinv

##What is it?
Clinv was created by my good friend and could be found [here](https://github.com/lyz-code/clinv). Beware, the documentation is very bare but I am working on adding content based off of my use case for no0bs. Clinv was created to asset inventory on AWS.

##Current Issue
I need to connect clinv to my aws. But how to do that? One must first download `aws cli`. More information can be found [here](https://aws.amazon.com/cli/). 

Running `aws configure` will have me at a prompt in which I will use my AWS credentials for the IAM key.
The IAM key can be found within your security settings of your aws account.The password only shows once - so you will want to do it that one time. If you have forgotten the password, simply create a new one and add into `aws configure` or amend your `/.aws/config` file. 

To connect clinv with the recently created `aws cli` run `clinv update` to update and this will show you a layout of the items you have connected to your amazon.

##Clinv troubleshooting:
My `clinv update` was not working so I needed to see the error. The output said that it was with the region not connecting. I needed to check my aws configure file. To do that I typed `cd .aws` from there I ran  `ls` which showed me the contents of the `.aws` directory, within there I saw the config file. There I opened and realized I had Region: US East (N. Virginia) us-east-1. The region needed to be: us-east-1

Once that was changed I reran `clinv update` and it worked! Clinv was connected to my aws. 