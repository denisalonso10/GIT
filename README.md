# Práctica de Git

## Crear directorio con los distintos archivos

```
Denís@PC MINGW64 ~
$ mkdir prueba_git

Denís@PC MINGW64 ~
$ cd prueba_git

Denís@PC MINGW64 ~/prueba_git
$ nano texto.txt

Denís@PC MINGW64 ~/prueba_git
$ nano script.sh
```

`mkdir` crea la carpeta, `cd` entra en ella y `nano` abre el editor para crear cada archivo.

## Iniciar repositorio en Git

```
Denís@PC MINGW64 ~/prueba_git
$ git init
Initialized empty Git repository in C:/Users/Denís/prueba_git/.git/
```

Crea la carpeta oculta `.git`, donde Git guarda todo el historial del proyecto.

## Ver el estado del repositorio en Git

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Hay dos archivos `untracked`: `script.sh` y `texto.txt`. Untracked significa que Git ve los archivos pero todavía no los sigue.

## Cambiar nombre de la rama

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git branch -m main

Denís@PC MINGW64 ~/prueba_git (main)
$ git branch -m master
```

`-m` renombra la rama actual. Aquí se pasó a `main` y se volvió a `master`.

### Añadir y confirmar los archivos

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git add script.sh
warning: in the working copy of 'script.sh', LF will be replaced by CRLF the next time Git touches it

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git commit -m "Confirmación Inicial"
[master (root-commit) ddc4390] Confirmación Inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh

Denís@PC MINGW64 ~/prueba_git (master)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

Denís@PC MINGW64 ~/prueba_git (master)
$ git commit -m "Añadido archivo texto.txt"
[master 4fd325f] Añadido archivo texto.txt
 1 file changed, 3 insertions(+)
 create mode 100644 texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
nothing to commit, working tree clean
```

`git add` pasa el archivo al área de preparación y `git commit` guarda esa preparación en el historial. Al final, `git status` dice `working tree clean`: no queda nada pendiente. El aviso `LF will be replaced by CRLF` es normal en Windows (cambia el tipo de salto de línea) y no es un error.

## Modificar archivo

```
Denís@PC MINGW64 ~/prueba_git (master)
$ nano texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git detecta que el archivo cambió, pero el cambio todavía no está preparado para el commit.

## Añadir los cambios

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ nano texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

Denís@PC MINGW64 ~/prueba_git (master)
$ git commit -m "Ampliada la explicación del texto"
[master dccc55a] Ampliada la explicación del texto
 1 file changed, 2 insertions(+)

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
nothing to commit, working tree clean
```

Tras el primer `add`, el archivo aparece en `Changes to be committed`. Al editarlo otra vez, aparece a la vez preparado y modificado: `git add` guarda el archivo tal como está en ese momento, así que hay que repetirlo para incluir lo último.

## Ver la información sobre la última versión confirmada

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git show
commit dccc55a8a6246265f4d58d76f3701a80ba75faa7 (HEAD -> master)
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:28:07 2026 +0100

    Ampliada la explicación del texto

diff --git a/texto.txt b/texto.txt
index cda1a21..11ce7ce 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
 tres
+cuatro
+cinco
```

Muestra el último commit: autor, fecha, mensaje y los cambios (`+cuatro`, `+cinco`).

### Ver el historial

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git log
commit dccc55a8a6246265f4d58d76f3701a80ba75faa7 (HEAD -> master)
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:28:07 2026 +0100

    Ampliada la explicación del texto

commit 4fd325fd93bcbf985d07617cb40a009840d67ad9
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:23:05 2026 +0100

    Añadido archivo texto.txt

commit ddc4390910edb81cd2ff38fa268eb100203d3bac
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:21:50 2026 +0100

    Confirmación Inicial
```

Lista los commits, del más reciente al más antiguo, con su identificador (hash).

### Ver los cambios sin confirmar

```
Denís@PC MINGW64 ~/prueba_git (master)
$ nano texto.txt

Denís@PC MINGW64 ~/prueba_git (master)
$ git diff
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/texto.txt b/texto.txt
index 11ce7ce..b82b6c8 100644
--- a/texto.txt
+++ b/texto.txt
@@ -3,3 +3,4 @@ dos
 tres
 cuatro
 cinco
+siete
```

