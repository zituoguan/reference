---
title: Alpine Linux
date: 2024-03-20 12:00:00
icon: icon-alpine
background: bg-blue-600
tags:
    - linux
    - server
    - container
categories:
    - 操作系统
intro: Alpine Linux 综合速查表，涵盖包管理、系统管理、网络等。Alpine Linux 是一个基于 musl libc 和 busybox 的、面向安全的轻量级 Linux 发行版。
---

# Alpine Linux 速查表

## 包管理 (apk)

### 基本包操作
```bash
# 更新包索引
apk update

# 升级所有已安装的包
apk upgrade

# 安装一个包
apk add <package-name>

# 移除一个包
apk del <package-name>

# 搜索一个包
apk search <package-name>

# 显示包信息
apk info <package-name>

# 列出所有已安装的包
apk list --installed
```

### 高级包操作
```bash
# 从测试仓库添加包
apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing <package-name>

# 添加多个包
apk add package1 package2 package3

# 清理包缓存
apk cache clean
```

## 系统管理

### 服务管理 (OpenRC)
```bash
# 启动一个服务
rc-service <service-name> start

# 停止一个服务
rc-service <service-name> stop

# 重启一个服务
rc-service <service-name> restart

# 将服务添加到默认运行级别
rc-update add <service-name> default

# 从默认运行级别移除服务
rc-update del <service-name> default

# 列出所有服务
rc-status
```

### 系统信息
```bash
# 显示系统信息
uname -a

# 显示磁盘使用情况
df -h

# 显示内存使用情况
free -h

# 显示运行中的进程
ps aux

# 显示系统运行时间
uptime
```

### 网络配置
```bash
# 显示网络接口
ip addr show

# 配置网络接口
setup-interfaces

# 测试网络连接
ping -c 4 google.com

# 显示路由表
ip route show

# 编辑网络配置
vi /etc/network/interfaces
```

### 用户管理
```bash
# 添加一个新用户
adduser <username>

# 将用户添加到组
addgroup <username> <groupname>

# 更改密码
passwd <username>

# 删除用户
deluser <username>

# 列出所有用户
cat /etc/passwd
```

## 文件系统操作

### 基本文件操作
```bash
# 创建目录
mkdir <directory-name>

# 移除目录
rm -r <directory-name>

# 复制文件
cp <source> <destination>

# 移动/重命名文件
mv <source> <destination>

# 更改权限
chmod <permissions> <file>

# 更改所有权
chown <user>:<group> <file>
```

## 容器操作

### Docker 支持
```bash
# 安装 Docker
apk add docker

# 启动 Docker 服务
rc-service docker start

# 开机启动 Docker
rc-update add docker default
```

## 系统维护

### 磁盘操作
```bash
# 检查磁盘空间
df -h

# 检查目录大小
du -sh <directory>

# 挂载设备
mount /dev/<device> /mnt/<mountpoint>

# 卸载设备
umount /mnt/<mountpoint>
```

### 备份与恢复
```bash
# 创建 tar 归档文件
tar -czf backup.tar.gz /path/to/backup

# 解压 tar 归档文件
tar -xzf backup.tar.gz

# 创建系统备份 (需要 root 权限)
lbu package /media/backup.apkovl.tar.gz
```

## 提示与技巧

### 常用配置文件
- `/etc/apk/repositories` - 包仓库
- `/etc/network/interfaces` - 网络配置
- `/etc/hostname` - 系统主机名
- `/etc/hosts` - 主机映射
- `/etc/resolv.conf` - DNS 配置

### 环境变量
```bash
# 设置环境变量
export VARIABLE=value

# 查看所有环境变量
env

# 添加永久环境变量
echo "export VARIABLE=value" >> ~/.profile
```

### 系统日志
```bash
# 查看系统日志
less /var/log/messages

# 查看启动信息
dmesg

# 实时跟踪日志
tail -f /var/log/messages
```

## 安全

### 防火墙 (使用 iptables)
```bash
# 安装 iptables
apk add iptables

# 允许 SSH (端口 22)
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# 保存 iptables 规则
/etc/init.d/iptables save

# 恢复 iptables 规则
/etc/init.d/iptables restart
```

### SSH 配置
```bash
# 生成 SSH 密钥
ssh-keygen -t rsa -b 4096

# 将 SSH 密钥复制到远程服务器
ssh-copy-id user@remote-server

# 编辑 SSH 配置
vi /etc/ssh/sshd_config
```

## 故障排除

### 常用命令
```bash
# 检查系统日志中的错误
dmesg | grep -i error

# 检查服务状态
rc-service <service-name> status

# 检查系统资源使用情况
top

# 检查网络连接
netstat -tuln

# 检查磁盘健康状况 (需要 smartmontools 包)
smartctl -a /dev/sda
```