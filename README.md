# PLANTILLA PROFESOR — aprender {{TEMA}} con Claude Code

Sistema de estudio con Claude Code como profesor particular: yo le paso
el material por tandas (texto de un libro, pantallazos, docs...), él lo
explica en español, mantiene la guía (`GUIA.md`), lleva las prácticas
con repetición espaciada (`EJERCICIOS.md`) y el plan por fases hacia mi
objetivo (`RUTA.md`). **Yo hago TODA la práctica a mano.**

No hay mensajes que copiar y pegar: **cada cosa es un comando**, y el
profe me dice cuál sigue. Tampoco escribo comandos de git: los hace él.

¿Primera vez en la vida con git/GitHub/SSH, o vas a enlazar otro PC?
→ Leé `INSTALACION.md`: ahí está TODO explicado desde cero.

## Los dos lugares donde se escriben cosas

- `[TERMINAL]` = la consola de siempre
- `[CLAUDE]` = dentro del programa, después de escribir `claude`

## El mapa en 30 segundos

```
{{NOMBRE-CARPETA}}/
├── material/        acá dejo la tanda de hoy (NO va a git: copyright)
│   └── visto/       lo ya explicado — lo archiva Claude solo
├── ejercicios/      mis prácticas. Claude deja el ENUNCIADO + el
│   │                prompt de entrega; la solución la escribo yo
│   └── repasos/     los repasos, siempre desde cero
├── ToDo/            checklists: qué verificar antes de dar algo por
│                    terminado (los mantiene Claude)
├── GUIA.md        ★ lo que ENTENDÍ, sesión a sesión
├── EJERCICIOS.md  ★ SOLO lo vivo: pendientes, repasos y conceptos
│                    dominados. Se lee entero cada sesión: va corto
├── PENDIENTES.md    la deuda que NO es una práctica: material que no
│                    llegó y contenido diferido. Lo triagea
│                    /pendientes, no se lee al empezar
├── RUTA.md          el plan por fases hasta mi objetivo
├── MECANOGRAFIA.md  frases de tipeo de cada sesión (ttyper)
├── ANKI.txt         tarjetas de repaso 80/20 para importar en Anki
├── CLAUDE.md        las reglas del profe
└── .claude/          los comandos (commands/) y los dos automatismos
                      (hooks/): pull al abrir, y el candado
```

**Los dos automatismos que corren solos:**
- al abrir cualquier sesión se hace `git pull`, aunque me olvide de
  `/arranque`;
- Claude tiene **prohibido por el harness** editar o pisar cualquier archivo
  que ya exista en las carpetas de trabajo. Solo puede CREAR el archivo de
  arranque. Si algún día necesito desactivarlo: `/hooks`.

Archivos que crecen aparte y NO se leen al empezar:
`GUIA-ARCHIVO.md` (sesiones viejas) y `EJERCICIOS-ARCHIVO.md`
(prácticas completadas con su corrección).

# ============================================================
# EL ÚNICO FLUJO QUE TENGO QUE SABER
# ============================================================

Da igual si vengo a estudiar material nuevo, a entregar una práctica o
a hacer un repaso. **Siempre es lo mismo:**

```
[TERMINAL]  cd ~/Proyectos/{{NOMBRE-CARPETA}}
[TERMINAL]  armo la tanda en material/  (ver "Cómo armar una tanda")
[TERMINAL]  claude
[CLAUDE]    /arranque
```

Y ya está. El profe hace `git pull`, mira dónde quedamos, qué prácticas
tengo pendientes y qué repasos vencieron, y me dice en menos de 10
líneas qué toca hoy. Termina siempre con un bloque así:

```
▶ SIGUE: explicar las páginas 70-78 (tanda de texto, 8 páginas)
  1. /rename java-s08     ← el nombre de ESTA sesión
  2. /tanda
```

Copio eso y sigo. **No tengo que acordarme de ningún número, ningún
nombre ni ningún mensaje.** Si el bloque no aparece, lo pido: "¿qué
sigue?".

Si quiero forzar algo distinto a lo que detectó, se lo digo de una:
`/arranque vengo a entregar la práctica 3`.

**La primera vez de todas** (proyecto recién creado desde la
plantilla): en vez de `/arranque`, va `/setup` con mis datos — tema,
material, formato, idioma, nivel de partida, objetivo final y prefijo
de sesiones. Se corre UNA sola vez en la vida del proyecto.

# ============================================================
# LOS COMANDOS
# ============================================================

Los prompts completos viven en `.claude/commands/`.

| Comando | Para qué | Cuándo lo uso |
| --- | --- | --- |
| `/arranque` | dónde quedamos, cómo se llama esta sesión y qué toca hoy | **siempre, primero** |
| `/tanda` | me explica el material que dejé en `material/` | por cada tanda |
| `/entrega` | corrige la práctica que terminé | cuando termino una |
| `/repaso` | repaso vencido, desde cero | cuando el profe avisa |
| `/pendientes` | triage: qué se pudre, qué se salda, qué doy de baja | domingo, 5 minutos |
| `/examen` | me toma examen en frío, sin material al lado | cuando quiera probarme |
| `/cambio` | cierra esta sesión y abre una limpia | mitad del día |
| `/cierre` | guarda todo y sube a git | antes de salir, siempre |
| `/setup` | configura el proyecto | una sola vez |

Todos aceptan contexto extra: `/tanda son 4 pantallazos del capítulo 5`,
`/entrega la práctica 3 está en ejercicios/p03.java, compila y corre bien`.

