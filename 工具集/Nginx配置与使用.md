# Nginx 

Nginx 是一款轻量级的 Web 服务器/反向代理服务器及电子邮件（ IMAP/POP3 ）代理服务器，其特点是占有内存少，并发能力强。

## Nginx 常用功能

### Http代理，反向代理

Nginx 在做反向代理时，提供性能稳定，并且能够提供配置灵活的转发功能。 Nginx 可以根据不同的正则匹配，采取不同的转发策略。比如图片文件结尾的走文件服务器，动态页面走 web 服务器，并且 Nginx 对返回结果进行错误页跳转，异常判断等。如果被分发的服务器存在异常，他可以将请求重新转发给另外一台服务器，然后自动去除异常服务器。

### 负载均衡

Nginx 提供的负载均衡策略有 2 种：内置策略和扩展策略。内置策略为轮询，加权轮询，Ip hash。扩展策略，就天马行空，只有你想不到的没有他做不到的啦，你可以参照所有的负载均衡算法，给他一一找出来做下实现。

Ip hash 算法，对客户端请求的 ip 进行 hash 操作，然后根据 hash 结果将同一个客户端 ip 的请求分发给同一台服务器进行处理，可以解决 session 不共享的问题。

### web缓存

Nginx可以对不同的文件做不同的缓存处理，配置灵活，并且支持 FastCGI_Cache ，主要用于对 FastCGI 的动态程序进行缓存。配合着第三方的 ngx_cache_purge ，对制定的 URL 缓存内容可以的进行增删管理。

## Nginx 命令

Nginx 的操作命令需要在安装目录执行。

* 启动 Nginx

```
$ start nginx
// or
$ nginx
```

建议使用第一种，第二种会使你的 cmd 窗口一直处于执行中，不能进行其他命令操作。且由于nginx默认端口也是80端口，如果此时你的机器上开启了Apache或者IIS服务，切忌在启动nginx之前务必关闭IIS或Apache服务，否则nginx启动命令不会成功。

* 停止 Nginx

```
$ nginx -s stop
// or
$ nginx -s quit
```

nginx 停止命令 stop 与 quit 参数的区别在于 stop 是快速停止 nginx ，可能并不保存相关信息，quit 是完整有序的停止 nginx ，并保存相关信息。

* 重启 Nginx

```
$ nginx -s reload
```

当配置信息修改，需要重新载入这些配置时使用此命令。

* 重新打开日志文件

```
$ nginx -s reopen
```

* 更换配置文件

```
$ nginx -c xx.conf
```

此命令参数指定一个新的 nginx 配置文件来替换默认的 nginx 配置文件，如果你不确定新的 nginx 配置文件语法是否正确，你可以通过 `nginx -t -c xx.conf` 参数来测试，`-t` 参数代表不运行配置文件，而仅仅只是测试配置文件，即

```
$ nginx -t -c xx.conf
```

* 查看 Nginx 版本

```
$ nginx -v  // 简单显示 nginx 的版本信息;
$ nginx -V  // 不但显示 nginx 的版本信息，而且还显示nginx的配置参数信息;
```

## Nginx配置

### 文件结构

在安装目录下的 `conf/nginx.conf` 文件，Nginx 的默认配置文件就是放在这里。

Nginx 配置文件的注释符号为 `#`。

nginx文件结构：

```nginx
...              #全局块

events {         #events块
   ...
}

http      #http块
{
    ...   #http全局块
  server        #server块
  { 
    ...       #server全局块
    location [PATTERN]   #location块
    {
      ...
    }
    location [PATTERN] 
    {
      ...
    }
  }
  server
  {
    ...
  }
  ...     #http全局块
}
```

1. 全局块：配置影响 Nginx 全局的指令。一般有运行 Nginx 服务器的用户组，Nginx 进程 pid 存放路径，日志存放路径，配置文件引入，允许生成 worker process 数等。

2. events 块：配置影响 Nginx 服务器或与用户的网络连接。有每个进程的最大连接数，选取哪种事件驱动模型处理连接请求，是否允许同时接受多个网路连接，开启多个网络连接序列化等。

3. http 块：可以嵌套多个 server ，配置代理，缓存，日志定义等绝大多数功能和第三方模块的配置。如文件引入，mime-type 定义，日志自定义，是否使用 sendfile 传输文件，连接超时时间，单连接请求数等。

4. server 块：配置虚拟主机的相关参数，一个 http 中可以有多个 server 。

5、location 块：配置请求的路由，以及各种页面的处理情况。

