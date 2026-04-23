## **Capítulo IV: Solution Software Design** 
- **4.1. Strategic-Level Domain-Driven Design** 
    - **4.1.1. Design-Level EventStorming** 
    
      Con el objetivo de comprender en profundidad el dominio y la lógica de funcionamiento de DispenXCore, se llevó a cabo una sesión de Event Storming. Esta dinámica permitió al equipo organizar el flujo de datos desde múltiples perspectivas: la interacción física del hardware, la gestión lógica del middleware y la experiencia del usuario final a través de las interfaces móviles y web.
    
      Se abordaron los siguientes puntos durante la sesión:
      
      * **Exploración del dominio y flujo de automatización:** Se analizó el ciclo de vida completo del producto, comenzando por el registro y vinculación del dispensador. Se puso especial énfasis en el flujo de telemetría: desde que los sensores capturan datos físicos de peso, nivel y flujo, hasta que el sistema procesa dicha información para determinar el estado del inventario en tiempo real.
      
      * **Identificación de eventos y comandos de control activo:** Utilizamos notas naranjas para los eventos de dominio y notas azules para los comandos. Para esto se siguieron las user stories realizadas previamente.
      
      * **Asignación de roles y actores del ecosistema:** Se diferenciaron claramente los actores: el **Usuario**, el **Hardware**, que actúa como un sistema autónomo que reporta telemetría.
      
      * **Políticas y reglas de negocio:** Se establecieron reglas de negocio para definir umbrales de alerta. Esto garantiza que las notificaciones push se envíen solo cuando el sistema detecta que el recipiente de uso ha alcanzado niveles críticos, optimizando la relevancia de las alertas para el usuario.
    
    **Evidencia de lo realizado en la reunión:**
    
    Paso 1: Recopilación de Eventos de dominio
    ![Event Storming DispenXCore1](/images/EventStorm1.png)
    
    Paso 2: Refinación de Eventos de dominio
    ![Event Storming DispenXCore2](/images/EventStorm2.png)
    
    Paso 3: Hallando Causas
    ![Event Storming DispenXCore3](/images/EventStorm3.png)
    **4.1.1.1. Candidate Context Discovery**
          
    Para identificar los Bounded Contexts candidatos buscamos entender los elementos importantes del sistema, identificando hitos donde el estado del negocio cambia drásticamente y la responsabilidad pasa de un componente a otro.

    ![Event Storming DispenXCore4](/images/EventStorm4.png)
    **4.1.1.2. Domain Message Flows Modeling**

    Para analizar y diseñar la arquitectura de comunicación de DispenXCore, se utiliza el Modelado de Flujos de Mensajes de Dominio. Este método ilustra de manera detallada la transferencia de información entre los Bounded Contexts y los sistemas externos mediante el intercambio de mensajes (Comandos, Eventos y Consultas).

    ![Domain Flow Message DispenXCore](/images/FlowMessage.png)     
    **4.1.1.3. Bounded Context Canvases** 

    **Users and Access**
    ![Users Bounded Canvas DispenXCore](/images/UsersBoundedCanvas.png)     

    **Inventory and Telemetry**
    ![Inventory Bounded Canvas DispenXCore](/images/InventoryBoundedCanvas.png)     

    **Notifications and Alerts**
    ![Notifications Bounded Canvas DispenXCore](/images/NotificationBoundedCanvas.png)     
    
    **4.1.2. Context Mapping**

    En esta sección desarrollamos un conjunto de *context maps* para visualizar las relaciones estructurales entre los *bounded contexts* de **DispenXCore**. A partir de la lógica de dominio establecida, exploramos distintas alternativas de diseño, cuestionando cómo cambiaría la estabilidad del sistema si agrupamos o dividimos las responsabilidades de telemetría y gestión de usuarios. Evaluamos cada propuesta considerando patrones de DDD como *Anti-corruption Layer*, *Customer/Supplier* y *Shared Kernel* para definir la arquitectura más robusta.

    **Opción 1: Estructura de Contextos Independientes**

    En esta propuesta mantenemos los tres *bounded contexts* completamente separados, utilizando relaciones de tipo *Customer/Supplier*.

    * **Descripción:** **Inventario y Telemetría** actúa como proveedor de datos para **Notificaciones y Alertas**. A su vez, **Usuarios y Accesos** provee la información de identidad necesaria para personalizar las alertas.
    * **Ventaja:** Existe una separación total de responsabilidades. Los cambios en el hardware no afectan la lógica de seguridad de los usuarios.
    * **Desventaja:** Requiere una alta coordinación y sincronización constante entre los tres contextos para que una alerta llegue al usuario correcto, aumentando la latencia en el procesamiento de mensajes.
    ![Option1 DispenXCore3](/images/Option1.png)

    **Opción 2: Arquitectura Basada en ACL y Shared Kernel**

    Esta alternativa busca equilibrar la autonomía de los equipos con la integridad de los datos, utilizando patrones específicos para proteger el núcleo del sistema.

    * **Inventario y Telemetría** se comunica con el hardware mediante una **Anti-corruption Layer (ACL)**. Esta capa traduce las señales crudas de los sensores de peso y nivel a un lenguaje que el dominio entienda, protegiendo al sistema de cambios en los protocolos del hardware.
    * **Usuarios y Accesos** y **Notificaciones y Alertas** comparten un **Shared Kernel** que contiene los modelos de "Perfil de Usuario" y "Tokens de Dispositivo". Esto asegura que ambos contextos hablen el mismo idioma al momento de dirigir una notificación push.
    * **Notificaciones y Alertas** mantiene una relación de **Customer/Supplier** con el contexto de Inventario, donde el contexto de Inventario es el proveedor de los eventos de stock crítico.
    ![Option3 DispenXCore3](/images/Option3.png)

    **Opción 3: Unificación de Core y Notificaciones**

    Esta alternativa propone unir los contextos de **Inventario y Telemetría** con **Notificaciones y Alertas** en un solo *bounded context* de "Gestión de Stock".

    * **Descripción:** Al estar en un mismo contexto, la detección de nivel crítico dispara la alerta de forma interna e inmediata sin necesidad de comunicación entre contextos.
    * **Ventaja:** Simplifica la arquitectura al reducir la cantidad de contextos y elimina la latencia de red entre la detección y la generación de la alerta.
    * **Desventaja:** Riesgo de crear un "Big Ball of Mud". Al combinar la infraestructura técnica de sensores con la lógica de mensajería (Firebase), el contexto asume demasiadas funciones, dificultando su mantenimiento y escalabilidad independiente.
    ![Option2 DispenXCore3](/images/Option2.png)

    **Elección**

    Se eligio la **opción 2**, ya que proporciona el mejor equilibrio entre la separación de responsabilidades y la facilidad de implementación. Al implementar una **Anti-corruption Layer**, garantizamos que el software sea agnóstico a cambios en los sensores físicos, lo cual es vital para un proyecto IoT. Asimismo, el uso de un **Shared Kernel** para la identidad del usuario optimiza la entrega de alertas sin duplicar la lógica de seguridad, brindando una experiencia fluida tanto para el usuario doméstico como para el cuidador remoto.
    
    **4.1.3. Software Architecture** 

    En esta sección, se explica la representación de la arquitectura de software para DispenXCore utilizando el C4 Model. Con estos diagramas se busca proporcionar una comprensión clara de la arquitectura, permitiendo a los miembros del equipo, stakeholders y futuros desarrolladores entiender cómo se organiza y comunica el sistema.

    **4.1.3.1. Software Architecture System Landscape Diagram** 
  
    El ecosistema de DispenXCore está diseñado para servir a dos perfiles de usuario principales: el Usuario Doméstico, que busca automatización en su cocina, y el Cuidador, que supervisa el abastecimiento de forma remota. El sistema central, DispenXCore, actúa como el núcleo que procesa la información proveniente del Hardware IoT (Sensores). Además, se integra con Firebase Cloud Messaging (FCM) para la entrega de notificaciones en tiempo real.

    ![SystemLandscape DispenXCore](/images/SystemLandscape.png)

    **4.1.3.2. Software Architecture Context Level Diagrams**

    Este diagrama muestra que el sistema DispenXCore interactúa con dos tipos de usuarios: el Usuario Doméstico, que utiliza el sistema para digitalizar la gestión de su cocina, configurar umbrales de alerta y monitorear niveles de stock. Luego el Cuidador, que supervisa de forma remota el abastecimiento de sus familiares. DispenXCore también se comunica con dos sistemas externos: el Hardware DispenXCore, que mediante sensores y actuadores proporciona datos de telemetría y ejecuta el auto-rellenado, y el Firebase Cloud Messaging, encargado de distribuir las notificaciones preventivas a los dispositivos móviles de los usuarios. 

    ![SystemContext DispenXCore](/images/SystemContext.png)

    **4.1.3.3. Software Architecture Container Level Diagrams** 

    Este diagrama muestra que el sistema DispenXCore está compuesto por diversos contenedores que trabajan en conjunto para ofrecer una solución integral. En el entorno del usuario, se dispone de una Landing Page informativa, una Aplicación Web y una Aplicación Móvil dedicada al monitoreo en tiempo real.

    ![DiagramContainer DispenXCore](/images/ContainerDiagram.png)

    **4.1.3.4. Software Architecture Deployment Diagrams** 

    Este diagrama ilustra la topología física y la distribución de los componentes de DispenXCore en un ecosistema que integra la computación perimetral con servicios de nube de alta disponibilidad.

    ![DiagramDeployment DispenXcore](/images/DeploymentDiagram.png)

