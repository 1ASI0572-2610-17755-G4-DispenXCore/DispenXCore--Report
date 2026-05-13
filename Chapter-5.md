## **Capítulo V: Solution Software Design** 


### 5.1. Style Guidelines

En esta sección se definen los lineamientos visuales y de comunicación que guían el diseño de la solución DispenXCore. Estas guías garantizan una identidad coherente, accesible y reconocible en todos los entornos donde se manifiesta el producto: la landing page informativa, la aplicación web en Angular, la aplicación móvil en Flutter y la interfaz embebida del dispositivo IoT. El propósito es transmitir confianza tecnológica, precisión y cercanía con el usuario, alineando la experiencia visual con la misión de la startup: facilitar la gestión inteligente de suministros mediante el Internet de las Cosas.

#### 5.1.1. General Style Guidelines

**Nombre y Logotipo**

El nombre DispenXCore transmite precisión, tecnología y control central, reflejando la propuesta de la startup Los Guerreros Z de digitalizar la gestión de suministros a granel mediante IoT. La palabra se compone de tres conceptos clave: *Dispen* hace referencia al dispensador físico, *X* representa la triple validación de sensores (peso, nivel y flujo) que diferencia al producto, y *Core* alude al núcleo inteligente que centraliza la información del ecosistema. El logotipo de DispenXCore está compuesto por un símbolo y un logotipo tipográfico, donde el ícono combina elementos de tecnología y gestión de inventario, representando la conectividad IoT y el monitoreo de stock en tiempo real.

El diseño general es limpio, minimalista y moderno, asegurando una identidad visual fácil de reconocer y adaptable a distintos entornos digitales, como aplicaciones móviles, dashboards web y dispositivos embebidos. El conjunto visual busca inspirar confianza, precisión y tranquilidad, alineado con la misión de la marca: transformar la alacena tradicional en un sistema inteligente y conectado que anticipe las necesidades del usuario.

<p align="center">
  <img src="feature/chapter5/styles/logo-dispenxcore.png" alt="Logotipo DispenXCore" width="400"/>
</p>

**Tono de Comunicación**

El tono de comunicación de DispenXCore será humano, confiable, técnico y cercano. Se evita el lenguaje excesivamente complejo o frío, priorizando una comunicación clara y accesible para usuarios de distintos perfiles, desde entusiastas de la domótica hasta cuidadores de adultos mayores. El mensaje de la marca debe proyectar control, anticipación y tranquilidad, actuando como un asistente inteligente que acompaña al usuario en la gestión cotidiana de sus suministros sin perder la calidez del trato humano.

**Colors**

La identidad visual de DispenXCore se basa en una paleta de azules oscuros, teal y celestes, que representa confianza, tecnología y precisión, al mismo tiempo que evoca una sensación de modernidad y bienestar. El uso del contraste entre el azul profundo (Primary) y el teal vibrante (Secondary) simboliza la integración entre lo estructurado y lo dinámico, mostrando la conexión entre el hardware preciso y la experiencia digital fluida. Los colores secundarios neutros aportan claridad, equilibrio visual y legibilidad en interfaces densas en datos como dashboards de consumo.

| Rol | Hex | Uso principal |
|-----|-----|----------------|
| Primary | `#1E293B` | Cabeceras, navegación principal, textos destacados |
| Secondary | `#14B8A6` | Acciones positivas, confirmaciones, indicadores de stock saludable |
| Tertiary | `#38BDF8` | Elementos interactivos, enlaces, gráficos de telemetría |
| Neutral | `#F8FAFC` | Fondos, superficies, contenedores |
| Alert Critical | `#EF4444` | Alertas de stock crítico, errores |
| Alert Warning | `#F59E0B` | Alertas preventivas de stock bajo |

<p align="center">
  <img src="feature/chapter5/styles/paleta-colores.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

**Typography**

La tipografía principal de DispenXCore es **Inter**, elegida por su claridad, modernidad y excelente legibilidad en pantallas de distintos tamaños y resoluciones. Su estructura geométrica y limpia refleja la precisión tecnológica del proyecto, mientras que su amplia variedad de pesos permite establecer jerarquías visuales claras tanto en dashboards de datos como en notificaciones móviles. Los títulos usan un peso bold o semibold, los subtítulos un peso medium, y el texto regular se mantiene ligero y cómodo de leer.

<p align="center">
  <img src="feature/chapter5/styles/typography.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

**Spacing**

