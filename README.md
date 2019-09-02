# CC-4

Página del curso de CC-4 construida utilizando MkDocs

## Instalación

```shell
pip install -r requirements.txt
```

Luego generar un ***Personal Access Token*** de GitHub utilizando el siguiente [link](https://github.com/settings/tokens). Este token solo debería de habilitarse con las opciones: `public_repo` y `repo:status`. En el archivo de configuración de la terminal, por ejemplo `.bashrc` agregar lo siguiente:

```shell
# reemplazar <token> con el hex string
export MKDOCS_GIT_COMMITTERS_APIKEY=<token>
```

Luego hacer `source` al archivo:

```shell
source ~/.bashrc
```

## Deploy

Para construir la página utilizar lo siguiente

```shell
mkdocs build
```

el contenido generado en la carpeta `site/` copiarlo en el repositorio cc-4.github.io


## Serve

Para probar la página en un servidor local

```shell
mkdocs serve
```
