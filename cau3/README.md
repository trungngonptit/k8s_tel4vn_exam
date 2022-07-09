Câu 3: Truy cập cluster tạo ra ở câu 1 và thực hiện các thao tác sau:
1. Tạo một deployment tên là webapp2, với 1 label là “app:web2" với 2 replica, sử dụng image là nginx:latest và expose ra port 80 trên một ClusterIP service.
2. Tạo 1 Network Policy tên là default-deny-ingress để chặn tất cả các traffic đi vào pod trong namespace default. Triển khai NP này.
3. Tạo một Network Policy với tên là access-web cho phép chỉ những pod với label
“access:accepted" có thể truy cập deployment này. Triển khai Network Policy này.
4. Tạo một pod với tên là busybox thoả mãn điều kiện của Network Policy để kiểm tra vào webapp2 deployment thông qua ClusterIP service. Chạy lệnh wget trên pod này để truy cập vào webapp.
- Ghi câu lệnh trên và kết quả vào file ~/cau3/ketqua.txt
- Lưu deployment manifest (yaml) vào ~/cau3/webapp2.yaml
- Lưu network policy manifest (yaml) vào ~/cau3/access-web.yaml
```
kubectl apply -f webapp2.yaml
```
```
kubectl get deployment webapp2
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
webapp2   2/2     2            2           2m57s
```
