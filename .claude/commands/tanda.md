---
description: Explica la tanda de material que dejé en material/ (repetible, una vez por tanda)
argument-hint: [opcional: qué hay en la tanda, ej "páginas 70-78 en texto" o "4 pantallazos"]
---

Tanda nueva. $ARGUMENTS

El material está en `material/` (si vino como texto, en los `.md`; si
vino como imágenes, en la raíz de la carpeta). No entres a
`material/visto/`: eso ya está explicado.

Aplicá el **flujo por tanda** completo de CLAUDE.md (no lo leas con
Read: ya lo tenés cargado), respetando el presupuesto de contexto:

1. Leé el material de la tanda en orden de nombre.
2. Explicámelo PIEZA POR PIEZA, anunciando siempre cuál ("PÁGINA 70:",
   "PANTALLAZO 2:") para que lo pueda seguir con la vista. En español,
   con palabras propias, COMPRIMIENDO — no transcribiendo. Si algo no
   tiene base previa, frená y explicá la base primero.
3. Mostrame el contenido clave en el chat, comentado solo donde enseña
   algo nuevo.
4. Si la tanda trae ejercicios del material, avisame cuáles son y
   creales su archivo de arranque.
5. Verificá que entendí con 1-2 preguntas cortas antes de cerrar.

Cuando termines de explicar, en el mismo turno:
- mové el material de la tanda a `material/visto/` para que la raíz
  quede vacía;
- actualizá `GUIA.md` con la sesión en FORMATO CORTO (5-8 bullets,
  máx ~15 líneas) y el INICIO RÁPIDO, incluida la línea
  **PRÓXIMA SESIÓN**;
- agregá 1-2 frases nuevas a `MECANOGRAFIA.md` y volcá cada frase
  NUEVA a su propio archivo de ttyper (append-only);
- agregá las tarjetas 80/20 de esta tanda a `ANKI.txt`
  (autocontenidas, separadas por tab);
- revisá si hace falta crear o actualizar un checklist de `ToDo/`;
- guardá en Engram el punto exacto del material donde quedamos.

Cerrá con el bloque `▶ SIGUE`. Si la tanda fue de IMÁGENES, el
próximo paso es cambiar de sesión (`/cambio`): decilo y explicá por
qué en una línea.
