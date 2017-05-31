
## 概要
```shell
ssh-keygen
scp .ssh/idrsa.pub root@10.20.25.144:idrsa.pub
cat idrsa.pub > .ssh/authorized_keys
chmod 600 .ssh/authorized_keys

``` 


