

find ./ -type f -mtime +30  -print
sudo find ./ -type f -mtime +30 -delete
find . -type d -empty -find
sudo find . -type d -empty -delete

10 0 * * *  find /home/ec2-user/efs/es-log -type f -mtime +30 -delete
10 0 * * *  find /home/ec2-user/efs/es-log -type d -empty -delete