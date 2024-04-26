# K8S_SETUP

{
 `sudo su -
 export VERSION=1.25
 export OS=CentOS_8
 curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo        https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/devel:kubic:libcontainers:stable.repo
 curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$VERSION/$OS/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo
 yum install crio
 systemctl status crio
 systemctl start crio `
}

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
