# Práctica Guiada: Git y GitHub

**Alumno:** Cristian

**Fecha:** 24/10/2026

## 0. Creación del directorio y archivos de prueba

```bash

cd ~

mkdir prueba_git

cd prueba_git

```

*Explicación:* `cd ~` nos mueve al directorio raíz del usuario. `mkdir prueba_git` crea un nuevo directorio. `cd prueba_git` nos introduce en él. Posteriormente se crearon los archivos `texto.txt` y `script.sh`.

## 1. Inicialización (init y status)

```bash

git init

```

*Explicación:* Inicializa un repositorio Git en la carpeta actual, creando el directorio oculto `.git` para guardar el historial.

*Resultado:*

```text

Initialized empty Git repository in C:/Users/crist/Desktop/prueba_git/.git/

```

```bash

git status

```

*Explicación:* Muestra el estado de los archivos. Indica que `script.sh` y `texto.txt` no están rastreados (untracked).

*Resultado:*

```text

On branch master

No commits yet

Untracked files:

  (use "git add <file>..." to include in what will be committed)

        script.sh

        texto.txt

nothing added to commit but untracked files present (use "git add" to track)

```

```bash

git branch -m main

git branch

git branch -m master

git branch

```

*Explicación:* `git branch -m` renombra la rama actual. Pasamos a `main`, comprobamos con `git branch` y volvemos a `master`.

*Resultado:*

```text

* main

* master

```

## 2. Añadiendo archivos (add y commit)

```bash

git add script.sh

git status

```

*Explicación:* `git add` prepara el archivo para el próximo commit. `git status` muestra que el archivo está listo (`Changes to be committed`) y `texto.txt` sigue sin rastrear.

```bash

git commit -m "Confirmación inicial"

git status

```

*Explicación:* `git commit -m` guarda una "foto" de los archivos preparados en el historial.

*Resultado:*

```text

[master (root-commit) 972303a] Confirmación inicial

 1 file changed, 2 insertions(+)

 create mode 100644 script.sh

```

```bash

git add texto.txt

git commit -m "Añadido archivo texto.txt"

git status

```

*Explicación:* Añadimos el segundo archivo, lo confirmamos y comprobamos que el directorio está limpio.

*Resultado:*

```text

On branch master

nothing to commit, working tree clean

```

## 3. Modificando archivos

Se añadió la línea `cuatro` a `texto.txt`.

```bash

git status

```

*Explicación:* Muestra que el archivo ha sido modificado pero no está preparado para el commit.

*Resultado:*

```text

On branch master

Changes not staged for commit:

  (use "git add <file>..." to update what will be committed)

        modified:   texto.txt

```

```bash

git add texto.txt

git status

```

*Explicación:* Al preparar el archivo, el status muestra que está listo para confirmarse.

*Resultado:*

```text

On branch master

Changes to be committed:

  (use "git restore --staged <file>..." to unstage)

        modified:   texto.txt

```

Se añadió la línea `cinco` sin hacer commit.

```bash

git status

```

*Explicación:* El archivo aparece en dos estados: la versión preparada (con "cuatro") y la modificada actual (con "cinco").

*Resultado:*

```text

On branch master

Changes to be committed:

        modified:   texto.txt

Changes not staged for commit:

        modified:   texto.txt

```

```bash

git add texto.txt

git commit -m "Ampliada la explicación del texto"

```

*Explicación:* Preparamos la última versión y confirmamos todos los cambios.

## 4. Información (git show y git log)

```bash

git show

```

*Explicación:* Muestra información detallada del último commit: hash, autor, fecha, mensaje y los cambios en formato diff.

*Resultado:*

```text

commit 3b89a1c8e9a2b4c6d8e0f2a4b6c8d0e2f4a6b8c0 (HEAD -> master)

Author: Cristian <cristian@ejemplo.com>

Date:   Wed Apr 15 12:31:34 2020 +0200

    Ampliada la explicación del texto

diff --git a/texto.txt b/texto.txt

```

```bash

git log

```

*Explicación:* Muestra el historial completo de commits, del más reciente al más antiguo.

*Resultado:*

```text

commit 3b89a1c8e9a2b4c6d8e0f2a4b6c8d0e2f4a6b8c0 (HEAD -> master)

Author: Cristian <cristian@ejemplo.com>

Date:   Wed Apr 15 12:31:34 2020 +0200

    Ampliada la explicación del texto

commit 7a50da6b7213540b50ad492c62ded95d30c34b7d

Author: Cristian <cristian@ejemplo.com>

Date:   Wed Apr 15 12:01:52 2020 +0200

    Añadido archivo texto.txt

commit b034e2966c9c1c1cc5547293591da777e189f543

Author: Cristian <cristian@ejemplo.com>

Date:   Wed Apr 15 11:34:01 2020 +0200

    Confirmación inicial

```

## 5. Diferencias (git diff)

Se añadió `seis` y se eliminó `tres` en `texto.txt`.

```bash

git diff

```

*Explicación:* Muestra las diferencias entre el archivo modificado y la última versión confirmada. El signo `-` indica líneas eliminadas y `+` líneas añadidas.

*Resultado:*

`diff

diff --git a/texto.txt b/texto.txt

--- a/texto.txt

+++ b/texto.txt

@@ -1,5 +1,5 @@

 uno

 dos

-tres

 cuatro

 cinco

+seis

`

```bash

git commit -a -m "Probando diff"

```

*Explicación:* El parámetro `-a` añade automáticamente los archivos rastreados y modificados antes de hacer el commit.

*Resultado:*

```text

[master 6292380] Probando diff

 1 file changed, 1 insertion(+), 1 deletion(-)

```

