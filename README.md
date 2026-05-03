# DataRix Consulting — Landing Page

Proyecto Flask básico con miras a crecer. Por ahora sirve la landing page estática. Listo para subir a un servidor.

---

## Estructura del proyecto

```
datarix/
├── run.py                  ← Punto de entrada
├── config.py               ← Configuración dev / producción
├── requirements.txt        ← Dependencias Python
├── Procfile                ← Para Render / Heroku / Railway
├── render.yaml             ← Config automática para Render.com
├── .env                    ← Variables de entorno (NO subir a git)
├── .gitignore
└── app/
    ├── __init__.py         ← Application Factory
    ├── routes.py           ← Rutas (aquí agregas blog, contacto, etc.)
    ├── templates/
    │   └── index.html      ← Landing page
    └── static/
        ├── css/main.css    ← Todo el CSS
        ├── js/main.js      ← Animaciones
        └── img/            ← Imágenes (logo, favicon, etc.)
```

---

## Correr en local (desarrollo)

```bash
# 1. Crear y activar entorno virtual
python -m venv venv

# Windows:
venv\Scripts\activate
# Mac / Linux:
source venv/bin/activate

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Correr el servidor
python run.py
```

Abre el navegador en: **http://localhost:5000**

---

## Subir a internet — opciones recomendadas

### Opción A — Render.com (GRATIS, más fácil)

1. Crea cuenta en https://render.com
2. Conecta tu repositorio de GitHub
3. Render detecta el `render.yaml` automáticamente
4. En 2 minutos tienes la URL pública: `https://datarix.onrender.com`
5. Para conectar tu dominio: Settings → Custom Domain

### Opción B — Railway.app (GRATIS con límite)

1. Crea cuenta en https://railway.app
2. New Project → Deploy from GitHub
3. Agrega la variable de entorno `SECRET_KEY`
4. Deploy automático

### Opción C — VPS propio (DigitalOcean, Hostinger, etc.)

```bash
# En el servidor
git clone <tu-repo>
cd datarix
pip install -r requirements.txt

# Correr con gunicorn (producción)
gunicorn run:app --bind 0.0.0.0:8000 --workers 2
```

Luego configura Nginx como proxy inverso apuntando al puerto 8000.

---

## Dominio propio (.pe o .com)

1. Compra el dominio en **NIC Perú** (dominios .pe) o **Namecheap / GoDaddy** (.com)
2. En Render/Railway ve a Settings → Custom Domain
3. Agrega los registros DNS que te indican (CNAME o A record)
4. En 24-48 horas el dominio queda activo

---

## Cómo agregar funcionalidades futuras

### Agregar una nueva página (blog, nosotros, etc.)

1. Agrega la ruta en `app/routes.py`:
```python
@main_bp.route('/blog')
def blog():
    return render_template('blog/index.html')
```

2. Crea el template en `app/templates/blog/index.html`

### Agregar base de datos

```bash
pip install flask-sqlalchemy flask-migrate
pip freeze > requirements.txt
```

Luego en `app/__init__.py` inicializa SQLAlchemy y crea tus modelos.

### Variables de entorno en producción

En Render/Railway configura estas variables (NO las pongas en el código):
- `SECRET_KEY` → una cadena larga y aleatoria
- `FLASK_ENV`  → `production`

---

## Comandos útiles

```bash
# Ver la app corriendo
python run.py

# Instalar nueva dependencia y guardarla
pip install nombre-paquete
pip freeze > requirements.txt

# Subir cambios a GitHub
git add .
git commit -m "descripción del cambio"
git push
```

Render y Railway se redesplegan automáticamente cada vez que haces `git push`.