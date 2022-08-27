> Git Hub esta trabajando para reemplazar el término master en su servicio con un término mas neutral como main para evitar referencias innecesarias a la esclavitud.
Por eso  recominedan usar:
```
  $ git branch -M main
```
## Para comenzar un Repo Git Local

```
  $ git init
```

Crea un directorio .git en el directorio del proyecto.
En este punto nada de tu proyecto esta siendo seguido.
Hasta hacer tu primer commit inicial, donde ahora los archivos de ese commit estan siendo seguidos.

>**Recordar:** Cada archivo en tu directorio de trabajo puede estar en uno de estos 2 estados: con seguimiento o sin seguimiento.
+ Archivos con seguimiento => son aquellos que en su ultima instantanea(snapshot:=commit) pueden estar en el estado: unmodified, modified o staged.
+ Archivos sin seguimiento => son el resto.
# 4 estados del ciclo de vida de archivos git

![file-state-git](../Git/img/state-git.gif)

1. **untraked**(sin seguimiento) -> archivos sin seguimiento
  + No viven dentro del Git, solo estan en el disco duro.
  + Nunca han sido afectados por el comando git add o fue removido su seguimiento de Git
  + Git no tiene registros de su existencia
2. **unmodified**(sin modificar)
  + Viven dentro del Git
  + Se hizo al menos un commit del mismo, solo no ha sido modificado desde entonces
3. **modified**(modificado) -> cambios no rastreados para el commit
  + Viven dentro del Git
  + Son cambios en un archivo que fue commiteado previamente pero no han sido agregados al stage ni estan confirmados
4. **staged**(stage) -> cambios a ser confirmados
  + Viven dentro del Git
  + Estan en staging
  + Estan registrados por Git, al ser afectados por git add
  + Git sabe de sus ultimos cambios, pero aun no se han guardado en el repositorio hasta que hagan un git commit
  + Son cambios ha ser confirmados

**Nota:** Caso raro, archivos en 2 estados al mismo timepo: modified y staged. Pasa cuando guardas los cambios de un archivo en el area de stage(con git add), pero antes de hacer git commit para guardar los cambios en el repositorio, haces nuevos cambios que todavia no han sido guardados en el area de stage.

# Los 3 estados principales de Git

![three-state-git](./img/three-state-git.png)

> Recordar: Git tiene 3 estados principales donde viviran tus archivos:
> 1. commited: significa que los datos estan seguros almacenados en tu BD local.
> 2. modified: significa que tiene cambios el archivo pero no tienen una confirmacion en tu BD aun.
> 3. staged: significa que tienes marcado un archivo modificado en la version actual ha ser confirmado con un commit.

+ El **git directory** es donde se almacena los metadatos y la base de datos de objetos de tu proyecto. Esto es lo que se copia al hacer un clon.
+ El **working directory** es una simple confirmacion de una version del proyecto. Esos archivos son sacados de la base de datos comprimida en el *git directory* y pasadas al disco para ser usadas o modificas.
+ El **staging area** es un archivo, generalmente contenido en tu *git directory*, que almacena info sobre que va ha ser confirmado.

Flujo Basico:
1. Modificas un archivo en tu area de directorio
2. Los pasas al stage, haciendo una instantanea(git add)
3. Haces un commit(git commit), toma los archivos del stage y almacena la instantanea de manera permanente en tu Git Repositoty

Por lo tanto, en particular la version de los archivos en el Git Directory, se considera committed. Si es modificada pero esta agregada al staging area, esta staged. Y si fue modificada desde que fue chequeada pero no esta en el stage, esta modified.

# Instalacion

