First let's create and change into our training working directory,
```sh
git clone https://github.com/wayneeseguin/pgconf2016-steel-elephant-notes
cd pgconf2016-steel-elephant-notes
```

Let's pre-add the vagrant box we'll be using so that we can stand them up in parallel,
```sh
vagrant box add fgeerlingguy/centos7
```
If you decide to go the freebsd route,
```sh
vagrant box add freebsd/FreeBSD-11.0-CURRENT
```
Note you'll be prompted for the provider you are using, either virtualbox or vmware fusion. If you already have the box, great! Move along :)

```sh
bash ./training-setup-centos7
```

You'll have 3 directories `centos7-pg-{{N}}` that you can cd into and `vagrant ssh` to.
It will have a golang environment setup with consul & vault cloned and built for 
you to play around with the two technologies. 
`consul join` the clusters and run your own `vault` configured to connect to it.