El sistema de espaciado en la interfaz de DispenXCore prioriza la legibilidad y la claridad visual, especialmente importante en dashboards donde se muestran múltiples indicadores de stock simultáneamente. Se aplican márgenes amplios (20 px) entre secciones principales, padding de 16–18 px en botones y elementos interactivos, y un interlineado de 1.5x en textos largos. Este enfoque garantiza una experiencia ordenada y fluida, evitando la saturación visual cuando el usuario monitorea varios dispensadores a la vez.

**Íconos de la aplicación**

Los íconos de DispenXCore son minimalistas, coherentes y de trazo redondeado, alineados con la identidad tecnológica y cercana del logotipo. Su diseño utiliza la paleta azul-teal-celeste para mantener una apariencia homogénea en toda la interfaz. Cada ícono tiene un propósito funcional claro dentro del ecosistema: gestión de dispensadores, monitoreo de stock, alertas, telemetría y administración de cuidadores. Su consistencia visual refuerza la confianza del usuario y facilita la comprensión inmediata de las acciones disponibles dentro de la app.

| Ícono | Significado |
|-------|-------------|
| 🏠 | Inicio / Dashboard |
| 📦 | Dispensador |
| 🌾 | Tipo de grano (arroz, azúcar, legumbres) |
| 📊 | Estadísticas de consumo |
| 🔔 | Notificaciones |
| ⚠️ | Alerta de stock bajo |
| 🚨 | Alerta crítica / agotamiento |
| 📡 | Telemetría / sensores |
| ⚖️ | Peso (celda de carga) |
| 📏 | Nivel (sensor ultrasónico) |
| 💧 | Flujo granular (sensor IR) |
| 👤 | Usuario / perfil |
| 👨‍👩‍👧 | Familiar monitoreado (cuidador) |
| ➕ | Añadir dispensador |
| ⚙️ | Configuración / umbrales |
| ✏️ | Editar |
| ✅ | Confirmación / stock saludable |
| 🔋 | Estado de batería del dispositivo |
| 📶 | Conectividad Wi-Fi |

**Lenguaje aplicado**

El lenguaje de DispenXCore es claro, directo y orientado a la acción, diseñado para inspirar confianza tanto en usuarios tecnológicos como en cuidadores con menor familiaridad digital. Se evita el uso excesivo de tecnicismos del dominio IoT, priorizando frases cortas que comuniquen estado e intención: *"Arroz al 15%"*, *"Reponer pronto"*, *"Todo en orden"*. La app y la web comunican con una voz que acompaña y anticipa, reflejando la visión de la startup: transformar la gestión manual de la alacena en una experiencia inteligente y preventiva.

**Consistencia**

DispenXCore mantiene consistencia visual y comunicativa en todas sus plataformas: landing page, aplicación web en Angular, aplicación móvil en Flutter y la interfaz embebida del dispositivo IoT. El uso uniforme del contraste azul oscuro–teal, la tipografía Inter y los íconos minimalistas crea una identidad reconocible y confiable. Esta coherencia asegura que el usuario, ya sea que esté configurando un umbral desde el celular o revisando un gráfico de consumo en el navegador, perciba el mismo ecosistema tecnológico, sólido y empático.

**Simplicidad**

El diseño prioriza la simplicidad y funcionalidad, eliminando elementos innecesarios y destacando solo la información relevante para la toma de decisiones: nivel actual de stock, alertas activas y próximas acciones recomendadas. El objetivo es que cualquier usuario, independientemente de su edad o experiencia tecnológica, pueda comprender el estado de su alacena en menos de cinco segundos. La simplicidad refuerza la misión de DispenXCore: hacer que la tecnología del cuidado doméstico sea accesible y proactiva.

**Comunicación**

El sistema de comunicación visual de DispenXCore incluye confirmaciones visuales y auditivas al realizar acciones importantes, como vincular un nuevo dispensador, configurar un umbral de alerta o recibir una notificación de stock crítico. Estos elementos generan confianza y seguridad operativa, garantizando que el usuario siempre sepa que el sistema está activo, midiendo y atento al estado real de sus suministros. Cada interacción busca transmitir control, anticipación y tranquilidad.

    
    
  - **5.1.2. Web, Mobile and IoT Style Guidelines**
    **Diseño general**

