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

- Building documentation to directory: PATH-TO-REPOS\rappalini-com-ar\site
- Copying 'PATH-TO-REPOS\rappalini-com-ar\site' to 'gh-pages' branch and pushing to GitHub.
- remote: Create a pull request for 'gh-pages' on GitHub by visiting:
remote:      https://github.com/PRappalini/rappalini-com-ar/pull/new/gh-pages

To https://github.com/PRappalini/rappalini-com-ar.git

[new branch]      gh-pages -> gh-pages

[Your Site](https://PRappalini.github.io/rappalini-com-ar/)

## CHEQUEAR CONFIGURACION DE MI GUTHUB SITE

https://github.com/PRappalini/rappalini-com-ar/settings/pages

---

I´m creating a github page using mkdocs, for Ford Documentation. When I use "blue" as a color, is a light blue, not "Ford blue". how can I change this:
palette: 
    - media: "(prefers-color-scheme: light)"
        scheme: default primary: blue

*Google Gemini2.5 Flash*

You're encountering this because the blue specified in the palette setting for MkDocs Material theme refers to a predefined shade of blue within the theme's palette, not a specific brand color like "Ford blue." To use an exact "Ford blue," you'll need to define a custom color using CSS.

Here's how you can achieve this:

1. Find the "Ford Blue" Hex Code There are a few variations of "Ford Blue," but a commonly cited hex code for "Ford's Blue color" is $$#003478$$. This is a dark, rich blue that aligns with the brand's identity. Another often mentioned "Ford Blue" is $$#2C3968$$. I will use $$#003478$$ for this example.

2. Modify your mkdocs.yml file You need to tell MkDocs Material that you're using a custom primary color. Change your mkdocs.yml to set primary: custom and include an extra_css entry that links to your custom stylesheet.

Your mkdocs.yml should look something like this:

yaml

theme:
  name: material
  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: custom # Change 'blue' to 'custom'
      accent: blue # You can keep this or change it too
  extra_css:
    - stylesheets/extra.css # Link to your custom CSS file
3. Create your Custom CSS File Create a new directory named stylesheets inside your docs folder (e.g., docs/stylesheets/). Inside this stylesheets folder, create a file named extra.css.

Add the following CSS to docs/stylesheets/extra.css:

css

:root {
  /* Set the primary foreground color to Ford Blue */
  --md-primary-fg-color: #003478;

  /* You might also want to adjust other primary color shades for consistency.
     These are examples, you can fine-tune them based on how they look. */
  --md-primary-fg-color--light: #004D99; /* A lighter shade for hover/active states */
  --md-primary-fg-color--dark: #002652;  /* A darker shade for accents */

  /* If you want to change the link color to match, you can use: */
  --md-typeset-a-color: #003478;
}
Explanation:

primary: custom: This tells MkDocs Material that the primary color will not be one of its built-in names, but rather defined externally.
extra_css: - stylesheets/extra.css: This line tells MkDocs to include your extra.css file in the generated site.
:root { ... }: This CSS selector targets the root element of your HTML document, allowing you to define global CSS variables.
--md-primary-fg-color: This is the CSS variable that MkDocs Material uses for the main primary color (e.g., header, sidebar active links). By setting its value to $$#003478$$, you apply your desired "Ford blue."
--md-primary-fg-color--light and --md-primary-fg-color--dark: These are used for variations of the primary color, such as hover states or slightly different shades for certain elements. It's good practice to define these as well for a cohesive look.
--md-typeset-a-color: This variable controls the color of hyperlinks within your documentation.
After making these changes, rebuild your MkDocs site, and you should see the "Ford blue" applied as your primary color. Remember to clear your browser cache if the changes don't appear immediately.