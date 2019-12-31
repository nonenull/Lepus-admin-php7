# Lepus-php7
修改 天兔后台系统 支持 PHP7 

升级依赖的 Codeigniter 框架到 3.1.11 版本


## 安装

Ubuntu 18.04.1 LTS
PHP 7.2


apt install php7.2 php7.2-mysql php7.2-fpm
systemctl status php7.2-fpm && systemctl restart php7.2-fpm



## Nginx 配置

server {
        listen       80;
        listen       [::]:80;
        # 这里写你的域名
        server_name xxx;
        
        # 默认网站根目录（www目录）
        root         xxx;
	    index index.php index.htmm;

        location / {
	        try_files $uri $uri/ /index.php;
        }

        location ~ \.php$ {
            #fastcgi_pass   127.0.0.1:9000;
            # 这里根据实际配置修改
	        fastcgi_pass  unix:/run/php/php7.2-fpm.sock;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            # 引入fastcgi的配置文件
            include        fastcgi_params;
        }
    }
