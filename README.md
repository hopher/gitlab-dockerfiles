# debian-dockerfiles

用 Docker 容器服务的方式搭建 `gitlab` 环境, 易于维护、升级。

本环境基于 `gitlab/gitlab-ce:latest`, Linux版本: `Ubuntu 16.04.6 LTS`

> **NOTE**:  
> `cat /etc/issue`

## Where is the data stored?

The GitLab container uses host mounted volumes to store persistent data:

| Local location       | Container location | Usage                                      |
| -------------------- | ------------------ | ------------------------------------------ |
| `/srv/gitlab/data`   | `/var/opt/gitlab`  | For storing application data               |
| `/srv/gitlab/logs`   | `/var/log/gitlab`  | For storing logs                           |
| `/srv/gitlab/config` | `/etc/gitlab`      | For storing the GitLab configuration files |

You can fine tune these directories to meet your requirements.


## 参考资料

- [GitLab Installation](https://www.gitlab.com.cn/installation/#debian)
- [GitLab Docker 相关参数](https://docs.gitlab.com/omnibus/docker/)
- [[镜像站] 阿里云开源镜像站](https://opsx.alibaba.com/mirror)
- [[镜像站] 腾讯开源镜像站](https://mirrors.cloud.tencent.com/index.html)