- **4.2. Tactical-Level Domain-Driven Design** 
- **4.2.1. Bounded Context: Inventory and Telemetry**

  Este Bounded Context es el núcleo de captura de datos físicos de DispenXCore. Su responsabilidad es gestionar el ciclo de vida completo del dispensador, desde su registro y vinculación hasta la recepción, procesamiento y almacenamiento de las lecturas de los tres sensores (ultrasonido, celda de carga e infrarrojo). Actúa como el proveedor principal de eventos de telemetría hacia el contexto de Notificaciones y Alertas, siendo el punto de entrada de toda la información del mundo físico al sistema digital.

    - **4.2.1.1. Domain Layer**

      En la Domain Layer del bounded context Inventory and Telemetry se definen los modelos, eventos y servicios que encapsulan la lógica pura del monitoreo de insumos. Esta capa es agnóstica a cualquier tecnología externa; representa únicamente qué es un dispensador, qué significa una lectura de sensor y cómo se determina el estado del stock en un momento dado.

      **Sub-capa Model:**

      | Tipo         | Nombre              | Descripción                                                                                                                             | Responsabilidad Principal                                                                                      | Relación con otros elementos                                             |
      |--------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
      | Aggregate    | Dispenser           | Entidad principal que representa el dispositivo físico registrado y vinculado a la cuenta de un usuario.                                | Controlar el ciclo de vida del dispensador (ACTIVE, INACTIVE, OFFLINE) y centralizar sus lecturas asociadas.  | Se vincula a un `user_id` del contexto Users and Access.                 |
      | Aggregate    | StockReading        | Entidad que representa una captura de datos realizada por los sensores en un instante específico.                                       | Almacenar y validar los valores crudos de peso, nivel y flujo reportados por el hardware en cada ciclo.       | Pertenece a un `Dispenser`. Genera el evento `TelemetryReceived`.        |
      | Value Object | SensorData          | Encapsula los tres valores medidos simultáneamente: peso en gramos, nivel en porcentaje y flujo en g/s.                                 | Garantizar que los valores capturados sean coherentes y no negativos antes de ser persistidos.                | Atributo interno de `StockReading`.                                      |
      | Value Object | DispenserStatus     | Enum que representa el estado operativo del dispositivo: `ONLINE`, `OFFLINE`, `LOW_BATTERY`, `SENSOR_ERROR`.                           | Representar el estado actual del hardware de forma inmutable para evitar estados inconsistentes.              | Atributo de `Dispenser`.                                                 |
      | Value Object | GrainType           | Enum controlado que identifica el tipo de insumo contenido: `RICE`, `SUGAR`, `LEGUMES`, `OTHER`.                                       | Asegurar que solo se registren tipos de insumo válidos dentro del sistema.                                    | Atributo de `Dispenser`.                                                 |
      | Domain Event | TelemetryReceived   | Evento publicado cada vez que el ESP32 envía una nueva lectura de sensores al backend y esta es validada correctamente.                 | Notificar al contexto de Notifications and Alerts que hay datos nuevos disponibles para evaluación de umbral. | Disparado por `Dispenser`. Escuchado por `TelemetryReceivedSubscriber`.  |
      | Domain Event | DispenserRegistered | Evento emitido cuando un usuario vincula exitosamente un nuevo dispensador a su cuenta por primera vez.                                 | Informar a otros contextos que existe un nuevo dispositivo activo en el ecosistema.                           | Publicado hacia el contexto Users and Access.                            |

      **Sub-capa Service:**

      | Tipo           | Nombre                      | Descripción                                                                                                                            | Responsabilidad Principal                                                                                                         | Relación con otros elementos                           |
      |----------------|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
      | Interface      | TelemetryIngestionService   | Contrato que define cómo el sistema recibe y procesa los datos crudos provenientes del ESP32.                                          | Definir el método `ProcessReading(dispenserId, sensorData)` que desencadena el flujo completo de telemetría.                     | Implementado en la Infrastructure Layer.               |
      | Domain Service | StockLevelCalculatorService | Servicio que calcula el porcentaje de stock restante a partir del peso actual y la capacidad máxima configurada del dispensador.        | Centralizar la lógica de conversión de gramos a porcentaje para que ninguna otra capa duplique este cálculo crítico.             | Usado por los CommandHandlers de la Application Layer. |

    - **4.2.1.2. Interface Layer**

      En la Interface Layer del bounded context Inventory and Telemetry se implementan los controladores, recursos y ensambladores que gestionan la comunicación entre los clientes externos (App Móvil, App Web y ESP32) y la lógica de dominio. Esta capa expone los endpoints REST necesarios para registrar dispensadores, consultar el estado del stock en tiempo real y recibir las lecturas de telemetría enviadas por el ESP32 mediante HTTP POST.

      **Sub-capa REST:**

      | Tipo       | Nombre                         | Descripción                                                                                          | Responsabilidad Principal                                                                                     | Relación con otros elementos                             |
      |------------|--------------------------------|------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
      | Controller | DispenserController            | Gestiona las solicitudes HTTP relacionadas al registro y administración de dispensadores.             | Recibir solicitudes de vinculación, actualización de estado y consulta de dispensadores del usuario.         | Usa `DispenserResource` y `RegisterDispenserAssembler`.  |
      | Controller | TelemetryController            | Gestiona las solicitudes HTTP POST de entrada de datos desde el ESP32.                               | Recibir las lecturas de los sensores enviadas por el ESP32 vía Wi-Fi cada 1-2 segundos y procesarlas.        | Usa `TelemetryResource` y `TelemetryIngestionService`.   |
      | Controller | StockReadingController         | Gestiona las solicitudes HTTP para consultar el historial de lecturas de un dispensador.             | Exponer endpoints de solo lectura para que la App Web y Móvil visualicen el historial de stock.             | Usa `StockReadingResource` y `StockReadingAssembler`.    |
      | Resource   | DispenserResource              | Estructura JSON para representar los datos de un dispensador en las respuestas de la API.            | Exponer los atributos del dispensador (id, nombre, tipo de grano, estado) de forma estructurada al cliente. | Usado por `DispenserController`.                         |
      | Resource   | TelemetryResource              | Estructura JSON que recibe los datos crudos del ESP32 (peso, nivel, flujo, distancia ultrasonido).   | Representar la lectura de sensores enviada por el ESP32 en un formato que el sistema comprenda.             | Usado por `TelemetryController`.                         |
      | Resource   | StockReadingResource           | Estructura JSON para representar una lectura de stock procesada en las respuestas de la API.         | Exponer los valores ya calculados (porcentaje de stock, timestamp) de forma estructurada al cliente.        | Usado por `StockReadingController`.                      |
      | Assembler  | RegisterDispenserAssembler     | Convierte el `DispenserResource` recibido en un comando `RegisterDispenserCommand`.                  | Asegurar una transformación limpia entre los datos de la API y los comandos del dominio.                    | Usado por `DispenserController`.                         |
      | Assembler  | TelemetryFromResourceAssembler | Convierte el `TelemetryResource` recibido en un comando `ProcessTelemetryCommand`.                   | Prevenir inconsistencias al transformar los datos crudos del ESP32 a comandos de la Application Layer.     | Usado por `TelemetryController`.                         |

    - **4.2.1.3. Application Layer**

      En la Application Layer del bounded context Inventory and Telemetry se gestionan los comandos y eventos que coordinan la ejecución de la lógica de negocio entre la Interface Layer y el Domain. Esta capa no contiene lógica de dominio propia; su rol es orquestar el flujo de datos, invocar los servicios y repositorios correctos, y publicar los eventos de dominio resultantes hacia otros contextos del sistema.

      **Sub-capa Internal:**

      | Tipo           | Nombre                          | Descripción                                                                                                                                             | Responsabilidad Principal                                                                                                        | Relación con otros elementos                                                         |
      |----------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
      | CommandHandler | RegisterDispenserCommandHandler | Ejecuta la lógica de registro de un nuevo dispensador, validando que el dispositivo no esté previamente vinculado y persistiendo la entidad.            | Crear un nuevo `Dispenser` aggregate, asignarle su estado inicial `ONLINE` y publicar el evento `DispenserRegistered`.          | Usa `DispenserRepository` y `DomainEventPublisher`.                                  |
      | CommandHandler | ProcessTelemetryCommandHandler  | Ejecuta el flujo completo de ingesta de telemetría: valida los datos del sensor, calcula el porcentaje de stock y persiste la nueva lectura.            | Crear un `StockReading`, invocar `StockLevelCalculatorService` para calcular el nivel y publicar el evento `TelemetryReceived`.  | Usa `StockReadingRepository`, `StockLevelCalculatorService` y `DomainEventPublisher`.|
      | CommandHandler | UpdateDispenserStatusHandler    | Ejecuta la actualización del estado operativo de un dispensador cuando el ESP32 reporta un cambio (ej. batería baja, sensor desconectado).              | Modificar el `DispenserStatus` del aggregate `Dispenser` y persistir el cambio en el repositorio.                               | Usa `DispenserRepository`.                                                           |
      | EventPublisher | DomainEventPublisher            | Componente encargado de publicar los eventos de dominio generados por los CommandHandlers hacia los contextos suscriptores.                             | Publicar eventos como `TelemetryReceived` y `DispenserRegistered` para que el contexto Notifications and Alerts pueda reaccionar.| Usado por todos los CommandHandlers de este contexto.                               |

    - **4.2.1.4. Infrastructure Layer**

      En la Infrastructure Layer del bounded context Inventory and Telemetry se implementan los componentes técnicos que soportan la persistencia de datos, la comunicación con el ESP32 y la traducción del payload JSON al lenguaje del dominio. Esta capa es la única que conoce los detalles tecnológicos del sistema, como el mecanismo de HTTP Polling del microcontrolador, el motor de base de datos utilizado y la implementación concreta de los repositorios definidos en el dominio.

      **Sub-capa Repository:**

      | Tipo      | Nombre                     | Descripción                                                                                         | Responsabilidad Principal                                                                                        | Relación con otros elementos                                                  |
      |-----------|----------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
      | Interface | DispenserRepository        | Interfaz que define los métodos de acceso y manipulación de datos para el aggregate `Dispenser`.    | Definir operaciones como `FindById`, `FindByUserId`, `Save` y `UpdateStatus` para la gestión de dispensadores.  | Definida en el dominio, implementada en esta capa.                            |
      | Class     | DispenserRepositoryImpl    | Implementación concreta de `DispenserRepository` conectada al motor de base de datos del sistema.  | Ejecutar las operaciones de persistencia del `Dispenser` aggregate en SQL Server o PostgreSQL.                   | Usada por `RegisterDispenserCommandHandler` y `UpdateDispenserStatusHandler`. |
      | Interface | StockReadingRepository     | Interfaz que define los métodos de acceso y manipulación de datos para el aggregate `StockReading`. | Definir operaciones como `Save`, `FindByDispenserId` y `FindLatestByDispenserId` para el historial de stock.    | Definida en el dominio, implementada en esta capa.                            |
      | Class     | StockReadingRepositoryImpl | Implementación concreta de `StockReadingRepository` conectada al motor de base de datos.            | Ejecutar las operaciones de persistencia de cada lectura de sensores capturada por el ESP32.                    | Usada por `ProcessTelemetryCommandHandler`.                                   |

      **Sub-capa External Services:**

      | Tipo  | Nombre              | Descripción                                                                                                                                      | Responsabilidad Principal                                                                                                                    | Relación con otros elementos                              |
      |-------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
      | Class | HttpPollingAdapter  | Componente que gestiona la recepción de los HTTP POST enviados por el ESP32 cada 1-2 segundos con las lecturas de los tres sensores.             | Recibir el payload JSON del ESP32, verificar su estructura y entregarlo a la `SensorDataACL` para su traducción al modelo del dominio.       | Entrega datos procesados al `TelemetryController`.        |
      | Class | SensorDataACL       | Capa de traducción que convierte el payload JSON crudo del ESP32 al Value Object `SensorData` del dominio.                                       | Proteger al dominio de cambios en el formato de datos enviado por el ESP32, actuando como barrera entre el mundo físico y el sistema digital.| Usada por `HttpPollingAdapter` antes de invocar al controlador. |

      **Sub-capa Event Handling:**

      | Tipo         | Nombre                          | Descripción                                                                                        | Responsabilidad Principal                                                                                                      | Relación con otros elementos                                                        |
      |--------------|---------------------------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
      | EventHandler | TelemetryReceivedEventHandler   | Procesa el evento `TelemetryReceived` publicado por el `DomainEventPublisher` de este contexto.    | Retransmitir el evento hacia el contexto Notifications and Alerts para que evalúe si corresponde generar una alerta de stock. | Consume eventos del `DomainEventPublisher`. Notifica al contexto Notifications and Alerts. |
      | EventHandler | DispenserRegisteredEventHandler | Procesa el evento `DispenserRegistered` publicado al vincular un nuevo dispositivo al sistema.     | Registrar en el log de auditoría la vinculación del nuevo dispensador y notificar al contexto Users and Access si corresponde.| Consume eventos del `DomainEventPublisher`.                                         |

    - **4.2.1.5. Bounded Context Software Architecture Component Level Diagrams**

      A nivel de componentes, este contexto actúa como el punto de entrada del mundo físico al sistema digital. El ESP32 envía las lecturas de los sensores al backend mediante HTTP POST cada 1-2 segundos, donde la `SensorDataACL` traduce el payload JSON crudo al modelo del dominio, protegiendo al sistema de cambios en el formato de datos del hardware. Los controladores REST reciben tanto la telemetría del ESP32 como las solicitudes de la App Móvil y Web, delegando la lógica a los CommandHandlers correspondientes. El `ProcessTelemetryCommandHandler` orquesta el cálculo de porcentaje de stock mediante el `StockLevelCalculatorService`, persiste la lectura en el repositorio y finaliza publicando el evento `TelemetryReceived` hacia el contexto de Notifications and Alerts.
        - **4.2.1.6. Bounded Context Software Architecture Code Level Diagrams**
            - **4.2.1.6.1. Bounded Context Domain Layer Class Diagrams**
              En esta sección se presenta el diagrama de clases del bounded context Inventory and Telemetry. La clase `Dispenser` cumple el rol central como aggregate raíz, encapsulando el estado operativo del dispositivo físico y su relación con las lecturas de sensores. La clase `StockReading` registra cada captura de datos del ESP32, compuesta por el Value Object `SensorData` que agrupa los tres valores medidos: peso, nivel y flujo. Los Domain Events `TelemetryReceived` y `DispenserRegistered` son publicados por el aggregate `Dispenser` al detectar cambios de estado relevantes.

              ![Domain Class Diagram Inventory and Telemetry](/images/ComponentDiagramInventory.png)

            - **4.2.1.6.2. Bounded Context Database Design Diagram**

              En esta sección se presenta el diseño de la base de datos correspondiente al bounded context Inventory and Telemetry, donde se estructuran las cuatro tablas principales para la gestión de dispensadores, el historial de lecturas de sensores, el registro de eventos de estado y la configuración de sensores editable desde la app. Este diagrama garantiza la correcta relación entre las entidades y la trazabilidad de cada captura de telemetría enviada por el ESP32.

              ![Database Design Inventory and Telemetry](/images/ClassDiagramInventory.png)

              **Tabla: dispensers**

              | Columna        | Tipo         | Descripción                                                                             |
              |----------------|--------------|-----------------------------------------------------------------------------------------|
              | id             | UUID (PK)    | Identificador único del dispensador.                                                    |
              | user_id        | UUID (FK)    | ID del propietario del dispositivo (Referencia al contexto Users and Access).           |
              | name           | VARCHAR(100) | Nombre descriptivo asignado por el usuario (ej: "Dispensador Cocina").                 |
              | grain_type     | VARCHAR(50)  | Tipo de insumo contenido: RICE, SUGAR, LEGUMES, OTHER.                                 |
              | max_capacity_g | FLOAT        | Capacidad máxima del recipiente en gramos, usada para calcular el porcentaje de stock. |
              | status         | VARCHAR(20)  | Estado operativo del dispositivo: ONLINE, OFFLINE, LOW_BATTERY, SENSOR_ERROR.          |
              | created_at     | TIMESTAMP    | Fecha y hora de registro del dispensador en el sistema.                                 |
              | updated_at     | TIMESTAMP    | Fecha y hora de la última actualización del registro.                                   |

              **Tabla: stock_readings**

              | Columna           | Tipo      | Descripción                                                                                |
              |-------------------|-----------|--------------------------------------------------------------------------------------------|
              | id                | UUID (PK) | Identificador único de la lectura de sensores.                                             |
              | dispenser_id      | UUID (FK) | ID del dispensador que generó la lectura (Referencia a `dispensers`).                     |
              | weight_grams      | FLOAT     | Peso del insumo en gramos capturado por la celda de carga.                                 |
              | level_percentage  | FLOAT     | Porcentaje de stock calculado a partir del peso y la capacidad máxima del dispensador.     |
              | flow_rate_gs      | FLOAT     | Flujo de salida del insumo en gramos por segundo, capturado por el sensor infrarrojo.      |
              | raw_ultrasonic_cm | FLOAT     | Distancia cruda en centímetros reportada por el sensor ultrasonido antes de ser procesada. |
              | recorded_at       | TIMESTAMP | Fecha y hora exacta en que el ESP32 realizó y envió la lectura al backend.                 |

              **Tabla: dispenser_events**

              | Columna         | Tipo        | Descripción                                                                        |
              |-----------------|-------------|------------------------------------------------------------------------------------|
              | id              | UUID (PK)   | Identificador único del evento registrado.                                         |
              | dispenser_id    | UUID (FK)   | ID del dispensador asociado al evento (Referencia a `dispensers`).                |
              | event_type      | VARCHAR(50) | Tipo de evento ocurrido: REGISTERED, STATUS_CHANGED, SENSOR_ERROR, BACK_ONLINE.  |
              | previous_status | VARCHAR(20) | Estado operativo del dispensador antes del cambio.                                 |
              | new_status      | VARCHAR(20) | Estado operativo del dispensador después del cambio.                               |
              | occurred_at     | TIMESTAMP   | Fecha y hora en que ocurrió el evento.                                             |
              | details         | TEXT        | Descripción adicional del evento (ej: "Sensor ultrasonido sin respuesta por 10s"). |

              **Tabla: dispenser_sensor_config**

              | Columna                   | Tipo      | Descripción                                                                                          |
              |---------------------------|-----------|------------------------------------------------------------------------------------------------------|
              | id                        | UUID (PK) | Identificador único de la configuración.                                                             |
              | dispenser_id              | UUID (FK) | ID del dispensador al que pertenece esta configuración, relación 1 a 1 (Referencia a `dispensers`). |
              | polling_interval_ms       | INT       | Frecuencia de envío de datos del ESP32 en milisegundos (valor por defecto: 1000).                   |
              | weight_calibration_factor | FLOAT     | Factor de calibración aplicado a la celda de carga para corregir lecturas de peso.                  |
              | ultrasonic_offset_cm      | FLOAT     | Offset de corrección del sensor ultrasonido en centímetros.                                          |
              | min_flow_threshold_gs     | FLOAT     | Flujo mínimo detectable en g/s antes de considerar que el insumo está siendo dispensado.            |
              | updated_at                | TIMESTAMP | Última vez que el usuario modificó la configuración desde la app.                                    |
    - **4.2.2. Bounded Context: Notifications and Alerts** 

      Este Bounded Context es el corazón de la proactividad de DispenXCore. Su objetivo es procesar los eventos de telemetría provenientes del hardware, evaluarlos frente a reglas de negocio (umbrales) y despachar notificaciones multicanal (Push para Flutter y Web para Angular) tanto a dueños de casa como a cuidadores.
        - **4.2.2.1. Domain Layer** 
        
          Define la lógica pura de las alertas y la estructura de los mensajes, siendo agnóstico a si el mensaje se envía por Firebase o correo.

          **Sub-capa Model:** 

          | Tipo           | Nombre            | Descripción                                                                 | Responsabilidad Principal                                              | Relación                              |
          |----------------|------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------|----------------------------------------|
          | Aggregate      | Alert            | Entidad que representa la ocurrencia de un evento de stock bajo o crítico. | Controlar el ciclo de vida de una alerta (Generada, Atendida, Archivada). | Se vincula a un DispenserId.           |
          | Aggregate      | Notification     | El mensaje físico enviado al usuario.                                      | Gestionar el contenido del mensaje y su estado de lectura.            | Asociada a un User.                    |
          | Value Object   | Threshold        | Valor numérico (gramos o %) que dispara la alerta.                         | Validar que el umbral sea un valor lógico y no negativo.              | Parte de la configuración del usuario. |
          | Value Object   | NotificationType | Enum: CRITICAL_STOCK, LOW_STOCK, SYSTEM_UPDATE.                            | Clasificar la severidad de la alerta.                                 | Atributo de Notification.              |
          | Domain Event   | AlertTriggered   | Evento que ocurre cuando el stock cruza el umbral.                         | Notificar internamente que se debe preparar un mensaje.               | Disparado por la lógica de dominio.    |
          | Domain Event   | NotificationSent | Registro de que el mensaje salió hacia el proveedor (FCM).                | Trazabilidad del despacho.                                            | Usado para auditoría.                  |

          **Sub-capa Service:**
          | Tipo            | Nombre                   | Descripción                                   | Responsabilidad Principal                                             |
          |-----------------|--------------------------|-----------------------------------------------|------------------------------------------------------------------------|
          | Interface       | PushNotificationService  | Contrato para el envío de mensajes.           | Definir el método SendPush(targetToken, message).                     |
          | Domain Service  | AlertEvaluationService   | Compara telemetría vs umbrales.               | Lógica para decidir si una lectura de sensor merece una alerta.       |
          
        - **4.2.2.2. Interface Layer** 

          Gestiona los endpoints para que el usuario configure sus alertas desde la App Móvil o Web.

          **Sub-capa REST:**
          | Tipo        | Nombre                  | Responsabilidad Principal                                                                 |
          |-------------|--------------------------|--------------------------------------------------------------------------------------------|
          | Controller  | AlertConfigController    | Endpoints para que el usuario defina sus umbrales (ej: "Avisame al 15%").                |
          | Controller  | NotificationController  | Endpoints para listar notificaciones recibidas y marcarlas como leídas.                  |
          | Resource    | AlertConfigResource     | Estructura JSON para enviar/recibir límites de stock.                                    |
          | Resource    | NotificationResource    | Estructura JSON con el mensaje, fecha y estado de lectura.                               |
          | Assembler   | AlertConfigAssembler    | Transforma DTOs de la API a comandos de configuración.                                   |
          
        - **4.2.2.3. Application Layer** 

          Coordina las acciones de respuesta ante eventos externos (telemetría).

          **Sub-capa Internal:**

          | Tipo             | Nombre                        | Responsabilidad Principal                                                                 | Relación                               |
          |------------------|-------------------------------|--------------------------------------------------------------------------------------------|----------------------------------------|
          | CommandHandler   | CreateAlertConfigHandler      | Guarda la preferencia de umbral del usuario para un dispensador.                          | Usa AlertRepository.                   |
          | CommandHandler   | MarkAsReadHandler             | Cambia el estado de una notificación a "leída".                                           | Usa NotificationRepository.            |
          | EventSubscriber  | TelemetryReceivedSubscriber   | Crítico: Escucha eventos del contexto de Inventory y dispara la evaluación de alertas.    | Punto de unión entre contextos.        |

        - **4.2.2.4. Infrastructure Layer** 

          Implementaciones técnicas y conexiones con servicios externos.

          **Sub-capa External Services:**

          | Tipo  | Nombre                           | Descripción                                                                 |
          |-------|----------------------------------|-----------------------------------------------------------------------------|
          | Class | FirebaseCloudMessagingProvider   | Implementación de PushNotificationService usando el SDK de Firebase para Flutter/Web. |
          | Class | SignalRNotificationProvider      | (Opcional) Para actualizaciones en tiempo real en el Dashboard de Angular. |

          **Sub-capa Repository:**

          | Tipo  | Nombre                     | Responsabilidad                                                                 |
          |-------|----------------------------|----------------------------------------------------------------------------------|
          | Class | AlertRepositoryImpl        | Persistencia de las alertas históricas generadas en SQL Server/PostgreSQL.     |
          | Class | NotificationRepositoryImpl | Gestión de la bandeja de entrada de mensajes del usuario.                      |

        - **4.2.2.5. Bounded Context Software Architecture Component Level Diagrams**   

          A nivel de componentes, este contexto actúa como un Reactor. Recibe datos de telemetría (Input), los procesa contra las reglas de umbral en la base de datos (Logic) y genera una salida hacia Firebase Cloud Messaging (Output).

        - **4.2.2.6. Bounded Context Software Architecture Code Level Diagrams** 
            - **4.2.2.6.1. Bounded Context Domain Layer Class Diagrams** 
            - **4.2.2.6.2. Bounded Context Database Design Diagram**
                     <img src="https://i.imgur.com/m4kiSSr.png">
              **Tabla: alert_configurations**
              | Columna                      | Tipo        | Descripción                                                                 |
              |------------------------------|-------------|-----------------------------------------------------------------------------|
              | id                           | UUID (PK)   | Identificador único de la configuración de alerta.                         |
              | user_id                      | UUID (FK)   | ID del propietario del dispensador (Referencia al contexto Users).         |
              | dispenser_id                 | UUID (FK)   | ID del dispositivo físico (Referencia al contexto Inventory).              |
              | grain_type                   | VARCHAR(50) | Nombre del insumo (ej: "Arroz Extra", "Azúcar Rubia").                     |
              | low_threshold_percentage     | FLOAT       | Porcentaje de stock para disparar alerta preventiva (Default: 15.0).       |
              | critical_threshold_percentage| FLOAT       | Porcentaje de stock para disparar alerta de urgencia (Default: 5.0).       |
              | is_enabled                   | BOOLEAN     | Define si el usuario desea recibir notificaciones para este grano.         |
              | created_at                   | TIMESTAMP   | Fecha de creación del registro.                                            |

              **Tabla: notifications**
              | Columna         | Tipo        | Descripción                                                                                  |
              |------------------|-------------|----------------------------------------------------------------------------------------------|
              | id               | UUID (PK)   | Identificador único de la alerta generada.                                                   |
              | user_id          | UUID (FK)   | Usuario que debe visualizar la notificación.                                                 |
              | alert_config_id  | UUID (FK)   | Relación con la configuración que disparó la alerta.                                         |
              | type             | ENUM        | Categoría de la alerta (LOW_STOCK, CRITICAL_STOCK, etc.).                                    |
              | title            | VARCHAR(150)| Título corto de la notificación (ej: "¡Stock Crítico!").                                     |
              | message_body     | TEXT        | Mensaje detallado enviado al usuario.                                                        |
              | triggered_value  | FLOAT       | El valor exacto del sensor (gramos/%) detectado al momento del disparo.                     |
              | created_at       | TIMESTAMP   | Fecha y hora exacta de la detección.                                                        |

              **Tabla: user_push_tokens**
              | Columna       | Tipo         | Descripción                                                                 |
              |---------------|--------------|-----------------------------------------------------------------------------|
              | id            | UUID (PK)    | Identificador único del registro de dispositivo.                           |
              | user_id       | UUID (FK)    | ID del usuario dueño del dispositivo.                                      |
              | device_token  | VARCHAR(255) | Token único generado por Firebase para este dispositivo móvil/web.         |
              | device_os     | VARCHAR(20)  | Sistema operativo del dispositivo (Android, iOS, Web).                     |
              | last_used_at  | TIMESTAMP    | Última vez que se envió una notificación con éxito a este token.           |
              | is_active     | BOOLEAN      | Indica si el token sigue siendo válido para envíos.                        |

              **Tabla: notification_deliveries**
              | Columna              | Tipo         | Descripción                                                                                  |
              |----------------------|--------------|----------------------------------------------------------------------------------------------|
              | id                   | UUID (PK)    | Identificador único del intento de envío.                                                   |
              | notification_id      | UUID (FK)    | Relación con la notificación lógica.                                                        |
              | device_token_id      | UUID (FK)    | Dispositivo específico al que se intentó enviar.                                            |
              | status               | ENUM         | Estado del envío (PENDING, SENT, DELIVERED, FAILED, READ).                                  |
              | provider_response_id | VARCHAR(100) | ID de rastreo devuelto por el proveedor externo (FCM).                                      |
              | sent_at              | TIMESTAMP    | Fecha y hora en que se despachó el mensaje.                                                 |
              | error_message        | TEXT         | Descripción del error en caso de que el envío falle (ej: "Token expired").                  |

              **Tabla: caregiver_subscriptions**
              | Columna            | Tipo       | Descripción                                                                 |
              |--------------------|------------|-----------------------------------------------------------------------------|
              | id                 | UUID (PK)  | Identificador único de la suscripción de monitoreo.                        |
              | caregiver_id       | UUID (FK)  | ID del usuario que actúa como cuidador.                                    |
              | monitored_user_id  | UUID (FK)  | ID del familiar que está siendo monitoreado.                               |
              | alert_config_id    | UUID (FK)  | Configuración específica del dispensador que el cuidador desea vigilar.    |
              | is_active          | BOOLEAN    | Define si el cuidador tiene el permiso de monitoreo activo actualmente.    |
                            
    - **4.2.3. Bounded Context: Users and Access**    
    <br> En el bounded context User se aborda la gestión de identidad y acceso de los usuarios dentro del sistema. Este módulo garantiza la autenticación, autorización y registro seguro, mediante el manejo de credenciales, roles, tokens JWT y auditoría de eventos críticos, asegurando la integridad y trazabilidad del acceso a los servicios. <br>
      
        - **4.2.3.1. Domain Layer**
        <br> En la Domain Layer del bounded context Users and Access se definen los modelos, comandos, eventos y servicios que encapsulan la lógica principal de identidad y autenticación. <br>
        **Sub-capa Model:**

          | Tipo          | Nombre         | Descripción                                                                                                                                        | Responsabilidad Principal                                                 | Relación con otros elementos                                 |
          |---------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------|
          | Aggregate     | User           | Entidad que modela a un usuario en la aplicación, encapsulando reglas de negocio como validación de credenciales y manejo del estado del usuario.  | Gestionar la lógica de negocio del usuario y garantizar su consistencia   | Relacionado con otros contextos, encapsula reglas de negocio |
          | Command       | SignInCommand  | Comando para iniciar sesión                                                                                                                        | Encapsular los datos necesarios para autenticar a un usuario              | Usado por el servicio de autenticación                       |
          | Command       | SignUpCommand  | Comando para registrar un nuevo usuario                                                                                                            | Encapsular los datos requeridos para crear un nuevo usuario               | Usado por el servicio de autenticación                       |
          | Value Object  | EmailAddress   | Value object dentro de User                                                                                                                        | Representa y valida el correo electrónico                                 | Relacionado con User                                         |
          | Value Object  | Name           | Value object dentro de User                                                                                                                        | Encapsula el nombre completo y valida formato                             | Relacionado con User                                         |
          | Domain Event  | UserRegistered | Evento emitido al registrar un nuevo usuario                                                                                                       | Notificar a otros contextos sobre el registro de un usuario               | Usado por servicios de aplicación e infraestructura          |
          | Domain Event  | UserSignedIn   | Evento disparado al iniciar sesión un usuario                                                                                                      | Informar a otros sistemas sobre el inicio de sesión                       | Usado por servicios de aplicación e infraestructura          |

          **Sub-capa Service:**

          | Tipo        | Nombre              | Descripción                          | Responsabilidad Principal                                | Relación con otros elementos                        |
          |-------------|---------------------|--------------------------------------|----------------------------------------------------------|-----------------------------------------------------|
          | Interface   | AuthCommandService  | Interfaz para manejar autenticación  | Establecer contrato para la lógica de autenticación      | Implementado en la capa de aplicación               |
          | Interface   | TokenService        | Interfaz para manejo de tokens       | Definir operaciones de generación y validación de tokens | Implementado en infraestructura como JwtServiceImpl |

          - **4.2.3.2. Interface Layer**
            <br> En la Interface Layer del bounded context Users and Access se implementan los controladores, recursos y validadores que gestionan la comunicación entre el cliente y la lógica de dominio mediante servicios REST. <br>
            **Sub-capa REST**

          | Tipo       | Nombre                             | Descripción                                        | Responsabilidad Principal                                                | Relación con otros elementos                |
          |------------|------------------------------------|----------------------------------------------------|--------------------------------------------------------------------------|---------------------------------------------|
          | Resource   | AuthRequestResource                | Estructura para solicitudes de autenticación       | Exponer los datos de autenticación de forma estructurada para el cliente | Usado por AuthController                    |
          | Resource   | AuthResponseResource               | Estructura para respuestas de autenticación        | Proveer datos estructurados tras un inicio de sesión exitoso             | Usado por AuthController                    |
          | Resource   | RegisterRequestResource            | Estructura para solicitudes de registro            | Representar los datos necesarios para registrar un usuario               | Usado por AuthController                    |
          | Resource   | RegisterResponseResource           | Estructura para respuestas de registro             | Entregar datos estructurados tras un registro exitoso                    | Usado por AuthController                    |
          | Resource   | ErrorResponseResource              | Estructura para manejar respuestas de error        | Estandarizar mensajes de error enviados al cliente                       | Usado por AuthController en caso de errores |
          | Validator  | AuthRequestValidator               | Valida los datos de entrada de las solicitudes     | Garantizar que los datos recibidos cumplen con las reglas del dominio    | Usado por AuthController                    |
          | Controller | AuthController                     | Gestiona las solicitudes HTTP de los clientes      | Recibir solicitudes, coordinar su procesamiento y devolver respuestas    | Usa recursos, validadores y ensambladores   |
          | Assembler  | SignInCommandFromResourceAssembler | Convierte AuthRequestResource en SignInCommand     | Asegurar una transformación limpia entre recursos y comandos             | Usado por AuthController                    |
          | Assembler  | SignUpCommandFromResourceAssembler | Convierte RegisterRequestResource en SignUpCommand | Prevenir inconsistencias al transformar datos de recursos a comandos     | Usado por AuthController                    |

        - **4.2.3.3. Application Layer**
          <br> En la Application Layer del bounded context Users and Access se gestionan los comandos y eventos que coordinan la ejecución de la lógica de autenticación y registro de usuarios dentro del sistema. <br>
          **Sub-capa Internal**

          | Tipo            | Nombre                | Descripción                                                                                                                         | Responsabilidad Principal                                                                     | Relación con otros elementos       |
          |-----------------|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|------------------------------------|
          | CommandHandler  | SignInCommandHandler  | Ejecuta la lógica de autenticación, validando credenciales, utilizando el UserAggregate y generando un token mediante TokenService  | Ejecutar la lógica de autenticación de un usuario                                             | Usa UserRepository y TokenService  |
          | CommandHandler  | SignUpCommandHandler  | Ejecuta la lógica de registro, creando un nuevo UserAggregate, aplicando hash a la contraseña y persistiendo el usuario             | Ejecutar la lógica de registro de un usuario                                                  | Usa UserRepository                 |
          | EventPublisher  | DomainEventPublisher  | Publica eventos de dominio                                                                                                          | Publicar eventos como UserRegistered y UserSignedIn tras la ejecución de los CommandHandlers  | Usado por CommandHandlers          |

        - **4.2.3.4. Infrastructure Layer**
          <br> En la Infrastructure Layer del bounded context Users and Access se implementan los componentes técnicos que soportan la persistencia, seguridad, manejo de tokens JWT, eventos y auditoría, garantizando la integración del dominio con los servicios externos y la base de datos. <br>
          **Sub-capa Repository**

          | Tipo        | Nombre             | Descripción                                    | Responsabilidad Principal                                      | Relación con otros elementos             |
          |-------------|--------------------|------------------------------------------------|----------------------------------------------------------------|------------------------------------------|
          | Interface   | UserRepository     | Interfaz para acceder a los datos del User     | Definir métodos para manipular datos del usuario               | Definida en dominio, implementada aquí   |
          | Class       | UserRepositoryImpl | Implementación del repositorio UserRepository  | Conectar con la base de datos para operaciones de persistencia | Usado por CommandHandlers                |

          **Sub-capa Security**

          | Tipo       | Nombre          | Descripción                                 | Responsabilidad Principal                                    | Relación con otros elementos |
          |------------|-----------------|---------------------------------------------|--------------------------------------------------------------|------------------------------|
          | Config     | SecurityConfig  | Configura reglas de autorización y permisos | Establecer políticas de seguridad para la aplicación         | Aplicada globalmente         |
          | Component  | PasswordEncoder | Servicio de encriptación de contraseñas     | Aplicar hashing seguro a contraseñas antes de persistirlas   | Usado por CommandHandlers    |

          **Sub-capa JWT**

          | Tipo    | Nombre          | Descripción                                                                                                                    | Responsabilidad Principal                                                   | Relación con otros elementos                  |
          |---------|-----------------|--------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------|
          | Class   | JwtAuthFilter   | Filtro que valida tokens JWT en solicitudes HTTP                                                                               | Verificar la autenticidad de las solicitudes antes de llegar al controlador | Relacionado con la seguridad de la aplicación |
          | Class   | JwtServiceImpl  | Implementa la interfaz TokenService definida en la Domain Layer, separando la lógica de negocio de la implementación técnica.  | Encapsular toda la lógica relacionada con tokens JWT                        | Implementa TokenService                       |

          **Sub-capa Event Handling**

          | Tipo           | Nombre                       | Descripción                        | Responsabilidad Principal                                                | Relación con otros elementos                |
          |----------------|------------------------------|------------------------------------|--------------------------------------------------------------------------|---------------------------------------------|
          | EventHandler   | UserRegisteredEventHandler   | Procesa el evento UserRegistered   | Gestionar integraciones o notificaciones tras el registro de un usuario  | Usa sistemas de mensajería o APIs externas  |

          **Sub-capa Audit**

          | Tipo      | Nombre         | Descripción                 | Responsabilidad Principal                             | Relación con otros elementos                                                      |
          |-----------|----------------|-----------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|
          | Service   | AuditService   | Registra eventos críticos   | Mantener un registro de auditoría para trazabilidad   | Usado por CommandHandlers para registrar eventos como inicio de sesión y registro |
      
        - **4.2.3.5. Bounded Context Software Architecture Component Level Diagrams**
          <br> En esta sección se presentan los diagramas a nivel de código del bounded context Users and Access, mostrando la estructura de clases del dominio y el diseño de la base de datos. Estos elementos reflejan cómo se modelan las entidades, relaciones y tablas que sustentan la gestión de usuarios, roles y auditoría del sistema. <br>
          
         <img src="https://imgur.com/dsxpuei.png">
      
        - **4.2.3.6. Bounded Context Software Architecture Code Level Diagrams**
          <br> En esta imagen se muestra el diseño de la base de datos correspondiente al bounded context Users and Access, donde se estructuran las tablas principales para la gestión de usuarios, roles y auditorías. Este diagrama garantiza la correcta relación entre las entidades y la trazabilidad de las operaciones dentro del sistema. <br>

            - **4.2.3.6.1. Bounded Context Domain Layer Class Diagrams**
              <br> En esta imagen, la clase User cumple un rol central al gestionar los atributos predeterminados del usuario, asegurando la integridad de la información básica como identificadores, credenciales y datos personales necesarios para el sistema
              <img src="https://imgur.com/wcoM6j9.png">
              - **4.2.3.6.2. Bounded Context Database Design Diagram**
              <br> En esta imagen se muestra el diseño de la base de datos correspondiente al bounded context Users and Access, donde se estructuran las tablas principales para la gestión de usuarios, roles y auditorías. Este diagrama garantiza la correcta relación entre las entidades y la trazabilidad de las operaciones dentro del sistema. <br>
              <img src="https://imgur.com/0kHDW5g.png">

              **Tabla: users**

              | Nombre          | Descripción                                                        |
              |-----------------|--------------------------------------------------------------------|
              | id              | Identificador único del usuario (UUID), clave primaria.            |
              | email           | Dirección de correo electrónico del usuario, único y obligatorio.  |
              | first\_name     | Primer nombre del usuario.                                         |
              | last\_name      | Apellido del usuario.                                              |
              | password\_hash  | Contraseña del usuario, almacenada de forma segura (encriptada).   |
              | status          | Estado del usuario (ACTIVE, INACTIVE, SUSPENDED).                  |
              | last\_login\_at | Fecha y hora del último inicio de sesión.                          |
              | created\_at     | Fecha y hora en que se creó el registro.                           |
              | updated\_at     | Fecha y hora de la última actualización del registro.              |

              **Tabla: roles**

              | Nombre      | Descripción                                                     |
              |-------------|-----------------------------------------------------------------|
              | id          | Identificador único del rol (UUID), clave primaria.             |
              | name        | Nombre del rol, único y obligatorio (ej. ADMIN, USER, AUDITOR). |
              | description | Descripción opcional del rol.                                   |

              **Tabla: user_roles**

              | Nombre                 | Descripción                                                        |
              |------------------------|--------------------------------------------------------------------|
              | user\_id               | Identificador del usuario, clave foránea hacia `users`.            |
              | role\_id               | Identificador del rol, clave foránea hacia `roles`.                |
              | PK(user\_id, role\_id) | Llave primaria compuesta que asegura que un usuario no repita rol. |

              **Tabla: audit_log**

              | Nombre           | Descripción                                                                |
              |------------------|----------------------------------------------------------------------------|
              | id               | Identificador único del evento (UUID), clave primaria.                     |
              | user\_id         | Identificador del usuario asociado al evento, clave foránea hacia `users`. |
              | event\_type      | Tipo de evento (REGISTERED, SIGNED\_IN, FAILED\_LOGIN).                    |
              | event\_timestamp | Fecha y hora en que ocurrió el evento.                                     |
              | details          | Detalles adicionales del evento (ej. IP, descripción del error, etc.).     |
