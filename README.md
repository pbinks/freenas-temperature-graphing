freenas-temperature-graphing
============================

Bash scripts to graph FreeNAS CPU and drive temperatures. Tested on 9.3 and
9.10.

 

Example output:
---------------

![CPU temperatures per minute](examples/temps-1min-cpus.png)

![Drive temperatures per minute](examples/temps-1min-drives.png)

![CPU temperatures per 5 minutes](examples/temps-5min-cpus.png)

![Drive temperatures per 5 minutes](examples/temps-5min-drives.png)

The color scheme is easy to change. Pull requests welcome

 

Installation:
-------------

1.  Copy the .sh files to a share on your server. Note the full path to the
    files (ex. /mnt/mainpool/myshare/temperature-monitoring/rrd.sh)

2.  Schedule the scripts to run regularly. The recommended method is via the
    FreeNAS Tasks panel in the web interface, since any cronjobs in crontabs are
    wiped out during upgrades.

    1.  For samples to be collected every 5 minutes, create a new task ([see
        tasks screenshot](examples/tasks.png))

    2.  Set the user to root (SMART data access requires super-user privs). See
        [screenshot 1](examples/task1.png).

    3.  Enter the command to be run:

        1.  Example for data collection:
            /mnt/mainpool/misc/temperature-monitoring/rrd.sh
            /mnt/mainpool/misc/temperature-monitoring/temps-5min.rrd

        2.  Example for data graphing:
            /mnt/mainpool/misc/temperature-monitoring/rrd.sh
            /mnt/mainpool/misc/temperature-monitoring/temps-5min.rrd

        3.  NOTE: The time part of the name (5min) is important, since the
            scripts use it to know how to format the data. It has to be a number
            followed by "min".

    4.  Enter the time between runs: minutes (5), hours (1), and days (1) (see
        [screenshot 1](examples/task1.png) and [screenshot
        2](examples/task1.png)). Set it to run every month and day of the week.

    5.  Redirect Stdout (otherwise you'll get emails every time the graphs are
        generated). Make sure the task is enable. See [screenshot
        3](examples/task3.png)

 

Extras:
-------

The rrd-graph.sh script contains code to graph each device individually as well
as all together. Just uncomment the appropriate blocks.

 

The colors can be adjusted at the top of the rrd-graph.sh file.
