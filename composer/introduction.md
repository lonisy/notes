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

[中国全量镜像地址](https://pkg.phpcomposer.com/)



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

| 名称                                       | 用途说明                                     | 说明地址                                     |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| [mashape/unirest-php](https://packagist.org/packages/mashape/unirest-php) | 简单易用的HTTP请求库                             | [官网](http://unirest.io/)                 |
| [guzzlehttp/guzzle](https://packagist.org/packages/guzzlehttp/guzzle) | 功能强大的HTTP请求库                             | [文档](http://guzzlephp.org/)              |
| [hassankhan/config](https://packagist.org/packages/hassankhan/config) | 轻量级配置加载类,支持多种配置格式`PHP, INI, XML, JSON, and YML` |                                          |
| [desarrolla2/cache](https://packagist.org/packages/desarrolla2/cache) | 简单的缓存类,提供多种缓存驱动`Apc, Apcu, File, Mongo, Memcache, Memcached, Mysql, Mongo, Redis` |                                          |
| [phpFastCache/phpFastCache](https://packagist.org/packages/phpFastCache/phpFastCache) | PHP 缓存库,支持apc, memcache, memcached, wincache, files, pdo and mpdo | [官网](http://www.phpfastcache.com/)       |
| [hashids/hashids](https://packagist.org/packages/hashids/hashids) | 数字ID生成类似优酷视频ID,支持多语言,支持加盐生成              | [官网](http://hashids.org/)                |
| [sika/sitemap](https://packagist.org/packages/sika/sitemap) | XML网站地图生成器                               |                                          |
| [catfan/medoo](https://packagist.org/packages/catfan/medoo) | 简单易用数据库操作类 支持各种常见数据库                     | [文档](http://medoo.in/doc)                |
| [rize/uri-template](https://packagist.org/packages/rize/uri-template) | URL生成                                    |                                          |
| [jdorn/sql-formatter](https://packagist.org/packages/jdorn/sql-formatter) | SQL语句格式化 支持语法高亮                          |                                          |
| [intervention/image](https://packagist.org/packages/intervention/image) | 图片处理,提供对图片的各种操作:获取图片信息,上传,格式转换,缩放,裁剪等等等  | [文档](http://image.intervention.io/)      |
| [phpmailer/phpmailer](https://packagist.org/packages/phpmailer/phpmailer) | 邮件发送                                     |                                          |
| [phpoffice/phpexcel](https://packagist.org/packages/phpoffice/phpexcel) | excel操作类                                 | [文档](https://github.com/PHPOffice/PHPExcel/wiki/User%20Documentation) |
| [league/route](https://packagist.org/packages/league/route) | 路由调度                                     | [文档](http://route.thephpleague.com/)     |
| [willdurand/jsonp-callback-validator](https://packagist.org/packages/willdurand/jsonp-callback-validator) | JSONP callback参数验证 防止XSS攻击               |                                          |
| [michelf/php-markdown](https://packagist.org/packages/michelf/php-markdown) | PHP markdown 解析                          | [官网](https://daringfireball.net/projects/markdown/) |
| [erusev/parsedown](https://packagist.org/packages/erusev/parsedown) | PHP markdown 解析                          | [演示](http://parsedown.org/tests/) [文档](https://github.com/erusev/parsedown/wiki/) |
| [league/html-to-markdown](https://packagist.org/packages/league/html-to-markdown) | HTML转markdown                            |                                          |
| [monolog/monolog](https://packagist.org/packages/monolog/monolog) | 日志操作 composer官方就是用它做例子                   | [文档](https://github.com/Seldaek/monolog/blob/HEAD/doc/01-usage.md) |
| [phpcollection/phpcollection](https://packagist.org/packages/phpcollection/phpcollection) | PHP 集合操作                                 | [文档](http://jmsyst.com/libs/php-collection) |
| [seld/jsonlint](https://packagist.org/packages/seld/jsonlint) | JSON 语法检查                                |                                          |
| [geoip2/geoip2](https://packagist.org/packages/geoip2/geoip2) | IP地理位置信息                                 |                                          |
| [league/csv](https://packagist.org/packages/league/csv) | CSV操作类                                   | [例子](https://github.com/thephpleague/csv/tree/master/examples) |
| [jalle19/php-whitelist-check](https://packagist.org/packages/jalle19/php-whitelist-check) | IP/网址黑白名检查 支持模糊匹配                        |                                          |
| [shark/simple_html_dom](https://packagist.org/packages/shark/simple_html_dom) | php解析html类库                              | [文档](http://simplehtmldom.sourceforge.net/) |
| [naux/auto-correct](https://packagist.org/packages/naux/auto-correct) | 自动给中英文之间加入合理的空格并纠正专用名词大小写                |                                          |
| [fabpot/goutte](https://packagist.org/packages/fabpot/goutte) | PHP 爬虫库 它提供了一个优雅的 API，这使得从远程页面上选择特定元素变得简单 |                                          |
| [meenie/munee](https://packagist.org/packages/meenie/munee) | 一个集图片尺寸调整、CSS-JS合并/压缩、缓存等功能于一身的PHP库      | [官网](http://mun.ee/)                     |
| [league/flysystem](https://packagist.org/packages/league/flysystem) | 一个文件系统抽象层,为各类型文件操作(本地/Azure/Aws/FTP/内存等)提供统一的操作接口 | [官网](https://flysystem.thephpleague.com/) |
| [overtrue/wechat](https://easywechat.org/) | 一个简单易用,且全面的微信 SDK                        | [官网](https://easywechat.org/)            |
| [php-curl-class/php-curl-class](https://packagist.org/packages/php-curl-class/php-curl-class) | PHP通用请求类                                 | [官网](https://github.com/php-curl-class/php-curl-class) |

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