```
sudo apt install git
```
### Inicializar repositorio
```
git init 
```
### Colocar informacion personal
```
git config --global user.name "Fulano de tal"
git config --global user.email fulanodetal@gmail.com
```
### Comprobar estado del repositorio
```
git status
```
### Agregar archivos
```
git add archivo.txt
```
#### Confirmar cambios
```
git commit -m "Mensaje descriptivo"
```
#### Crear rama
```
git branch nuevarama
```
#### Listar ramas existentes
```
git branch
```
### Cambiarse de rama
```
git checkout nuevarama
```
### Crear rama a partir de otra y cambiarse a la misma (todo de un solo saque)
```
git checkout -b nuevarama ramaoriginal
```
### Agregar repositorio remoto
```
git remote add origin https://github.com/usuario/repositorio
```
### Subir archivos al repositorio remoto

Para la rama principal:
```
git push -u origin master
```
(eso lo hacemos la primera vez... luego, con poner git push será suficiente)

Para otra rama:
```
git push -u origin mirama
```
### Traerse cambios de una rama del repositorio remoto

Para la rama principal:
```
git pull origin master
```
Para otra rama:
```
git pull origin otrarama
```
### Fusionar rama1 a rama2
```
git checkout rama2
git merge --no-ff rama1
```
(en la pantalla que aparece, Ctrl+o y Ctrl+x)

### Historial
```
git log
git log --oneline (muestra historial resumido)
git log --oneline --graph (muestra además líneas que relacionan las ramas)
```
### Revertir cambios de todos los archivos hacia un determinado commit
```
git log --oneline (para obtener el hash del commit)
git reset --hard "hash_del_commit"
```
### Revertir cambios de un determinado archivo hacia un determinado commit
```
git log --oneline (para obterner el hash del commit)
git checkout "hash_del_commit" -- archivo.txt
```
# Mas

### Comando git videos

