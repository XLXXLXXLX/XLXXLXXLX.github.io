下文中的`${xxx}`仅仅代表此处为自定义，`[xxx]`表示此处为可选值，并非需要使用这些格式。
服务端（Ubuntu 22.04）：
```sh
sudo apt install samba

sudo smbpasswd -a [username]

sudo vim /etc/samba/smb.conf
####################
#在文件底部新增如下内容
[${NetworkDeviceName}]
path = /path/to/share_folder
available = yes
guest ok = no
browseable = yes
writable = yes
valid users = ${username} root 
####################

sudo systemctl enable --now samba
```

客户端（Debian 12）：
```
sudo mount -t cifs //ip_or_domain_of_samba/${NetworkDeviceName} /mnt/${mount_dirname} -o username=${username},password=${password} [,port=${port}]
```