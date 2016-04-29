# Dependencies
```bash
apt-get install gnutls-bin python
```

# Setup
```
# Create a letsencrypt user
useradd -d /etc/letsencrypt -r letsencrypt
usermod -a -G letsencrypt www-data

# Change to the user
sudo -u letsencrypt bash

# Clone this repository
cd ~
git clone https://github.com/Wassasin/letsencrypt-nginx-tiny.git bin
pushd bin
git clone submodule update --init
popd

# Create a Let's Encrypt account private key (if you haven't already)
openssl genrsa 4096 > account.key

# Create domains (directories and base certificates)
./bin/create-domain example.com www.example.com admin.example.com
...

# Prepare nginx for the challenges
# <TODO>

# Init+update domains (sign certificates via acme-tiny, prepare chains, and reboot)
./update_all

# Verify that nginx is still doing its thing

# Install cronjob
(crontab -l ; echo "0 0 1 * * ./bin/update-all") | crontab -
```
