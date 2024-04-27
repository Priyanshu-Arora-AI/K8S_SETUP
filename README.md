# K8S_SETUP
   IN AWS AMi

##### allocate public ip to instance
### set custom hostname
```
{
hostname should be in fqdn format
hostnamectl set-hostname
vi /etc/hosts
	public_ip hostname
}
```

## MASTER NODE

1. INSTALL IPTABLES
2. INSTALL IPROUTE
3. THEN INSTALL CRIO
 ## CRIO SETUP COMMAND
![alt text](https://github.com/Priyanshu-Arora-AI/K8S_SETUP/blob/main/source/crio.png) 			
```
{
 sudo su -
 export VERSION=1.25
 export OS=CentOS_8
 curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo        https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/devel:kubic:libcontainers:stable.repo
 curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$VERSION/$OS/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo
 yum install crio
 systemctl status crio
 systemctl start crio 
}
```
4. setup repo for k8s
   ```
   {
   cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
   [kubernetes]
   name=Kubernetes
   baseurl=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/
   enabled=1
   gpgcheck=1
   gpgkey=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/repodata/repomd.xml.key
   exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
   EOF
}

# run setup command
![alt text](https://github.com/Priyanshu-Arora-AI/K8S_SETUP/blob/main/source/k8s.png) 
```
{

   sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
   kubeadm config images pull
   systemctl enable kubelet.service --now
   sudo firewall-cmd --zone=public --add-port=6443/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=10250/tcp --permanent
   sudo firewall-cmd --reload
   sudo vim /etc/default/kubelet
	         KUBELET_EXTRA_ARGS=--feature-gates="NodeSwap=true"
   sudo systemctl restart kubelet
   sudo sysctl net.ipv4.ip_forward=1
   sudo vim /etc/sysctl.conf
	      net.ipv4.ip_forward = 1
   sudo sysctl -p
   kubeadm init  --pod-network-cidr 10.1.0.0/16

   
   
   
   }
   ```
   
