# Network

## Find IP address of all devices on local network

```sh
nmap -sP <ip addr>/<bitmask>
```

For example, `nmap -sP 192.168.0.1/24`.

## Scan wireless network access points

Using NetworkManager, run:

```sh
nmcli -f NAME,SSID,BSSID,MODE,CHAN,FREQ,RATE,SIGNAL,SECURITY,IN-USE device wifi
```

The `CHAN` column can be used to check whether a channel is too congested by
multiple access points.

To directly count access points using each channel, run:

```sh
nmcli -t -f CHAN device wifi | sort | uniq -c | sort -rn
```

## DNS lookup

Use the following tools for DNS lookups on the command line.

```sh
nslookup <ipaddr>
```

```sh
dig <ipaddr>
```
