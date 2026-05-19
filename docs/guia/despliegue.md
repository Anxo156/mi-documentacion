# Despliegue en GitHub Pages

Esta guía explica cómo desplegar un proyecto Python (o su documentación) en GitHub Pages usando MkDocs y GitHub Actions.

## Prerrequisitos

- Cuenta en [GitHub](https://github.com)
- Git instalado y configurado
- MkDocs instalado (`pip install mkdocs mkdocs-material`)

## Paso 1: Preparar el Repositorio

Inicializa Git en tu proyecto y realiza el primer commit:

```bash
git init
git add .
git commit -m "Primer commit"
git branch -M main
git remote add origin https://github.com/tu-usuario/tu-repositorio.git
git push -u origin main
```

## Paso 2: Configurar GitHub Actions

Crea el archivo `.github/workflows/deploy.yml`:

```yaml
name: Deploy MkDocs

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: '3.x'
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

## Paso 3: Permisos de GitHub Actions

1. Ve a **Settings → Actions → General** en tu repositorio.
2. En *Workflow permissions*, selecciona **Read and write access**.
3. Guarda los cambios.

## Paso 4: Configurar GitHub Pages

1. Ve a **Settings → Pages**.
2. En *Source*, selecciona **Deploy from a branch**.
3. Elige la rama **gh-pages** y guarda.

## Paso 5: Publicar

Haz push a `main` para disparar el workflow automáticamente:

```bash
git add .
git commit -m "Despliegue documentación"
git push origin main
```

Tu documentación estará disponible en:

```
https://tu-usuario.github.io/tu-repositorio
```

!!! tip "Consejo"
    El primer despliegue puede tardar entre 30 y 60 segundos. Revisa el estado en la pestaña **Actions** del repositorio.
