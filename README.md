# gitlab-dockerfiles

用 Docker 容器服务的方式搭建 `gitlab` 环境, 易于维护、升级。

本环境基于 `gitlab/gitlab-ce:latest`, Linux版本: `Ubuntu 16.04.6 LTS`

> **NOTE**:  
> `cat /etc/issue`


## 工具安装

### Get Docker CE for Debian

https://docs.docker.com/install/linux/docker-ce/debian/#prerequisites

### 安装 docker-compose

https://docs.docker.com/compose/install/


## 使用

进入 docker-compose.yml 所在目录

执行命令：
```
docker-compose up
```  

> **NOTE**
> 过程比较久, 请耐心等待, 可用 `docker logs -f --tail=10 my_gitlab` 查看日志进度

## 数据存储说明

**Where is the data stored?**

The GitLab container uses host mounted volumes to store persistent data:

| Local location       | Container location | Usage                                      |
| -------------------- | ------------------ | ------------------------------------------ |
| `/srv/gitlab/data`   | `/var/opt/gitlab`  | For storing application data               |
| `/srv/gitlab/logs`   | `/var/log/gitlab`  | For storing logs                           |
| `/srv/gitlab/config` | `/etc/gitlab`      | For storing the GitLab configuration files |

You can fine tune these directories to meet your requirements.


## 安装后，需要更新域名

> **参考文档**:
> https://docs.gitlab.com/omnibus/settings/configuration.html#configuring-the-external-url-for-gitlab

编辑 `/etc/gitlab/gitlab.rb`

```
docker exec -it my_gitlab vi /etc/gitlab/gitlab.rb
```

修改 `external_url` 对应的值，然后，重启容器

```
docker restart my_gitlab
```


## ssh方式, gitlab使用的不是标准22端口解决方法

> 参考：https://blog.csdn.net/wanwan5856/article/details/52797969

设置步骤：

1，本地进入.ssh查看是否存在密钥对：`xxx`和 `xxx.pub`

命令：`cd ~/.ssh`

2，如果不存在，使用ssh-keygen来创建

命令：ssh-keygen -t rsa -C "youremail@youremail.com"

> 注解：  
> Enter file in which to save the key 输入保存秘钥的文件 直接enter即可  
> Enter passphrase (empty for no passphrase) 输入密码 直接enter即可  
> 此时查看.ssh目录下可看到新增的一对秘钥id_rsa和id_rsa.pub

3，查看公钥

命令： `cat ~/.ssh/id_rsa.pub `

复制全部，包括后面的邮箱

4，添加到gitlab中

左侧栏Profile Settings → 左侧栏SSH Keys → 粘贴并Add key

5，创建config，端口为22可忽略这一步

命令：`cat>~/.ssh/config`

输入：

```
Host git.xxx.com
User git
Port 8003
IdentityFile /Users/hopher/.ssh/id_rsa
```
> IdentityFile（替换成你的id_rsa所在的路径）

6，验证是否设置成功

命令：`ssh -T git@git.xxx.com`

显示Welcome to GitLab, yourname! 代表成功

## 参考资料

- [GitLab Installation](https://www.gitlab.com.cn/installation/#debian)
- [GitLab Docker 相关参数](https://docs.gitlab.com/omnibus/docker/)
- [[镜像站] 阿里云开源镜像站](https://opsx.alibaba.com/mirror)
- [[镜像站] 腾讯开源镜像站](https://mirrors.cloud.tencent.com/index.html)
- [[ubuntu] 腾讯开源镜像站](https://mirrors.cloud.tencent.com/help/ubuntu.html)
- [Get Docker CE for Debian](https://docs.docker.com/install/linux/docker-ce/debian/#prerequisites)
