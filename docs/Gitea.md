# Gitea 
I came across Gitea at my old organization. It was what the systems team used instead of Github. Gitea allows you to host on your own sever and is 100% customizable. Coming into my new organization, as I would be a systems team by myself I wanted to have something similar for my boss to track what I was doing and for me to maintain myself organized. Later I would out that my boss prefers to use Asana for tracking so this project has been put on pause; nonetheless I want it documented as it was a bit of an adventure. 

### Starting
My friend JMP told me about [Disroot]( https://disroot.org/en/about) which met my needs for a) anonymity b) ease of use. So I created an account [here](https://git.disroot.org/). After being verified I had my own cup of tea for Gitea- but I had to use Disroot as the middle man, for now. 

### Custom Issue Templates 
In my old organization my team had a custom issue template that I really liked. With my new Gitea I realized that I had something similar but alas it was not the same. This revealed two problems:

1) I needed to connect to Gitea to modify the files so that the web would reflect my configurations 
2) How to connect to Gitea via my terminal 

### Problem #2 Solved
After doing some research & pulling from my memory bank I realized that I had to generate an SSH key, store it within the settings of my Gitea. This would come in hand when attempting to speak to the Disroot server that would then connect me to my Gitea. 