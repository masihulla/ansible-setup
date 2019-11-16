#! /bin/bash
yum update -y
amazon-linux-extras install ansible2
echo "please enter user name"
read id
adduser $id
passwd $id
echo "$id ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
sed -i s'/#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config
sed -i s'/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
service sshd restart
su - $id
ssh-keygen
echo "please enter the ip address of the remote host"
read ipadd
ssh-copy-id $id@$ipadd
