First let's create and change into our training working directory,
```sh
git clone https://github.com/wayneeseguin/pgconf2016-steel-elephant-notes
cd pgconf2016-steel-elephant-notes
```

Let's pre-add the vagrant box we'll be using so that we can stand them up in parallel,
```sh
vagrant up
```
You'll have 3 directories `centos7-pg-{{N}}` that you can cd into and `vagrant ssh` to.
It will have a golang environment setup with consul & vault cloned and built for 
you to play around with the two technologies. 
`consul join` the clusters and run your own `vault` configured to connect to it.

Eg. you can ssh into the vm's and play around with consul+vault+postgresql:
```sh
vagrant ssh
```
Recommended that you use `tmux` or `screen` to manage this task.

If you want to go the freebsd route, modify a few things in the Vagrantfile and use,
```sh
export BOX=freebsd/FreeBSD-11.0-CURRENT SSH_SHELL=sh PROVISION_SCRIPT="../scripts/provision-freebsd"
vagrant up
vagrant ssh
```
