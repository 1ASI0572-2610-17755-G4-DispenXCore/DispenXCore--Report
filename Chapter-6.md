## Capítulo VI: Product Implementation & Validation

---

### 6.1. Software Configuration Management

En esta sección definimos las reglas que permiten mantener la cohesión del proyecto de principio a fin, abarcando la configuración del entorno de desarrollo, la gestión del código fuente, las convenciones de estilo y el proceso de despliegue.

<br>

#### 6.1.1. Software Development Environment Configuration

Para garantizar la eficiencia en el desarrollo de DispenXCore, nos apoyamos en el siguiente conjunto de herramientas, organizadas según su propósito dentro del ciclo de vida del proyecto.

<br>

##### Requirements Management

- **UxPressia**

  Esta plataforma, dedicada a la gestión de componentes de UX, fue el eje para el desarrollo de la etapa de descubrimiento. En ella se diseñaron los entregables clave: User Personas, Journey Maps, Empathy Maps e Impact Maps, fundamentales para el análisis de necesidades.

  <p align="center">
    <img src="https://uxpressia.com/blog/wp-content/uploads/2022/08/2.png" width="150" alt="UxPressia logo"/>
  </p>

<br>

##### Product UX/UI Design

- **Figma**

  Para la construcción de la capa de presentación y prototipos dinámicos, empleamos una herramienta de trabajo compartido. Su capacidad de simulación fue fundamental para verificar la efectividad de la navegación y asegurar una experiencia de usuario fluida.

  <p align="center">
    <img src="https://cdn.sanity.io/images/599r6htc/regionalized/5094051dac77593d0f0978bdcbabaf79e5bb855c-1080x1080.png?w=540&h=540&q=75&fit=max&auto=format" width="150" alt="Figma logo"/>
  </p>

<br>

##### Software Development

- **Visual Studio Code**

  La arquitectura del frontend de la landing page se desarrolló utilizando el editor de código de Microsoft, integrando HTML, CSS y JavaScript para consolidar la interfaz del usuario. Utilizamos el editor de Microsoft como herramienta principal de programación para materializar la landing page, gestionando todo el desarrollo desde este entorno.

  <p align="center">
    <img src="./feature/chapter-6/vsc.png" width="300" alt="Visual Studio Code logo"/>
  </p>

- **Rider**

  Entorno de desarrollo oficial de JetBrains basado en C#. Empleado para el desarrollo nativo de la aplicación backend en .NET propuesta en el proyecto.

  <p align="center">
    <img src="./feature/chapter-6/rider.png" width="150" alt="JetBrains Rider logo"/>
  </p>

<br>

##### Software Deployment

- **Git**

  Esta herramienta de gestión de versiones descentralizada garantiza la trazabilidad total de los cambios, optimizando la integración del trabajo realizado por los distintos desarrolladores. Se implementó un sistema distribuido para salvaguardar el historial evolutivo del código, permitiendo una sincronización fluida y segura entre todos los colaboradores.

  <p align="center">
    <img src="https://git-scm.com/images/logos/downloads/Git-Logo-1788C.svg" width="180" alt="Git logo"/>
  </p>

- **GitHub**

  Este servicio de alojamiento potencia la sinergia del equipo mediante flujos de integración continua y una gestión estructurada de ramas. Asimismo, se vincula con un sistema de despliegue automático para mantener la landing page siempre actualizada. Se utiliza esta infraestructura para centralizar el código, facilitando el desarrollo paralelo y la validación mediante CI. Adicionalmente, se aprovechan sus capacidades de hosting estático para automatizar la publicación del sitio web.

  <p align="center">
    <img src="https://logos-world.net/wp-content/uploads/2020/11/GitHub-Logo.png" width="180" alt="GitHub logo"/>
  </p>

- **Netlify**

  Plataforma de despliegue continuo utilizada para publicar la landing page de DispenXCore. Permite la integración automática con el repositorio de GitHub, generando un enlace público accesible desde cualquier dispositivo y manteniendo el sitio actualizado tras cada cambio en la rama principal.

<br>

---

<br>

#### 6.1.2. Source Code Management

La gestión del proyecto de la aplicación móvil, landing page y aplicación backend siguen los principios del modelo **Git Branch Model**, una estrategia para administrar y organizar el trabajo en un repositorio de GitHub mediante la creación de ramas con distintas funcionalidades. Adicionalmente, aplicamos **Git Flow**, que define cómo crear ramas para mantener el control del ciclo de vida del desarrollo del software.

