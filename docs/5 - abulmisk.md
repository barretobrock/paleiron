## Install nginx-proxy-manager
docs [here](https://nginxproxymanager.com/)
```bash
# Create docker network
docker network create okr-network
# Open external ports
sudo ufw allow 80,81,443 proto tcp

cd ~/extras/paleiron/services/nginx-proxy-manager
docker-compose up -d
```