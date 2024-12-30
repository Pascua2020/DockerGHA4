##### Hashtags #️⃣ : #devops #docker #linux #automation #ci #github-actions #dokku #java-springboot #nginx #####

### README en Español.To read the English versión,go to README-English.md

# ✅️ **DockerGHA4**


( Docker, GitHub Actions, Java Spring Boot y Dokku )

![DevOps Logo](https://globalittrainers.com/wp-content/uploads/2021/06/Devops-logo1.png)

![Build Status](https://github.com/Pascua2020/DockerGHA/actions/workflows/main.yml/badge.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Docker](https://img.shields.io/badge/container-Docker-blue?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-blue?logo=githubactions&logoColor=white)
![Dokku](https://img.shields.io/badge/deployment-Dokku-blueviolet?logo=dokku)
![No License](https://img.shields.io/badge/license-None-red)


```diff 

- Este proyecto demuestra cómo integrar Docker, GitHub Actions, Java Spring Boot y Dokku para crear un flujo de trabajo de desarrollo y despliegue automatizado. 

- La aplicación es un servicio básico de Spring Boot que se ejecuta dentro de un contenedor Docker, se automatiza con GitHub Actions y se despliega usando Dokku.

```

## 1️⃣🟥 **Características**

#### ⚡️ *Docker:* 

![Docker Logo](https://dwglogo.com/wp-content/uploads/2017/09/Docker_container_engine_logo.png)

Empaqueta la aplicación Spring Boot en un contenedor para garantizar que se ejecute de la misma manera en cualquier entorno.

#### ⚡️ *GitHub Actions:* 

![GHA Logo](https://miro.medium.com/v2/resize:fit:1075/0*w5Fsp29pbWIUpW7Q.png)

Automatiza el proceso de construcción, prueba y despliegue de la aplicación con cada cambio en el repositorio.

#### ⚡️ *Java Spring Boot:* 

![Java SB Logo](https://miro.medium.com/v2/resize:fit:720/format:webp/1*MvUFlFTbiU40ae1SK69-Jg.png)

Framework backend para el desarrollo de la aplicación web.

#### ⚡️ *Dokku:* 

![Dokku Logo](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6mNvZ4G3tFQpY1qcVDQdWGSVUW5ljKhyUxfgTeFAZUX5r48Xm8M6mMf55h3IkCw1DC3ERygHIWgsvguq1cYntoluBXdW4-7W_Uhw8JHrvQIeW5T1lIGOuk7WTvkP5O-M_XR4J-6W9Gg-vfhG6B-Q6w75EaJ_eHlGvjxcbEGB3_xckw6OnTwxuBWsL-TRQ/s2800/A%20Deep%20Dive%20with%20Dokku.webp)

Plataforma de despliegue similar a Heroku que usa contenedores Docker para gestionar aplicaciones de forma sencilla.

**Diferencias entre DockerGHA 4 con 1 , 2 y 3 :**

#### ⚙️ *Todos los Dockerfiles son idénticos:*

- Usan la imagen base busybox:latest.

- Copian un script run.sh en el contenedor que imprime la hora actual en la consola en un bucle infinito.

- Configuran el script run.sh como el punto de entrada del contenedor.

#### ⚙️ *Main.yml - Diferencias generales*:

*🔷️ 1. Repositorios:*

- 1 y 2 suben imágenes solo a Docker Hub.

- 3 sube solo a GHCR.

- 4 sube a ambos registries (Docker Hub y GHCR).

*🔷️ 2. Automatización:*

- Repositorios 2, 3 y 4 usan docker/metadata-action para etiquetas automáticas, mientras que el 1 no.

*🔷️ 3. Nombres de imagen:*

- Repositorio 1 tiene un nombre fijo: clockbox:latest.

- Los demás repositorios usan configuraciones dinámicas o específicas.

## 2️⃣🟧 **Estructura del Proyecto**
```
DockerGHA4/
│
├── .github/
│   └── workflows/
│       └── main.yml             # Flujo de trabajo de GitHub Actions
├── Dockerfile                   # Dockerfile para contenerizar la app
├── README.md                    # Documentación del proyecto
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └──  DominioApplication.java   # Clase principal de Spring Boot
│   │   └── resources/
│   │       └── application.properties         # Configuración de la app
├── target/                       # Directorio de build (generado por Maven/Gradle)
├── pom.xml                       # Archivo de configuración de Maven (si usas Maven)
└── .gitignore                    # Archivos y directorios que Git debe ignorar
```
#### 💾 *Dockerfile:* 

Archivo que define cómo crear la imagen Docker para el proyecto Spring Boot.

#### 💾 *main.yml:* 

Archivo de configuración para GitHub Actions que automatiza la construcción, pruebas y despliegue.

#### 💾 *src/:* 

Contiene el código fuente de la aplicación Spring Boot.

#### 💾 *pom.xml:* 

Archivo de configuración de Maven para las dependencias y construcción del proyecto.

#### 💾 *dokku-deploy.sh:* 

Script que automatiza el proceso de despliegue de la aplicación en un servidor remoto usando Dokku.

## 3️⃣🟨 **Instalación**

 🖱 *Requisitos*

ℹ️ *Docker:* 

Necesario para construir y ejecutar la aplicación en contenedores.

ℹ️ *GitHub Actions:* 

Se utiliza para la integración continua y automatización de procesos de despliegue.

ℹ️ *Dokku:* 

Necesitas un servidor remoto con Dokku instalado para gestionar el despliegue.

ℹ️ *Java:* 

Debes tener instalado Java y Maven para desarrollar la aplicación de backend con Spring Boot.

## 4️⃣⬜️ **Código**

#### 💡 *Dockerfile*
```
# syntax=docker/dockerfile:1
FROM busybox:latest
COPY --chmod=755 <<EOF /app/run.sh
#!/bin/sh
while true; do
  echo -ne "The time is now $(date +%T)\\r"
  sleep 1
done
EOF

ENTRYPOINT /app/run.sh
```
Este Dockerfile crea una imagen Docker basada en busybox que ejecuta un script en un bucle infinito para mostrar la hora actual en tiempo real.

📀 *1. Base de la imagen:* 

Usa busybox:latest, una imagen minimalista de Unix.

📀 *2. Copia del script:* 

Copia un script llamado run.sh al contenedor, que:

Imprime la hora actual (HH:MM:SS) en la misma línea de la terminal, actualizándola cada segundo.

📀 *3. Permisos:* 

El script recibe permisos de ejecución (chmod=755).

📀 *4. Punto de entrada:* 

Define el script run.sh como el punto de entrada, lo que significa que se ejecutará automáticamente cuando se inicie el contenedor.

🔑 Función:

Cuando el contenedor se ejecuta, el script imprime la hora actual, sobrescribiéndola cada segundo en la misma línea.

#### 💡 *Main.yml*
```
name: Publish Docker image

on:
  push:
    branches: ['main']

jobs:
  push_to_registries:
    name: Push Docker image to multiple registries
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
    steps:
      - name: Check out the repo
        uses: actions/checkout@v4

      - name: Log in to Docker Hub
        uses: docker/login-action@f4ef78c080cd8ba55a85445d5b36e214a81df20a
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Log in to the Container registry
        uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
        with:
          images: |
            my-docker-hub-namespace/my-docker-hub-repository
            ghcr.io/${{ github.repository }}
      
      - name: Build and push Docker images
        uses: docker/build-push-action@3b5e8027fcad23fda98b2e3ac259d8d67585f671
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
```

Este archivo main.yml define un flujo de trabajo de GitHub Actions para crear y publicar una imagen Docker en dos registros diferentes (Docker Hub y GitHub Container Registry) cada vez que se hace un push a la rama main.

📀 *1. Trigger (Disparador):*

Se ejecuta automáticamente cuando hay un push a la rama main.

📀 *2. Permisos:*

Establece los permisos necesarios para escribir en los paquetes y leer los contenidos del repositorio.

📀 *3. Job (push_to_registries):*

Se ejecuta en un entorno Ubuntu (ubuntu-latest).

📀 *4. Pasos del Job:*

✨️ *Checkout repository:*

Clona el repositorio en el entorno de GitHub Actions.

✨️ *Log in to Docker Hub:*

Inicia sesión en Docker Hub usando las credenciales almacenadas en los secretos DOCKER_USERNAME y DOCKER_PASSWORD.

✨️ *Log in to GitHub Container Registry:*

Inicia sesión en GitHub Container Registry utilizando las credenciales del GITHUB_TOKEN.

✨️ *Extract metadata:*

Utiliza la acción docker/metadata-action para extraer las etiquetas y etiquetas adicionales para las imágenes Docker que se construirán, tanto para Docker Hub como para GitHub Container Registry.

✨️ *Build and push Docker images:*

Utiliza la acción docker/build-push-action para construir las imágenes Docker a partir del archivo Dockerfile y las sube a los registros definidos, aplicando las etiquetas y las etiquetas extraídas en el paso anterior.

🔑 Propósito:

Automatizar la construcción y publicación de una imagen Docker en Docker Hub y GitHub Container Registry cuando se actualiza la rama main, usando el archivo Dockerfile del repositorio.

## 5️⃣🟦 **Estado del Proyecto**

    ☑️ Terminado.

## 6️⃣👤 **Colaboración**

Este proyecto es de uso personal y no está abierto a colaboraciones externas.  
Sin embargo, si encuentras algo interesante o tienes alguna pregunta, ¡estaré encantado de escuchar! Puedes contactarme en mi perfil de Github.

## 7️⃣🟪 **Licencia**

Este proyecto no tiene licencia asignada. Al no contar con una licencia explícita, se considera que todos los derechos están reservados. Si deseas usar este proyecto, por favor, contáctame.

## 8️⃣🟫 **Autores**

- Pascua2020 (https://github.com/Pascua2020)
- UTN

## 9️⃣📒**Documentación Oficial:**

*Docker:*
https://docs.docker.com

*Github Actions:*
https://docs.github.com/es/actions

*Dokku:*
https://dokku.com/docs/getting-started/installation/

## 🔟🔄 **Notas**

🍪 *Consideraciones de seguridad*

- Este proyecto utiliza variables secretas (DOCKER_USERNAME, DOCKER_PASSWORD, GITHUB_TOKEN).

- Asegúrate de configurar los secretos en la sección "Settings > Secrets and Variables > Actions" de tu repositorio.

🍪 *Límites del proyecto*

- Este proyecto no incluye configuraciones avanzadas de orquestación como Kubernetes.

- Está diseñado para despliegues simples en entornos compatibles con Docker.

🍪 *Notas adicionales*

- Este proyecto es un ejemplo educativo.

- No se recomienda utilizarlo en entornos de producción sin realizar ajustes específicos.