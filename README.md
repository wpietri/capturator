Capturator is a simple system service that captures all network traffic
to /var/log/capturator. It's intended to be used on production and
development servers with modest traffic volumes so that one can go back
in time to examine problems.

By default it captures all packets and saves them for a week.

The capturator file itself belongs in /etc/init.d. On Ubuntu, you set
it up with

    sudo update-rc.d capturator defaults

For the cleanup, put capturator.cron into /etc/cron.daily.

Both files should be executable.

If you are also running AppArmor, this line belongs in tcpdump's profile:

    owner /var/log/capturator/* w,

after which you'll have to do something like this:

    sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.tcpdump


TODO

* make proper packages
* after each file closes:
    * look for old uncompressed packages
    * check total disk space and delete early if needed
* add a config file that includes
    * control of disk space limits
    * a tcpdump expression to ignore certain packets

