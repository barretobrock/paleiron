## influxdb + grafana
 - Log fail2ban activity
 - Log other activity
 - Visualize various data

### influx, telegraf
Follow instructions [here](https://portal.influxdata.com/downloads/) to set up the repo for influx & telegraf installation, then
```bash
sudo apt install influxdb2 telegraf
```

### Grafana
```bash 
# Download GPG, add
sudo wget -q -O /usr/share/keyrings/grafana.key https://packages.grafana.com/gpg.key
# Add repo
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
# Update sources & install
sudo apt update && sudo apt install grafana

# Start server
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
# Configure to run on boot
sudo systemctl enable grafana-server.service
```
Config changes `/etc/grafana/grafana.ini`
```bash
http_port=????
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
