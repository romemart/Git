# GIT

Git es un sistema de control de versiones distribuido de código abierto diseñado para rastrear cambios en archivos y coordinar el trabajo en proyectos de desarrollo de software. Fue creado por Linus Torvalds en 2005 para el desarrollo del kernel de Linux y desde entonces se ha convertido en una herramienta fundamental en el desarrollo de software colaborativo.

## Flujo de Trabajo en Git

En Git, es importante comprender cómo interactúan diferentes áreas de trabajo y repositorios para gestionar y controlar las versiones de tu código. Aquí se presentan los conceptos clave:

## Workspace (Directorio de Trabajo)

El workspace es el directorio de tu sistema de archivos donde trabajas en tus archivos y realizas cambios en tu código.

## Área de Preparación (Staging Area)

La Staging Area es un área intermedia donde se preparan los cambios antes de confirmarlos definitivamente en el repositorio. Aquí se seleccionan los archivos que se incluirán en el próximo commit.

## Repositorio Local

El repositorio local es donde se almacenan todos los cambios confirmados (commits) y la historia de tu proyecto. Aquí se lleva a cabo el seguimiento de versiones y se pueden realizar operaciones como ramificaciones, fusiones y revertir cambios.

## Repositorio Remoto

El repositorio remoto es una copia del repositorio local alojada en un servidor remoto. Permite la colaboración entre diferentes miembros del equipo y proporciona una copia de seguridad centralizada del proyecto.

## Interacción entre los Componentes

<p align="center">
    <img src="/git.png" alt="image"> 
</p>

Este gráfico muestra cómo interactúan cada uno de los componentes en el flujo de trabajo de Git. Los cambios se mueven desde el workspace a la Staging Area con `git add`, luego se confirman en el repositorio local con `git commit`, y finalmente se envían al repositorio remoto con `git push`.

Este tema proporciona una comprensión básica de cómo funcionan estos conceptos en Git, lo que te ayudará a gestionar eficazmente tu proyecto y colaborar con otros desarrolladores.

## Configuración Básica

Configurar Nombre que salen en los commits
```ssh
	git config --global user.name "romemart"
```
Configurar Email
```ssh	
	git config --global user.email romemart@gmail.com
```
Marco de colores para los comando
```ssh
	git config --global color.ui true
```

## Iniciando Repositorio

Iniciamos GIT en la carpeta donde está el proyecto
```ssh
	git init
```
Clonamos el repositorio de GitHub o Bitbucket
```ssh
	git clone <url>
```
Clonamos el repositorio de GitHub o Bitbucket y lo renombramos
```ssh
	git clone <url> git-demo
```

## Gestión de Archivos

Añadimos todos los archivos para el commit
```ssh
	git add .
```
Añadimos el/los archivos para el commit
```ssh
	git add <archivo 1> <archivo 2> ... <archivo n>
```
Añadimos todos los archivos para el commit omitiendo los nuevos
```ssh
	git add --all 
```
Añadimos todos los archivos con la extensión especificada
```ssh
	git add *.txt
```
Añadimos todos los archivos dentro de un directorio y de una extensión especifica
```ssh
	git add docs/*.txt
```
Añadimos todos los archivos dentro de un directorio
```ssh
	git add docs/
```

## Confirmación de Cambios

Cargar en el HEAD los cambios realizados
```ssh
	git commit -m "Texto que identifique por qué se hizo el commit"
```
Agregar y Cargar en el HEAD los cambios realizados
```ssh
	git commit -a -m "Texto que identifique por qué se hizo el commit"
```
De haber conflictos, muestra los cambios
```ssh
	git commit -a 
```
Agregar al último commit, este no se muestra como un nuevo commit en los logs. Se puede especificar un nuevo mensaje
```ssh
	git commit --amend -m "Texto que identifique por qué se hizo el commit"
```
El comando `git cherry-pick` aplica los cambios de un commit específico en otra ubicación la rama actual u otra rama.
```ssh
	git cherry-pick <commit_sha>
```

## Subida al Repositorio Remoto

Subimos al repositorio
```ssh
	git push origin master
```
Subimos un tag
```ssh
	git push --tags
```

## Visualización de Historial

