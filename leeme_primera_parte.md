# Proyecto: UIII_Agencia_De_Marketing_0591

**Lenguaje:** Python
**Framework:** Django
**Editor:** Visual Studio Code

---

## Índice

1. Estructura inicial y nombres
2. Procedimientos (paso a paso)

   * 1 Crear carpeta del proyecto
   * 2 Abrir VS Code en la carpeta
   * 3 Abrir terminal en VS Code
   * 4 Crear entorno virtual `.venv`
   * 5 Activar el entorno virtual
   * 6 Activar intérprete de Python en VS Code
   * 7 Instalar Django
   * 8 Crear proyecto `backend_agencia_de_marketing` sin duplicar carpeta
   * 9 Ejecutar servidor en el puerto `8591`
   * 10 Copiar y pegar el link en el navegador
   * 11 Crear aplicación `app_clientes`
   * 12 Realizar migraciones (makemigrations y migrate)
   * 13 Trabajar con el MODELO: `Cliente` (crear modelo y migrar)
   * 14 Vistas de `app_clientes` (funciones CRUD)
   * 15 Crear carpeta `templates` en `app_clientes` y archivos HTML
   * 16 Estructura de templates y ejemplos (`base.html`, `navbar.html`, etc.)
   * 17 Agregar Bootstrap en `base.html`
   * 18 Barra de navegación (`navbar.html`) con opciones e íconos
   * 19 Footer fijo con derechos de autor
   * 20 Página de inicio (`inicio.html`) con imagen desde la web
   * 21 Subcarpeta `cliente` en `app_clientes/templates`
   * 22 Archivos HTML para cliente (agregar, ver, actualizar)
   * 23 No usar `forms.py` (usar `request.POST`)
   * 24 `urls.py` en `app_clientes` y en proyecto
   * 25 Agregar `app_clientes` a `INSTALLED_APPS` en `settings.py`
   * 26 Registrar modelos en `admin.py` y migraciones de nuevo
   * 27 Solo trabajar con `Cliente` por ahora
   * 28 Estética: colores suaves y diseño sencillo
   * 29 Crear la estructura completa al inicio
   * 30 Proyecto totalmente funcional
   * 31 Ejecutar servidor en el puerto `8591` (repetido intencionalmente)
3. Código fuente (archivos clave)

   * `models.py` (solo `Cliente` por ahora)
   * `views.py` (funciones CRUD para clientes)
   * `app_clientes/urls.py`
   * `backend_agencia_de_marketing/urls.py`
   * `admin.py`
   * Templates: `base.html`, `navbar.html`, `footer.html`, `inicio.html`, `cliente/agregar_cliente.html`, `cliente/ver_clientes.html`, `cliente/actualizar_cliente.html`
4. Comandos Git y subir a GitHub (procedimiento y `.gitignore`)
5. Notas finales y recomendaciones

---

## 1. Estructura inicial recomendada (al terminar):

```
UIII_Agencia_De_Marketing_0591/
├─ .venv/                  # entorno virtual (oculto normalmente)
├─ backend_agencia_de_marketing/  # proyecto Django (contiene settings.py, urls.py)
│  ├─ backend_agencia_de_marketing/
│  │  ├─ __init__.py
│  │  ├─ settings.py
│  │  ├─ urls.py
│  │  └─ wsgi.py
│  └─ manage.py
├─ app_clientes/
│  ├─ migrations/
│  ├─ templates/
│  │  ├─ base.html
│  │  ├─ header.html
│  │  ├─ navbar.html
│  │  ├─ footer.html
│  │  ├─ inicio.html
│  │  └─ cliente/
│  │     ├─ agregar_cliente.html
│  │     ├─ ver_clientes.html
│  │     └─ actualizar_cliente.html
│  ├─ admin.py
│  ├─ apps.py
│  ├─ models.py
│  ├─ urls.py
│  └─ views.py
├─ .gitignore
└─ README.md
```

---

## 2. Procedimientos (paso a paso)

> **Nota:** algunos comandos cambian ligeramente entre Windows y macOS/Linux. Indico variantes cuando corresponde.

### 1) Crear carpeta del Proyecto: `UIII_Agencia_De_Marketing_0591`

En tu explorador de archivos o terminal crea la carpeta:

Linux / macOS / Windows PowerShell / CMD:

```bash
# en la carpeta donde quieras crear el proyecto:
mkdir UIII_Agencia_De_Marketing_0591
cd UIII_Agencia_De_Marketing_0591
```

### 2) Abrir VS Code sobre la carpeta `UIII_Agencia_De_Marketing_0591`

