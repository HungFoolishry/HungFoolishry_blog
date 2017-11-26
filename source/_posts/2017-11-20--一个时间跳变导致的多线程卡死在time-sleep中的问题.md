---
title: 一个时间跳变导致的多线程卡死在time.sleep中的问题
date: 2017-11-20 21:18:49
categories: Python
tags: ['Thread']
---

最近在公司遇到一个多线程卡死的问题：在对多个主机进行多线程操作的时候，主机的时钟进行ntp同步后进行了往后跳变，导致在线程进入time.sleep的时候卡死的问题。
<!-- more -->

主要问题在于，在用多线程进行time.sleep切换的时候，社区的oslo service 采用了wall clock，导致线程进行time sleep切换后，无法等待至end time。比如 end_time = start_time + sleep_time，比如说start_time =7:00，在进入sleep time（10s） 后，start_time由于主机的时钟同步，导致start_time时光回溯，start_time=6:00。此刻，多线程一直卡死在time.sleep(10)的状态下，一直等一个小时10秒后，才能进行sleep后的操作。

解决办法:
1,采用libc中time sleep，该sleep是monotonic clock，不会产生时光回溯的问题。但是该时钟在实际使用中无法实现time.sleep的多线程切换的功能。所以我进行了小小的改动，虽然不完善，后续会研究更加完美的方法。
2，暂时办法：用libc.time.sleep（1）然后紧跟time.sleep(0.0005)
第一个sleep可以进行正常的延迟，第二个超短时间的延迟用于线程的切换。

阅读的文档：

[Python 官方代码threading模块的一个死锁的bug](http://i2cbus.blog.51cto.com/9231371/1534933 "http://i2cbus.blog.51cto.com/9231371/1534933") 

[how-do-i-get-monotonic-time-durations-in-python](https://stackoverflow.com/questions/1205722/how-do-i-get-monotonic-time-durations-in-python)

- OpenStack社区上的相关bug
Relate issue: https://bugs.launchpad.net/mos/+bug/1642103 services hang when time is jumping forward and backward
Related patch that fixes the issue for oslo: 
https://review.openstack.org/#/c/190372/
Same topic:
https://review.openstack.org/#/c/286838/
https://review.openstack.org/#/c/434327