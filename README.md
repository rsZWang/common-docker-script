# common-docker-script

<H1>Apache + PHP</H1>
$ docker run --name apache-php -d -p 20080:80 -p20443:443 --restart always \
-v $HOME/Desktop/docker/apache-php/www:/var/www/app/ romeoz/docker-apache-php

<H1>Reverse Proxy</H1>
$ sudo docker run -p 80:80 -p 443:443 -p 22:22 -p 8080:8080 -p 28888:8888 \
-it --restart always -d \
-v /var/run/docker.sock:/tmp/docker.sock:ro \
-v $HOME/Desktop/docker/neilpang/proxy/certs:/etc/nginx/certs \
-v $HOME/Desktop/docker/neilpang/proxy/acme:/acmecerts \
-v $HOME/Desktop/docker/neilpang/proxy/conf.d:/etc/nginx/conf.d \
-v $HOME/Desktop/docker/neilpang/vhost.d:/etc/nginx/vhost.d \
-v $HOME/Desktop/docker/neilpang/stream.d:/etc/nginx/stream.d \
-v $HOME/Desktop/docker/neilpang/dhparam:/etc/nginx/dhparam \
--name reverse-proxy  neilpang/nginx-proxy

<H1>GitLab</H1>
$ sudo docker run --detach \
--hostname yhw.gitlab.com \
-e VIRTUAL_HOST=yhw.gitlab.com \
--publish 10080:80 --publish 10443:443 --publish 10022:22 \
--name gitlab --restart always \
--volume $HOME/Desktop/gitlab/config:/etc/gitlab \
--volume $HOME/Desktop/gitlab/logs:/var/log/gitlab \
--volume $HOME/Desktop/gitlab/data:/var/opt/gitlab \
gitlab/gitlab-ce:latest


$ sudo docker run --detach --hostname serverIP \
--publish ???:443 --publish ???:80 --publish ???:22 \
--name gitlab --restart always \
--volume $HOME/Desktop/gitlab/config:/etc/gitlab \
--volume $HOME/Desktop/gitlab/logs:/var/log/gitlab \
--volume $HOME/Desktop/gitlab/data:/var/opt/gitlab \
gitlab/gitlab-ce:latest

docker run: 生成 container 及執行 </br>
--detach, -d: 在背景執行 </br>
--hostname: 設定 host </br>
--publish, -p: 將外部的port和內部的連結 </br>
	ex: [10443:443] 主機端的10443 port 即對應 Container 的 443 port </br>
	      443 - https,  80 - http,  22 - SSH </br>
--name: 設定 Container 的 name </br>
--restart always: 每次主機重新開機即執行Container </br>
--volume A:B: Link主機及Container的Volume (備份用) </br>
	ex: [/$HOME/Desktop/gitlab/logs:/var/log/gitlab] A和B的資料將會同步, A是在主機的 </br>
      資料夾, B則是在Container裡的資料夾 </br>
gitlab/gitlab-ce:latest: 要用的 image (如果本機沒有會自動pull) </br>
