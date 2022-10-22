## fail2ban
### Installation
```bash
sudo apt install fail2ban
# Then...
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
sudo systemctl status fail2ban
```

### Configuration
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
# Then..
sudo nano /etc/fail2ban/jail.local
```
Change the following:
 - Ignore ips
   - `127.0.0.1/8 ::1 192.168.1.0/24 <REMOTE_IP>`
 - bantime: 120d
 - findtime: 24h
 - maxretry = 3

Then restart the service
```bash
sudo systemctl restart fail2ban
```

### Add slack message option
Next, add slack message to action (see link in sources)

First, copy contents in the link provided to a new file
```bash
sudo nano /etc/fail2ban/action.d/slack-notify.conf
```
Then, make changes in the local jail
```bash
sudo nano /etc/fail2ban/jail.local
```
Such:
```bash
action = %(action_)s
         slack-notify
```

Restart the service
```bash
sudo systemctl restart fail2ban
```

### Later Stage Options
#### Influxdb logging

#### Add invalid webpage blocking [nginx]


First, make a new file to hold the regex patterns and other settings
```bash
sudo nano /etc/fail2ban/filter.d/nginx-4xx.conf
```
Add the following:
```unit file (systemd)
[Definition]
failregex = ^<HOST>.*"(GET|POST).*" (4\d{2}) .*$
ignoreregex =
```
Then open the jail.local
```bash
sudo nano /etc/fail2ban/jail.local
```
Add the following:
```unit file (systemd)
[nginx-4xx]
enabled = true
port = http,https
logpath = /var/log/nginx/access.log
maxretry = 3
```
Restart fail2ban
```bash
sudo systemctl restart fail2ban
```
