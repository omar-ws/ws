# Criar SystemCTL

```bash
mkdir /var/www/ && cd /var/www/
wget https://worldskills.s3.us-east-1.amazonaws.com/br-pr-2026/lab2/site.zip
unzip site.zip
chmod +x site-linux-amd64
cat > /etc/systemd/system/site.service << EOF
[Unit]
After=network.target
[Service]
ExecStart=/var/www/site-linux-amd64
WorkingDirectory=/mnt/efs/fs1
[Install]
WantedBy=multi-user.target
EOF
systemctl daemon-reload
systemctl enable site
systemctl start site
```