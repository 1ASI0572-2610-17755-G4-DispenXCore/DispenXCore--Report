## **Capítulo VI: Product Implementation & Validation**
- **6.1. Software Configuration Management**<br>
  En esta sección definimos las reglas que permiten mantener la cohesión del proyecto de principio a fin.

    - **6.1.1. Software Development Environment Configuration**
      Para garantizar la eficiencia en el desarrollo de DispenXCore, nos apoyamos en este conjunto de herramientas:
      #### Requirements Management:
        - **UxPressia**<br>
          Esta plataforma, dedicada a la gestión de componentes de UX, fue el eje para el desarrollo de la etapa de descubrimiento. En ella se diseñaron los entregables clave: User Personas, Journey Maps, Empathy Maps e Impact Maps, fundamentales para el análisis de necesidades.
          <br><br>
        <div align="center">
        <img src="https://uxpressia.com/blog/wp-content/uploads/2022/08/2.png" width="150">
        <br>


      #### Product UX/UI Design:

        - **Figma**<br>
          Para la construcción de la capa de presentación y prototipos dinámicos, empleamos una herramienta de trabajo compartido. Su capacidad de simulación fue fundamental para verificar la efectividad de la navegación y asegurar una experiencia de usuario fluida.
          <br><br>
        <div align="center">
        <img src="https://cdn.sanity.io/images/599r6htc/regionalized/5094051dac77593d0f0978bdcbabaf79e5bb855c-1080x1080.png?w=540&h=540&q=75&fit=max&auto=format" width="150">
        </div>

      #### Software Development

        - **Visual Studio Code**<br>
          La arquitectura del frontend de la landing page se desarrolló utilizando el editor de código de Microsoft, integrando HTML, CSS y JS para consolidar la interfaz del usuario.
          Utilizamos el editor de Microsoft como herramienta principal de programación para materializar la landing page, gestionando todo el desarrollo de HTML, CSS y JavaScript desde este entorno.
          <br><br>
        <div align="center">
        <img src="./feature/chapter-6/vsc.png" width="300">
        </div>
        <br>

        - **Rider**<br>
          Entorno de desarrollo oficial para Rider, basado en C#. Empleado para el desarrollo nativo de la aplicación de C# propuesta en el proyecto.
          <br><br>
        <div align="center">
        <img src="./feature/chapter-6/rider.png" width="150">
        </div>
        <br>

      #### Software Deployment

        - **Git**
          Esta herramienta de gestión de versiones descentralizada garantiza la trazabilidad total de los cambios, optimizando la integración del trabajo realizado por los distintos desarrolladores Se implementó un sistema distribuido para salvaguardar el historial evolutivo del código, permitiendo una sincronización fluida y segura entre todos los colaboradores.
          <br><br>
        <div align="center">
        <img src="https://git-scm.com/images/logos/downloads/Git-Logo-1788C.svg" width="180">
        </div>
        <br>

        - **GitHub**
          Este servicio de alojamiento potencia la sinergia del equipo mediante flujos de integración continua y una gestión estructurada de ramas. Asimismo, se vincula con un sistema de despliegue automático para mantener la landing page siempre actualizada. Se utiliza esta infraestructura para centralizar el código, facilitando el desarrollo paralelo y la validación mediante CI. Adicionalmente, se aprovechan sus capacidades de hosting estático para automatizar la publicación del sitio web.
          <br><br>
        <div align="center">
        <img src="https://logos-world.net/wp-content/uploads/2020/11/GitHub-Logo.png" width="180">
        </div>
    - **6.1.2. Source Code Management**
      La gestión del proyecto de la aplicación móvil, landing page y aplicación Backend, siguen los principios del modelo "Git Branch Model" en la cual se define como una estrategia para administrar y organizar un trabajo en un repositorio de Github mediante la creación de ramas con distintas funcionalidades. Uno de los modelos que usaremos es el "Git Flow", la cual define como crear ramas para mantener el control del ciclo de vida del desarrollo del software.
   ---   
  **Repositorio de Landing Page:** [https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Landing](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Landing)

  **Repositorio del Frontend:** [https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-FrontEnd](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-FrontEnd)

  **Repositorio del Backend:** [https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-Backend](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-Backend)

   ---

  **Estructura de ramas**

    1. Rama main (rama principal): Esta rama resguarda las versiones finales del código. Todo cambio debe validarse y probarse primero en otras ramas antes de integrarse.<br><br>

    1. Rama develop (rama de desarrollo): En esta rama se concentra el trabajo colaborativo, incorporando gradualmente cada funcionalidad hasta que se estabilice y pueda fusionarse con main.<br><br>

    1. Rama feature (rama de características): Estas ramas, derivadas de `develop`, se usan únicamente para crear nuevas funcionalidades. Cuando se implementan y validan, vuelven a integrarse en la rama de desarrollo. Aunque suelen ser temporales, en el caso de la Landing Page se conservarán con fines documentales.<br><br>

    4. Convenciones de commits: Para los mensajes de commit, seguimos la especificación Conventional Commits con la siguiente estructura:

              "(tipo):(titulo)" y "(descripcion)"

    - **6.1.3. Source Code Style Guide & Conventions**

        Para construir DispenXCore, utilizamos los siguientes lenguajes y tecnologías:

        **Angular**<br>
        Como framework full-stack se trabajó con Next.js, aplicando estas prácticas:

        - **Estructura del proyecto:**
            Se mantuvo una organización estándar con los directorios app/ para enrutamiento, components/ para elementos reutilizables y lib/ para utilidades y configuración.

        - **Renderizado híbrido:**
            Se combinó Server-Side Rendering (SSR) para contenido dinámico con Static Site Generation (SSG) para páginas estáticas, mejorando SEO y rendimiento.

        **CSS**<br>
        Se siguió la metodología BEM junto con guías de estilo definidas:

        - **Nomenclatura descriptiva:**
            Las clases se escriben en formato "kebab-case" en inglés para identificar claramente su función.

        - **Mejoras en la experiencia de usuario:**
            Se incorporaron transiciones suaves en las interacciones y efectos en botones.

        - **Recursos tipográficos:**
            Se optimizó la carga de tipografías personalizadas mediante `@font-face`, respetando buenas prácticas de rendimiento.

        **.NET**<br>
        En el desarrollo de la API RESTful se aplicaron las convenciones recomendadas por Microsoft:

        - **Convenciones de nomenclatura:**
            Se emplea PascalCase en clases y métodos, y lowerCamelCase en parámetros y variables.

        - **Arquitectura limpia:**
            Se implementó Clean Architecture junto con principios de Domain-Driven Design, estructurando el proyecto en capas separadas (Aplicación, Infraestructura, Dominio y Presentación).

    - **6.1.4. Software Deployment Configuration**

      **Landing Page:**<br>
      Para el despliegue de la Landing Page, utilizaremos **Github Pages**, usando el servico integrado de enlace con GitHub.

        1. Ingresamos a netlify, y seleccionamos import git
