# CentOs 9 Stream

## Network configuration

display devices
``` 
nmcli device
```

shown device info
```
nmcli device show enp1s0 
```

set dhcp client on
```
nmcli connection modify enp1s0 ipv4.method auto
```

set ip configuration to manual
```
 nmcli connection modify enp1s0 ipv4.method manual
```

set IPv4 address
```
nmcli connection modify enp1s0 ipv4.addresses ADDRESS/PREFIX
```

set gateway
```
 nmcli connection modify enp1s0 ipv4.gateway GATEWAY
```

set dns server
```
nmcli connection modify enp1s0 ipv4.dns "DNS1 DNS2 DNS3"
```

set dns search
```
nmcli connection modify enp1s0 ipv4.dns-search my.net
```

restart network interface
```
nmcli connection down enp1s0; nmcli connection up enp1s0
```

## Disable IPv6
```
grubby --update-kernel ALL --args ipv6.disable=1
grubby --update-kernel ALL --remove-args ipv6.disable
```

## Configure dnf
Set fastest mirror
```
echo "fastestmirror=1" >> /etc/dnf/dnf.conf
```

Set proxy for dnf
```
cat << EOF >> /etc/dnf/dnf.conf
proxy=http://PROXY:PORT/
proxy_username=PROXYUSER
proxy=password=PROXYPASS
minrate=1
timeout=1000
EOF
```

## Add CA to base os
Copy your certs to
> /etc/pki/ca-trust/source/anchors/

Update Certs
```
update-ca-trust extract
```

## Automatic updates
Install needed package
```
dnf install dnf-automatic
```

If you want to download packages only you doesnt change anything. If you want to use a real automatic update
you must change these line
> apply_updates = no
to yes
in
> /etc/dnf/automatic.conf

```
sed -i "/^apply_updates*./c\apply_updates = yes" /etc/dnf/automatic.conf
```


