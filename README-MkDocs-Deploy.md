# 📘 GitHub Actions: Deploy MkDocs a GitHub Pages

Este `README.md` documenta un workflow de GitHub Actions para desplegar documentación usando [MkDocs](https://www.mkdocs.org/) (tema `material` o cualquier otro) en GitHub Pages, **sin usar `requirements.txt`**, con explicaciones detalladas y enlaces útiles.

---

## 🚀 ¿Qué hace este workflow?

1. Corre cuando hacés `push` al branch `master`.
2. Usa un runner `ubuntu-latest`.
3. Instala Python 3.11.
4. Instala MkDocs y los plugins necesarios vía `pip`.
5. Genera el sitio estático con `mkdocs build`.
6. Publica el sitio en el branch `gh-pages` usando [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages).

---

## 📄 Archivo `.github/workflows/deploy.yml`

```yaml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches:
      - master

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:

      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install mkdocs mkdocs-material mkdocs-cinder

      - name: Build site
        run: mkdocs build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site
```

---

## 🔐 Sobre `${{ secrets.GITHUB_TOKEN }}`

GitHub proporciona este token de forma automática en todos los workflows.

- No tenés que crearlo manualmente.
- Tiene permisos temporales para hacer push, pull, etc.
- Asegurate de tener activada la opción:

**Settings → Actions → General → Workflow permissions → `Read and write permissions`**

[Más info sobre `GITHUB_TOKEN`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)

---

## 📂 Ignorá el directorio `site/`

Agregá esto a tu `.gitignore`:

```
# MkDocs
/site/
```

---

## 🛠️ Consejos adicionales

### ✅ Usar `--strict` para detectar errores

```yaml
- name: Build site
  run: mkdocs build --strict
```

Hace que el build falle si hay enlaces rotos, referencias inválidas, etc.

---

### ✅ Fijar versiones (opcional)

```bash
pip install mkdocs==1.6.0 mkdocs-material==9.5.19
```

Esto evita sorpresas cuando se actualicen paquetes.

---

### ✅ Agregar commit message personalizado

```yaml
commit_message: "Deploy site: ${{ github.sha }}"
```

---

### ✅ Usar caché de pip (opcional)

```yaml
- name: Cache pip
  uses: actions/cache@v4
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-mkdocs
```

---

## 📚 Enlaces útiles

- [MkDocs](https://www.mkdocs.org/)
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages](https://pages.github.com/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages)
- [Lista de runners compatibles (`runs-on`)](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners)

---

## 💬 Autor

Este template fue armado por un Sysadmin DevSecOps que ama los workflows bien hechos 🤘🏼

¡Documentá o morirás!

---

## 📦 Opcional: Usar `requirements.txt`

Si preferís manejar tus dependencias de Python de forma más explícita, podés usar un archivo `requirements.txt`.

### 🔧 Ejemplo de `requirements.txt`

```txt
mkdocs
mkdocs-material
mkdocs-cinder
mkdocs-awesome-pages-plugin
```

Podés fijar versiones para mayor estabilidad:

```txt
mkdocs==1.6.0
mkdocs-material==9.5.19
```

Guardá este archivo en la raíz del repositorio.

---

### 🔄 Actualizar dependencias

Para generar o actualizar tu `requirements.txt`, usá:

```bash
pip freeze > requirements.txt
```

Usalo con cuidado: puede incluir paquetes innecesarios del entorno local.

---

### 🧪 Actualizar el workflow

Reemplazá el paso `pip install` en línea por:

```yaml
- name: Install dependencies
  run: pip install -r requirements.txt
```

Esto garantiza que se instalen exactamente las versiones listadas.

---

### 💡 Beneficios de `requirements.txt`

✅ Manejo de dependencias más claro en equipos  
✅ Tu workflow es más limpio y mantenible  
✅ Mejor control de versiones  
✅ Permite cacheo por hash del archivo

---

### ⚠️ Cuándo no usarlo

- Si solo usás algunos paquetes y preferís control total en el `.yml`.
- Si tu proyecto cambia seguido y preferís instalar directo con `pip`.

---

🔗 [Más sobre `pip install -r`](https://pip.pypa.io/en/stable/cli/pip_install/#requirements-file-format)

---

#### Ejemplo

File ***"requirements.txt"***

```python
# requirements.txt - Dependencies for MkDocs project

mkdocs==1.6.0
mkdocs-material==9.5.19
mkdocs-cinder==1.0.0

# Plugins adicionales que podrías usar:
# mkdocs-awesome-pages-plugin==2.9.1
# mkdocs-macros-plugin==0.6.0
# mkdocs-i18n==0.1.1

# Si usás Python >=3.11, revisá la compatibilidad de los plugins.

# Para actualizar esta lista, usar:
# pip freeze > requirements.txt
```

---