En terminal (desde dentro de la carpeta):

```bash
code .
```

O abre VS Code y usa `File > Open Folder...` y selecciona `UIII_Agencia_De_Marketing_0591`.

### 3) Abrir terminal en VS Code

* Atajo: `` Ctrl+` `` (control + la tecla de la tilde invertida)
* O `View > Terminal`.

### 4) Crear carpeta entorno virtual `.venv` desde terminal de VS Code

Recomendado crear el entorno virtual dentro de la carpeta del proyecto con nombre `.venv`:

Windows (PowerShell):

```powershell
python -m venv .venv
```

macOS / Linux:

```bash
python3 -m venv .venv
```

Esto crea la carpeta `.venv`.

### 5) Activar el entorno virtual

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
# si da error de ejecución, usar: Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Windows CMD:

```cmd
.\.venv\Scripts\activate
```

macOS / Linux:

```bash
source .venv/bin/activate
```

Verás el prompt cambiar a `(.venv)`.

### 6) Activar intérprete de Python (VS Code)

* Abre la paleta de comandos: `Ctrl+Shift+P`.
* Escribe `Python: Select Interpreter` y elige la que apunta a la ruta `.../UIII_Agencia_De_Marketing_0591/.venv/bin/python` (o `Scripts\python.exe` en Windows).

Esto asegura que VS Code use el entorno virtual para linting, ejecución y depuración.

### 7) Instalar Django

Con el entorno activado:

```bash
pip install --upgrade pip
pip install django
```

Puedes fijar una versión si deseas: `pip install django==4.2` (por ejemplo).

### 8) Crear proyecto `backend_agencia_de_marketing` sin duplicar carpeta

**Importante**: para evitar crear una carpeta anidada debes ejecutar `django-admin startproject` dentro de la carpeta raíz y usar `.` o crear una carpeta con el nombre del proyecto.

Opción A (crear carpeta del proyecto directamente — recomendado):

```bash
django-admin startproject backend_agencia_de_marketing .
```

El `.` al final crea los archivos del proyecto en la carpeta actual (evita una carpeta extra). Si prefieres tener una carpeta, omite el `.`.

> Si ya ejecutaste `startproject backend_agencia_de_marketing` y se creó otra carpeta con el mismo nombre dentro, borra la carpeta innecesaria y repite con `.` o mueve los archivos.

### 9) Ejecutar servidor en el puerto `8591`

Primero crea la app `app_clientes` (punto 11) y realiza migraciones antes de correr. Para correr inmediatamente:

```bash
python manage.py runserver 8591
```

Si `python` apunta a Python 2 en tu SO, usa `python3`.

### 10) Procedimiento para copiar y pegar el link en el navegador

La consola mostrará algo como `Starting development server at http://127.0.0.1:8591/`. Copia esa URL y pégala en tu navegador.

### 11) Crear aplicación `app_clientes`

Con el entorno activado y ubicado en la raíz del proyecto (donde está `manage.py`):

```bash
python manage.py startapp app_clientes
```

### 12) Procedimiento para realizar las migraciones (makemigrations y migrate)

Cada vez que cambies modelos:

```bash
python manage.py makemigrations
python manage.py migrate
```

Si quieres solo la app:

```bash
python manage.py makemigrations app_clientes
python manage.py migrate
```

### 13) Primero trabajamos con el MODELO: `CLIENTE`

A continuación está el `models.py` simplificado para `app_clientes` (solo `Cliente`).

---

## 3. Código fuente (archivos clave)

### `app_clientes/models.py` (solo Cliente por ahora)

```python
from django.db import models

class Cliente(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    empresa = models.CharField(max_length=100)
    correo = models.CharField(max_length=100, unique=True)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    direccion = models.CharField(max_length=255, blank=True, null=True)
    fecha_registro = models.DateField(auto_now_add=True)
    estado = models.CharField(max_length=50)

    def __str__(self):
        return f"{self.nombre} ({self.empresa})"
```

> **Nota:** He dejado solo `Cliente` ya que solicitaste trabajar solo con este modelo por ahora.

---

### `app_clientes/views.py` (funciones: inicio_clientes, agregar_cliente, ver_clientes, actualizar_cliente, realizar_actualizacion_cliente, borrar_cliente)

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Cliente
from django.utils import timezone

# 1. Página de inicio (informativa)
def inicio_clientes(request):
    return render(request, 'inicio.html')

