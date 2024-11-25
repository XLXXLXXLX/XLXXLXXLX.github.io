```sh
sudo apt install tlp tlp-rdw
sudo systemctl enable --now tlp
suod vim /etc/tlp.conf
```
```
# in /etc/tlp.conf
CPU_SCALING_GOVERNOR_ON_AC=performance
CPU_SCALING_GOVERNOR_ON_BAT=powersave
DISK_APM_LEVEL_ON_AC="254"
DISK_APM_LEVEL_ON_BAT="128"
```

参考资料：
1. [使用 tlp 来为 linux 省电](https://www.meow-2.com/posts/linux/tlp-for-power-saving)
2. [TLP：一个可以延长 Linux 笔记本电池寿命的高级电源管理工具](https://linux.cn/article-10848-1.html)