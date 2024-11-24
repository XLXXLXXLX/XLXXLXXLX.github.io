Docker进入容器：
```sh
docker exec -it ${容器ID} /bin/bash
```
为`docker pull`添加代理：
在执行docker pull时，是由守护进程dockerd来执行。因此，代理需要配在dockerd的环境中。而这个环境，则是受systemd所管控，因此实际是systemd的配置。
```
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo vim /etc/systemd/system/docker.service.d/proxy.conf
```
写入以下内容：
```
[Service]
Environment="HTTP_PROXY=http://localhost:7890/"
Environment="HTTPS_PROXY=http://localhost:7890/"
Environment="NO_PROXY=localhost,127.0.0.1,.noproxy.com"
```