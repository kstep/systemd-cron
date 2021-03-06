systemd-cron
================
[systemd][1] units to run [cron][2] scripts

Description
---------------
systemd units to provide cron daemon functionality by running scripts in cron directories.
The crontabs are automaticaly translated using (/usr)/lib/[systemd-crontab-generator][6].

Usage
---------
Add executable scripts to the appropriate cron directory (e.g. `/etc/cron.daily`) and enable systemd-cron:

    # systemctl enable cron.target
    # systemctl start cron.target

The project also includes simple crontab command equivalent, which behaves like standard crontab command (and accepts the same main options).
   
The scripts should now be automatically run by systemd. See man:systemd.cron(7) for more information.

Dependencies
----------------
* systemd ≥ 197
    * systemd ≥ 209, yearly timers
    * systemd ≥ 212, persistent timers
* [run-parts][3]
* python 2

Installation
----------------
There exists a Debian package: http://packages.debian.org/systemd-cron/ .
You can also build it manually from source.


Packaging
--------------

### Building

    $ ./configure
    $ make

### Staging

    $ make DESTDIR="$destdir" install

### Configuration

The `configure` script takes command line arguments to configure various details of the build. The following options
follow the standard GNU [installation directories][4]:

* `--prefix=<path>`
* `--bindir=<path>`
* `--confdir=<path>`
* `--datadir=<path>`
* `--libdir=<path>`
* `--statedir=<path>`
* `--mandir=<path>`
* `--docdir=<path>`

Other options include:

* `--unitdir=<path>` Path to systemd unit files.
  Default: `<libdir>/systemd/system`.
* `--runpaths=<path>` The path installations should use for the `run-parts` executable.
  Default: `<prefix>/bin/run-parts`.
* `--enable-boot[=yes|no]` Include support for the boot timer.
  Default: `yes`.
* `--enable-hourly[=yes|no]` Include support for the hourly timer.
  Default: `yes`.
* `--enable-daily[=yes|no]` Include support for the daily timer.
  Default: `yes`.
* `--enable-weekly[=yes|no]` Include support for the weekly timer.
  Default: `yes`.
* `--enable-monthly[=yes|no]` Include support for the monthly timer.
  Default: `yes`.
* `--enable-yearly[=yes|no]` Include support for the yearly timer. Requires systemd ≥ 209.
  Default: `no`.
* `--enable-persistent[=yes|no]` Make timers [persistent][5]. Requires systemd ≥ 212.
  Default: `no`.

A typical configuration for the latest systemd would be:

    $ ./configure --prefix=/usr --confdir=/etc --enable-yearly --enable-persistent

See Also
------------
`systemd.cron(7)` or in source tree `man -l src/man/systemd.cron.7`


License
-----------
The project is licensed under MIT.


Copyright
-------------
© 2014, Dwayne Bent : original package with static units  
© 2014, Konstantin Stepanov (me@kstep.me) : author of crontab generator  
© 2014, Daniel Schaal : review of crontab generator  
© 2014, Alexandre Detiste (alexandre@detiste.be) : manpage for crontab generator  


[1]: http://www.freedesktop.org/wiki/Software/systemd/ "systemd"
[2]: http://en.wikipedia.org/wiki/Cron "cron"
[3]: http://packages.qa.debian.org/d/debianutils.html "debianutils"
[4]: https://www.gnu.org/prep/standards/html_node/Directory-Variables.html "Directory Variables"
[5]: http://www.freedesktop.org/software/systemd/man/systemd.timer.html#Persistent= "systemd.timer"
[6]: https://github.com/kstep/systemd-crontab-generator "crontab generator"
