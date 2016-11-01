Sandbox for Citrix client
=========================

If you don't trust the closed source binaries of Citrix (and you
shouldn't when you work in an enterprise organisation that takes
security seriously), then here is a Vagrantbox that installs the
citrix client and firefox and you can run it from within that sandbox


Build the box
=============

Downdload the Citrix receiver client from https://www.citrix.dk/downloads/citrix-receiver/linux/receiver-for-linux-latest.html
Select

* Debian Packages
  * Full Package (Self-service support) Receiver for Linux (x86_64)

and put the file in this directory. Then run

```
vagrant up
```


Use the citrix client
=====================

```
vagrant ssh -- -X firefox -no-remote
```

Then visit your citrix server url
