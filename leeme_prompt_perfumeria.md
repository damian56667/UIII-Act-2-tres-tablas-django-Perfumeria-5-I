Perfecto — te entrego **la primera parte** completa y lista para copiar/pegar. Incluye los procedimientos (pasos, comandos), la estructura de carpetas y los archivos clave (models, views, urls, templates, admin), así como ejemplos de templates HTML (Bootstrap) y comandos para migraciones y ejecutar el servidor en los puertos que pediste. No uso `forms.py` (como indicaste) y dejo pendientes producto/cliente para que sigas después.

---

# Resumen rápido (qué vas a crear)

* Carpeta del proyecto: `UIII_Perfumeria_0566`
* Proyecto Django: `backend_perfumeria`
* App Django: `app_perfumeria`
* Entorno virtual: `.venv`
* Modelo principal por ahora: `Empleado` (CRUD funcional)
* Templates: `templates/` + `templates/empleado/` con vistas HTML (Bootstrap)
* No se usa `forms.py` (formularios HTML y `request.POST` en views)

---

# 1–6: Crear carpeta, abrir VS Code, terminal, crear y activar `.venv`, activar intérprete Python

Abre tu terminal (CMD/PowerShell / Git Bash) o usa la terminal integrada de VS Code.

1. Crear carpeta del proyecto:

```bash
mkdir UIII_Perfumeria_0566
cd UIII_Perfumeria_0566
```

2. Abrir VS Code en la carpeta:

```bash
code .
```

(Esto abrirá VS Code en `UIII_Perfumeria_0566`.)

3. Abrir terminal en VS Code:

* Menú: `Terminal` → `New Terminal`
  o atajo `Ctrl+ñ` / `Ctrl+` (según tu configuración).

4. Crear entorno virtual `.venv` desde terminal de VS Code:
   Windows:

```bash
python -m venv .venv
```

Linux / macOS:

```bash
python3 -m venv .venv
```

5. Activar entorno virtual:

* Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

(si da error, usa `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` en PowerShell una vez)

* Windows CMD:

```cmd
.venv\Scripts\activate
```

* Linux / macOS:

```bash
source .venv/bin/activate
```

6. Activar intérprete de Python en VS Code:

* Abre `Ctrl+Shift+P` → `Python: Select Interpreter` → elige `./UIII_Perfumeria_0566/.venv/...`.
  (Esto asegura que VS Code use el `.venv` para ejecución y depuración.)

---

# 7: Instalar Django

Con el `.venv` activo:

```bash
pip install --upgrade pip
pip install django
```

Puedes fijar versión si quieres, por ejemplo `pip install "django==4.2"`.

---

# 8: Crear proyecto `backend_perfumeria` sin duplicar carpeta

Dentro de `UIII_Perfumeria_0566` ejecuta:

```bash
django-admin startproject backend_perfumeria .
```

**Importante:** el `.` al final evita crear una carpeta extra `backend_perfumeria/backend_perfumeria`.

Estructura resultante (inicial):

```
UIII_Perfumeria_0566/
  .venv/
  manage.py
  backend_perfumeria/
    __init__.py
    settings.py
    urls.py
    asgi.py
    wsgi.py
```

---

# 9 y 31: Ejecutar servidor en puerto 8036 y luego en 8066

Puedes ejecutar el servidor en cualquier puerto así:

Puerto 8036:

```bash
python manage.py runserver 8036
```

Puerto 8066 (final):

```bash
python manage.py runserver 8066
```

(El navegador deberá abrir: `http://127.0.0.1:8036/` o `http://127.0.0.1:8066/` — abajo explico copiar/pegar link.)

---

# 10: Copiar y pegar el link en el navegador

Abre tu navegador y pega:

* `http://127.0.0.1:8036/` o `http://127.0.0.1:8066/` según el puerto que uses.

---

# 11: Crear aplicación `app_perfumeria`

Con el `.venv` activo y en la raíz del proyecto:

```bash
python manage.py startapp app_perfumeria
```

Estructura añadida:

