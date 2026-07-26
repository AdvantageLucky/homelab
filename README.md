# Personal Homelab
Self-hosted infra on a *Lenovo ThinkCentre M720q*, using docker for services and Tailscale for secure remote access.

Original goal was to be able to listen to my own music, but then the goal was expanded: own my data, learn infraestructure/DevOps, hands-on, and have files, tools and music available eanywhere without exposing everything to the internet

## Hardware
- **Machine**: Lenovo ThinkCentre M720q Tiny
- **CPU**: Intel Core i3-8100T (4 cores, 35W TDP)
- **RAM**: 8 GB DDR4
- **Storage**: 256 GB SATA SDD
- **OS**: Debian 13 Trixie, headless

## Architecture 
All services run as Docker containers and remote access goes exclusively through Tailscale (WireGuard-based mesh VPN). Container ports are bound to localhost and reached only over the Tailscale interface, so services are never accessible from the LAN or the open internet. 

## Services
| Service | Purpose |
|-------------|-------------------------------|
| Tailscale | Secure remote access (mesh VPN) |
| Navidrome | Music streaming server |
| Syncthing | File sync across devices |
| RSSHub | RSS feed generation |
| Glance | Dashboard |

## Networking
- Static IP on the LAN via NetworkManager
- Remote access through Tailscale with MagicDNS
- UFW firewall

## Deployment
Each service is self-contained. To bring one up:
```bash
cd <service>
docker compose up -d
```
