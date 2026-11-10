# Guía Rápida: Configuración de Entornos en el Servidor (Conda)

Para evitar problemas de permisos al instalar librerías en YUCA, trabajaremos dentro de un entorno aislado usando Conda. Asumiendo que ya estás conectado y tienes la sesión abierta en VS Code, sigue estos pasos:

## 1. Abrir la terminal

Abre la terminal integrada de VS Code. Puedes hacerlo desde el menú superior en **Terminal > New Terminal**, o usando el atajo de teclado `Ctrl + ñ` (o `` Ctrl + ` `` dependiendo de la configuración de tu teclado).

## 2. Crear el entorno

*(Este paso solo necesitas hacerlo la primera vez)*.
En la terminal, ejecuta el siguiente comando para crear un entorno llamado `entorno_ml` con Python 3.10:

```
conda create --name entorno_ml python=3.10 -y

```

En lugar de `entorno_ml` puedes darle el nombre que prefieras (sin espacios).


## 3. Activar e instalar librerías

Activa tu nuevo entorno ejecutando:

```
conda activate entorno_ml

```

Recuerda usar el mismo nombre que en el paso anterior.

*Sabrás que funcionó porque el texto `(entorno_ml)` aparecerá al inicio de tu línea de comandos.*

Ahora, con el entorno activo, instala las herramientas del curso:

```
pip install numpy pandas seaborn scikit-learn matplotlib

```

Es muy importante instalar el soporte para los GPUs:
```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.3
```

## 4. Seleccionar el entorno en tus Notebooks

Para usar estas librerías en tus archivos de Jupyter (`.ipynb`), el proceso es muy sencillo:

1. Abre tu notebook.

2. **Intenta ejecutar cualquier celda de código** (con el botón de "Play" a la izquierda de la celda o presionando `Shift + Enter`).

3. VS Code pausará la ejecución y te mostrará un menú desplegable en la parte superior pidiéndote seleccionar un entorno (o *Kernel*).

4. Selecciona **Python Environments** (Entornos de Python) y elige el que dice **`entorno_ml`** (el nombre que le hayas dado).

> **¿Qué pasa si no aparece o hay un error?**
> 
> Si el entorno `entorno_ml` no aparece en la lista al intentar ejecutar la celda, es porque VS Code aún no ha refrescado los directorios. Simplemente **cierra la pestaña de tu notebook y vuélvela a abrir**, y vuelve a intentar ejecutar la celda.

---

Es imporante que tengas un entorno por cada proyecto en el que trabajes, en el caso del curso, bastará con un sólo entorno.