`git diff` muestra lo que se ha modificado y aún no está en un commit (aquí, `+siete`).

### Ignorar archivos

```
Denís@PC MINGW64 ~/prueba_git (master)
$ nano .gitignore

Denís@PC MINGW64 ~/prueba_git (master)
$ nano Hola.java

Denís@PC MINGW64 ~/prueba_git (master)
$ nano temporal~

Denís@PC MINGW64 ~/prueba_git (master)
$ nano importante~

Denís@PC MINGW64 ~/prueba_git (master)
$ ls -a
./  .git/  Hola.java  script.sh  texto.txt
../  .gitignore  importante~  temporal~

Denís@PC MINGW64 ~/prueba_git (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        Hola.java
        importante~

no changes added to commit (use "git add" and/or "git commit -a")
```

`.gitignore` indica qué archivos debe ignorar Git. En `git status` no aparece `temporal~` porque se ignora; `importante~` sí aparece como untracked.

### Confirmar todo

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git add .
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'Hola.java', LF will be replaced by CRLF the next time Git touches it

Denís@PC MINGW64 ~/prueba_git (master)
$ git commit -m "Añadidos fuentes en java y archivos importantes"
[master 6d65e2d] Añadidos fuentes en java y archivos importantes
 4 files changed, 13 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 Hola.java
 create mode 100644 importante~
```

`git add .` prepara todos los cambios de la carpeta a la vez.

### Ver un commit concreto

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git show 4fd325fd93bcbf985d07617cb40a009840d67ad9
commit 4fd325fd93bcbf985d07617cb40a009840d67ad9
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:23:05 2026 +0100

    Añadido archivo texto.txt

diff --git a/texto.txt b/texto.txt
new file mode 100644
index 0000000..cda1a21
--- /dev/null
+++ b/texto.txt
@@ -0,0 +1,3 @@
+uno
+dos
+tres
```

Con el hash de cualquier commit se ve solo ese.

## TAGS

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git tag v0.7

Denís@PC MINGW64 ~/prueba_git (master)
$ git tag v0.3 4fd325fd93bcbf985d07617cb40a009840d67ad9

Denís@PC MINGW64 ~/prueba_git (master)
$ git log --oneline
6d65e2d (HEAD -> master, tag: v0.7) Añadidos fuentes en java y archivos importantes
dccc55a Ampliada la explicación del texto
4fd325f (tag: v0.3) Añadido archivo texto.txt
ddc4390 Confirmación Inicial
```

Una etiqueta pone nombre a un commit. Sin hash, etiqueta el commit actual (`v0.7`); con hash, uno anterior (`v0.3`). `--oneline` muestra el historial con una línea por commit.

## Ver por versión

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git show v0.3
commit 4fd325fd93bcbf985d07617cb40a009840d67ad9 (tag: v0.3)
Author: Denís <denisalonsoo10@gmail.com>
Date:   Thu Oct 29 18:23:05 2026 +0100

    Añadido archivo texto.txt

diff --git a/texto.txt b/texto.txt
new file mode 100644
index 0000000..cda1a21
--- /dev/null
+++ b/texto.txt
@@ -0,0 +1,3 @@
+uno
+dos
+tres

Denís@PC MINGW64 ~/prueba_git (master)
$ git checkout v0.3
Note: switching to 'v0.3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 4fd325f Añadido archivo texto.txt

Denís@PC MINGW64 ~/prueba_git ((v0.3))
$ git checkout master
Previous HEAD position was 4fd325f Añadido archivo texto.txt
Switched to branch 'master'
```

`git checkout v0.3` lleva el proyecto a esa versión y deja el estado `detached HEAD`: no se está en ninguna rama, es solo para mirar. `git checkout master` vuelve a la rama principal.

## Ramas

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git branch Prueba

Denís@PC MINGW64 ~/prueba_git (master)
$ git log --oneline
6d65e2d (HEAD -> master, tag: v0.7, Prueba) Añadidos fuentes en java y archivos importantes
dccc55a Ampliada la explicación del texto
4fd325f (tag: v0.3) Añadido archivo texto.txt
ddc4390 Confirmación Inicial

Denís@PC MINGW64 ~/prueba_git (master)
$ git branch
  Prueba
* master

Denís@PC MINGW64 ~/prueba_git (master)
$ git branch Prueba

