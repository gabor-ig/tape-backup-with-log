# tape-backup-with-log
This is a simple setup involving a few bash scripts to make regular backups of a few directories for example home and var/www to a tape drive. Tested and regularly used with HP LTO-3 tape drive. The tapes get a name and backups are logged (timestamp, first block, last block). An email notification is sent for every backup.  When end of tape is reached, the user gets an email with the tape log attached and the tape is ejected. There is a script ("newtape") to "initialize" new tapes: the tape log is rotated with logrotate ("taperotate"), the new tape gets ereased and numbered or named for the new log file.
Automation is done with /etc/crontab.

## Instructions

### Install
- copy the contents of etc to /etc.
- keep the two scripts "newtape" and "taperotate" in the same folder, ie. /home/user or /srv/tape.
- update /etc/crontab with the contents of the exaple crontab file here.
- change directories to backup and your email address in the script "backup_daily" and in the crontab file
- mkdir /var/log/tape && chmod 755 /var/log/tape
- see further tips and explanations in the commented scripts

### Use
- the "backup_daily" script (including any additional backup scripts in the directory /etc/backup) get called automatically by cron every day at 4:25 am
- run "newtape" manually when starting a new tape. 
- all scripts need to be run as sudo/root because of the tape commands

Feel free to fork and adapt to your needs :-)
