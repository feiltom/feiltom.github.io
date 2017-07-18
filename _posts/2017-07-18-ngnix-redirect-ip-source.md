---
layout: post
title: Config ngnix redirection en fonction de l ip source
subtitle: Si l Ip est differente on redirige
---
    
```
geo $bad_user {
  default 1;
  1.2.3.4/32 0;
  4.2.3.4/32 0;
}

server {
    listen 80;
	server_name example.com;
  if ($bad_user) {
    rewrite ^ http://www.feillant.com;
  }
```

