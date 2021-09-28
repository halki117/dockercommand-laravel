1. リポジトリをクローンする
```
git clone <リポジトリ名>
```

2. クローンしたリポジトリに移動する
```dockr
cd <リポジトリ>
```

3. phpディレクトリのdocker image作成
```
docker image build -t sample/php ./docker/php
```

4. phpコンテナの起動
```
docker run --name docekr_task_php -v /Users/user/projects/dockercommand-laravel/src:/src -d sample/php
```

5. phpコンテナの中に入ってIPアドレスを調べる
```
docker exec -it docker_task_php bash
hostname -i
exit
```

6. nginxディレクトリのdefault.confの下記の部分を調べたIPアドレスに書き換える
```
fastcgi_pass <調べたIPアドレス>:9000;
```

7. nginxディレクトリのdocker imageを作成
```
docker image build -t sample/nginx ./docker/nginx
```

8. nginxコンテナの起動  
```
docker run --name docker_task_nginx -v /Users/user/dockercommand-laravel/src:/src -p 80:80 -d sample/nginx
```

9. dockerボリュームの作成
```
docker volume create db_storage
```

10. mysqlコンテナの起動  
```
docker run -d --name docker_task_mysql -e MYSQL_DATABASE=docktask_mysql -e MYSQL_ROOT_PASSWORD=root -v db_storage:/var/lib/mysql -p 3306:3306 mysql:5.7 
```

. mysqlコンテナの中に入りIPアドレスを調べる
```
docker exec -it docker_task_mysql bash
```

11. mysqlコンテナのIPアドレスを調べる
```
docker exec -it <mysqlコンテナ> bash
hostname -i 
exit
```

12. PHPコンテナに入ってLaravelの.envを編集する
```
docker exec -it <PHPコンテナ> bash
vi .env
DB_CONNECTION=mysql  
DB_HOST=<mysqlコンテナのIPアドレス>  
DB_PORT=3306  
DB_DATABASE=db_name  
DB_USERNAME=root  
DB_PASSWORD=root
```  
