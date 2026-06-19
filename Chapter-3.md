<div style="page-break-after: always;"></div>

## **Capítulo III: Requirements Specification**
- **3.1. User Stories**
    ### Epic Story

    | Epic ID | Título |
    |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **EP01** | **Integración de Hardware y Procesamiento de Datos de Sensores (Backend)** |
    | | Como integrador de hardware, quiero leer y procesar datos de los 3 sensores (carga, ultrasónico, IR) en el backend para generar estimaciones de stock precisas y alertas preventivas. |

    | Epic ID | Título |
    |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **EP02** | **Core de Alertas Preventivas y Notificaciones Móviles** |
    | | Como usuario del hogar, quiero recibir notificaciones push instantáneas en mi celular cuando un grano baja del umbral crítico para no quedarme sin insumos básicos y gestionar las compras proactivamente. |

    | Epic ID | Título |
    |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **EP03** | **Panel de Control Centralizado para Usuarios Finales (Web/Angular)** |
    | | Como usuario del hogar, quiero ver el stock actual y el historial de consumo de todos mis granos en una interfaz web centralizada cuando accedo al dashboard para tener una visión rápida y detallada de mi alacena. |

    | Epic ID | Título |
    |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **EP04** | **Funcionalidad de Monitoreo Remoto para Cuidadores (Móvil/Flutter)** |
    | | Como cuidador de un adulto mayor, quiero ver el stock de granos y recibir alertas de nivel bajo en mi aplicación móvil cuando un grano baja de nivel para gestionar la reposición de forma proactiva en casa de mi familiar. |

    | Epic ID | Título |
    |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **EP05** | **Presencia Digital y Captación de Usuarios** |
    | | Como visitante, quiero acceder a una plataforma informativa para conocer la solución DispenXCore, ver testimonios de precisión y registrar mi interés en el producto. |

---

### Epic Story 1 | Integración de Hardware y Procesamiento de Datos de Sensores

| Epic / Story ID | Título | Descripción | Criterios de Aceptación | Relacionado con (Epic ID) |
| :--- | :--- | :--- | :--- | :--- |
| **US01** | Visualización de Stock Crudo en Firmware de Depuración | **Como** desarrollador de firmware,<br>**quiero** ver los valores crudos de los sensores en tiempo real,<br>**para** verificar la correcta calibración y funcionamiento del hardware durante la instalación inicial. | Escenario 1: **Dado que** estoy en la interfaz de depuración, **cuando** aplico peso a la celda de carga, **entonces** veo el cambio instantáneo en el valor crudo en gramos.<br><br>**Escenario 2:** **Dado que** estoy en la interfaz de depuración, **cuando** bloqueo el sensor ultrasónico, **entonces** veo el cambio instantáneo en el valor de distancia. | EP01 |
| **US02** | Actualización de Firmware Remota (OTA) | **Como** administrador del sistema,<br>**quiero** poder actualizar el firmware de los dispensadores de forma remota,<br>**para** corregir errores e implementar mejoras sin intervención física en el hogar. | Escenario 1: **Dado que** hay una nueva versión de firmware disponible, **cuando** inicio la actualización desde el panel de control, **entonces** el dispensador descarga e instala la actualización de forma automática.<br><br>**Escenario 2:** **Dado que** el dispensador está actualizándose, **cuando** el proceso finaliza, **entonces** el sistema notifica el éxito o fracaso de la operación. | EP01 |
| **TS01** | Migración de Base de Datos para Lecturas de Sensores | Crear el esquema de base de datos necesario en C# para almacenar lecturas históricas y crudas de los 3 sensores. | Escenario 1: Migración ejecutada con éxito y esquema verificado. Pruebas de inserción y consulta de datos. | EP01 |
| **TS02** | Implementación del Backend para Procesamiento de Datos de Sensores | Desarrollar el algoritmo en el backend C# para combinar las lecturas de peso, nivel y flujo IR en una estimación de stock significativa. | Escenario 1: API endpoint `GET /api/processed-stock` creado y validado. Pruebas unitarias para múltiples escenarios de combinación de sensores. | EP01 |
| **TS03** | Firmware del Microcontrolador para Lectura de 3 Sensores | Desarrollar el firmware (ej: para ESP32) para leer datos crudos de la celda de carga, sensor ultrasónico e IR. | Escenario 1: API endpoint en el microcontrolador funcional para lectura de sensores. Pruebas de lectura directa exitosas. | EP01 |