# 2. Agregar cliente (mostrando formulario simple y guardando sin forms.py)
def agregar_cliente(request):
    if request.method == 'POST':
        nombre = request.POST.get('nombre')
        empresa = request.POST.get('empresa')
        correo = request.POST.get('correo')
        telefono = request.POST.get('telefono')
        direccion = request.POST.get('direccion')
        estado = request.POST.get('estado')

        Cliente.objects.create(
            nombre=nombre,
            empresa=empresa,
            correo=correo,
            telefono=telefono,
            direccion=direccion,
            estado=estado
        )
        return redirect('ver_clientes')

    return render(request, 'cliente/agregar_cliente.html')

# 3. Ver clientes (lista)
def ver_clientes(request):
    clientes = Cliente.objects.all().order_by('-fecha_registro')
    return render(request, 'cliente/ver_clientes.html', {'clientes': clientes})

# 4. Mostrar formulario de actualización
def actualizar_cliente(request, cliente_id):
    cliente = get_object_or_404(Cliente, id=cliente_id)
    return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente})

# 5. Realizar la actualización (POST)
def realizar_actualizacion_cliente(request, cliente_id):
    cliente = get_object_or_404(Cliente, id=cliente_id)
    if request.method == 'POST':
        cliente.nombre = request.POST.get('nombre')
        cliente.empresa = request.POST.get('empresa')
        cliente.correo = request.POST.get('correo')
        cliente.telefono = request.POST.get('telefono')
        cliente.direccion = request.POST.get('direccion')
        cliente.estado = request.POST.get('estado')
        cliente.save()
        return redirect('ver_clientes')
    return redirect('actualizar_cliente', cliente_id=cliente.id)

# 6. Borrar cliente
def borrar_cliente(request, cliente_id):
    cliente = get_object_or_404(Cliente, id=cliente_id)
    if request.method == 'POST':
        cliente.delete()
        return redirect('ver_clientes')
    # opcional: pedir confirmación con una plantilla
    return render(request, 'cliente/confirmar_borrado.html', {'cliente': cliente})
```

> Observación: yo incluyo una plantilla opcional `confirmar_borrado.html`. Si no deseas confirmación, puedes borrar directamente con `Cliente.objects.filter(id=cliente_id).delete()`.

---

### `app_clientes/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_clientes, name='inicio_clientes'),
    path('clientes/agregar/', views.agregar_cliente, name='agregar_cliente'),
    path('clientes/', views.ver_clientes, name='ver_clientes'),
    path('clientes/actualizar/<int:cliente_id>/', views.actualizar_cliente, name='actualizar_cliente'),
    path('clientes/realizar_actualizacion/<int:cliente_id>/', views.realizar_actualizacion_cliente, name='realizar_actualizacion_cliente'),
    path('clientes/borrar/<int:cliente_id>/', views.borrar_cliente, name='borrar_cliente'),
]
```

---

### `backend_agencia_de_marketing/urls.py` (archivo principal del proyecto)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_clientes.urls')),
]
```

---

### `app_clientes/admin.py`

```python
from django.contrib import admin
from .models import Cliente

@admin.register(Cliente)
class ClienteAdmin(admin.ModelAdmin):
    list_display = ('id', 'nombre', 'empresa', 'correo', 'telefono', 'fecha_registro', 'estado')
    search_fields = ('nombre', 'empresa', 'correo')
```

---

## 4. Templates (básicos y simples, colores suaves)

### `templates/base.html`

```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AgenciaDeMarketing</title>
  <!-- Bootstrap CSS CDN -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light text-dark">
  {% include 'navbar.html' %}

  <main class="container py-4">
    {% block content %}{% endblock %}
  </main>

  {% include 'footer.html' %}

  <!-- Bootstrap JS CDN -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

### `templates/navbar.html`

```html
<nav class="navbar navbar-expand-lg navbar-light bg-white shadow-sm">
  <div class="container">
    <a class="navbar-brand d-flex align-items-center" href="#">
      <!-- ícono simple usando emoji o svg -->
      <span style="font-weight:700; font-size:1.1rem;">🚀</span>
      <span class="ms-2">Sistema de Administración AgenciaDeMarketing</span>
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navMenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="/">Inicio</a></li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Clientes</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="{% url 'agregar_cliente' %}">Agregar Cliente</a></li>
            <li><a class="dropdown-item" href="{% url 'ver_clientes' %}">Ver Clientes</a></li>
          </ul>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Empleados</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Empleados</a></li>
            <li><a class="dropdown-item" href="#">Ver Empleados</a></li>
          </ul>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Proyectos</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Proyectos</a></li>
            <li><a class="dropdown-item" href="#">Ver Proyectos</a></li>
          </ul>
        </li>

      </ul>
    </div>
  </div>
