First let's create and change into our training working directory,
```sh
git clone https://gist.github.com/wayneeseguin/a824a70711f9e857eb9af69b5033ecfb steel-elephant-training
cd steel-elephant-training
```

Let's pre-add the vagrant box we'll be using so that we can stand them up in parallel,
```sh
vagrant box add freebsd/FreeBSD-11.0-CURRENT
```
Note you'll be prompted for the provider you are using, either virtualbox or vmware fusion. If you already have the box, great! Move along :)

```sh
bash ./training-setup-freebsd
```