---

### Epic Story 2 | Core de Alertas Preventivas y Notificaciones Móviles

| Epic / Story ID | Título | Descripción | Criterios de Aceptación | Relacionado con (Epic ID) |
| :--- | :--- | :--- | :--- | :--- |
| **US03** | Configuración de Umbral de Alerta de Stock Bajo | **Como** usuario del hogar,<br>**quiero** configurar un umbral de stock bajo personalizado para cada grano,<br>**para** recibir alertas preventivas antes del agotamiento total. | Escenario 1: **Dado que** estoy en la pantalla de detalles del producto, **cuando** selecciono el porcentaje de umbral, **entonces** el sistema guarda el valor y lo usa para futuras evaluaciones.<br><br>**Escenario 2:** **Dado que** estoy en la gestión de inventario, **cuando** añado un nuevo grano, **entonces** el sistema asigna un umbral predeterminado de 20%. | EP02 |
| **US04** | Visualización de Alertas Activas en la App Móvil | **Como** usuario del hogar,<br>**quiero** ver una lista de todas las alertas activas de stock bajo en la aplicación móvil,<br>**para** saber qué granos comprar pronto. | Escenario 1: **Dado que** tengo productos por debajo del umbral, **cuando** abro la pestaña de alertas en la app móvil, **entonces** veo una lista clara con el nombre del grano y el nivel actual.<br><br>**Escenario 2:** **Dado que** no tengo alertas activas, **cuando** abro la pestaña de alertas, **entonces** veo un mensaje claro indicando que todo está en orden. | EP02 |
| **US05** | Recepción de Notificaciones Push de Stock Bajo | **Como** usuario del hogar,<br>**quiero** recibir una notificación push instantánea en mi celular,<br>**para** no quedarme sin insumos básicos. | Escenario 1: **Dado que** el dispensador detecta un nivel bajo de grano, **cuando** se cruza el umbral crítico, **entonces** recibo una notificación instantánea con el mensaje personalizado.<br><br>**Escenario 2:** **Dado que** el dispensador detecta un nivel bajo de grano, **cuando** se agota totalmente, **entonces** recibo una notificación de agotamiento de stock. | EP02 |
| **TS04** | Servicio de Notificaciones Push (Firebase/APNs) | Configurar la infraestructura de notificaciones push (ej: Firebase Cloud Messaging para Android) en el backend C# y en la app Flutter. | Escenario 1: API endpoint funcional para envío de notificaciones. Pruebas de envío y recepción de notificaciones exitosas. | EP02 |
| **TS05** | Implementación del Backend para Gestión de Reglas de Alerta | Desarrollar la lógica de negocio en el backend C# para evaluar las lecturas procesadas contra los umbrales configurados. | Escenario 1: API endpoint `GET /api/active-alerts` creado y validado. Pruebas unitarias para múltiples escenarios de evaluación de umbrales. | EP02 |
| **TS06** | Sincronización de Base de Datos entre Backend y Móvil | Implementar mecanismos eficientes de sincronización de base de datos para asegurar una vista de stock casi en tiempo real en la aplicación móvil. | Escenario 1: API endpoint funcional para sincronización de datos. Pruebas de sincronización exitosas. | EP02 |

---

### Epic Story 3 | Panel de Control Centralizado para Usuarios Finales (Web/Angular)

