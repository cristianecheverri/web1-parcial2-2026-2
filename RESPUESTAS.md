# Parcial 2 · Respuestas de razonamiento

Nombre:

Responde debajo de cada pregunta. Se califica la explicación, no solo el resultado. Puedes ejecutar el código para comprobar, pero escribe el porqué con tus palabras: te lo pueden preguntar.

## P1 · ¿En qué orden? (5 pts)

```js
console.log('1');
setTimeout(() => console.log('2'), 0);
const cargar = async () => {
  console.log('3');
  const respuesta = await fetch('https://rickandmortyapi.com/api/episode/1');
  console.log('4');
};
cargar();
console.log('5');
```

¿Qué imprime la consola y en qué orden? Explica por qué el `3` aparece donde aparece y por qué el `5` no espera al `fetch`.

**Respuesta:**


## P2 · Un 404 que no llega al catch (5 pts)

El episodio 9999 no existe: la API responde con código **404** y el cuerpo `{"error":"Episode not found"}`.

```js
try {
  const respuesta = await fetch('https://rickandmortyapi.com/api/episode/9999');
  const datos = await respuesta.json();
  console.log('Episodio:', datos.name);
} catch (error) {
  console.log('Falló:', error.message);
}
```

(a) ¿Qué imprime? (b) ¿Por qué no entra al `catch`? (c) Escribe la línea que falta para que sí entre, y di qué imprimiría entonces.

**Respuesta:**


## P3 · LocalStorage sin JSON (5 pts)

```js
const vistos = [1, 5, 8];
localStorage.setItem('vistos', vistos);
const leido = localStorage.getItem('vistos');
console.log(leido, typeof leido);      // (a)
console.log(leido.length);             // (b)
const recuperado = JSON.parse(leido);  // (c)
```

¿Qué imprimen (a) y (b)? ¿Qué pasa en (c)? Corrige la segunda línea para que `recuperado` sea otra vez un array de tres números, y explica por qué en tu `leerVistos` el `JSON.parse` va dentro de `try/catch`.

**Respuesta:**


## P4 · Botones que dejan de funcionar (5 pts)

Un compañero escribió esto. Al cargar la página, el primer clic en «Marcar como visto» funciona; después de ese clic, o de escribir una letra en el buscador, **ningún botón responde**.

```js
render();
document.querySelectorAll('[data-id]').forEach((boton) => {
  boton.addEventListener('click', () => {
    vistos = alternarId(vistos, Number(boton.dataset.id));
    guardarVistos(vistos);
    render();
  });
});
```

Explica qué les pasó a los botones y reescribe el código con delegación.

**Respuesta:**
