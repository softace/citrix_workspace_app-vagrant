Sandbox for Citrix Workspace App
================================

If you don't trust the closed source binaries of Citrix (and you
shouldn't when you work in an enterprise organisation that takes
security seriously), then here is a Vagrantbox that installs the
citrix software and firefox and you can run it from within that sandbox


Build the box
=============

1. Clone this repository

2. Downdload the Citrix Workspace app https://www.citrix.com/downloads/workspace-app/linux/workspace-app-for-linux-latest.html

    Select
    * Debian Packages
      * Full Package (Self-service support)
        * Citrix Workspace app for Linux (x86_64)

    and put the file in the directory of this repository.

3. Run

    ```
    vagrant up
    ```


Use the citrix client
=====================

```
vagrant ssh -- -X firefox -no-remote
```

Then visit your citrix server url
