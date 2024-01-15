---
{"dg-publish":true,"permalink":"/sys-admin-hand-book/operating-systems/mac-os/cloud-watch-agent-on-mac-os/","title":"CloudWatch agent on MacOS","tags":["aws","macos","ec2"]}
---



## Download the installation package
https://s3.amazonaws.com/amazoncloudwatch-agent/darwin/amd64/latest/amazon-cloudwatch-agent.pkg

## Allow it to install
When you try to install it, you will be met with security restriction messages.
Go to System preferences -> Security and Privacy -> unlock the padlock (might ask for password, should be the same as the main user) -> allow apps from store and identified developers ->ok

## Configure the agent
In command line:


```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Answer the questions as required.
The config file is also located at /opt/aws/amazon-cloudwatch-agent/bin/config.json.

## start the agent using the config.json generated by the above.

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

## check CloudWatch metrics for the new data.

(c) Dawid Krysiak https://itisoktoask.me/ 