El diseño en los entornos web, móvil e IoT de DispenXCore mantiene una identidad visual uniforme, priorizando la claridad, accesibilidad y consistencia. Todos los componentes siguen la misma línea estética basada en la paleta azul oscuro, teal y celeste, acompañada de tonos neutros (blanco, gris y negro suave) para garantizar una presentación limpia, moderna y profesional, ideal para la visualización de datos de telemetría.

El objetivo es que la experiencia del usuario sea fluida y coherente, sin importar el dispositivo o entorno desde el cual interactúe con la plataforma: navegador web (Angular), aplicación móvil (Flutter) o el propio dispositivo IoT (ESP32) en la alacena.

**Colores y degradados**

La paleta principal de DispenXCore se centra en azules oscuros y tonos teal/celeste para reflejar confianza, tecnología y precisión. El uso de contrastes entre el `#1E293B` y los acentos `#14B8A6` / `#38BDF8` crea una apariencia dinámica y moderna, sin perder sobriedad ni legibilidad. Los colores semánticos (rojo para crítico, ámbar para advertencia) están reservados exclusivamente para estados del sistema, evitando su uso decorativo.
<p align="center">
  <img src="feature/chapter5/styles/paleta-colores.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

**Aplicación por entorno:**

- **Web (Angular):** uso de tonos planos con acentos teal en cabeceras, botones de acción y secciones destacadas del dashboard de telemetría. Fondos neutros para resaltar gráficos de consumo.
- **Móvil (Flutter):** colores planos con acentos teal y celeste para mejorar contraste y legibilidad en pantallas pequeñas. Las notificaciones push de stock crítico usan el rojo como ícono distintivo.
- **IoT (ESP32 / display embebido):** uso del azul principal y blanco para retroiluminación o pantallas LED, complementado por celeste para indicadores de estado, manteniendo una lectura clara incluso en entornos con poca luz como la cocina.

**Tipografía**

Se utiliza la tipografía **Inter** en todos los entornos, asegurando una experiencia legible y moderna en cualquier dispositivo. Su diseño geométrico y limpio transmite precisión y profesionalismo, ideal para productos tecnológicos enfocados en el monitoreo de datos en tiempo real. En la web se aprovechan los pesos mayores para encabezados de dashboards, mientras que en el móvil se priorizan los pesos regular y medium para reducir la carga visual en pantallas reducidas.

<p align="center">
  <img src="feature/chapter5/styles/typography.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

**Componentes visuales**

Los elementos visuales de DispenXCore comparten una estética minimalista y funcional. Se prioriza la simplicidad para facilitar la interacción, especialmente en usuarios cuidadores que necesitan reaccionar rápido ante alertas críticas.

Principales componentes:

- **Botones:** bordes redondeados, fondo teal (`#14B8A6`) para acciones primarias y azul oscuro (`#1E293B`) para acciones secundarias. Texto blanco.
- **Tarjetas de stock:** fondo blanco o gris claro, sombras suaves, barra de progreso lateral que indica el nivel actual del dispensador.
- **Alertas y notificaciones:** color teal para confirmaciones, ámbar para alertas preventivas y rojo para alertas críticas de agotamiento.
- **Gráficos de consumo:** líneas finas en teal o celeste sobre fondo neutro, con tooltips claros que muestran el peso exacto en gramos y la fecha de la lectura.
- **Inputs y formularios:** bordes redondeados, foco en celeste (`#38BDF8`), validación inline para configuración de umbrales.


<p align="center">
  <img src="feature/chapter5/styles/buttons.png" alt="Paleta de colores DispenXCore" width="600"/>
</p>

**Diseño responsivo**

El diseño es completamente adaptable y mantiene su coherencia visual en todos los dispositivos. Los elementos se ajustan según el entorno:

- **Web:** estructura modular con grid de tarjetas, sidebar de navegación y secciones amplias para gráficos detallados de consumo histórico.
- **Móvil:** diseño vertical, tarjetas apiladas, botones amplios y navegación táctil optimizada para el monitoreo rápido y la atención inmediata de notificaciones push.
- **IoT:** interfaz reducida con elementos esenciales (porcentaje de stock, estado de conexión, tipo de grano), priorizando claridad y reacción inmediata ante alertas de nivel crítico.

**Interacción y usabilidad**

El sistema de diseño de DispenXCore se centra en la experiencia del usuario. Cada interacción debe generar claridad, confianza y sensación de control sobre el inventario.

Principios de interacción:

