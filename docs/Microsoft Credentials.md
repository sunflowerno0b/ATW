## Microsoft Mystery

At my current organization, I attempted to gain admin access to our MS Office. I needed to find out how -these licenses came to be. I reached out to Tech Soup and found that if you go to [tech soup](techsoup.org/) , login, click my account, then click Request history, this will take you to another page. In that page you will see manage Microsoft requests. There you can see the details on the donations that Microsoft has given your organization.

Seeing this confirmed that we do have Microsoft accounts. So when I went to https://admin.microsoft.com and tried to register- it stated that the domain was already in use. Confusion.

Odd, because in our password manager there was no persons / accounts listed as admin. I reached out to MS support. They got back to me after a few emails and listed a user who did not even know they were admin. I asked that they try to login, or hit forgot password. The user did not know the account in which this was tied to (they attempted to use their work address- it did not work). MS support said that in their records the "tenant" was unmanaged, this was the silver lining in the solution. So I had to proceed with the following steps:
#### From Microsoft Support
I needed:
1. An email address with the domain where you can send and receive emails.  
2. The DNS records associated with the domain.  
   
 

## To become an Admin:  
1. First, go to https://powerbi.microsoft.com/en-us/  and select "Start Free" so that you have an Office 365 Business user account for this "tenant". Then under “Getting started with Power BI” click on “Try Power BI For Free”
2. You will need to sign up using your email address with the domain. I used my IT Admin not my work email tied to me. No one wants bloat mail.
3. Once you sign up for Power BI use those credentials to sign in at portal.office.com 
4. After logging in to portal.office.com with the same credential you used on the Power BI website,click on the yellow square in the upper left-hand corner and then the Admin icon app. If the Admin icon is not displayed right away, click the view all my apps option to see if that is there.  
5. Finally, select the Admin icon. You should have the “Become an Administrator”. You will need to verify the DNS records and then your account will be elevated to “Global Administrator”.  




After completing steps 5, it took me to a page ***insert image of page Screen Shot 2021-07-19 at 12.24.15 PM*** 
that included the TXT name, TXT Value and TTL. I had no idea what this meant. I had to go to my DNS, but I thought because this was Google that held it I went there first. I was wrong- google is merely an email provider. 

I had to: check  out- https://lookup.icann.org/lookup, here I was able to see that Linode was our DNS provider. 

So I went to Linode and there I saw that there was a Domain(s) tab. I clicked in there and saw that there was a space for TXT records, I entered the three items that were on MS and waited 10 minutes then clicked confirm on the Microsoft admin page. At that point, it was confirmed and I was made admin for the domain pulitzer center.org.

