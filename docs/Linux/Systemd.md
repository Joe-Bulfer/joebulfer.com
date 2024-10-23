Just some notes of mine so far.

Here is a [blog post](http://0pointer.de/blog/projects/systemd.html) titled *Rethinking PID 1* in 2010 of experiments with a new init system.

Unix System V is as old as 1983.

Systemd is a relatively new system manager introduced in 2010 as a replacement for SysV init manager. Despite criticism of feature creep and bloat, Systemd has gained massive popularity in the last decade and is here to stay. Most distros such as Ubuntu and Red Hat ship it by default. 

Here are various changes introduced in Systemd to be aware of. Though these new features do not necessarily make the traditional tools obsolete, adoption may be the best long term solution.

##### Cron Jobs > Systemd Timers 

##### /etc/fstab > Unit Files

##### Run Levels > Targets 
Instead of traditional Sysv runlevels, such as switching to Single-User Mode with `telinit 1`, you would now use `systemctl isolate rescue.target`.

Check out this Sysv to Systemd [cheatsheet](https://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet).

|Run Level|Description|Systemd Target|
|--|--|--|
|0 | Poweroff|poweroff.target|
|1 | Single user mode (recovery mode)|rescue.target|
|2 | Multi user mode with no networking|multi-user.target|
|3 | Multi user mode with networking|multi-user.target|
|4 | User Definable|multi-user.target|
|5 | Multi user mode under GUI (standard in most systemds)|graphical.target|
|6 | Reboot|reboot.target|

##### Community Feedback and Opinion
Notes of The Linux Experiment's [video](https://www.youtube.com/watch?v=Fv3tQbOkz-E):

- All Linux based systems use an init system, the first process that starts after you boot your OS and continues to run essential programs and services.
- Systemd was spearheaded by Red Hat to replace existing Sysv (1983) and Ubuntu's now discontinued Upstart (2006-2015).
- Critics claim Systemd violates the Unix Philosophy of modularity, separate programs that communicate with each other. Instead, Systemd has become a monolithic, umbrella project that has more functions than traditional init systems were meant for.
- There is really not much competition to Systemd.

##### Unit Timers
[Cron to Systemd Time Format](https://silentlad.com/systemd-timers-oncalendar-(cron)-format-explained)
[Tutorial](https://www.airplane.dev/blog/systemd-timer-how-to-schedule-tasks-with-systemd)

```
❯ cat foo.timer 
[Unit]
Description=Append to file in /tmp every minute

[Timer]
Unit=foo.service
OnCalendar=*:*:0

[Install]
WantedBy=timers.target
```

```
❯ cat foo.service 
[Unit]
Description=Append text to /tmp file

[Service]
ExecStart=/usr/local/bin/systemd-timer.sh

[Install]
WantedBy=multi-user.target

```

```
❯ cat /usr/local/bin/systemd-timer.sh 
#!/bin/bash
echo "Systemd at `date`" >> /tmp/from-systemd.txt
```

```
❯ cat /tmp/from-systemd.txt 
Systemd at Mon Dec 25 10:40:01 AM CST 2023
Systemd at Mon Dec 25 10:41:01 AM CST 2023
Systemd at Mon Dec 25 10:42:01 AM CST 2023
...
```


For more information:`man systemd.unit`. WantedBy and Required by just create symlinks in .wants/ and .requires/ directories when `systemctl enable` is called. Wants and Requires are for actual dependencies.
