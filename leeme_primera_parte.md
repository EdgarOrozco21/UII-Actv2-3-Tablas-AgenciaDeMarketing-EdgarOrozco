# 🚀 Proyecto: UII_Agencia_De_Marketing_0591 (Primera Parte)

**Lenguaje:** Python | **Framework:** Django | **Editor:** VS Code

---

## 💻 Procedimientos de Configuración Inicial

| Paso | Procedimiento | Comando de Terminal |
| :--- | :--- | :--- |
| **1** | Crear carpeta del Proyecto | `mkdir UII_Agencia_De_Marketing_0591` |
| **2** | Abrir VS Code sobre la carpeta | `cd UII_Agencia_De_Marketing_0591` seguido de `code .` |
| **3** | Abrir Terminal en VS Code | `Ctrl + Shift + \`` |
| **4** | Crear carpeta entorno virtual `.venv` | `python -m venv .venv` |
| **5** | Activar el entorno virtual | `source .venv/bin/activate` (Linux/macOS) o `.venv\Scripts\activate` (Windows) |
| **6** | Activar intérprete de python | *(Automático al activar el entorno)* |
| **7** | Instalar Django | `pip install django` |
| **8** | Crear proyecto `backend_agencia_de_marketing` sin duplicar carpeta | `django-admin startproject backend_agencia_de_marketing .` |
| **11**| Crear aplicación `app_clientes` | `python manage.py startapp app_clientes` |

## 🛠️ Modelos, Migraciones y Configuración Core

### 12. Modelos (`app_clientes/models.py`)

```python
from django.db import models

# ========================================== #
# MODELO: EMPLEADO (Pendiente)
# ==========================================#
class Empleado(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    puesto = models.CharField(max_length=50)
    correo = models.CharField(max_length=100, unique=True)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    fecha_contratacion = models.DateField()
    salario = models.DecimalField(max_digits=10, decimal_places=2)
    area = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre

# ========================================== #
# MODELO: CLIENTE (Foco Principal)
# ========================================== #
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

# ========================================== #
# MODELO: PROYECTO (Pendiente)
# ========================================== #
class Proyecto(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=150)
    fecha_inicio = models.TextField(help_text="Descripción o detalles del proyecto")
    fecha_entrega = models.DateField()
    new_field_3 = models.IntegerField(default=0)
    presupuesto = models.DecimalField(max_digits=10, decimal_places=2)
    estado = models.CharField(max_length=50)
    # Relaciones (Foreign Keys)
    cliente_id = models.ForeignKey(Cliente, on_delete=models.CASCADE, related_name="proyectos")
    empleado_id = models.ForeignKey(Empleado, on_delete=models.CASCADE, related_name="proyectos_asignados")

    def __str__(self):
        return self.nombre


## Hacer Migraciones
python manage.py makemigrations app_clientes
python manage.py migrate

## Configuración backend_agencia_de_marketing/settings.py
Agregar app_clientes a la lista INSTALLED_APPS.

# backend_agencia_de_marketing/settings.py

INSTALLED_APPS = [
    # ... otras apps de Django
    'app_clientes', # <--- NUEVA APP
]

## Enlace de URLs Principal (backend_agencia_de_marketing/urls.py)
# backend_agencia_de_marketing/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # Enlace a las URLs de la aplicación clientes (ruta vacía para la raíz)
    path('', include('app_clientes.urls')), 
]

## 27 27. Registro en Administración (app_clientes/admin.py)
Solo se registra el modelo Cliente por ahora.
# app_clientes/admin.py

from django.contrib import admin
from .models import Cliente, Empleado, Proyecto

# Registrado el modelo Cliente (Paso 27)
admin.site.register(Cliente)
# Empleado y Proyecto pendientes

🔑 Vistas y Rutas para CRUD (Clientes)
24. Rutas de la Aplicación (app_clientes/urls.py)
Crear este archivo dentro de la carpeta app_clientes.

# app_clientes/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_clientes, name='inicio_clientes'),
    path('agregar/', views.agregar_cliente, name='agregar_cliente'),
    path('ver/', views.ver_clientes, name='ver_clientes'),
    path('actualizar/<int:id_cliente>/', views.actualizar_cliente, name='actualizar_cliente'),
    path('realizar_actualizacion/<int:id_cliente>/', views.realizar_actualizacion_cliente, name='realizar_actualizacion_cliente'),
    path('borrar/<int:id_cliente>/', views.borrar_cliente, name='borrar_cliente'),
]

## Vistas de Clientes (app_clientes/views.py)
# app_clientes/views.py

from django.shortcuts import render, redirect, get_object_or_404
from .models import Cliente
from django.db import IntegrityError 

# Funciones de Vistas para Cliente (Paso 14)
def inicio_clientes(request):
    return render(request, 'inicio.html')

def ver_clientes(request):
    clientes = Cliente.objects.all()
    return render(request, 'cliente/ver_clientes.html', {'clientes': clientes})

def agregar_cliente(request):
    if request.method == 'POST':
        # ... lógica de guardado
        nombre = request.POST.get('nombre')
        empresa = request.POST.get('empresa')
        correo = request.POST.get('correo')
        telefono = request.POST.get('telefono')
        direccion = request.POST.get('direccion')
        estado = request.POST.get('estado')
        try:
            Cliente.objects.create(nombre=nombre, empresa=empresa, correo=correo, telefono=telefono, direccion=direccion, estado=estado)
            return redirect('ver_clientes')
        except IntegrityError:
            mensaje_error = "El correo electrónico ya está registrado."
            return render(request, 'cliente/agregar_cliente.html', {'error': mensaje_error})
    return render(request, 'cliente/agregar_cliente.html')

def actualizar_cliente(request, id_cliente):
    cliente = get_object_or_404(Cliente, id=id_cliente)
    return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente})

def realizar_actualizacion_cliente(request, id_cliente):
    if request.method == 'POST':
        cliente = get_object_or_404(Cliente, id=id_cliente)
        
        cliente.nombre = request.POST.get('nombre')
        cliente.empresa = request.POST.get('empresa')
        cliente.correo = request.POST.get('correo')
        cliente.telefono = request.POST.get('telefono')
        cliente.direccion = request.POST.get('direccion')
        cliente.estado = request.POST.get('estado')

        try:
            cliente.save()
            return redirect('ver_clientes')
        except IntegrityError:
            mensaje_error = "El correo electrónico ya está registrado."
            return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente, 'error': mensaje_error})
    return redirect('actualizar_cliente', id_cliente=id_cliente)

def borrar_cliente(request, id_cliente):
    cliente = get_object_or_404(Cliente, id=id_cliente)
    cliente.delete()
    return redirect('ver_clientes')

¡Absolutamente! Aquí tienes el contenido completo, en un solo bloque, formateado con Markdown y con todos los encabezados (#, ##, ###) y bloques de código (```lenguaje) listos para que lo copies y pegues directamente en el archivo .md de tu repositorio (como README.md o leerme_primera_parte.md).

