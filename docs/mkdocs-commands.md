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
INFO    -  Building documentation to directory: PATH-TO-REPOS\rappalini-com-ar\site
```







mkdocs gh-deploy
INFO    -  Cleaning site directory
INFO    -  Building documentation to directory: C:\Users\pablo.rappalini\0-REPOS\rappalini-com-ar\site
INFO    -  Documentation built in 0.30 seconds
WARNING -  Version check skipped: No version specified in previous deployment.
INFO    -  Copying 'C:\Users\pablo.rappalini\0-REPOS\rappalini-com-ar\site' to 'gh-pages' branch and pushing to GitHub.
Enumerating objects: 74, done.
Counting objects: 100% (74/74), done.
Delta compression using up to 12 threads
Compressing objects: 100% (68/68), done.
Writing objects: 100% (74/74), 2.22 MiB | 1.34 MiB/s, done.
Total 74 (delta 6), reused 10 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (6/6), done.
remote: 
remote: Create a pull request for 'gh-pages' on GitHub by visiting:
remote:      https://github.com/PRappalini/rappalini-com-ar/pull/new/gh-pages
remote: 
To https://github.com/PRappalini/rappalini-com-ar.git
 * [new branch]      gh-pages -> gh-pages
INFO    -  Your documentation should shortly be available at: https://PRappalini.github.io/rappalini-com-ar/


