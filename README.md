System V init script template
=============================

A simple template for init scripts that provide the start, stop,
restart and status commands.

Handy for [Node.js](http://http://nodejs.org/) apps and everything
else that runs itself.

Getting started
---------------

Copy _template_ to /etc/init.d and rename it to something
meaningful. 

Here's an example for an app called
[algorithms](http://algorithms.ubercode.de):

    /etc/inid.d/alorithms

Then edit the script and enter that name after _Provides:_ (between _### BEGIN INIT INFO_ and _### END INIT INFO_).

Now set the following three variables in the script:

### dir ###

The working directory of your process.

### cmd ###

The command line to start the process.

### user ###

The user that should execute the command (optional).
If not set, the command will be called as root (via `sudo ...`).

    #!/bin/sh
    ### BEGIN INIT INFO
    # Provides: algorithms
    # Required-Start:    $network $remote_fs $syslog
    # Required-Stop:     $remote_fs $syslog
    # Default-Start:     2 3 4 5
    # Default-Stop:      0 1 6
    # Short-Description: Start daemon at boot time
    # Description:       Enable service provided by daemon.
    ### END INIT INFO

    dir="/var/apps/algorithms"
    cmd="node server.js"
    user="node"


Make Executable & install
---------------
To be able to use the script you have to change the file permissions and 'install' the script:
    
    sudo chmod 755 /etc/init.d/algorithms
    sudo update-rc.d algorithms defaults

Script usage
------------

### Start ###

Starts the app.

    /etc/init.d/algorithms start

### Stop ###

Stops the app.

    /etc/init.d/algorithms stop

### Restart ###

Restarts the app.

    /etc/init.d/algorithms restart

### Status ###

Tells you whether the app is running. Exits with _0_ if it is and _1_
otherwise.

    /etc/init.d/algorithms status

Logging
-------

By default, standard output goes to _/var/log/scriptname.log_ and
error output to _/var/log/scriptname.err_. If you're not happy with
that, change the variables `stdout_log` and `stderr_log`.

To view the running logs, you can tail the output log or error log:

    tail -f /var/log/algorithms.log
    tail -f /var/log/algorithms.err

License
-------

Copyright (C) 2012-2014 Felix H. Dahlke

This is open source software, licensed under the MIT License. See the
file LICENSE for details.