<p align="center">
  <img src="assets/paso1.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        2. Elegimos importar de github un proyecto
<p align="center">
  <img src="assets/paso2.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        3. Configuramos o enlazamos netlify con github
<p align="center">
  <img src="assets/paso3.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        4. Seleccionamos nuestro repositorio
<p align="center">
  <img src="assets/paso4.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        5  . Seleccionamos el repositorio del landing page
<p align="center">
  <img src="assets/paso5.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        6. Definimos el nombre de nuestro link
<p align="center">
  <img src="assets/paso6.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        7. Definimos variables y le damos a deploy
<p align="center">
  <img src="assets/paso7.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        8. Ingresamos a nuestro link
<p align="center">
  <img src="assets/paso8.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>
        9. Ingresamos a nuestra pag
<p align="center">
  <img src="assets/paso9.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

      **Enlace del Landing Page:** []()
- **6.2. Landing Page & Mobile Application Implementation**
  <br>En esta sección se describe la implementación técnica de la Landing Page y de las aplicaciones móviles, incluyendo las herramientas, tecnologías y la metodología ágil aplicada mediante sprints en cada entrega del producto.<br><br>
    - **6.2.1. Sprint 1**<br>
      Este apartado presenta los resultados del Sprint #1, correspondiente a la primera entrega del proyecto. Se incluyen los avances organizativos, la asignación del trabajo y los entregables desarrollados: una landing page funcional, el avance del Web Service y una versión inicial de la Mobile Application.
        - **6.2.1.1. Sprint Planning 1**<br>
          <br>Seguidamente, se expone la planificación del Sprint 1, en la que se establecieron los objetivos iniciales, se priorizaron las tareas del backlog y se definieron las responsabilidades del equipo para este primer ciclo de desarrollo.<br><br>
      
          <table>
            <tr>
              <th> Sprint # </th>
              <th> Sprint 1 </th>
            </tr>
            <tr>
                        <td style="font-weight: bold;" colspan="2"> Contexto de Planificación del Sprint </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Fecha </td>
              <td> 08/05/2026 </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Hora </td>
              <td> 22:38 horas (GMT-5) </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Lugar </td>
                        <td> Reunión virtual (Discord) </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Elaborado por </td>
              <td> Bastidas Bastidas, Diego Martin </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Participantes (reunión de planificación) </td>
              <td>
                Bastidas Bastidas, Diego Martin<br>
                Cardenas Minaya, Ricardo Fernando<br>
                Dominguez Vargas, Rafael Alexander<br>
                Escobar Palomino, Sebastian Matias<br>
                Muñiz Huayanca, Percy Alonso	
              </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Resumen de la Sprint Review 1 </td>
                        <td> Al tratarse del primer sprint de desarrollo, no existe un resumen de revisión anterior. </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Resumen de la Retrospectiva del Sprint 1 </td>
                        <td> Como este es el sprint inicial, todavía no se han detectado oportunidades de mejora concretas en el proceso. </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;" colspan="2"> Objetivo del Sprint e Historias de Usuario </td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Objetivo del Sprint 1 </td>
                        <td>Buscamos desarrollar una landing page que comunique de forma visual y comprensible las funcionalidades y beneficios de DispenXCore, generando en los visitantes una percepción inicial sólida sobre la plataforma y su propuesta de valor. Esta página facilitará la exploración de sus secciones para que los usuarios entiendan cómo nuestra solución vincula eficazmente a empresas con profesionales. Además, se pondrá en valor la app web por su uso práctico y accesible, permitiendo la interacción con la plataforma desde cualquier ubicación. Validaremos este enfoque analizando la navegación de los visitantes en la landing page y su uso de la integración con la app web.</td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Velocidad del Sprint 1 </td>
              <td>20</td>
            </tr>
            <tr>
                        <td style="font-weight: bold;"> Total de Story Points </td>
              <td>  20</td>
            </tr>
          </table>
        - **6.2.1.2. Sprint Backlog 1**
          <br> En el primer sprint, el equipo enfocó su trabajo en crear una landing page que fuera tanto funcional como atractiva, asignando las tareas en el tablero de Sprint según las habilidades de cada miembro.

          | **ID** | **Title**                      | **Description**                                                                                                                                            | **Estimation (Hours)** | **Assigned To**                 | **Status (To-do / In Process / To Review / Done)** |
          | ------ | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------------- | -------------------------------------------------- |
          | LPS01  | Navigation                     | Implementación de la barra de navegación con enlaces a las secciones “¿Cómo funciona?”, “Casos de éxito”, “Planes” y “Contactos”.                          | 4                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS02  | Hero Section                   | Implementación de la sección “Hero Section”, diseñada para captar la atención de los usuarios y presentar brevemente la aplicación móvil.                  | 2                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS03  | About the Product              | Desarrollo de la sección “About the Product”, donde se describen brevemente el producto y sus principales beneficios.                                      | 2                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS04  | Services and Technical Workers | Desarrollo de la sección “Services and Technical Workers”, donde se muestran los servicios ofrecidos por los técnicos calificados.                         | 3                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS05  | Testimonials                   | Desarrollo de la sección “Testimonials”, donde se presentan los comentarios y experiencias de usuarios que han utilizado la aplicación.                    | 3                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS06  | Contact                        | Desarrollo de la sección “Contact”, donde se detalla la forma en que los usuarios pueden comunicarse con el equipo detrás de *AlguienDijoChamba*.          | 2                      | Bastidas Bastidas, Diego Martín | Done                                               |
          | LPS07  | Footer                         | Desarrollo de la sección “Footer”, que incluye enlaces de navegación, redes sociales del equipo y accesos rápidos a las distintas secciones del sitio web. | 2                      | Bastidas Bastidas, Diego Martín | Done                                               |




        - **6.2.1.3. Development Evidence for Sprint Review**
          <br>Esta sección se presenta la Evidencia de Desarrollo completada durante el sprint, demostrando el trabajo funcional realizado y los incrementos del producto listos para ser inspeccionados y validados en la Sprint Review.

          | *Repository*                                                             | *Branch*      | *Commit Id*                               | *Commit Message*                                                                                                                         | *Committed By*    | *Committed On* |
          |--------------------------------------------------------------------------|---------------|-------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------------|
          | Repositorio | chapter-1     | commit  | nombre del commit                                                                                                                           | usuario  | fecha   |
          | Repositorio | chapter-1     | commit  | nombre del commit                                                                                                                           | usuario  | fecha   |
          |             

        - **6.2.1.4. Testing Suite Evidence for Sprint Review**

          <br> En este primer Sprint, veremos los archivos .feature relacionados a los user tasks que hemos desarrollado, subidos en el repositorio.

          <table><thead>
          <tr>
            <th>&nbsp;&nbsp;&nbsp;<br>Repository&nbsp;&nbsp;&nbsp;</th>
            <th>&nbsp;&nbsp;&nbsp;<br>Branch&nbsp;&nbsp;&nbsp;</th>
            <th>&nbsp;&nbsp;&nbsp;<br>Commit ID&nbsp;&nbsp;&nbsp;</th>
            <th>&nbsp;&nbsp;&nbsp;<br>Commit<br>&nbsp;&nbsp;&nbsp;<br>Message&nbsp;&nbsp;&nbsp;</th>
            <th>&nbsp;&nbsp;&nbsp;<br>Commit<br>&nbsp;&nbsp;&nbsp;<br>Message Body&nbsp;&nbsp;&nbsp;</th>
            <th>&nbsp;&nbsp;&nbsp;<br>Committed on&nbsp;&nbsp;&nbsp;(Date)&nbsp;&nbsp;&nbsp;</th>
          </tr></thead>
          <tbody>
          <tr>
          <td rowspan="10"><a href="hhttps://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore--Reports" target="_blank" rel="noopener noreferrer">https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore--Report</a></td>
            <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
            <td>&nbsp;&nbsp;&nbsp;<br>numero de commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>nombre del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>mensaje del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>fecha del commit</td>
          </tr>

          <tr>
            <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
            <td>&nbsp;&nbsp;&nbsp;<br>numero de commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>nombre del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>mensaje del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>fecha del commit</td>
          </tr>

          <tr>
            <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
            <td>&nbsp;&nbsp;&nbsp;<br>numero de commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>nombre del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>mensaje del commit</td>
            <td>&nbsp;&nbsp;&nbsp;<br>fecha del commit</td>
          </tr>

          </tbody></table>

    - **6.2.1.5. Execution Evidence for Sprint Review**
      <br>Esta sección expone la Evidencia de Ejecución del sprint, donde se aprecia el producto operativo o el incremento de valor implementado, preparado para su revisión y validación en la Sprint Review.<br><br>

      ### LANDING PAGE:

      A continuación, se presentan las evidencias de la implementación de la landing page desarrollada en HTML, CSS y JS con la biblioteca Bootstrap.

      #### LPS 01:

      Ver Hero Section

      <div align="center">
      <img src="">
      </div>

      #### LPS 02:

      Ver sección sobre el producto

      <div align="center">
      <img src="" alt="About us">
      </div>

      #### LPS 03:

      Ver sección de servicios y características

      <div align="center">
      <img src="" alt="Services">
      </div>


      #### LPS 04:

      Ver testimonios de usuarios

      <div align="center">
      <img src="">
      </div>

      #### LPS 05:

      Acceder a sección de contacto

      <div align="center">
      <img src="" alt="Contacts">
      </div>

      #### LPS 07:

      Ver sección Footer con enlaces útiles

      <div align="center">
      <img src="" alt="Footer">
      </div>

      ### WEB APPLICATION:
      <div align="center">
      <img src="">
       </div>

      <div align="center">
       <img src="">
      </div>

      <div align="center">
      <img src="">
       </div>

      <div align="center">
      <img src="">
      </div>

      <div align="center">
       <img src="">
      </div>

      <div align="center">
       <img src="">
       </div>

      <div align="center">
      <img src="">
      </div>

       <div align="center">
      <img src="">
       </div>
 
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>
    
       <div align="center">
       <img src="">
       </div>


        - **6.2.1.6. Services Documentation Evidence for Sprint Review**
          <br> En este Sprint se logró documentar con OpenAPI los endpoints correspondientes a las funcionalidades implementadas. La documentación incluye detalles técnicos de los servicios consumidos por la aplicación móvil, como los verbos HTTP, parámetros de entrada y respuestas esperadas, permitiendo una mejor comprensión e integración de la app con la API.

  | *Endpoint*                          | *Accion*                            | *Verbo HTTP* | *Sintaxis de llamada*              | *Parámetros o Peticiones*                                                                                                                             | *Ejemplo de Response*                                                                                                                                                                             | *URL de Documentacion*                                   |
  |-------------------------------------|-------------------------------------|--------------|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------| 
  | /api/auth/login                     | Autenticación                       | POST         | api/auth/login                     | {"email": "string", "password": "string"}                                                                                                             | {"accessToken": "string", "refreshToken": "string"}                                                                                                                                               | http://localhost:8080/api/auth/login                     |
  | /api/auth/register                  | Registro de usuario                 | POST         | api/auth/register                  | {"email": "string", "firstName": "string", "lastName": "string", "password": "string"}                                                                | {"userId": "string", "message": "Usuario registrado exitosamente"}                                                                                                                                | http://localhost:8080/api/auth/register                  |
  | /api/v1/workers                     | Registrar Worker                    | POST         | api/v1/workers                     | {"name": "string", "email": "string", "phone": "string", "location": "string", "experience": "string", "categoryId": "integer", "skills": ["string"]} | {"workerId": "string", "message": "Worker registrado"}                                                                                                                                            | http://localhost:8080/api/v1/workers                     |
  | /api/v1/workers/{id}                | Actualizar perfil de Worker         | PUT          | api/v1/workers/{id}                | {"name": "string", "email": "string", "phone": "string", "location": "string", "experience": "string"}                                                | {"workerId": "string", "message": "Perfil actualizado"}                                                                                                                                           | http://localhost:8080/api/v1/workers/{id}                |
  | /api/v1/workers/{id}                | Obtener perfil de Worker por ID     | GET          | api/v1/workers/{id}                | none                                                                                                                                                  | {"name": "string", "email": "string", "phone": "string", "location": "string", "experience": "string", "ratingAvg": "decimal", "status": "string", "skills": ["string"], "categoryId": "integer"} | http://localhost:8080/api/v1/workers/{id}                |
  | /api/v1/workers                     | Obtener Workers por categoría       | GET          | api/v1/workers                     | none (query params: ?category=string)                                                                                                                 | [{"workerId": "string", "name": "string", "ratingAvg": "decimal", "skills": ["string"]}]                                                                                                          | http://localhost:8080/api/v1/workers                     |
  | /api/v1/workers/{id}/skills         | Añadir skill a Worker               | POST         | api/v1/workers/{id}/skills         | {"skillName": "string"}                                                                                                                               | {"message": "Skill añadido"}                                                                                                                                                                      | http://localhost:8080/api/v1/workers/{id}/skills         |
  | /api/v1/workers/{id}/ratings        | Calificar Worker                    | POST         | api/v1/workers/{id}/ratings        | {"score": "integer", "comment": "string"}                                                                                                             | {"message": "Calificación registrada"}                                                                                                                                                            | http://localhost:8080/api/v1/workers/{id}/ratings        |
  | /api/v1/categories                  | Crear categoría                     | POST         | api/v1/categories                  | {"name": "string", "description": "string"}                                                                                                           | {"categoryId": "integer", "message": "Categoría creada"}                                                                                                                                          | http://localhost:8080/api/v1/categories                  |
  | /api/v1/categories                  | Listar categorías                   | GET          | api/v1/categories                  | none                                                                                                                                                  | [{"categoryId": "integer", "name": "string", "description": "string"}]                                                                                                                            | http://localhost:8080/api/v1/categories                  |
  | /api/v1/categories/{id}             | Obtener categoría por ID            | GET          | api/v1/categories/{id}             | none                                                                                                                                                  | {"categoryId": "integer", "name": "string", "description": "string"}                                                                                                                              | http://localhost:8080/api/v1/categories/{id}             |
  | /api/v1/payments                    | Crear pago                          | POST         | api/v1/payments                    | {"orderId": "string", "amount": "decimal", "method": "string"}                                                                                        | {"paymentId": "string", "status": "string"}                                                                                                                                                       | http://localhost:8080/api/v1/payments                    |
  | /api/v1/payments/{id}               | Obtener pago por ID                 | GET          | api/v1/payments/{id}               | none                                                                                                                                                  | {"paymentId": "string", "amount": "decimal", "status": "string", "date": "datetime"}                                                                                                              | http://localhost:8080/api/v1/payments/{id}               |
  | /api/v1/refunds                     | Solicitar reembolso                 | POST         | api/v1/refunds                     | {"paymentId": "string", "reason": "string"}                                                                                                           | {"refundId": "string", "status": "string"}                                                                                                                                                        | http://localhost:8080/api/v1/refunds                     |
  | /api/v1/alerts                      | Crear alerta                        | POST         | api/v1/alerts                      | {"type": "string", "title": "string", "message": "string", "customerId": "integer", "workerId": "integer"}                                            | {"alertId": "integer", "message": "Alerta creada"}                                                                                                                                                | http://localhost:8080/api/v1/alerts                      |
  | /api/v1/alerts/{id}                 | Eliminar alerta                     | DELETE       | api/v1/alerts/{id}                 | none                                                                                                                                                  | {"message": "Alerta eliminada"}                                                                                                                                                                   | http://localhost:8080/api/v1/alerts/{id}                 |
  | /api/v1/alerts/{id}/accept          | Aceptar alerta                      | PUT          | api/v1/alerts/{id}/accept          | none                                                                                                                                                  | {"message": "Alerta aceptada"}                                                                                                                                                                    | http://localhost:8080/api/v1/alerts/{id}/accept          |
  | /api/v1/alerts/{id}/decline         | Rechazar alerta                     | PUT          | api/v1/alerts/{id}/decline         | none                                                                                                                                                  | {"message": "Alerta rechazada"}                                                                                                                                                                   | http://localhost:8080/api/v1/alerts/{id}/decline         |
  | /api/v1/alerts                      | Obtener alertas por Customer        | GET          | api/v1/alerts                      | none (query params: ?customerId=integer)                                                                                                              | [{"alertId": "integer", "type": "string", "title": "string", "message": "string"}]                                                                                                                | http://localhost:8080/api/v1/alerts                      |
  | /api/v1/alerts                      | Obtener alertas por Worker          | GET          | api/v1/alerts                      | none (query params: ?workerId=integer)                                                                                                                | [{"alertId": "integer", "type": "string", "title": "string", "message": "string"}]                                                                                                                | http://localhost:8080/api/v1/alerts                      |
  | /api/v1/work-requests               | Crear solicitud de trabajo          | POST         | api/v1/work-requests               | {"title": "string", "description": "string", "date": "datetime", "time": "string", "address": "string", "category": "string"}                         | {"requestId": "string", "message": "Solicitud creada"}                                                                                                                                            | http://localhost:8080/api/v1/work-requests               |
  | /api/v1/work-requests/{id}          | Actualizar solicitud de trabajo     | PUT          | api/v1/work-requests/{id}          | {"title": "string", "description": "string", "date": "datetime", "time": "string", "address": "string"}                                               | {"requestId": "string", "message": "Solicitud actualizada"}                                                                                                                                       | http://localhost:8080/api/v1/work-requests/{id}          |
  | /api/v1/work-requests/{id}/accept   | Aceptar solicitud de trabajo        | PUT          | api/v1/work-requests/{id}/accept   | none                                                                                                                                                  | {"message": "Solicitud aceptada"}                                                                                                                                                                 | http://localhost:8080/api/v1/work-requests/{id}/accept   |
  | /api/v1/work-requests/{id}/complete | Completar solicitud de trabajo      | PUT          | api/v1/work-requests/{id}/complete | {"finalAmount": "decimal", "finalWorkDescription": "string"}                                                                                          | {"message": "Solicitud completada"}                                                                                                                                                               | http://localhost:8080/api/v1/work-requests/{id}/complete |
  | /api/v1/work-requests               | Obtener solicitudes por Worker      | GET          | api/v1/work-requests               | none (query params: ?workerId=integer)                                                                                                                | [{"requestId": "string", "title": "string", "status": "string"}]                                                                                                                                  | http://localhost:8080/api/v1/work-requests               |
  | /api/v1/work-requests               | Obtener solicitudes por Customer    | GET          | api/v1/work-requests               | none (query params: ?customerId=integer)                                                                                                              | [{"requestId": "string", "title": "string", "status": "string"}]                                                                                                                                  | http://localhost:8080/api/v1/work-requests               |
  | /api/v1/work-requests/{id}          | Obtener solicitud de trabajo por ID | GET          | api/v1/work-requests/{id}          | none                                                                                                                                                  | {"title": "string", "description": "string", "date": "datetime", "status": "string", "workerId": "integer"}                                                                                       | http://localhost:8080/api/v1/work-requests/{id}          |

    - **6.2.1.7. Software Deployment Evidence for Sprint Review**
      <br>En esta sección se presenta la Evidencia de Despliegue del Software, verificando que el incremento desarrollado durante el sprint ha sido implementado y se encuentra accesible en el entorno de destino para su revisión final.<br><br>

      ### LANDING PAGE:

      A continuación, se muestran las evidencias del despliegue del landing page hecha en HTML, CSS y JS usando la biblioteca Bootstrap usando funcionalidades de GitHubPage.

      #### Hero Section:

      Vista representativa que busca llamar la atencion al usuario

        <div align="center">
        <img src="" alt="Hero Section">
        </div>

      #### SERVICES:

      Seccion donde se veran los servicios que ofrecen nuestros tecnicos cualificados

        <div align="center">
        <img src="">
        </div>

      #### TESTIMONIALS:

      Seccion donde se veran testimonios de usuarios reales

        <div align="center">
        <img src="">
        </div>

      #### CONTACT:

      Seccion en la cual el usuario puede contactar con el equipo de AlguienDijoChamba

        <div align="center">
        <img src="">
        </div>

      #### FOOTER:

      Seccion donde se veran enlaces rapidos y redes sociales

        <div align="center">
        <img src="">
        </div>

      ### WEB APPLICATION:
      A continuación, se muestran las evidencias de la ejecución de la aplicación móvil desarrollada en Android Studio.

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

        <div align="center">
        <img src="">
        </div>

    - **6.2.1.8. Team Collaboration Insights during Sprint**
          <br>En esta sección se exponen las Reflexiones sobre la Colaboración del Equipo durante el sprint, detallando las dinámicas de trabajo y las lecciones clave identificadas para la mejora continua del proceso.<br><br>

      | *Alumno*                            | *Actividad*                                |
      |-------------------------------------|--------------------------------------------|
      | Bastidas Bastidas, Diego Martin     | Figma Design, Backend           |
      | Cardenas Minaya, Ricardo Fernando         | Figma Design, Prototyping, Frontend        |
      | Dominguez Vargas, Rafael Alexander  | Figma Design, Frontend  |
      | Escobar Palomino, Sebastian Matias  | Figma Design, Frontend                                   |
      | Muñiz Huayanca, Percy Alonso        | Landing Page Deployment, Figma Design Backend                                    |

      ## Report:

      <div align="center">
          <img src="">
          </div>

      <div align="center">
          <img src="">
          </div>

      <div align="center">
          <img src="">
          </div>

      ## Landing Page:

      <div align="center">
          <img src=""
          </div>

      <div align="center">
          <img src="">
          </div>

      <div align="center">
          <img src="">
          </div>

      ## Web Application:

     <div align="center">
          <img src="">
          </div>

     <div align="center">
          <img src="">
          </div>

     <div align="center">
          <img src="">
          </div>




