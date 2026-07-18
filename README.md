# PLANTILLA PROFESOR — aprender {{TEMA}} con Claude Code

Sistema de estudio con Claude Code como profesor particular: yo le
paso el material por tandas (pantallazos de un libro, curso, docs...),
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

- material/ → acá dejo la tanda actual (3-8 pantallazos por vez)
- material/visto/ → Claude archiva acá lo ya explicado (lo hace él)
- ejercicios/ → mis prácticas, una carpeta o archivo por práctica.
  Claude crea el ARCHIVO DE ARRANQUE (enunciado + prompt de entrega
  adentro, sin nada de la solución); yo resuelvo ahí mismo
- ejercicios/repasos/ → mis repasos (desde cero, sin mirar el original)
- GUIA.md → la guía por sesiones (la escribe Claude)
- EJERCICIOS.md → prácticas y repasos (los escribe Claude)
- RUTA.md → el plan por fases hasta mi objetivo (lo mantiene Claude)
- CLAUDE.md → las reglas del profe (se adaptan al tema con el MENSAJE 0)

# ============================================================
# PRIMERA VEZ CON ESTE TEMA (sesión {{PREFIJO}}-s01)
# ============================================================

0. Creá el repo desde la plantilla y clonalo (INSTALACION.md, PARTE 4).
1. [TERMINAL] cd ~/Proyectos/NOMBRE-DEL-TEMA
2. [TERMINAL] mkdir -p material/visto ejercicios/repasos
3. [TERMINAL] pasá la primera tanda (3-8 pantallazos) a material/
4. [TERMINAL] claude
5. [CLAUDE] /rename PREFIJO-s01   (ej: ingles-s01)
6. [CLAUDE] /mcp → engram tiene que decir "connected"
7. [CLAUDE] pegá el MENSAJE 0 CON TUS DATOS RELLENADOS → el profe
   adapta CLAUDE.md y RUTA.md a tu tema y te resume qué decidió
8. [CLAUDE] cuando diga "listo", pegá el MENSAJE 2
   (la primera vez pide permiso para mover/crear archivos → aceptá)
9. ¿Más estudio hoy? → otra tanda a material/ y MENSAJE 2 otra vez
10. [CLAUDE] al terminar el día: MENSAJE 5 → salí con Ctrl+D
11. [TERMINAL] engram search "tema de hoy" --project NOMBRE-DEL-TEMA
12. [TERMINAL] git add . && git commit -m "sesión s01" && git push

# ============================================================
# CADA DÍA DE ESTUDIO (s02, s03, ...)
# ============================================================

1. [TERMINAL] cd ~/Proyectos/NOMBRE-DEL-TEMA
2. [TERMINAL] git pull ← lo primero SIEMPRE (clave con más de un PC)
3. [TERMINAL] pasá la tanda (3-8 pantallazos) a material/
4. [TERMINAL] claude
5. [CLAUDE] /rename PREFIJO-sNN ← el número que sigue
6. [CLAUDE] /mcp → engram "connected"
7. [CLAUDE] pegá el MENSAJE 1 → dónde quedamos, pendientes, repasos
   vencidos y qué toca hoy
8. [CLAUDE] si ya hiciste algo pendiente, entregalo ANTES de material
   nuevo: MENSAJE 3 (práctica) o MENSAJE 4 (repaso). El prompt de
   entrega YA RELLENO está al final del archivo de arranque: copialo
   de ahí, es más rápido
9. [CLAUDE] pegá el MENSAJE 2 → explica la tanda y la archiva solo
10. ¿Seguís? → otra tanda a material/ y volvé al paso 9, las veces
    que quieras
11. [CLAUDE] al terminar: MENSAJE 5 → Ctrl+D
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

1. Normalmente una sesión por día; el número solo avanza.
2. Tandas de 3-8 pantallazos MÁXIMO, ajustando según densidad.
3. NUNCA salir sin pegar el MENSAJE 5: es lo que guarda todo.
4. Si Claude olvida cosas o se pone lento: MENSAJE 5, Ctrl+D, y
   sesión nueva (número siguiente, mismo día).
5. Los ejercicios que trae el propio material SIEMPRE los intento a
   mano ANTES de mirar la solución o pedírsela a Claude.
6. material/ NUNCA se sube a git (copyright; ya está en .gitignore).
7. Los repasos se hacen DESDE CERO, sin mirar mi versión original.
8. Con dos PCs: git pull al empezar, git push al terminar. SIEMPRE.

# ============================================================
# MENSAJES PARA COPIAR Y PEGAR
# ============================================================

