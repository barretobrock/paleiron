## Install nginx-proxy-manager
docs [here](https://nginxproxymanager.com/)
```bash
# Create docker network (if not already done)
docker network create okr-network

# Open external ports
sudo ufw allow 80
sudo ufw allow 81
sudo ufw allow 443
sudo ufw reload

cd ~/extras/paleiron/services/nginx-proxy-manager
docker-compose up -d
```