## Mosyle Configuration

### Apologies 
I wish that I had more for this as there were many steps. I will look into the Admin guide and see what I can update when I have a moment. 


### Issue
But to jump into this specific situation. At my old organization, I wanted to reduce the IT Friction by rolling out an MDM for all company owned computers, this would allow me to push out updates, app control, remote wiping etc. When I came to my new organization I was approved for this. 

When enrolling the MDM, I wanted to make sure that the computers in my fleet could only be logged in via my organizations Domain. I needed to connect the MDM to Google, when I attempted within the settings of the MDM, Google blocked me.  
I could not connect SSO as it was blocked by Google

### Solution
I needed to log into my Google Admin Suite. From there on the left hand side I needed to find "Security" and then click on "API controls". Once there, I needed to find & click "Manage third-party app access".
And from the new page, click on "Configure new app".
Then I needed to look for "Mosyle" and add it as "Trusted".

Once that was done, I was able to go into the MDM settings and set the policy to allow SSO with Gmail for all the computers enrolled in the MDM.