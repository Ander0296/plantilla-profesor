# PLANTILLA PROFESOR — aprender {{TEMA}} con Claude Code

Sistema de estudio con Claude Code como profesor particular: yo le
paso el material por tandas (texto de un libro, pantallazos, docs...),
él lo explica en español, mantiene la guía (GUIA.md), lleva las
prácticas con repetición espaciada (EJERCICIOS.md) y el plan por
fases hacia mi objetivo (RUTA.md). Yo hago TODA la práctica a mano.

¿Primera vez en la vida con git/GitHub/SSH, o vas a enlazar otro PC?
→ Leé INSTALACION.md: ahí está TODO explicado desde cero.

## Los dos lugares donde se escriben cosas

- [TERMINAL] = la consola de siempre
- [CLAUDE] = dentro del programa, después de escribir `claude`
Cada paso dice dónde va. Los MENSAJES están al final del archivo.

## Carpetas y archivos

- material/ → acá dejo la tanda actual (ver "Cómo armar una tanda")
- material/visto/ → Claude archiva acá lo ya explicado (lo hace él)
- ejercicios/ → mis prácticas, una carpeta o archivo por práctica.
  Claude crea el ARCHIVO DE ARRANQUE (enunciado + prompt de entrega
  adentro, sin nada de la solución); yo resuelvo ahí mismo
- ejercicios/repasos/ → mis repasos (desde cero, sin mirar el original)
- GUIA.md → la guía activa por sesiones, en formato corto (Claude)
- GUIA-ARCHIVO.md → sesiones viejas archivadas cuando la guía crece
- EJERCICIOS.md → SOLO lo vivo: pendientes, repasos programados y
  conceptos dominados (Claude). Se lee entero cada sesión: va corto
- EJERCICIOS-ARCHIVO.md → prácticas ya completadas con su corrección
  (Claude). No se lee al inicio: solo consulta puntual
- RUTA.md → el plan por fases hasta mi objetivo (lo mantiene Claude)
- MECANOGRAFIA.md → frases de tipeo por sesión (las anota Claude al
  cerrar cada tanda y las vuelca a ttyper; yo practico con
  CTRL+SUPER+ALT+T sin mirar el teclado)
- ANKI.txt → tarjetas de repaso 80/20 (las crea Claude al cerrar
  cada tanda; yo lo importo en Anki — re-importar actualiza y
  agrega, no duplica)
- CLAUDE.md → las reglas del profe (se adaptan al tema con el MENSAJE 0)

## Cómo uso la mecanografía y las tarjetas Anki

Mecanografía (las frases salen de MECANOGRAFIA.md):
- CTRL+SUPER+ALT+T (atajo de mis dotfiles) abre/oculta ttyper
  flotante con una frase al azar de mis proyectos de estudio.
- Al terminar una frase: q pasa a otra al azar, r repite la misma.
  Cada frase vive en su propio archivo de ttyper; Claude solo agrega
  los archivos nuevos al cerrar cada tanda. Yo no los toco.

Tarjetas Anki (ANKI.txt):
- En Anki: Archivo → Importar → elegir el ANKI.txt de este repo. El
  mazo, el separador tab y las etiquetas ya vienen preconfigurados
  en las cabeceras del propio archivo.
- Re-importar el MISMO archivo no duplica: actualiza las tarjetas
  que cambiaron y agrega las nuevas (Anki matchea por la pregunta).
- Rutina: después de cada git pull con tarjetas nuevas, re-importo.

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

| Formato del material         | Tanda        | Tandas por sesión |
| ---------------------------- | ------------ | ----------------- |
| TEXTO (copiado a material/)  | 6-10 páginas | 2-3               |
| TEXTO denso o con mucho código | 5-8 páginas | 2                 |
| IMÁGENES (pantallazos)       | 3-5 imágenes | 1                 |
| MIXTA (aunque sea 1 imagen)  | como imágenes| 1                 |

Cómo paso una tanda de TEXTO (lo más barato y lo preferido):
- Copio el texto del libro/curso y lo pego en un archivo nuevo:
  material/tanda.md (o tanda-01.md, tanda-02.md...).
