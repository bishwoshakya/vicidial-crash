vicidial-crash
==============

repair database


Troubleshoot the vicidial server if you face above problem

Cause for the above error
1. Mysql crashed or mysql stopped
2. Either the vicidial server shutdown all of sudden due to powercut or imporper shutdown (pressing the powerbutton directly)
3. Overload of server leads to mysql crash
4. Shortage of Harddisk space 

Troubleshooting
Login to the server via ssh using putty
1. Check whether the harddisk is full  type  df -h
    /dev/mapper/VolGroup00-LogVol00
                      446G   54G  0  100% /
2. If it shows 100%  then the harddisk is full you need to delete the recordings and logs
3. go to /var/spool/asterisk/monitorDONE/ORIG
4. type rm -rf *     ### this will delete all the file under ORIG directory
5. if the above command displays cannot delete file too long  , then  download the WINSCP software and login to the server , or run this command " find . -type f -name "*.wav" | xargs -l500 rm -f " this will delete every 1500 files one by one and empty the folder.
6. Goto var/spool/asteirsk/monitoreDONE/ORIG
7. select all the files and click delete
8. Now go to /var/spool/asterisk/monitorDONE/MP3   ### if u record in gsm then goto GSM directory
9. select all and delete
9a. goto /var/log/  and delete  message.1,2,4 secure.1,2,3...  ,boot.1,2,3.....
10. now login to the server via ssh using putty
11. type /etc/init.d/mysqld start
12. type mysqlcheck -u cron -p --auto-repair --check --optimize --all-databases
13. password : 1234
14. once finishes the repair of the MYSQL
15. reboot the server and check wheter you are getting above error

Troubleshoot due to powecut or overload on the server

1. login to the server via ssh using putty
2. type mysqlcheck -u cron -p --auto-repair --check --optimize --all-databases
3. password: 1234
4. once repairing finished
5. reboot the server
