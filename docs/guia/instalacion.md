# Guía de Instalación

Esta sección explica cómo instalar Python en los sistemas operativos más comunes.

## Requisitos Previos

- Conexión a Internet
- Permisos de administrador en el sistema
- Al menos 200 MB de espacio en disco

## Instalación en Windows

1. Visita [python.org/downloads](https://www.python.org/downloads/) y descarga el instalador más reciente.
2. Ejecuta el instalador `.exe`.
3. **Importante**: marca la casilla **"Add Python to PATH"** antes de continuar.
4. Haz clic en *Install Now*.
5. Verifica la instalación abriendo la terminal y ejecutando:

```bash
python --version
```

## Instalación en macOS

Usa [Homebrew](https://brew.sh/) para instalar Python de forma sencilla:

```bash
brew install python
```

O descarga el instalador oficial desde [python.org](https://www.python.org/downloads/macos/).

## Instalación en Linux (Ubuntu/Debian)

Python suele venir preinstalado. Para instalarlo o actualizarlo:

```bash
sudo apt update
sudo apt install python3 python3-pip
```

Comprueba la versión instalada:

```bash
python3 --version
```

## Verificar la Instalación

Una vez instalado, abre una terminal y ejecuta:

```bash
python --version
pip --version
```

Deberías ver algo similar a:

```
Python 3.11.4
pip 23.2.1
```

## Solución de Problemas

| Problema | Solución |
|---|---|
| `python` no se reconoce | Añadir Python al PATH manualmente |
| Versión desactualizada | Descargar la última versión desde python.org |
| `pip` no encontrado | Instalar con `python -m ensurepip --upgrade` |
