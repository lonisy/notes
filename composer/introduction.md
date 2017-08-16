## Composer 介绍
编写日期: 2017-08-16

[Composer 英文网站](https://getcomposer.org/)
[Composer 中文网站](http://www.phpcomposer.com/)

### 简介

Composer 是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。

### 安装

下载 Composer 的可执行文件

#### Linux or unix 操作系统
```
# 局部安装
curl -sS https://getcomposer.org/installer | php

# 全局安装
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer

# 全局安装 OSX
brew update
brew tap josegonzalez/homebrew-php
brew tap homebrew/versions
brew install php55-intl
brew install josegonzalez/php/composer
```
#### Windows 操作系统

1. 使用安装程序安装

下载并且运行 [Composer-Setup.exe](Composer-Setup.exe)，它将安装最新版本的 Composer ，并设置好系统的环境变量，因此你可以在任何目录下直接使用 composer 命令。

2. 动手安装 Composer

```
C:\Users\username>cd C:\bin
C:\bin>php -r "readfile('https://getcomposer.org/installer');" | php
```

> **注意**： 如果收到 readfile 错误提示，请使用 http 链接或者在 php.ini 中开启 php_openssl.dll 

[参考资料](http://docs.phpcomposer.com/00-intro.html#Dependency-management)

### 镜像用法

[参考资料](https://pkg.phpcomposer.com/#how-to-use-packagist-mirror)

#### 全局配置
系统全局配置： 即将配置信息添加到 Composer 的全局配置文件 config.json 中。

```
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

#### 单个项目配置
单个项目配置： 将配置信息添加到某个项目的 composer.json 文件中。

```
$ composer config repo.packagist composer https://packagist.phpcomposer.com
# 或者直接修改 项目中的 composer.json 文件, 手工添加一下代码

"repositories": {
    "packagist": {
        "type": "composer",
        "url": "https://packagist.phpcomposer.com"
    }
}
```

### 使用

```
require 'vendor/autoload.php';
```



### 相关命令

```
$ composer -V                // 显示 Composer 版本
$ php composer.phar install  // 局部安装 要解决和下载依赖 执行命令
$ composer install           // 全局安装 在当前项目下初始化 Composer 
$ composer require "foo/bar:1.0.0" // 安装一个依赖包
$ composer update            // 更新依赖
$ composer update foo/bar    // 更新指定依赖
$ composer update --lock     // 锁定 Composer 状态, 在确保当前依赖足够新, 切稳定的情况下
$ composer create-project doctrine/orm path 2.2.0  // 签出指定版本的依赖包
$ composer dump-autoload --optimize // 部署到生产时 需要优化自动加载, 性能提示20%~25%
```


### 常用项目

[常用的 Composer Package](https://github.com/baiy/composer-package)


#### 微信相关
```
$ composer require "overtrue/wechat"	
```
[Easy We Chat 微信 SDK](https://easywechat.org/)

#### 二维码
```
$ composer require endroid/qrcode
```
https://packagist.org/packages/endroid/qrcode

#### 请求类

```
$ composer require guzzlehttp/guzzle
```
https://packagist.org/packages/guzzlehttp/guzzle

#### 日志

```
$ composer require monolog/monolog
```

https://packagist.org/packages/monolog/monolog

#### ORM

```
$ composer require catfan/medoo
```

https://packagist.org/packages/catfan/medoo

#### 邮件相关

```
$ composer require phpmailer/phpmailer
```

https://packagist.org/packages/phpmailer/phpmailer

#### 图片处理

```
$ composer require intervention/image
```

https://packagist.org/packages/intervention/image

#### PHP 函数补充

```
$ composer require phpcollection/phpcollection
```

https://packagist.org/packages/phpcollection/phpcollection

#### 框架

YII 框架
```
$ composer create-project yiisoft/yii2-app-basic basic 2.0.12          // 基础应用程序模板
$ composer create-project yiisoft/yii2-app-advanced advanced 2.0.12    // 高级应用程序模板
```
[参考资料](http://www.yiichina.com/download)


Laravel 框架

```
$ composer global require "laravel/installer"   // 全局安装 laravel 手脚架
$ composer create-project --prefer-dist laravel/laravel blog  // 使用 composer 创建 laravel 项目
```
[参考资料](https://laravel.com/docs/5.4)

### 其他

