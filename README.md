# runner
Host configuration

1. Install Ubuntu 22.04

2. Enable remote ssh
```
sudo apt-get install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

3. Set static ip
To see current ip
```
ip addr show
```
To set static ip address
```
sudo vim /etc/netplan/01-netcfg.yaml
```
add
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp1s0: # Edit this line according to your network interface name.
      dhcp4: no
      addresses:
        - 192.168.50.252/24 # Edit this line according to your host ip.
      routes:
        - to: default
          via: 192.168.50.1 # Edit this line according to your router ip.
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```
```
sudo netplan apply
reboot
```

4. Add to your `/etc/hosts`
```
192.168.50.252  kestrel-runner1
```
