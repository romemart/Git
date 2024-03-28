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
**`git cherry-pick`**: Aplica los cambios de un commit específico a la rama actual
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
**`git blame`**: Muestra quién modificó cada línea de un archivo y en qué commit se realizó el cambio
```ssh
	git blame <archivo>
```

## Comparación de Archivos

Muestra los cambios realizados a un archivo
```ssh
	git diff
	git diff --staged
```

## Deshacer Cambios

Saca un archivo del commit
```ssh
	git reset HEAD <archivo>
```
Devuelve el último commit que se hizo y pone los cambios en staging
```ssh
	git reset --soft HEAD^
```
Devuelve el último commit y todos los cambios
```ssh
	git reset --hard HEAD^
```
Devuelve los 2 últimos commit y todos los cambios
```ssh
	git reset --hard HEAD^^
```
Rollback merge/commit
```ssh
	git log
	git reset --hard <commit_sha>
```
**`git revert`**: Crea un nuevo commit que deshace los cambios realizados en un commit específico
```ssh
	git revert <commit_sha>
```

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

**`git bisect`**: Ayuda a encontrar el commit que introdujo un error o problema específico mediante una búsqueda binaria
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

Los rebase se usan cuando trabajamos con branches esto hace que los branches se pongan al día con el master sin afectar al mismo

Une el branch actual con el master, esto no se puede ver como un merge
```ssh
	git rebase
```
Cuando se produce un conflicto no das las siguientes opciones:

Cuando resolvemos los conflictos --continue continua la secuencia del rebase donde se pausó
```ssh	
	git rebase --continue 
```
Omite el conflicto y sigue su camino
```ssh
	git rebase --skip
```
Devuelve todo al principio del rebase
```ssh
	git rebase --abort
```
Para hacer un rebase a un branch en especifico
```ssh	
	git rebase <nameBranch>
```

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

Falta abordar el comando `git stash`, que es útil cuando deseas guardar temporalmente cambios sin hacer commit para trabajar en otra tarea o resolver algún problema urgente.

## Almacenar Cambios Temporalmente

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

El comando `git stash` es muy útil cuando estás en medio de cambios y necesitas cambiar rápidamente a otra tarea o rama sin hacer commit de los cambios actuales. Te permite guardar temporalmente esos cambios en un "stash" y luego recuperarlos más tarde cuando estés listo para continuar trabajando en ellos.