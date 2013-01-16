run-script
====================

The run-script run the specified script and it uses file locking on
the specified script to attempt to eliminate multiple running on the same machine.

Usage
---------------------

```
run-script <start|stop|status> <script> [arguments]
```

For exameple, when you run ``sample-script``:

```console
$ cp run-script/run-script <sample-script directory>
$ cd <sample-script directory>
$ ./run-script start sample-script [arguments]
```

or

```console
$ cd <sample-script directory>
$ /path/to/run-script/run-script start ./sample-script [arguments]
```

or

```console
$ /path/to/run-script/run-script start <sample-script directory>/sample-script [arguments]
```

## About lock file and pid file

Create lock file (like sample-script.lock) and pid file (like sample-script.pid)
on the directory where run-script is by default.
But if you change these directory, run as follows:

```console
$ LOCK_DIR=/var/lock PID_DIR=/var/run ./run-script <start|stop|status> <script> [arguments]
```

## Cron

Sample:

```bash
$ crontab -l
SHELL=/bin/bash
PATH=/usr/local/bin:/bin:/usr/bin

*  00  *  *  * cd /path/to/<sample-script directory> && ./run-script/run-script start ./sample-script 2>&1 | logger -t sample-script -p local0.info
```
