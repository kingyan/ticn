yum install python3

yum install python-virtualenv

virtualenv env1

cd env1/

source bin/activate

python -V

mkdir /root/snap2html

cd /root/snap2html

wget https://github.com/ZapperDJ/DiogenesList/archive/master.zip

yum install unzip

unzip master.zip

cd /root/snap2html/DiogenesList-master/

rm -rf diogeneslist.py

wget https://share.dxz.plus/BlogContent/diogeneslist.py

curl https://rclone.org/install.sh | sudo bash

rclone config

...

mkdir /root/00

yum install fuse

rclone mount gd:bot /root/00 --copy-links --no-gzip-encoding --no-check-certificate --allow-other --allow-non-empty --umask 000

++++++++++++重启机器+++++++++++++++++

cd env1/

source bin/activate

command="mount gd:bot /root/00 --copy-links --no-gzip-encoding --no-check-certificate --allow-other --allow-non-empty --umask 000"

#以下是一整条命令，一起复制到SSH客户端运行
cat > /etc/systemd/system/rclone.service <<EOF
[Unit]
Description=Rclone
After=network-online.target

[Service]
Type=simple
ExecStart=$(command -v rclone) ${command}
Restart=on-abort
User=root

[Install]
WantedBy=default.target
EOF

+++++++++++++分割线+++++++++++++++

systemctl start rclone

systemctl enable rclone

cd /root/snap2html/DiogenesList-master/

python /root/snap2html/DiogenesList-master/diogeneslist.py /root/00 index

yum install git

mkdir /root/snapGit

cd /root/snapGit

git init

git remote add origin https://github.com/ticn/gd.git

git pull origin master

cd /root/snapGit

git config credential.helper store

git add .

git commit -m 'test'

git push -u origin master

nano /root/snapGit/snap.sh

#!/bin/bash
#cd /root/snap2html/DiogenesList-master/
#python /root/snap2html/DiogenesList-master/diogeneslist.py /root/00 index
sed -i "s#\[LINK ROOT\]#https://media.dxz.plus#g"  /root/snap2html/DiogenesList-master/index.html
sed -i "s#\[LINK PROTOCOL\]##g"  /root/snap2html/DiogenesList-master/index.html
sed -i "s#\[SOURCE ROOT\]##g"  /root/snap2html/DiogenesList-master/index.html
sed -i "s#\\\\\\\root\\\\\\\rclone\\\\\\\00##g"  /root/snap2html/DiogenesList-master/index.html
sed -i "s#1>index#1>所有内容均来自公开分享_收藏自用_侵权联系https://t.me/dxb22abad(telegram)#g" /root/snap2html/DiogenesList-master/index.html
sed -i "s#e>index#e>00盘_用法详见dxz.plus#g" /root/snap2html/DiogenesList-master/index.html
cp /root/snap2html/DiogenesList-master/index.html /root/snapGit/
cd /root/snapGit
git add .
git commit -m 'snap2htmlDailyUpdate'
git push  https://github.com/ticn/gd.git

chmod +x /root/snapGit/snap.sh
nano /etc/crontab

0 3 * * * root /root/snapGit/snap.sh
