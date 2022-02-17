# chirpstack-helm-chart
开源lorawan server 项目chirpstack的helm chart [english](../README.md)

# 如何贡献
如果你想对这个项目进行贡献可以点击`fork`按钮`fork`这个项目并且发起`PR`

## Fork  
贡献的准备工作:`Fork`这个项目.

## 贡献流程  

```bash
$ git remote add chirpstack-helm-chart git@github.com:liangyuanpeng/chirpstack-helm-chart.git
# sync with the remote master
$ git checkout master
$ git fetch chirpstack-helm-chart
$ git rebase chirpstack-helm-chart/master
$ git push origin master
# create a PR branch
$ git checkout -b your_branch   
# do something
$ git add [your change files]
$ git commit -sm "xxx"
$ git push origin your_branch  
```  
# 安装helm chart

```bash
$ git clone https://github.com/liangyuanpeng/chirpstack-helm-chart.git  
$ cd chirpstack-helm-chart/  
# install helm chart from this repo
$ helm install chirpstack .   
```  

`注意：默认使用名叫longorn的storageClass存储.`

```bash
$ kubectl get po 
# 执行命令后可以看到以下pod
NAME                              READY   STATUS    RESTARTS   AGE
chirpstack-as-84b68cb7fd-zgs5j    1/1     Running   0          45s
chirpstack-ns-7d9b9867f-zftn6     1/1     Running   0          45s
mosquitto-0                       1/1     Running   0          45s
pgsql-0                           1/1     Running   0          45s
redis-0                           1/1     Running   0          45s
redis-exporter-64f8bf4f46-2rcgl   1/1     Running   0          45s
```  

```bash
$ kubectl get svc
# 执行命令后可以看到以下svc
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
chirpstack-as    ClusterIP   10.98.227.61     <none>        8080/TCP,8001/TCP,8003/TCP   77s
chirpstack-ns    ClusterIP   10.108.182.238   <none>        8000/TCP                     77s
mosquitto        ClusterIP   10.104.149.103   <none>        1883/TCP                     77s
pgsql            ClusterIP   10.102.33.231    <none>        5432/TCP                     77s
redis            ClusterIP   10.109.138.95    <none>        6379/TCP                     77s
redis-exporter   ClusterIP   10.106.66.131    <none>        9121/TCP                     77s
```  

```bash
$ kubectl get pvc
# 执行命令后可以看到以下pvc
NAME                               STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
pgsql-pvc-pgsql-0                  Bound    pvc-c1c6adf4-32ef-4431-bd6a-3825a6ef408c   96Mi       RWO            longhorn       3d
redis-pvc-redis-0                  Bound    pvc-e464d0e8-e04a-4958-858e-5efef1aeba9c   48Mi       RWO            longhorn       3d
```  

```bash
$ helm list
# 执行命令后可以看到以下chart
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                           APP VERSION
chirpstack      default         1               2021-01-29 16:11:48.984574857 +0800 CST deployed        chirpstack-helm-chart-0.1.0     1.16.0
```   
# 暴露application-server的svc，访问application-server
```bash
kubectl port-forward svc/chirpstack-as 8080:8080 --address 0.0.0.0
```

# 在application-server上设置network-server

你可以设置为 `chirpstack-ns.{namespace}:8000` 或者 `chirpstack-ns.{namespace}.svc.cluster.local:8000`

#  如果你用了gateway-bridge这个组件的话，可以用下面的命令把svc暴露出来

```
kubectl expose deploy gateway-bridge --port 1700 --target-port=1700 --protocol=UDP --name udpservice --type=NodePort  
```