### 配置命令解析

```nginx
########### 每个指令必须有分号结束 #################
#user administrator administrators;  # 配置用户或者组，默认为nobody nobody。
#worker_processes auto;  # 允许生成的进程数，默认为 1
#pid /nginx/pid/nginx.pid;   # 指定nginx进程运行文件存放地址
error_log log/error.log debug;  # 制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
# 工作模式及连接数上限
events {
    accept_mutex on;   # 设置网路连接序列化，防止惊群现象发生，默认为on
    multi_accept on;   # 设置一个进程是否同时接受多个网络连接，默认为off
    #use epoll;        # 事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
    worker_connections  1024;    # 最大连接数，默认为512
    # 并发总数是 worker_processes 和 worker_connections 的乘积
    multi_accept on;   # multi_accept 告诉nginx收到一个新连接通知后接受尽可能多的连接。
}
http {
    include       mime.types;   # 文件扩展名与文件类型映射表,类型由 mime.type 文件定义
    default_type  application/octet-stream;  # 默认文件类型，默认为text/plain
    #access_log off;  # 取消服务日志    
    log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for';  # 自定义日志格式
    access_log log/access.log myFormat;  # combined 为日志格式的默认值
    
    sendfile on;   # 允许 sendfile 方式传输文件，默认为 off，可以在 http 块，server 块，location 块。
    # sendfile 指令指定 nginx 是否调用 sendfile 函数（zero copy 方式）来输出文件，
    # 对于普通应用，必须设为 on,
    # 如果用来进行下载等应用磁盘IO重负载应用，可设置为 off，
    # 以平衡磁盘与网络I/O处理速度，降低系统的uptime.

    # 高效文件传输
    tcp_nopush on;
    tcp_nodelay on;
    
    types_hash_max_size 2048;
    # 影响散列表的冲突率。types_hash_max_size 越大，就会消耗更多的内存，但散列 key 的冲突率会降低，检索速度就更快。types_hash_max_size 越小，消耗的内存就越小，但散列 key 的冲突率可能上升。
    
    sendfile_max_chunk 100k;  # 每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
    keepalive_timeout 65;  # 连接超时时间，默认为75s，可以在http，server，location块。
 
    # 开启gzip压缩
    gzip  on;
    gzip_disable "MSIE [1-6].";
    gzip_comp_level  6;
    gzip_min_length  1000; # 配置对数据启用压缩的最少字节数。如果一个请求小于 1000 字节，我们最好不要压缩它，因为压缩这些小的数据会降低处理此请求的所有进程的速度。
    gzip_proxied     expired no-cache no-store private auth;
    gzip_types       text/plain application/x-javascript text/xml text/css application/xml;

    # 设定请求缓冲
    client_header_buffer_size    1k;
    large_client_header_buffers  2 1k;
    client_body_buffer_size      10K;
    client_max_body_size         8m;
    # Buffers：另一个很重要的参数为 buffer，如果 buffer 太小，Nginx 会不停的写一些临时文件，这样会导致磁盘不停的去读写，现在我们先了解设置 buffer 的一些相关参数：
    # client_header_buffer_size:用于设置客户端请求的 Header 头缓冲区大小，大部分情况 1KB 大小足够
    # large_client_header_buffers:该指令用于设置客户端请求的 Header 头缓冲区大小
    # client_body_buffer_size:允许客户端请求的最大单个文件字节数
    # client_max_body_size:设置客户端能够上传的文件大小，默认为 1m

    map $http_user_agent $outdated {  # 判断浏览器版本
            default                    0;
            "~MSIE [6-9].[0-9]"        1;
            "~MSIE 10.0"               1;
    }

    # 负载均衡
    upstream mysvr {   
        # ip_hash; # 每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器，可以解决 session 的问题。
        server 127.0.0.1:7878;  # weight=1 max_fails=2 fail_timeout=30s;
        server 192.168.10.121:3333 backup;  # 热备
        # weight：轮询权值，默认值为 1。
        # down：表示当前的 server 暂时不参与负载。
        # max_fails：允许请求失败的次数，默认为 1 。当超过最大次数时，返回 proxy_next_upstream 模块定义的错误。
        # fail_timeout：有两层含义，一是在 fail_timeout 时间内最多容许 max_fails 次失败；二是在经历了 max_fails 次失败以后，30s 时间内不分配请求到这台服务器。
        # backup ： 备份机器。当其他所有的非 backup 机器出现故障的时候，才会请求 backup 机器，因此这台机器的压力最轻。
        # max_conns： 限制同时连接到某台后端服务器的连接数，默认为 0。即无限制。
        # proxy_next_upstream ： 这个指令属于 http_proxy 模块的，指定后端返回什么样的异常响应
    }

    error_page 404 https://www.baidu.com; # 错误页
    
    # 设定虚拟主机配置
    server {
        listen       80;   # 监听端口
        keepalive_requests 120; # 单连接请求上限次数
        server_name  127.0.0.1;   # 监听地址，即设定访问地址
        root html;  # 定义服务器的默认网站根目录位置
        access_log  logs/nginx.access.log  main;  # 设定本虚拟主机的访问日志
        
        # 默认请求
        location  ~*^.+$ {       # 请求的 url 过滤，正则匹配，~ 为区分大小写，~* 为不区分大小写
            #root path;  # 根目录
            if ($outdated = 1){
                rewrite ^ http://oisbyqrnc.bkt.clouddn.com redirect;  #判断浏览器版本跳转
            }
            #index vv.txt;  # 默认访问页面
            try_files $uri $uri/ /index.html;
            deny 127.0.0.1;  # 拒绝的ip
            allow 172.18.5.54; # 允许的ip           
        } 

        location /api {  #代理API
            proxy_pass  http://mysvr;  # 请求转向mysvr 定义的服务器列表
            # proxy_set_header Host      $host;
            # proxy_set_header X-Real-IP $remote_addr;  # 在web服务器端获得用户的真实 ip
            # proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_redirect     off;
            proxy_connect_timeout 600; # nginx跟后端服务器连接超时时间(代理连接超时)
            proxy_read_timeout 600; # 连接成功后，后端服务器响应时间(代理接收超时)
            proxy_send_timeout 600; # 后端服务器数据回传时间(代理发送超时)
            proxy_buffer_size 32k; # 设置代理服务器（nginx）保存用户头信息的缓冲区大小
            proxy_buffers 4 32k; # proxy_buffers缓冲区，网页平均在32k以下的话，这样设置
            proxy_busy_buffers_size 64k; # 高负荷下缓冲大小（proxy_buffers*2）
            proxy_temp_file_write_size 64k; # 设定缓存文件夹大小，大于这个值，将从upstream服>务器传
            keepalive_requests 500;
            proxy_http_version 1.1;
            proxy_ignore_client_abort on;
        }
        
        error_page   500 502 503 504 /50x.html;  # 定义错误提示页面

        # 静态文件，nginx自己处理
        location ~ ^/(images|javascript|js|css|flash|media|static)/ {
            expires 30d;
            # 30天过期，静态文件不怎么更新的，可以设大一点，如果频繁更新，则可以设置得小一点。
        }

        # PHP 脚本请求全部转发到 FastCGI处理. 使用FastCGI默认配置.
        location ~ .php$ {
          fastcgi_pass 127.0.0.1:9000;
          fastcgi_index index.php;
          fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
          include fastcgi_params;
        }

        # 禁止访问 .htxxx 文件
        location ~ /.ht {
          deny all;
        }
    }

    #启用 https, 使用 http/2 协议
    server {
        listen       443 ssl;
        server_name  localhost;
        ssl on;
        ssl_certificate      cert.pem;  # 证书路径;
        ssl_certificate_key  cert.key;  # 私钥路径;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;  # 指定的套件加密算法
        ssl_prefer_server_ciphers  on;  # 设置协商加密算法时，优先使用我们服务端的加密套件，而不是客户端浏览器的加密套件。
        ssl_session_timeout 60m;        # 缓存有效期
        ssl_session_cache shared:SSL:10m;  # 储存SSL会话的缓存类型和大小
        location / {
            root   html;
            index  index.html index.htm;
        }
    }
}
```

上面是nginx的基本配置，需要注意的有以下几点：

1. `$remote_addr` 与 `$http_x_forwarded_for` 用以记录客户端的 ip 地址； 
2. `$remote_user`：用来记录客户端用户名称； 
3. `$time_local`：用来记录访问时间与时区；
4. `$request`：用来记录请求的 url 与 http 协议；
5. `$status`：用来记录请求状态，成功是 200； 
6. `$body_bytes_s ent`：记录发送给客户端文件主体内容大小；
7. `$http_referer`：用来记录从那个页面链接访问过来的； 
8. `$http_user_agent`：记录客户端浏览器的相关信息；

惊群现象：一个网路连接到来，多个睡眠的进程被同事叫醒，但只有一个进程能获得链接，这样会影响系统性能。
