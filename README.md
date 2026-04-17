# 🎓 Sistema de Alertas Tempranas (SAE)

El **Sistema de Alertas Tempranas (SAE)** es una aplicación web diseñada para tutores y docentes. Su objetivo principal es detectar de forma proactiva a estudiantes en riesgo académico (basado en promedios e inasistencias), permitiendo una intervención rápida. Además, integra un Asistente Académico Inteligente (Chatbot RAG) que genera planes de estudio personalizados para los estudiantes.

---

## ✨ Características Principales

1. **Dashboard Directivo:** Panel general con métricas (KPIs), gráficas interactivas y un top 5 de alumnos en riesgo crítico.
2. **Directorio y Perfil Estudiantil:** Listado filtrable de alumnos (por riesgo, carrera, etc.) y un perfil detallado con historial de calificaciones y alertas.
3. **Gestión de Alertas:** Bandeja de entrada donde los docentes pueden atender o escalar las alertas automáticas que el sistema genera por bajo rendimiento.
4. **Chatbot RAG (IA Local):** Un asistente que utiliza Recuperación Aumentada (Retrieval-Augmented Generation) cruzando la información del estudiante con una base de conocimientos local para dar consejos precisos.
5. **Diseño Moderno:** Interfaz de usuario con modo oscuro (Dark Mode), diseño Glassmorphism y notificaciones en tiempo real (Toasts).

---

## 🛠️ Tecnologías Utilizadas

*   **Backend:** Python 3 + Flask
*   **Base de Datos:** SQLite (Sin configuración extra) + SQLAlchemy (ORM)
*   **Inteligencia (Chatbot):** Scikit-learn (Algoritmo TF-IDF local, sin costo de API externa)
*   **Frontend:** Jinja2 (Motor de plantillas), HTML5, CSS3 Nativo, JavaScript (AJAX)
*   **Gráficos:** Chart.js (CDN)

---

## ⚙️ Estructura del Proyecto

```text
sistema-alertas/
│
├── app.py                  # Archivo principal de la aplicación (Rutas y Lógica)
├── chatbot.py              # Motor RAG local para el Asistente Inteligente
├── telegram_bot.py         # Bot de Telegram (recibe mensajes, alertas y comandos como /salir)
├── models.py               # Modelos de Bases de Datos (Estudiantes, Alertas, BC...)
├── seed_db.py              # Script para poblar la BD con datos simulados
├── upgrade_db.py           # Script para extender la BD (añade Chat IDs sin borrar data)
├── requirements.txt        # Dependencias de Python necesarias
├── .env                    # Configuraciones de entorno (Ej. Token del Bot)
├── sistema_alertas.db      # ¡Tu Base de Datos SQLite autogenerada!
│
├── static/
│   └── css/styles.css      # Hoja de estilos principal (Glassmorphism & Variables)
│
└── templates/              # Vistas y componentes HTML
    ├── base.html           # Plantilla maestra (Navbar, Estilos, Toasts base)
    ├── dashboard.html      # Pantalla 1: Home y gráficas generales
    ├── students.html       # Pantalla 2: Directorio con filtros
    ├── student_detail.html # Pantalla 3: Perfil individual y progreso
    ├── alerts.html         # Pantalla 4: Área para atender/escalar alertas
    └── chatbot.html        # Pantalla 5: Interfaz del asistente IA
```

---

## 🚀 Cómo inicializar y correr el proyecto

Sigue estos pasos para instalar el proyecto en tu computadora local:

### 1. Prerrequisitos
Asegúrate de tener instalado **Python 3.8 o superior** en tu sistema.

### 2. Instalar las dependencias
Abre una terminal o consola de comandos, ubícate en la carpeta del proyecto y ejecuta:

```bash
pip install -r requirements.txt
```

### 3. Configurar Telegram (Opcional pero Recomendado)
Si quieres probar el bot y las alertas en tu celular, debes crear el archivo `.env` vacío (si no existe) y añadirle el token que te dé BotFather en Telegram, así:
`TELEGRAM_TOKEN=tu_token_aqui`

### 4. Crear y Poblar la Base de Datos
Para generar la base de datos `sistema_alertas.db` y llenarla con 20 alumnos de prueba y los textos para el chatbot Inteligente, ejecuta estos dos comandos en orden:

```bash
python seed_db.py
python upgrade_db.py
```

### 5. Arrancar el Ecosistema
El proyecto tiene dos motores: El servidor web (Para el profesor) y el bot (Para el alumno). Puedes abrir dos pestañas en tu terminal y correr ambos:

```bash
# Terminal 1 (Servidor Web de Flask):
python app.py

# Terminal 2 (Bot de Telegram para estudiantes):
python telegram_bot.py
```
👉 Abre tu navegador y dirígete a: **http://127.0.0.1:5000** 

---

## 📖 Instrucciones de Uso Rápido (Demo)

1. **Botón "Generar Alertas":** Si visitas el *Dashboard* o *Alertas*, verás un botón azul arriba a la derecha. Si lo presionas y tu cuenta de Telegram está vinculada, recibirás la alerta Push en tiempo real en tu teléfono.
2. **Atender Alerta:** Ve al panel de *Alertas*. Verás botones verdes (Atender) y naranjas (Escalar) que cambian estados en tiempo real sin recargar.
3. **Probar el RAG en la Web:** Ve a la pestaña *Chatbot*, selecciona el nombre de un alumno y hazle consultas académicas.
4. **Probar el RAG en Telegram:** Entra a Telegram y búscalo. Si quieres registrar otra cuenta de estudiante ficticio para la demostración, escríbele al bot el comando **`/salir`**, te desvinculará y permitirá meter otro correo (ej. *carlos.rodriguez@universidad.edu*).
