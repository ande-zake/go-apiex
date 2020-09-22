==============
Note
==============

**************
Golang
**************
1. go run main.go
2. go build -> arahkan pada folder yg dalamnya ada main.go -> maka akan terbentuk file binary -> namanya adalah nama package
3. untuk menjalankan file binary cukup ketik perintah -> ./binary_name
**************
Configurasi Golang with Apache
**************

1. enable port 81 in /etc/httpd/conf/httpd.conf 
	menambahkan baris 43 -> Listen 81
2. enable firewall untuk port 81, agar bisa diakses dari luar
	a. check apakah port 81 ready di -> http_port_t ? jika iya lanjut ke langkah c
	b. jika port 81 blm ready, maka tambahkan port 81 ke "http_port_t". command dibawah :
		semanage port -a -t "http_port_t" -p tcp 81
	c. firewall-cmd --permanent --add-port=81/tcp -> output : success
	d. firewall-cmd --permanent --add-port=81/udp -> output : success
	e. firewall-cmd --reload -> output : success
	f. port 81 ready to access from real world

3. membuat proxy di conf.
- file ada di go-apiex-prod/server-103.82.241.60/etc/httpd/conf.d/golang.conf
- restart -> sudo systemctl restart httpd

2. membuat service agar aktif pada session2 berikutnya. *MASIH GAGAL*  
  a. misal file binary golang ada pada -> ~/golang/go-apiex/fullstack (fullstack nama binary)
  b. membuat service -> misal namanya go-apiex.service
	  sudo nano /etc/systemd/system/go-apiex.service
  c. copas script dibawah
	
  Description= instance to serve go-apiex api
  After=network.target

  [Service]
  User=root
  Group=www-data
  ExecStart=/root/golang/go-apiex/fullstack
  [Install]
  WantedBy=multi-user.target

d. reload daemon
	sudo systemctl daemon-reaload

d. start service 
	sudo systemctl start go-apiex
	sudo systemctl enable go-apiex


[![CircleCI](https://circleci.com/gh/victorsteven/Go-JWT-Postgres-Mysql-Restful-API.svg?style=svg)](https://circleci.com/gh/victorsteven/Go-JWT-Postgres-Mysql-Restful-API)

# Go-JWT-Postgres-Mysql-Restful-API
This is an application built with golang, jwt, gorm, postgresql, mysql.

You can follow the guide here:
https://levelup.gitconnected.com/crud-restful-api-with-go-gorm-jwt-postgres-mysql-and-testing-460a85ab7121

### Dockerizing the API
The dockerized API can be found here:
https://github.com/victorsteven/Dockerized-Golang-Postgres-Mysql-API