Esto garantizará que se vea bien en el preview de GitHub.

Markdown

# 🚀 Proyecto: UII_Agencia_De_Marketing_0591 (Primera Parte)

**Lenguaje:** Python | **Framework:** Django | **Editor:** VS Code

---

## 💻 Procedimientos de Configuración Inicial

| Paso | Procedimiento | Comando de Terminal |
| :--- | :--- | :--- |
| **1** | Crear carpeta del Proyecto | `mkdir UII_Agencia_De_Marketing_0591` |
| **2** | Abrir VS Code sobre la carpeta | `cd UII_Agencia_De_Marketing_0591` seguido de `code .` |
| **3** | Abrir Terminal en VS Code | `Ctrl + Shift + \`` |
| **4** | Crear carpeta entorno virtual `.venv` | `python -m venv .venv` |
| **5** | Activar el entorno virtual | `source .venv/bin/activate` (Linux/macOS) o `.venv\Scripts\activate` (Windows) |
| **6** | Activar intérprete de python | *(Automático al activar el entorno)* |
| **7** | Instalar Django | `pip install django` |
| **8** | Crear proyecto `backend_agencia_de_marketing` sin duplicar carpeta | `django-admin startproject backend_agencia_de_marketing .` |
| **11**| Crear aplicación `app_clientes` | `python manage.py startapp app_clientes` |

## 🛠️ Modelos, Migraciones y Configuración Core

### 12. Modelos (`app_clientes/models.py`)

