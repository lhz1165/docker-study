# Nginx配置

配置文件下载

/usr/local/business/attachment/2023818文件夹下面有文件

 http://localhost:9002/app-system/attachment/（必须以/结尾）  

可以访问到/usr/local/business/attachment  目录

```config
  
  
  
   location  /app-system/attachment/ {
                alias /usr/local/business/attachment/; # 必须加/
         	add_header Access-Control-Allow-Origin '*';
			add_header Access-Control-Allow-Methods 'GET, POST, OPTIONS, PUT, DELETE';
			add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';
        if ($request_filename ~* ^.*?\.(html|doc|pdf|zip|docx|txt)$) {
            add_header Content-Disposition attachment;
            add_header Content-Type application/octet-stream;
        }
            sendfile on;   # 开启高效文件传输模式
            autoindex on;  # 开启目录文件列表
            autoindex_exact_size on;  # 显示出文件的确切大小，单位是bytes
            autoindex_localtime on;  # 显示的文件时间为文件的服务器时间
            charset utf-8,gbk;  # 避免中文乱码
      }
```

 http://localhost:9002/attachment/

可以访问到/usr/local/business/attachment  目录,root会拼接url

```
 location  /attachment/ {
        root /usr/local/business/; # 必须加/
 
        if ($request_filename ~* ^.*?\.(html|doc|pdf|zip|docx|txt)$) {
            add_header Content-Disposition attachment;
            add_header Content-Type application/octet-stream;
        }
            sendfile on;   # 开启高效文件传输模式
            autoindex on;  # 开启目录文件列表
            autoindex_exact_size on;  # 显示出文件的确切大小，单位是bytes
            autoindex_localtime on;  # 显示的文件时间为文件的服务器时间
            charset utf-8,gbk;  # 避免中文乱码
      }
      
      
```