| Epic / Story ID | Título | Descripción | Criterios de Aceptación | Relacionado con (Epic ID) |
| :--- | :--- | :--- | :--- | :--- |
| **US06** | Visualización de Stock Actual en Panel Web | **Como** usuario del hogar,<br>**quiero** ver el stock actual de todos mis granos en una interfaz web centralizada,<br>**para** tener una visión rápida de mi alacena. | **Escenario 1:** **Dado que** accedo al panel web y mis credenciales son válidas, **cuando** se carga la página principal, **entonces** veo widgets claros con el porcentaje de stock de cada grano.<br><br>**Escenario 2:** **Dado que** accedo al panel web y mis credenciales son válidas, **cuando** paso el cursor sobre un widget, **entonces** veo el valor exacto en gramos. | EP03 |
| **US07** | Visualización de Gráficos de Consumo Histórico | **Como** usuario del hogar,<br>**quiero** ver gráficos de mi historial de consumo de granos,<br>**para** identificar patrones y optimizar mis compras. | **Escenario 1:** **Dado que** estoy en la pestaña de analítica, **cuando** selecciono un rango de fechas, **entonces** veo un gráfico de línea detallado con la disminución del stock a lo largo del tiempo.<br><br>**Escenario 2:** **Dado que** estoy en la pestaña de analítica, **cuando** selecciono un rango de fechas, **entonces** veo un gráfico de barra con el consumo diario promedio. | EP03 |
| **US08** | Gestión de Inventario (Añadir/Editar Granos) | **Como** usuario del hogar,<br>**quiero** añadir nuevos tipos de granos y editar la información de los existentes en mi inventario,<br>**para** mantener el registro preciso de mi alacena. | **Escenario 1:** **Dado que** estoy en la gestión de inventario, **cuando** completo el formulario con el nuevo nombre de grano y capacidad, **entonces** el sistema actualiza el registro y asocia la telemetría correspondiente.<br><br>**Escenario 2:** **Dado que** estoy en la gestión de inventario, **cuando** decido eliminar un grano, **entonces** el sistema elimina el registro y la telemetría asociada. | EP03 |
| **TS07** | UI de Dashboard Front-end (Angular) | Crear la estructura de interfaz de usuario básica del dashboard en Angular (páginas, navegación, widgets de stock). | **Escenario 1:** UI de dashboard funcional con componentes básicos. Comunicación exitosa con el backend para visualización de stock. | EP03 |
| **TS08** | API Endpoint para Historial de Consumo | Desarrollar el endpoint de backend en C# para obtener lecturas históricas y crudas de los sensores. | **Escenario 1:** API endpoint `GET /api/historic-stock` creado y validado. Pruebas unitarias para recuperar una lista vacía y una lista con registros. | EP03 |

---

### Epic Story 4 | Funcionalidad de Monitoreo Remoto para Cuidadores (Móvil/Flutter)

| Epic / Story ID | Título | Descripción | Criterios de Aceptación | Relacionado con (Epic ID) |
| :--- | :--- | :--- | :--- | :--- |
| **US09** | Visualización Remota de Stock para Cuidadores | **Como** cuidador de un adulto mayor,<br>**quiero** ver el stock actual de granos en la casa de mi familiar,<br>**para** asegurar que siempre tenga insumos básicos disponibles. | **Escenario 1:** **Dado que** soy un cuidador autorizado, **cuando** abro la pestaña de "Familiar Monitoreado" en la app móvil, **entonces** veo los mismos widgets de stock que en el panel principal del hogar.<br><br>**Escenario 2:** **Dado que** soy un cuidador autorizado, **cuando** abro la pestaña de "Familiar Monitoreado", **entonces** veo el valor exacto en gramos para cada grano. | EP04 |
| **US10** | Recepción de Alertas de Stock Bajo de Familiar Monitoreado | **Como** cuidador de un adulto mayor,<br>**quiero** recibir una alerta push en mi celular cuando el stock de un grano baja del umbral en casa de mi familiar,<br>**para** gestionar la reposición de forma proactiva. | **Escenario 1:** **Dado que** estoy autorizado como cuidador, **cuando** el dispensador en casa del familiar detecta un nivel bajo de grano, **entonces** recibo una notificación instantánea específica para ese familiar.<br><br>**Escenario 2:** **Dado que** estoy autorizado como cuidador, **cuando** el dispensador en casa del familiar detecta un nivel bajo de grano, **entonces** recibo una notificación instantánea específica para ese familiar. | EP04 |
| **US11** | Visualización de Confirmación de Flujo Granular | **Como** cuidador de un adulto mayor,<br>**quiero** ver un registro de confirmación de flujo granular,<br>**para** saber si mi familiar ha estado utilizando el dispensador últimamente. | **Escenario 1:** **Dado que** estoy en los detalles del grano del familiar en la app móvil, **cuando** cargo la página, **entonces** veo un registro cronológico de los momentos en que se detectó flujo granular.<br><br>**Escenario 2:** **Dado que** estoy en los detalles del grano del familiar, **cuando** abro la pestaña de analítica, **entonces** veo un gráfico detallado con el uso del dispensador a lo largo del tiempo. | EP04 |
| **TS09** | Gestión de Permisos de Acceso Remoto (ACLs) | Implementar control de acceso a nivel de API para garantizar que los cuidadores solo puedan ver datos de los dispensadores que tienen legalmente vinculados. | **Escenario 1:** API endpoint funcional para gestión de permisos. Pruebas de permisos exitosas. | EP04 |
| **TS10** | API de Backend para Gestión de Cuentas de Cuidadores | Desarrollar la lógica de backend en C# para gestionar cuentas de usuario específicas para cuidadores (registro, autenticación, vinculación). | **Escenario 1:** API endpoint funcional para gestión de cuentas de cuidadores. Pruebas de creación de cuenta exitosa. | EP04 |