- Le pongo marcas de dónde viene, para que Claude pueda anunciarlas:
  una línea `## PÁGINA 70` (o Ubicación, minuto, sección) antes de
  cada pedazo. Con eso puedo seguir el material con la vista.
- Si una figura o tabla NO se puede copiar como texto, agrego ESE
  pantallazo suelto y el resto va en texto. Eso ya hace la tanda
  mixta: una sola tanda en esa sesión.

Cómo paso una tanda de IMÁGENES (solo cuando no hay texto):
- Dejo 3-5 pantallazos en material/ y listo. Después de esa tanda
  cambio de sesión (MENSAJE 1): las imágenes ya explicadas no tienen
  por qué seguir pesando en el contexto el resto del día.

# ============================================================
# PRIMERA VEZ CON ESTE TEMA (sesión {{PREFIJO}}-s01)
# ============================================================

0. Creá el repo desde la plantilla y clonalo (INSTALACION.md, PARTE 4).
1. [TERMINAL] cd ~/Proyectos/NOMBRE-DEL-TEMA
2. [TERMINAL] mkdir -p material/visto ejercicios/repasos
3. [TERMINAL] armá la primera tanda en material/ (ver arriba)
4. [TERMINAL] claude
5. [CLAUDE] /rename PREFIJO-s01   (ej: ingles-s01)
6. [CLAUDE] /mcp → engram tiene que decir "connected"
7. [CLAUDE] pegá el MENSAJE 0 CON TUS DATOS RELLENADOS → el profe
   adapta CLAUDE.md y RUTA.md a tu tema y te resume qué decidió
8. [CLAUDE] cuando diga "listo", pegá el MENSAJE 3
   (la primera vez pide permiso para mover/crear archivos → aceptá)
9. ¿Seguís hoy? → según el formato: tanda de texto = otra tanda acá
   mismo; tanda de imágenes = MENSAJE 1 y sesión nueva
10. [CLAUDE] al terminar el día: MENSAJE 5 → salí con Ctrl+D
11. [TERMINAL] engram search "tema de hoy" --project NOMBRE-DEL-TEMA
12. [TERMINAL] git add . && git commit -m "sesión s01" && git push

# ============================================================
# CADA DÍA DE ESTUDIO (s02, s03, ...)
# ============================================================

1. [TERMINAL] cd ~/Proyectos/NOMBRE-DEL-TEMA
2. [TERMINAL] git pull ← lo primero SIEMPRE (clave con más de un PC)
3. [TERMINAL] armá la tanda en material/ (ver "Cómo armar una tanda")
4. [TERMINAL] claude
5. [CLAUDE] /rename PREFIJO-sNN ← el número que sigue
6. [CLAUDE] /mcp → engram "connected"
7. [CLAUDE] pegá el MENSAJE 2 → dónde quedamos, pendientes, repasos
   vencidos y qué toca hoy
8. [CLAUDE] si ya hiciste algo pendiente, entregalo ANTES de material
   nuevo: MENSAJE 4 (práctica) o MENSAJE 6 (repaso). El prompt de
   entrega YA RELLENO está al final del archivo de arranque: copialo
   de ahí, es más rápido
9. [CLAUDE] pegá el MENSAJE 3 → explica la tanda y la archiva solo
10. ¿Seguís estudiando? Depende del formato de la tanda que viene:
    - fue de TEXTO y la próxima también → otra tanda a material/ y
      volvé al paso 9 (hasta 2-3 tandas en la misma sesión)
    - fue de IMÁGENES, o Claude ya avisó que conviene cortar →
      MENSAJE 1, Ctrl+D, y volvé al paso 3 con sesión nueva
      (/rename con el número siguiente, MENSAJE 2 corto y seguís)
11. [CLAUDE] al terminar el día: MENSAJE 5 → Ctrl+D
12. [TERMINAL] engram search "tema de hoy" --project NOMBRE-DEL-TEMA
13. [TERMINAL] git add . && git commit -m "sesión sNN" && git push
    (con DOS PCs es OBLIGATORIO; si no, el otro PC no se entera)

