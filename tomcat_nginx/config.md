# tomcat+nginx 负载均衡
  nginx.conf
  1，nginx代理tomcat
     location / {
       proxy_pass http://tomcat_8111_8222;
       }

  2,动静分离
     location ~\.(css|js|png)$ {
       root F:/Project/learn/how2j/tomcat_8111/webapps/ROOT;
       }

  3,负载均衡

     upstream tomcat_8111_8222 {
      server 127.0.0.1:8111 weight=2;
      server 127.0.0.1:8222 weight=1;
      }

##tomcat session共享
    每个tomcat lib文件导入jar包
    分别在context.xml中配置
   “<Valve className="com.orangefunction.tomcat.redissessions.RedisSessionHandlerValve" />
    "<Manager className="com.orangefunction.tomcat.redissessions.RedisSessionManager"
   host="127.0.0.1"
   port="6379"
   database="0"
   maxInactiveInterval="60" />"

