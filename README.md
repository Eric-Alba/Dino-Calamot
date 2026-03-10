# 🦖 Dino Docker Run - Calamot Edition

¡Bienvenido a **Dino Docker Run**! Este es un clon del famoso juego del dinosaurio de Google, diseñado para ejecutarse en entornos **Docker**. El proyecto incluye un sistema de registro de usuarios, inicio de sesión y un ranking global de puntuaciones que persiste en una base de datos.

## 🚀 Cómo desplegar el juego

No necesitas descargar el código fuente para jugar, ya que la imagen está publicada en **Docker Hub**. Solo sigue estos pasos:

### 1. Requisitos
* Tener instalado [Docker Hub (naipeer/dino-calamot)](https://hub.docker.com/r/naipeer/dino-calamot) en Windows, Mac o Linux.

### 2. Configuración
Crea un archivo llamado `docker-compose.yml` en cualquier carpeta de tu ordenador y pega el siguiente código:

```yaml
services:
  # Base de Datos (MariaDB)
  db:
    image: mariadb:10.11
    container_name: juego_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: juego_dino
    volumes:
      - db_data:/var/lib/mysql

  # Aplicación Web (PHP + JavaScript)
  web:
    image: naipeer/dino-calamot:v1
    container_name: juego_app
    ports:
      - "8080:80"
    depends_on:
      - db

volumes:
  db_data:

```

### 3. Ejecución

Abre una terminal (PowerShell o CMD en Windows) en esa carpeta y ejecuta:

```bash
docker-compose up -d

```

### 4. Acceso

Una vez levantado, abre tu navegador y entra en:
👉 **http://localhost:8080**

---

## 🛠️ Características técnicas

* **Imagen Web**: Basada en PHP 8.2 Apache, alojada en [Docker Hub (naipeer/dino-calamot)](https://hub.docker.com/r/naipeer/dino-calamot).
* **Base de Datos**: MariaDB 10.11 con persistencia de datos mediante volúmenes.
* **Sistema de Usuarios**: Registro seguro con hashing de contraseñas y guardado de récords personales.
* **Lógica del Juego**: Desarrollada en JavaScript puro utilizando el elemento `<canvas>`.

---

## 📝 Notas de uso

* **Persistencia**: Gracias al volumen `db_data`, si detienes o borras el contenedor, los usuarios y sus récords **no se perderán**.
* **Arranque inicial**: MariaDB puede tardar unos segundos en inicializarse la primera vez. Si ves un error de conexión al entrar, espera 10 segundos y pulsa **F5**.

---

## 👤 Autor

Proyecto creado por **naipeer**.
IES El Calamot.

