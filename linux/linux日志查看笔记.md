linux日志查看笔记
========================================

## 基本命令
```
tail -n 10 system.log 查询日志尾部最后10行记录;
tail -n +10  system.log 查询10行之后所有的记录;
head -n 10 system.log 查询日志前十条记录;
head -n -10 system.log 查询日志除了后10行之外的所有记录;

```
## 关键信息查询
```
cat -n system.log | grep "关键字"  得到关键字所在行数;

```

## 根据关键信息的行数,查看关键信息前后日志

```
cat -n system.log |tail -n +100 | head -n 20
tail -n +100 表示查询100行之后的日志;
head -n 20 则表示在前面的查询结果里再查前20条记录;

```

## 按照日期查询
```
sed -n '/日期/,/日期/p' system.log
grep '日期' system.log 可以先查是否有日期存在;

```
## 查看日志分页,使用less,more
```
cat -n system.log |grep "关键字" | more
按空格键翻页


```
