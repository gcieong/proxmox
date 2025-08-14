# Tailscale

- Install tailscale

[https://tailscale.com/download/linux](https://tailscale.com/download/linux)

- Exit nodes

[https://tailscale.com/kb/1103/exit-nodes?tab=linux](https://tailscale.com/kb/1103/exit-nodes?tab=linux)

- Verify service status.
```bash
systemctl status tailscaled
```

- Activate and open Tailscale web interface.
```bash
tailscale web
```

- Performance best practices
```
[https://tailscale.com/kb/1320/performance-best-practices](https://tailscale.com/kb/1320/performance-best-practices)
```

## Setup Cloudflare DNS in host

- Show NetworkManager service status.
```bash
nmcli general status
```

- Show connections.

```bash
nmcli connection show
```

- Disable DNS update.
```bash
sudo nmcli connection modify wifi-home ipv4.ignore-auto-dns yes
```

- Add Cloudflare DNS.

```bash
nmcli connection modify 4B_5G ipv4.dns "1.1.1.1 1.0.0.1"
```

- Reboot network connection.

```bash
nmcli connection down 4B_5G-home
nmcli connection up 4B_5G
```

- Verify configuration.

[https://1.1.1.1/help](https://1.1.1.1/help)