```
app_perfumeria/
  migrations/
  __init__.py
  admin.py
  apps.py
  models.py
  views.py
  urls.py (lo crearás)
  tests.py
```

---

# 12: `models.py` (usa el que proporcionaste)

Copia tu bloque en `app_perfumeria/models.py`. Aquí lo dejo tal cual para pegar:

```python
from django.db import models

# ==========================================
# MODELO: EMPLEADO
# ==========================================
class Empleado(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    fecha_nacimiento = models.DateField(blank=True, null=True)
    puesto = models.CharField(max_length=100, blank=True, null=True)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    email = models.EmailField(blank=True, null=True)
    fecha_contratacion = models.DateField(blank=True, null=True)
    activo = models.BooleanField(default=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"

# ==========================================
# MODELO: PRODUCTO
# (Por ahora trabajamos con este modelo: CRUD completo)
# ==========================================
class Producto(models.Model):
    nombre = models.CharField(max_length=150, unique=True)
    descripcion = models.TextField(blank=True, null=True)
    precio = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)
    stock = models.PositiveIntegerField(default=0)
    categoria = models.CharField(max_length=100, blank=True, null=True)  # texto libre
    fecha_creacion = models.DateField(auto_now_add=True)
    activo = models.BooleanField(default=True)
    sku = models.CharField(max_length=50, blank=True, null=True)

    def __str__(self):
        return self.nombre

# ==========================================
# MODELO: CLIENTE
# ==========================================
class Cliente(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    email = models.EmailField(blank=True, null=True)
    direccion = models.CharField(max_length=250, blank=True, null=True)
    ciudad = models.CharField(max_length=100, blank=True, null=True)
    fecha_registro = models.DateField(auto_now_add=True)
    activo = models.BooleanField(default=True)
    def __str__(self):
        return f"{self.nombre} {self.apellido}"
```

> **Nota:** por ahora trabajarás con `Empleado`. Dejamos `Producto` y `Cliente` definidos pero no usados.

---

# 12.5: Procedimiento para realizar migraciones

1. Crear migraciones (app):

```bash
python manage.py makemigrations app_perfumeria
```

2. Aplicar migraciones:

```bash
python manage.py migrate
```

---

# 13: Primero trabajamos con el MODELO: PRODUCTO

(Tu lista dice primero producto; después indicas trabajar con empleado. En este entregable implemento CRUD para **Empleado** según el detalle que pediste en views/templates. Mantengo el `Producto` definido para usar después.)

---

# 14: `views.py` — funciones para empleado

Copia este contenido a `app_perfumeria/views.py` (reemplaza contenido existente):

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Empleado
from django.urls import reverse

def inicio_perfumeria(request):
    return render(request, 'inicio.html')

# Mostrar lista de empleados
def ver_empleado(request):
    empleados = Empleado.objects.all().order_by('id')
    return render(request, 'empleado/ver_empelado.html', {'empleados': empleados})

# Formulario para agregar empleado (GET muestra formulario, POST guarda)
def agregar_empleado(request):
    if request.method == 'POST':
        nombre = request.POST.get('nombre')
        apellido = request.POST.get('apellido')
        fecha_nacimiento = request.POST.get('fecha_nacimiento') or None
        puesto = request.POST.get('puesto')
        telefono = request.POST.get('telefono')
        email = request.POST.get('email')
        fecha_contratacion = request.POST.get('fecha_contratacion') or None

        Empleado.objects.create(
            nombre=nombre,
            apellido=apellido,
            fecha_nacimiento=fecha_nacimiento,
            puesto=puesto,
            telefono=telefono,
            email=email,
            fecha_contratacion=fecha_contratacion,
            activo=True
        )
        return redirect('ver_empleado')
    return render(request, 'empleado/agregar_empelado.html')

# Mostrar formulario de actualización con datos actuales
def actualizar_empleado(request, empleado_id):
    empleado = get_object_or_404(Empleado, id=empleado_id)
    return render(request, 'empleado/actualizar_empelado.html', {'empleado': empleado})

