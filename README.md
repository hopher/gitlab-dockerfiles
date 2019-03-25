# debian-dockerfiles



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