---

### Epic Story 5 | Presencia Digital y Captación de Usuarios

| Epic / Story ID | Título | Descripción | Criterios de Aceptación | Relacionado con (Epic ID) |
| :--- | :--- | :--- | :--- | :--- |
| **US12** | Landing Page del Proyecto | **Como** visitante,<br>**quiero** acceder a una landing page informativa cuando busco soluciones de domótica,<br>**para** conocer las funciones de DispenXCore y los beneficios de automatizar mi alacena. | **Escenario 1:** **Dado que** entro al enlace principal del proyecto, **cuando** navego por la sección de características, **entonces** visualizo claramente el beneficio de la triple validación de los sensores (peso, nivel y flujo).<br><br>**Escenario 2:** **Dado que** pertenezco al segmento de cuidadores, **cuando** accedo a la sección de beneficios, **entonces** puedo ver cómo el monitoreo remoto me ayuda a cuidar a mis familiares. | EP05 |
| **US13** | Formulario de Pre-registro y Leads | Cuando estoy interesado en adquirir el dispensador, quiero completar un formulario de suscripción, para recibir noticias sobre el lanzamiento oficial y ofertas exclusivas. | Dado que estoy en la sección de "Próximamente", cuando ingreso un correo electrónico válido, entonces el sistema almacena el lead y me muestra un mensaje de agradecimiento.<br><br>Dado que ingreso un formato de correo inválido, cuando intento enviar el formulario, entonces el sistema resalta el error y no permite el envío. | EP05 |
| **US14** | Sección de Testimonios y Casos de Éxito | Cuando evalúo la compra del dispositivo, quiero leer testimonios de otros usuarios (hogares y cuidadores), para confirmar la fiabilidad de la triple validación de los sensores. | Dado que navego por la landing page, cuando llego a la sección de testimonios, entonces puedo visualizar historias reales clasificadas por los dos segmentos objetivo.<br><br>Dado que los testimonios tienen imágenes, cuando hago clic en una, entonces se amplía para mostrar el dispositivo DispenXCore en un entorno real. | EP05 |
| **US15** | Centro de Ayuda y Preguntas Frecuentes (FAQ) | Cuando tengo dudas técnicas sobre el hardware (ESP32), quiero acceder a una sección de preguntas frecuentes, para resolver mis inquietudes sobre la instalación y el Wi-Fi sin contactar a soporte. | Dado que tengo dudas sobre la conectividad, cuando selecciono una categoría en el FAQ, entonces el sistema despliega las respuestas correspondientes de forma clara.<br><br>Dado que no encuentro mi duda en la lista, cuando hago clic en "Contactar Soporte", entonces el sistema me redirige al canal de atención directa. | EP05 |

<div style="page-break-after: always;"></div>

- **3.2. Impact Mapping**
  <br><br>
  **Segmento 1: Entusiastas de la Automatización y Hogares Inteligentes**
  
  <img src="https://imgur.com/S4yEY1o.png">
  <br><br>
  
