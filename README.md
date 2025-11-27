# Twitch-Categorias
Imagenes de Categorias que se actualizan todos los dias (No tenemos todas las categorias pero puedes pedirla en Issues)


## Uso de la API de Categorías de Twitch

Este proyecto es un archivo `.json` con las imágenes de portada de las categorías de Twitch. Puedes utilizarlo de varias formas, por ejemplo:

- En una **página web**, para mostrar las imágenes de las categorías de Twitch en tiempo real.  
- En un **bot de Discord**, para enviar notificaciones sobre transmisiones y usar la imagen más reciente de una categoría como `setThumbnail`.  

El archivo JSON se actualiza automáticamente y está disponible públicamente en:
[https://njmd13.github.io/Twitch-Categorias/categorias-ttv.json](https://njmd13.github.io/Twitch-Categorias/categorias-ttv.json)

Como es un archivo JSON, puedes acceder a los datos usando la **clave** de la categoría y obtener el valor de la imagen directamente.

### Ejemplo de contenido:

```json
{
  "Minecraft": "https://static-cdn.jtvnw.net/ttv-boxart/27471_IGDB-285x380.jpg",
  "Battlefield REDSEC": "https://static-cdn.jtvnw.net/ttv-boxart/1848745913_IGDB-285x380.jpg"
}
```
- **Clave:** el nombre de la categoría de Twitch.
- **Valor:** la URL de la imagen de portada correspondiente.


## Ejemplos de Integración

### 1. Usando en un Bot de Discord

Puedes usar la API para mostrar la imagen de la categoría en un embed de Discord.  
Ejemplo usando `discord.js`:

```javascript
const fetch = require("node-fetch");
const Discord = require("discord.js");
const client = new Discord.Client({ intents: ["GUILDS", "GUILD_MESSAGES"] });

client.on("messageCreate", async (message) => {
  if (message.content === "!categoria minecraft") {
    // Obtener JSON desde GitHub
    const res = await fetch("https://njmd13.github.io/Twitch-Categorias/categorias-ttv.json");
    const categorias = await res.json();

    const imagen = categorias["Minecraft"];
    if (imagen) {
      const embed = new Discord.MessageEmbed()
        .setTitle("Minecraft")
        .setImage(imagen)
        .setColor("#9146FF");

      message.channel.send({ embeds: [embed] });
    } else {
      message.channel.send("No se encontró la categoría.");
    }
  }
});

client.login("TU_TOKEN_DE_DISCORD");
```


### 2. Usando en una Página Web

Puedes mostrar las imágenes de las categorías directamente en tu página con JavaScript:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Categorías de Twitch</title>
</head>
<body>
  <div id="categorias"></div>

  <script>
    async function mostrarCategorias() {
      const res = await fetch("https://njmd13.github.io/Twitch-Categorias/categorias-ttv.json");
      const categorias = await res.json();

      const container = document.getElementById("categorias");
      for (const [nombre, imagen] of Object.entries(categorias)) {
        const div = document.createElement("div");
        div.innerHTML = `
          <h3>${nombre}</h3>
          <img src="${imagen}" alt="${nombre}" style="width: 200px;">
        `;
        container.appendChild(div);
      }
    }

    mostrarCategorias();
  </script>
</body>
</html>
```


## Uso en Otros Proyectos

Puedes utilizarlo en **cualquier proyecto** que permita:

- Obtener datos desde un **enlace HTTP/HTTPS**.
- Leer o cargar archivos **.json**.

Por ejemplo, puedes usarlo en:

- Aplicaciones web o móviles.
- Bots de Discord o Telegram.
- Scripts de automatización.
- Paneles de visualización de datos.
- Cualquier proyecto que necesite mostrar las imágenes de las categorías de Twitch en tiempo real.

Solo necesitas añadir el enlace del archivo JSON a tu proyecto, obtener los datos y mostrarlos.