<br>

##### Repositorios del proyecto

- **Repositorio del Reporte:** [DispenXCore--Report](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore--Report)
- **Repositorio del Landing Page:** [DispenXCore-Landing](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Landing)
- **Repositorio del Frontend:** [DispenXCore-Web-FrontEnd](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-FrontEnd)
- **Repositorio del Backend:** [DispenXCore-Web-Backend](https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore-Web-Backend)

<br>

##### Estructura de ramas

**1. Rama `main` (rama principal).** Esta rama resguarda las versiones finales del código. Todo cambio debe validarse y probarse primero en otras ramas antes de integrarse.

**2. Rama `develop` (rama de desarrollo).** En esta rama se concentra el trabajo colaborativo, incorporando gradualmente cada funcionalidad hasta que se estabilice y pueda fusionarse con `main`.

**3. Rama `feature/*` (ramas de características).** Estas ramas, derivadas de `develop`, se usan únicamente para crear nuevas funcionalidades. Cuando se implementan y validan, vuelven a integrarse en la rama de desarrollo. Aunque suelen ser temporales, en el caso de la Landing Page se conservarán con fines documentales.

**4. Convenciones de commits.** Para los mensajes de commit, seguimos la especificación **Conventional Commits** con la siguiente estructura:

```
(tipo): (título)

(descripción)
```

<br>

---

<br>

#### 6.1.3. Source Code Style Guide & Conventions

Para construir DispenXCore, utilizamos los siguientes lenguajes y tecnologías, cada uno con sus respectivas guías de estilo y convenciones.

<br>

##### Angular

Como framework para el desarrollo del frontend web, se aplicaron estas prácticas:

- **Estructura del proyecto:** se mantuvo una organización modular con directorios `app/` para componentes principales, `shared/` para elementos reutilizables y `core/` para servicios y configuración global.
- **Componentes reutilizables:** se aplicó el principio de separación de responsabilidades, dividiendo la lógica entre componentes presentacionales y contenedores.
- **Lazy loading:** se implementó carga diferida de módulos para optimizar el rendimiento inicial de la aplicación.

<br>

##### CSS

Se siguió la metodología **BEM** junto con guías de estilo definidas:

- **Nomenclatura descriptiva:** las clases se escriben en formato `kebab-case` en inglés para identificar claramente su función.
- **Mejoras en la experiencia de usuario:** se incorporaron transiciones suaves en las interacciones y efectos en botones.
- **Recursos tipográficos:** se optimizó la carga de tipografías personalizadas mediante `@font-face`, respetando buenas prácticas de rendimiento.

<br>

##### .NET

En el desarrollo de la API RESTful se aplicaron las convenciones recomendadas por Microsoft:

- **Convenciones de nomenclatura:** se emplea `PascalCase` en clases y métodos, y `lowerCamelCase` en parámetros y variables.
- **Arquitectura limpia:** se implementó Clean Architecture junto con principios de Domain-Driven Design, estructurando el proyecto en capas separadas (Aplicación, Infraestructura, Dominio y Presentación).

<br>

---

<br>

#### 6.1.4. Software Deployment Configuration

Para el despliegue de la Landing Page utilizamos **Netlify**, aprovechando su servicio de integración continua con GitHub para mantener el sitio actualizado automáticamente con cada push a la rama principal.

A continuación se detalla el proceso paso a paso para desplegar la landing page de DispenXCore en Netlify, integrándola con el repositorio de GitHub del proyecto.

<br>

**Paso 1.** Ingresamos a Netlify y seleccionamos la opción **Import from Git**.

<p align="center">
  <img src="feature/chapter-6/steps/paso1.png" alt="Paso 1: Import from Git en Netlify" width="600"/>
</p>

<br>

**Paso 2.** Elegimos importar un proyecto desde **GitHub**.

<p align="center">
  <img src="feature/chapter-6/steps/paso2.png" alt="Paso 2: Selección de GitHub como origen" width="600"/>
</p>

<br>

**Paso 3.** Configuramos o enlazamos Netlify con nuestra cuenta de GitHub.

<p align="center">
  <img src="feature/chapter-6/steps/paso3.png" alt="Paso 3: Autorización de Netlify con GitHub" width="600"/>
