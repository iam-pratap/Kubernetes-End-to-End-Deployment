# prerequisites

kubectl – A command line tool for working with Kubernetes clusters.

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```


eksctl – A command line tool for working with EKS clusters that automates many individual tasks. 

```
# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

# (Optional) Verify checksum
curl -sL "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin
```
Save the above script as `eksctl.sh` then run `chmod +x eksctl.sh` and `sudo sh eksctl.sh`

AWS CLI – A command line tool for working with AWS services, including Amazon EKS. 

```
apt install awscli -y
apt install python3-pip
pip install awscli --upgrade
```
```
aws configure
```
Enter the `Access-key` and `Secret-Access-key`
