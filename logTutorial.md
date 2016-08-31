---
layout: post
title:  "python log Tutorial "
date:   August 31, 2016 10:40 PM
categories: blog
---

## 概述 ##
日志可以指示程序的运行状态、事件，帮助调试程序。python日志可以根据事件的重要性选择日志的输出等级。
## 选择日志等级
* 通用的console输出：print（）
* 程序能正常运行是报告事件：logging.info() (or logging.debug() 输出详细信息或诊断）
* 运行是可能出告警：logging.warning()-程序不能修改，但是特殊事件还是需要报告    ;warnings.warn()-问题可以避免，应该修改代码来消除告警。
* 运行时可能出现错误：抛出异常
* 出现错误不抛出异常：logging.error(),logging.exception(),logging.critical()

## 日志等级
* DEBUG:详细信息
* INFO：确认代码逻辑符合预期
* WARNING：代码运行符合预期，但可能出现问题
* ERROR：严重问题，某些功能不可用
* CRITICAL：程序崩溃
  *默认等级WARNING，被跟踪到的消息通常输出到console或写入日志文件*
 
### example
日志输出到console：
````
import logging
logging.warning('Watch out!')  # will print a message to the console
logging.info('I told you so')  # will not print anything

````
日志输出到文件：
```
import logging
logging.basicConfig(filename='example.log',level=logging.DEBUG)
logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
```
打开example.log 可以看到输出了所有的信息。

## python设置日志等级的输出
除了上面例子里，在代码里面调用logging.basicConfig()设置日志等级，还可以通过类似命令行参数来设置，如--log=INFO
```
numeric_level = getattr(logging, loglevel.upper(), None)
if not isinstance(numeric_level, int):
    raise ValueError('Invalid log level: %s' % loglevel)
logging.basicConfig(level=numeric_level, ...)
```
logging.basicConfig()应该在调用logging.XX之前。

可以设置每次输出的日志覆盖之前的日志。
```
logging.basicConfig(filename='example.log', filemode='w', level=logging.DEBUG)
```
## 设置日志输出的格式
<pre><code>
import logging
logging.basicConfig(format='%(levelname)s:%(message)s', level=logging.DEBUG)
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')

</code></pre>
输出：
```
DEBUG:This message should appear on the console
INFO:So should this
WARNING:And this, too

```
## 设置日志输出时间
```
import logging
logging.basicConfig(format='%(asctime)s %(message)s')
logging.warning('is when this event was logged.')

```
输出：
```
2016-08-31 21:22:12,825 is when this event was logged.
```

