Sandbox for Citrix client
=========================

If you don't trust the binaries of Citrix (and you shouldn't when you
work in an enterprise organisation that takes security seriously),
then here is a Vagrantbox that installs the citrix client and firefox
and you can run it from within that sandbox


Build the box
=============

```
vagrant up
```


Use the citrix client
=====================

```
vagrant ssh -- -X firefox
```

Then visit your citrix server url
