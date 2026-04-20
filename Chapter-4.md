## **Capítulo IV: Solution Software Design** 
- **4.1. Strategic-Level Domain-Driven Design** 
    - **4.1.1. Design-Level EventStorming** 
        - **4.1.1.1. Candidate Context Discovery** 
        - **4.1.1.2. Domain Message Flows Modeling** 
        - **4.1.1.3. Bounded Context Canvases** 
    - **4.1.2. Context Mapping** 
    - **4.1.3. Software Architecture** 
        - **4.1.3.1. Software Architecture System Landscape Diagram** 
        - **4.1.3.2. Software Architecture Context Level Diagrams** 
        - **4.1.3.3. Software Architecture Container Level Diagrams** 
        - **4.1.3.4. Software Architecture Deployment Diagrams** 
- **4.2. Tactical-Level Domain-Driven Design** 
    - **4.2.1. Bounded Context: Inventory and Telemetry** 
        - **4.2.1.1. Domain Layer** 
        - **4.2.1.2. Interface Layer** 
        - **4.2.1.3. Application Layer** 
        - **4.2.1.4. Infrastructure Layer** 
        - **4.2.1.5. Bounded Context Software Architecture Component Level Diagrams** 
        - **4.2.1.6. Bounded Context Software Architecture Code Level Diagrams** 
            - **4.2.1.6.1. Bounded Context Domain Layer Class Diagrams** 
            - **4.2.1.6.2. Bounded Context Database Design Diagram**
    - **4.2.2. Bounded Context: Notifications and Alerts** 
        - **4.2.2.1. Domain Layer** 
        - **4.2.2.2. Interface Layer** 
        - **4.2.2.3. Application Layer** 
        - **4.2.2.4. Infrastructure Layer** 
        - **4.2.2.5. Bounded Context Software Architecture Component Level Diagrams** 
        - **4.2.2.6. Bounded Context Software Architecture Code Level Diagrams** 
            - **4.2.2.6.1. Bounded Context Domain Layer Class Diagrams** 
            - **4.2.2.6.2. Bounded Context Database Design Diagram**
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