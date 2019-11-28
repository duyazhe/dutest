# caddy
> caddy是一款由 Go 编写的 Web Server，与 Nginx 相比，最大的特点就是部署简单并默认启用 HTTPS，它是第一个无需额外配置即可提供 HTTPS 特性的 Web 服务器。

##特性

 1. HTTP/2 全自动支持HTTP/2协议，无需任何配置。 
 2. Auto HTTPS Caddy 使用 Let’s Encrypt让你的站点全自动变成全站HTTPS，无需任何配置。当然你想使用自己的证书也是可以的。 
 3. Multi-core因为caddy是golang写的，所以当然可以合理使用多核啦。 IPv6 完全支持IPv6环境. 
 4. WebSockets Caddy对WebSockets有很好的支持. 
 5. Markdown 自动把md转成 HTML.
 6. Logging Caddy 对log格式的定义很容易，更好的满足你日志收集的需求。 
 7. Easy Deployment 得益于go的特性，caddy只是一个小小的二进制文件，没有依赖，很好部署

## Let’s Encrypt
>Let's Encrypt 是一个免费、开放，自动化的证书颁发机构，由 ISRG（Internet Security Research Group）运作。ISRG 是一个关注网络安全的公益组织，其赞助商包括 Mozilla、Akamai、Cisco、EFF、Chrome、IdenTrust、Facebook等公司。ISRG 的目的是消除资金和技术领域的障碍，全面推进网站从HTTP到HTTPS过度的进程。

##安装
> github:https://github.com/caddyserver/caddy/
> 源码编译

##配置
```json
http://su.bj1993.net, https://su.bj1993.net {
        gzip
        root  /home/caddy/html
        fastcgi / /tmp/php-cgi.sock php
        log /home/caddy/log/caddy.access.log

        git {
                repo https://github.com/duyazhe/dutest.git
                path /home/caddy/html_git
                clone_args --recursive
                pull_args --recurse-submodules
                key /root/.ssh/id_rsa
                hook /hook duyazhe
                hook_type github
                then  sh /home/caddy/a.sh
        }
}

http://www.bj1993.net {
        proxy / localhost:8080 {
                header_upstream Host {host}
                header_upstream X-Real-IP {remote}
                header_upstream X-Forwarded-For {remote}
                header_upstream X-Forwarded-Port {server_port}
                header_upstream X-Forwarded-Proto {scheme}
        }
        gzip
}
```

> 自动申请证书，申请完证书存放在~/.caddy/acme/acme-v02.api.letsencrypt.org/sites/位置
![图片](https://agroup-bos.cdn.bcebos.com/eefc8a45f543bd66dd58a5130d01444262fe9cc0)

##webhook配置
![图片](https://agroup-bos.cdn.bcebos.com/7ff7cafb956392385af3544e606afa7c8107bfd8)

