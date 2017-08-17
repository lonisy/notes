
Phalcon 开发笔记
=======
以下笔记开发中遇到的问题,以及处理方法,不定期更新

### 跨域问题
跨域设置主要考虑两方面,一是服务器跨域配置, 二是服务端响应头设置
在phalcon 开发接口时,跨域请求需要配置
```
...
$this->response->setHeader('Access-Control-Allow-Origin','*');
$this->response->send();
...
```

### phalcon 控制器的方法名大小写问题
该问题主要体现在,程序上线后, 在运行的时候会遇到   
比如: StockFunds 控制器   
访问的时候  \*\*\*/stockFunds/  错误  
访问的时候  \*\*\*/stockfunds/  错误  
访问的时候  \*\*\*/stock_funds/  正确  

建议1: 根据路由写过滤条件,或者转换方式
建议2: 控制器尽量用一个单词标示,或者多个单词均为小写标示



### model 中关联表的用法
$account->getStockContestInfo();  获取相关模型的信息

### $this->flash->success(); 的用法
输出是在目标模板中使用 {{ content() }}
