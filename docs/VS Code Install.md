## What is it?
VS code is a free open-source code editor 
that is available for all major platforms. I 
was attempting to run Git in a more 
traditional fashion with the command line but
I found it hard to find a spell checker for
vim. ***IF you're reading this, please feel
free to drop tips on how to do this, also 
taking a mental note to find my own solution.***

In the interim, I am using VS code downloaded
[here](https://code.visualstudio.com/Download). 

What I have learned is that you can use VS 
code to write in several languages with a 
nice UX. There is a built in terminal & you 
can connect it to your GitHub. 

## How to Connect GitHub<->VS Code 
Once downloaded, if you click the branch icon on the left panel it will ask if you want to clone, create, import a repository. If you click import, it will give you the option to paste the link to you git. Go into your repo, and paste the HTTPS URL. From there, a pop up will prompt you to connect your VSCODE to your GIT. Once you login on GIT, it will link. You should get a successful output. 

Note: there is other forms, I am sure- but this very straight forward. 

## VSCode Spell-Right
I have tested VSCODE spell-check, while very easy to install, (its plug and play-it) does not provide case sensitive feedback for your languages, in my case- markdown. So, I have used [VS Spell-right](https://github.com/bartosz-antosik/vscode-spellright). Installation was a bit complicated on Debian, but I sorted it out. 


### Steps
Going into the extensions option
The steps on the VS spell-right [git](https://github.com/bartosz-antosik/vscode-spellright) states that you have to Create the dictionaries sub folder as it doesn't exist by default.

[Here](https://github.com/bartosz-antosik/vscode-spellright/issues/325)

[Here](https://github.com/bartosz-antosik/vscode-spellright)