</nav>
```

> **Nota:** los íconos principales pueden ser emojis o usar icon libraries luego (p. ej. FontAwesome). No los incluí en submenus como pediste.

### `templates/footer.html`

```html
<footer class="bg-white text-center py-3 mt-auto shadow-sm" style="position:fixed; left:0; right:0; bottom:0;">
  <div class="container">
    <small>
      © {{ now|date:"Y" }} - Derechos reservados. Creado por Ing. Edgar Orozco, Cbtis 128
    </small>
  </div>
</footer>
```

**Nota:** Para que `now` funcione en plantillas, asegúrate de habilitar el contexto o usar `from django.utils import timezone` y pasar la fecha desde la vista. Alternativamente usa la etiqueta `now` de Django: `{% now "Y" %}`.

### `templates/inicio.html`

```html
{% extends 'base.html' %}

{% block content %}
  <div class="row align-items-center">
    <div class="col-md-6">
      <h1>Bienvenido al Sistema de Administración</h1>
      <p>AgenciaDeMarketing - Gestiona clientes y proyectos de forma simple.</p>
    </div>
    <div class="col-md-6">
      <!-- Imagen desde la web: usar URL válida (ejemplo de Unsplash) -->
      <img src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=1080&auto=format&fit=crop&ixlib=rb-4.0.3&s=example" alt="Agencia de Marketing" class="img-fluid rounded">
    </div>
  </div>
{% endblock %}
```

### `templates/cliente/agregar_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
<h2>Agregar Cliente</h2>
<form method="post">
  {% csrf_token %}
  <div class="mb-3">
    <label class="form-label">Nombre</label>
    <input class="form-control" name="nombre" required>
  </div>
  <div class="mb-3">
    <label class="form-label">Empresa</label>
    <input class="form-control" name="empresa">
  </div>
  <div class="mb-3">
    <label class="form-label">Correo</label>
    <input class="form-control" name="correo" type="email">
  </div>
  <div class="mb-3">
    <label class="form-label">Teléfono</label>
    <input class="form-control" name="telefono">
  </div>
  <div class="mb-3">
    <label class="form-label">Dirección</label>
    <input class="form-control" name="direccion">
  </div>
  <div class="mb-3">
    <label class="form-label">Estado</label>
    <input class="form-control" name="estado">
  </div>
  <button class="btn btn-primary" type="submit">Guardar</button>
</form>
{% endblock %}
```

### `templates/cliente/borrar_cliente.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Clientes</title>
</head>
<body>
    <h1>Lista de Clientes</h1>

    <a href="{% url 'agregar_cliente' %}">Agregar nuevo cliente</a>

    <table border="1">
        <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Correo</th>
            <th>Teléfono</th>
            <th>Acciones</th>
        </tr>

        {% for cliente in clientes %}
        <tr>
            <td>{{ cliente.id }}</td>
            <td>{{ cliente.nombre }}</td>
            <td>{{ cliente.correo }}</td>
            <td>{{ cliente.telefono }}</td>
            <td>
                <a href="{% url 'borrar_cliente' cliente.id %}" onclick="return confirm('¿Seguro que deseas eliminar este cliente?')">
                    Eliminar
                </a>
            </td>
        </tr>
        {% endfor %}
    </table>

</body>
</html>

```


### `templates/cliente/ver_clientes.html`

```html
{% extends 'base.html' %}
{% block content %}
<h2>Clientes</h2>
<table class="table table-striped">
  <thead>
    <tr>
      <th>ID</th>
      <th>Nombre</th>
      <th>Empresa</th>
      <th>Correo</th>
      <th>Teléfono</th>
      <th>Fecha</th>
      <th>Estado</th>
      <th>Acciones</th>
    </tr>
  </thead>
  <tbody>
    {% for c in clientes %}
    <tr>
      <td>{{ c.id }}</td>
      <td>{{ c.nombre }}</td>
      <td>{{ c.empresa }}</td>
      <td>{{ c.correo }}</td>
      <td>{{ c.telefono }}</td>
      <td>{{ c.fecha_registro }}</td>
      <td>{{ c.estado }}</td>
      <td>
        <a class="btn btn-sm btn-info" href="{% url 'actualizar_cliente' c.id %}">Editar</a>
        <form action="{% url 'borrar_cliente' c.id %}" method="post" style="display:inline-block;">
          {% csrf_token %}
          <button class="btn btn-sm btn-danger" type="submit">Borrar</button>
        </form>
      </td>
    </tr>
    {% empty %}
    <tr><td colspan="8">No hay clientes registrados.</td></tr>
    {% endfor %}
  </tbody>
