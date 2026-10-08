\# Bài 3: Viết Dockerfile đóng gói trang Web HTML tĩnh



\## 1. Mục tiêu



\* Tạo một trang HTML tĩnh đơn giản.

\* Sử dụng Dockerfile để đóng gói trang HTML vào Nginx image.

\* Build Docker image và chạy container trên port 8081.



\## 2. Tạo trang HTML



Tạo file `index.html` với nội dung:



```html

<h1>Hello Docker Session 09!</h1>

```



\## 3. Dockerfile



Tạo file `Dockerfile` gồm 2 câu lệnh:



```dockerfile

FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

```



Trong đó:



\* `FROM nginx:alpine`: sử dụng Nginx Alpine làm image cơ sở.

\* `COPY`: sao chép file `index.html` vào thư mục mặc định chứa trang web của Nginx.



\## 4. Build Docker Image



Sử dụng lệnh:



```bash

docker build -t my-html-app:v1 .

```



Kết quả:



```text

Successfully built bb60d814047a

Successfully tagged my-html-app:v1

```



Image được tạo thành công với tên `my-html-app:v1`.



\## 5. Khởi chạy container



Sử dụng lệnh:



```bash

docker run -d -p 8081:80 --name html-app my-html-app:v1

```



Container được khởi chạy với port mapping:



```text

0.0.0.0:8081->80/tcp

```



Port `8081` của VPS được chuyển tiếp đến port `80` của Nginx trong container.



\## 6. Kiểm tra kết quả



Sử dụng lệnh:



```bash

curl http://localhost:8081

```



Kết quả:



```html

<h1>Hello Docker Session 09!</h1>

```



Kết quả kiểm tra HTTP:



```text

HTTP/1.1 200 OK

Content-Type: text/html

Content-Length: 33

```



Như vậy Web Server Nginx đã hoạt động và trả về đúng nội dung HTML yêu cầu.



\## 7. Kiểm tra file trong container



Đã kiểm tra file HTML bên trong container bằng:



```bash

docker exec html-app cat /usr/share/nginx/html/index.html

```



Kết quả:



```html

<h1>Hello Docker Session 09!</h1>

```



\## 8. Dọn dẹp container



Sau khi kiểm tra, container được dừng bằng:



```bash

docker stop html-app

```



Sau đó xóa:



```bash

docker rm html-app

```



Kiểm tra lại bằng:



```bash

docker ps -a

```



Container `html-app` đã được xóa thành công.



\## 9. Kết luận



Đã hoàn thành bài thực hành Dockerfile đóng gói trang Web HTML tĩnh.



Các yêu cầu đã thực hiện:



\* Tạo `index.html`.

\* Tạo Dockerfile với 2 câu lệnh.

\* Sử dụng image `nginx:alpine`.

\* Build image `my-html-app:v1`.

\* Chạy container `html-app` trên port `8081`.

\* Kiểm tra thành công bằng `curl`.

\* Đã dừng và xóa container sau khi kiểm tra.



