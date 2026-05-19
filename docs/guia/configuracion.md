# Configuración

Esta página documenta detalladamente el proceso seguido para configurar el entorno de desarrollo, crear la documentación con MkDocs y desplegarla en GitHub Pages.

---

## 1. Instalación de Python

Se descargó Python 3.11 desde [python.org](https://www.python.org/downloads/). Durante la instalación en Windows, se marcó la opción **"Add Python to PATH"** para poder usar `python` desde cualquier terminal.

**Verificación:**
```bash
python --version
# Python 3.11.x
```

**Decisión tomada**: se eligió Python 3.11 por ser la versión estable más reciente en el momento de la práctica y garantizar compatibilidad con MkDocs.

---

## 2. Creación del Directorio y Entorno Virtual

```bash
mkdir mi-documentacion
cd mi-documentacion
python -m venv venv
```

Activación del entorno virtual:

- **Windows**: `venv\Scripts\activate`
- **Linux/Mac**: `source venv/bin/activate`

**¿Por qué usar un entorno virtual?** Aislar las dependencias del proyecto evita conflictos con otras instalaciones de Python en el sistema. Es una buena práctica en cualquier proyecto Python.

---

## 3. Instalación de MkDocs y el Tema Material

```bash
pip install mkdocs mkdocs-material
```

**Decisión tomada**: se eligió el tema `material` por su diseño moderno, su soporte para navegación por pestañas y su amplia documentación.

---

## 4. Inicialización del Proyecto MkDocs

```bash
mkdocs new .
```

Esto generó automáticamente:
- `mkdocs.yml`: archivo de configuración principal.
- `docs/index.md`: página de inicio de la documentación.

---

## 5. Configuración de `mkdocs.yml`

Se editó el archivo para activar el tema Material y sus características de navegación:

```yaml
site_name: Mi Documentación
theme:
  name: material
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.expand
    - content.code.copy
```

**Decisión tomada**: se activaron `navigation.tabs` y `navigation.sections` para organizar la documentación en secciones claramente diferenciadas, y `content.code.copy` para facilitar la copia de fragmentos de código.

---

## 6. Estructura de la Documentación

Se creó la siguiente estructura en la carpeta `docs/`:

```
docs/
├── index.md
├── guia/
│   ├── instalacion.md
│   ├── configuracion.md
│   └── despliegue.md
└── ejemplos/
    └── ejemplo1.md
```

Cada archivo fue redactado en Markdown con contenido sobre Python.

---

## 7. Creación del Repositorio en GitHub

Desde Visual Studio Code:

1. Se inicializó el repositorio con *Source Control → Initialize Repository*.
2. Se creó el archivo `.gitignore` con el contenido `venv/` para excluir el entorno virtual.
3. Se realizó el primer commit y se publicó en GitHub con *Publish to GitHub*.

**Problema encontrado**: al intentar hacer push sin configurar el email de Git, apareció un error. Se solucionó ejecutando:
```bash
git config --global user.email "tu@email.com"
git config --global user.name "Tu Nombre"
```

---

## 8. Configuración de GitHub Actions

Se creó el archivo `.github/workflows/deploy.yml`:

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

Este workflow se ejecuta automáticamente en cada push a `main` y despliega la documentación en la rama `gh-pages`.

---

## 9. Permisos de GitHub Actions

En **Settings → Actions → General → Workflow permissions** se seleccionó **"Read and write access"**.

**¿Por qué es necesario?** Sin este permiso, el workflow no puede hacer push a la rama `gh-pages` y el despliegue falla con un error de permisos (exit code 1).

---

## 10. Configuración de GitHub Pages

En **Settings → Pages**:
- *Source*: Deploy from a branch
- *Branch*: `gh-pages`

---

## 11. Despliegue Final

```bash
git add .
git commit -m "Configuración de GitHub Pages"
git push origin main
```

Se verificó el despliegue en la pestaña **Actions** del repositorio. Tras unos 30-60 segundos, la documentación quedó disponible en:

```
https://tu-usuario.github.io/tu-repositorio
```

---

## Conclusiones

El proceso fue fluido en general. El único problema destacable fue el error de permisos en GitHub Actions, que se resolvió activando el acceso de lectura y escritura. MkDocs con el tema Material ofrece un resultado muy profesional con una configuración mínima.