<div style="page-break-after: always;"></div>

  **Segmento 2: Cuidadores de Adultos Mayores o Personas con Movilidad Reducida**
  <img src="https://imgur.com/4b1Ihgm.png">
  <br>

<div style="page-break-after: always;"></div>

- **3.3. Product Backlog**

| # Orden | User Story Id | Título | Descripción | Story Points |
| :---: | :--- | :--- | :--- | :---: |
| 1 | US12 | Landing Page del Proyecto | Como visitante, quiero acceder a una landing page informativa cuando busco soluciones de domótica, para conocer las funciones de DispenXCore y los beneficios de automatizar mi alacena. | 3 |
| 2 | US13 | Formulario de Pre-registro y Leads | Cuando estoy interesado en adquirir el dispensador, quiero completar un formulario de suscripción, para recibir noticias sobre el lanzamiento oficial y ofertas exclusivas. | 2 |
| 3 | US06 | Visualización de Stock Actual en Panel Web | Como usuario del hogar, quiero ver el stock actual de todos mis granos en una interfaz web centralizada cuando accedo al dashboard, para tener una visión rápida y detallada de mi alacena. | 5 |
| 4 | US05 | Recepción de Notificaciones Push de Stock Bajo | Como usuario del hogar, quiero recibir una notificación push instantánea en mi celular cuando un grano baja del umbral crítico, para no quedarme sin insumos básicos y gestionar las compras proactivamente. | 5 |
| 5 | US09 | Visualización Remota de Stock para Cuidadores | Como cuidador de un adulto mayor, quiero ver el stock actual de granos en la casa de mi familiar cuando un grano baja de nivel, para asegurar que siempre tenga insumos básicos disponibles. | 8 |
| 6 | US15 | Centro de Ayuda y Preguntas Frecuentes (FAQ) | Cuando tengo dudas técnicas sobre el hardware (ESP32), quiero acceder a una sección de preguntas frecuentes, para resolver mis inquietudes sobre la instalación y el Wi-Fi sin contactar a soporte. | 1 |
| 7 | US10 | Recepción de Alertas de Familiar Monitoreado | Como cuidador de un adulto mayor, quiero recibir una alerta push en mi celular cuando el stock de un grano baja del umbral en casa de mi familiar, para gestionar la reposición de forma proactiva. | 3 |
| 8 | US14 | Sección de Testimonios y Casos de Éxito | Cuando evalúo la compra del dispositivo, quiero leer testimonios de otros usuarios, para confirmar la fiabilidad de la triple validación de los sensores. | 1 |
| 9 | US03 | Configuración de Umbral de Alerta | Como usuario del hogar, quiero configurar un umbral de stock bajo personalizado para cada grano, para recibir alertas preventivas antes del agotamiento total. | 2 |
| 10 | US07 | Visualización de Gráficos de Consumo Histórico | Como usuario del hogar, quiero ver gráficos de mi historial de consumo de granos cuando accedo al dashboard, para identificar patrones y optimizar mis compras. | 5 |
| 11 | US11 | Visualización de Confirmación de Flujo Granular | Como cuidador de un adulto mayor, quiero ver un registro de confirmación de flujo granular, para saber si mi familiar ha estado utilizando el dispensador últimamente. | 3 |
| 12 | US08 | Gestión de Inventario (Añadir/Editar Granos) | Como usuario del hogar, quiero añadir nuevos tipos de granos y editar la información de los existentes en mi inventario, para mantener el registro preciso de mi alacena. | 3 |
| 13 | US04 | Visualización de Alertas Activas en la App | Como usuario del hogar, quiero ver una lista de todas las alertas activas de stock bajo en la aplicación móvil, para saber qué granos comprar pronto. | 2 |
| 14 | US01 | Visualización de Stock Crudo (Debug) | Como desarrollador de firmware, quiero ver los valores crudos de los sensores en tiempo real, para verificar la correcta calibración y funcionamiento del hardware durante la instalación inicial. | 2 |
| 15 | US02 | Actualización de Firmware Remota (OTA) | Como administrador del sistema, quiero poder actualizar el firmware de los dispensadores de forma remota, para corregir errores e implementar mejoras sin intervención física en el hogar. | 8 |
