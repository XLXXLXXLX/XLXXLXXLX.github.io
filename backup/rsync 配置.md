客户端，在不同文件系统中使用rsync时，可能出现文件系统时间格式不兼容，由于我也不在意文件时间的同步，于是加上了`--no-times`参数，端口默认值为873，可以自定义：
```sh
rsync -avzsPuriy --no-times --delete "rsync://username@ip:port/path/to/folder" /localpath/to/folder
```
服务端：
```
sudo apt install rsync
sudo systemctl enable --now rsync
```