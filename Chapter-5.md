## **Capítulo V: Solution Software Design** 

- **5.1. Style Guidelines**
    - **5.1.1. General Style Guidelines**
    - **5.1.2. Web, Mobile and IoT Style Guidelines**

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
    
    - **5.2.3. SEO Tags and Meta Tags**
    
    Para asegurar la accesibilidad en la gestión de insumos, se han definido los siguientes estándares:

    1.  **Jerarquía de Datos:** Uso de `h2` y `h3` para separar claramente las especificaciones técnicas del hardware de las funciones del software.
    2.  **Visualización de Estados:** Claves de color (`text-success`, `text-warning`) para representar niveles de inventario (lleno, bajo, crítico) de forma intuitiva.
    3.  **Iconografía:** Integración de **Lucide Icons** para representar tipos de granos (arroz, azúcar, legumbres) y conectividad (wifi, nube).
    4.  **Accesibilidad:** Contraste alto para facilitar el uso por parte de diversos perfiles de usuario en entornos de cocina o almacén.

    <br>

    - **5.2.4. Searching Systems**
    
    La navegación implementa un sistema de anclas directas en el header. Dado que el ecosistema incluye hardware y software, el sistema de búsqueda/navegación se enfoca en:
    * **Navegación de Producto:** Acceso rápido a las especificaciones técnicas del dispensador.
    * **Dashboard:** Un acceso directo para que el usuario visualice cómo se verían sus datos de consumo real.
    * **Flujo Natural:** Propuesta de valor → Funcionamiento de sensores → Gestión en la App → Planes de suscripción.

    <br>

    - **5.2.5. Navigation Systems**
    
    La barra de navegación del header está diseñada para ser el centro de control de la información:
    * **Inicio:** Propuesta general del ecosistema DispenXCore.
    * **Dispositivo:** Detalle técnico del dispensador físico y sus sensores.
    * **App:** Funcionalidades de la aplicación en Flutter/Angular (gráficos de consumo).
    * **Planes:** Opciones de almacenamiento en la nube para el historial de inventario.
    * **Soporte:** Ayuda técnica para la configuración del dispositivo IoT.

- **5.3. Landing Page UI Design**
    - **5.3.1. Landing Page Wireframe**
    - **5.3.2. Landing Page Mock-up**

- **5.4. Applications UX/UI Design**
    - **5.4.1. Applications Wireframes**
    - **5.4.2. Applications Wireflow Diagrams**
    - **5.4.3. Applications Mock-ups**
    - **5.4.4. Applications User Flow Diagrams**

- **5.5. Applications Prototyping**
- **5.6. IoT Device Design**