Muestra los logs de los commits
```ssh
	git log
```
Muestra los cambios en los commits
```ssh
	git log --oneline --stat
```
Muestra gráficos de los commits
```ssh
	git log --oneline --graph
```
El comando `git blame` muestra quién modificó cada línea de un archivo y en qué commit se realizó el cambio
```ssh
	git blame <archivo>
```
El comando `git reflog` examina un registro de donde han estado todas las cabezas de tus ramas mientras trabajas para encontrar commits que puedes haber perdido después de realizar operaciones como reset, rebase, checkout, entre otras.

```ssh
	git reflog
```
Muestra información detallada sobre un commit específico
```ssh
	git show <commit>
```

Muestra un resumen de todos los commits agrupados por autor.
```ssh
	git shortlog
```
## Comparación de Archivos

Muestra los cambios realizados a un archivo
```ssh
	git diff
	git diff --staged
```

## Reset

#### Tipos
- **git reset --soft**: Este comando mueve la punta de la rama y el HEAD al commit especificado, pero conserva los cambios realizados en los commits posteriores en el área de preparación (stage). Esto significa que los cambios permanecen preparados para ser confirmados nuevamente. Es útil para deshacer un commit pero conservar los cambios para realizar ajustes antes de confirmarlos nuevamente.

- **git reset --mixed**: Similar a `git reset --soft`, este comando mueve la punta de la rama y el HEAD al commit especificado, pero los cambios realizados en los commits posteriores no se colocan en el área de preparación. Los cambios permanecen en el directorio de trabajo como modificaciones no preparadas. Es útil para deshacer un commit y revisar los cambios antes de prepararlos para una nueva confirmación.

- **git reset --hard**: Este comando mueve la punta de la rama y el HEAD al commit especificado, y elimina completamente los cambios realizados en los commits posteriores tanto del árbol de confirmaciones como del directorio de trabajo. Es una operación destructiva y no reversible que deshace completamente los cambios, por lo que debes tener cuidado al usarlo, ya que los cambios no confirmados se perderán permanentemente.

#### Ejemplos

Saca un archivo del commit
```ssh
	git reset HEAD <archivo>
```
Revierte el último commit que se hizo y pone los cambios en staging
```ssh
	git reset --soft HEAD^
```
Revierte el último commit y todos los cambios
```ssh
	git reset --hard HEAD^
```
Revierte los 2 últimos commit y todos los cambios
```ssh
	git reset --hard HEAD^^
```
Rollback o revertir los efectos de un `git reset` anterior, restaurando el repositorio como estaba en estado anterior.
```ssh
	git log
	git reset --hard <commit_sha>
```
## Revertir un Commit

El comando `git revert -n <commit>` se utiliza para revertir un commit específico sin realizar automáticamente un commit después de la reversión. El argumento opcional `-n` indica que no se debe hacer un commit automático después de revertir los cambios del commit especificado. Si no se aplica el argumento, se generará un nuevo commit derivado del revert.

**Intervención del Usuario**: El usuario modifica el contenido del archivo(s) afectado por el commit a revertir según sea necesario para deshacer los cambios introducidos por ese commit.

`git add <archivo>`: Después de realizar las modificaciones necesarias, el usuario agrega el(s) archivo(s) modificado(s) al área de preparación para incluirlos en el próximo commit.

`git commit -m "<mensaje>"`: Finalmente, el usuario hace un commit para confirmar la reversión de los cambios del commit especificado. Se proporciona un mensaje descriptivo que indique la acción realizada, como "Revertir cambios del commit `<hash>`".

**Rollback**: Si se desea deshacer los cambios producidos por un `git revert` de manera más drástica y eliminar permanentemente los commits posteriores, se puede utilizar `git reset --hard <commit>`. Esto restablecerá el HEAD y el estado del directorio de trabajo al estado de un commit específico, eliminando los commits posteriores y restaurando el repositorio al estado en que estaba en ese commit. Es importante tener en cuenta que `git reset --hard` es irreversible y puede causar la pérdida permanente de datos, por lo que debe usarse con precaución.

En resumen, tanto `git revert` como `git reset --hard` proporcionan formas de revertir cambios en un repositorio de Git, cada uno con sus propias implicaciones y niveles de control. El uso del argumento `-n` con `git revert` brinda la flexibilidad de realizar modificaciones adicionales antes de confirmar la reversión con un nuevo commit, mientras que `git reset --hard` ofrece una solución más drástica para deshacer los cambios y realizar un rollback en el historial de commits.


## Repositorios Remotos

