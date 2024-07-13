# New post title here
Installed minikube finally
## Introduction
In the book they recommend to use minik8s, but I had problems using snap pakcage manager in my WSL system. So I decided to proceed and install minikube.

## Prerequisite
Basically my system is Ubuntu so I only needed to have install docker, which I found an issue related with iptables in wsl, but here is the fix https://dev.to/bowmanjd/install-docker-on-windows-wsl-without-docker-desktop-34m9

## Use Case
Once docker is installed I also had to add my local user to the docker group to be able to initialize minikube with my user (it needs the privileges).

Here how to add the user to the group:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
Then run this command to apply the changes at the moment
```
newgrp docker
```

## Try yourself
The to install minukube I followed the steps here: https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

```

And finally to start the minikluster:
```
minikube start
```

Yo can already run commands like "kubectl get pods".

## Notes
I added an alias in my .bashrc to simplify "kubectl" command to just "kube", I thought the original comand was too long to type every time.
```
alias kube="kubectl"
```