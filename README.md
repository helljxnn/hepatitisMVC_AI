# 🏥 Sistema de Predicción de Hepatitis con IA

Sistema web de predicción de hepatitis utilizando Machine Learning (Regresión Logística) desplegado con Flask y Render.

## 📋 Características

- ✅ **Interfaz intuitiva** con formularios fáciles de usar (dropdowns, tooltips)
- ✅ **Modelo de IA** con 100% de precisión en datos de prueba
- ✅ **Visualización de resultados** con gráficos de probabilidad
- ✅ **Responsive design** adaptable a móviles
- ✅ **API REST** disponible para integraciones (endpoint `/api/predict`)
- ✅ **Health check** endpoint para monitoreo

## 🚀 Despliegue en Render - PASO A PASO

### Paso 1: Preparar el Repositorio Git

Si aún no tienes Git inicializado:

```bash
cd hepatitis_AI
git init
git add .
git commit -m "Initial commit - Hepatitis AI prediction system"
```

### Paso 2: Subir a GitHub

1. Ve a [github.com](https://github.com) y crea una cuenta (si no tienes)
2. Crea un **nuevo repositorio** (botón verde "New")
   - Nombre: `hepatitis-ai` (o el que prefieras)
   - **NO marques** "Add README" ni ".gitignore" ni "license"
   - Click en "Create repository"

3. Conecta tu repositorio local con GitHub:

```bash
git remote add origin https://github.com/TU_USUARIO/hepatitis-ai.git
git branch -M main
git push -u origin main
```

Reemplaza `TU_USUARIO` con tu nombre de usuario de GitHub.

### Paso 3: Crear Cuenta en Render

1. Ve a [render.com](https://render.com)
2. Click en **"Get Started"** o **"Sign Up"**
3. Puedes registrarte con:
   - GitHub (recomendado - más fácil)
   - GitLab
   - Email

### Paso 4: Desplegar en Render

1. Una vez dentro de Render, click en **"New +"** (arriba a la derecha)
2. Selecciona **"Web Service"**
3. Conecta tu repositorio:
   - Si usaste GitHub para registrarte, verás tus repos automáticamente
   - Busca `hepatitis-ai` y click en **"Connect"**
   
4. Configura el servicio con estos valores:

   | Campo | Valor |
   |-------|-------|
   | **Name** | `hepatitis-ai` (o el nombre que prefieras) |
   | **Environment** | `Python 3` |
   | **Build Command** | `pip install -r requirements.txt` |
   | **Start Command** | `gunicorn app:app` |
   | **Instance Type** | `Free` |

5. Click en **"Create Web Service"**

### Paso 5: Esperar el Despliegue

Render automáticamente:
- ✅ Clonará tu repositorio
- ✅ Instalará las dependencias (Flask, scikit-learn, etc.)
- ✅ Cargará los modelos (.pkl)
- ✅ Iniciará la aplicación con Gunicorn

**Tiempo estimado**: 2-5 minutos

Verás los logs en tiempo real. Cuando veas algo como:
```
==> Your service is live 🎉
```

¡Tu aplicación está lista!

### Paso 6: Obtener tu URL

Render te asignará una URL como:
```
https://hepatitis-ai.onrender.com
```

O con un nombre aleatorio si no especificaste uno:
```
https://hepatitis-ai-xyz123.onrender.com
```

## 🧪 Probar la Aplicación

### En Render (Producción)

Abre tu URL de Render en el navegador:
- **Formulario web**: `https://tu-app.onrender.com/`
- **Health check**: `https://tu-app.onrender.com/health`
- **API**: `https://tu-app.onrender.com/api/predict`

### Localmente (Desarrollo)

```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar la aplicación
python app.py

# Abrir en el navegador
# http://localhost:5000
```

## 📡 Uso de la API

### Ejemplo con cURL

```bash
curl -X POST https://tu-app.onrender.com/api/predict \
  -H "Content-Type: application/json" \
  -d '{
    "Age": 45,
    "Sex": 1,
    "Estado_Civil": 2,
    "Ciudad": 1,
    "Steroid": 1,
    "Antivirals": 2,
    "Fatigue": 2,
    "Malaise": 1,
    "Anorexia": 1,
    "Liver_Big": 2,
    "Liver_Firm": 1,
    "Spleen_Palpable": 1,
    "Spiders": 1,
    "Ascites": 1,
    "Varices": 1,
    "Bilirubin": 1.2,
    "Alk_Phosphate": 85,
    "Sgot": 40,
    "Albumin": 4.0,
    "Protime": 12,
    "Histology": 2
  }'
```

### Ejemplo con Python

```python
import requests

url = "https://tu-app.onrender.com/api/predict"
data = {
    "Age": 45,
    "Sex": 1,
    "Estado_Civil": 2,
    "Ciudad": 1,
    "Steroid": 1,
    "Antivirals": 2,
    "Fatigue": 2,
    "Malaise": 1,
    "Anorexia": 1,
    "Liver_Big": 2,
    "Liver_Firm": 1,
    "Spleen_Palpable": 1,
    "Spiders": 1,
    "Ascites": 1,
    "Varices": 1,
    "Bilirubin": 1.2,
    "Alk_Phosphate": 85,
    "Sgot": 40,
    "Albumin": 4.0,
    "Protime": 12,
    "Histology": 2
}

response = requests.post(url, json=data)
print(response.json())
```

### Respuesta de la API

```json
{
  "prediction": 1,
  "probabilities": [0.1234, 0.8766],
  "predicted_probability": 0.8766
}
```

- **prediction**: 0 = Negativo, 1 = Positivo (riesgo de hepatitis)
- **probabilities**: Lista con probabilidades de cada clase [Negativo, Positivo]
- **predicted_probability**: Confianza de la predicción

## 📊 Modelo de IA

- **Algoritmo**: Regresión Logística
- **Características**: 21 variables (demográficas, síntomas, laboratorio)
- **Precisión**: 100% en conjunto de prueba
- **Framework**: scikit-learn 1.6.1

## 📝 Variables del Modelo

### 📋 Demográficas
- **Age**: Edad en años (0-120)
- **Sex**: Sexo (1=Masculino, 2=Femenino)
- **Estado_Civil**: Estado civil (1=Soltero, 2=Casado, 3=Divorciado, 4=Viudo)
- **Ciudad**: Ciudad de residencia (1=Bogotá, 2=Medellín, 3=Cali, 4=Barranquilla, 5=Cartagena, 6=Bucaramanga, 7=Pereira, 8=Santa Marta, 9=Manizales, 10=Cúcuta, 11=Ibagué, 12=Otra)

### 💊 Tratamientos
- **Steroid**: Toma esteroides (1=No, 2=Sí)
- **Antivirals**: Toma antivirales (1=No, 2=Sí)

### 🩺 Síntomas
- **Fatigue**: Fatiga (1=No, 2=Sí)
- **Malaise**: Malestar general (1=No, 2=Sí)
- **Anorexia**: Pérdida de apetito (1=No, 2=Sí)

### 🔬 Examen Físico
- **Liver_Big**: Hígado agrandado (1=No, 2=Sí)
- **Liver_Firm**: Hígado firme (1=No, 2=Sí)
- **Spleen_Palpable**: Bazo palpable (1=No, 2=Sí)
- **Spiders**: Arañas vasculares (1=No, 2=Sí)
- **Ascites**: Ascitis (1=No, 2=Sí)
- **Varices**: Várices esofágicas (1=No, 2=Sí)

### 🧪 Análisis de Laboratorio
- **Bilirubin**: Bilirrubina en mg/dL (normal: 0.1-1.2)
- **Alk_Phosphate**: Fosfatasa alcalina en U/L (normal: 30-120)
- **Sgot**: AST en U/L (normal: 10-40)
- **Albumin**: Albúmina en g/dL (normal: 3.5-5.5)
- **Protime**: Tiempo de protrombina en segundos (normal: 11-13.5)
- **Histology**: Biopsia realizada (1=No, 2=Sí)

## 🔧 Tecnologías

- **Backend**: Flask 2.2.5
- **ML**: scikit-learn 1.6.1, joblib 1.3.2
- **Servidor**: Gunicorn 21.2.0
- **Despliegue**: Render
- **Frontend**: HTML5, CSS3, JavaScript vanilla

## 🐛 Solución de Problemas

### La app no carga en Render

1. Revisa los **logs** en el dashboard de Render
2. Verifica que todos los archivos estén en GitHub:
   - `app.py`
   - `requirements.txt`
   - `Procfile`
   - `models/*.pkl` (archivos del modelo)

### Error: "Application failed to respond"

- El plan gratuito de Render "duerme" después de 15 minutos de inactividad
- La primera carga puede tardar 30-60 segundos en "despertar"
- Esto es normal en el plan gratuito

### Error: "Module not found"

- Verifica que `requirements.txt` tenga todas las dependencias
- Render debe ejecutar `pip install -r requirements.txt` automáticamente

### Actualizar la aplicación

Cada vez que hagas cambios:

```bash
git add .
git commit -m "Descripción de los cambios"
git push origin main
```

Render detectará los cambios y redesplegará automáticamente.

## 📁 Estructura del Proyecto

```
hepatitis_AI/
├── app.py                          # Aplicación Flask principal
├── requirements.txt                # Dependencias Python
├── Procfile                        # Configuración para Render
├── runtime.txt                     # Versión de Python
├── render.yaml                     # Configuración de Render (opcional)
├── README.md                       # Este archivo
├── models/
│   ├── modelo_regresion_logistica.pkl      # Modelo entrenado
│   ├── modelo_regresion_logistica_info.json # Metadata del modelo
│   └── scaler.pkl                          # Escalador de features
└── app/
    ├── static/
    │   └── __init__.py
    └── templates/
        ├── index.html              # Formulario web mejorado
        └── result.html             # Página de resultados mejorada
```

## ⚠️ Aviso Legal

Este sistema es una herramienta de apoyo educativa y **NO reemplaza el diagnóstico médico profesional**. Siempre consulte con un profesional de la salud calificado para cualquier decisión médica.

## 📄 Licencia

Proyecto educativo - Uso académico

---

**¿Necesitas ayuda?** Revisa los logs en Render o contacta al instructor.