- **Retroalimentación inmediata:** cambios de color o microanimaciones al interactuar con botones, sliders de umbral o íconos del dashboard.
- **Estados visuales claros:** diferenciación inequívoca entre stock saludable (teal), stock bajo (ámbar) y stock crítico (rojo).
- **Animaciones suaves:** transiciones ligeras entre pantallas y actualizaciones de stock para dar sensación de fluidez y tiempo real.
- **Iconografía uniforme:** íconos redondeados, minimalistas, en azul oscuro o teal sobre fondo blanco o neutro.
- **Accesibilidad:** contrastes que cumplen WCAG AA, tamaños de toque mínimos de 44 px en móvil, soporte para lectores de pantalla en la app de cuidadores.
    

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

        ##### Hero Banner Section

        ![Hero Banner](./feature/chapter5/landing_page/wireframes/1_Hero_Section.png)

        ##### Features Section

        ![Features](./feature/chapter5/landing_page/wireframes/2_Section_Problem.png)

        ##### Services Section

        ![Services](./feature/chapter5/landing_page/wireframes/3_Section_Solution.png)

        ##### Product Overview Section

        ![Product Overview](./feature/chapter5/landing_page/wireframes/4_Section_Carac.png)

        ##### Target Users Section

        ![Target Users](./feature/chapter5/landing_page/wireframes/5_Section_Carac.png)

        ##### Team Section

        ![Team](./feature/chapter5/landing_page/wireframes/6_Section_Team.png)

        ##### FAQ Section

        ![FAQ](./feature/chapter5/landing_page/wireframes/7_Section_Faq.png)

        ##### Contact Us Section

        ![Contact Us](./feature/chapter5/landing_page/wireframes/8_Section_Contact.png)

        ##### Footer Section

        ![Footer](./feature/chapter5/landing_page/wireframes/10_Section_Footer.png)



    <hr class="page-break">

    - **5.3.2. Landing Page Mock-up**

        ##### Hero Banner Section

        ![Hero Banner](./feature/chapter5/landing_page/muckups/1_Hero_Section.png)

        ##### Features Section

        ![Features](./feature/chapter5/landing_page/muckups/2_Section_Problem.png)

        ##### Services Section

        ![Services](./feature/chapter5/landing_page/muckups/3_Section_Solution.png)

        ##### Product Overview Section

        ![Product Overview](./feature/chapter5/landing_page/muckups/4_Section_Carac.png)

        ##### Target Users Section

        ![Target Users](./feature/chapter5/landing_page/muckups/5_Section_Users.png)

        ##### Team Section

        ![Team](./feature/chapter5/landing_page/muckups/6_Section_Team.png)

        ##### FAQ Section

        ![FAQ](./feature/chapter5/landing_page/muckups/7_Section_Faq.png)

        ##### Contact Us Section

        ![Contact Us](./feature/chapter5/landing_page/muckups/8_Section_Contact.png)

        ##### Footer Section

        ![Footer](./feature/chapter5/landing_page/muckups/9_Section_Footer.png)

<hr class="page-break">

