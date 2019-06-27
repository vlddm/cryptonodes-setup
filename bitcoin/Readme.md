Ubuntu 18.04 is recommended

Create user and install packages:

```
useradd --create-home --home-dir /opt/bitcoin bitcoin
useradd --create-home --home-dir /opt/electrumx-bitcoin electrumx-bitcoin
apt install python3-pip
```

Download distributives:
```
cd /opt/bitcoin
wget https://bitcoin.org/bin/bitcoin-core-0.18.0/bitcoin-0.18.0-x86_64-linux-gnu.tar.gz
tar -xf bitcoin-0.18.0-x86_64-linux-gnu.tar.gz
ln -s bitcoin-0.18.0 bitcoin
chown -R bitcoin:bitcoin /opt/bitcoin
```

Now need to setup some configs
```
mkdir -p ~/.bitcoin
wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/bitcoin/bitcoin.conf -O /opt/bitcoin/.bitcoin/bitcoin.conf
wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/bitcoin/electrumx.conf -O /opt/electrumx-bitcoin/config

wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/bitcoin/bitcoin.service -O /etc/systemd/system/bitcoin.service
wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/bitcoin/electrumx-bitcoin.service -O /etc/systemd/system/electrumx-bitcoin.service
```

Start it up:
```
systemctl daemon-reload
systemctl enable bitcoin.service
systemctl start bitcoin.service
```

When bitcoin node synced we can run electrumx service:
```
systemctl enable electrumx-bitcoin.service
systemctl start electrumx-bitcoin.service
```

Check if its ok:
```
ps auxww | fgrep bitcoind
ps auxww | fgrep electrumx_server
journalctl -u bitcoin.service
journalctl -u electrumx-bitcoin.service
```
