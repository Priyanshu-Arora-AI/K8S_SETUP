# K8S_SETUP
   IN RHEL 9

#### MAKE YOUR VM IP STATIC AND ENABLE BRIDGE AND NAT ADAPTER
1. Open the network configuration file for the NAT interface. This could be located at /etc/sysconfig/network-scripts/ifcfg-enp0s8 (replace enp0s8 with the actual interface name).
  ```
    {
  sudo vim /etc/sysconfig/network-scripts/ifcfg-enp0s3     [ENP IS NAT ADAPTER NAME]
     TYPE="Ethernet"
     BOOTPROTO="static"
     NAME="enp0s3"
     DEVICE="enp0s3"
     ONBOOT="yes"
     IPADDR="desired_static_ip"
     NETMASK="subnet_mask"
     GATEWAY="gateway_address"
     DNS1="dns_server_address"
 sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s8   [it is bridge adapter name}
     TYPE="Ethernet"
     BOOTPROTO="static"
     NAME="enp0s8"
     DEVICE="enp0s8"
     ONBOOT="yes"
     IPADDR="desired_static_ip"
     NETMASK="subnet_mask"


}
```
## MASTER NODE

1. INSTALL IPTABLES
2. INSTALL IPROUTE
3. THEN INSTALL CRIO
 ## CRIO SETUP COMMAND
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
```
{

   sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
   kubeadm config images pull
   
   
   
   }
   ```
   
