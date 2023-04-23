# uptime-kuma

Uptime Kuma là một công cụ giám sát mã nguồn mở được viết bằng Nodejs. Nó là một công cụ giám sát độc lập với bảng điều khiển đẹp mắt và hỗ trợ một số phương pháp thông báo. Uptime Kuma giám sát thời gian hoạt động của các máy chủ hoặc máy chủ thông qua các giao thức HTTP, TCP và Ping. Nếu website không phản hồi qua các giao thức này trong khoảng thời gian, Uptime Kuma sẽ gửi tin nhắn qua Webhooks, Telegram, Discord, Gotify, Slack, Pushover, Email (SMTP),...

Các tính năng nổi bật của Uptime Kuma có thể kể tới:

* Giám sát hoạt động của website thông qua các giao thức HTTP(s) / TCP / HTTP(s) Keyword / Ping / DNS Record / Push / Steam Game Server. Fancy, Reactive, Fast UI/UX,... rất phong phú lựa chọn cho mọi người
* Thông báo được đa kênh: Telegram, Discord, Gotify, Slack, Pushover, Email (SMTP),...
* Thời gian giãn cách giữa cách lần thăm dò tối thiểu 20s
* Giao diện website đa ngôn ngữ
* Có biểu đồ heartbeat rõ ràng cho từng Monitor


Uptime Kuma is an open-source tool to monitor the uptime of hosts or servers. This tool can be used to check if a website or service is up. If the monitored target is not reachable for a specified time interval, then notifications can be sent via Slack, Telegram, Discord, or other notification service. Uptime Kuma provides a dashboard that can be accessed via a web browser.

This tutorial explains how to install Uptime Kuma inside a Docker container in the Linux. Commands have been tested on Ubuntu.

Prepare environment
Make sure you have installed Docker in your system

Install Uptime Kuma Inside Docker Container in Linux:

Host network

Run the following command to create a container for Uptime Kuma that uses host network:
```
mkdir -p /opt/uptime-kuma/data
```
```
docker run -d --name=uptime-kuma --restart=always --network=host \
    -v /opt/uptime-kuma/data:/app/data \
    louislam/uptime-kuma
```    
User-defined bridge network

User-defined bridge network can be used for listening on different port. By default, Uptime Kuma service is listening on port 3001. It can be changed with -p option.
```
docker network create app-net

docker run -d --name=uptime-kuma --restart=always --network=app-net \
    -p 8080:3001 \
    -v /opt/uptime-kuma/data:/app/data \
    louislam/uptime-kuma
```    
Testing Uptime Kuma

Open a web browser and go to http://<IP_ADDRESS>:8090, where <IP_ADDRESS> is the IP address of the system. For the first time, you will be asked to create the administrator account. After that, you will be redirected to the dashboard.

Uninstall Uptime Kuma

To completely remove Uptime Kuma, remove its container:
```
docker rm --force uptime-kuma
```
Remove Uptime Kuma image:
```
docker rmi louislam/uptime-kuma
```
You can also remove Uptime Kuma data:
```
sudo rm -rf /opt/uptime-kuma
```
If a user-defined bridge network was created, you can delete it as follows:
```
docker network rm app-net
```
