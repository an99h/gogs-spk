# 猫盘群晖上gogs的编译
## MAC OS 安装 go
```
$ brew install go
```

## 编译猫盘群晖 gogs
```
$ git clone --depth 1 https://github.com/gogs/gogs.git
$ alias go_build_linux="GOOS=linux GOARCH=arm GOARM=7 go build"
$ go_build_linux
```
运行完即可在 gogs 目录下得到 gogs 二进制文件

## 打包群晖上的spk套件 
克隆本工程，将之前生成的 gogs 二进制文件和public/scripts/templates 三个文件夹一起拷贝到`1_create_package/gogs`
再执行 `./create_spk.sh`即可得到 gogs.spk

## 猫盘群晖上安装 gogs.spk
1. 安装git server 、MariaDB5(设置密码)
2. 手动安装 gogs.spk
3. 执行 gogs mysql.sql
	 
	 ```
	 $ cd /usr/local/gogs/gogs/scripts  
	 $ mysql -uroot -p密码  
	 MariaDB> source mysql.sql  
	 ```
4. 在套件中心打开 gogs 开始配置，数据库选择 mysql

---
---
---
---


# gogs-spk

[Gogs](https://gogs.io) (Go Git Service) SPK package ([Synology PacKages](https://www.synology.com/en-us/dsm/app_packages))

Install Gogs into a Synology NAS.

## Requirements

<sub>this package, to see Gogs requirements check https://gogs.io</sub>

* armv7 (Tested only with DS213j, Marvell Armada 370)
* intel Atom D2700 (RS2414rp+)
* intel Atom CE5335 (DS214 play)
* MariaDB, SQLite
* Git Server

## Usage

Change **Package Center -> Trust Level** to **Any Publisher** and import manually the package from **Manual install**.
Finally, install with Gogs web installation.

## To use with another arch

Download the binary from https://gogs.io/docs/installation/install_from_binary, replace the content from **1_create_package/gogs** directory and exec create_spk.sh:

```alex@vostok:/Volumes/HD/Development/synology/gogs-spk(master)$ rm -rf 1_create_package/gogs/ && tar zxvf gogs_v0.9.13_linux_386.tar.gz -C 1_create_package/```

```$ sh create_spk.sh```


## Compiled from source

Suggested by [hirakujira](https://github.com/hirakujira)

```
GOOS=linux GOARCH=arm GOARM=7 go get -u github.com/gogits/gogs
```


## Screenshots

![Install](screenshots/install2.png)

![Install](screenshots/install.png)

![Stopping](screenshots/stopping.png)

![Desktop icon](screenshots/icon.png)


Gogs screenshots
https://github.com/gogits/gogs


## ToDo

- Don't force to use Git Server and MariaDB (PostgreSQL? Gogs ARM version haven't Sqlite/TiDB)
- Support to archs (and DBs)
- Don't use **root** user and create and use **gogs** user, if possible


