## DNMP (Docker、Nginx、MySQL、PHP) 範例




### 調整 Project 設定 (project name, uid, gid)
### System user 或 group，uid & gid 範圍請參考 SYS_UID_MIN & SYS_GID_MIN (/etc/login.defs)
### 注意: PROJECT_GROUP 是獨立的，PROJECT_GID 不要和 PROJECT_UID 相同，名稱也一樣
.env


### Project user 預設是 root，若需要新增 project user 可執行下面指令 (要先調整 .env)
[root]# ./usr/local/create_system_project_user.sh


### Nginx 設定
將 etc/nginx119/conf.d/samples/994-demo.conf 複製到 etc/nginx119/conf.d/vhosts 底下
並修改 server_name 為 127.0.0.1 或你自己的 domain (localhost 是 nginx 預設值，請不要使用，或自行調整預設值 etc/nginx119/conf.d/default.conf)


### MySQL 設定
先到 https://www.phpmyadmin.net/ 下載最新版本 phpMyAdmin
解壓縮到 volumes/htdocs 底下
將資料夾名稱改為 phpMyAdmin，複製 config.sample.inc.php 存成 config.inc.php，並將 $cfg['Servers'][$i]['host'] 設定改為 mysql80 (docker-compose.yml 裡 services 定義的名稱)
複製 nginx 裡 995-phpMyAdmin.conf 設定 (請參考 Nginx 設定)
預設的登入帳密是 root / root (可以到 ./env/mysql80 更改預設密碼)


### 啟動 DNMP
[user]$ docker-compose up -d


### 畫面檢視
http://127.0.0.1:9080	// Web
https://127.0.0.1:9443	// phpMyAdmin


### 關閉 DNMP
[user]$ docker-compose down -v