# Procesar la actualización (separado según tu petición)
def realizar_actualizacion_empleado(request, empleado_id):
    empleado = get_object_or_404(Empleado, id=empleado_id)
    if request.method == 'POST':
        empleado.nombre = request.POST.get('nombre')
        empleado.apellido = request.POST.get('apellido')
        empleado.fecha_nacimiento = request.POST.get('fecha_nacimiento') or None
        empleado.puesto = request.POST.get('puesto')
        empleado.telefono = request.POST.get('telefono')
        empleado.email = request.POST.get('email')
        empleado.fecha_contratacion = request.POST.get('fecha_contratacion') or None
        activo_val = request.POST.get('activo')
        empleado.activo = True if activo_val == 'on' else False
        empleado.save()
        return redirect('ver_empleado')
    return redirect('actualizar_empleado', empleado_id=empleado.id)

# Borrar empleado (confirmación GET -> borrar en POST)
def borrar_empleado(request, empleado_id):
    empleado = get_object_or_404(Empleado, id=empleado_id)
    if request.method == 'POST':
        empleado.delete()
        return redirect('ver_empleado')
    return render(request, 'empleado/borrar_empelado.html', {'empleado': empleado})
```

---

# 15: Crear carpeta `templates` dentro de `app_perfumeria`

Estructura:

```
app_perfumeria/
  templates/
    base.html
    header.html
    navbar.html
    footer.html
    inicio.html
    empleado/
      agregar_empelado.html
      ver_empelado.html
      actualizar_empelado.html
      borrar_empelado.html
```

---

# 16–17: `base.html` con Bootstrap CSS y JS

Crea `app_perfumeria/templates/base.html`:

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{% block title %}Sistema Perfumería{% endblock %}</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Opcional: Bootstrap Icons -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css" rel="stylesheet">

    <style>
      :root{
        --morado: #7b2cbf;
        --rosa: #ff6bcb;
        --suave: #f8f2fb;
      }
      body{ background: var(--suave); }
      .footer-fixed{
        position: fixed;
        left:0;
        bottom:0;
        width:100%;
        background:#fff;
        border-top:1px solid #eaeaea;
        padding:10px 0;
      }
      .container-main{ padding-bottom:80px; } /* espacio para footer */
    </style>
  </head>
  <body>
    {% include 'navbar.html' %}
    <div class="container container-main mt-4">
      {% block content %}{% endblock %}
    </div>

    {% include 'footer.html' %}

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

---

# 18: `navbar.html` con opciones e íconos (no en submenus)

Crea `templates/navbar.html`:

```html
<nav class="navbar navbar-expand-lg navbar-light bg-white shadow-sm">
  <div class="container">
    <a class="navbar-brand d-flex align-items-center" href="{% url 'inicio_perfumeria' %}">
      <i class="bi bi-bag-heart-fill me-2" style="font-size:1.2rem;color:var(--morado)"></i>
      <span style="font-weight:700;color:var(--morado)">Sistema de Administración perfumeria</span>
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navMenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="{% url 'inicio_perfumeria' %}"><i class="bi bi-house-door-fill"></i> Inicio</a></li>

        <!-- Empleado -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-people-fill"></i> Empleado
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="{% url 'agregar_empleado' %}">Agregar empleado</a></li>
            <li><a class="dropdown-item" href="{% url 'ver_empleado' %}">Ver empleado</a></li>
            <!-- actualizar y borrar se acceden desde la tabla -->
          </ul>
        </li>

        <!-- Producto -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-box-seam"></i> Producto
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar producto</a></li>
            <li><a class="dropdown-item" href="#">Ver producto</a></li>
          </ul>
        </li>

        <!-- Clientes -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">
            <i class="bi bi-person-lines-fill"></i> Clientes
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar clientes</a></li>
            <li><a class="dropdown-item" href="#">Ver clientes</a></li>
          </ul>
        </li>

      </ul>
    </div>
  </div>
</nav>
```

---

# 19: `footer.html` fijo al final con derechos y autor

Crea `templates/footer.html`:

```html
<footer class="footer-fixed">
  <div class="container d-flex justify-content-between">
    <div>© {{ now.year }} Todos los derechos reservados.</div>
    <div>Creado por Damian Dominguez, Cbtis 128</div>
  </div>