# ============================================================
# SI SE CERRÓ LA TERMINAL SIN QUERER (mismo día)
# ============================================================

[TERMINAL] claude --resume PREFIJO-sNN
OJO: solo para retomar el MISMO día. Día nuevo = sesión nueva.

# ============================================================
# REGLAS DE ORO
# ============================================================

1. El número de sesión solo avanza. Varias sesiones en un día es lo
   NORMAL, no un problema: cada tanda de imágenes abre una nueva.
2. Si el material se puede copiar como texto, va como texto. Siempre.
3. Tamaño de tanda según formato (tabla de arriba). Nunca más de 5
   pantallazos ni más de 10 páginas de texto por tanda.
4. NUNCA salir sin pegar el MENSAJE 5: es lo que guarda el día.
5. Al cambiar de sesión a mitad del día, MENSAJE 1 primero: sin eso
   la tanda no queda registrada en la guía y se pierde.
6. Los ejercicios que trae el propio material SIEMPRE los intento a
   mano ANTES de mirar la solución o pedírsela a Claude.
7. material/ NUNCA se sube a git (copyright; ya está en .gitignore).
8. Los repasos se hacen DESDE CERO, sin mirar mi versión original.
9. Con dos PCs: git pull al empezar, git push al terminar. SIEMPRE.

# ============================================================
# MENSAJES PARA COPIAR Y PEGAR
# ============================================================

--- MENSAJE 0 — configuración inicial (ÚNICA vez por tema; rellená los {{...}}) ---

```
Este es un proyecto de estudio nuevo creado desde mi plantilla, y vos
sos mi profesor particular. Configurémoslo:

QUÉ VOY A APRENDER: {{tema, lo más concreto posible}}
MATERIAL PRINCIPAL: {{libro/curso/docs, autor, edición, formato}}
FORMATO DEL MATERIAL: {{texto seleccionable / solo imágenes / audio /
  video; aclarar si puedo copiar el texto o no}}
IDIOMA DEL MATERIAL: {{idioma; aclarar si NO lo domino}}
MI NIVEL DE PARTIDA: {{qué sé y qué no; sé honesto}}
MI OBJETIVO FINAL: {{para qué aprendo esto; qué quiero lograr}}
PREFIJO DE SESIONES: {{corto, ej: ingles, sql, guitarra}}
NOTAS EXTRA: {{opcional: tiempo disponible, proyectos hermanos, etc.}}

AHORA HACÉ EL SETUP (protocolo completo en CLAUDE.md, sección
"Protocolo del MENSAJE 0"). No lo leas con Read: ya lo tenés cargado.
1. Reemplazá TODOS los {{placeholders}} de CLAUDE.md y RUTA.md con
   mis datos, y COMPLETÁ lo que CLAUDE.md te pide definir para este
   tema: prioridades Pareto, tipos de práctica y sus formatos de
   archivo, cómo se "prueba" una práctica en este tema, el formato
   por defecto del material, herramientas necesarias y carpetas
   extra si hacen falta (crealas).
2. Adaptá las fases de RUTA.md a MI objetivo final.
3. Configurá Engram con project = nombre de esta carpeta.
4. Mostrame un resumen de todas tus decisiones para que las apruebe.
   Cuando te diga "aprobado", guardá todo y decime "listo para la
   primera tanda".
```

--- MENSAJE 1 — cambio de sesión (mitad del día, antes de Ctrl+D) ---

```
Cerramos esta sesión para arrancar una limpia. Sin resumen largo:
1. Confirmá en una línea que la tanda quedó registrada en GUIA.md,
   MECANOGRAFIA.md (+ su archivo de ttyper) y ANKI.txt, y que las
   prácticas nuevas tienen su archivo de arranque creado.
2. Guardá en Engram el punto exacto del material donde quedamos y
   qué sigue.
3. TERMINÁ con estas dos líneas exactas, para que las copie sin pensar:
   - el comando listo: /rename PREFIJO-sNN  (el número de la sesión
     que acabamos de cerrar + 1)
   - y en UNA línea con qué arranca esa sesión.
```