Agregar repositorio remoto
```ssh
	git remote add origin <url>
```
Cambiar de remote
```ssh
	git remote set-url origin <url>
```
Remover repositorio
```ssh
	git remote rm <name/origin>
```
Mostrar lista de repositorios
```ssh
	git remote -v
```
Mostrar los branches remotos
```ssh	
	git remote show origin
```
Limpiar todos los branches eliminados
```ssh
	git remote prune origin 
```

## Ramas (Branches)

Crea un branch
```ssh
	git branch <nameBranch>
```
Lista los branches
```ssh
	git branch
```
Comando -d elimina el branch y lo une al master
```ssh
	git branch -d <nameBranch>
```
Elimina sin preguntar
```ssh
	git branch -D <nameBranch>
```

El comando `git bisect` ayuda a encontrar el commit que introdujo un error o problema específico mediante una búsqueda binaria
```ssh
	git bisect start
	git bisect bad
	git bisect good <commit_sha>
```

## Etiquetas (Tags)

Muestra una lista de todos los tags
```ssh
	git tag
```
Crea un nuevo tag
```ssh
	git tag -a <version> -m "Esta es la versión x"
```
Eliminar una etiqueta localmente
```ssh
	git tag -d <nombre_etiqueta>
```
Eliminar una etiqueta en el repositorio remoto
```ssh
	git push origin --delete <nombre_etiqueta>
```

## Rebase

El comando `git rebase` se utiliza para reorganizar, editar y combinar commits durante la integración de cambios de una rama a otra. Esto es especialmente útil cuando deseas actualizar una rama con los cambios de otra rama (como `master`) de una manera más limpia y ordenada. El rebase une el historial de commits de una rama con el de otra, aplicando los commits uno a uno en orden cronológico.

#### Opciones del Rebase Interactivo `-i`:

- **Pick**: Mantiene el commit tal como está.

- **Reword**: Cambia el mensaje de confirmación de un commit.

- **Edit**: Detiene el rebase en un commit para realizar cambios.

- **Squash**: Combina un commit con su commit anterior.

- **Fixup**: Combina un commit con el commit anterior, descartando su mensaje de confirmación.

- **Drop**: Elimina el commit del historial.

- **Move Up** y **Move Down**: Reordena los commits durante el rebase interactivo.

- **Search**: Busca un commit por su mensaje de confirmación.

#### Ejemplos de Uso:

- `git rebase`: Une el branch actual con el master, actualizando el branch con los cambios de master.
- `git rebase <nameBranch>`: Realiza un rebase del branch actual a otro branch especificado.
- `git rebase --continue`: Continúa la secuencia del rebase después de resolver conflictos.
- `git rebase --skip`: Omite un conflicto y continúa el rebase.
- `git rebase --abort`: Cancela el rebase y vuelve al estado previo al rebase.

## Otros Comandos

Lista un estado actual del repositorio con lista de archivos modificados o agregados
```ssh
	git status
```
Quita del HEAD un archivo y le pone el estado de no trabajado
```ssh
	git checkout -- <file>
```
Crea un branch en base a uno online
```ssh
	git checkout -b newlocalbranchname origin/branch-name
```
Busca los cambios nuevos y actualiza el repositorio
```ssh
	git pull origin <nameBranch>
```
Cambiar de branch
```ssh
	git checkout <nameBranch/tagname>
```
Une el branch actual con el especificado
```ssh
	git merge <nameBranch>
```
Verifica cambios en el repositorio online con el local
```ssh
	git fetch
```
Borrar un archivo del repositorio
```ssh
	git rm <archivo> 
```
## Clean

El comando `git clean` se utiliza para eliminar archivos no rastreados en el directorio de trabajo. Los archivos no rastreados son aquellos que no están bajo control de versiones de Git, es decir, que no han sido añadidos al repositorio ni incluidos en el área de preparación (staging).

#### Ejemplo:

Supongamos que tienes un repositorio de Git con algunos archivos no rastreados en tu directorio de trabajo. Para eliminar estos archivos no rastreados, puedes utilizar el comando `git clean`.

```ssh
# Lista los archivos no rastreados que serán eliminados (dry-run)
	git clean -n

# Elimina los archivos no rastreados
	git clean -f
```

## Fork

Descargar remote de un fork
```
	git remote add upstream <url>
```

Merge con master de un fork
```
	git fetch upstream
	git merge upstream/master
```

## Stash

