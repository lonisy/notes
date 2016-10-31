
PHP开发笔记
==========


### json_encode 返回json 的 时候

>
> json_encode(array()) =>  返回js数组  => `[]`
> json_encode(new stdClass()) =>  返回js对象 => `{}`
>

### var_dump输出没有格式化的问题
1. 首先要安装 xdebug 扩展
2. 修改php.ini 文件中 html_errors=On
3. 重启php服务


### 获取本周一的日期
```
/**
 * 并不是一个合适的方式,结果不对, 有文章指出是PHP的 bug
 */
date("Y-m-d 00:00:00", strtotime("Monday"));  

// 改为
$currentMonday = date('w') == 1 ? date('Y-m-d 00:00:00') : date("Y-m-d 00:00:00", strtotime("last Monday"));

```
