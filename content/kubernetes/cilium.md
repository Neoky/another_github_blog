---
title: "Cilium"
date: 2021-12-06T12:26:00-06:00
draft: true
---

# Cilium

Open-source and light-weight CNI. I have been working with this one for it's ease of use, documentation, easy multi-cluster communication, and can be setup for encrypted traffic.


Where do you go to learn about Cilium? I recommend going to the docs section I have referenced below. The docs are incredibly informative.


## CLI Tools

I highly recommend getting the CLI tools Cilium and Hubble installed. They are invaluable for debugging. Then install the CNI to your cluster. You can even use the CLI to inall the CNI.

```bash
curl -L --remote-name-all https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-amd64.tar.gz{,.sha256sum}
sha256sum --check cilium-linux-amd64.tar.gz.sha256sum
sudo tar xzvfC cilium-linux-amd64.tar.gz /usr/local/bin
rm cilium-linux-amd64.tar.gz{,.sha256sum}
```

Install Hubble
```bash
export HUBBLE_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/hubble/master/stable.txt)
curl -L --remote-name-all https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-amd64.tar.gz{,.sha256sum}
sha256sum --check hubble-linux-amd64.tar.gz.sha256sum
sudo tar xzvfC hubble-linux-amd64.tar.gz /usr/local/bin
rm hubble-linux-amd64.tar.gz{,.sha256sum}
```


## Install
* Reference: https://docs.cilium.io/en/v1.10/gettingstarted/k8s-install-helm/

I installed on EKS using Terraform and Helm.

First add the helm repo. ```helm repo add cilium https://helm.cilium.io/```

Next delete the aws-node cni with ```kubectl -n kube-system delete daemonset aws-node```

Install the helm chart.
```bash
helm install cilium cilium/cilium --version 1.10.5 \
  --namespace kube-system \
  --set eni.enabled=true \
  --set ipam.mode=eni \
  --set egressMasqueradeInterfaces=eth0 \
  --set tunnel=disabled \
  --set nodeinit.enabled=true\
  --set hubble.relay.enabled=true \
  --set hubble.ui.enabled=true
```

Restart all of the other pods. 
```kubectl get pods --all-namespaces -o custom-columns=NAMESPACE:.metadata.namespace,NAME:.metadata.name,HOSTNETWORK:.spec.hostNetwork --no-headers=true | grep '<none>' | awk '{print "-n "$1" "$2}' | xargs -L 1 -r kubectl delete pod```

Check the install with the CLI.
```cilium status --wait```

## Hubble Access
First you need to port-forward
```cilium hubble port-forward&```
Optionally you can verisfy install.
```hubble status```
Bring up the GUI
```cilium hubble ui```


# Extra Tools

* editor.cilium.io
Incredible tool to help new and advanced devs to quickly deploy CiliumNetworkPolicies.
https://editor.cilium.io/

# References

* Docs - at time of writing
https://docs.cilium.io/en/v1.10/gettingstarted/k8s-install-helm/

* Network Policy
Lookup basics, L3/4/7 examples, and Deny/Host Policies.
https://docs.cilium.io/en/stable/policy/


## Important Cheat sheet
Note: The guide does not do the best job at separating commands that get ran locally vs. ones that get ran from ```kubectl exec cilium```. 
https://docs.cilium.io/en/v1.10/cheatsheet/

# Troubleshooting

* cilium/hubble commands - ca.crt not found

# Last updated
2021-12-06

