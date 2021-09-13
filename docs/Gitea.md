# Gitea 
I came across Gitea at my old organization. It was what the systems team used instead of Github. Gitea allows you to host on your own sever and is 100% customizable. Coming into my new organization, as I would be a systems team by myself I wanted to have something similar for my boss to track what I was doing and for me to maintain myself organized. Later I would out that my boss prefers to use Asana for tracking so this project has been put on pause; nonetheless I want it documented as it was a bit of an adventure. 

### Starting
My friend told me about [Disroot]( https://disroot.org/en/about) which met my needs for a) anonymity b) ease of use. So I created an account [here](https://git.disroot.org/). After being verified I had my own cup of tea for Gitea- but I had to use Disroot as the middle man, for now. 

### Custom Issue Templates 
In my old organization my team had a custom issue template that I really liked. With my new Gitea I realized that I had something similar but alas it was not the same. This revealed two problems:

1) I needed to connect to Gitea to modify the files so that the web would reflect my configurations 
2) How to connect to Gitea via my terminal 

### Problems Solved
After doing some research & pulling from my memory bank I realized that I had to generate an SSH key, store it within the settings of my Gitea. This would come in hand when attempting to speak to the Disroot server that would then connect me to my Gitea. 

The next issue was actually verifying that the ssh key could speak to git and connect. 

You have to install git and use it in a terminal by example :
`cd /path/where/you/want/your/clone`
`git clone git://user@host/path/to/git/repo.git`

I then went into my git-repo folder from there I saw that I had an old git so I had to remove with `rm -rf .gitea` so that it would clear everything out and there would not be conflict. Then I ran git clone with the SSH URL pulled from my gitea online. They were connected and I could run commands like `git push`, `git pull` etc.

From there I needed to create the `mkdir .gitea`. When Gitea runs, it searches the configuration files for something called `ISSUE_TEMPLATE` if it doesn't find then it will continue to look the same as before. Once the issue template file is created you can add content from online templates. My friend shared the one he created which I used.  Including it below for your own modification or starting point.

``` 
---

name: "Bug"
about: "Maintenance of existing infrastructure"
---

name: "Bug"
about: "Maintenance of existing infrastructure"
labels:

- "OKR: Maintenance"
- "Priority: High"

---

<!-- Write a meaningful description of the issue below this line. -->

## Validation Criteria
<!-- Describe what do you expect to have once the task is done -->

* [ ]

## Steps
<!-- Describe the steps required to fulfill the validation criteria. They should
be clear enough so that anyone of the team is able to follow them. -->

* [ ]
```