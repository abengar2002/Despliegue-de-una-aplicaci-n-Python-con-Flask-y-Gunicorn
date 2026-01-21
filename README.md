# Despliegue de una aplicación Python con Flask y Gunicorn

**Alumno:** Antonio Benitez Garcia  
**Módulo:** Despliegue de Aplicaciones Web  
**Curso:** 2025-2026

---

## 1. Introducción

En esta práctica se documenta el proceso completo de despliegue de una aplicación web basada en Python (Flask) sobre una máquina virtual Debian. El objetivo es configurar un entorno de producción profesional utilizando **Gunicorn** como servidor de aplicaciones WSGI y **Nginx** como proxy inverso, finalizando con un despliegue real desde un repositorio de GitHub.

---

## 2. Preparación del Entorno

### Instalación de Paquetes
El primer paso es la actualización de repositorios y la instalación de las herramientas necesarias: Nginx, Gunicorn, Pipenv y Git, así como el entorno de Python.

![Instalación de paquetes completos](img/installtodo.png)
![Instalación de herramientas Python](img/install-python.png)

Verificamos las versiones para asegurar que el sistema está listo:

![Versión de Nginx](img/version-ngnic.png)
![Versiones de Pipenv y Gunicorn](img/version-pipenv-gunicorn.png)

### Configuración de Directorios y Permisos
Creamos el directorio de la aplicación y ajustamos los permisos para el usuario `vagrant` y el grupo `www-data`.

![Creación de carpetas y permisos](img/sudo-cambos.png)

---

## 3. Configuración del Entorno Virtual

### Inicialización y Dependencias
Dentro del directorio del proyecto, instalamos las dependencias (`flask` y `gunicorn`) y activamos el entorno virtual.

![Instalación con Pipenv](img/pipenv-install.png)
![Activación del entorno virtual](img/pipenv-shell-activado.png)

---

## 4. Creación de la Aplicación y Archivos de Configuración

Creamos y editamos los archivos esenciales: el archivo de entorno `.env`, la aplicación (`application.py`) y el punto de entrada (`wsgi.py`).

![Configuración del archivo .env](img/cat-.env.png)

**Código de la Aplicación:**

![Código de application.py](img/flask-import.png)

**Punto de Entrada (WSGI):**

![Código de wsgi.py](img/run-nano.png)

### Prueba de Desarrollo
Antes de configurar el servidor de producción, verificamos que la aplicación arranca correctamente en modo desarrollo.

![Prueba de arranque Flask 0.0.0.0](img/flask-run-0.0.0.0.png)

---

## 5. Configuración de Gunicorn (Servidor de Aplicaciones)

Comprobamos que Gunicorn funciona manualmente y localizamos su ruta de instalación dentro del entorno virtual.

![Ejecución manual de Gunicorn](img/flask-gunicorn.png)
![Logs de los workers de Gunicorn](img/gunicon-workers.png)
![Ruta del ejecutable Gunicorn](img/which–gunicorn.png)

### Automatización con Systemd
Creamos un servicio del sistema para que la aplicación se ejecute automáticamente en segundo plano.

![Edición del servicio systemd](img/flask-app.service-nano.png)
![Variables de entorno en el servicio](img/nano-info.png)

---

## 6. Configuración de Nginx (Proxy Inverso)

Configuramos Nginx para redirigir el tráfico del puerto 80 al socket de nuestra aplicación Flask.

![Edición del archivo de configuración de sitio](img/app-primera-nano.png)

Reiniciamos el servicio y comprobamos su estado:

![Estado del servicio Nginx](img/nginx.png)

### Comprobación del Despliegue Manual
Accedemos desde el navegador para verificar que la aplicación "Hola Mundo" se ha desplegado correctamente.

![Navegador mostrando App desplegada](img/app-desplegada.png)

---

## 7. Despliegue Final: Repositorio GitHub

Como tarea de ampliación, realizamos el despliegue de una aplicación real clonada desde un repositorio externo ("msdocs-python-flask-webapp-quickstart").

### Clonado y Dependencias
Clonamos el repositorio y preparamos el entorno.

![Clonado del repositorio git](img/cosas-app-git.png)
![Listado de archivos de la nueva app](img/cosas-app.png)

### Resultado Final
Tras reconfigurar los servicios para apuntar a la nueva carpeta, la aplicación de Microsoft Azure carga correctamente, mostrando la pantalla de bienvenida y el funcionamiento tras el login.

![Pantalla de bienvenida Azure](img/app.png)
![Aplicación funcionando correctamente](img/app-funciona.png)
