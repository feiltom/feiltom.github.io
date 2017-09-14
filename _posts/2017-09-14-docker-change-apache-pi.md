---
layout: post
title: Config PID file for apache 2 in docker
subtitle: for perform easily docker start / stop
---
In Dockerfile add to change the PID file for apache 2
```    
RUN sed -i "s/PidFile/#PidFile/g" /etc/apache2/apache2.conf
RUN echo "PidFile /dev/shm/apache.pid" >> /etc/apache2/apache2.conf
```