Guardar cambios sin hacer commit
```ssh
	git stash
```
Guardar cambios con un mensaje descriptivo
```ssh
	git stash save "Mensaje descriptivo"
```
Listar los cambios almacenados en el stash
```ssh
	git stash list
```
Aplicar los cambios almacenados más recientes del stash y eliminarlos del stash
```ssh
	git stash pop
```
Aplicar los cambios almacenados más recientes del stash pero mantenerlos en el stash
```ssh
	git stash apply
```
Aplicar cambios almacenados de un stash específico
```ssh
	git stash apply stash@{<n>}
```
Eliminar los cambios almacenados más recientes del stash
```ssh
	git stash drop
```
Eliminar un stash específico
```ssh
	git stash drop stash@{<n>}
```
Limpiar todos los cambios almacenados en el stash
```ssh
	git stash clear
```
Crea una nueva rama a partir de los cambios almacenados en el stash.
supongamos tener una rama features y queres aplicar ese cambio en otra que se llamaria hotfix 
```ssh
	git checkout features  # Cambia a la rama features
	git stash              # Guarda los cambios en el stash
	git stash branch hotfix stash@{0}  # Crea una nueva rama hotfix a partir de los cambios guardados en el stash
```

El comando `git stash` es muy útil cuando estás en medio de cambios y necesitas cambiar rápidamente a otra tarea o rama sin hacer commit de los cambios actuales. Te permite guardar temporalmente esos cambios en un "stash" y luego recuperarlos más tarde cuando estés listo para continuar trabajando en ellos.

## Grep

El comando `git grep` se utiliza para buscar patrones de texto en los archivos del repositorio. Funciona de manera similar al comando `grep` de Unix, pero está optimizado para trabajar con repositorios de Git.

#### Ejemplo:

Supongamos que deseas buscar todas las ocurrencias de una palabra específica, como "error", en los archivos de tu repositorio de Git. Puedes utilizar el comando `git grep` de la siguiente manera:

```ssh
	git grep "error"
```

Este comando buscará todas las ocurrencias de la palabra "error" en los archivos del repositorio y mostrará los resultados en la consola, junto con el nombre del archivo y la línea donde se encontró la coincidencia.

Además de buscar una palabra específica, también puedes utilizar expresiones regulares con `git grep`. Por ejemplo, si deseas buscar todas las ocurrencias de números de teléfono en el repositorio, puedes hacerlo de la siguiente manera:

```ssh
	git grep "[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}"
```

Este comando buscará todas las ocurrencias de números de teléfono en el formato XXX-XXX-XXXX en los archivos del repositorio y mostrará los resultados en la consola.

`git grep` también proporciona varias opciones adicionales para personalizar la búsqueda, como buscar en un directorio específico, ignorar ciertos archivos, mostrar solo el nombre de los archivos que contienen coincidencias, entre otros. Puedes consultar la documentación de Git o ejecutar `git help grep` para obtener más información sobre estas opciones.

## Submodule

Los submódulos en Git son referencias a repositorios externos dentro de un repositorio principal. Permiten incluir otros repositorios como subdirectorios dentro de un proyecto más grande. Los submódulos son útiles cuando deseas incluir código de otros proyectos en tu propio proyecto, pero mantenerlos separados y gestionar sus versiones de manera independiente.

#### Ejemplo:

Supongamos que tienes un proyecto principal en Git y quieres agregar un submódulo que contiene una biblioteca externa. Aquí hay un ejemplo paso a paso de cómo hacerlo:

1. Agrega el submódulo al repositorio principal:

```ssh
	git submodule add <URL_del_repositorio> <nombre_directorio>
```

Por ejemplo:

```ssh
	git submodule add https://ejemplo.com/repo-libreria libreria
```

2. Confirma los cambios:

```ssh
	git commit -m "Agregado submódulo de la librería"
```

3. Clona el repositorio principal (incluyendo submódulos) en otro lugar:

```ssh
	git clone --recursive <URL_del_repositorio_principal>
```

El uso de `--recursive` asegura que los submódulos también se clonen correctamente.

4. Para actualizar el submódulo a la última versión:

```ssh
	git submodule update --remote <nombre_directorio>
```

Por ejemplo, si el directorio del submódulo se llama `libreria`:

```ssh
	git submodule update --remote libreria
```

5. Confirma los cambios en el repositorio principal para registrar la actualización del submódulo:

```ssh
	git commit -am "Actualizado submódulo de la librería"
```

Estos pasos te permitirán agregar, actualizar y gestionar submódulos en tu proyecto de Git de manera efectiva. Los submódulos son una herramienta útil para trabajar con código de otros proyectos dentro de tu propio repositorio, manteniendo la independencia y la gestión de versiones de manera ordenada.

