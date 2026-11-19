<h1 align="center"> Personal Homelab </h1>
<img width="1366" height="768" alt="homelab" src="https://github.com/user-attachments/assets/9abbb0c7-bc69-473c-98f8-8dd201f62f92" />

<p align="center"> Self-hosted infra on a <em><b>Lenovo ThinkCentre M720q</b></em>, using Docker for services and Tailscale for secure remote access </p>

## Purpose
Original purpose was to be able to listen to my own music, but then the goal was expanded: own my data, learn infrastructure/DevOps, hands-on, and have files, tools and music available anywhere without exposing everything to the internet

## Hardware
- **Machine**: Lenovo ThinkCentre M720q Tiny
- **CPU**: Intel Core i3-8100T (4 cores, 35W TDP)
- **RAM**: 8 GB DDR4
- **Storage**: 256 GB SATA SSD & 492 GB SATA HDD
- **OS**: Debian 13 Trixie, headless

## Architecture 
All services run as Docker containers and remote access goes exclusively through Tailscale (WireGuard-based mesh VPN). Container ports are bound to localhost and reached only over the Tailscale interface, so services are never accessible from the LAN or the open internet. 

## Services
| Service | Purpose |
|-------------|-------------------------------|
| Tailscale | Secure remote access (mesh VPN) |
| Uptime Kuma | Uptime and service monitoring |
| Frigate | Self-Hosted NVR server |
| Frigate-Notify | Notification service for frigate |
| Vaultwarden | Self-Hosted personal vault |
| Navidrome | Music streaming server |
| Calibre-Web-Automated | E-book library and automated downloader |
| Syncthing | File sync across devices |
| Photoview | Self-Hosted photo gallery |
| Forgejo | Self-Hosted Git server |
| Mosquitto | lightweight MQTT broker |
| Glance | Dashboard |

## Backup
All important data is backed up using restic, backblaze B2 and healthchecks.io. restic handles backup automation, backblaze B2 handles bucket-like cloud storage, and healthchecks.io pushes notifications for backup events such as backups/errors

## Networking
- Static IP on the LAN via NetworkManager
- Remote access through Tailscale with MagicDNS
- UFW firewall

## Deployment
Each service is self-contained. To bring one up:
```bash
cd <service>
docker compose up -d
tailscale serve --bg --https=PORT http://127.0.0.1:PORT
```
