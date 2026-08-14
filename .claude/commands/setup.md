---
description: Configuración inicial del proyecto — se corre UNA sola vez, en la sesión s01
argument-hint: [tema, material, formato, idioma, nivel, objetivo y prefijo — ver ejemplo abajo]
---

Este es un proyecto de estudio nuevo creado desde mi plantilla, y vos
sos mi profesor particular. Configurémoslo con estos datos:

$ARGUMENTS

Si te falta alguno de estos, PREGUNTÁMELO antes de decidir nada
(suponerlo calibra mal el Pareto y las prácticas, y eso es peor que
tenerlo vacío):

- QUÉ VOY A APRENDER (lo más concreto posible)
- MATERIAL PRINCIPAL (libro/curso/docs, autor, edición)
- FORMATO DEL MATERIAL (texto seleccionable / solo imágenes / audio /
  video — aclarando si puedo copiar el texto o no)
- IDIOMA DEL MATERIAL (y si NO lo domino)
- MI NIVEL DE PARTIDA (qué sé y qué no)
- MI OBJETIVO FINAL (para qué aprendo esto)
- PREFIJO DE SESIONES (corto: ingles, sql, guitarra...)

Ahora hacé el setup siguiendo el **Protocolo de setup** de CLAUDE.md
(no lo leas con Read: ya lo tenés cargado):

1. Reemplazá TODOS los `{{placeholders}}` de `CLAUDE.md`, `README.md`,
   `GUIA.md`, `EJERCICIOS.md` y `RUTA.md`, y completá lo que CLAUDE.md
   te pide definir para este tema: prioridades Pareto, tipos de
   práctica y su formato de archivo de arranque, cómo se "prueba" una
   práctica acá, el formato por defecto del material, herramientas
   necesarias (y cómo verificar que están) y carpetas extra si hacen
   falta (crealas).
2. Adaptá las fases de `RUTA.md` a MI objetivo final.
3. Adaptá los comandos de `.claude/commands/` al tema si algo no
   aplica tal cual (por ejemplo, cómo se prueba una práctica).
4. Dejá la línea **PRÓXIMA SESIÓN** del INICIO RÁPIDO de `GUIA.md`
   apuntando a la sesión que sigue.
5. Agregá al `.gitignore` los temporales típicos de este tema.
6. Configurá Engram con project = nombre de esta carpeta.

Mostrame el resumen de TODAS tus decisiones y esperá mi "aprobado"
antes de guardar. Cuando apruebe, guardá todo, hacé el primer commit y
cerrá con el bloque `▶ SIGUE` para pasarte la primera tanda.
