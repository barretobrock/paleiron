## Server Setup
NB! This assumes a freshly-created Ubuntu server
### Update packages
```bash
sudo apt update && sudo apt upgrade
```
### Non-root user creation
```bash
MYUSER=username_here
adduser ${MYUSER}
usermod -aG sudo ${MYUSER}
```
### Firewall setup
```bash
ufw allow OpenSSH
ufw enable
ufw status
```
### Enable non-root user access
```bash
rsync --archive --chown=${MYUSER}:${MYUSER} ~/.ssh /home/${MYUSER}
```

Open up a new terminal window, try to log in as non-root user.
Close root session upon successful log in.

Make some new directories on the non-root user's home & set the timezone
```bash
mkdir keys logs venvs extras data
sudo timedatectl set-timezone America/Chicago
# Reconfigure dash to bash
sudo dpkg-reconfigure dash  # select 'No' to default to bash
```

Some general packages to add:
```bash
sudo apt install python3.10-venv
```