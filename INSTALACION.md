# INSTALACIÓN — todo desde cero, sin asumir nada

Este archivo se lee UNA vez por computador (y cuando algo falle).
El uso diario está en README.md.

# ============================================================
# PARTE 0 — QUÉ ES CADA COSA (en cristiano)
# ============================================================

- GIT: un programa que le saca "fotos" a tu carpeta cada vez que vos
  se lo pedís. Cada foto se llama COMMIT y guarda cómo estaba todo en
  ese momento. Sirve para no perder nada y para ver la historia.
- GITHUB: una página web donde guardás una copia de tu carpeta con
  toda su historia. Es "la nube" de git. Un REPOSITORIO (repo) es una
  carpeta guardada ahí.
- PUSH: subir tus fotos (commits) nuevas a GitHub.
- PULL: bajar a tu PC las fotos nuevas que estén en GitHub (por
  ejemplo, las que subiste desde tu otro PC).
- LLAVE SSH: un par de archivos (uno privado que NUNCA se comparte y
  uno público que le das a GitHub) que funcionan como llave y candado.
  Con esto GitHub te reconoce sin pedirte usuario ni contraseña.
- CLAUDE CODE: el programa `claude` en la terminal; acá hace de profe.
- ENGRAM: la memoria del profe entre sesiones (se conecta como MCP).
- .gitignore: un archivo de texto con una lista de cosas que git debe
  IGNORAR (nunca fotografiar ni subir). Acá lo usamos para que
  material/ (fotos de libros con copyright) jamás llegue a GitHub.

# ============================================================
# PARTE 1 — INSTALAR LO NECESARIO (una vez por PC)
# ============================================================

1. git: en Arch `sudo pacman -S git` (en Debian/Ubuntu:
   `sudo apt install git`). Verificá con `git --version`.
2. Decile a git quién sos (aparece en cada commit):
   git config --global user.name "Tu Nombre"
   git config --global user.email "tucorreo@ejemplo.com"
3. Claude Code y Engram: instalalos como ya los tenés en tu PC
   principal; verificá con `claude --version` y `engram --version`.
4. Las herramientas del TEMA (compilador, intérprete, etc.) se
   definen en el /setup con el profe; no hacen falta todavía.

# ============================================================
# PARTE 2 — LLAVE SSH DESDE CERO (una vez por PC)
# ============================================================

Cada PC tiene SU PROPIA llave. Esto se repite en cada computador.

1. Crear la llave:
   ssh-keygen -t ed25519 -C "tucorreo@ejemplo.com"
   → Enter a todo (ubicación por defecto; frase de paso opcional).
2. Ver la llave PÚBLICA (la que sí se comparte):
   cat ~/.ssh/id_ed25519.pub
   → copiá TODA esa línea (empieza con "ssh-ed25519").
3. Dársela a GitHub: github.com → tu foto (arriba derecha) →
   Settings → SSH and GPG keys → New SSH key → Title: el nombre del
   PC → pegá la llave → Add SSH key.
4. Probar: ssh -T git@github.com
   → la primera vez pregunta "Are you sure...?" → escribí yes.
   → debe responder "Hi TU-USUARIO!" (Hola TU-USUARIO). Listo.

NOTA: si usás 1Password u otro gestor como agente SSH, la llave vive
ahí; el paso 4 debe responder igual "Hi TU-USUARIO!".

# ============================================================
# PARTE 3 — CREAR LA PLANTILLA EN GITHUB (una sola vez en la vida)
# ============================================================

1. github.com → botón "+" (arriba derecha) → New repository.
2. Nombre: plantilla-profesor. Public. NO marques nada más. Create.
3. En tu PC:
   cd ~/Proyectos
   git clone git@github.com:TU-USUARIO/plantilla-profesor.git
   (avisa "cloned an empty repository": normal, está vacío)
4. Copiá adentro TODO el contenido de la plantilla: los archivos
   (README.md, INSTALACION.md, CLAUDE.md, RUTA.md, GUIA.md,
   EJERCICIOS.md, .gitignore) y las carpetas ocultas o especiales
   (.claude/commands/ con los comandos del profe, ToDo/). Verificá con
   `ls -a` que .gitignore y .claude estén (son ocultos: empiezan con
   punto). Sin .claude/commands/ no existen /arranque, /tanda ni el
   resto: el sistema entero cuelga de ahí.
