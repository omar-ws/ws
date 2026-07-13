# Nginx Pronto

```jsx
User data básico com Nginx:

#!/bin/bash
yum update -y

#!/bin/bash
yum update -y
yum install -y nginx
systemctl start nginx
systemctl enable nginx
echo "<h1>Hello World</h1>" > /usr/share/nginx/html/index.html

Para Ubuntu:
#!/bin/bash
apt update -y
apt install -y nginx
systemctl start nginx
systemctl enable nginx
echo "<h1>Hello World</h1>" > /var/share/nginx/html/index.html

```