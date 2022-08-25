## docker / docker-compose
### install docker
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
# GPG
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# Add repo to sources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# Update
sudo apt update
# Ensure this is the proper 'from docker' repo
apt-cache policy docker-ce
# Install
sudo apt install docker-ce
# Check status
sudo systemctl status docker
```
### install docker-compose
Get latest version of docker compose, install it in the `cli-plugins` directory in `~/.docker/`
```bash
LATEST=$(curl -sL https://api.github.com/repos/docker/compose/releases/latest | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/') 
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/${LATEST}/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
# Make executable
chmod +x ~/.docker/cli-plugins/docker-compose
# Add username to docker group
sudo usermod -aG docker ${MY_USER}
su - ${MY_USER}
# Create symlink to expose it in PATH
sudo ln -s ~/.docker/cli-plugins/docker-compose /usr/bin/docker-compose
```