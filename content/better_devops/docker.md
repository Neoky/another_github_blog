---
title: "Docker"
date: 2021-12-06T19:01:16-06:00
draft: true
---

# Docker

## How-to Install

### Amazon Linux Image 2
```bash
# Install docker
sudo amazon-linux-extras install docker
# Start docker service
sudo service docker start
# Allow ec2-user to make docker calls.
sudo usermod -a -G docker ec2-user
# Logout and log back in to be able to execute docker commands.
# Test docker works
docker ps
# Install latest docker-compose
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
# Make docker-compose executable
sudo chmod +x /usr/local/bin/docker-compose
# Test to see if docker-compose works
docker-compose version
```
* Reference: https://gist.github.com/saikrishnamylaram/fa5300be226f1a69869e146c614ecad8