5. Subilos:
   git add .
   git commit -m "plantilla base"
   git push -u origin main
   (si dice que tu rama es "master": git branch -M main y repetí)
6. Convertirla en plantilla oficial: en GitHub, dentro del repo →
   Settings → casilla "Template repository" → marcala. Ya está: ahora
   el repo muestra un botón verde "Use this template".

# ============================================================
# PARTE 4 — EMPEZAR UN TEMA NUEVO (cada vez que aprendas algo)
# ============================================================

1. Entrá a github.com/TU-USUARIO/plantilla-profesor → botón verde
   "Use this template" → Create a new repository.
2. Nombre: el del tema, corto y sin espacios (ej: Ingles-B2,
   Guitarra, SQL-Postgres). Public o Private, como quieras. Create.
   OJO: el nombre importa — la carpeta local se llamará igual y ese
   nombre será el "project" de la memoria de Engram.
3. En tu PC:
   cd ~/Proyectos
   git clone git@github.com:TU-USUARIO/NOMBRE-DEL-TEMA.git
   cd NOMBRE-DEL-TEMA
   mkdir -p material/visto ejercicios/repasos
4. Abrí `claude` en la carpeta y corré `/setup` con tus datos (ver README.md).

# ============================================================
# PARTE 5 — ENLAZAR UN SEGUNDO PC (o tercero...)
# ============================================================

1. Hacé la PARTE 1 y la PARTE 2 en ese PC (git + su propia llave SSH).
2. Cloná el repo del tema:
   cd ~/Proyectos
   git clone git@github.com:TU-USUARIO/NOMBRE-DEL-TEMA.git
   cd NOMBRE-DEL-TEMA
   mkdir -p material/visto
   (material/ llega vacía A PROPÓSITO: las imágenes no viajan por git)
3. LA REGLA DE ORO CON VARIOS PCs — la ejecuta el PROFE, no vos:
   - Al EMPEZAR: `/arranque` hace `git pull` antes de leer nada.
   - Al TERMINAR: `/cierre` (o `/cambio`) te muestra qué cambió, te
     pide el OK y hace `git add` + `git commit` + `git push`.
   ¿Por qué importa? Si tocás archivos en dos PCs sin sincronizar, git
   no sabe cuál versión vale y se arma un "conflicto". Pull al empezar
   + push al terminar = cero conflictos, siempre. Por eso nunca hay
   que saltearse el `/cierre`.
4. La memoria de Engram es LOCAL de cada PC y puede estar desparejada.
   No importa: GUIA.md y EJERCICIOS.md viajan por git y son la fuente
   de verdad — el profe los lee siempre al arrancar.

# ============================================================
# PARTE 6 — PROBLEMAS TÍPICOS (todos ya nos pasaron)
# ============================================================

- Git pide usuario y contraseña al hacer push:
  el repo quedó enlazado por HTTPS y git ignora tu llave SSH.
  Diagnóstico: git remote -v  → si dice https://... es esto.
  Arreglo:
  git remote set-url origin git@github.com:TU-USUARIO/NOMBRE-REPO.git
  Verificá la llave con: ssh -T git@github.com

- "error: cannot run less" al ver historial:
  falta el paginador. Usá `git --no-pager log` (o `git --no-pager
  show --stat HEAD`), o instalá less.

- Subí por error algo que debía estar ignorado (ej: material/):
  1) asegurate de que esté listado en .gitignore
  2) git rm -r --cached CARPETA/   (lo saca de git SIN borrar tus
     archivos del disco)
  3) si NO habías hecho push: git add .gitignore && git commit --amend
     --no-edit  (corrige el mismo commit)
     si YA habías hecho push: commit normal nuevo + push. Y si lo
     subido tiene copyright, avisale al profe: hay que limpiar el
     historial (con un repo nuevo suele ser más fácil recrearlo).

- Claude Code pide permiso para crear o mover archivos:
  es normal la primera vez que toca material/ o ejercicios/ → aceptá.

- El archivo .gitignore "desapareció" al copiarlo:
  empieza con punto, es oculto. Se ve con `ls -a`. Si el download le
  cambió el nombre (gitignore, .gitignore.txt): mv NOMBRE .gitignore