[video explicativo de Merge](https://www.youtube.com/watch?v=vu4Rv1SmzwM)

[Sobre git remote](https://diego.com.es/compartir-y-actualizar-proyectos-en-git)

[git fetch vs pull, rama oculta origin/master](https://es.stackoverflow.com/questions/245/cu%C3%A1l-es-la-diferencia-entre-pull-y-fetch-en-git)

[Explicacion git merge --no-ff <name rama de la cual obtendremos los datos a fusionar>](https://aprendegit.com/forzando-merge-commits/)

[Fusion Avanzada, y comandos git diff para comparar](https://git-scm.com/book/es/v2/Herramientas-de-Git-Fusi%C3%B3n-Avanzada)

### Otros comandos

+ Mas simpatico vist de las ramas
```
git log --pretty=format:"%h %s" --graph
```
+ Estrategia recursiva de merge
```
  - git merge --no-ff <name rama de la cual obtendremos los datos a fusionar>
```
+ obtener una descripción más detallada de las ramas
```
  - git show-branch
```
+ obtener la lista de ramas
```
  - git branch -a
``` 
+ Git para procesar los merge usa un antecesor común y comprueba los cambios
  que se han introducido al proyecto desde entonces, combinando el código de ambas ramas.

  Debo situarme en la rama que deseo que se fusione con la rama que obtendremos los datos para fusionarlos.
  
  Si estamos en la rama master y queremos fusionarla con la rama experimental hacemos, un merge es un commit por lo que lleva un msj.
  
```
    git merge experimental -m 'Esto es un merge con mensaje'
```
  - En caso de haber un conflictos podemos abotar el merge la fusion para que quede como antes con:
```
    git merge --abort
```
  - Si hay conflictos, hacemos:
```
    git status (vemos donde dice **both modificated**, que indica el archivo en conflicto)
```
     vamos al archivo con algun editor donde se mostrara lo sgte.:
      <<<<HEAD
      .....
      ====
      .....
      >>>>name_branch
    * Debemos elegir alguno borrando lo sobrante, ademas del <<<<HEAD, ====, >>>>name_branch
    * O poner algo nuevo con lo mejor de ambos mundos, sin olvidar borrar las dos ...,  ademas del <<<<HEAD, ====, >>>>name_branch
    * Luego guardamos el archivo
    * Lo agragamos al stage con git add
    * Hacemos un commit con git commit -m "algun msj del merge sobre la resolucion del conflicto"
  
+ Para comitear usar solo
```
git commit -m "algun msj"
```
  - pues -a -m te comitea todas la modificaciones incluso las que no estan en el staging area
```
git commit -a -m "algun msj"
```
+ Para ver los archivos asociados a los commit
```
  - git log --name-only
```
+ commit de algunos archivos modificados que esten en es stage area
```
  - git commit name_archivo0 ... name_archivoN -m "algun mensaje"
```
+ descartar los cambios realizados en un archivo
```
  - git checkout -- name_archivo
```
[comandos git para borrar archivos o carpetas](https://www.bufa.es/git-borrar-archivos-carpetas/)
  
+ comando para cambiar el nombre de una rama
  Posicionarse en la rama y :
```
  - git branch -m <nuevo-nombre>
  - git push origin -u <new-name>
  - git push origin --delete <old-name>
```
+ comando para mostrar los comites de manera agradable y que rama esta HEAD
```
  - git log --oneline --decorate
  - git log --oneline --decorate --all {para ver todos los commit que tenemos y la rama a la que pertenecen}
  - git log --oneline --decorate --all --graph {ademas vere el arbol graficamente}
```
+ comando para borrar arhivos/capetas del repositorio
```
    git rm -r micarpeta
    git rm miarchivo
    git commit -m "elimino carperta/archivo innecesarios de seguimiento"
    git push origin -u <name-branch>
```
+ Si quieres que el archivo permanezca en tu ordenador pero simplemente que se borre del repostorio
```
    git rm --cached nombre_archivo
    git rm -r --cached nombre_directorio {caso de ser un directorio entero}
    git commit -m 'Eliminados archivos o directorio no deseados'
```

# Token

> Una vez aceptada la invitacion de colaboración

1. Ir a tu Email asociado a tu GitHub
2. Buscar el correo de invitación
3. Te redireccionara a tu GitHub
4. Selecciona *Accept invitation*

- Clonar el repositorio de github.

> Si te sale fatal: Authentication failed y te pida generar un token

1. Ir a tu GitHub
2. Ir a *Settings*
3. Ir a *Developent Settings*
4. Ir a *Personal Access token*
5. Seleccionar *Generar New Token*
6. Especificar en Notes para que es el token
7. Determinar fecha de expiración
8. Marcar la primera casilla y de ser necesaria algun otra tambien marcarla
9. Seleccionar *Generate token*
10. Copiar el token o escribirlo es como una contraseña y se muestra solo una vez por lo que debes guardalo en algun lado
11. Al hacer git clone por HTTPS te pedira tu usuario de GitHub y en Password deberas poner el token que copiaste asi se establecera la conexion remota y esto se te pedira cada vez que realices alguna accion de local a remoto pidiendote el usuario y contraseña donde contraseña usaras el token

```
    $ git clone https://github.com/<name-user-repository>/<name-repository>.git
    $ git pull    
```

- Listar las ramas (local y remotas).
```
    $ git branch
    $ git branch -rv
```

# Crear Repo Remoto

- Crear un repositorio remoto en github y agregarlo.

1. Ir a tu GitHub
2. En tu logo al lado hay un + donde seleccionar **New Repository**
3. Ponerles un Nombres y Descripcion. Seleccionar si publico o privado. Luego crear y listo.

**Nota 1:** GitHub ya nos da info para **push an existing repository from the command line**

**Nota 2:** origin es el <nombre del repositorio remoto> por convencion, aunque podria ser cualquier otro nombre

**Nota 3:** **git branch -M main** cambia el nombre de la rama principal por lo general llamada master por otra llamada main, a veces es necesario.

```
    $ git remote add origin https://github.com/<usuario git hub>/<nombre del repositorio creado en github>.git
```

**Observacion Importante:** Si tienes obtienes la salida por terminal:
    
    fatal: Authentication failed for 'https://github.com/<usuario git hub>/<nombre del repositorio creado en github>.git/'

Entonces lo mas seguro es que tengas mal configurado el user y el email por lo tanto debes modificarlos exactamente igual
al user name del GitHub y el user email del GitHub. O sea al email y usuario que registras para ingresar a GitHub, esto es:
```
    $ git config user.name "<nombre del usuario de GitHub>"
    $ git config user.mail "<nombre del mail de GitHub>"
    $ git config user.email "<nombre del mail de GitHub>"
```

De ahi que al hacer push te pedira elegir la opcion de token personal(debes hacer por el GitHub) o usar el navegador predeterminado
en el cual ingresas tu usario y email de GitHub y aceptas la conexion remota.

**Nota:** Mas facil es hacerte un SSH, ademas es mas seguro que usar HTTPS

# Añadir Colaborador

1. Ir a GitHub
2. Ir a *Your Repositories*
3. Seleccionar el Repositorio
4. Seleccionar la pestaña *Settings*
5. Seleccionar *Collaborators* debajo de Access
6. Ingresar Contraseña de GitHub si lo pide
7. Seleccionar *Add People* debajo de Manage Access
8. Buscamos username, full-name, email de la persona en GitHub que queremos que colabore con el repositorio
9. Le enviamos la solicitud

# Tag

- Generar el tag “v1.0” y subirlo al repositorio remoto.
```
    $ git tag v1.0 -m “v1.0”
    $ git push origin v1.0
```

**Nota:**

Cuando hablamos de Git tag no nos referimos a la versión de un archivo en particular, sino de todo el proyecto de manera global. Sirve para etiquetar con un tag el estado del repositorio completo, algo que se suele hacer cada vez que se libera una nueva versión del software.

> Mas Detalles: [Especificar versiones en Git con tag](https://desarrolloweb.com/articulos/especificar-versiones-git-tag.html#:~:text=Cuando%20hablamos%20de%20Git%20tag,una%20nueva%20versi%C3%B3n%20del%20software.)

## Git si no quieres perder los cambios hechos y debes hacer algo con el ultimo commmit trabajado

+ Guarda los cambios que no han sido commitiados

+ Los stash se guardan en forma de pila comenzando desde 0,1,2,...

+ Usamos save para ponerle un nombre al stash guardado

```
  $ git status
    modified: ...
  $ git stash save "name-del-stash"
    stash@{0}: WIP on master: 96d5004
  $ git status
    nothing to commit, working tree clean
``` 
+ Muestra la lista de stash guardados

```
  $ git stash list
    stash@{0}: WIP on master: 96d5004
```

+ Desapilar el stash y que vuelvan los cambios

```
  $ git stash apply
```
  ,ó ,
```
  $ git stash pop stash@{<numero-de-cambio-guardado>}
```

# Git si hiciste cambios que quieres esten en el actual commit y no en uno nuevo

```
  $ git status
    modified : <algun cambio de algun/algunos archivos>
  $ git add .
  $ git commit --amend
```

# Git ignore
  El archivo .gitignore es un archivo de texto que le dice a Git que archivos o carpetas ignoras en un proyecto
  Puede ser de manera global o local
  
 + Local
    - Se coloca en el directorio raiz del proyecto
    - Crea un archivo .gitignore
    - Editamos el archivo segun sea necesario
    - Cada nueva linea debe incluir un archivo o carpeta adicional que quieras que Git ignore
  
  + Global
    - Para agregar o cambiar tu .gitignore global, ejecuta el siguiente comando en la terminal:
  ```
    git config --global core.excludesfile ~/.gitignore_global
  ```
  
  + Las entradas de este archivo también pueden seguir un patrón coincidente:
      * \*se utiliza como una coincidencia comodín
      * / se usa para ignorar las rutas relativas al archivo .gitignore
      * # es usado para agregar comentarios
  
  + Ejemplos
```
    # Ignora archivos del sistema Mac 
    .DS_store

    # Ignora la carpeta node_modules
    node_modules

    # Ignora todos los archivos de texto
    *.txt

    # Ignora los archivos relacionados a API keys
    .env

    # Ignora archivos de configuración SASS
    .sass-cache
```
