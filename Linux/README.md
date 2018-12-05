## Linux

### centos 管理
* 安装最新版的 nodejs
  * 卸载老版本的 nodejs 及 npm:
    * `yum uninstall nodejs`
  * 安装新版本的 nodejs:
    * `curl -sL https://rpm.nodesource.com/setup_10.x | bash -`
    * `yum install -y nodejs`
    * 如果安装失败，可以将 /etc/yum.repo.d/* 里面的文件备份到其他地方，只保留 nodesource 的源，再重试
* 安装 mysql
  * 先安装源
    * 在这个页面(https://dev.mysql.com/downloads/repo/yum/)找到最新的 rpm 包，下载后使用 yum install 命令安装。
    * 如:  `https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm`
  * 安装 mysql
    * `yum install mysql-community-server`
  * 启动
    * `service mysqld start`
  * 安装后默认有 root 用户，使用如下命令查找密码
    * `grep 'temporary password' /var/log/mysqld.log`
  * 登录
    * `mysql -uroot -p`
  * 如果密码错误，可考虑免密登录后修改密码
    * `service mysqld stop`
    * edit `/etc/my.conf`; add [mysqld] `skip-grant-tables`
  * 修改密码
    * `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '密码要复杂'`
  * 授权远程访问
    * `GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '密码' WITH GRANT OPTION;`
    * `flush privileges;`

* 修改时区
  * 进入 `/etc` 目录，`ls -l` 可以看到当前的 `localtime` 文件：
    * `localtime -> ../usr/share/zoneinfo/America/New_York`
  * 修改为正确的时区
    * `ln -sf ../usr/share/zoneinfo/Asia/Shanghai localtime`
  * 查看本机时间
    * `date -R`
### book
* [The Linux Command Line](http://billie66.github.io/TLCL/book/index.html)