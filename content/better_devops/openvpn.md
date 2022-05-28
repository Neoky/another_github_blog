---
title: "Openvpn"
date: 2021-12-06T19:06:09-06:00
draft: true
---

# OpenVPN

I currently use kylemanna's docker-openvpn. It is a good standard for a containerized openvpn. I currently have some issues with it crashing an EC2 server that I am working on debugging.

https://github.com/kylemanna/docker-openvpn

To expand on their README.

I like putting variables like their OVPN_DATA in a setenv.sh file. Make sure you make these your own.
```bash
cat <<EOF > setenv.sh
OVPN_DATA="ovpn-data-example"
URL="example.com"
EOF
```
Now I can ```source setenv.sh``` whenever I want to work with the project.

You just need to run these once to inialize. 
```bash
docker volume create --name $OVPN_DATA
docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://$URL
docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
```

Start the server.
```docker run --restart unless-stopped -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN kylemanna/openvpn```

Generate or user certificate without a passphrase. *Change CLIENTNAME your username*.
```docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass```

Retrieve ovpn file from container.
```docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn```