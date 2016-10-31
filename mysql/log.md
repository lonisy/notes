
### 允许指定IP使用该用户登录mysql服务
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'asd..123' WITH GRANT OPTION;
flush privileges;

GRANT ALL PRIVILEGES ON *.* TO 'root'@'10.26.49.171' IDENTIFIED BY 'asd..123' WITH GRANT OPTION;
flush privileges;


```
