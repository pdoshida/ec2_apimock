# ec2(amazonlinux)でapiモックを作る
```
# nvmをインストールする
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
```
```
# Node.jsのインストール
nvm install stable
nvm use stable
nvm alias default stable
node -v
```
```
# json-serverのインストール
npm install -g json-server
```
```
# json-server起動(お試し)
json-server db.json
```
```
# nginxのインストール
yum install -y nginx
```
```
# nginxの設定を一部修正
vim /etc/nginx/nginx.conf
```
```
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  xxx.xxx.xxx.xxx;                #修正箇所（globalip）
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            proxy_pass http://localhost:3000;　　　　　　　　　　　　　#追加箇所
        }
```
```
# nginxあげとく
service nginx start
chkconfig nginx on
```
```
# api叩いてみる
http://${globalip}/keywords
```

参考(api叩き方とか)
https://github.com/typicode/json-server
