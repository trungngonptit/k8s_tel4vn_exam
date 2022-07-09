Câu 2: Truy cập cluster tạo ra ở câu 1 và thực hiện các thao tác sau:
- Tạo một namespace với tên cau2
```
kubectl create namespace cau2
```
```
kubectl get namespaces
```
```
NAME              STATUS   AGE
cau2              Active   10s
default           Active   35d
kube-node-lease   Active   35d
kube-public       Active   35d
kube-system       Active   35d
```

- Tạo một pod vớt tên pod2 với 2 container lần lượt với tên c1 và c2, một volume tên vol gắn với pod và được mount tới mọi container trong đó nhưng không cố định và không chia sẻ với các pod khác.
- Container c1 sử dụng image busybox:1.31.1 và ghi kết quả của lệnh date vào file /vol/date.log mỗi 5 giây trên shared volume
- Container c2 sử dụng image busybox:1.31.1 liên tục xuất nội dung của date.log ra màn hình sử dụng lệnh tail.
- Kiểm tra log của container c2 và ghi kết quả vào ~/cau2/ketqua.txt - Lưu pod manifest (yaml) vào ~/cau2/pod2.yaml
```
kubectl apply -f pod2.yaml -n cau2
```
```
kubectl logs pod2 -c c2 -n cau2
```
```
date: Sat Jul 9 08:29:37 UTC 2022
date: Sat Jul 9 08:29:42 UTC 2022
date: Sat Jul 9 08:29:47 UTC 2022
```
