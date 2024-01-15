---
{"dg-publish":true,"permalink":"/sys-admin-hand-book/aws/aws-cloud-watch-insights-count-visits-from-ip-addresses/","title":"AWS CloudWatch Insights - count visits from IP addresses","tags":["AWS","EC2","CloudWatch","security"]}
---



# CloudWatch Insights to find an abuser
Recently I had a case where a customer tried to figure out who is abusing their systems, probably by invoking bots.
Fortunately, their application was recording registrations in the main application logs, so the solution was quite simple:

```
fields @message
| filter @message like /POST \"\/registration/
| parse @message /(?<@ip>([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3})[.]*)/
| stats count() as requestCount by @ip
| sort requestCount desc
| filter requestCount >5
```

## let's break it down
* first line selects the fields (in this case, just the body of the message
* second line filters out the lines that are relevant in this case - containing `POST "/registration` string
* third line filters the remaining lines by looking for an regex matching the IP address format
* fourth line is the equivalent of 'count()'
* fifth line orders the results in descending order
* sixth line filters out only IPs that occurred more than 5 times
* 