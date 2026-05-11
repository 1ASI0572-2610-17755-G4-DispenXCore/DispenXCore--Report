## **Capítulo V: Solution Software Design** 

- **5.1. Style Guidelines**
    - **5.1.1. General Style Guidelines**
    - **5.1.2. Web, Mobile and IoT Style Guidelines**

<hr class="page-break">

- **5.2. Information Architecture**

    - **5.2.1. Organization Systems**

    En la landing page se han aplicado sistemas de organización para estructurar la solución IoT de manera clara, permitiendo que tanto usuarios domésticos como pequeños negocios comprendan la propuesta de valor:

    * **Organización visual jerárquica:** Utilizada en la *hero section*, donde se destaca el propósito de "Digitalizar tu despensa". El uso de contraste guía al usuario hacia el botón de acción para adquirir o conocer el dispositivo físico.
    * **Organización secuencial:** El flujo guía al usuario desde la problemática, pasando por la solución, hasta la visualización de datos en la aplicación móvil/web.
    * **Organización matricial:** Aplicada en la comparativa de dispositivos o planes de monitoreo, permitiendo evaluar en paralelo métricas como capacidad de carga, tipos de sensores incluidos y niveles de analítica predictiva.

    **Esquemas de categorización:**
    * **Por tópicos:** Secciones divididas en "Hardware" y "Software".
    * **Según audiencia:** Segmentación entre "Hogar Inteligente" y "Smart Business".
    
    <br>
    
    <hr class="page-break">

    - **5.2.2. Labeling Systems**

    A continuación, se detallan las etiquetas del sistema diseñadas:

    **1. Navegación Principal (Navbar)**
    | Clave JS | Etiqueta Simplificada |
    | :--- | :--- |
    | `nav-home` | Inicio |
    | `nav-iot-solution` | Dispositivo IoT |
    | `nav-app` | App Multiplataforma |
    | `nav-plans` | Planes de Gestión |
    | `nav-contact` | Soporte |

    **2. Sección Hero**
    | Clave JS | Etiqueta Simplificada |
    | :--- | :--- |
    | `hero-title` | Automatiza tu Despensa |
    | `hero-description` | Control de inventario en tiempo real con sensores de precisión. |
    | `hero-cta-button` | Ver Dispositivo |

    **3. Servicios: Hardware y Monitoreo**
    | Clave JS | Etiqueta Simplificada |
    | :--- | :--- |
    | `iot-sensors-title` | Tecnología de Precisión |
    | `iot-feature-loadcell` | Celda de Carga |
    | `app-predictive-title` | Analítica Predictiva |
    | `app-notif-description` | Alertas preventivas de stock bajo. |
    
    <br>
    
    <hr class="page-break">

    - **5.2.3. SEO Tags and Meta Tags**
    
    Para asegurar la accesibilidad en la gestión de insumos, se han definido los siguientes estándares:

    1.  **Jerarquía de Datos:** Uso de `h2` y `h3` para separar claramente las especificaciones técnicas del hardware de las funciones del software.
    2.  **Visualización de Estados:** Claves de color (`text-success`, `text-warning`) para representar niveles de inventario (lleno, bajo, crítico) de forma intuitiva.
    3.  **Iconografía:** Integración de **Lucide Icons** para representar tipos de granos (arroz, azúcar, legumbres) y conectividad (wifi, nube).
    4.  **Accesibilidad:** Contraste alto para facilitar el uso por parte de diversos perfiles de usuario en entornos de cocina o almacén.

    <br>

    - **5.2.4. Searching Systems**
    
    La navegación implementa un sistema de anclas directas en el header. Dado que el ecosistema incluye hardware y software, el sistema de búsqueda/navegación se enfoca en:
    1. **Navegación de Producto:** Acceso rápido a las especificaciones técnicas del dispensador.
    2. **Dashboard:** Un acceso directo para que el usuario visualice cómo se verían sus datos de consumo real.
    3. **Flujo Natural:** Propuesta de valor → Funcionamiento de sensores → Gestión en la App → Planes de suscripción.

    <br>

    - **5.2.5. Navigation Systems**
    
    La barra de navegación del header está diseñada para ser el centro de control de la información:
    1. **Inicio:** Propuesta general del ecosistema DispenXCore.
    2. **Dispositivo:** Detalle técnico del dispensador físico y sus sensores.
    3. **App:** Funcionalidades de la aplicación en Flutter/Angular (gráficos de consumo).
    4. **Planes:** Opciones de almacenamiento en la nube para el historial de inventario.
    5. **Soporte:** Ayuda técnica para la configuración del dispositivo IoT.

    <hr class="page-break">

