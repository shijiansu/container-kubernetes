## Docs

- https://minikube.sigs.k8s.io/docs/

MiniKube是本地Kubernetes单节点环境

## 命令行

```bash
# installation
# docker: https://www.docker.com/get-started
# kubectl
# 在MacOS中使用 "Docker Desktop", 已经存在kubectl
/usr/local/bin/kubectl -> /Applications/Docker.app/Contents/Resources/bin/kubectl
# 与Docker Desktop的冲突, 无需再安装 # brew install kubectl # 使用单独的kubectl, 而非minikube自带的
which kubectl # /usr/local/bin/kubectl
kubectl version -o json # 这里会显示The connection to the server localhost:8080 was refused, 由于没有启动 "kubernetes master"
kubectl version --client -o json # 这样就没error显示

# minikube - https://minikube.sigs.k8s.io/docs/start/
# env: darwin/amd64
brew install minikube
minikube version -o json | jq

# https://minikube.sigs.k8s.io/docs/drivers/docker/
minikube config set driver docker # make docker the default driver
minikube config view # list all configuration

# 启动前, 查看本地可分配的资源
# CPU
sysctl -a | grep machdep.cpu | grep core_count
# Memory: MacOS check "Activity Monitor"

minikube start # start a cluster
# Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
minikube start --kubernetes-version=v1.11.10 # selective version
minikube start --kubernetes-version=latest # upgrade your cluster

minikube start --cpus 6 --memory 8000
minikube start --cpus=max --memory=max

minikube start --extra-config kubeadm.ignore-preflight-errors=SystemVerification # force to skip errors from system limitation

# will not work if minikube is using the bare-metal/none driver
minikube start -p cluster2 # start a second local cluster

minikube profile list # list of your current clusters

minikube dashboard # enable the dashboard
minikube dashboard --url

minikube addons list # list all addon: https://minikube.sigs.k8s.io/docs/handbook/deploying/
minikube addons enable <name>
minikube addons disable <name>

kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4 # starting a server
kubectl expose deployment hello-minikube --type=NodePort --port=8080 # exposing a service as a NodePort
minikube service hello-minikube # shortcut for exposing a service as a NodePort

minikube stop # stop your local cluster
minikube delete # delete your local cluster
minikube delete --all # delete all local clusters and profiles

minikube start --help
minikube config --help
```

