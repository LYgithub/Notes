# IP代理
#爬虫

## 代理池的要求

* 多站抓取，异步检测
* 定时筛选，持续更新
* 提供接口，易于提取

## 代理池架构

```
获取器-> 过滤器 -> 代理队列 1->定时监测  2-> API
```
[17](https://www.bilibili.com/video/av90928927?p=17) ~[18](https://www.bilibili.com/video/av90928927?p=18)

# PySpider框架
安装 pip3 install PySpider


## 随机取出一条记录
select * from table 
order by rand()
limit 1