## Server Setup
NB! This assumes a freshly-created Ubuntu server
### Update packages
```bash
sudo apt update && sudo apt upgrade
```
### Non-root user creation
```bash
read -p "Enter user: " MYUSER
echo "Adding ${MYUSER}..."
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

Poetry
```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
```

### Terminal mods
Purely optional, but may help with adminning
#### Install zsh
```bash
sudo apt install zsh
# Check version
zsh --version

# Set as default shell, then log out & back in
chsh -s /usr/bin/zsh
```
After logging back in,
```bash
# Confirm zsh is the new default
echo $SHELL
# >>> /usr/bin/zsh
```
#### Install oh-my-zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
#### Install powerline fonts
```bash
sudo apt install fonts-powerline
```
#### Install powerlevel10k
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Then edit in ~/.zshrc
ZSH_THEME="powerlevel10k/powerlevel10k"
# Log out, log back in
```

#### Shell completion?