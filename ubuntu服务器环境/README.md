# ubuntu20 服务器环境搭建

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [ubuntu20 服务器环境搭建](#ubuntu20-服务器环境搭建)
  - [基础软件安装](#基础软件安装)
    - [开机启动设置](#开机启动设置)

<!-- /code_chunk_output -->

## 基础软件安装

```shell
# git
# gcc
# clang
# automake
# cmake
# curl
# wget
# npm
# cnpm
# zsh
# rust
# fzf
# bat
# sqlite3
# python3，pip，ipython
# nginx
# mongodb
sudo apt-get install mongodb
# redis
# mysql
# tree
```

### 开机启动设置

1. `/lib/systemd/system/`目录下有很多启动脚本，我们修改`rc-local.service`：

   ```shell
   ➜ ls ./rc-local.service
   ───┬──────────────────┬──────┬───────┬─────────────
   # │       name       │ type │ size  │  modified   
   ───┼──────────────────┼──────┼───────┼─────────────
   0 │ rc-local.service │ File │ 776 B │ 9 hours ago 
   ───┴──────────────────┴──────┴───────┴─────────────
   ```

2. 打开该文件，添加`[Install]`字段，用户描述如何启动，添加：

   ```shell
   [Install]
   WantedBy=multi-user.target  
   Alias=rc-local.service
   ```

3. 增加`/etc/rc.local`文件，添加：

   ```shell
   #!/bin/sh
   echo "my startup"
   exit 0
   ```

4. 增加执行权限：

   ```shell
   sudo chmod +x /etc/rc.local
   ```

5. 增加软连接：

   ```shell
   ln -s /lib/systemd/system/rc.local.service /etc/systemd/system/ 
   ```

重启下就好了。

db.createUser({user: "JerryYu", pwd: "bluse.io", roles:[{role: "userAdminAnyDatabase" , db:"admin"}]})