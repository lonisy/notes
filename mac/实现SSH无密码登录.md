## [实现SSH无密码登录](https://wangheng.org/implement-ssh-without-password.html)

有问题暂时不提交

**一、在Linux中**

有机器A[192.168.1.1]，B[192.168.1.2]。现想A通过ssh免密码登录到B。
**第一步，在A机下生成公钥/私钥对。**

```

```

[![image](https://wangheng.org/wp-content/uploads/2012/07/image_thumb.png)](https://wangheng.org/wp-content/uploads/2012/07/image.png)

直接三次回车，它将在~/下生成.ssh目录，.ssh下有id_rsa和id_rsa.pub。

**第二步，把A机下的id_rsa.pub复制到B机下**

完成后还需要将id_rsa.pub内容追加到B机的.ssh/authorized_keys文件里。

```

```

由于还没有免密码登录的，所以这里还要输入密码。 输入B机器的登录密码后，文件就复制到了B机器的~/目录。

**第三步、B机把从A机复制的id_rsa.pub添加到.ssh/authorzied_keys文件里。**

**authorized_keys的权限必须是600。(**要保证.ssh和authorized_keys都只有用户自己有写权限。否则验证无效。)

**第四步、验证A机无密码登录B机。**

第一次登录时如果询问是否将B机器加到A机器的list of known hosts，还需要你输入yes。现在A机可以无密码登录B机了。

**小结：**私钥文件也可以保存下来在别的机器上面使用，被登录的机子要有登录机子的公钥。这个**公钥/私钥对**一般在私钥宿主机产生。想让A，B机无密码互登录，B机器上重复以上步骤即可~

**二、在Windows中**

在Windows中要想实现无密码登录Linux主机也很简单。一般在Windows中远程ssh连接Linux主机大家都会使用[putty](http://wangheng.org/url/http://www.putty.org/) 或者Tunnelier这样的工具，我一般使用Tunnelier比较多，因为它集成了sftp工具和其他一些很实用的功能。例如使用Tunnelier很容易实现[Firefox+SSH+AutoProxy智能翻墙](http://wangheng.org/firefox-the-ssh-the-autoproxy-smart-over-wall.html)，想试试的同学可以翻翻我以前发过的文章。下面具体介绍Windows下使用putty无密码登录Linux

1、首先使用PUTTYGEN.EXE这个工具生成**公钥/私钥对，**点击Generate，并在空白处移动鼠标几次就行了，如下：

[![image](https://wangheng.org/wp-content/uploads/2012/07/image_thumb1.png)](https://wangheng.org/wp-content/uploads/2012/07/image1.png)

2、选择Save public key和Save private key可以分别保存公钥和私钥，然后将public key的内容追加到Linux主机中的**.ssh/authorzied_keys文件里。**

3、使用putty这个工具创建自动登录的session

首先在Session节点填写Host Name和你Linux VPS的ssh端口，然后在/Connection/SSH/Auth节点选择你Private key文件的保存位置，然后在/Connection/Data节点填写自动登录的用户名，最后在Session节点为Session起一个名字并保存，以后就可以直接双击保存的Session名字来自动无密码登录Linux主机了。