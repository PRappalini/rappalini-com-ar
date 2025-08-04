# Welcome to Rappalini

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## INSTALATION

### Instalar pip para python 3

```bash
sudo apt install python3-pip -y 
```

### Crear un entorno virtual en la carpeta .venv y Activarlo (SOLO EN DEBIAN y derivados)

```bash
python3 -m venv .venv && source .venv/bin/activate
```

### Instalar MkDocs, el tema Material y el tema Cinder

```bash
pip install mkdocs mkdocs-material mkdocs-cinder
```

## EDITAR A GUSTO LOS ARCHIVOS

### PROBARLO LOCAL

```bash
mkdocs serve
```

[Sitio Local](localhost:8000)

### Generar el sitio estático Desde la raíz del proyecto

```bash
mkdocs build
# Respuesta:
# INFO    -  Building documentation to directory: PATH-TO-REPOS\rappalini-com-ar\site
```

### Subir el sitio estático a GitHub en el branch gh-pages

#### Manual

Creás el branch *gh-pages*

Subís el contenido de **site/** a ese branch (raíz del branch, no en una carpeta)

En GitHub configurás que Pages sirva desde gh-pages branch / root

#### Automático con mkdocs

```bash
mkdocs gh-deploy
```

**Respuesta:**

INFO    -  Building documentation to directory: PATH-TO-REPOS\rappalini-com-ar\site
INFO    -  Copying 'PATH-TO-REPOS\rappalini-com-ar\site' to 'gh-pages' branch and pushing to GitHub.
remote: Create a pull request for 'gh-pages' on GitHub by visiting:
remote:      https://github.com/PRappalini/rappalini-com-ar/pull/new/gh-pages

To https://github.com/PRappalini/rappalini-com-ar.git

[new branch]      gh-pages -> gh-pages

[Your documentation should shortly be available at:](https://PRappalini.github.io/rappalini-com-ar/)

