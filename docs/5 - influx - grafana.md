## influxdb + grafana
 - Log fail2ban activity
 - Log other activity
 - Visualize various data

### Installation
```bash
# Create network
docker create network okr-network

# Add Env vars
. ./secrets/influx-grafana-env.sh

cd ~/extras/paleiron/services/influx-grafana
docker-compose up -d
```
### Config
```bash
# Add influx logging of fail2ban notifications
sudo nano /etc/fail2ban/action.d/influxdb.conf
# In jail.local:

```
### Create user
```bash
curl -XPOST "http://localhost:8086/query" \
  --data-urlencode "q=CREATE USER username WITH PASSWORD 'strongpassword' WITH ALL PRIVILEGES"
```