## Mover o Copiar archivos

Git no tiene un único comando que pueda copiar o mover archivos directamente entre ramas. Sin embargo, hay formas más concisas de lograr esto en menos pasos.

Para copiar un archivo de una rama a otra:

```ssh
git checkout origen -- ruta/al/archivo && git checkout destino && git add ruta/al/archivo
```

Explicación:
- `git checkout origen -- ruta/al/archivo` extrae el archivo de la rama origen al área de trabajo
- `git checkout destino` cambia a la rama destino
- `git add ruta/al/archivo` agrega el archivo al área de preparación en la rama destino

Para mover un archivo de una rama a otra:

```ssh
git mv -k origen destino -- ruta/al/archivo && git commit
```

Explicación:
- `git mv -k origen destino -- ruta/al/archivo` mueve el archivo del árbol de la rama origen al de la rama destino
- `git commit` confirma los cambios en la rama destino

Estas son formas más cortas, pero aún requieren varios comandos encadenados. Git no tiene un comando único para esta tarea porque mover/copiar archivos entre ramas implica cambios en más de una rama, lo cual va en contra del modelo de ramificación de Git donde las ramas son líneas de desarrollo independientes.

## Worktree
Permite acoplar tantos directorios externos como necesites al mismo repositorio Git, cada uno apuntando a una rama o commit diferente. Esto brinda una gran flexibilidad y aislamiento en tu flujo de trabajo.



Un ejemplo sencillo:

Supongamos que estás trabajando en la rama `master` de un proyecto y necesitas hacer algunos cambios experimentales en una nueva rama `feature`. Normalmente tendrías que cambiar de rama con `git checkout feature`. Pero con `git worktree`, puedes crear un nuevo árbol de trabajo para la rama `feature` sin abandonar `master`:

```ssh
# Crear un nuevo árbol de trabajo para la rama feature
git worktree add -b feature ../feature-worktree

# Esto creará un nuevo directorio feature-worktree que estará en la rama feature
```

Ahora puedes ir a `../feature-worktree` y trabajar allí en la rama `feature` haciendo commits, etc. Mientras que en el directorio original puedes continuar trabajando en `master`.

Cuando termines con la rama `feature`, puedes fusionarla a `master` desde cualquiera de los dos árboles de trabajo.

Otras operaciones útiles con `git worktree`:

- `git worktree list` - Listar todos los árboles de trabajo
- `git worktree remove ../feature-worktree` - Eliminar un árbol de trabajo

`git worktree` es una herramienta poderosa que puede mejorar significativamente el flujo de trabajo al permitir trabajar en múltiples ramas o commits de manera aislada pero eficiente.

## Archive

Crea un archivo comprimido que contiene todos los archivos y directorios de un commit o rama específica, excluyendo el directorio `.git` y el historial de versiones. Es como si tomaras una "instantánea" del código en ese punto en el tiempo.

Ejemplo sencillo:

Supongamos que queremos crear un archivo zip con el contenido de la rama `master` de nuestro proyecto.

1. Abrimos una terminal y navegamos hasta el directorio del repositorio.

2. Ejecutamos el siguiente comando:

```
git archive --format=zip --output=proyecto.zip master
```

Explicación de los argumentos:
- `--format=zip`: Especifica el formato de salida como un archivo zip.
- `--output=proyecto.zip`: Indica el nombre del archivo de salida (en este caso, `proyecto.zip`).
- `master`: Especifica la rama o commit del que se creará el archivo. En este ejemplo, usamos la rama `master`.

3. Después de ejecutar el comando, se creará un archivo llamado `proyecto.zip` en el mismo directorio.

4. Puedes compartir o distribuir este archivo `proyecto.zip` con otros usuarios. Cuando lo descompriman, obtendrán una copia del contenido del código en la rama `master`, sin incluir el directorio `.git` ni el historial de versiones.

Otro ejemplo sencillo:

Si quisieras crear un archivo tar.gz (comprimido con gzip) del commit `abc123` en lugar de una rama, podrías usar el siguiente comando:

```
git archive --format=tar.gz --output=proyecto.tar.gz abc123
```

Esto creará un archivo `proyecto.tar.gz` que contendrá el código en el estado del commit `abc123`.

`git archive` es útil cuando necesitas distribuir o compartir una "instantánea" del código sin incluir todo el historial de versiones, lo que puede ahorrar espacio y facilitar la distribución.