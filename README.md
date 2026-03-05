# Repostería Flask

Aplicación web de gestión para una repostería, desarrollada con Flask, Flask-Admin y MySQL. Incluye autenticación de usuarios, panel de administración y migraciones de base de datos.

## ✨ Características

- Login con validación y mensajes flash mediante SweetAlert2.
- Panel de administración (Flask-Admin) protegido por autenticación.
- Gestión de usuarios (solo visualización por ahora).
- Botón de cierre de sesión integrado en el panel.
- Migraciones de base de datos con Flask-Migrate.
- Interfaz responsive y moderna.

## 📋 Requisitos previos

- Python 3.8 o superior
- MySQL (puede ser XAMPP, WAMP o MySQL standalone)
- Git (opcional)

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/reposteria-flask.git
cd reposteria-flask

2. Crear y activar un entorno virtual
bash
python -m venv venv
En Windows:

bash
venv\Scripts\activate
En macOS/Linux:

bash
source venv/bin/activate
3. Instalar dependencias
bash
pip install -r requirements.txt
requirements.txt:

text
Flask
Flask-SQLAlchemy
Flask-Login
Flask-Admin
PyMySQL
Flask-Migrate
4. Configurar la base de datos
Asegúrate de que MySQL esté corriendo.

Crea una base de datos (por ejemplo, db_reposteria):

sql
CREATE DATABASE IF NOT EXISTS db_reposteria;
5. Configurar la conexión
Edita el archivo config.py con tus credenciales de MySQL:

python
class Config:
    SECRET_KEY = 'clave_secreta_123'
    SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://usuario:contraseña@localhost:3306/db_reposteria'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
Por defecto, para XAMPP el usuario es root y sin contraseña.

6. Inicializar la base de datos y aplicar migraciones
El proyecto ya tiene migraciones configuradas. Ejecuta:

bash
flask db upgrade
Esto creará las tablas necesarias (user, producto, etc.) y aplicará cualquier cambio pendiente.

Si prefieres crear las tablas desde cero sin migraciones (solo para desarrollo), puedes usar:

bash
python run.py
Pero asegúrate de haber comentado la línea db.create_all() en run.py si ya usas migraciones.

7. Crear un usuario administrador (opcional)
El usuario admin con contraseña 1234 se crea automáticamente al ejecutar la aplicación por primera vez (ver run.py). Si deseas agregar más usuarios, puedes hacerlo desde la consola de Python o directamente en la base de datos.

8. Ejecutar la aplicación
bash
python run.py
Luego abre tu navegador en http://127.0.0.1:5000.

🔑 Credenciales por defecto
Usuario: admin

Contraseña: 1234

📁 Estructura del proyecto
text
reposteria-flask/
├── app/
│   ├── templates/
│   │   ├── admin/
│   │   │   └── master.html          # Plantilla personalizada para logout
│   │   └── login.html                # Página de login
│   ├── __init__.py                    # Fábrica de la aplicación
│   ├── admin.py                       # Configuración de Flask-Admin
│   ├── auth.py                         # Rutas de autenticación
│   ├── extensions.py                   # Inicialización de extensiones
│   ├── models.py                       # Modelos de base de datos
│   └── ...
├── migrations/                          # Carpeta de migraciones (Flask-Migrate)
├── .gitignore
├── config.py
├── requirements.txt
└── run.py
🧪 Pruebas
Accede a /login e ingresa credenciales incorrectas → verás un mensaje de error con SweetAlert2.

Ingresa credenciales correctas → serás redirigido a /admin.

En el panel de administración, haz clic en "Cerrar sesión" → volverás al login.

🛠️ Personalizaciones
Botón de logout en el panel de admin
Se ha personalizado la plantilla base de Flask-Admin agregando un enlace en la barra de navegación. El código se encuentra en app/templates/admin/master.html.

Mensajes flas