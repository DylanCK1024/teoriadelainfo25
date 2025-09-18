# Informe de Implementación del Proyecto TheHive + Cortex + MISP + Wazuh  
**Tarea #997**  
**Fecha:** 18 de Septiembre de 2025  
**Estudiante:** Dylan Fernando Chan Koh  

---

## 1. Introducción  

En el contexto actual, la ciberseguridad se ha convertido en un pilar fundamental para cualquier organización que gestione información sensible. La creciente sofisticación de los ataques y el aumento en la superficie de exposición requieren soluciones integradas que permitan no solo detectar y analizar incidentes, sino también dar respuesta rápida y coordinada.  

Este proyecto documenta la implementación de un ecosistema de seguridad compuesto por **TheHive, Cortex, MISP y Wazuh**, desplegado mediante **Docker Compose en un entorno Windows 11**.  

### 1.1 Objetivos del Proyecto  

- Implementar una plataforma integrada de gestión de incidentes de seguridad.  
- Configurar **TheHive** como plataforma central de gestión de casos.  
- Integrar **Cortex** para análisis automatizado de observables.  
- Preparar la arquitectura para integración futura con **MISP** y **Wazuh**.  
- Documentar todo el proceso de instalación y configuración.  

### 1.2 Alcance  

La implementación se realizó en un entorno de testing utilizando contenedores Docker, incluyendo:  
- **TheHive 5.5.2-1** (Gestión de incidentes).  
- **Cortex 3.1.8-1** (Análisis de observables).  
- **Elasticsearch 7.17.28** (Motor de búsqueda e indexación).  
- **Cassandra 4.1.8** (Base de datos principal).  
- **Nginx 1.27.5** (Proxy reverso con SSL).  

---

## 2. Descripción de los Componentes  

### 2.1 TheHive  
**Descripción:** Plataforma de gestión de respuesta a incidentes de seguridad (SIRP) de código abierto.  

**Funcionalidades principales:**  
- Gestión de casos e incidentes de seguridad.  
- Colaboración en equipo para investigaciones.  
- Seguimiento de tareas y observables.  
- Integración con herramientas de análisis externas.  

**Versión implementada:** 5.5.2-1  
**Puerto de acceso:** 9000  
**URL de acceso:** [http://localhost:9000/thehive](http://localhost:9000/thehive)  

![TheHive](https://github.com/user-attachments/assets/557bcbd2-dc5a-49ab-afe0-78498ee7d87b)  

---

### 2.2 Cortex  
**Descripción:** Motor de análisis de observables que permite automatizar el análisis de indicadores de compromiso.  

**Funcionalidades principales:**  
- Análisis automatizado de IPs, dominios, hashes, URLs.  
- Integración con múltiples fuentes de threat intelligence.  
- Ejecución de analyzers y responders.  
- API REST para integración con TheHive.  

**Versión implementada:** 3.1.8-1  
**Puerto de acceso:** 9001  
**URL de acceso:** [http://localhost:9001/cortex](http://localhost:9001/cortex)  

![Cortex-UI](https://github.com/user-attachments/assets/9bfb6dab-d978-408e-a0f5-27ee1e7886ae)  
![Cortex-Analyzers](https://github.com/user-attachments/assets/a95666d2-4a04-4b9e-8c01-4680b61d10dc)  

---

### 2.3 Elasticsearch  
**Descripción:** Motor de búsqueda y análisis distribuido utilizado como backend de indexación.  

**Funcionalidades principales:**  
- Indexación de datos de TheHive y Cortex.  
- Búsquedas rápidas y análisis de datos.  
- Almacenamiento de logs y métricas.  

**Versión implementada:** 7.17.28  
**Configuración:** Modo single-node con autenticación habilitada.  

---

### 2.4 Cassandra  
**Descripción:** Base de datos NoSQL distribuida utilizada como almacén principal de TheHive.  

**Funcionalidades principales:**  
- Almacenamiento de casos, tareas y observables.  
- Alta disponibilidad y escalabilidad.  
- Consistencia eventual.  

**Versión implementada:** 4.1.8  
**Configuración:** Cluster de un solo nodo con autenticación.  

---

### 2.5 Nginx  
**Descripción:** Servidor web y proxy reverso para acceso seguro a las aplicaciones.  

**Funcionalidades principales:**  
- Proxy reverso para TheHive y Cortex.  
- Terminación SSL/TLS.  
- Balanceador de carga.  

**Versión implementada:** 1.27.5  
**Configuración:** SSL con certificado autofirmado para testing.  

**Evidencia de despliegue:**  
![Deploy](https://github.com/user-attachments/assets/35a83b71-4a3c-4667-83f5-a24544059baf)  

---

## 3. Arquitectura e Integración  

### 3.1 Diagrama de Arquitectura  