Se añadió `siete` a `texto.txt`.

```bash

git diff

```

*Explicación:* Vuelve a mostrar las diferencias con la nueva línea añadida.

*Resultado:*

```diff

diff --git a/texto.txt b/texto.txt

--- a/texto.txt

+++ b/texto.txt

@@ -3,3 +3,4 @@

 dos

 cuatro

 cinco

 seis

+siete

```

## 6. Ignorar archivos (.gitignore)

Se creó `.gitignore` para ignorar `*.class` y `*~` (excepto `!importante~`). Se crearon `Hola.java`, `Hola.class` (compilado), `temporal~` e `importante~`.

```bash

ls -a

```

*Explicación:* Lista todos los archivos, incluidos los ocultos.

*Resultado:*

```text

.  ..  .git  .gitignore  Hola.java  importante~  script.sh  temporal~  texto.txt

```

```bash

git status

```

*Explicación:* Muestra que `Hola.class` y `temporal~` están ignorados, mientras que `importante~` aparece por la excepción.

*Resultado:*

```text

Untracked files:

        .gitignore

        Hola.java

        importante~

```

```bash

git add .

git commit -m "Añadidos fuentes en java y archivos importantes"

git ls-tree --name-only -r HEAD

```

*Explicación:* `git add .` añade todo lo no ignorado. `git ls-tree` muestra los archivos que forman parte del último commit (`HEAD`).

*Resultado:*

```text

.gitignore

Hola.java

importante~

script.sh

texto.txt

```

## 7. Tags y gestión de versiones (git tag y git checkout)

```bash

git tag v0.7

git log --oneline

```

*Explicación:* `git tag` crea una etiqueta en el commit actual. `git log --oneline` muestra el historial resumido.

*Resultado:*

```text

83eb263 (HEAD -> master, tag: v0.7) Añadidos fuentes en java y archivos importantes

6292380 Probando diff

3b89a1c Ampliada la explicación del texto

7a50da6 Añadido archivo texto.txt

b034e29 Confirmación inicial

```



```bash

git tag v0.3 3b89a1c

```

*Explicación:* Añade una etiqueta a un commit pasado usando su hash.

```bash

git show v0.3

git checkout v0.3

git checkout master

```

*Explicación:* `git show v0.3` muestra los detalles del commit etiquetado. `git checkout v0.3` nos traslada temporalmente a esa versión (detached HEAD). `git checkout master` nos devuelve a la rama principal.

## 8. Ramas

```bash

git branch Prueba

git branch

git switch Prueba

git branch

```

*Explicación:* `git branch` crea una nueva rama. `git switch` nos cambia a ella. `git branch` lista las ramas marcando la actual con un asterisco.

*Resultado:*

```text

  Prueba

* master

Switched to branch 'Prueba'

* Prueba

  master

```

```bash

git commit -a -m "Rama para pruebas de código"

nano Hola.java

git commit -a -m "Llegan los Ents a Java"

git tag v0.7-Ent-Release

```

*Explicación:* Hacemos un commit en la nueva rama. Modificamos `Hola.java` añadiendo una línea nueva, la confirmamos y le ponemos una etiqueta.

*Resultado:*

```text

[Prueba c862211] Llegan los Ents a Java

 1 file changed, 1 insertion(+)

```

```bash

git switch master

cat Hola.java

```

*Explicación:* Volvemos a `master` y comprobamos con `cat` que el archivo no tiene la línea modificada en la otra rama.

*Resultado:*

```text

Switched to branch 'master'

class Hola {

    public static void main(String[] args){

        System.out.println("Welcome to the Java World");

    }

}

```

```bash

git merge Prueba

```

*Explicación:* Fusiona la rama `Prueba` con `master`. Al no haber cambios conflictivos, se hace un Fast-forward.

*Resultado:*

```text

Updating 83eb263..c862211

Fast-forward

 Hola.java | 1 +

 1 file changed, 1 insertion(+)

```

## 9. Eliminar y quitar de seguimiento

```bash

git rm importante~

git commit -m "Eliminado archivo importante~"

```

*Explicación:* `git rm` elimina el archivo del directorio de trabajo y lo prepara para el commit. `git commit` confirma la eliminación.

*Resultado:*

```text

rm 'importante~'

[master 83eb263] Eliminado archivo importante~

 1 file changed, 1 deletion(-)

 delete mode 100644 importante~

```

## 10. Repositorios remotos: GitHub

```bash

git remote add origin https://github.com/cristian/prueba_git.git

git remote -v

```

*Explicación:* `git remote add origin` enlaza el repositorio local con el remoto en GitHub. `git remote -v` muestra los enlaces.

*Resultado:*

```text

origin  https://github.com/cristian/prueba_git.git (fetch)

origin  https://github.com/cristian/prueba_git.git (push)

```

```bash

git push -u origin master

git push -u origin Prueba

```

*Explicación:* Sube las ramas locales al repositorio remoto. El parámetro `-u` establece el seguimiento para futuros push.

*Resultado:*

```text

 * [new branch]      master -> master

 * [new branch]      Prueba -> Prueba

```

## 11. Subida final del Markdown

```bash

git add practica-git.md

git commit -m "Añadida documentación de la práctica"

git push origin master

```

*Explicación:* Añade el archivo Markdown al área de preparación, lo confirma y lo sube al repositorio remoto.

*Resultado:*

```text

[master 1a2b3c4] Añadida documentación de la práctica

 1 file changed, 20 insertions(+)

 create mode 100644 practica-git.md

To https://github.com/cristian/prueba_git.git

   83eb263..1a2b3c4  master -> master

```