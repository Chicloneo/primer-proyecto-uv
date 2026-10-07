# Creación de mi primer proyecto con uv

## ¿Qué es uv?

`uv` es un gestor de proyectos y librerías de Python.

## ¿Por qué usarlo?

Es la herramienta más rápida y eficiente del mercado actualmente. Sustituye a `pip` y `conda`.

## ¿Qué ventajas tiene?
Permite crear la estructura moderna de proyecto vista en clase:
```text
mi-proyecto-ia/
├── README.md
├── pyproject.toml
├── uv.lock
├── .gitignore
├── .env.example
├── src/
│   └── app/
│       ├── __init__.py
│       └── inference.py
├── tests/
│   └── test_inference.py
└── notebooks/
    └── exploracion.ipynb
```
Además gestiona las librerías Python de manera eficiente evitando que haya conflictos entre las versiones. Ej: versión de Pandas incompatible con versión de NumPy.

También puede crear un entorno virtual cada proyecto ocupando poca memoria.

## Paso 1

Vamos a crear el proyecto desde la terminal. En mi caso se trata de un Mac.

EL primer paso es buscar el lugar donde queremos crear el proyecto.

Iniciamos la terminal y preguntamos "dónde estamos" con `pwd` (print working directory)

```bash
santiago@Santiagos-MacBook-Pro ~ % pwd
/Users/santiago
```

Pedimos la lista de carpetas con `ls` (list).

```bash
santiago@Santiagos-MacBook-Pro ~ % ls
Desktop         Documents       Downloads       Library         Movies          Music           Pictures        Postman         Public
```

Nos movemos a `Desktop` con `cd` (change directory) y observamos que ahora aparece `Desktop` en la ruta.

```bash
santiago@Santiagos-MacBook-Pro ~ % cd Desktop
santiago@Santiagos-MacBook-Pro Desktop % 
```

Vamos a crear nuestro proyecto `primer-proyecto-uv` en el escritorio, pero podría ser cualquier otra, como `MUIAAp/Operación_de_Modelos`. Lo hacemos con `mkdir` (make directory). Con `ls` se puede ver que el proyecto está entre los archivos del escritorio.

```bash
santiago@Santiagos-MacBook-Pro Desktop % mkdir primer-proyecto-uv
```

## Paso 2

Hasta ahora solamente hemos creado una carpeta. Accedemos a ella.

```bash
santiago@Santiagos-MacBook-Pro Desktop % cd primer-proyecto-uv
santiago@Santiagos-MacBook-Pro primer-proyecto-uv % 
```

Creamos un repositorio local.

```bash
santiago@Santiagos-MacBook-Pro primer-proyecto-uv % git init   
Initialized empty Git repository in /Users/santiago/Desktop/primer-proyecto-uv/.git/
```

Los archivos cuyo nombre empiezan por un punto `.` están ocultos.

Creamos la estructura con el comando `uv init`.

```bash
santiago@Santiagos-MacBook-Pro primer-proyecto-uv % uv init --package --vcs none
Initialized project `primer-proyecto-uv`
```

`--package` Le dice a uv que cree una estructura de paquete redistribuible. Según la documentación oficial de uv, _Sets up the project to be built as a Python package. Defines a [build-system] for the project. This is the default behavior._

`--vcs none` Le indica a uv que no cree un repositorio Git, ya que acabamos de crearlo manualmente.

El comando `ls -la` (list long version all) muestra los archivos dentro de `primer-proyecto-uv`, incluso los ocultos.

Actualmente tiene la siguiente estructura:

```text
primer-proyecto-uv/
├── README.md
├── pyproject.toml
├── .git
├── .python-version
├── src/
    └── primer_proyecto_uv/
        ├── __init__.py
```

`uv` cambia por defecto los guines de `primer_proyecto-uv` a guiones bajos en `primer_proyecto_uv`.

Además, `__init__.py` es necesario para poder importar clases o funciones del proyecto desde otros directorios. Este es creado por defecto, pero si creamos subcarpetas, debemos crearlo manualmente nosotros. Está vacío.

## Paso 3

No hace falta crear el entorno virtual y activarlo manualmente cada vez que lo queramos utilizar.

Basta con que añadamos la librería con la que queremos trabajar

```bash
uv add pandas
```

y aparece nuestro entorno virtual `.venv`. Además, cada vez que entremos a este proyecto, uv activa el entorno virtual por defecto.

### ¡Ojo!

Debemos añadir la carpeta `.venv/` a nuestro archivo `.gitignore` (esto es, los archivos que no queremos commitear -puedes pedirle a la IA que te cree uno completo). El entorno virtual está creado específicamente para nuestro ordenador, así que un usuario externo que descargue el proyecto no podrá activarlo. Por eso son importantes los archivos `.pyproject.toml` y `uv.lock`, que indican qué librerías y qué versiones son necesarias para el proyecto (como un `requirements.txt`).

## Paso 4

¿Cómo ejecutar un archivo Python con uv? Supongamos que tenemos el proyecto

```text
```text
primer-proyecto-uv/
├── README.md
├── pyproject.toml
├── .git
├── .python-version
├── src/
    └── primer_proyecto_uv/
        ├── __init__.py
        ├── main.py
```

y queremos ejecutar `main.py`. Lo hacemos con el comando

```bash
uv run python main.py
```