---
title: Git server Synology
date: 2022-01-06 12:00:00 -500
categories: [homelab, software]
tag: [git, synology]        #TAG names should always be lowercase
---

# Setup Git server Synology
ssh gituser@diskstation.local
mkdir /volume1/homes/gituser/.ssh

ssh-keygen
cp ~/.ssh/id_rsa.pub ~/
scp ~/Users/<user>/id_rsa.pub gituser@diskstation.local:/volume1/homes/gituser/.ssh

sudo -i

mv /volume1/homes/gituser/.ssh/id_rsa.pub /volume1/homes/gituser/.ssh/authorized_keys

cd /volume1/homes/gituser/
chown -R gituser:users .ssh
chmod 700 .ssh
chmod 644 .ssh/authorized_keys

cd /volume1/homes/
cdmod 755 gituser

cd /volume1/git/
git --bare init server.git
chmod -R 766 server.git
chown -R gituser:users server.git
cd server.git
git update-server-info

git clone ssh://gituser@diskstation.local/volume1/git/server.git

nano test.txt

git add .
git commit -m ‘first commit’ 
git push origin