--- MENSAJE 0 — configuración inicial (ÚNICA vez por tema; rellená los {{...}}) ---

```
Este es un proyecto de estudio nuevo creado desde mi plantilla, y vos
sos mi profesor particular. Configurémoslo:

QUÉ VOY A APRENDER: {{tema, lo más concreto posible}}
MATERIAL PRINCIPAL: {{libro/curso/docs, autor, edición, formato}}
IDIOMA DEL MATERIAL: {{idioma; aclarар si NO lo domino}}
MI NIVEL DE PARTIDA: {{qué sé y qué no; sé honesto}}
MI OBJETIVO FINAL: {{para qué aprendo esto; qué quiero lograr}}
PREFIJO DE SESIONES: {{corto, ej: ingles, sql, guitarra}}
NOTAS EXTRA: {{opcional: tiempo disponible, proyectos hermanos, etc.}}

AHORA HACÉ EL SETUP (protocolo completo en CLAUDE.md, sección
"Protocolo del MENSAJE 0"):
1. Leé CLAUDE.md, RUTA.md, GUIA.md y EJERCICIOS.md.
2. Reemplazá TODOS los {{placeholders}} de CLAUDE.md y RUTA.md con
   mis datos, y COMPLETÁ lo que CLAUDE.md te pide definir para este
   tema: prioridades Pareto, tipos de práctica y sus formatos de
   archivo, cómo se "prueba" una práctica en este tema, herramientas
   necesarias y carpetas extra si hacen falta (crealas).
3. Adaptá las fases de RUTA.md a MI objetivo final.
4. Configurá Engram con project = nombre de esta carpeta.
5. Mostrame un resumen de todas tus decisiones para que las apruebe.
   Cuando te diga "aprobado", guardá todo y decime "listo para la
   primera tanda".
```

--- MENSAJE 1 — arranque del día (s02 en adelante) ---

```
Nueva sesión de estudio. Leé CLAUDE.md, GUIA.md y EJERCICIOS.md,
buscá en Engram (project = nombre de esta carpeta) dónde quedamos, y
decime: (1) qué vimos la última vez en una línea, (2) qué prácticas
tengo pendientes, (3) si hay algún repaso vencido (fechas de la
sección REPASOS), (4) qué toca hoy. Después decido si entrego algo,
repaso, o te paso la siguiente tanda.
```

--- MENSAJE 2 — tanda de material (repetible: una vez por tanda) ---

```
Tanda nueva: leé todas las imágenes que hay en la raíz de material/
(sin entrar a material/visto/), en orden de nombre, y arrancá el
flujo completo de CLAUDE.md. Cuando termines de explicarme esta
tanda, antes de cualquier otra cosa, mové esas mismas imágenes a
material/visto/ para que la raíz quede vacía.
```

--- MENSAJE 3 — entregar una práctica (la versión YA RELLENA está al final del archivo de arranque; usá esa) ---

```
Terminé la práctica [#NN / "nombre"], está en [ruta].
Resultado al probarla: [salida, error, o "no aplica"].
Revisala en detalle: qué está bien, qué está mal y POR QUÉ, sin darme
la solución completa de entrada si es del material (primero pistas).
Actualizá su estado en EJERCICIOS.md y, si quedó completada, agendá
sus repasos.
```

--- MENSAJE 4 — hacer un repaso (cuando el MENSAJE 1 avise que hay uno vencido) ---

```
Voy a hacer el repaso rX de la práctica #NN. NO me muestres ni me
resumas mi versión anterior: va desde cero. Creá el archivo de
arranque del repaso en ejercicios/repasos/ (solo enunciado + prompt
de entrega, nada de la solución) y esperá a que lo entregue con su
prompt. Al revisarlo, comparalo con mi versión original: qué mejoré,
qué error repetí y POR QUÉ, actualizá REPASOS en EJERCICIOS.md y
agendá el siguiente si corresponde.
```

--- MENSAJE 5 — cierre (SIEMPRE antes de salir) ---

```
Cerramos acá:
1. Verificá que GUIA.md y EJERCICIOS.md quedaron actualizados con
   todo lo de hoy (incluida la sección REPASOS si completé algo).
2. Verificá que TODA práctica o repaso pendiente tenga su archivo de
   arranque creado (si falta alguno, crealo ahora: solo enunciado y
   prompt, nada de solución).
3. Guardá en Engram (project = nombre de esta carpeta) el resumen y
   en qué punto del material quedamos.
4. Dame el resumen final de la sesión.
```