Denís@PC MINGW64 ~/prueba_git (master)
$ git log --oneline
6d65e2d (HEAD -> master, tag: v0.7, Prueba) Añadidos fuentes en java y archivos importantes
dccc55a Ampliada la explicación del texto
4fd325f (tag: v0.3) Añadido archivo texto.txt
ddc4390 Confirmación Inicial

Denís@PC MINGW64 ~/prueba_git (master)
$ git branch
  Prueba
* master

Denís@PC MINGW64 ~/prueba_git (master)
$ git switch Prueba
Switched to branch 'Prueba'

Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git branch
* Prueba
  master

Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git log --oneline
6d65e2d (HEAD -> Prueba, tag: v0.7, master) Añadidos fuentes en java y archivos importantes
dccc55a Ampliada la explicación del texto
4fd325f (tag: v0.3) Añadido archivo texto.txt
ddc4390 Confirmación Inicial
```

`git branch Prueba` crea la rama pero no cambia a ella. `git branch` lista las ramas y marca con `*` la actual. `git switch` cambia de rama.

### Trabajar en la rama

```
Denís@PC MINGW64 ~/prueba_git (Prueba)
$ nano Hola.java

Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git commit -a -m "Llegan los Ents a Java"
[Prueba 9cd14d3] Llegan los Ents a Java
 1 file changed, 2 insertions(+)

Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git tag v0.7-Ent-Release

Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git log --oneline
9cd14d3 (HEAD -> Prueba, tag: v0.7-Ent-Release) Llegan los Ents a Java
6d65e2d (tag: v0.7, master) Añadidos fuentes en java y archivos importantes
dccc55a Ampliada la explicación del texto
4fd325f (tag: v0.3) Añadido archivo texto.txt
ddc4390 Confirmación Inicial
```

`-a` incluye automáticamente los archivos ya seguidos que se modificaron, sin hacer `git add`.

## Fusionar ramas

```
Denís@PC MINGW64 ~/prueba_git (Prueba)
$ git switch master
Switched to branch 'master'

Denís@PC MINGW64 ~/prueba_git (master)
$ cat Hola.java
class Hola {
public static void main(String[] args){
System.out.println("Welcome to the Java World");
}
}

Denís@PC MINGW64 ~/prueba_git (master)
$ git merge Prueba
Updating 6d65e2d..9cd14d3
Fast-forward
 Hola.java | 2 ++
 1 file changed, 2 insertions(+)
```

En `master`, `Hola.java` aún no tiene los cambios de `Prueba`. `git merge Prueba` los trae. 

## Eliminar un archivo

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git rm importante~
rm 'importante~'

Denís@PC MINGW64 ~/prueba_git (master)
$ git commit -m "Eliminado importante~"
[master 8c07a87] Eliminado importante~
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 importante~
```

`git rm` borra el archivo y deja el borrado preparado para el commit.

## Repositorio remoto (GitHub)

```
Denís@PC MINGW64 ~/prueba_git (master)
$ git remote add origin https://github.com/denisalonso10/GIT.git

Denís@PC MINGW64 ~/prueba_git (master)
$ git push -u origin Prueba
Enumerating objects: 18, done.
Counting objects: 100% (18/18), done.
Delta compression using up to 16 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (18/18), 1.70 KiB | 581.00 KiB/s, done.
Total 18 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), done.
remote:
remote: Create a pull request for 'Prueba' on GitHub by visiting:
remote:      https://github.com/denisalonso10/GIT/pull/new/Prueba
remote:
To https://github.com/denisalonso10/GIT.git
 * [new branch]      Prueba -> Prueba
branch 'Prueba' set up to track 'origin/Prueba'.

Denís@PC MINGW64 ~/prueba_git (master)
$ git push -u origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 235 bytes | 235.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/denisalonso10/GIT/pull/new/master
remote:
To https://github.com/denisalonso10/GIT.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.

Denís@PC MINGW64 ~/prueba_git (master)
$ git remote -v
origin  https://github.com/denisalonso10/GIT.git (fetch)
origin  https://github.com/denisalonso10/GIT.git (push)
```

`remote add` conecta la carpeta con el repositorio de GitHub y lo llama `origin`. `push -u` sube la rama y la deja enlazada, para poder usar luego solo `git push`. `remote -v` muestra las direcciones configuradas.
