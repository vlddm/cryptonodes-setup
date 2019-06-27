Ubuntu 18.04 is recommended

All commands running as root
Create user:
```
useradd --create-home --home-dir /opt/ethereum ethereum
```

Download geth binary and startup script:
```
wget https://gethstore.blob.core.windows.net/builds/geth-linux-amd64-1.8.27-4bcc0a37.tar.gz -O - | tar -xz --strip 1 -C /usr/local/bin
wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/ethereum-geth/ethereum-geth-mainnet.service -O /etc/systemd/system/ethereum-geth-mainnet.service

```

Start it up:
```
systemctl daemon-reload
systemctl enable ethereum-geth-mainnet.service
systemctl start ethereum-geth-mainnet.service
```
Check if node is running well: 
`ps auxww | fgrep geth` should return process with full agruments and metadata.
If not use `journalctl -u geth-mainnet.service` to check logs

