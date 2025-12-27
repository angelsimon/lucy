---
title: "Montar Jekyll en un entorno local para probar el tema Lucy"
date: 2025-01-02 10:00:00 -0300
categories: [Jekyll, Docker]
tags: [lucy, docker, docker-compose, jekyll, livereload]
excerpt: "Qué hace el docker-compose.yml de Lucy y cómo usarlo para desarrollo local con LiveReload."
---

Configurar un entorno de desarrollo para Jekyll a veces puede ser complicado debido a las versiones de Ruby y las dependencias del sistema (gemas). Para el tema **Lucy** se puede simplificar este proceso utilizando **Docker Compose**.

Esto permite levantar el blog con un solo comando sin instalar nada extra en nuestra máquina local más que Docker.

## Análisis del docker-compose.yml

El archivo de configuración que utilizamos está diseñado para desarrollo activo. 

{% highlight yaml %}
version: '3.8'

services:
  jekyll:
    # Usamos 'latest' para asegurar compatibilidad con Ruby 3.x
    image: jekyll/jekyll:latest 
    
    container_name: jekyll_blog_container
    command: jekyll serve --livereload --force_polling
    ports:
      - "4000:4000"   # Puerto del servidor web
      - "35729:35729" # Puerto para LiveReload
    volumes:
      - .:/srv/jekyll
      # Mantenemos esto para evitar conflictos de _site
      - jekyll_site:/srv/jekyll/_site
    environment:
      - JEKYLL_ENV=development

volumes:
  jekyll_site:
{% endhighlight %}

### Puntos clave de esta configuración

1.  **Imagen Base (`jekyll/jekyll:latest`)**: 
    Utilizamos la última versión oficial. Esto es crucial porque el tema Lucy aprovecha características modernas que requieren **Ruby 3.x**. Al usar Docker, evitamos conflictos con versiones antiguas de Ruby que puedas tener instaladas en tu macOS o Linux.

2.  **Comandos de Ejecución**:
    * `jekyll serve`: Inicia el servidor local.
    * `--livereload`: Permite que el navegador refresque la página automáticamente cuando guardas un cambio en un archivo Markdown o CSS.
    * `--force_polling`: A veces, en sistemas Windows o ciertos montajes de Docker, el sistema de archivos no notifica los cambios al contenedor. Esta bandera fuerza a Jekyll a buscar cambios activamente.

3.  **Volúmenes y la carpeta `_site`**:
       
    ```yaml
    volumes:
      - .:/srv/jekyll
      - jekyll_site:/srv/jekyll/_site
    ```

    La primera línea mapea tu carpeta actual al contenedor. La segunda le dice a Docker que guarde la carpeta generada `_site` en un volumen interno de Docker, no en tu disco local. Esto mejora el rendimiento y evita problemas de permisos donde el contenedor crea archivos que luego tú no puedes borrar desde el explorador de archivos.

## Cómo ponerlo en marcha

Una vez que has clonado el repositorio del tema Lucy, solo necesitas dos comandos en tu terminal.

### 1. Iniciar el servidor

Ejecuta el siguiente comando en la raíz del proyecto:

{% highlight bash %}
docker-compose up
{% endhighlight %}

La primera vez tardará unos minutos en descargar la imagen y las gemas. Una vez veas el mensaje `Server address: http://0.0.0.0:4000/`, tu blog estará disponible en tu navegador.

### 2. Detener el servidor

Para apagar el contenedor limpiamente, usa:

{% highlight bash %}
docker-compose down
{% endhighlight %}


Con este entorno, puedes centrarte en escribir contenido y modificar el diseño en `styles.css` sin preocuparte por la infraestructura.