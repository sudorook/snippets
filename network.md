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

## Trace network routes

To track route to any host, use `traceroute`:

```sh
traceroute <ip address>
```

## `netstat`

The output of `netstat -at` is:

The columns are as follows from left to right:

- `Proto`: Protocol used, TCP or UDP.
- `Recv-Q`: Data that is queued to be received
- `Send-Q`: Data that is queued to be sent
- `Local Address`: Locally connected host
- `Foreign Address`: Remotely connected host
- `State`: The state of the socket

See the manpage for a list of socket states, but here are a few:

- `LISTENING`: The socket is listening for incoming connections, remember when
  we make a TCP connection our destination has to be listening for us before we
  can connect.
- `SYN_SENT`: The socket is actively attempting to establish a connection.
- `ESTABLISHED`: The socket has an established connection
- `CLOSE_WAIT`: The remote host has shutdown and we're waiting for the socket to
  close
- `TIME_WAIT`: The socket is waiting after close to handle packets still in the
  network

## DNS lookup

Use the following tools for DNS lookups on the command line.

```sh
nslookup <ipaddr>
```

```sh
dig <ipaddr>
```