```python
from django.db import models

# ========================================== #
# MODELO: EMPLEADO (Pendiente)
# ==========================================#
class Empleado(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    puesto = models.CharField(max_length=50)
    correo = models.CharField(max_length=100, unique=True)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    fecha_contratacion = models.DateField()
    salario = models.DecimalField(max_digits=10, decimal_places=2)
    area = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre

# ========================================== #
# MODELO: CLIENTE (Foco Principal)
# ========================================== #
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

# ========================================== #
# MODELO: PROYECTO (Pendiente)
# ========================================== #
class Proyecto(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=150)
    fecha_inicio = models.TextField(help_text="Descripción o detalles del proyecto")
    fecha_entrega = models.DateField()
    new_field_3 = models.IntegerField(default=0)
    presupuesto = models.DecimalField(max_digits=10, decimal_places=2)
    estado = models.CharField(max_length=50)
    # Relaciones (Foreign Keys)
    cliente_id = models.ForeignKey(Cliente, on_delete=models.CASCADE, related_name="proyectos")
    empleado_id = models.ForeignKey(Empleado, on_delete=models.CASCADE, related_name="proyectos_asignados")

    def __str__(self):
        return self.nombre
12.5. Procedimiento para Realizar Migraciones
Bash

python manage.py makemigrations app_clientes
python manage.py migrate
25. Configuración backend_agencia_de_marketing/settings.py
Agregar app_clientes a la lista INSTALLED_APPS.

Python

# backend_agencia_de_marketing/settings.py

INSTALLED_APPS = [
    # ... otras apps de Django
    'app_clientes', # <--- NUEVA APP
]
26. Enlace de URLs Principal (backend_agencia_de_marketing/urls.py)
Python

# backend_agencia_de_marketing/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # Enlace a las URLs de la aplicación clientes (ruta vacía para la raíz)
    path('', include('app_clientes.urls')), 
]
27. Registro en Administración (app_clientes/admin.py)
Solo se registra el modelo Cliente por ahora.

Python

# app_clientes/admin.py

from django.contrib import admin
from .models import Cliente, Empleado, Proyecto

# Registrado el modelo Cliente (Paso 27)
admin.site.register(Cliente)
# Empleado y Proyecto pendientes
🔑 Vistas y Rutas para CRUD (Clientes)
24. Rutas de la Aplicación (app_clientes/urls.py)
Crear este archivo dentro de la carpeta app_clientes.

Python

# app_clientes/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_clientes, name='inicio_clientes'),
    path('agregar/', views.agregar_cliente, name='agregar_cliente'),
    path('ver/', views.ver_clientes, name='ver_clientes'),
    path('actualizar/<int:id_cliente>/', views.actualizar_cliente, name='actualizar_cliente'),
    path('realizar_actualizacion/<int:id_cliente>/', views.realizar_actualizacion_cliente, name='realizar_actualizacion_cliente'),
    path('borrar/<int:id_cliente>/', views.borrar_cliente, name='borrar_cliente'),
]
14. Vistas de Clientes (app_clientes/views.py)
Python

# app_clientes/views.py

from django.shortcuts import render, redirect, get_object_or_404
from .models import Cliente
from django.db import IntegrityError 

# Funciones de Vistas para Cliente (Paso 14)
def inicio_clientes(request):
    return render(request, 'inicio.html')

def ver_clientes(request):
    clientes = Cliente.objects.all()
    return render(request, 'cliente/ver_clientes.html', {'clientes': clientes})

def agregar_cliente(request):
    if request.method == 'POST':
        # ... lógica de guardado
        nombre = request.POST.get('nombre')
        empresa = request.POST.get('empresa')
        correo = request.POST.get('correo')
        telefono = request.POST.get('telefono')
        direccion = request.POST.get('direccion')
        estado = request.POST.get('estado')
        try:
            Cliente.objects.create(nombre=nombre, empresa=empresa, correo=correo, telefono=telefono, direccion=direccion, estado=estado)
            return redirect('ver_clientes')
        except IntegrityError:
            mensaje_error = "El correo electrónico ya está registrado."
            return render(request, 'cliente/agregar_cliente.html', {'error': mensaje_error})
    return render(request, 'cliente/agregar_cliente.html')

def actualizar_cliente(request, id_cliente):
    cliente = get_object_or_404(Cliente, id=id_cliente)
    return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente})

def realizar_actualizacion_cliente(request, id_cliente):
    if request.method == 'POST':
        cliente = get_object_or_404(Cliente, id=id_cliente)
        
        cliente.nombre = request.POST.get('nombre')
        cliente.empresa = request.POST.get('empresa')
        cliente.correo = request.POST.get('correo')
        cliente.telefono = request.POST.get('telefono')
        cliente.direccion = request.POST.get('direccion')
        cliente.estado = request.POST.get('estado')

        try:
            cliente.save()
            return redirect('ver_clientes')
        except IntegrityError:
            mensaje_error = "El correo electrónico ya está registrado."
            return render(request, 'cliente/actualizar_cliente.html', {'cliente': cliente, 'error': mensaje_error})
    return redirect('actualizar_cliente', id_cliente=id_cliente)

def borrar_cliente(request, id_cliente):
    cliente = get_object_or_404(Cliente, id=id_cliente)
    cliente.delete()
    return redirect('ver_clientes')
🎨 Archivos HTML (Templates)
(Crear la carpeta templates dentro de app_clientes y la subcarpeta cliente dentro de templates)

17. base.html (Incluye Bootstrap)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}AgenciaDeMarketing{% endblock %}</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css">
    
    <style>
        body {
            background-color: #f8f9fa; /* Colores suaves */
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }
        .content-wrap {
            padding-bottom: 60px;
            flex: 1;
        }
    </style>
</head>
<body>
    <div class="content-wrap">
        {% include 'header.html' %}
        {% include 'navbar.html' %}
        <main class="container mt-4">
            {% block content %}
            {% endblock %}
        </main>
    </div>
    {% include 'footer.html' %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
</body>
</html>
