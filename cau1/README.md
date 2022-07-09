### Câu 1: Sử dụng GCP hoặc hạ tầng ảo hoá của bạn để thực hiện các task sau:
#### 1. Tạo 1 kubernetes cluster bao gồm 1 master + 2 workers. Liệt kê các node của cluster và thông tin chi tiết: ROLES, INTERNAL-IP, EXTERNAL-IP, ...
```
vagrant up
```
```
kubectl get nodes -o wide
```
```
NAME            STATUS   ROLES                  AGE   VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
kube-master     Ready    control-plane,master   34d   v1.22.0   192.168.56.10   <none>        Ubuntu 18.04.6 LTS   4.15.0-184-generic   docker://20.10.7
kube-worker-1   Ready    <none>                 34d   v1.22.0   192.168.56.11   <none>        Ubuntu 18.04.6 LTS   4.15.0-184-generic   docker://20.10.7
kube-worker-2   Ready    <none>                 34d   v1.22.0   192.168.56.12   <none>        Ubuntu 18.04.6 LTS   4.15.0-184-generic   docker://20.10.7
```

### 2. Tạo 1 deployment tên là webapp với 2 replica, sử dụng image nginx 1.18.0. Kiểm tra trạng thái của deployment và pod.
```
kubectl apply -f nginx.yaml
```
```
kubectl get deployment -o wide
```
```
kubectl get deployment -o wide
NAME     READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
webapp   2/2     2            2           56s   nginx        nginx:1.18.0   app=nginx
```
### 3. Expose webapp sử dụng một dịch vụ dạng NodePort
```
kubectl apply -f nginx-service.yaml
```
```
kubectl get svc -o wide
```
```
NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE   SELECTOR
grafana-1654940643   ClusterIP   10.100.79.78   <none>        3000/TCP       27d   app.kubernetes.io/component=grafana,app.kubernetes.io/instance=grafana-1654940643,app.kubernetes.io/name=grafana
kubernetes           ClusterIP   10.96.0.1      <none>        443/TCP        35d   <none>
nginx                NodePort    10.101.99.2    <none>        80:30080/TCP   13m   app=nginx
```


```
curl 192.168.56.10:30080
```

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