</footer>
```

> Para que `now` funcione, activa la variable en el contexto (ver nota más abajo). Si prefieres simple texto: reemplaza `{{ now.year }}` por el año actual, p.e. `2025`.

Si quieres usar la fecha dinámica, añade un context processor o en `inicio_perfumeria` añade `context={'now': datetime.datetime.now()}` (importa datetime).

---

# 20: `inicio.html` con info del sistema y una imagen desde la red sobre Cinépolis

Crea `templates/inicio.html`:

```html
{% extends 'base.html' %}
{% block title %}Inicio - Perfumería{% endblock %}
{% block content %}
  <div class="card p-3">
    <h2>Bienvenido al sistema de administración - Perfumería</h2>
    <p>Información del sistema y descripción breve.</p>
    <!-- Imagen tomada desde la red sobre Cinepolis (ejemplo) -->
    <div class="mt-3">
      <img src="https://via.placeholder.com/900x300?text=Cinepolis+Imagen+Ejemplo" class="img-fluid rounded" alt="Imagen Cinepolis (reemplazar)">
    </div>
  </div>
{% endblock %}
```

> **Sustituye** el `src` por la URL de la imagen que quieras sobre Cinepolis cuando la tengas.

---

# 21–22: Carpeta `templates/empleado` y archivos

Crea `app_perfumeria/templates/empleado/` y estos archivos con el contenido:

## `agregar_empelado.html`

```html
{% extends 'base.html' %}
{% block content %}
<h3>Agregar Empleado</h3>
<form method="post">
  {% csrf_token %}
  <div class="mb-3">
    <label>Nombre</label>
    <input class="form-control" name="nombre" required>
  </div>
  <div class="mb-3">
    <label>Apellido</label>
    <input class="form-control" name="apellido" required>
  </div>
  <div class="mb-3">
    <label>Fecha Nacimiento</label>
    <input type="date" class="form-control" name="fecha_nacimiento">
  </div>
  <div class="mb-3">
    <label>Puesto</label>
    <input class="form-control" name="puesto">
  </div>
  <div class="mb-3">
    <label>Teléfono</label>
    <input class="form-control" name="telefono">
  </div>
  <div class="mb-3">
    <label>Email</label>
    <input type="email" class="form-control" name="email">
  </div>
  <div class="mb-3">
    <label>Fecha Contratación</label>
    <input type="date" class="form-control" name="fecha_contratacion">
  </div>
  <button class="btn btn-primary">Guardar</button>
  <a href="{% url 'ver_empleado' %}" class="btn btn-secondary">Volver</a>
</form>
{% endblock %}
```

## `ver_empelado.html` (tabla con botones Ver / Editar / Borrar)

```html
{% extends 'base.html' %}
{% block content %}
<h3>Lista de Empleados</h3>
<a class="btn btn-success mb-3" href="{% url 'agregar_empleado' %}">Agregar Empleado</a>
<table class="table table-striped table-bordered">
  <thead>
    <tr>
      <th>ID</th><th>Nombre</th><th>Apellido</th><th>Puesto</th><th>Teléfono</th><th>Email</th><th>Acciones</th>
    </tr>
  </thead>
  <tbody>
    {% for e in empleados %}
    <tr>
      <td>{{ e.id }}</td>
      <td>{{ e.nombre }}</td>
      <td>{{ e.apellido }}</td>
      <td>{{ e.puesto }}</td>
      <td>{{ e.telefono }}</td>
      <td>{{ e.email }}</td>
      <td>
        <a class="btn btn-info btn-sm" href="{% url 'actualizar_empleado' e.id %}">Editar</a>
        <a class="btn btn-danger btn-sm" href="{% url 'borrar_empleado' e.id %}">Borrar</a>
      </td>
    </tr>
    {% empty %}
    <tr><td colspan="7">No hay empleados registrados.</td></tr>
    {% endfor %}
  </tbody>
