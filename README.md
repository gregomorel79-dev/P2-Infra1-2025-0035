# P2 – Infra 1: VPN Site-to-Site FortiGate ↔ FortiGate
**Gregorys Morel Duluc – 2025-0035 – Seguridad de Redes (ITLA)**
https://youtu.be/j5v7lGj5dFg
## Topología
FG1 (usuarios) ⇄ ISP 200.35.0.0/24 ⇄ FG2 (servidor). Emulado en GNS3.

## Plan de IPs
| Equipo | WAN | LAN | Gestión |
|---|---|---|---|
| FG1 | 200.35.0.1/24 | 10.0.35.129/25 (VLAN 10, DHCP .130–.254) | 192.168.56.51 |
| FG2 | 200.35.0.2/24 | 10.0.35.1/28 | 192.168.56.52 |
| Servidor web HTTPS | — | 10.0.35.2/28 | — |

## Configuración (GUI)
- Interfaces LAN, DHCP en FG1.
- VPN IPsec site-to-site (IKEv1, DES/SHA1, DH14, PSK) con el asistente.
- Rutas estática y blackhole hacia la red remota; políticas LAN ⇄ VPN.

## Pruebas
- PC1 recibe IP por DHCP (`ip a`).
- `ping`, `curl -k https://10.0.35.2` y `traceroute` por el túnel.
- Túnel deshabilitado → curl falla (timeout); habilitado → funciona.

## Archivos
`FG1-Infra1.conf`, `FG2-Infra1.conf`
