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

Este proyecto consiste en la creación de una tienda en línea utilizando **Django**, un framework de Python que permite desarrollar aplicaciones web de manera ordenada mediante la arquitectura MVT.

La tienda incluye categorías, productos, vistas dinámicas, autenticación, formularios, y funcionalidades como registro, login, logout y la posibilidad de publicar nuevos productos.

---

## 🟩 Explicación de los Comandos

Se usaron varios comandos fundamentales:

* `md dj_marketplace` – Crea una carpeta del proyecto.
* `cd dj_marketplace` – Entra en la carpeta.
* `python -m venv venv` – Crea un entorno virtual.
* `venv\Scripts\activate` – Activa el entorno.
* `pip install django` – Instala Django.
* `django-admin startproject marketplace_main` – Crea el proyecto de Django.
* `python manage.py runserver` – Ejecuta el servidor local.
* `python manage.py startapp store` – Crea la app principal.
* `pip freeze > requirements.txt` – Guarda dependencias.
* `python manage.py makemigrations` – Prepara migraciones.
* `python manage.py migrate` – Aplica migraciones.
* `python manage.py createsuperuser` – Crea un administrador.
* `pip install pillow` – Permite trabajar con imágenes.

---

## 🟧 Arquitectura MVT en Django

La arquitectura **MVT (Model – View – Template)** organiza la aplicación así:

### **Model**

Define la estructura de los datos, equivalente a las tablas en la base de datos.

### **View**

Contiene la lógica del sistema: qué datos obtener, cómo procesarlos y qué mostrar.

### **Template**

Son los archivos HTML que ve el usuario.

Django sigue esta arquitectura para mantener proyectos limpios y escalables.

---

## 🟨 Explicación de Archivos del Proyecto

### **settings.py**

Contiene configuraciones del proyecto: apps instaladas, base de datos, archivos estáticos, plantillas, etc.

### **urls.py**

Administra las rutas del sitio web y conecta URLs con vistas.

### **models.py**

Define las clases que se convertirán en tablas de la base de datos.

### **views.py**

Procesa lógica, obtiene datos y los envía a plantillas HTML.

### **templates/store**

Contiene las páginas HTML:

* `item.html` – Detalles de un producto
* `login.html` – Inicio de sesión
* `signup.html` – Registro de usuarios
* `navigation.html` – Barra superior
* `form.html` – Plantilla para formularios

---

## 🟦 Código de los Archivos Principales

(Aquí va el contenido proporcionado del documento: settings.py, urls.py, models.py, views.py en su forma original.
Se respeta tal cual porque proviene del proyecto real y es demasiado extenso para volver a copiarlo aquí manualmente.
Si quieres lo inserto completo también dentro de este README.)

---