- **5.4. Applications UX/UI Design**
    - **5.4.1. Applications Wireframes**

        #### Web Application

        ##### Login

        ![Wireframe2](./feature/chapter5/Applications_Wireframes/1_Login.png)

        ##### Register

        ![Wireframe3](./feature/chapter5/Applications_Wireframes/2_Register.png)

        <hr class="page-break">

        ##### Dashboard

        ![Wireframe4](./feature/chapter5/Applications_Wireframes/3_DashBoard_1.png)

        ##### Schedule

        ![Wireframe5](./feature/chapter5/Applications_Wireframes/4_Schedule.png)

        <hr class="page-break">

        ##### History

        ![Wireframe6](./feature/chapter5/Applications_Wireframes/5_History.png)

        ##### Settings

        ![Wireframe7](./feature/chapter5/Applications_Wireframes/6_Settings.png)

        <hr class="page-break">

        ##### Support

        ![Wireframe8](./feature/chapter5/Applications_Wireframes/7_Support.png)

    <hr class="page-break">

    - **5.4.2. Applications Wireflow Diagrams**

        #### Web Application

        ##### Register

        ![WireflowRegister](./feature/chapter5/Applications_Wireflow_Diagrams/1_Register.png)

        ##### Login

        ![WireflowLogin](./feature/chapter5/Applications_Wireflow_Diagrams/2_Login.png)

        ##### Schedule

        ![WireflowSchedule](./feature/chapter5/Applications_Wireflow_Diagrams/3_Schedule.png)

        ##### History

        ![WireflowHistory](./feature/chapter5/Applications_Wireflow_Diagrams/4_History.png)

        <hr class="page-break">

        ##### Settings

        ![WireflowSettings](./feature/chapter5/Applications_Wireflow_Diagrams/5_Settings.png)

        ##### Support

        ![WireflowSupport](./feature/chapter5/Applications_Wireflow_Diagrams/6_Support.png)

    <hr class="page-break">

    - **5.4.3. Applications Mock-ups**

        #### Web Application

        ##### Login

        ![MockupLogin](./feature/chapter5/Applications_Mock-ups/1_Login.png)

        ##### Register

        ![MockupRegister](./feature/chapter5/Applications_Mock-ups/2_Register.png)

        <hr class="page-break">

        ##### Dashboard

        ![MockupDashboard](./feature/chapter5/Applications_Mock-ups/3_DashBoard_1.png)

        ##### Schedule

        ![MockupSchedule](./feature/chapter5/Applications_Mock-ups/4_Schedule.png)

        <hr class="page-break">

        ##### Schedule Create

        ![MockupScheduleCreate](./feature/chapter5/Applications_Mock-ups/5_ScheduleCrear.png)

        ##### History

        ![MockupHistory](./feature/chapter5/Applications_Mock-ups/6_History.png)

        <hr class="page-break">

        ##### Settings

        ![MockupSettings](./feature/chapter5/Applications_Mock-ups/7_Settings.png)

        ##### Support

        ![MockupSupport](./feature/chapter5/Applications_Mock-ups/8_Support.png)

        <hr class="page-break">

        ##### Support Asked Questions

        ![MockupSupportFAQ](./feature/chapter5/Applications_Mock-ups/9_Support_2.png)

        ##### Searching Box

        ![MockupSearchBox](./feature/chapter5/Applications_Mock-ups/10_Buscador.png)

        <hr class="page-break">

        ##### Perfil Configuration

        ![MockupProfileConfig](./feature/chapter5/Applications_Mock-ups/11_ConfiguracionPerfil.png)

        ##### Notifications List

        ![MockupNotifications](./feature/chapter5/Applications_Mock-ups/12_NotificacionesLista.png)

    <hr class="page-break">

    - **5.4.4. Applications User Flow Diagrams**

        #### Web Application

        ##### Register

        ![UserFlowRegister](./feature/chapter5/Applications_User_Flow_Diagrams/1_Register.png)

        ##### Login

        ![UserFlowLogin](./feature/chapter5/Applications_User_Flow_Diagrams/2_Login.png)

        ##### US002 Actualizacion de Firmware Remote

        ![UserFlowUS002](./feature/chapter5/Applications_User_Flow_Diagrams/7_US02_Actualización_de_Firmware_Remota_(OTA).png)

        ##### US003 Configuracion de Umbral de Alerta de Stock Bajo

        ![UserFlowUS003](./feature/chapter5/Applications_User_Flow_Diagrams/5_US03_Configuración_de_Umbral_de_Alerta_de_Stock_Bajo.png)

        <hr class="page-break">

        ##### US006 Visualizacion de Stock Actual en Panel Web

        ![UserFlowUS006](./feature/chapter5/Applications_User_Flow_Diagrams/3_US06_Visualización_de_Stock_Actual_en_Panel_Web.png)

        ##### US007 Visualizacion de Graficos de Consumo Historico

        ![UserFlowUS007](./feature/chapter5/Applications_User_Flow_Diagrams/4_US07_Visualización_de_Gráficos_de_Consumo_Histórico.png)

        ##### US015 Centro de Ayuda y Preguntas Frecuentes (FAQ)

        ![UserFlowUS015](./feature/chapter5/Applications_User_Flow_Diagrams/6_US15_Centro_de_Ayuda_y_Preguntas_Frecuentes_(FAQ).png)

<hr class="page-break">

- **5.5. Applications Prototyping**

#### Web Application

A continuación, se presenta el video demostrativo donde se evidencia el prototipo interactivo de las aplicaciones móviles, mostrando el flujo de usuario y la experiencia de interacción final.

Prototyping: https://www.figma.com/proto/9zfoLcEEgnm15cXfdElAv6/Prototyping?node-id=1-2015&p=f&t=lTXhQ079NFQ9NE2a-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=1%3A2015


Link del video: https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312318_upc_edu_pe/IQD95BReG4PVTIdWSt4Xts5IATR2tJSg7a6IYBVbzCr34Po?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=OwGYah

