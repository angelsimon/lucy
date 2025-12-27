---
title: "Markdown: ejemplos rápidos"
date: 2025-01-03 10:00:00 -0300
categories: [Guías]
tags: [markdown, codigo, tipografia]
excerpt: "Una entrada de ejemplo con títulos, listas, tablas, citas y bloques de código."
---

Esta entrada sirve como demostración de los estilos visuales definidos en el archivo `styles.css`. A continuación repasaremos la tipografía básica, la jerarquía de títulos y cómo se renderizan los bloques de código y las tablas.

## Títulos y Jerarquía (H2)

El título principal de la entrada utiliza la etiqueta `H1` y se renderiza automáticamente a través del layout. Dentro del contenido, utilizamos `H2` para las secciones principales. Tu CSS define la fuente de los títulos como **IBM Plex Sans**.

### Subtítulo de nivel 3 (H3)

Para subdivisiones dentro de una sección, utilizamos el `H3`.

#### Subtítulo de nivel 4 (H4)

Aunque es menos común, el estilo también soporta niveles más profundos si la estructura del documento lo requiere.

## Formato de Texto

El cuerpo del texto utiliza la fuente **Noto Sans**. Aquí tienes ejemplos de estilos de línea:

* Podemos resaltar texto en **negrita** para dar énfasis fuerte.
* Utilizamos la *cursiva* para énfasis sutil o terminología.
* También es posible combinar **ambos estilos si es _necesario_**.
* El código en línea se ve así: `const variable = true;`. Este estilo utiliza la fuente **Cascadia Mono** y toma el color de fondo del header según tu configuración.

> "Esto es una cita en bloque (blockquote). Es útil para destacar fragmentos importantes o citas textuales. En tu diseño, esto hereda el estilo de párrafo pero suele tener márgenes distintos."

## Listas y Tablas

El diseño soporta listas desordenadas y ordenadas, así como tablas con bordes personalizados definidos en las variables de color.

| Variable CSS | Propósito | Ejemplo (Light Mode) |
| :--- | :--- | :--- |
| `--primary-color` | Color principal de acento | `#111111` |
| `--link-color` | Enlaces y elementos interactivos | `#ee6e73` |
| `--font-color` | Color base del texto | `#333333` |

## Bloques de Código

## Explicación de las Variables CSS

Tu archivo de estilos es muy modular gracias al uso de **CSS Custom Properties** (Variables). Esto te permite manejar tres temas distintos: **Light**, **Dark** y **Gameboy**.

### 1. Configuración Base (`:root`)
Aquí defines las propiedades que no cambian entre temas, principalmente tamaños de fuente y familias tipográficas.

{% highlight css %}
:root {
    /* Tamaños de encabezados */
    --h1-size: 1.75rem;
    --h2-size: 1.5rem;
    
    /* Tipografías */
    --title-font: 'IBM Plex Sans', source-sans;
    --body-font: 'Noto Sans', sans-serif;
    --monospace-font: 'Cascadia Mono', monospace;
}
{% endhighlight %}

### 2. Temas de Color
Los colores se redefinen según el atributo `data-theme`. Por ejemplo, el tema "Gameboy" utiliza una paleta nostálgica de verdes:

{% highlight css %}
[data-theme="gameboy"] {
    --body-background-color: #DDE7C7; /* Verde pantalla clásico */
    --font-color: #0F380F;            /* Verde oscuro casi negro */
    --header-font-color: #9BBC0F;     /* Verde medio */
    --link-color: #306230; 
}
{% endhighlight %}

Esto permite que, al cambiar una clase en el `<html>` o `<body>` mediante JavaScript, todo el sitio cambie de apariencia instantáneamente sin necesidad de cargar nuevas hojas de estilo.