# Intro
At time of writing my organization is bringing up the
idea of using cloudflare as our CDN. I have no idea
what this - below are my findings.

## Cloudflare
Cloudflare is a free CDN. CDN stands for content 
delivery network. The idea behind a CDN is that
the content is not stored in a single web host / server. With the CDN you're able to distribute
that information across hundreds of data centers 
across the globe thus providing intelligent routing
of content is delivered to site visitor. 

Because of the distribution this will give a faster 
experience to the end users. 

### Pings
As site users ping our server, if we only have one
this will create high ping rates. A ping (Packet Internet or Inter-Network Groper) is a basic Internet program that allows a user to test and verify if a particular destination IP address exists and can accept requests in computer network administration. 

Pings serve two purposes:
* verifying that the target host is available  
* determining round-trip time (RTT) or latency

## Plug-in's
You can attach several plug-ins to Cloudflare, some 
include caching & image optimization. This of course 
increases the cost of Cloudflare.

## Security Measures
With hosts using CDN's, they create robust databases
that can protect a site from malicious actors.

## Setting up Cloudflare
* Cloudflare.com, sign up as normal with email and password
* Add your site
* Cloudflare will pull all DNS records that it found
* Log into your DNS and change the name servers
* Allow for Propagation 