</table>
{% endblock %}
```

## `actualizar_empelado.html`

```html
{% extends 'base.html' %}
{% block content %}
<h3>Actualizar Empleado</h3>
<form method="post" action="{% url 'realizar_actualizacion_empleado' empleado.id %}">
  {% csrf_token %}
  <div class="mb-3"><label>Nombre</label><input class="form-control" name="nombre" value="{{ empleado.nombre }}"></div>
  <div class="mb-3"><label>Apellido</label><input class="form-control" name="apellido" value="{{ empleado.apellido }}"></div>
  <div class="mb-3"><label>Fecha Nacimiento</label><input type="date" class="form-control" name="fecha_nacimiento" value="{{ empleado.fecha_nacimiento }}"></div>
  <div class="mb-3"><label>Puesto</label><input class="form-control" name="puesto" value="{{ empleado.puesto }}"></div>
  <div class="mb-3"><label>Teléfono</label><input class="form-control" name="telefono" value="{{ empleado.telefono }}"></div>
  <div class="mb-3"><label>Email</label><input class="form-control" name="email" value="{{ empleado.email }}"></div>
  <div class="mb-3"><label>Fecha Contratación</label><input type="date" class="form-control" name="fecha_contratacion" value="{{ empleado.fecha_contratacion }}"></div>
  <div class="form-check mb-3"><input type="checkbox" class="form-check-input" id="activo" name="activo" {% if empleado.activo %}checked{% endif %}><label class="form-check-label" for="activo">Activo</label></div>

  <button class="btn btn-primary">Guardar cambios</button>
  <a class="btn btn-secondary" href="{% url 'ver_empleado' %}">Cancelar</a>
</form>
{% endblock %}
```

## `borrar_empelado.html`

```html
{% extends 'base.html' %}
{% block content %}
<h3>Confirmar borrado</h3>
<p>¿Deseas eliminar al empleado <strong>{{ empleado.nombre }} {{ empleado.apellido }}</strong>?</p>
<form method="post">
  {% csrf_token %}
  <button class="btn btn-danger">Sí, eliminar</button>
  <a class="btn btn-secondary" href="{% url 'ver_empleado' %}">No, volver</a>
</form>
{% endblock %}
```

---

# 23: No utilizar `forms.py`

Los formularios son HTML simples y en `views.py` usamos `request.POST` — ya cumplido.

---

# 24: `urls.py` en `app_perfumeria`

Crea `app_perfumeria/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_perfumeria, name='inicio_perfumeria'),
    path('empleado/', views.ver_empleado, name='ver_empleado'),
    path('empleado/agregar/', views.agregar_empleado, name='agregar_empleado'),
    path('empleado/actualizar/<int:empleado_id>/', views.actualizar_empleado, name='actualizar_empleado'),
    path('empleado/actualizar/realizar/<int:empleado_id>/', views.realizar_actualizacion_empleado, name='realizar_actualizacion_empleado'),
    path('empleado/borrar/<int:empleado_id>/', views.borrar_empleado, name='borrar_empleado'),
]
```

---

# 25: Agregar `app_perfumeria` en `settings.py` de `backend_perfumeria`

En `backend_perfumeria/settings.py` -> agregar la app:

```python
INSTALLED_APPS = [
    # apps por defecto...
    'django.contrib.admin',
    'django.contrib.auth',
    # ...
    'app_perfumeria',  # <-- agregar aquí
]
```

Asegúrate también de tener la configuración de `TEMPLATES` (por defecto Django la trae) y `STATIC` si usas CSS/JS locales.

---

# 26: Configurar `urls.py` de `backend_perfumeria` para enlazar con `app_perfumeria`

Edita `backend_perfumeria/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_perfumeria.urls')),  # raíz del sitio apunta a la app
]
```

---

# 27: Registrar modelos en `admin.py` y volver a migrar

En `app_perfumeria/admin.py`:

```python
from django.contrib import admin
from .models import Empleado, Producto, Cliente

@admin.register(Empleado)
class EmpleadoAdmin(admin.ModelAdmin):
    list_display = ('id', 'nombre', 'apellido', 'puesto', 'email', 'activo')
    search_fields = ('nombre', 'apellido', 'puesto')