## Bibliografia
    
- Gartner, Inc. (2025). *Forecast: Internet of Things — Endpoints and spending*. Gartner.  
  https://www.gartner.com/en/information-technology/insights/internet-of-things  

- Statista. (2024). *Smart home - Worldwide*.  
  https://www.statista.com/outlook/dmo/smart-home/worldwide  

- International Data Corporation (IDC). (2024). *Worldwide Internet of Things forecast*. IDC.  
  https://www.idc.com/getdoc.jsp?containerId=prUS  

- McKinsey & Company. (2023). *The state of smart homes*.  
  https://www.mckinsey.com/industries/technology-media-and-telecommunications/our-insights  

- Deloitte. (2024). *Connected consumer survey*. Deloitte Insights.  
  https://www2.deloitte.com/global/en/insights/industry/technology/connected-consumer-survey.html  

- Food and Agriculture Organization of the United Nations (FAO). (2023). *Food loss and waste database*.  
  https://www.fao.org/platform-food-loss-waste  

- World Bank. (2023). *Urban consumption patterns*.  
  https://www.worldbank.org/en/topic/urbandevelopment  

- Google. (2023). *Material design guidelines*.  
  https://material.io/design  

- Nielsen Norman Group. (2022). *Mobile UX and notification behavior*.  
  https://www.nngroup.com/articles/mobile-notifications  

- Institute of Electrical and Electronics Engineers (IEEE). (2023). *IoT systems and sensor integration*.  
  https://ieeexplore.ieee.org  

- Microsoft. (2024). *IoT architecture guide*.  
  https://learn.microsoft.com/en-us/azure/architecture/iot  
