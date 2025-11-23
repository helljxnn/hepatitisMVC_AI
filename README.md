# 🏥 Sistema de Predicción de Hepatitis

Aplicación web para predicción de hepatitis usando Machine Learning con Flask.

## � Caracteríísticas

- Interfaz intuitiva con dropdowns y tooltips
- Predicción con Regresión Logística
- Visualización de resultados con gráficos
- API REST disponible
- Responsive design

## 📋 Requisitos

- Python 3.11+
- Flask 2.2.5
- scikit-learn 1.6.1

### Endpoint: `POST /api/predict`

**Request:**
```json
{
  "Age": 45,
  "Sex": 1,
  "Estado_Civil": 2,
  "Ciudad": 1,
  "Steroid": 1,
  "Antivirals": 1,
  "Fatigue": 1,
  "Malaise": 1,
  "Anorexia": 1,
  "Liver_Big": 1,
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
  "Histology": 1
}
```

**Response:**
```json
{
  "prediction": 0,
  "probabilities": [0.95, 0.05],
  "predicted_probability": 0.95
}
```

## 📝 Variables del Modelo

### Demográficas
- **Age:** Edad (0-120)
- **Sex:** 1=Masculino, 2=Femenino
- **Estado_Civil:** 1=Soltero, 2=Casado, 3=Divorciado, 4=Viudo
- **Ciudad:** 1=Bogotá, 2=Medellín, 3=Cali, etc.

### Tratamientos y Síntomas
- **Steroid, Antivirals, Fatigue, Malaise, Anorexia:** 1=No, 2=Sí

### Examen Físico
- **Liver_Big, Liver_Firm, Spleen_Palpable, Spiders, Ascites, Varices:** 1=No, 2=Sí

### Laboratorio
- **Bilirubin:** mg/dL (normal: 0.1-1.2)
- **Alk_Phosphate:** U/L (normal: 30-120)
- **Sgot:** U/L (normal: 10-40)
- **Albumin:** g/dL (normal: 3.5-5.5)
- **Protime:** segundos (normal: 11-13.5)
- **Histology:** 1=No, 2=Sí

## 🧪 Casos de Prueba

### Caso NEGATIVO (Paciente Sano)
```
Edad: 30, Sexo: Femenino
Todos los síntomas: No
Bilirrubina: 0.8, SGOT: 25, Albúmina: 4.5
```
**Resultado:** ✅ NEGATIVO (~95% confianza)

### Caso POSITIVO (Alto Riesgo)
```
Edad: 55, Sexo: Masculino
Todos los síntomas: Sí
Bilirrubina: 3.5, SGOT: 120, Albúmina: 2.5, Protrombina: 18
```
**Resultado:** ⚠️ POSITIVO (~70% confianza)

Ver archivos `PRUEBA_NEGATIVO.txt` y `PRUEBA_POSITIVO.txt` para más detalles.

## 🔧 Tecnologías

- **Backend:** Flask 2.2.5, Gunicorn 21.2.0
- **ML:** scikit-learn 1.6.1, NumPy, Pandas
- **Frontend:** HTML5, CSS3, JavaScript
- **Despliegue:** Render

## 📁 Estructura

```
hepatitis_AI/
├── app.py                  # Aplicación Flask
├── requirements.txt        # Dependencias
├── Procfile               # Config Render
├── models/                # Modelos ML
│   ├── modelo_regresion_logistica.pkl
│   ├── scaler.pkl
│   └── modelo_regresion_logistica_info.json
└── app/
    ├── static/css/        # Estilos
    └── templates/         # HTML
```

## ⚠️ Aviso Legal

Este sistema es una herramienta educativa y **NO reemplaza el diagnóstico médico profesional**. Siempre consulte con un profesional de la salud.

## 📚 Documentación Adicional

- `GUIA_DESPLIEGUE.md` - Guía detallada de despliegue
- `CASOS_PRUEBA_RAPIDA.md` - Casos de prueba completos
- `ARQUITECTURA.md` - Diagramas técnicos

---

**Proyecto educativo AI** - By Jenn
