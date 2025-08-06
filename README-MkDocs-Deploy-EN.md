# 📘 GitHub Actions: Deploy MkDocs to GitHub Pages

This `README.md` documents a GitHub Actions workflow to deploy documentation using [MkDocs](https://www.mkdocs.org/) (with the `material` theme or others) to GitHub Pages, **without using `requirements.txt`**, with detailed explanations and helpful links.

---

## 🚀 What does this workflow do?

1. Triggers on `push` to the `master` branch.
2. Uses the `ubuntu-latest` runner.
3. Installs Python 3.11.
4. Installs MkDocs and required plugins using `pip`.
5. Builds the static site with `mkdocs build`.
6. Publishes the site to the `gh-pages` branch using [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages).

---

## 📄 File: `.github/workflows/deploy.yml`

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

## 🔐 About `${{ secrets.GITHUB_TOKEN }}`

GitHub automatically provides this token in all workflows.

- You don't need to create it manually.
- It has temporary permissions to push, pull, etc.
- Make sure to enable:

**Settings → Actions → General → Workflow permissions → `Read and write permissions`**

[More about `GITHUB_TOKEN`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)

---

## 📂 Ignore the `site/` directory

In your `.gitignore`:

```
# MkDocs
/site/
```

---

## 🛠️ Additional tips

### ✅ Use `--strict` to catch issues

```yaml
- name: Build site
  run: mkdocs build --strict
```
This fails the build if there are broken links, invalid references, etc.

---

### ✅ Pin versions (optional)

```bash
pip install mkdocs==1.6.0 mkdocs-material==9.5.19
```
Avoid surprises from automatic package updates.

---

### ✅ Customize the deploy commit message

```yaml
commit_message: "Deploy site: ${{ github.sha }}"
```

---

### ✅ Use pip cache (optional)

```yaml
- name: Cache pip
  uses: actions/cache@v4
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-mkdocs
```

---

## 📚 Useful links

- [MkDocs](https://www.mkdocs.org/)
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages](https://pages.github.com/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages)
- [List of supported runners (`runs-on`)](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners)

---

## 💬 Author

This template was created by a DevSecOps Sysadmin who loves well-crafted workflows 🤘🏼

Document or perish!

---

## 📦 Optional: Using `requirements.txt`

If you prefer to manage your Python dependencies more explicitly, you can use a `requirements.txt` file.

### 🔧 Example `requirements.txt`

```txt
mkdocs
mkdocs-material
mkdocs-cinder
mkdocs-awesome-pages-plugin
```

You can freeze versions for better stability:

```txt
mkdocs==1.6.0
mkdocs-material==9.5.19
```

Place this file at the root of your repository.

---

### 🔄 Update dependencies

To generate or update your `requirements.txt`:

```bash
pip freeze > requirements.txt
```

Use this cautiously, as it may include unnecessary packages from your local environment.

---

### 🧪 Update your workflow

Replace the inline `pip install` step with:

```yaml
- name: Install dependencies
  run: pip install -r requirements.txt
```

This ensures all required packages are installed exactly as listed.

---

### 💡 Benefits of `requirements.txt`

✅ Easier dependency management across teams  
✅ Keeps your workflow DRY  
✅ Better version control  
✅ Enables caching strategies based on file hash

---

### ⚠️ When not to use it

- If you only use a few packages and want full control in the workflow file.
- If your project changes frequently and you prefer direct `pip install`.

---

🔗 [More on `pip install -r`](https://pip.pypa.io/en/stable/cli/pip_install/#requirements-file-format)

---

#### Example Given

***File "requirements.txt"***

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
