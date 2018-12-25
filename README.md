# backup-script
Linux back up script for mysql and dir

Let's assume along with the /home directory there are also Apache and MySQL servers and we want to make more complete backup of the system.

1. Create a file named mybackup; make it executable; locate it in /usr/local/bin to be accessible as shell command system wide. Create a directory where the backup files will be stored:

sudo touch /usr/local/bin/mybackup && sudo chmod +x /usr/local/bin/mybackup
sudo mkdir /var/backup
Paste the following script as content of the file /usr/local/bin/mybackup and save it.

If this is a VPS, maybe you would want to access your backup file from Internet through the web browser. In this case we could encrypt the file for additional security. If you are fan of 7zip add some command as the next to the bottom of the script:
rm /var/www/html/the-location/*
7za a -tzip -p'<my-strong-pwd>' -mem=AES256 "/var/www/html/the-location/my-backup-$TODAY.tgz.7z" "/var/backup/my-backup-$TODAY.tgz"

To automate the the task you can add a new entry in root's crontab by the command sudo crontab -e. For example to execute the script every night at 1:15 the Cron job definition should be:

15 1 * * * /usr/local/bin/mybackup > /var/log/mybackup-cron.log 2>&1
this will create also the log file /var/log/mybackup-cron.log that will contain and the error messages 2>&1 if there are any. Read the log periodically to be sur everything works fine.