</table>
{% endblock %}
```

### `templates/cliente/actualizar_cliente.html`

```html
{% extends 'base.html' %}
{% block content %}
<h2>Actualizar Cliente</h2>
<form method="post" action="{% url 'realizar_actualizacion_cliente' cliente.id %}">
  {% csrf_token %}
  <div class="mb-3">
    <label class="form-label">Nombre</label>
    <input class="form-control" name="nombre" value="{{ cliente.nombre }}">
  </div>
  <div class="mb-3">
    <label class="form-label">Empresa</label>
    <input class="form-control" name="empresa" value="{{ cliente.empresa }}">
  </div>
  <div class="mb-3">
    <label class="form-label">Correo</label>
    <input class="form-control" name="correo" value="{{ cliente.correo }}" type="email">
  </div>
  <div class="mb-3">
    <label class="form-label">Teléfono</label>
    <input class="form-control" name="telefono" value="{{ cliente.telefono }}">
  </div>
  <div class="mb-3">
    <label class="form-label">Dirección</label>
    <input class="form-control" name="direccion" value="{{ cliente.direccion }}">
  </div>
  <div class="mb-3">
    <label class="form-label">Estado</label>
    <input class="form-control" name="estado" value="{{ cliente.estado }}">
  </div>
  <button class="btn btn-success" type="submit">Actualizar</button>
</form>
{% endblock %}
```

---

## 5. `settings.py` - agregar `app_clientes` a `INSTALLED_APPS`

En `backend_agencia_de_marketing/settings.py`:

```python
INSTALLED_APPS = [
    # apps de Django...
    'django.contrib.admin',
    'django.contrib.auth',
    # ...

    # nuestras apps
    'app_clientes',
]

# Opcional: si quieres que las plantillas las busque en app templates, deja TEMPLATE 'APP_DIRS': True (por defecto sí está)
```

---

## 6. Registrar modelos en admin y volver a migrar

1. Edita `app_clientes/admin.py` (ver arriba).
2. Ejecuta:

```bash
python manage.py makemigrations app_clientes
python manage.py migrate
```

---

## 7. Git y GitHub (subir el proyecto)

1. Crear `.gitignore` (ejemplo):

```
# Python
__pycache__/
*.py[cod]
*.egg-info/
.env
.env/
# virtual env
.venv/

# Django
*.sqlite3
/staticfiles/
/media/

# VS Code
.vscode/

# OS
.DS_Store
Thumbs.db
```

2. Inicializar repo y primer commit:

```bash
git init
git add .
git commit -m "Inicial: Proyecto UIII_Agencia_De_Marketing_0591 - base"
```

3. Crear repo en GitHub (interfaz web) y seguir instrucciones para conectar remoto:

```bash
git remote add origin git@github.com:TU_USUARIO/TU_REPO.git
git branch -M main
git push -u origin main
```

Si usas HTTPS: `git remote add origin https://github.com/TU_USUARIO/TU_REPO.git` y luego `git push -u origin main`.

---

## 8. Comprobaciones y puesta en marcha final

1. Asegúrate de que `app_clientes` esté en `INSTALLED_APPS`.
2. Ejecuta migrations: `python manage.py makemigrations` y `python manage.py migrate`.
3. Crea superusuario para acceder a admin: `python manage.py createsuperuser` y sigue indicaciones.
4. Ejecuta servidor: `python manage.py runserver 8591`.
5. Abre `http://127.0.0.1:8591/` en tu navegador.

---

## 9. Notas, limitaciones y recomendaciones

* No validamos entrada como pediste (sin validación). En producción siempre valida y limpia datos.
* Este README se centra en `Cliente`. Los modelos `Empleado` y `Proyecto` quedaron pendientes tal como solicitaste.
* Si más adelante quieres agregar formularios completos con validación, te sugiero usar `forms.py` y `ModelForm`.
* Para iconos más profesionales puedes usar FontAwesome o Bootstrap Icons.
* Si deseas que el footer muestre la fecha del sistema sin pasarla desde la vista, usa `{% now "Y" %}` en la plantilla.

---

## 10. Añadir al README de GitHub

Copia este documento y pégalo en el `README.md` de tu repositorio. Incluye también instrucciones para ejecutar en local (venv, instalar dependencias, migraciones y runserver) y una captura de pantalla si quieres.

---

Si quieres, puedo ahora:

* Generar los archivos exactos (código listo para pegar) en un ZIP descargable,
* O crear una estructura de archivos en el canvas para que copies/pegues más rápido.

Dime cuál prefieres y lo hago ahora.
