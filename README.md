# Bastionado de Sistemas con Ansible

Trabajo Final - Bastionado de Redes y Sistemas - IES San Clemente - Pablo Capelo Solís

Proyecto de bastionado automatizado de servidores Ubuntu 24.04 mediante Ansible, desarrollado para el módulo de Bastionado de Redes y Sistemas de la Especialización en Ciberseguridad IT.

## Entorno

| Máquina | SO | IP | Rol |
|---|---|---|---|
| Ansible | Ubuntu Desktop 24.04 | 192.168.56.10 | Nodo de control |
| Servidor1 | Ubuntu Desktop 24.04 | 192.168.56.11 | Cliente |
| Servidor2 | Ubuntu Server 24.04 | 192.168.56.12 | Cliente |
| Kali | Kali Linux 2026.1 | DHCP | Máquina atacante |

## Roles

| Rol | Responsabilidad |
|---|---|
| `common` | Actualización del sistema, herramientas básicas y usuario admin |
| `ssh` | Bastionado SSH: autenticación por clave, parámetros de seguridad y banner |
| `firewall` | Firewall con iptables: bloqueo de tráfico entrante excepto puerto 22 |
| `fail2ban` | Protección contra fuerza bruta: bloqueo de IPs tras intentos fallidos |
| `pam` | Política de contraseñas: complejidad, caducidad, historial y bloqueo de cuenta |
| `hardening` | Bastionado del kernel con sysctl y banners legales del sistema |

## Uso

```bash
# Clonar el repositorio
git clone https://github.com/a25pablocs/ansible-bastionado.git
cd ansible-bastionado

# Lanzar el bastionado completo
ansible-playbook playbooks/site.yml --ask-become-pass

# Lanzar la auditoría post-hardening
ansible-playbook playbooks/audit.yml --ask-become-pass
```

## Resultados — Lynis Hardening Index

| Momento | Hardening Index |
|---|---|
| Antes del bastionado | 63 / 100 |
| Después del bastionado | 73 / 100 |
