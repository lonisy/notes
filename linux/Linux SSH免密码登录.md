
## 概要
```shell
ssh-keygen
scp .ssh/id_rsa.pub root@10.20.25.144:/root/id_rsa.pub
cat id_rsa.pub > .ssh/authorized_keys
chmod 600 .ssh/authorized_keys

``` 