- **5.6. IoT Device Design**

    En esta sección presentamos el diseño y la implementación del dispositivo IoT desarrollado en Wokwi para DispenXCore. El sistema integra cuatro sensores principales: un sensor de temperatura y humedad DHT22, una celda de carga con módulo HX711 para medición de peso, y un sensor ultrasónico HC-SR04 para medición de nivel. Los datos son visualizados en tiempo real a través de una pantalla LCD 20x4. <br>
    El sistema cuenta con un módulo de alertas mediante buzzer que se activa en dos condiciones críticas: cuando el peso desciende por debajo de 0.5 kg, indicando que el dispensador está casi vacío, y cuando la humedad supera el 70%, lo que podría comprometer la calidad del producto almacenado. <br>
    La simulación fue desarrollada en Wokwi con un ESP32, permitiendo validar el comportamiento del firmware antes de pasar a la implementación física del dispositivo.

    ##### Prototipo en funcionamiento
    ![MockupScheduleCreate](./feature/chapter5/wokwi_1.png)

    ##### Cuando la humedad es mayor a 70

    ![MockupScheduleCreate](./feature/chapter5/wokwi_2.png)

    ##### Cuando el peso es menor a 0.5 kg

    ![MockupScheduleCreate](./feature/chapter5/wokwi_3.png)

    ##### Codigo de wokwi

    ```cpp
    #include <DHT.h>
    #include <HX711.h>
    #include <Wire.h>
    #include <LiquidCrystal_I2C.h>

    #define DHTPIN 13
    #define DHTTYPE DHT22
    #define BUZZER_PIN 19
    #define TRIG_PIN 26
    #define ECHO_PIN 27
    #define HX_DT 4
    #define HX_SCK 5

    DHT dht(DHTPIN, DHTTYPE);
    HX711 scale;
    LiquidCrystal_I2C lcd(0x27, 20, 4);

    #define PESO_MINIMO    0.5 
    #define HUMEDAD_MAXIMA 70.0

    void setup() {
    Serial.begin(115200);
    delay(1000);

    pinMode(BUZZER_PIN, OUTPUT);
    pinMode(TRIG_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);

    dht.begin();

    scale.begin(HX_DT, HX_SCK);
    scale.set_scale(420);
    scale.tare();

    lcd.init();
    lcd.backlight();
    lcd.setCursor(0, 0);
    lcd.print("Dispenser Ready");
    delay(2000);
    lcd.clear();
    }

    float readDistance() {
    digitalWrite(TRIG_PIN, LOW);
    delayMicroseconds(2);
    digitalWrite(TRIG_PIN, HIGH);
    delayMicroseconds(10);
    digitalWrite(TRIG_PIN, LOW);
    long duration = pulseIn(ECHO_PIN, HIGH);
    return duration * 0.034 / 2;
    }

    void loop() {
    float weight      = scale.get_units(10);
    float humidity    = dht.readHumidity();
    float temperature = dht.readTemperature();
    float distance    = readDistance();

    if (isnan(humidity) || isnan(temperature)) {
        Serial.println("ERROR: DHT no responde");
        return;
    }

    Serial.println("==========");
    Serial.print("Temperatura: "); Serial.print(temperature); Serial.println(" C");
    Serial.print("Humedad: ");     Serial.print(humidity);    Serial.println(" %");
    Serial.print("Peso: ");        Serial.print(weight, 2);   Serial.println(" kg");
    Serial.print("Distancia: ");   Serial.print(distance);    Serial.println(" cm");

    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Temp:"); lcd.print(temperature, 1); lcd.print(" C");
    lcd.setCursor(0, 1);
    lcd.print("Hum:"); lcd.print(humidity, 1); lcd.print(" %");
    lcd.setCursor(0, 2);
    lcd.print("Peso:"); lcd.print(weight, 2); lcd.print(" kg");
    lcd.setCursor(0, 3);
    lcd.print("Nivel:"); lcd.print(distance, 1); lcd.print(" cm");

    if (humidity > 70.0) {
        tone(BUZZER_PIN, 1000);
        Serial.println("ALERTA: HUMEDAD ALTA");
    } else if (weight < 0.5) {
        tone(BUZZER_PIN, 1500);
        Serial.println("ALERTA: PESO BAJO");
    } else {
        noTone(BUZZER_PIN);
    }

    delay(2000);
    }
    ```

    ##### Wokwi link: 

    https://wokwi.com/projects/463881485998547969
