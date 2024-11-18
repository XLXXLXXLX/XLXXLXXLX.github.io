生成ssh密钥对：
```sh
ssh-keygen -t rsa -b 4096 -C "miasanmia147@gmail.com"
```
ssh使用代理：
```
ssh ${target}  -T -c aes128-gcm@openssh.com -o ProxyCommand="nc -X 5 -x ${ip}:${port} %h %p" -o Compression=no -x"
```