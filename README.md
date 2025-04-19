compose-systemd
===============

This script is used to install and manage docker compose projects with systemd.

A semi-automatic dependency mechanism is available.

This can be used to automatically start the different compose services in the correct order (but no waiting for availability is done, as containers in a compose file).

Configuration
-------------

You need to copy `compose-systemd.conf` in `/etc/` and `compose-systemd` in `/usr/local/bin/` or any directory in your `PATH`

Edit `/etc/compose-systemd.conf` file to adjust configuration to your liking.

By default, the following configuration is:
* compose directory: `/etc/compose`
* compose user: `compose`
* systemd base service name: `compose@.service`
* dependencies file: `/etc/compose/compose.deps`

Dependencies:
* bash
* systemd
* docker with Compose v2 or docker-compose
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
compose-systemd install
```

Usage
-----

Every time you modify a compose project or a dependency, just run:
```
compose-systemd update
```
or run:
```
compose-systemd update your_application
```

You can then start the whole chain with:
```
compose-systemd start
```
Or just your application with:
```
compose-systemd start your_application
```

There are also `stop`, `restart` and `status` commands.

Use `-h` or `--help` to get help.

Use `-v` or `--verbose` to get verbose output.

Use `-V` or `--version` to show compose-systemd version.


Testing
-------

You can use `./testindocker` to install it in a temporary docker

- Add `app1:` and `app2:` to `/etc/compose/compose.deps` file by using `docker exec` or a local `ssh` connection.
- Install systemd services: `compose-systemd update`
- Start them: `systemctl start compose@app1`, same for app2.
