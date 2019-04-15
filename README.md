compose-dirs
============

This script is used to install and manage docker compose projects with systemd.

A semi-automatic dependency mechanism is available.

This can be used to automatically start the different compose services in the correct order.

Configuration
-------------

You need to copy `compose-dirs.conf` in `/etc/` and `compose-dirs` in `/usr/local/bin/`.

Edit `/etc/compose-dirs.conf` file to adjust for the wanted configuration.

By default, the following configuration is:
* compose directory: `/etc/docker-compose`
* compose user: `root`
* systemd base service name: `compose@.service`
* dependencies file: `/etc/docker-compose/dirs.deps`

`dirs.deps` format
------------------

This file specify one compose directory per line, following by a colon and a coma separated list of compose directories dependencies.

Ex:
```
compose_1:
compose_2:
compose_3:compose_1,compose_2
compose_4:compose_2
```

Installation
------------

Create you compose project in `/etc/docker-compose`, fill in the `dirs.deps` file, and then ask for installation:
```
compose-dirs install
```

Every time you modify a compose project or a dependency, just run:
```
compose-dirs update
```

You can then start the whole chain with:
```
compose-dirs start
```

There are also `stop`, `restart` and `status` commands.
Use `-h` or `--help` to get help.