- **5.3. Landing Page UI Design**
    - **5.3.1. Landing Page Wireframe**

    <hr class="page-break">

    - **5.3.2. Landing Page Mock-up**

<hr class="page-break">

- **5.4. Applications UX/UI Design**
    - **5.4.1. Applications Wireframes**

        #### Web Application

        ##### Login

        ![Wireframe2](./feature/chapter-5/applications-uxui-design/applications_wireframes/1_login.png)

        ##### Register

        ![Wireframe3](./feature/chapter-5/applications-uxui-design/applications_wireframes/2_register.png)

        <hr class="page-break">

        ##### Dashboard

        ![Wireframe4](./feature/chapter-5/applications-uxui-design/applications_wireframes/3_dashboard_1.png)

        ##### Schedule

        ![Wireframe5](./feature/chapter-5/applications-uxui-design/applications_wireframes/4_schedule.png)

        <hr class="page-break">

        ##### History

        ![Wireframe6](./feature/chapter-5/applications-uxui-design/applications_wireframes/5_history.png)

        ##### Settings

        ![Wireframe7](./feature/chapter-5/applications-uxui-design/applications_wireframes/6_settings.png)

        <hr class="page-break">

        ##### Support

        ![Wireframe8](./feature/chapter-5/applications-uxui-design/applications_wireframes/7_support.png)

    <hr class="page-break">

    - **5.4.2. Applications Wireflow Diagrams**

        #### Web Application

        ##### Register

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/1_register.png)

        ##### Login

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/2_login.png)

        ##### Schedule

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/3_schedule.png)

        ##### History

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/4_history.png)

        <hr class="page-break">

        ##### Settings

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/5_settings.png)

        ##### Support

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_wireflow_diagrams/6_support.png)

    <hr class="page-break">

    - **5.4.3. Applications Mock-ups**

        #### Web Application

        ##### Login

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/1_login.png)

        ##### Register

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/2_register.png)

        <hr class="page-break">

        ##### Dashboard

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/3_dashboard_1.png)

        ##### Schedule

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/4_schedule.png)

        <hr class="page-break">

        ##### Schedule Create

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/5_schedulecrear.png)

        ##### History

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/6_history.png)

        <hr class="page-break">

        ##### Settings

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/7_settings.png)

        ##### Support

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/8_support.png)

        <hr class="page-break">

        ##### Support Asked Questions

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/9_support_2.png)

        ##### Searching Box

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/10_buscador.png)

        <hr class="page-break">

        ##### Perfil Configuration

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/11_configuracionperfil.png)

        ##### Notifications List

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_mock-ups/12_notificacioneslista.png)

        <hr class="page-break">

    - **5.4.4. Applications User Flow Diagrams**

        #### Web Application

        ##### Register

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/1_register.png)

        ##### Login

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/2_login.png)

        ##### US002 Actualizacion de Firmware Remote

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/7_us02-actualizacion_de_firmware_remota_(ota).png)

        ##### US003 Configuracion de Umbral de Alerta de Stock Bajo

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/5_us03-configuracion_de_umbral_de_alerta_de_stock_bajo.png)

        <hr class="page-break">

        ##### US006 Visualizacion de Stock Actual en Panel Web

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/3_us06-visualizacion_de_stock_actual_en_panel_web.png)

        ##### US007 Visualizacion de Graficos de Consumo Historico

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/4_us07-visualizacion_de_graficos_de_consumo_historico.png)

        ##### US015 Centro de Ayuda y Preguntas Frecuentes (FAQ)

        ![Wireflow1](./feature/chapter-5/applications-uxui-design/applications_user_flow_diagrams/6_us15-centro_de_ayuda_y_preguntas_frecuentes_(faq).png)

<hr class="page-break">
- **5.5. Applications Prototyping**

#### Web Application

A continuación, se presenta el video demostrativo donde se evidencia el prototipo interactivo de las aplicaciones móviles, mostrando el flujo de usuario y la experiencia de interacción final.

Prototyping: https://www.figma.com/proto/9zfoLcEEgnm15cXfdElAv6/Prototyping?node-id=1-2015&p=f&t=lTXhQ079NFQ9NE2a-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=1%3A2015


Link del video: https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312318_upc_edu_pe/IQD95BReG4PVTIdWSt4Xts5IATR2tJSg7a6IYBVbzCr34Po?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=OwGYah

- **5.6. IoT Device Design**
