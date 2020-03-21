compose-dirs
============

This script is used to install and manage docker compose projects with systemd.

A semi-automatic dependency mechanism is available.

This can be used to automatically start the different compose services in the correct order (but no waiting for availability is done, as containers in a compose file).

Configuration
-------------

You need to copy `compose-dirs.conf` in `/etc/` and `compose-dirs` in `/usr/local/bin/` or any directory in your `PATH`

Edit `/etc/compose-dirs.conf` file to adjust configuration to your liking.

By default, the following configuration is:
* compose directory: `/etc/compose`
* compose user: `compose`
* systemd base service name: `compose@.service`
* dependencies file: `/etc/compose/compose.deps`

Dependencies:
* bash
* systemd
* docker-compose
* python3
* coreutils
* findutils

`compose.deps` format
---------------------

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

Install the Systemd service template:
```
compose-dirs install
```

Usage
-----

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