Después: Ctrl+D → armá la tanda nueva en material/ → `claude` → pegás el
`/rename` que te di → MENSAJE 2 → MENSAJE 3.

--- MENSAJE 2 — arranque del día (o de una sesión nueva) ---

```
Nueva sesión de estudio. Sin leer CLAUDE.md con Read (ya lo tenés
cargado): leé el INICIO RÁPIDO de GUIA.md (solo esa sección, con
limit) y EJERCICIOS.md, buscá en Engram (project = nombre de esta
carpeta) dónde quedamos, y decime corto: (1) qué vimos la última vez
en una línea, (2) qué prácticas tengo pendientes, (3) si hay algún
repaso vencido (fechas de la sección REPASOS), (4) qué toca hoy.
Después decido si entrego algo, repaso, o te paso la tanda.
```

--- MENSAJE 3 — tanda de material (repetible: una vez por tanda) ---

```
Tanda nueva: está en material/ (si hay texto, en los .md; si hay
imágenes, en la raíz de material/, sin entrar a material/visto/).
Leela en orden de nombre y arrancá el flujo completo de CLAUDE.md,
respetando el presupuesto de contexto: explicás COMPRIMIENDO, no
transcribiendo, y no repetís lo que ya está en el material.
Cuando termines de explicarme la tanda, antes de cualquier otra cosa:
mové ese material a material/visto/ para que la raíz quede vacía,
agregá las frases de esta tanda a MECANOGRAFIA.md y volcá cada frase
NUEVA a su propio archivo de ttyper (append-only, sin reescribir los
viejos), y agregá las tarjetas 80/20 de esta tanda a ANKI.txt.
Si la tanda fue de imágenes, recordame al final que conviene cambiar
de sesión.
```

--- MENSAJE 4 — entregar una práctica (la versión YA RELLENA está al final del archivo de arranque; usá esa) ---

```
Terminé la práctica [#NN / "nombre"], está en [ruta].
Resultado al probarla: [salida, error, o "no aplica"].
Revisala en detalle EN EL CHAT: qué está bien, qué está mal y POR
QUÉ, sin darme la solución completa de entrada si es del material
(primero pistas). En EJERCICIOS.md actualizá el estado con una
corrección de 3 líneas como máximo; si quedó completada, movela con
su corrección a EJERCICIOS-ARCHIVO.md y agendá sus repasos.
```

--- MENSAJE 5 — cierre del día (SIEMPRE antes de salir) ---

```
Cerramos el día:
1. Verificá que GUIA.md, EJERCICIOS.md, MECANOGRAFIA.md y ANKI.txt
   quedaron actualizados con todo lo de hoy (incluidos los repasos
   agendados, el archivo de ttyper de cada frase nueva, y que las
   tarjetas nuevas sean autocontenidas).
2. Verificá que TODA práctica o repaso pendiente tenga su archivo de
   arranque creado (si falta alguno, crealo ahora: solo enunciado y
   prompt, nada de solución).
3. Archivá lo cerrado: si EJERCICIOS.md pasa de ~150 líneas, mové las
   prácticas completadas y los repasos cumplidos a
   EJERCICIOS-ARCHIVO.md. Si GUIA.md pasa de ~500, mové las sesiones
   viejas a GUIA-ARCHIVO.md.
4. Guardá en Engram (project = nombre de esta carpeta) el resumen y
   en qué punto del material quedamos.
5. Dame el resumen final del día.
```

--- MENSAJE 6 — hacer un repaso (cuando el MENSAJE 2 avise que hay uno vencido) ---

```
Voy a hacer el repaso rX de la práctica #NN. NO me muestres ni me
resumas mi versión anterior: va desde cero. Creá el archivo de
arranque del repaso en ejercicios/repasos/ (solo enunciado + prompt
de entrega, nada de la solución) y esperá a que lo entregue con su
prompt. Al revisarlo, comparalo con mi versión original (está en
EJERCICIOS-ARCHIVO.md): qué mejoré, qué error repetí y POR QUÉ,
actualizá REPASOS en EJERCICIOS.md y agendá el siguiente si
corresponde.
```
