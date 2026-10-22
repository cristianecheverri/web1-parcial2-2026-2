# Parcial 2 · Guía de episodios de Rick and Morty

**Programación para entornos web 1 · 2026-2 · Trabajo práctico individual · Entrega: miércoles 28 de octubre de 2026, antes de las 6:00 p. m. · 20 % de la nota**

Vas a construir una guía de episodios que consume `https://rickandmortyapi.com/api/episode`, un recurso que **no** usamos en clase. Abre esa URL en el navegador antes de escribir código: la respuesta es un objeto con `info` y `results`, y cada episodio de `results` tiene `id`, `name`, `air_date`, `episode` (el código, por ejemplo `S01E01`) y `characters` (un array de URLs).

## Condiciones

- Individual. Sin IA de ningún tipo: Copilot, chats o extensiones. Este repo trae `.vscode/settings.json` con la IA de VS Code desactivada: no lo cambies.
- Puedes consultar MDN, tu propio repositorio del Explorador y el material del curso. Es individual: no compartas ni copies código de compañeros.
- Abre el proyecto con **Live Server** (los módulos no funcionan con doble clic).
- Haz **commit y push al terminar cada requisito** (mensaje: `R1 listo`, `R2 listo`…). Se califica lo que esté en GitHub a la hora límite de entrega.
- El docente puede pedirte que expliques cualquier línea durante 2 minutos. Lo que no puedas explicar no suma.

## Cómo empezar y cómo entregar

1. Abre este repositorio base en GitHub y presiona **Use this template → Create a new repository**.
2. Ponle de nombre `parcial2-web1-<tu-apellido>` y déjalo **Public**.
3. Clona tu repositorio nuevo, ábrelo en VS Code y arráncalo con Live Server.
4. Haz commit y push al terminar cada requisito.
5. Envía el enlace de **tu** repositorio respondiendo el correo del docente, antes del miércoles 28 de octubre a las 6:00 p. m.

No trabajes en el repositorio base ni le hagas fork: crea el tuyo con el botón de plantilla.

## Lo que recibes

| Archivo | Qué tiene |
|---|---|
| `index.html` | La página completa con Tailwind por CDN y, al final, **comentados**, los modelos HTML de la tarjeta y de los estados de carga, error y vacío. No necesitas tocarlo. |
| `js/api.js` | `pedirJSON` y `obtenerEpisodios`, por completar. |
| `js/logica.js` | `filtrarEpisodios`, `contarPersonajes` y `alternarId`, por completar. Funciones puras. |
| `js/vistos.js` | `leerVistos` y `guardarVistos`, por completar. |
| `js/app.js` | Estado, referencias al DOM y las funciones de la interfaz, por completar. |
| `respaldo/episodios.json` | La respuesta real de la API, guardada. Solo se usa si la API no responde (ver el final). |
| `RESPUESTAS.md` | Las cuatro preguntas de razonamiento. Respóndelas ahí mismo. |

No cambies los nombres de las funciones ni de los archivos.

## Requisitos de la parte práctica (80 puntos)

**R1 · API (12 pts).** En `api.js`, `pedirJSON(url)` hace `fetch` con `await`, **lanza un `Error`** con el código HTTP en el mensaje si `respuesta.ok` es falso y, si no, devuelve el JSON. `obtenerEpisodios()` usa `pedirJSON` y devuelve solo el array `results`.

**R2 · Cargando y error (12 pts).** Mientras llegan los datos, `#lista` muestra «Cargando episodios…». Si la petición falla (error HTTP o sin red), muestra el estado de error con el motivo y un botón **Reintentar** que vuelve a pedir los datos.

**R3 · Tarjetas (14 pts).** `render()` pinta una tarjeta por episodio con `map`, un template literal y `join`: código, nombre, fecha de emisión, **cantidad** de personajes y el botón con `data-id`. Si el episodio está en `vistos`, la tarjeta usa la variante «vista» del modelo 2.

**R4 · Filtros (16 pts).** El buscador (evento `input`) filtra por nombre sin importar mayúsculas; el select (evento `change`) filtra por temporada; los dos se combinan. Enter en el buscador **no** recarga la página. Si nada coincide, se ve el estado vacío. La lógica vive en `filtrarEpisodios`, que no toca el DOM.

**R5 · Contador (6 pts).** `#contador` muestra, para lo que está visible, `7 de 20 episodios · 187 personajes` (ese es el resultado de buscar «rick»). El total de personajes se calcula con `reduce` en `contarPersonajes`.

**R6 · Episodios vistos (20 pts).** Un **único** listener en `#lista` (delegación) atiende el botón de cada tarjeta, que marca o desmarca el episodio como visto con `alternarId`, y también el botón Reintentar. Los ids vistos se guardan en LocalStorage con `JSON.stringify` y se leen con `JSON.parse` dentro de `try/catch`. Al recargar la página, los episodios vistos siguen marcados. Si alguien daña el valor guardado a mano en DevTools, la app arranca igual, sin vistos.

## Preguntas de razonamiento (20 puntos)

Están en `RESPUESTAS.md`: cuatro preguntas de 5 puntos. Escribe la respuesta debajo de cada una; se califica la explicación, no solo el resultado.

## Si la API no responde

Si `https://rickandmortyapi.com/api/episode` no carga en el navegador, en `js/api.js` cambia `URL_EPISODIOS` por `'./respaldo/episodios.json'` y sigue trabajando: todo funciona igual y no pierdes puntos. Dilo en el mensaje del commit (por ejemplo, `R1 listo (con respaldo: la API no respondía)`). Antes de entregar, si la API ya responde, vuelve a la URL real.
