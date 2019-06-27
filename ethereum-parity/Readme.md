Ubuntu 18.04 is recommended

All commands as root

Create user:
```
useradd --create-home --home-dir /opt/ethereum ethereum
```

Fullnode setup:
```
wget https://releases.parity.io/ethereum/v2.4.7/x86_64-unknown-linux-gnu/parity -O /usr/local/bin/parity
chmod +x /usr/local/bin/parity
wget https://raw.githubusercontent.com/vlddm/cryptonodes-setup/master/ethereum-parity/ethereum-parity.service -O /etc/systemd/system/ethereum-parity.service
```

Start it up:
```
systemctl --user daemon-reload
systemctl --user enable ethereum-parity.service
systemctl --user start ethereum-parity.service
```
Check if node is running well: 
`ps auxww | fgrep parity` should return process with full agruments and metadata.
If not user `journalctl --user -u ethereum-parity.service` to check logs

