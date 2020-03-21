# DOCUMENTACION GIT Y GITHUB
## BY PLATZI

### CONFIGURACIÓN INICIAL
1. **Nombre:** `git config --global user.name 'Daniel Vergara'`
2. **Email:** `git config --global user.email danielvsuarez01@gmail.com `
3. **Color:** `git config --global color.ui true`
4. **Listar cambios:** `git config --list`

### FLUJO DE TRABAJO EN GIT
**Creando repositorio:** `git init`  
**Borrar repositorio:** `rm -rf .git`
#### Definiciones:
**Stagin:** Area temporal en memoria RAM, area completamente desconectada, y donde al principio se van agregando los cambios
**Repositorio:** Carpeta .git es donde van a estar todos los cambios al final del proyecto, nombre por defecto *master*
**Untracked:** Archivo modificado que no esta en staging
**Traked:** Archivo modificado

**Agregando archivos:**
1. `git add archivo` (agrega un archivo) 
2. `git add -A` (agrega todos los archivos) 
3. `git add -n archivo` (no hace nada, sirve para ver los archivos que puedes agregar)

**Quitando archivos cambiados:** 
1. `git rm --cached archivo` (lo borra del staging) 
2. `git rm -f archivo` (lo borra complemetamente)

**Viendo estados:** 
1. `git status` Estado del archivo
2. `git show archivo` Cambios que ha sufrido el archivo, importante cuando tenemos un archivo que no funciona y no sabemos que le pasa 
3. `git blame archivo`: ver quien hizo que cosa en cada linea del archivo
**Confirmando cambios:** 
1. `git commit -m 'mensaje'` 
2. `git commit -am 'mensaje'` hace git add y hace el commit enseguida, solo sirve para archivos que ya le hemos hecho git add anteriormente 
**Corrigiendo ultimo cambios:** `git commit --amend` (puede cambiar el ultimo commit que hiciste)  
**Etiquetando:** cuando queremos colocarle etiquetas al proyecto como por ejemplo: version 1, version 2 y asi 
1. `git tag 0.5`(etiquetar solamente con un numero de version) 
2. `git tag -a 0.5 -m 'version estable'` (etiquetar con un mensaje)
3. `git tag -a 0.5 -m 'version estable' sha1` (etiquetar con un mensaje en especifico)
4. `git tag 0.3 (sha1)` (etiquetar commit anterior) 
5. `git tag -l` (lista de etiquetas) 
6. `git tag -d 0.5` (elimina la etiqueta) 
7. `git tag -f -a 0.1 -m 'mensaje' (sha1)` (renombrar etiqueta)   
_hay que tener en cuenta que despues de renombrar hay que eliminar la que tiene le nombre errado_

**Revisando historia del proyecto:** 
1. `git log` (toda la informacion del log)
2. `git log --oneline` (log resumido)
3. `git log --oneline --graph` (grafico de como van los commits en el proyecto) _importante para cuando se trabaje con ramas_
4. `git log --stat` nos muestra el git log con los cambios que hemos hecho en cada commit

**Busqueda:**
1. `git grep palabra`: veces en que hemos usado una palabra en nuestro codigo
2. `git grep -n palabra`: linea en donde implementamos esa linea
3. `git grep -c palabra`: cantidad de veces que uso una palabra
4. `git grep -c "<p>"`: para etiquetas
5. `git log -S "palabra"`: para buscar dentro del log

**Revisando cambios entre commits:**
1. `git diff sha1` (cambios entre estado actual y el commit del sha1)
2. `git diff 0.3` (cambios entre una etiqueta y la otra etiqueta)
3. `git diff sha1 sha1` (cambios entre dos estados)

**Git reset:** Sirve para reescribir lo que hicimos anteriormente
1. **--soft:** `git reset --soft sha1` borra el ultimo commit, pero no elimina los archivos modificados y los mantiene en staging
2. **--mixed:** `git reset --mixed sha1` borra el ultimo commit, pero no elimina los archivos modificados y elimina del staging
3. **--hard:** `git reset --hard sha1` elimina todo fisicamente si esta en el working directory, pero si no han sido agregados no los elimina. Si borramos gran parte del proyecto, podemos volver a recuperar si tenemos el log anterior con el ultimo commit y hacer `git reset --hard sha1` con el sha de este ultimo commit y podemos volver al estado actual.
4. **git reflog:** es un git log pero con mas cosas para referenciar

### MULTIPLES ENTORNOS DE TRABAJO
**Git branch (Multiples variantes del repositorio):**
1. `git branch nombre_rama` (para crear una rama)
2. `git branch -l` (listar ramas)
3. `git branch -d rama` (eliminar rama)
4. `git branch -D rama` (eliminar rama a la fuerza)
5. `git branch -m nombre_rama nombre_nuevo` (renombrar rama)

**Git checkout (Moviendonos entre ramas y versiones):**
1. `git checkout rama` (movernos a la rama que queramos)
2. `git checkout sha1` (movenos a un commit en especifico)
3. `git checkout -b nuevarama` (crear una rama nueva y movernos a ella enseguida)
4. `git checkout -- file` (resetea cambios que no han sido movidos a stage)


**Git merge (Mezclando ramas y resolviendo conflictos):** _Importante, para mezclar las ramas debemos estar en la rama que queremos actualizar (por ejemplo master)_  `git merge rama` (esta _rama_ es la que queremos que se fusione con master)  

**Git rebase (Reescribiendo la historia del proyecto):** 
1. `git rebase rama` es como _merge_ pero no muestra bifurcaciones en el codigo, pero es recomendable solo hacerlo en local no cuando no estes trabajando en un equipo con otras personas
2. `git rebase -i rama` lo hace de manera interactiva y muestra el editor donde tenemos los commits

**Git stash(guardando cambios temporales)** Guardar archivos que todavian no estan listos para ser confirmados
1. `git stash` guarda cambios de rapidez, los cuales no quieren ser agregados aun en un commit
2. `git stash list` listado de todos los stash
3. `git stash drop stash@{numero}` eliminar un stash en especifico
4. `git stash apply stash@{numero}` aplicar un stash en especifico

**Cherry pick: eligiendo commits selectivamente**
1. `git cherry pick sha1` elige un commit en especifico de otra rama y lo agrega a la rama que estamos actualmente

### GITHUB
**Iniciando**
1. **README** archivo que se va a ver cuando la persona entre al repositorio en github
2. **git ignore:**
3. **Licencias:** Licencias que regiran nuestro codigo
**Git clone/fork (clonando repositorios remotos):**
1. `git clone https://repositorio` para descargar un repositorio remoto desde github para el computador (tambien podemos descargar el .zip)
2. fork es para copiar un repositorio remoto de otro perfil de GitHub a nuestro propio perfil

**Git remote (Añadiendo un repositorio remoto a uno local)**
1. `git remote add origin https` conecta un repositorio remoto con uno local
2. `git remote -v` lista de las conexiones existentes
3. `git remote remove origin` elimina la conexion entre repositorios

**Git pull/fetch (Trayendo cambios desde el repositorio remoto)**
1. `git fetch origin rama` trae los cambios desde una rama del repositorio remoto a uno local
2. `git merge origin/rama --allow-unrelated-histories` mezcla los cambios de la rama que descargamos con la rama master u otra rama
3. `git pull origin rama` hace los dos pasos anteiores pero en uno solo, descarga y mezcla los cambios

**Git push(enviando cambios al repositorio remoto)**
1. `git push origin rama` sube los cambios del local al remoto a la rama donde necesitemos
2. `git push origin rama --tags` sube los tags que tenemos en el repositorio local


