Câu 4: Truy cập cluster tạo ra ở câu 1 và thực hiện các thao tác sau:
- Tạo một pod đặt tên là web, sử dụng image nginx:latest thoả mãn điều kiện chỉ chạy
master node, không được schedule lên worker node.
- Kiểm tra trạng thái để chắc chắn pod được khởi tạo và vận hành bình thường trên master
node
- Copy các câu lệnh được sử dụng vào file ~/cau4/ketqua.txt - Copy pod manifest vào file ~/cau4/pod.yaml

```
kubectl apply -f pod4.yaml
```

```
kubectl get pod web -o wide
```
```
NAME   READY   STATUS    RESTARTS   AGE   IP          NODE          NOMINATED NODE   READINESS GATES
web    1/1     Running   0          41s   10.42.0.2   kube-master   <none>           <none>
```
```
kubectl logs web
```
```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2022/07/09 08:49:49 [notice] 1#1: using the "epoll" event method
2022/07/09 08:49:49 [notice] 1#1: nginx/1.23.0
2022/07/09 08:49:49 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
2022/07/09 08:49:49 [notice] 1#1: OS: Linux 4.15.0-184-generic
2022/07/09 08:49:49 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2022/07/09 08:49:49 [notice] 1#1: start worker processes
2022/07/09 08:49:49 [notice] 1#1: start worker process 30
2022/07/09 08:49:49 [notice] 1#1: start worker process 31
```