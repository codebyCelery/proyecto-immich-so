# Proyecto Sistemas Operativos: Despliegue de Immich con Podman

## Descripción
Este repositorio contiene la configuración y evidencias del despliegue de la arquitectura de microservicios de Immich utilizando contenedores rootless (Podman) en una instancia de AWS EC2. 

El proyecto demuestra la gestión de recursos del Sistema Operativo mediante la implementación de límites de memoria (Cgroups) y la comprobación de la intervención del OOM-Killer del Kernel de Linux.

## Comandos de Despliegue utilizados (Scripts)

**1. Preparación del entorno y Swap:**
\`\`\`bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
\`\`\`

**2. Despliegue de Contenedores:**
\`\`\`bash
podman-compose up -d
\`\`\`

**3. Comandos de Auditoría e Instrumentación (Evidencias):**
\`\`\`bash
# Monitoreo de límites (Cgroups)
sudo podman stats --no-stream

# Validación de memoria directa al Kernel
cat /proc/$(sudo podman inspect -f '{{.State.Pid}}' immich_postgres)/status | grep -i mem

# Verificación de red (Puerto 80)
curl -I http://localhost
\`\`\`

## URL del video
https://drive.google.com/file/d/1tCDNfDyhQxYqHp7l17fhRVWMyoDiEsoe/view?usp=sharing
