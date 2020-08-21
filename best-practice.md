# Installing Redis On Linux Ubuntu 18.04

This is best practice on installing Redis with its own username and group.

```console
sudo apt update -y
sudo apt install build-essential tcl -y
sudo apt install tcl-tls libssl-dev -y

sudo adduser --system --group --no-create-home redis

sudo mkdir /var/lib/redis
sudo chown redis:redis /var/lib/redis
sudo chmod 770 /var/lib/redis

sudo mkdir /var/log/redis
sudo touch /var/log/redis/redis.log
sudo chmod 660 /var/log/redis/
sudo chmod 640 /var/log/redis/redis.log

cd /tmp
wget http://download.redis.io/releases/redis-6.0.6.tar.gz

sha256sum redis-6.0.6.tar.gz

tar xzf redis-6.0.6.tar.gz
cd ./redis-6.0.6

sudo make BUILD_TLS=yes install

sudo mkdir /etc/redis
sudo cp redis.conf /etc/redis
sudo chown -R redis:redis /etc/redis
sudo chmod 640 /etc/redis/redis.conf

sudo runuser -u redis /usr/local/bin/redis-server /etc/redis/redis.conf & 

sudo apt install redis-tools -y
```