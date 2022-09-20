---
title: Ubuntu 饥荒服务器搭建教程
date: 2022-09-16 10:02:21
tags: coding
category: 教程
---

# Ubuntu 饥荒服务器搭建教程

服务器： ubuntu-18.04-amd64-20220507111916



## 安装依赖

```shell
sudo apt-get install libstdc++6:i386 libgcc1:i386 libcurl4-gnutls-dev:i386
```



## 安装 steamCMD

```shell
mkdir -p ~/steamcmd/
cd ~/steamcmd/
wget "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz"
tar -xvzf steamcmd_linux.tar.gz
```



## 注册账号

[依照官网教程注册 Klei 账号，注册服务器](https://forums.kleientertainment.com/forums/topic/64441-dedicated-server-quick-setup-guide-linux)

下载 MyDediServer/ 文件夹

MyDediServer/ 放入 ~/.klei/DoNotStarveTogether/ 路径



## 设置入口脚本

```shell
vim ~/run_dedicated_servers.sh
```

```shell
#!/bin/bash

steamcmd_dir="$HOME/steamcmd"
install_dir="$HOME/dontstarvetogether_dedicated_server"
cluster_name="MyDediServer"
dontstarve_dir="$HOME/.klei/DoNotStarveTogether"

function fail()
{
	echo Error: "$@" >&2
	exit 1
}

function check_for_file()
{
	if [ ! -e "$1" ]; then
		fail "Missing file: $1"
	fi
}

cd "$steamcmd_dir" || fail "Missing $steamcmd_dir directory!"

check_for_file "steamcmd.sh"
check_for_file "$dontstarve_dir/$cluster_name/cluster.ini"
check_for_file "$dontstarve_dir/$cluster_name/cluster_token.txt"
check_for_file "$dontstarve_dir/$cluster_name/Master/server.ini"
check_for_file "$dontstarve_dir/$cluster_name/Caves/server.ini"

./steamcmd.sh +force_install_dir "$install_dir" +login anonymous +app_update 343050 validate +quit

check_for_file "$install_dir/bin64"

cd "$install_dir/bin64" || fail

run_shared=(./dontstarve_dedicated_server_nullrenderer_x64)
run_shared+=(-console)
run_shared+=(-cluster "$cluster_name")
run_shared+=(-monitor_parent_process $$)

"${run_shared[@]}" -shard Caves  | sed 's/^/Caves:  /' &
"${run_shared[@]}" -shard Master | sed 's/^/Master: /'
```

### 脚本权限

```shell
chmod u+x ~/run_dedicated_servers.sh
```



## 运行入口脚本

```shell
cd ~
~/run_dedicated_servers.sh

```

## 可能的问题

### 库缺失

```shell
./dontstarve_dedicated_server_nullrenderer: error while loading shared libraries: libcurl-gnutls.so.4: cannot open shared object file: No such file or directory

```

#### 解决

```shell
apt-get install libcurl4-gnutls-dev
dpkg --add-architecture i386
```

