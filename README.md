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
- Dejo 3-5 pantallazos en `material/` y listo. Después de una tanda así el
  profe me va a decir que cortemos (`/cambio`): las imágenes ya explicadas
  no tienen por qué seguir pesando en el contexto el resto del día.

Cuando termina de explicar, Claude mueve solo la tanda a
`material/visto/`. Yo no muevo nada.

# ============================================================
# CÓMO ES UNA SESIÓN, PASO A PASO (como si no supiera nada)
# ============================================================

Dos palabras que uso todo el tiempo, y no son lo mismo:

- **SESIÓN** = una conversación con Claude, de punta a punta. Empieza cuando
  escribo `claude` en la terminal y termina cuando aprieto `Ctrl+D`.
- **TANDA** = el pedazo de material que le paso de una vez.

**En una sesión puede entrar más de una tanda.** Cuántas, no lo calculo yo:
me lo dice el profe (ver "quién decide qué", más abajo).

### PASO 1 — preparo el material `[TERMINAL]`

```
cd ~/Proyectos/{{NOMBRE-CARPETA}}
```

Y dejo la tanda en `material/`: el texto copiado en un `.md`, o los
pantallazos si no se puede copiar. (Cómo armarla: la sección "Cómo armar una
tanda".)

Si hoy no vengo a ver material nuevo —vengo a entregar una práctica, a hacer
un repaso o a que me tome examen— este paso no va: `material/` queda vacía y
listo.

### PASO 2 — abro la sesión `[TERMINAL]`

```
claude
```

Al abrir, el profe hace `git pull` solo. No tengo que hacer nada.

### PASO 3 — `/arranque` `[CLAUDE]`

**Siempre es el primer comando, sin excepción.** Me responde en menos de 10
líneas: dónde quedamos, qué prácticas tengo pendientes, qué repasos
vencieron y qué toca hoy. Y termina con un bloque así:

```
▶ SIGUE: explicar las páginas 70-78 (tanda de texto, 8 páginas)
  1. /rename {{PREFIJO}}-s08
  2. /tanda
```

Si quiero otra cosa, se lo digo de una: `/arranque vengo a entregar la 3`.

(La primera vez de todas, en vez de `/arranque` va `/setup`: se corre una
sola vez en la vida del proyecto.)

### PASO 4 — le pongo nombre a la sesión `[CLAUDE]`

Copio el `/rename` que me dio y lo pego. Eso es todo lo que hace: le pone
nombre a esta conversación para poder retomarla con `claude --resume` si se
cierra la terminal. **El número no lo invento yo ni lo cuento**: sale de la
guía y me lo pasa el profe ya escrito.

### PASO 5 — entrego lo que traigo hecho `[CLAUDE]`

Si terminé una práctica, va **antes** que el material nuevo: el prompt ya
relleno está al final del archivo de arranque, lo copio de ahí.

```
/entrega la práctica 3 está en ejercicios/p03, la probé y funciona
```

Si toca un repaso vencido, `/repaso`. Si el profe me propuso examen,
`/examen`.

### PASO 6 — `/tanda` `[CLAUDE]`

Me explica el material pieza por pieza, anunciando cuál va ("PÁGINA 70:")
para que lo siga con la vista. Cuando termina, deja todo guardado solo:
guía, frases de tipeo, tarjetas de Anki, y mueve el material a
`material/visto/`.

**Puedo interrumpirlo cuando quiera.** Si algo no se entendió, lo digo y lo
explica de nuevo de otra forma, las veces que haga falta. Eso no "gasta" la
sesión: es exactamente para lo que está.

### PASO 7 — el profe decide qué sigue `[CLAUDE]`

Acá no decido yo. Al terminar la tanda me dice una de estas tres, con el
motivo en una línea:

| Me dice | Qué hago |
| --- | --- |
| "seguimos con otra tanda" | armo la próxima en `material/` y otro `/tanda` |
| "conviene cortar acá" | `/cambio` → `Ctrl+D` → `claude` → el `/rename` que me dio |
| "cerremos el día" | `/cierre` |

**`/cambio` no es lo mismo que `/cierre`.** `/cambio` es "sigo estudiando
hoy, pero en una conversación limpia": guarda todo, sube a git y me da el
nombre de la sesión siguiente. `/cierre` es "terminé por hoy".

### PASO 8 — cierro `[CLAUDE]` + `[TERMINAL]`

```
/cierre
```

Verifica que quedó todo guardado, archiva lo cerrado, me muestra qué cambió
en git y me pide el OK para subirlo. Después, `Ctrl+D` y listo.

**Nunca me voy sin `/cierre`.** Es lo que guarda el día y lo sube: sin eso,
mañana (o el otro PC) no se entera de nada.

# ============================================================
# QUIÉN DECIDE QUÉ (para no tener que acordarme de nada)
# ============================================================

| Decisión | Quién |
| --- | --- |
| Qué material entra hoy | **yo** |
| Si la tanda es muy grande | el profe me avisa |
| **Cuándo cortar la sesión** | **el profe** — me lo dice con el motivo |
| Cómo se llama cada sesión | el profe (sale de la guía) |
| **Cuándo tomar examen** | **el profe lo propone**, yo digo sí o no |
| Cuándo toca un repaso | el profe (las fechas están agendadas) |
| Qué pendiente se da de baja | yo, con la propuesta del profe (`/pendientes`) |
| Resolver las prácticas | **yo, siempre** |
| Todo lo de git | el profe (`pull` al abrir, `commit` + `push` al cerrar) |

Si en algún momento no sé qué sigue, la pregunta es literal: **"¿qué sigue?"**
El profe siempre tiene que poder contestarla con un bloque `▶ SIGUE`.

### Cuándo me va a proponer un examen

No tengo que acordarme: me lo propone él, en una línea, cuando pasa alguna de
estas. Si digo que no, no insiste.

- Sumé 3 conceptos nuevos a la lista de dominados.
- Cerré una unidad del material.
- Se graduó una práctica (pasó su tercer repaso).
- Pasaron ~2 semanas sin ningún examen.
- Contesté algo con la palabra correcta pero sonó recitado.

El examen va **al principio** de una sesión, nunca al final de una cargada:
ahí el que rinde mal es el contexto, no yo.

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
3. Tamaño de tanda según formato (tabla de arriba). Es un techo, no una
   cuota: si me paso, el profe me avisa.
4. NUNCA salir sin `/cierre`: es lo que guarda el día y lo sube.
5. **Cuándo cortar lo dice el profe**, yo no lo calculo. Cuando lo dice:
   `/cambio` primero, nunca `Ctrl+D` pelado — sin eso la tanda no queda
   registrada en la guía y se pierde. Y si noto que empieza a olvidar
   cosas dichas antes o se pone lento, se lo digo: esa es la señal de
   contexto saturado y se corta igual.
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
