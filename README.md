# 🚚 GateOpsPro - Sistema Integral de Gestión de Flotas y Logística

![Google Apps Script](https://img.shields.io/badge/Google%20Apps%20Script-Backend-blue?style=flat-square&logo=google)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Database-green?style=flat-square&logo=google-sheets)
![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-yellow?style=flat-square&logo=powerbi)
![Status](https://img.shields.io/badge/Status-Producción-success?style=flat-square)

## 📝 Descripción del Proyecto
**GateOpsPro** es una solución integral desarrollada en Google Apps Script (V8) diseñada para la gestión, control y auditoría de flotas vehiculares en entornos de alta exigencia operativa (Sector Industrial/Seguridad). 

El sistema funciona como una Single Page Application (SPA) que se conecta a Google Sheets como base de datos, automatizando procesos críticos como el control de kilometraje, la generación de tickets de mantenimiento preventivo/correctivo, el cálculo de rendimiento de combustible y la restricción de uso de vehículos por áreas.
<img width="825" height="707" alt="foto1" src="https://github.com/user-attachments/assets/e1dffc64-2f06-49c9-916c-8d2552472880" />

## 🏗️ Arquitectura del Sistema
El proyecto opera bajo una arquitectura Serverless utilizando el ecosistema de Google:
1.  **Frontend:** Interfaz web (HTML/JS) servida mediante `HtmlService`.
2.  **Backend:** Lógica de negocio en Google Apps Script (`Código.gs`).
3.  **Base de Datos:** Google Sheets (tablas relacionales simuladas mediante hojas).
4.  **Notificaciones:** Integración con `MailApp` para alertas automáticas en tiempo real.
5.  **Business Intelligence:** Conexión vía API para el despliegue de Dashboards interactivos en Power BI.

## ⚙️ Características y Lógica de Negocio

### 1. Control Operativo y Catálogo Anti-Préstamo
- **Validación de Área:** El sistema cuenta con un catálogo de vehículos que restringe el uso de unidades a su área asignada (Operaciones, Mantenimiento, Logística). Si un usuario intenta registrar un vehículo de otra área, el sistema lo bloquea y envía una alerta al administrador.
- **Bloqueo de Unidades:** Permite marcar vehículos como "Bloqueados" (por avería o seguridad) impidiendo su salida a ruta o carga de combustible.

### 2. Mantenimiento Automatizado (Tickets)
- **Generación Automática:** Al registrar el kilometraje, el sistema evalúa la distancia recorrida desde el último servicio. Si se superan los 5,000 km, genera automáticamente un **Ticket Preventivo**.
- **Tickets Correctivos:** Si el conductor reporta una falla en el estado del equipo, se abre un ticket correctivo y el vehículo queda bloqueado hasta que el taller lo libere.

### 3. Gestión de Combustible y Rendimiento (KPIs)
- **Cálculo de Rendimiento Real:** Implementa una lógica de "Tanque Lleno a Tanque Lleno" (Full-to-Full), acumulando litros parciales para calcular el rendimiento exacto en `km/L`.
- **Alertas de Anomalía:** Si el rendimiento del vehículo cae por debajo del umbral configurado (ej. 8 km/L), el sistema dispara una alerta por correo para auditar posible robo de combustible o fallas mecánicas.
  <img width="1567" height="887" alt="foto3" src="https://github.com/user-attachments/assets/ec115a13-96ab-4533-96a5-43dca1bcb39c" />

### 4. Auditoría y Mantenimiento de Base de Datos
- **Archivado Automático:** Para evitar el colapso de Google Sheets, el sistema monitorea el tamaño de las hojas. Al superar los 10,000 registros, mueve automáticamente los datos más antiguos (protegiendo los últimos 3 meses) a un archivo de respaldo en Google Drive.

## 📊 Panel de Control (Business Intelligence)
El Backend de GateOpsPro exporta los datos limpios y estructurados para ser consumidos por un **Dashboard en Power BI** (construido a la medida), el cual permite visualizar:
- Rendimiento de flota (Km/L por vehículo).
- Costos operativos de combustible.
- Cantidad de viajes realizados y equipos en operación.
- Historial de mantenimientos (Preventivos vs. Correctivos).

<img width="1902" height="805" alt="foto4" src="https://github.com/user-attachments/assets/342d4e9b-e460-4ff6-b6d3-e0f993bde56f" />
<img width="1252" height="855" alt="foto2" src="https://github.com/user-attachments/assets/2df09868-2910-4a2b-98c9-146ed3631443" />


## 🧠 Desafíos Técnicos Superados
- **Manejo de Zonas Horarias:** Uso de `Utilities.formatDate` con la zona `America/Managua` para asegurar que los registros coincidan con la hora local del país, evitando desfases en los reportes.
- **Rendimiento de Datos:** Implementación de lecturas invertidas en los arrays (de abajo hacia arriba) para obtener el último kilometraje de un vehículo sin recorrer toda la base de datos, optimizando los tiempos de ejecución del script.

## 👨‍💻 Autor
**Nestor Gonzalo Moreira Largaespada** 
*Ingeniero en Sistemas | Especialista en Infraestructura y Automatización*
- [LinkedIn](https://linkedin.com/in/nestormoreira)
- [Portafolio Web](https://nestor-moreira.netlify.app)
