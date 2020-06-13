---
layout:     post
title:      Python Celery介绍
subtitle:   Python Celery介绍
date:       2020-06-13
author:     wangzw
header-img: img/fenbushi.jpeg
catalog: true
tags:
    - Python分布式
---

# Celery图解
  ![avatar](img/celery.jpg)

  如上图所示，由三部分组成：消息中间件（message broker）、任务执行单元（worker）、任务执行结果存储（task result store）

##消息中间件
Celery本身不提供消息服务，但是可以方便的和第三方提供的消息中间件集成。包括，RabbitMQ, Redis, MongoDB (experimental), Amazon SQS (experimental),CouchDB (experimental), SQLAlchemy (experimental),Django ORM (experimental), IronMQ

##任务执行单元
Worker是Celery提供的任务执行的单元，worker并发的运行在分布式的系统节点中。

##任务结果存储
Task result store用来存储Worker执行的任务的结果，Celery支持以不同方式存储任务的结果，包括AMQP, Redis，memcached, MongoDB，SQLAlchemy, Django ORM，Apache Cassandra, IronCache

# Celery 简介

    除了redis，还可以使用另外一个神器---Celery。Celery是一个异步任务的调度工具。

    Celery 是 Distributed Task Queue，分布式任务队列，分布式决定了可以有多个 worker 的存在，队列表示其是异步操作，即存在一个产生任务提出需求的工头，和一群等着被分配工作的码农。

    在 Python 中定义 Celery 的时候，我们要引入 Broker，中文翻译过来就是“中间人”的意思，在这里 Broker 起到一个中间人的角色。在工头提出任务的时候，把所有的任务放到 Broker 里面，在 Broker 的另外一头，一群码农等着取出一个个任务准备着手做。

    这种模式注定了整个系统会是个开环系统，工头对于码农们把任务做的怎样是不知情的。所以我们要引入 Backend 来保存每次任务的结果。这个 Backend 有点像我们的 Broker，也是存储任务的信息用的，只不过这里存的是那些任务的返回结果。我们可以选择只让错误执行的任务返回结果到 Backend，这样我们取回结果，便可以知道有多少任务执行失败了。

    Celery(芹菜)是一个异步任务队列/基于分布式消息传递的作业队列。它侧重于实时操作，但对调度支持也很好。Celery用于生产系统每天处理数以百万计的任务。Celery是用Python编写的，但该协议可以在任何语言实现。它也可以与其他语言通过webhooks实现。Celery建议的消息队列是RabbitMQ，但提供有限支持Redis, Beanstalk, MongoDB, CouchDB, 和数据库（使用SQLAlchemy的或Django的 ORM） 。

    Celery是易于集成Django, Pylons and Flask，使用 django-celery, celery-pylons and Flask-Celery 附加包即可。


