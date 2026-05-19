# Ejemplo Práctico: Script de Gestión de Tareas

Este ejemplo muestra cómo crear un pequeño gestor de tareas en Python usando solo la librería estándar.

## Código

```python title="gestor_tareas.py"
tareas = []

def agregar_tarea(nombre: str) -> None:
    """Añade una nueva tarea a la lista."""
    tareas.append({"nombre": nombre, "completada": False})
    print(f"✅ Tarea añadida: {nombre}")

def listar_tareas() -> None:
    """Muestra todas las tareas con su estado."""
    if not tareas:
        print("No hay tareas registradas.")
        return
    for i, tarea in enumerate(tareas, start=1):
        estado = "✔" if tarea["completada"] else "✗"
        print(f"{i}. [{estado}] {tarea['nombre']}")

def completar_tarea(indice: int) -> None:
    """Marca una tarea como completada."""
    if 1 <= indice <= len(tareas):
        tareas[indice - 1]["completada"] = True
        print(f"🎉 Tarea {indice} completada.")
    else:
        print("Índice no válido.")

# --- Uso del gestor ---
agregar_tarea("Instalar Python")
agregar_tarea("Crear entorno virtual")
agregar_tarea("Subir proyecto a GitHub")

listar_tareas()

completar_tarea(1)
completar_tarea(2)

print("\nEstado actualizado:")
listar_tareas()
```

## Salida esperada

```
✅ Tarea añadida: Instalar Python
✅ Tarea añadida: Crear entorno virtual
✅ Tarea añadida: Subir proyecto a GitHub
1. [✗] Instalar Python
2. [✗] Crear entorno virtual
3. [✗] Subir proyecto a GitHub
🎉 Tarea 1 completada.
🎉 Tarea 2 completada.

Estado actualizado:
1. [✔] Instalar Python
2. [✔] Crear entorno virtual
3. [✗] Subir proyecto a GitHub
```

## Conceptos utilizados

- **Listas y diccionarios**: estructura de datos fundamental en Python.
- **Funciones con anotaciones de tipo**: mejoran la legibilidad del código.
- **f-strings**: formato moderno para interpolación de cadenas.
- **Enumerate**: iteración con índice automático.
