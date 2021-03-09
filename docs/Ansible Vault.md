## Task 

Playbooks that had `.vault_pass.sh` files with permissions of 644 needed to be updated to 655. Passwords stored here would be easy to decrypt in these playbooks. 

## Lesson learned
+ this explanation is mediocre at best because I am taking the notes from memory rather than having typed it in parallel as I worked. Will amend this for future tasks.
+ read the steps with caution if you ever find yourself on this page for [pass](https://www.passwordstore.org/) assistance. 

## Steps 
When working with an organizations private/public git repo, its important to understand that these repo's need to be copied locally on to your machine. The most secure format is to SSH, be sure that your rdsa key is within the organizations LDAP, these brings ease & security when trying to access private severs, machines & services. 

Once the repo is local on your machine, insure that you have the `.git` file as this will contain the information needed for you to `push` `pull` `merge` & `commit` to the organizations repo. 

In each playbook, I searched for the `.vault_pass.sh` with a `ls -la` command. Once found, I checked for the permissions a 644 would read as `[-rw-r-r]` which is not what we want. 

Good practice to take note of all the playbooks that have the permissions set to this. I took notes in a note pad.

Make a backup of of `vault_pass.sh` with the following command `cp vault_pass.sh bk.vault_pass.sh`. This covers you in the event something goes wrong with the file you're working on, the authenticity of the original remains.

Pass reads from the `vault_pass.sh` file, this file should be pointing to the pass path so it can decrypt and show you your passwords. It should resemble something like `pass show ${XXXX_PASS_PATH}reponame/department/vault`

With the `vault_pass.sh` pointing to the correct path you now have to find all the other secret files, using the `tree` command at the root of the folder will allow you to see easier where the path to these files are.
Once found you can run:

`ansible-vault rekey --new-vault-password-file .vault_pass.sh --vault-password-file bk.vault_pass.sh directory/secrets.yml` 

After this you can run pass show to secure that the passwords have been encrypted and are able to function with the changes made. 