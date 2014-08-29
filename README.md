cl-search
==================

基于Solr的搜索系统


一、前置项目依赖

https://github.com/pumadong/cl-commodity

Solr官网：http://lucene.apache.org/solr/

二、项目说明

简单演示对商品信息的全量索引建立、主从配置以及搜索的Dubbo接口提供。

对Solr做了入门型的说明，基本满足基于Solr的搜索的日常应用，对于更多Solr的参数设置，深入研究需要在实践中不断总结进步。

Solr版本4.9.0，关于Solr4.9.0的入门级使用，基本配置、中文分词、主从配置，可以参阅这篇文章：

http://blog.csdn.net/puma_dong/article/details/38880699

关于索引，基本内容大致包含如下：商品（编码，款号、名称、价格、尺码编号、尺码名称、颜色、价格、折扣、图片链接、销量）、分类（名称、别名、编码、拼音名称）、品牌（编码、中英文名称、别名、拼音名称、首字母拼音名称）、商品的属性项目（属性值），以及一些用来排序的信息：销量、价格、折扣等。对于品牌分类等，需要同时记录英文名称。 

索引还需要一些管理控制功能，比如脏词屏蔽、扩展词库等；为了提高建立索引的效率，可能还需要对一些中间结果进行计算，比如：商品的2周销售数量。

注：关于分类的别名、品牌的别名之类，不建议在搜索系统中单独为，建议提需求给商品管理系统。

本项目仅仅是演示的雏形，流程是可用的，单没有完整的信息完整的索引创建、索引接口、及管理控制功能，这个留待以后是否有足够的业余时间。

索引建立的运行方式如下：

crontab: */10 * * * * /usr/local/cl/create_index.sh &

三、技术框架

在索引建立项目中，没有使用任何框架，使用最基础的JDK编码，定时任务方式采用crontab，任务流程控制采用linux shell命令。

索引查询接口项目中，依旧是采用dubbo提供接口。 