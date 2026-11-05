# Sopa de letras interactiva

Sopa de letras para el móvil y el ordenador con **temas de España**: comunidades, ciudades, comida, fiestas y tradiciones, monumentos, naturaleza, animales, deportes y arte y cultura.

- **50 niveles por tema.** Cada nivel tiene la cuadrícula más grande, más palabras, más direcciones (también al revés y en diagonal), letras trampa y menos pistas.
- **Puntos** por cada palabra y un **premio extra** al terminar cada nivel. Cuanto más alto es el nivel, más puntos.
- **Se juega con el dedo**: desliza desde la primera letra hasta la última, o toca la primera y luego la última.
- **Puntos online con código de jugador** (por ejemplo `SL-7K3Q-9XPA`): sirve para recuperar el progreso en cualquier dispositivo y salir en la **clasificación**.
- Opciones del jugador: cambiar el nombre (2 veces como máximo), generar un código nuevo y borrar el jugador.
- **Copia de seguridad**: en *Opciones del jugador*, «Guardar copia de seguridad» descarga un archivo `sopa-progreso-AAAA-MM-DD.json` con los puntos y niveles. Con «Cargar una copia de seguridad» se recupera en otro móvil o en este mismo si se borran los datos del navegador. Sirve también para quien juega sin código.
- **Aviso de versión nueva** para quien tenga el juego abierto cuando se publica una actualización.

## Publicarlo con GitHub Pages

**Settings → Pages → Deploy from a branch → main / (root) → Save.** La web queda en `https://pctecnikk.github.io/sopadeletrasinteractiva/`.

En el móvil, abre el enlace y usa **Añadir a pantalla de inicio** para tenerlo como una app.

## Base de datos (Supabase)

El juego usa un proyecto de Supabase con sus propias tablas (`sl_players` y `sl_presence`).

1. En Supabase, abre **SQL Editor → New query**, pega `supabase.sql` y pulsa **Run**.
2. Pon la URL del proyecto y la clave pública (*publishable*) en `supabase-config.js`.

La URL y la clave pública no son secretas. Las tablas están cerradas: solo se pueden usar a través de las funciones de `supabase.sql`, que guardan el código cifrado y en la clasificación solo muestran el nombre de jugador y los puntos.

### Ver quién está jugando ahora (solo tú)

Supabase → **Table Editor** → **sopa_jugando_ahora**. Salen las personas que han dado señales en los últimos 2 minutos, con su nombre de jugador y el tema y nivel en que están. Los jugadores no ven nada de esto, y los avisos de más de un día se borran solos.

## Avisar de una versión nueva

La web consulta `version.json` cada minuto. Cada versión nueva es una *release* de GitHub (v1.0.0, v1.1.0…). Si cambias `index.html` a mano, pon el mismo número en `APP_VERSION` (dentro de `index.html`) y en `version.json` (por ejemplo `{"version": "1.1.0"}`) y crea la release `v1.1.0`. Ese número aparece al pie de la pantalla de temas como «Versión 1.1.0», así se ve qué versión está funcionando.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | El juego completo |
| `supabase-config.js` | URL y clave pública de Supabase |
| `supabase.sql` | Script para preparar la base de datos |
| `version.json` | Número de versión (el mismo que `APP_VERSION` y la release) para avisar de actualizaciones |
| `manifest.webmanifest`, `icon-*.png`, `icon.svg` | Nombre e icono al añadirlo a la pantalla de inicio |