</p>

<br>

**Paso 4.** Seleccionamos la organización donde se encuentra nuestro repositorio.

<p align="center">
  <img src="feature/chapter-6/steps/paso4.png" alt="Paso 4: Selección de la organización" width="600"/>
</p>

<br>

**Paso 5.** Seleccionamos el repositorio correspondiente al landing page de DispenXCore.

<p align="center">
  <img src="feature/chapter-6/steps/paso5.png" alt="Paso 5: Selección del repositorio del landing page" width="600"/>
</p>

<br>

**Paso 6.** Definimos el nombre del subdominio que tendrá nuestro sitio publicado.

<p align="center">
  <img src="feature/chapter-6/steps/paso6.png" alt="Paso 6: Definición del nombre del sitio" width="600"/>
</p>

<br>

**Paso 7.** Configuramos las variables de entorno necesarias y presionamos **Deploy**.

<p align="center">
  <img src="feature/chapter-6/steps/paso7.png" alt="Paso 7: Configuración de variables y despliegue" width="600"/>
</p>

<br>

**Paso 8.** Una vez finalizado el despliegue, ingresamos al enlace generado por Netlify.

<p align="center">
  <img src="feature/chapter-6/steps/paso8.png" alt="Paso 8: Acceso al enlace generado" width="600"/>
</p>

<br>

**Paso 9.** Verificamos el funcionamiento correcto de la landing page publicada.

<p align="center">
  <img src="feature/chapter-6/steps/paso9.png" alt="Paso 9: Verificación de la landing page" width="600"/>
</p>

<br>

##### Enlace del Landing Page

