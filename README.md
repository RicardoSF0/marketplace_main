# Construye Aplicaciones Web

## Práctica Evaluatoria – Parcial 3

### Proyecto: Marketplace con Django

**Equipo 1 – 5BMPG**

* Aguirre Gutiérrez Juanita Ofelia
* Cota del Prado Moisés David
* Cruz Bustamante Annah Haday
* Hernández Hernández María Fernanda
* Sánchez Flores Ricardo

---

## 📌 Índice

1. [Introducción](#introducción)
2. [Explicación de comandos utilizados](#explicación-de-los-comandos)
3. [Arquitectura MVT de Django](#arquitectura-mvt-en-django)
4. [Explicación de archivos principales del proyecto](#explicación-de-archivos-del-proyecto)
5. [Código base del proyecto](#código-de-los-archivos-principales)
6. [Ejecución del proyecto](#ejecución-del-proyecto)
7. [Actualizaciones del proyecto](#actualizaciones-del-proyecto)
8. [Código actualizado](#código-actualizado)
9. [Conclusiones](#conclusiones)

---

## 🟦 Introducción

Este proyecto consiste en la construcción de un **Marketplace web con Django**, donde los usuarios pueden:

- Publicar productos  
- Navegar entre categorías  
- Registrarse e iniciar sesión  
- Ver detalles específicos de un artículo  
- Añadir productos propios con imágenes  

Este proyecto aplica la arquitectura **MVT (Model–View–Template)** y el flujo típico de desarrollo en Django: modelos, migraciones, autenticación, manejo de imágenes, vistas dinámicas y rutas limpias.

---

## 🟩 Explicación de los Comandos

Durante la creación y ejecución del proyecto se utilizaron los siguientes comandos:

* `md dj_marketplace` – Crear carpeta  
* `cd dj_marketplace` – Entrar a carpeta  
* `python -m venv venv` – Crear entorno virtual  
* `venv\Scriptsctivate` – Activar entorno  
* `pip install django` – Instalar Django  
* `django-admin startproject marketplace_main` – Crear proyecto  
* `python manage.py runserver` – Correr servidor local  
* `python manage.py startapp store` – Crear la aplicación principal  
* `pip freeze > requirements.txt` – Exportar dependencias  
* `python manage.py makemigrations` – Preparar cambios de BD  
* `python manage.py migrate` – Aplicar migraciones  
* `python manage.py createsuperuser` – Crear usuario administrador  
* `pip install pillow` – Permite subir imágenes  

---

## 🟧 Arquitectura MVT en Django

Django organiza su funcionamiento usando:

### 🔹 Model
Define la estructura de la base de datos.  
Ejemplo: Categorías, Productos, Usuarios.

### 🔹 View
Procesa la lógica del proyecto.  
Ejemplo: cargar productos, validar formularios, registrar usuarios.

### 🔹 Template
Son los archivos HTML que ve el usuario.  
Ejemplo: home, login, detalles de producto.

Esta arquitectura hace que el proyecto sea modular, organizado y escalable.

---

## 🟨 Explicación de Archivos del Proyecto

### settings.py
Configuración global del proyecto:  
- Apps instaladas  
- Base de datos  
- Rutas de medios e imágenes  
- Templates  
- Seguridad  

### urls.py
Define todas las rutas que el usuario puede visitar.  
Conecta URLs con funciones de `views.py`.

### models.py
Define las clases que representan tablas en la BD:  
- Category  
- Item  

### views.py
Contiene la lógica que responderá a las rutas:  
- home()  
- detail()  
- add_item()  
- register()  

### templates/store/
Contiene las páginas del sitio:

* home.html  
* item.html  
* login.html  
* signup.html  
* navigation.html  
* form.html  

Cada una extiende de base.html.

---

## 🟦 Código de los Archivos Principales

### models.py

```python
class Category(models.Model):
    name = models.CharField(max_length=255)

    class Meta:
        ordering = ('name',)
        verbose_name_plural = 'Categories'

    def __str__(self):
        return self.name
```

```python
class Item(models.Model):
    category = models.ForeignKey(Category, related_name='items', on_delete=models.CASCADE)
    name = models.CharField(max_length=255)
    description = models.TextField(blank=True, null=True)
    price = models.FloatField()
    image = models.ImageField(upload_to='item images', blank=True, null=True)
    is_sold = models.BooleanField(default=False)
    created_by = models.ForeignKey(User, related_name='items', on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

---

### views.py

```python
def home(request):
    items = Item.objects.filter(is_sold=False)
    categories = Category.objects.all()
    return render(request, 'store/home.html', {
        'items': items,
        'categories': categories
    })
```

```python
def detail(request, pk):
    item = get_object_or_404(Item, pk=pk)
    related_items = Item.objects.filter(
        category=item.category,
        is_sold=False
    ).exclude(pk=pk)[0:3]

    return render(request, 'store/item.html', {
        'item': item,
        'related_items': related_items
    })
```

```python
@login_required
def add_item(request):
    if request.method == 'POST':
        form = NewItemForm(request.POST, request.FILES)
        if form.is_valid():
            item = form.save(commit=False)
            item.created_by = request.user
            item.save()
            return redirect('detail', pk=item.id)
    else:
        form = NewItemForm()

    return render(request, 'store/form.html', {
        'form': form,
        'title': 'New Item'
    })
```

---

### urls.py

```python
urlpatterns = [
    path('', home, name='home'),
    path('contact/', contact, name='contact'),
    path('register/', register, name='register'),
    path('login/', auth_views.LoginView.as_view(
        template_name='store/login.html',
        authentication_form=LoginForm
    ), name='login'),
    path('logout/', logout_user, name='logout'),
    path('add_item/', add_item, name='add_item'),
    path('detail/<int:pk>/', detail, name='detail'),
]
```

---

## 🟩 Ejecución del Proyecto

### 1️⃣ Instalar dependencias
```
pip install django pillow
```

### 2️⃣ Aplicar migraciones
```
python manage.py migrate
```

### 3️⃣ Ejecutar el servidor
```
python manage.py runserver
```

### 4️⃣ Entrar al sitio
```
http://127.0.0.1:8000/
```

---

## 🟧 Actualizaciones del Proyecto

✔ Configuración de MEDIA_URL y MEDIA_ROOT  
✔ Integración de carga de imágenes  
✔ Implementación de login y registro  
✔ Página de detalle de producto  
✔ Filtrado de productos relacionados  
✔ Protección con login_required  

---

## 🟪 Conclusiones

El proyecto Marketplace permitió:

- Comprender la arquitectura MVT  
- Crear modelos con relaciones  
- Implementar autenticación  
- Renderizar vistas dinámicas con HTML  
- Trabajar con carga de imágenes  
- Organizar un proyecto Django real
--------  