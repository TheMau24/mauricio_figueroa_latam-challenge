Aunque no logré completar el desafío, desarrollé las partes alcanzadas aplicando mis conocimientos actuales. Mi experiencia se centra en trabajar con GCP a nivel de consultas y análisis de datos en Looker, apoyando la toma de decisiones basadas en datos.

Tengo la capacidad de aprender rápidamente y pude avanzar en el desafío a pesar de que mi experiencia técnica no es tan profunda. Estoy convencido de que, con la oportunidad de desarrollar estas habilidades, puedo contribuir significativamente, ya que comprendo los problemas que surgen de la falta de integración de sistemas o desfases de información.

# mauricio_figueroa_latam-challenge
Desarrollo del desafío DevSecOps/SRE de LATAM

# Desafío LATAM DevSecOps/SRE
Este repositorio contiene mi solución al desafío de LATAM Airlines para implementar un sistema de ingesta y almacenamiento de datos utilizando el patrón Pub/Sub y BigQuery.

# Desafío DevSecOps/SRE - Latam Airlines

## Introducción
Este proyecto tiene como objetivo construir un sistema para la ingesta y almacenamiento de datos enfocado en analítica avanzada, y exponer esos datos mediante una API HTTP. Utiliza Google Cloud Platform y sigue el esquema Pub/Sub para la ingesta de datos.

## Parte 1: Infraestructura e IaC

### 1.1. Configuración del Proyecto en Google Cloud
- Se creó un proyecto en Google Cloud llamado "LATAM CHALLENGE".
- **Project ID**: `calm-inkwell-437122-p3`.

### 1.2. Habilitar APIs en Google Cloud
- Se habilitaron las siguientes APIs para el proyecto:
  - **Cloud Pub/Sub API**
  - **BigQuery API**

### 1.3. Creación del Tópico y Esquema en Pub/Sub

#### 1.3.1. Crear Tópico de Pub/Sub
- Se creó un tópico en Pub/Sub llamado `data-ingestion-topic` para la ingesta de datos.

#### 1.3.2. Definir Esquema de Mensajes
- Se definió un esquema para los mensajes del tópico en formato JSON:
```json
{
  "type": "record",
  "name": "FlightEvent",
  "fields": [
    {"name": "event_type", "type": "string"},
    {"name": "flight_number", "type": "string"},
    {"name": "timestamp", "type": "string"},  // Formato de fecha y hora
    {"name": "status", "type": "string"},
    {"name": "details", "type": ["null", "string"]}
  ]
}

###1.4. Creación de Suscripción en Pub/Sub

- Se creó una suscripción llamada data-ingestion-subscription para el tópico data-ingestion-topic utilizando el método de extracción (Pull).

### 1.5. Configuración de BigQuery

#### 1.5.1. Crear Conjunto de Datos

- Se creó un conjunto de datos en BigQuery llamado analytics_data.

### 1.6. Configuración de la Autenticación en Google Cloud

- Se creó una cuenta de servicio en Google Cloud y se generó una clave en formato JSON para la autenticación.
- Se configuró la variable de entorno GOOGLE_APPLICATION_CREDENTIALS para apuntar al archivo de credenciales en cada terminal utilizada.

###1.7. Configuración del Entorno de Desarrollo

- Se creó un entorno virtual para gestionar las dependencias de Python
- Se instalaron las siguientes bibliotecas necesarias (google-cloud-pubsub y google-cloud-bigquery)

### 1.8. Verificación de la Configuración de Google Cloud

- Se creó un script verify_setup.py para verificar que los recursos (tópico y dataset en BigQuery) existan en Google Cloud.

## Parte 2: Aplicaciones y Flujo CI/CD

### 2.1. Implementación de la API HTTP
- Se implementó una API HTTP utilizando **FastAPI** para exponer los datos almacenados en la tabla `my_table` del dataset `analytics_data` en BigQuery.
- El endpoint creado permite consultar los datos más recientes almacenados en la tabla a través de una petición `GET`.

### 2.2. Despliegue de la API HTTP en Google Cloud Run
- Se configuró un `Dockerfile` para construir la imagen de la aplicación.
- Aún no se ha completado el despliegue en Google Cloud Run debido a un problema con la herramienta `gcloud` en la configuración local.

### 2.3. Ingesta de Datos desde Pub/Sub
- Se agregó una suscripción al sistema Pub/Sub (`data-ingestion-subscription`) con lógica para insertar los datos recibidos en la tabla `my_table` de BigQuery.
- Esta lógica se implementó en el script `process_messages.py`, que se ejecuta para procesar y almacenar los mensajes de forma automática.

### 2.4. Próximos Pasos
- Completar la configuración de `gcloud` y realizar el despliegue de la API HTTP en Google Cloud Run.
- Realizar pruebas de la API en la nube para verificar que funcione correctamente.