🔗 **[https://comforting-pony-e834fe.netlify.app/](https://comforting-pony-e834fe.netlify.app/)**

<br>

**Paso 1.** Iniciar la creación del proyecto.

<p align="center">
  <img src="https://i.imgur.com/qOO3Jdk.png" alt="Paso 1: Import from Git en Netlify" width="600"/>
</p>

<br>

**Paso 2.** Autorizar y seleccionar la organización

<p align="center">
  <img src="https://i.imgur.com/OiIGt1p.png" alt="Paso 2: Selección de GitHub como origen" width="600"/>
</p>

<br>

**Paso 3.** Configurar el acceso a los repositorios

<p align="center">
  <img src="https://i.imgur.com/5VcU1jt.png" alt="Paso 3: Autorización de Netlify con GitHub" width="600"/>
</p>

<p align="center">
  <img src="https://i.imgur.com/oHvqYHU.png" alt="Paso 3: Autorización de Netlify con GitHub" width="600"/>
</p>

<br>

**Paso 4.** Configurar parámetros de despliegue

<p align="center">
  <img src="https://i.imgur.com/3ceaHLi.png" alt="Paso 4: Selección de la organización" width="600"/>
</p>

<br>

**Paso 5.** Verificación final
<p align="center">
  <img src="https://i.imgur.com/tUAibBX.png" alt="Paso 5: Selección del repositorio del landing page" width="600"/>
</p>

<br>

<br>

<br>

### 6.2. Landing Page & Mobile Application Implementation

En esta sección se describe la implementación técnica de la Landing Page y de las aplicaciones móviles, incluyendo las herramientas, tecnologías y la metodología ágil aplicada mediante sprints en cada entrega del producto.

<br>

#### 6.2.1. Sprint 1

Este apartado presenta los resultados del **Sprint #1**, correspondiente a la primera entrega del proyecto. Se incluyen los avances organizativos, la asignación del trabajo y los entregables desarrollados: una landing page funcional, el avance del Web Service y una versión inicial de la Mobile Application.

<br>

##### 6.2.1.1. Sprint Planning 1

Seguidamente, se expone la planificación del Sprint 1, en la que se establecieron los objetivos iniciales, se priorizaron las tareas del backlog y se definieron las responsabilidades del equipo para este primer ciclo de desarrollo.

<table>
  <tr>
    <th>Sprint #</th>
    <th>Sprint 1</th>
  </tr>
  <tr>
    <td colspan="2" style="font-weight: bold;">Contexto de Planificación del Sprint</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Fecha</td>
    <td>08/05/2026</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Hora</td>
    <td>22:38 horas (GMT-5)</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Lugar</td>
    <td>Reunión virtual (Discord)</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Elaborado por</td>
    <td>Bastidas Bastidas, Diego Martin</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Participantes</td>
    <td>
      Bastidas Bastidas, Diego Martin<br>
      Cardenas Minaya, Ricardo Fernando<br>
      Dominguez Vargas, Rafael Alexander<br>
      Escobar Palomino, Sebastian Matias<br>
      Muñiz Huayanca, Percy Alonso
    </td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Resumen de la Sprint Review 1</td>
    <td>Al tratarse del primer sprint de desarrollo, no existe un resumen de revisión anterior.</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Resumen de la Retrospectiva del Sprint 1</td>
    <td>Como este es el sprint inicial, todavía no se han detectado oportunidades de mejora concretas en el proceso.</td>
  </tr>
  <tr>
    <td colspan="2" style="font-weight: bold;">Objetivo del Sprint e Historias de Usuario</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Objetivo del Sprint 1</td>
    <td>Buscamos desarrollar una landing page que comunique de forma visual y comprensible las funcionalidades y beneficios de DispenXCore, generando en los visitantes una percepción inicial sólida sobre la plataforma y su propuesta de valor. Esta página facilitará la exploración de sus secciones para que los usuarios entiendan cómo nuestra solución vincula eficazmente la gestión inteligente de suministros con sus hogares. Además, se pondrá en valor la app web por su uso práctico y accesible, permitiendo la interacción con la plataforma desde cualquier ubicación. Validaremos este enfoque analizando la navegación de los visitantes en la landing page y su uso de la integración con la app web.</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Velocidad del Sprint 1</td>
    <td>20</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Total de Story Points</td>
    <td>20</td>
  </tr>
</table>

<br>

##### 6.2.1.2. Sprint Backlog 1

En el primer sprint, el equipo enfocó su trabajo en crear una landing page que fuera tanto funcional como atractiva, asignando las tareas en el tablero de Sprint según las habilidades de cada miembro.

| ID    | Title                          | Description                                                                                                                                                | Estimation (Hours) | Assigned To                     | Status |
| ----- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------- | ------ |
| LPS01 | Navigation                     | Implementación de la barra de navegación con enlaces a las secciones "¿Cómo funciona?", "Casos de éxito", "Planes" y "Contactos".                          | 4                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS02 | Hero Section                   | Implementación de la sección "Hero Section", diseñada para captar la atención de los usuarios y presentar brevemente la aplicación.                        | 2                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS03 | About the Product              | Desarrollo de la sección "About the Product", donde se describen brevemente el producto y sus principales beneficios.                                      | 2                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS04 | Services and Features          | Desarrollo de la sección "Services and Features", donde se muestran las funcionalidades clave de DispenXCore.                                              | 3                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS05 | Testimonials                   | Desarrollo de la sección "Testimonials", donde se presentan los comentarios y experiencias de usuarios que han utilizado la aplicación.                    | 3                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS06 | Contact                        | Desarrollo de la sección "Contact", donde se detalla la forma en que los usuarios pueden comunicarse con el equipo detrás de **DispenXCore**.              | 2                  | Bastidas Bastidas, Diego Martín | Done   |
| LPS07 | Footer                         | Desarrollo de la sección "Footer", que incluye enlaces de navegación, redes sociales del equipo y accesos rápidos a las distintas secciones del sitio web. | 2                  | Bastidas Bastidas, Diego Martín | Done   |

<br>

##### 6.2.1.3. Development Evidence for Sprint Review

En esta sección se presenta la Evidencia de Desarrollo completada durante el sprint, demostrando el trabajo funcional realizado y los incrementos del producto listos para ser inspeccionados y validados en la Sprint Review.

| Repository | Branch | Commit Id | Commit Message | Committed By | Committed On |
|---|---|---|---|---|---|
| 1ASI0572-2610-17755-G4-DispenXCore | main | e0722ca | Initial commit | alomsoo | May 07, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | b1de01f | added message to read.me | alomsoo | May 07, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 0c9186c | feat: landing page DispenXCore | alomsoo | May 07, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 4c7916f | Merge pull request #1 from 1ASI0572-2610-17755-G4-DispenXCore/feature/landing-page | alomsoo | May 07, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 5b9d73e | feat: add support | sebasepe | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | d6ab4df | feat: add settings | sebasepe | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | a2482c5 | Merge pull request #2 from 1ASI0572-2610-17755-G4-DispenXCore/feature/Support-Dashboard-Settings | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | db582de | feat(iamUser): Add user conection and | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 3072183 | Merge pull request #3 from 1ASI0572-2610-17755-G4-DispenXCore/feature/iam-user | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 99e0d68 | Merge pull request #4 from 1ASI0572-2610-17755-G4-DispenXCore/develop | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 858d82e | feat(iamUser): Add json-server dependency and update db.json structure | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 2f2b504 | Merge pull request #5 from 1ASI0572-2610-17755-G4-DispenXCore/feature/iam-user | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 4237f05 | Merge pull request #6 from 1ASI0572-2610-17755-G4-DispenXCore/develop | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 806d0c0 | feat(iamUser): Update environment configurations and budget limits | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 9f711c5 | Merge pull request #7 from 1ASI0572-2610-17755-G4-DispenXCore/feature/iam-user | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 9d6ef65 | Merge pull request #8 from 1ASI0572-2610-17755-G4-DispenXCore/develop | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | eeef321 | feat(iamUser): Add package.json with json-server configuration | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 30be5d6 | Merge pull request #9 from 1ASI0572-2610-17755-G4-DispenXCore/feature/iam-user | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 43557e4 | Merge pull request #10 from 1ASI0572-2610-17755-G4-DispenXCore/develop | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | c7ba0e1 | feat(iamUser): Update supply types to uppercase and modify db.json structure | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 63fabe7 | feat(iamUser): Refactor components and implement NotFound and Support pages | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | 996e9a5 | Merge pull request #11 from 1ASI0572-2610-17755-G4-DispenXCore/feature/iam-user | Radv2005 | May 12, 2026 |
| 1ASI0572-2610-17755-G4-DispenXCore | main | fa6ee40 | Merge pull request #12 from 1ASI0572-2610-17755-G4-DispenXCore/develop | Radv2005 | May 12, 2026 |
|

<br>

##### 6.2.1.4. Testing Suite Evidence for Sprint Review

En este primer Sprint, veremos los archivos `.feature` relacionados a los user tasks que hemos desarrollado, subidos en el repositorio.

<table>
  <thead>
    <tr>
      <th>&nbsp;&nbsp;&nbsp;<br>Repository&nbsp;&nbsp;&nbsp;</th>
      <th>&nbsp;&nbsp;&nbsp;<br>Branch&nbsp;&nbsp;&nbsp;</th>
      <th>&nbsp;&nbsp;&nbsp;<br>Commit ID&nbsp;&nbsp;&nbsp;</th>
      <th>&nbsp;&nbsp;&nbsp;<br>Commit<br>&nbsp;&nbsp;&nbsp;<br>Message&nbsp;&nbsp;&nbsp;</th>
      <th>&nbsp;&nbsp;&nbsp;<br>Commit<br>&nbsp;&nbsp;&nbsp;<br>Message Body&nbsp;&nbsp;&nbsp;</th>
      <th>&nbsp;&nbsp;&nbsp;<br>Committed on&nbsp;&nbsp;&nbsp;(Date)&nbsp;&nbsp;&nbsp;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="7">
        <a href="https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore--Features" target="_blank" rel="noopener noreferrer">
          https://github.com/1ASI0572-2610-17755-G4-DispenXCore/DispenXCore--Features
        </a>
      </td>
      <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
      <td>&nbsp;&nbsp;&nbsp;<br>d8b5cca</td>
      <td>&nbsp;&nbsp;&nbsp;<br>feat: add epic story 05</td>
      <td>&nbsp;&nbsp;&nbsp;<br>Add epic story 05</td>
      <td>&nbsp;&nbsp;&nbsp;<br>13/05/2026</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
      <td>&nbsp;&nbsp;&nbsp;<br>673a263</td>
      <td>&nbsp;&nbsp;&nbsp;<br>feat: add epic story 04</td>
      <td>&nbsp;&nbsp;&nbsp;<br>Add epic story 04</td>
      <td>&nbsp;&nbsp;&nbsp;<br>13/05/2026</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
      <td>&nbsp;&nbsp;&nbsp;<br>c71ee8d</td>
      <td>&nbsp;&nbsp;&nbsp;<br>feat: add epic story 03</td>
      <td>&nbsp;&nbsp;&nbsp;<br>Add epic story 03</td>
      <td>&nbsp;&nbsp;&nbsp;<br>13/05/2026</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
      <td>&nbsp;&nbsp;&nbsp;<br>893bf09</td>
      <td>&nbsp;&nbsp;&nbsp;<br>feat: add epic story 02</td>
      <td>&nbsp;&nbsp;&nbsp;<br>Add epic story 02</td>
      <td>&nbsp;&nbsp;&nbsp;<br>13/05/2026</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&nbsp;<br>main&nbsp;&nbsp;&nbsp;</td>
      <td>&nbsp;&nbsp;&nbsp;<br>cfd73e5</td>
      <td>&nbsp;&nbsp;&nbsp;<br>feat: add epic story 01</td>
      <td>&nbsp;&nbsp;&nbsp;<br>Add epic story 01</td>
      <td>&nbsp;&nbsp;&nbsp;<br>13/05/2026</td>
    </tr>

  </tbody>
</table>


<br>

##### 6.2.1.5. Execution Evidence for Sprint Review

Esta sección expone la Evidencia de Ejecución del sprint, donde se aprecia el producto operativo o el incremento de valor implementado, preparado para su revisión y validación en la Sprint Review.

<br>

###### Landing Page

A continuación, se presentan las evidencias de la implementación de la landing page desarrollada en HTML, CSS y JS con la biblioteca Bootstrap.

**LPS 01 — Hero Section**

<p align="center">
  <img src="https://i.imgur.com/zotNqEo.png" alt="Hero Section"/>
</p>

<br>

**LPS 02 — Problema**

<p align="center">
  <img src="https://i.imgur.com/UJQGp0F.png" alt="About the product"/>
</p>

<br>

**LPS 03 — Solución al problema**

<p align="center">
  <img src="https://i.imgur.com/mIUbX7Y.png" alt="Services"/>
</p>

<br>

**LPS 04 — Características**

<p align="center">
  <img src="https://i.imgur.com/6WnoumP.png" alt="Testimonials"/>
</p>

<br>

**LPS 05 — Para quien es?**

<p align="center">
  <img src="https://i.imgur.com/DPbgwpQ.png" alt="Contact"/>
</p>

<br>

**LPS 07 — Nuestro Equipo**

<p align="center">
  <img src="https://i.imgur.com/0kgTgFw.png" alt="Footer"/>
</p>

<br>

**LPS 08 — Preguntas Frecuentes**

<p align="center">
  <img src="https://i.imgur.com/TmqTwZf.png" alt="Footer"/>
</p>

<br>

**LPS 09 — Contactos**

<p align="center">
  <img src="https://i.imgur.com/nQjAJiu.png" alt="Footer"/>
</p>

<br>

###### Web Application
**WA 01 — Sign In**
<p align="center">
  <img src="https://i.imgur.com/RWyXGZp.png" alt="Web app screen 1"/>
</p>

**WA 02 — Sign Up**
<p align="center">
  <img src="https://i.imgur.com/Sq2HXyg.png" alt="Web app screen 2"/>
</p>

**WA 03 — Dashboard**
<p align="center">
  <img src="https://i.imgur.com/MsFNk7D.png" alt="Web app screen 3"/>
</p>

**WA 04 — Schedule**
<p align="center">
  <img src="https://i.imgur.com/mIwQrFW.png" alt="Web app screen 4"/>
</p>

**WA 05 — History**
<p align="center">
  <img src="https://i.imgur.com/s39boQc.png" alt="Web app screen 5"/>
</p>

**WA 06 — Settings**
<p align="center">
  <img src="https://i.imgur.com/AKIxkpG.png" alt="Web app screen 5"/>
</p>

**WA 07 — Support**
<p align="center">
  <img src="https://i.imgur.com/PJ3iBiY.png" alt="Web app screen 5"/>
</p>
<br>

##### 6.2.1.6. Services Documentation Evidence for Sprint Review

En este Sprint se logró documentar con **OpenAPI** los endpoints correspondientes a las funcionalidades implementadas. La documentación incluye detalles técnicos de los servicios consumidos por la aplicación móvil, como los verbos HTTP, parámetros de entrada y respuestas esperadas, permitiendo una mejor comprensión e integración de la app con la API.

| Endpoint                            | Acción                              | Verbo HTTP | Sintaxis de llamada                | Parámetros o Peticiones                                                                                                                              | Ejemplo de Response                                                                                                                                                                              | URL de Documentación                                     |
| ----------------------------------- | ----------------------------------- | ---------- | ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| /api/auth/login                     | Autenticación                       | POST       | api/auth/login                     | `{"email": "string", "password": "string"}`                                                                                                          | `{"accessToken": "string", "refreshToken": "string"}`                                                                                                                                            | http://localhost:8080/api/auth/login                     |
| /api/auth/register                  | Registro de usuario                 | POST       | api/auth/register                  | `{"email": "string", "firstName": "string", "lastName": "string", "password": "string"}`                                                             | `{"userId": "string", "message": "Usuario registrado exitosamente"}`                                                                                                                             | http://localhost:8080/api/auth/register                  |
| /api/v1/dispensers                  | Registrar dispensador               | POST       | api/v1/dispensers                  | `{"name": "string", "userId": "string", "grainType": "string", "maxCapacityG": "float"}`                                                             | `{"dispenserId": "string", "message": "Dispensador registrado"}`                                                                                                                                 | http://localhost:8080/api/v1/dispensers                  |
| /api/v1/dispensers/{id}             | Actualizar dispensador              | PUT        | api/v1/dispensers/{id}             | `{"name": "string", "grainType": "string", "maxCapacityG": "float"}`                                                                                 | `{"dispenserId": "string", "message": "Dispensador actualizado"}`                                                                                                                                | http://localhost:8080/api/v1/dispensers/{id}             |
| /api/v1/dispensers/{id}             | Obtener dispensador por ID          | GET        | api/v1/dispensers/{id}             | none                                                                                                                                                 | `{"id": "string", "name": "string", "grainType": "string", "status": "string", "maxCapacityG": "float"}`                                                                                         | http://localhost:8080/api/v1/dispensers/{id}             |
| /api/v1/dispensers                  | Listar dispensadores por usuario    | GET        | api/v1/dispensers                  | query params: `?userId=string`                                                                                                                       | `[{"id": "string", "name": "string", "grainType": "string", "status": "string"}]`                                                                                                                | http://localhost:8080/api/v1/dispensers                  |
| /api/v1/telemetry                   | Recibir lectura de sensores         | POST       | api/v1/telemetry                   | `{"dispenserId": "string", "weightGrams": "float", "levelPercentage": "float", "flowRateGs": "float", "rawUltrasonicCm": "float"}`                   | `{"readingId": "string", "message": "Lectura registrada"}`                                                                                                                                       | http://localhost:8080/api/v1/telemetry                   |
| /api/v1/stock-readings              | Obtener historial de stock          | GET        | api/v1/stock-readings              | query params: `?dispenserId=string`                                                                                                                  | `[{"id": "string", "weightGrams": "float", "levelPercentage": "float", "recordedAt": "datetime"}]`                                                                                               | http://localhost:8080/api/v1/stock-readings              |
| /api/v1/alert-configurations        | Crear configuración de alerta       | POST       | api/v1/alert-configurations        | `{"dispenserId": "string", "lowThresholdPercentage": "float", "criticalThresholdPercentage": "float"}`                                               | `{"configId": "string", "message": "Configuración creada"}`                                                                                                                                      | http://localhost:8080/api/v1/alert-configurations        |
| /api/v1/alert-configurations/{id}   | Actualizar umbrales de alerta       | PUT        | api/v1/alert-configurations/{id}   | `{"lowThresholdPercentage": "float", "criticalThresholdPercentage": "float", "isEnabled": "boolean"}`                                                | `{"message": "Configuración actualizada"}`                                                                                                                                                       | http://localhost:8080/api/v1/alert-configurations/{id}   |
| /api/v1/notifications               | Listar notificaciones del usuario   | GET        | api/v1/notifications               | query params: `?userId=string`                                                                                                                       | `[{"id": "string", "type": "string", "title": "string", "messageBody": "string", "isRead": "boolean"}]`                                                                                          | http://localhost:8080/api/v1/notifications               |
| /api/v1/notifications/{id}/read     | Marcar notificación como leída      | PUT        | api/v1/notifications/{id}/read     | none                                                                                                                                                 | `{"message": "Notificación marcada como leída"}`                                                                                                                                                 | http://localhost:8080/api/v1/notifications/{id}/read     |
| /api/v1/caregiver-subscriptions     | Vincular cuidador a familiar        | POST       | api/v1/caregiver-subscriptions     | `{"caregiverId": "string", "monitoredUserId": "string", "alertConfigId": "string"}`                                                                  | `{"subscriptionId": "string", "message": "Suscripción creada"}`                                                                                                                                  | http://localhost:8080/api/v1/caregiver-subscriptions     |
| /api/v1/caregiver-subscriptions/{id}| Desactivar suscripción de cuidador  | DELETE     | api/v1/caregiver-subscriptions/{id}| none                                                                                                                                                 | `{"message": "Suscripción desactivada"}`                                                                                                                                                         | http://localhost:8080/api/v1/caregiver-subscriptions/{id}|

<br>

##### 6.2.1.7. Software Deployment Evidence for Sprint Review

En esta sección se presenta la Evidencia de Despliegue del Software, verificando que el incremento desarrollado durante el sprint ha sido implementado y se encuentra accesible en el entorno de destino para su revisión final.

<br>

###### Landing Page

A continuación, se proporcina el enlace del landing page

🔗 **Enlace:** [https://comforting-pony-e834fe.netlify.app/](https://comforting-pony-e834fe.netlify.app/)

<br>

<p align="center">
  <img src="https://i.imgur.com/rx1xRHY.png" alt="Hero Section desplegada"/>
</p>

<br>

###### Web Application

A continuación, se proporcina el enlace de despliegue del web application  

🔗 **Enlace:** [https://dispenxcore.netlify.app/](https://dispenxcore.netlify.app/)

<br>
<p align="center">
  <img src="https://i.imgur.com/FHNG8jA.png" alt="Web app deploy 1"/>
</p>

<br>

##### 6.2.1.8. Team Collaboration Insights during Sprint

En esta sección se exponen las **Reflexiones sobre la Colaboración del Equipo** durante el sprint, detallando las dinámicas de trabajo y las lecciones clave identificadas para la mejora continua del proceso.

| Alumno                              | Actividad                                     |
| ----------------------------------- | --------------------------------------------- |
| Bastidas Bastidas, Diego Martin     | Figma Design, Backend                         |
| Cardenas Minaya, Ricardo Fernando   | Figma Design, Prototyping, Frontend           |
| Dominguez Vargas, Rafael Alexander  | Figma Design, Frontend                        |
| Escobar Palomino, Sebastian Matias  | Figma Design, Frontend                        |
| Muñiz Huayanca, Percy Alonso        | Landing Page Deployment, Figma Design, Backend|

<br>

###### Evidencias de colaboración — Report

<p align="center">
  <img src="https://i.imgur.com/gkaUpXA.png" alt="Collaboration report 1"/>
</p>

<p align="center">
  <img src="https://i.imgur.com/T3SeC3t.png" alt="Collaboration report 2"/>
</p>


<br>

###### Evidencias de colaboración — Landing Page

<p align="center">
  <img src="https://i.imgur.com/jyGDh2I.png" alt="Collaboration landing 1"/>
</p>

<p align="center">
  <img src="https://i.imgur.com/SzE4rtX.png" alt="Collaboration landing 2"/>
</p>

<br>

###### Evidencias de colaboración — Web Application

<p align="center">
  <img src="https://i.imgur.com/GE7PYPi.png" alt="Collaboration web 1"/>
</p>

<p align="center">
  <img src="https://i.imgur.com/ocP0ZIB.png" alt="Collaboration web 2"/>
</p>

<br>

## Bibliografía

- Gartner, Inc. (2025). *Forecast: Internet of Things — Endpoints and spending*. Gartner.
  https://www.gartner.com/en/information-technology/insights/internet-of-things

- Statista. (2024). *Smart home — Worldwide*.
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


## **Anexos**

  **LANDING PAGE:** [LANDING PAGE](https://comforting-pony-e834fe.netlify.app/)

  **PPT DEL PROYECTO:** [PPT](https://www.canva.com/design/DAGzQEpBtMs/zjEr8_HDH_y-mSaGu_7O3A/edit) 

  **VIDEO DEL PROYECTO:** [VIDEO](https://acortar.link/se3cmV)

  **WEB APPLICATION:** [WEB APPLICATION](https://dispenxcore.netlify.app/)