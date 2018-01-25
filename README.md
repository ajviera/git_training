# GIT TRAINING

## BLOBS

  - Archivo unico para git, luego devuelve la comparación para cada uno

## TAGS

- `git tag [TAG_NAME] -a`
  - Liviano: solo con nombre
  - Pesado: se le pone descripción
    - El `-a` es para poner descripción
  - Para subir `git push -u origin [TAG_NAME]`
  - Para subir todos, `git push --tags`
  - Queda fijo a un commit en particular, esto sirve principalmente para releases

## BRANCHS

- Convención:
  - `01-am-branch_name`

## COMMITS

- Convención:
  - Titulo
  - Descripción, separado por una linea con el titulo

- `git log --oneline`, para ver el log solo, sin tanta data y uno debajo del otro.

## HEAD

- Donde esta apuntando el ultimo commit donde estas parado.

## REBASE

- Para reescribir la historia de un commit
- `git rebase -i [COMMIT_HASH]` para hacerlo interactivo

## CHERRY-PICK

- Agarra los cambios del un commit y los pone dentro de otro:
  - `git cherry-pick [COMMIT_HASH]` parado donde quiero meterlo
  - `git rebase --onto master next topic` :
    - Lo que hace es sacar los cambios de `topic` y que no estan en `next`, meterlos en `master`
- Ejemplo:

```
:: Checkout of master to get the latest

git checkout master
git pull origin master
:: Move to the branch you are about to merge

git checkout xx-branch-to-merge
:: Check in that branch with commit you whan to merge

git log

commit b157620b6f5517d1341efb2b81c5d6e4e4c645bd
Author: John Doe john@amalgama.co
Date:   Tue Jul 4 16:59:12 2017 -0300
  Close #99 - Do something

:: Copy the hash of the commit

:: Rename the branch in your machine (ex: append '-old')

git branch -m xx-branch-to-merge-old
:: Checkout master

git checkout master
:: Recreate new branch now from master (with everythign merged and issues closed)

git checkout -b xx-branch-to-merge
:: Merge just the commit you want with the hash copied before

git cherry-pick b157620b6f5517d1341efb2b81c5d6e4e4c645bd
:: Force push of the new branch

git push -f -u origin xx-branch-to-merge
:: Erase old branch

git branch -D origin xx-branch-to-merge-old
:: Finally do corrections in the clean commit 
```

## SUBMODULES

- Clone de un proyecto con un modulo:
  - `git submodule init` para inicializar los submodulos que tenga un proyecto
  - `git submodule update` para updatear todos los modulos
- Agrego un modulo:
  - `git submodule init`
  - `git submodule add [URL_REPO]`

## REFLOG

- Muestra el historial de cosas que se fue haciendo con los commits.
- Si hago un `git reset --hard [COMMIT_HASH]`y quiero volver a agregar un commit que se perdió por el `reset`, uso `git reflog` y luego hago un `git cherry-pick [COMMIT_HASH]` para agregarlo.

## RESET

- `--hard` rompe todo
- `--soft` saca los cambios y los deja para poder volver a agregar usando `git add`

