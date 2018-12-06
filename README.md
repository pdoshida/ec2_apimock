# ec2(amazonlinux)でapiモックを作る


## nvmをインストールする
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash

## Node.jsのLTSバージョンをインストールする（ここはお好みで）
$ nvm install stable

## インストールしたNode.jsの設定 + デフォルトver.として指定する
```
$ nvm use stable
$ nvm alias default stable
```

## インストールされたNode.jsのver.を確認する
$ node -v

## json-serverのインストール
$ npm install -g json-server

## db.json作成
$ vim db.json
```
{
  "users": [],
  "keywords": [
    {
      "id": 1,
      "text": "hoge"
    },
    {
      "id": 2,
      "text": "fuga"
    },
    {
      "id": 3,
      "text": "piyo"
    }
  ],
  "articles": []
}
```

## json-server起動(お試し)
$ json-server db.json

## nginxのインストール
$ yum install -y nginx

## nginxの設定を一部修正
$ vim /etc/nginx/nginx.conf
```
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  52.193.75.127;                #修正箇所
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            proxy_pass http://localhost:3000;　　　　　　　　　　　　　#追加箇所
        }
```

## nginxあげとく
```
$ service nginx start
$ chkconfig nginx on
```