@admin.register(Producto)
class ProductoAdmin(admin.ModelAdmin):
    list_display = ('id','nombre','precio','stock','activo')
    search_fields = ('nombre','categoria')

@admin.register(Cliente)
class ClienteAdmin(admin.ModelAdmin):
    list_display = ('id','nombre','apellido','email','ciudad','activo')
    search_fields = ('nombre','apellido','email')
```

Después:

```bash
python manage.py makemigrations
python manage.py migrate
```

Crear superusuario para acceder al admin:

```bash
python manage.py createsuperuser
```

Sigue prompts (email, contraseña, etc).

---

# 28: Estética — colores suaves y código sencillo

Ya definí variables CSS en `base.html` y diseño simple con Bootstrap para mantener interfaz moderna y suave.

---

# 29: Estructura completa de carpetas y archivos (recomendación)

```
UIII_Perfumeria_0566/
├─ .venv/
├─ manage.py
├─ backend_perfumeria/
│  ├─ settings.py
│  ├─ urls.py
│  └─ ...
├─ app_perfumeria/
│  ├─ migrations/
│  ├─ templates/
│  │  ├─ base.html
│  │  ├─ navbar.html
│  │  ├─ footer.html
│  │  ├─ inicio.html
│  │  └─ empleado/
│  │     ├─ agregar_empelado.html
│  │     ├─ ver_empelado.html
│  │     ├─ actualizar_empelado.html
│  │     └─ borrar_empelado.html
│  ├─ admin.py
│  ├─ apps.py
│  ├─ models.py
│  ├─ views.py
│  └─ urls.py
```

---

# 30: Proyecto totalmente funcional (qué probar ahora)

1. Activa `.venv`.
2. `python manage.py migrate`
3. `python manage.py createsuperuser`
4. `python manage.py runserver 8066` (o 8036)
5. En el navegador: `http://127.0.0.1:8066/` → deberías ver la página de inicio.
6. Ve a `http://127.0.0.1:8066/empleado/` → tabla de empleados.
7. Agrega empleados, edítalos, bórralos; admin en `http://127.0.0.1:8066/admin/`.

---

# Notas, consejos y observaciones (importantes)

* **Nombres de archivos y pequeñas variantes de escritura**: en la lista usas `empelado` (sin 'r') en los nombres de archivos; usé exactamente esos nombres en templates para mantener tu convención (`agregar_empelado.html`, etc.). Puedes renombrar si prefieres `empleado`.
* **Fecha dinámica en footer**: si quieres `{{ now.year }}` en `footer.html`, modifica `inicio_perfumeria` para pasar `now`, o configura `context_processor`. Ejemplo simple: en `views.inicio_perfumeria`:

  ```python
  import datetime
  def inicio_perfumeria(request):
      return render(request, 'inicio.html', {'now': datetime.datetime.now()})
  ```
* **Imágenes**: puse un placeholder en `inicio.html`. Sustituye la URL por la imagen real de Cinepolis cuando la consigas.
* **Validaciones**: solicitaste *no validar entrada de datos* → por eso no hay validaciones ni `forms` ni `clean`.
* **Producto/Cliente**: modelos creados pero CRUD pendientes. Cuando quieras, te hago las vistas y templates equivalentes para `Producto` y `Cliente`.
* **Puerto**: mostrados comandos para ambos puertos (8036 y 8066). Usa el que necesites.
* **Static files**: si quieres CSS/JS locales crea `static/` y configura `STATICFILES_DIRS` en settings; por simplicidad estoy usando CDNs.
* **Context processors / timezone**: tu zona horaria ya está en `settings.py` (ajusta `TIME_ZONE = 'America/Ciudad_Juarez'` si quieres que refleje tu zona).

---

Si quieres, lo siguiente que puedo entregarte **ahora** (elige una):

1. CRUD completo para `Producto` (vistas + templates) — listo para pegar.
2. CRUD completo para `Cliente`.
3. Añadir búsqueda y paginación en la vista `ver_empleado`.
4. Convertir los templates para usar un archivo CSS propio en `static/`.

Dime cuál de estas quieres y te lo genero inmediatamente.

