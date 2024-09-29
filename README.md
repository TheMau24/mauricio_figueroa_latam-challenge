# mauricio_figueroa_latam-challenge
Desarrollo del desafío DevSecOps/SRE de LATAM
# Desafío LATAM DevSecOps/SRE
Este repositorio contiene mi solución al desafío de LATAM Airlines para implementar un sistema de ingesta y almacenamiento de datos utilizando el patrón Pub/Sub y BigQuery.

# Desafío DevSecOps/SRE

## Introducción
Este proyecto tiene como objetivo construir un sistema para la ingesta y almacenamiento de datos enfocado en analítica avanzada, y exponer esos datos mediante una API HTTP. Utiliza Google Cloud Platform y sigue el esquema Pub/Sub para la ingesta de datos.

## 1. Configuración del Proyecto

### 1.1 Crear un Proyecto en Google Cloud
- Se creó un proyecto en Google Cloud llamado "LATAM CHALLENGE".
- **Project ID**: `calm-inkwell-437122-p3`.

### 1.2 Habilitar APIs
- Se habilitaron las siguientes APIs:
  - **Cloud Pub/Sub API**
  - **BigQuery API**

## 2. Creación de Tópico y Esquema

### 2.1 Crear Tópico de Pub/Sub
- Se creó un tópico llamado `data-ingestion-topic` para la ingesta de datos.

### 2.2 Crear Esquema
- Se definió un esquema para los mensajes del tópico en formato JSON:
```json
{
  "type": "record",
  "name": "FlightEvent",
  "fields": [
    {
      "name": "event_type",
      "type": "string"
    },
    {
      "name": "flight_number",
      "type": "string"
    },
    {
      "name": "timestamp",
      "type": "string"  // Formato de fecha y hora
    },
    {
      "name": "status",
      "type": "string"
    },
    {
      "name": "details",
      "type": ["null", "string"]  // Detalles opcionales
    }
  ]
}
