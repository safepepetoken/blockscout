ssh root@154.49.246.65
Pepesafe123@

apt-get install git

ssh-keygen
cat ~/.ssh/id_rsa.pub

git clone git@github.com:safepepetoken/blockscout.git

sudo apt-get update && sudo apt-get install ca-certificates curl gnupg lsb-release && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io && sudo apt-get install docker-compose-plugin

cd blockscout && docker compose -f docker-compose.yml up -d && cd ../

docker exec -it blockscout /bin/bash -c 'find / -type d -name "images"'
docker exec -it blockscout /bin/bash -c "cd /app/lib/block_scout_web-5.1.4/priv/static/images && wget -O -c https://pepesafe.finance/assets/images/logo.png -O pepesafe-white.png"
docker exec -it blockscout /bin/bash -c "cd /app/lib/block_scout_web-5.1.4/priv/static/images && wget -O -c https://pepesafe.finance/assets/images/logo.png -O pepesafe-black.png"

docker exec -it blockscout /bin/sh
docker cp blockscout:/app/lib/block_scout_web-5.1.4/priv/static/css/main-page-b397b8c137115fb50bdca66592d0a677.css main-page-b397b8c137115fb50bdca66592d0a677.css
docker cp main-page-b397b8c137115fb50bdca66592d0a677.css blockscout:/app/lib/block_scout_web-5.1.4/priv/static/css/main-page-b397b8c137115fb50bdca66592d0a677.css
gzip -c main-page-b397b8c137115fb50bdca66592d0a677.css > main-page-b397b8c137115fb50bdca66592d0a677.css.gz
docker cp main-page-b397b8c137115fb50bdca66592d0a677.css.gz blockscout:/app/lib/block_scout_web-5.1.4/priv/static/css/main-page-b397b8c137115fb50bdca66592d0a677.css.gz
#5c34a2 - #47b858
#673ab5 - #47b858
#8258cd - #00C853
#3c226a - #00C853
#dcc8ff - #ffffff
#bda6e7 - #ffffff


apt-get remove apache2
apt-get purge apache2
sudo apt update
sudo apt install nginx
systemctl start nginx
nano /etc/nginx/conf.d/explorer-pepesafe-finance.conf
server {
    listen 80;
    server_name explorer.pepesafe.finance;
    location / {
        proxy_pass http://127.0.0.1:4000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 36000;

        # WebSocket support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
systemctl enable nginx
systemctl restart nginx

sudo apt install python3 python3-venv libaugeas0
sudo python3 -m venv /opt/certbot/
sudo /opt/certbot/bin/pip install --upgrade pip
sudo /opt/certbot/bin/pip install certbot certbot-nginx
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
certbot --nginx -d explorer.pepesafe.finance
export EDITOR=/bin/nano
export VISUAL=nano
crontab -e
0 12 * * * /usr/bin/certbot renew --dry-run