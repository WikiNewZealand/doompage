## Figure.NZ Doom Page
This repository generates (via jekyll) a static 503 page to be served as an alternative to the Figure.NZ application stack.

### Purpose
In the event of a catastrophic failure of the Figure.NZ application stack, this page serves as the last line of defence, serving a branded error message from an unrelated host and without any external asset dependencies. 

### Known issues
A significant upstream failure (eg. the loss of AWS) will stop this from working, partly because deployment requires access to Route 53 (and for Route 53 to then serve the changed records), and partly because a serious AWS outage would probably disable GitHub as well.

### How to deploy
1. Log into AWS and go to Route 53.
2. Remove the A record from the *figure.nz* record set.
3. Replace it with A records for the following addresses:  

```
192.30.252.153
192.30.252.154
```

### How to recover
1. Log into AWS and go to Route 53.
2. Find the DNS name for the production ELB (EC2 / Load Balancers / website2-prod / DNS name). It should look something like: "website2-prod-1335915850.ap-southeast-2.elb.amazonaws.com".
3. Remove the A records for the IP addresses above.
4. Create an apex A record with the Amazon-specific alias to the ELB names from step 1.