El prompt de `/entrega` ya relleno está **al final de cada archivo de
arranque**: lo copio de ahí, es más rápido.

# ============================================================
# CÓMO ARMAR UNA TANDA (esto define si la sesión vuela o se arrastra)
# ============================================================

Una tanda es el pedazo de material que le paso a Claude de una vez.
Lo que hace lenta y cara una sesión es el material acumulado en el
contexto: TODO lo que le pasé antes se le vuelve a enviar en cada
respuesta. Por eso el tamaño de la tanda depende del FORMATO.

REGLA MADRE: si el material tiene texto que puedo seleccionar y
copiar, va como TEXTO. Un pantallazo cuesta 3 o 4 veces más que la
misma página en texto, y encima Claude lo lee con menos precisión.

| Formato del material           | Tanda        | Tandas por sesión |
| ------------------------------ | ------------ | ----------------- |
| TEXTO (copiado a material/)    | 6-10 páginas | 2-3               |
| TEXTO denso o con mucho código | 5-8 páginas  | 2                 |
| IMÁGENES (pantallazos)         | 3-5 imágenes | 1                 |
| MIXTA (aunque sea 1 imagen)    | como imágenes| 1                 |

Cómo paso una tanda de TEXTO (lo más barato y lo preferido):
- Copio el texto del libro/curso y lo pego en un archivo nuevo:
  `material/tanda.md` (o `tanda-01.md`, `tanda-02.md`...).
- Le pongo marcas de dónde viene, para que Claude pueda anunciarlas:
  una línea `## PÁGINA 70` (o Ubicación, minuto, sección) antes de
  cada pedazo. Con eso puedo seguir el material con la vista.
- Si una figura o tabla NO se puede copiar como texto, agrego ESE
  pantallazo suelto y el resto va en texto. Eso ya hace la tanda
  mixta: una sola tanda en esa sesión.

Cómo paso una tanda de IMÁGENES (solo cuando no hay texto):
- Dejo 3-5 pantallazos en `material/` y listo. Después de esa tanda,
  `/cambio`: las imágenes ya explicadas no tienen por qué seguir
  pesando en el contexto el resto del día.

Cuando termina de explicar, Claude mueve solo la tanda a
`material/visto/`. Yo no muevo nada.

# ============================================================
# UN DÍA DE ESTUDIO, ENTERO
# ============================================================

```
[TERMINAL]  cd ~/Proyectos/{{NOMBRE-CARPETA}}
[TERMINAL]  armo la tanda en material/
[TERMINAL]  claude
[CLAUDE]    /arranque          → me dice el /rename y qué toca
[CLAUDE]    /rename {{PREFIJO}}-sNN
[CLAUDE]    /entrega ...       → si traigo algo hecho, PRIMERO esto
[CLAUDE]    /tanda             → me explica el material
            ¿sigo? tanda de TEXTO → armo otra en material/ y /tanda
                   tanda de IMÁGENES → /cambio, Ctrl+D, sesión nueva
[CLAUDE]    /cierre            → guarda todo, commitea y pushea
[TERMINAL]  Ctrl+D
```

Todo lo de git lo hace el profe: `pull` al abrir, y `commit` + `push`
al cerrar (me muestra qué cambió y me pide el OK antes de subir).

# ============================================================
# SI SE CERRÓ LA TERMINAL SIN QUERER (mismo día)
# ============================================================

`[TERMINAL]` `claude --resume {{PREFIJO}}-sNN`
Solo para retomar el MISMO día. Día nuevo = sesión nueva.

# ============================================================
# REGLAS DE ORO
# ============================================================

1. `/arranque` siempre primero. De ahí sale el nombre de la sesión y
   todo lo demás.
2. Si el material se puede copiar como texto, va como texto. Siempre.
3. Tamaño de tanda según formato (tabla de arriba). Nunca más de 5
   pantallazos ni más de 10 páginas de texto por tanda.
4. NUNCA salir sin `/cierre`: es lo que guarda el día y lo sube.
5. Al cambiar de sesión a mitad del día, `/cambio` primero: sin eso la
   tanda no queda registrada en la guía y se pierde.
6. Los ejercicios que trae el propio material SIEMPRE los intento a
   mano ANTES de mirar la solución o pedírsela a Claude.
7. Los repasos se hacen DESDE CERO, sin mirar mi versión original.
8. `material/` NUNCA va a git (copyright; ya está en `.gitignore`).
   El profe lo verifica antes de cada commit.
9. El número de sesión solo avanza. Varias sesiones en un día es lo
   NORMAL: cada tanda de imágenes abre una nueva.

# ============================================================
# MECANOGRAFÍA Y TARJETAS ANKI
# ============================================================

Mecanografía (las frases salen de `MECANOGRAFIA.md`):
- CTRL+SUPER+ALT+T (atajo de mis dotfiles) abre/oculta ttyper flotante
  con una frase al azar de mis proyectos de estudio.
- Al terminar una frase: `q` pasa a otra al azar, `r` repite la misma.
  Cada frase vive en su propio archivo de ttyper; Claude solo agrega
  los archivos nuevos al cerrar cada tanda. Yo no los toco.

Tarjetas Anki (`ANKI.txt`):
- En Anki: Archivo → Importar → elegir el `ANKI.txt` de este repo. El
  mazo, el separador tab y las etiquetas ya vienen preconfigurados en
  las cabeceras del propio archivo.
- Re-importar el MISMO archivo no duplica: actualiza las tarjetas que
  cambiaron y agrega las nuevas (Anki matchea por la pregunta).
- Rutina: después de cada `git pull` con tarjetas nuevas, re-importo.
