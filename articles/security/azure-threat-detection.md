---
title: "aaaAzure avanzada de detección de amenazas | Documentos de Microsoft"
description: "Información acerca de la protección de identidad y sus funcionalidades."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Detección de amenazas avanzada de Azure
## <a name="introduction"></a>Introducción

### <a name="overview"></a>Información general

Microsoft ha desarrollado una serie de notas del producto, información general de seguridad, prácticas recomendadas y las listas de comprobación tooassist Azure Hola a los clientes sobre diversos hello adyacente de la plataforma Azure y funciones relacionadas con la seguridad disponibles en. temas de Hello en cuanto a la amplitud y la profundidad de intervalo y se actualizan periódicamente. Este documento es parte de esa serie como se resume en hello pasos de la sección abstracta.

### <a name="azure-platform"></a>Plataforma Azure

Azure es una plataforma de servicio de nube pública que admite Hola selección más amplia de sistemas operativos, lenguajes de programación, marcos, herramientas, las bases de datos y dispositivos.
Admite Hola después de los lenguajes de programación:
-   Ejecute contenedores de Linux con integración de Docker.
-   Compile aplicaciones con JavaScript, Python,. NET, PHP, Java y Node.js.
-   Crear back-ends para dispositivos iOS, Android y Windows.

Servicios de nube pública de Azure admiten Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Cuando se migra tooa nube pública con una organización, esa organización es tooprotect responsable de los datos y proporcionar seguridad y gobernanza en todo sistema Hola.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus necesidades de seguridad. Azure proporciona una amplia gama de opciones tooconfigure y personalizar los requisitos de seguridad toomeet Hola de las implementaciones de aplicación. Este documento le ayuda a cumplir estos requisitos.

### <a name="abstract"></a>Descripción breve

Microsoft Azure ofrece funcionalidades de detección de amenazas avanzada integradas en servicios como Azure Active Directory, Azure Operations Management Suite (OMS) y Azure Security Center. Esta colección de servicios de seguridad y las capacidades proporciona una manera sencilla y rápida toounderstand lo que ocurre en las implementaciones de Azure.

Este documento le guiará Hola "enfoques de Microsoft Azure" hacia una vulnerabilidad de amenaza diagnóstico y análisis de riesgos de hello asociados a actividades malintencionadas hello como destinadas frente al servidores y otros recursos de Azure. Esto le ayudará a métodos de hello tooidentify de identificación y administración de vulnerabilidades con optimizado soluciones por hello plataforma Windows Azure y las tecnologías y servicios de seguridad de orientado al cliente.

En este documento se centra en la tecnología de saludo de la plataforma Windows Azure y los controles de orientado al cliente y no intenta tooaddress SLA, modelos y consideraciones sobre los procedimientos DevOps de precios.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) es una característica de hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition que proporciona una visión general de los eventos de riesgo de Hola y vulnerabilidades potenciales que afectan a su organización identidades. Microsoft ha Proteger identidades basadas en la nube para más de una década, y con Azure AD Identity Protection, Microsoft está realizando estos mismos sistemas de protección disponible tooenterprise clientes. Identity Protection usa las funcionalidades de detección de anomalías existentes de Azure AD (disponibles mediante [informes de actividad anómala de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)) e introduce nuevos tipos de eventos de riesgo que pueden detectar anomalías en tiempo real.

Protección de identidad utiliza algoritmos de aprendizaje automático adaptable y las anomalías de toodetect heurística y eventos de riesgo que pueden indicar que se ha puesto en peligro una identidad. Con estos datos, Identity Protection genera informes y alertas que le permiten tooinvestigate estos eventos de riesgo y tome las medidas adecuadas de mitigación o corrección.

Pero Azure Active Directory Identity Protection es más de una herramienta de supervisión e informes. Según los eventos de riesgo, Identity Protection calcula un nivel de riesgo de usuario para cada usuario, lo que le tooconfigure riesgo las directivas basadas en tooautomatically proteger Hola identidades de su organización.

Estas directivas en función del riesgo, en suma tooother [controles de acceso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) proporcionada por Azure Active Directory y [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), automáticamente puede bloquear u ofrecen acciones correctoras adaptable que incluyen restablecimiento de contraseñas y cumplimiento de la autenticación multifactor.

### <a name="identity-protections-capabilities"></a>Funcionalidades de Identity Protection

Azure Active Directory Identity Protection es más que una herramienta de supervisión e informes. tooprotect las identidades de su organización, puede configurar las directivas basadas en el riesgo que responden automáticamente toodetected problemas cuando se ha alcanzado un nivel de riesgo especificado. Estas directivas además tooother condicional tener acceso a controles proporcionados por Azure Active Directory y EMS, puede bloquear de forma automática o iniciar acciones de corrección adaptable entre ellos los restablecimientos de contraseña y la aplicación de la autenticación multifactor.

Ejemplos de algunas de las formas de Hola que protección de la identidad de Azure puede ayudar a protección sus cuentas e identidades incluyen:

[Detección de eventos de riesgo y cuentas peligrosas:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Detectar seis tipos de eventos de riesgo mediante el aprendizaje automático y las reglas heurísticas
-   Calcular los niveles de riesgo del usuario
-   Proporcionar recomendaciones personalizadas tooimprove condiciones globales de seguridad resaltando las vulnerabilidades

[Investigación de los eventos de riesgo:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Enviar notificaciones de los eventos de riesgo
-   Investigar los eventos de riesgo con información pertinente y contextual
-   Proporcionar flujos de trabajo básicos de las investigaciones de tootrack
-   Proporciona un acceso sencillo tooremediation acciones como el restablecimiento de contraseña

[Directivas de acceso condicional basadas en riesgos:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Directiva toomitigate arriesgados inicios de sesión bloqueando inicios de sesión o solicitando retos de la autenticación multifactor.
-   Directiva tooblock o cuentas de usuario de riesgo segura
-   Directiva toorequire usuarios tooregister para la autenticación multifactor

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

Con [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Administración de identidades con privilegios de Azure AD](./media/azure-threat-detection/azure-threat-detection-fig2.png)

puede administrar, controlar y supervisar el acceso dentro de la organización. Esto incluye tooresources de acceso de Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.

Privileged Identity Management de Azure AD le ayuda a:

-   Recibe una alerta e informar sobre los administradores de Azure AD y "justo a tiempo" acceso administrativo tooMicrosoft servicios en línea como Office 365 e Intune

-   Obtener informes sobre el historial de acceso de administrador y sobre los cambios en las asignaciones de administrador

-   Obtener alertas sobre los roles con privilegios de acceso tooa

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube. Puesto que OMS se implementa como un servicio basado en la nube, puede hacer que funcione rápidamente con una inversión mínima en servicios de infraestructura. Las características nuevas de seguridad se entregan automáticamente, lo que supone un ahorro en costos permanentes de mantenimiento y actualización.

Además tooproviding servicios valiosos en su propio, OMS pueden integrarse con componentes de System Center como [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend sus inversiones de administración de seguridad existentes a hello en la nube. System Center y OMS pueden trabajar juntos tooprovide experiencia de una administración híbrida completa.

### <a name="holistic-security-and-compliance-posture"></a>Seguridad integral y postura de cumplimiento

Hola [panel seguridad de OMS y auditoría](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) proporciona una vista completa de su organización postura de seguridad de TI con consultas de búsqueda integradas para problemas importantes que requieren su atención. panel de seguridad y auditoría de Hello es pantalla principal de Hola para todo lo relacionado con toosecurity de OMS. Proporciona una visión de alto nivel sobre estado de seguridad de Hola de los equipos. Hola capacidad tooview también incluye todos los eventos de hello últimas 24 horas, 7 días, o cualquier otro período de tiempo personalizado.

OMS paneles le servirán de forma rápida y sencilla Hola condiciones globales de seguridad de cualquier entorno, todo ello en contexto Hola de operaciones de TI, incluido: evaluación de actualizaciones de software, evaluación de antimalware y líneas base de configuración. Además, los datos de registro de seguridad no están accesibles en todo momento toostreamline Hola seguridad y cumplimiento de procesos de auditoría.

panel de OMS seguridad y auditoría de Hola se organiza en cuatro categorías principales:

![Panel de Seguridad y auditoría de OMS](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Dominios de seguridad:** en esta área, será capaz de toofurther explorar registros de seguridad con el tiempo, tener acceso a la evaluación de malware, actualizar evaluación, seguridad de red, información de identidad y acceso, los equipos con los eventos de seguridad y tener rápidamente panel de centro de seguridad de acceso tooAzure.

-   **Problemas importantes:** esta opción le permite tooquickly identificar el número de problemas activos Hola y Hola gravedad de estos problemas.

-   **Detecciones (versión preliminar):** permite tooidentify patrones de ataque al visualizar alertas de seguridad que realicen en los recursos.

-   **Inteligencia sobre amenazas:** permite tooidentify patrones de ataque al visualizar el número total de Hola de servidores con tráfico malintencionado saliente de IP, tipo de amenaza malintencionados de Hola y un mapa que muestra dónde proceden estas direcciones IP.

-   **Consultas comunes de seguridad:** esta opción proporciona una lista de seguridad más comunes de hello las consultas puede utilizar toomonitor en su entorno. Al hacer clic en una de las consultas, abre la hoja de búsqueda de hello con resultados de Hola para esa consulta.

### <a name="insight-and-analytics"></a>Insight and Analytics
En el centro de Hola de [análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) es el repositorio de OMS hello, que se hospeda en hello nube de Azure.

![Insight and Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Recopilar datos en el repositorio de Hola de orígenes conectados por configurar orígenes de datos y agregar suscripción de tooyour de soluciones.

![suscripción](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Soluciones y los orígenes de datos creará diferentes tipos de registros que tienen su propio conjunto de propiedades, pero pueden seguir analizando juntos en el repositorio de consultas toohello. Esto le permite hello toouse mismo toowork de herramientas y los métodos con distintos tipos de datos recopilado por diferentes orígenes.


La mayor parte de la interacción con análisis de registros es a través del portal de OMS hello, que se ejecuta en todos los exploradores y le proporciona acceso tooconfiguration configuración y varias herramientas tooanalyze y actuar en los datos recopilados. Desde el portal de hello, puede usar [búsquedas de registro](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) donde construir consultas tooanalyze recopilan datos, [paneles](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), que se pueden personalizar mediante vistas gráficas de las búsquedas más valiosas y [soluciones](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), que proporcionan las herramientas de análisis y funcionalidad adicionales.

![herramientas de análisis](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Las soluciones agregan funcionalidad tooLog análisis. Principalmente ejecutan en la nube de Hola y proporcionar un análisis de datos recopilados en el repositorio de OMS Hola. También pueden definir nuevos toobe de tipos de registro recopilado que se pueden analizar con búsquedas de registros o mediante la interfaz de usuario adicionales de solución de hello en el panel de OMS de Hola.
Hola seguridad y auditoría es un ejemplo de estos tipos de soluciones.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automation & Control: desviación de la alerta de configuración de seguridad

Automatización de Azure automatiza los procesos administrativos con runbooks que se basan en PowerShell y ejecutar en hello nube de Azure. Runbooks también se pueden ejecutar en un servidor en los recursos de local de toomanage de centros de datos locales. Azure Automation proporciona administración de configuración con DSC de PowerShell (Configuración de estado deseada).

![Azure Automation](./media/azure-threat-detection/azure-threat-detection-fig7.png)

Puede crear y administrar recursos de DSC hospedados en Azure y aplicarlos toodefine sistemas toocloud y local y automáticamente aplicar su configuración u obtener informes en una desviación toohelp asegurarse de que las configuraciones de seguridad permanezcan dentro de la directiva.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center ayuda a proteger los recursos de Azure. Proporciona una supervisión de la seguridad y una administración de directivas integradas en suscripciones de Azure. En el servicio de hello, es posible toodefine directivas no solo en las suscripciones de Azure, sino también en [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), por lo que puede ser más específico.

![Azure Security Center](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Los investigadores de seguridad de Microsoft están constantemente en lookout hello en busca de amenazas. Tienen acceso tooan amplio conjunto de telemetría adquirida de la presencia global de Microsoft en la nube de Hola y local. Esta colección de gran alcance y distintas de conjuntos de datos permite que Microsoft toodiscover nuevos ataques patrones y tendencias en sus productos locales de consumidor y empresa, así como a sus servicios en línea.

Por lo tanto, Security Center es capaz de actualizar rápidamente los algoritmos de detección a medida que los atacantes idean nuevos y más sofisticados ataques de seguridad. Este enfoque le ayuda a mantenerse al día en entornos con amenazas que cambian continuamente.

![Security Center](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Detección de amenazas de centro de seguridad funciona mediante la recopilación automáticamente información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados.  Analiza esta información, correlacionando la información de varios orígenes, tooidentify amenazas.
En el centro de seguridad se priorizan las alertas de seguridad junto con recomendaciones sobre cómo tooremediate Hola amenaza.

Security Center utiliza análisis avanzados que superan con creces los enfoques basados en firmas. Avances en grandes cantidades de datos y [aprendizaje automático](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologías son tooevaluate usa eventos a través de tejido de nube todo hello: detectar amenazas que serían imposible tooidentify usar métodos manuales y predecir Hola evolución de los ataques. Este análisis de seguridad incluye siguiente de saludo.

### <a name="threat-intelligence"></a>Información sobre amenazas

Microsoft dispone de una ingente cantidad de información sobre amenazas globales.
Flujos de telemetría en desde varios orígenes, como Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, Hola unidad de crímenes digitales (DCU) de Microsoft y Microsoft Security Response Center (MSRC).

![Información sobre amenazas](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Los investigadores de recibirán información de inteligencia de amenazas que se comparte entre los proveedores de servicios de nube principales y se suscribe toothreat intelligence fuentes de terceros. Centro de seguridad de Azure puede usar este tooalert de información que toothreats de conocidos actores no válidos. Estos son algunos ejemplos:

-   **Aprovechamiento de Hola Power de aprendizaje automático -** centro de seguridad de Azure tiene acceso tooa gran cantidad de datos sobre la actividad de red en la nube, que puede ser usa amenazas toodetect dirige a las implementaciones de Azure. Por ejemplo:

-   **Detecciones de fuerza bruta:** es toocreate usa un patrón histórico de intentos de acceso remoto, lo que permite que los ataques de fuerza bruta toodetect con puertos SQL, RDP y SSH de aprendizaje automático.

-   **Salida DDoS y detección de Botnet** -un objetivo común de ataques dirigidos recursos de nube es la capacidad de proceso de hello toouse de estos recursos tooexecute otros ataques.

-   **Nuevos servidores de análisis de comportamiento y las máquinas virtuales -** una vez que un servidor o la máquina virtual está en peligro, los atacantes emplean una gran variedad de técnicas tooexecute programas malintencionados en el sistema al evitar la detección, asegurándose de persistencia y obviando controles de seguridad.

-   **Detección de amenazas de base de datos SQL Azure -** tooaccess o vulnerabilidad de seguridad de bases de datos de intentos de detección de amenazas para Azure SQL Database, que identifica actividades anómalas de la base de datos que indica inusuales y potencialmente dañinos.

### <a name="behavioral-analytics"></a>Análisis del comportamiento

Análisis de comportamiento es una técnica que analiza y compara la recopilación de datos de tooa de patrones conocidos. No obstante, estos patrones no son simples firmas, Están determinados a través de algoritmos de aprendizaje de máquina complejas que son conjuntos de datos de toomassive aplicado.

![Análisis del comportamiento](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


También se determinan por medio de un análisis cuidadoso, llevado a cabo por analistas expertos, de los comportamientos malintencionados. Centro de seguridad de Azure puede usar recursos de tooidentify en peligro de análisis de comportamiento basados en el análisis de registros de la máquina virtual, los registros de tejido, registros de dispositivo de red virtual, volcados de memoria y otros orígenes.

Además, hay una correlación con los otro toocheck de señales para admitir la evidencia de una campaña generalizada. Esta correlación ayuda tooidentify eventos que son coherentes con los establecidos indicadores de riesgo.

Estos son algunos ejemplos:
-   **Ejecución de procesos sospechosa:** los atacantes emplean varias software malintencionado en tooexecute de técnicas sin que se detecte. Por ejemplo, un atacante podría dar malware Hola mismos nombres que los archivos del sistema legítimo pero coloque estos archivos en una ubicación alternativa, utilice un nombre que es muy similar a un archivo supone un riesgo o extensión real del archivo de máscara Hola. Monitores y los comportamientos de los procesos de modelos de centro de seguridad procesan a valores atípicos de toodetect ejecuciones como los siguientes.

-   **Oculta los intentos de malware y aprovechamiento:** sofisticado malware puede eludir los productos antimalware tradicional nunca escribir toodisk o cifrar los componentes de software que se almacenan en el disco. Sin embargo, dicho código mal intencionado se puede detectar mediante el análisis de memoria, malware Hola debe dejar los seguimientos en toofunction de memoria. Cuando se bloquea el software, un volcado de memoria captura una parte de la memoria en tiempo de Hola de fallo de Hola. Mediante el análisis de memoria de hello en el volcado de memoria hello, puede detectar técnicas empleadas tooexploit vulnerabilidades de software, tener acceso a datos confidenciales y conserva escondidas dentro de una máquina en peligro sin afectar al rendimiento de Hola de Azure Security Center su equipo.

-   **Lateral movimiento y reconocimiento interno:** toopersist en un datos valiosos en peligro de red y busque/cosecha, los atacantes a menudo tratar toomove lateralmente de hello en peligro tooothers máquina dentro de Hola la misma red. Centro de seguridad supervisa el proceso y toodiscover de las actividades de inicio de sesión trata tooexpand establecerse de un atacante en red hello, como la ejecución de comando remoto, el sondeo de red y la enumeración de cuentas.

-   **Los Scripts de PowerShell malintencionados:** PowerShell puede usarse por código malintencionado de los atacantes tooexecute en máquinas virtuales de destino para distintos fines. Security Center analiza la actividad de PowerShell en busca de evidencias de actividad sospechosa.

-   **Ataques de salida:** los atacantes a menudo los recursos de nube con el objetivo de hello del uso de dichos ataques adicionales de toomount de recursos de destino. Máquinas virtuales en peligro, por ejemplo, podría ser usado toolaunch ataques de fuerza bruta con otras máquinas virtuales, enviar correo basura o examinar puertos abiertos y otros dispositivos de hello Internet. Aplicando máquina toonetwork tráfico de aprendizaje, el centro de seguridad puede detectar cuándo las comunicaciones de red saliente superan norm Hola. Cuando correo no deseado, centro de seguridad también correlaciona tráfico inusual de correo electrónico con inteligencia de Office 365 toodetermine si es probable que correo electrónico de hello malintencionadas u Hola resultado de una campaña de correo electrónico legítima.

### <a name="anomaly-detection"></a>Detección de anomalías

Centro de seguridad de Azure también utiliza las amenazas de tooidentify de detección de anomalías. En análisis de toobehavioral de contraste (que depende de patrones conocidos que se deriva de grandes conjuntos de datos), detección de anomalías más "personalizada" y se centra en las líneas de base que son implementaciones de tooyour específico. Aprendizaje automático es toodetermine aplicada la actividad normal para las implementaciones y, a continuación, las reglas son las condiciones de valores atípicos de toodefine generado que pudieron representar un evento de seguridad. Veamos un ejemplo:

-   **Ataques por fuerza bruta de RDP/SSH entrantes:** es posible que las implementaciones integren máquinas virtuales con mucha actividad que tengan multitud de inicios de sesión al día y otras máquinas virtuales que tengan pocos o ningún inicio de sesión. Centro de seguridad de Azure puede determinar la actividad de inicio de sesión de línea de base para estas máquinas virtuales y usar toodefine de aprendizaje de máquina en las actividades de inicio de sesión normal de Hola. Si no hay ninguna discrepancia con línea de base de hello definido para inicio de sesión relacionados con las características, a continuación, se puede generar una alerta. Una vez más, es el aprendizaje automático el que se encarga de determinar qué es significativo.

### <a name="continuous-threat-intelligence-monitoring"></a>Supervisión continuada de la información sobre amenazas

Centro de seguridad de Azure funciona con seguridad datos ciencia equipos de investigación y a lo largo de Hola a todos que supervisar continuamente los cambios en el panorama de amenazas de Hola. Esto incluye Hola siguiendo las iniciativas:

-   **Supervisión de la información sobre amenazas:** la información sobre amenazas incluye mecanismos, indicadores, implicaciones y notificaciones que tienen relación con amenazas nuevas o existentes. Esta información se comparte en la Comunidad de seguridad de Hola y Microsoft supervisa continuamente las fuentes de inteligencia de amenazas desde fuentes internas y externas.

-   **Uso compartido de señales:** se comparte y se analiza la información que recopilan los equipos de Microsoft a partir de la amplia cartera de servicios en la nube y locales, de servidores y de dispositivos cliente de punto de conexión de Microsoft.

-   **Especialistas en seguridad de Microsoft:** colaboración continua con equipos de Microsoft que trabajan en ámbitos de seguridad especializados, como análisis forense y detección de ataques web.

-   **Ajuste de detección:** algoritmos se ejecutarán en conjuntos de datos reales de los clientes y los investigadores de seguridad trabajar con resultados de los clientes toovalidate Hola. Positivos true y false son algoritmos de aprendizaje automático de toorefine usado.

Estos esfuerzos combinados culminan en detecciones nuevas y mejoradas, que puede beneficiarse de forma instantánea: no hay ninguna acción para tootake.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Características de la detección de amenazas avanzada: otros servicios de Azure

### <a name="virtual-machine-microsoft-antimalware"></a>Microsoft Antimalware de máquina virtual

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) para Azure es una solución de agente único para aplicaciones y entornos de inquilino, diseñado toorun en segundo plano de hello sin intervención humana. Puede implementar la protección en función de las necesidades de Hola de las cargas de trabajo de aplicación, con cualquier básica proteger de forma predeterminada o avanzadas de configuración personalizada, incluida la supervisión de antimalware. Azure Antimalware es una opción de seguridad para Azure Virtual Machines que se instala automáticamente en todas las máquinas virtuales de PaaS de Azure.

**Características de Azure toodeploy y habilitar Microsoft Antimalware para las aplicaciones**

#### <a name="microsoft-antimalware-core-features"></a>Características principales de Microsoft Antimalware

-   **Protección en tiempo real -** supervisa la actividad en los servicios en la nube y en máquinas virtuales toodetect y bloquear la ejecución de malware.

-   **Análisis - programado** lleva a cabo periódicamente destino malware toodetect análisis, incluidos los programas que se ejecutan activamente.

-   **Corrección de malware:** actúa automáticamente sobre el malware detectado, y elimina o pone en cuarentena los archivos malintencionados y limpia las entradas del registro malintencionadas.

-   **Las actualizaciones de firma -** automáticamente instala hello más reciente protección firmas (las definiciones de virus) tooensure protección está actualizado en una frecuencia predeterminada.

-   **Actualizaciones del motor de antimalware -** automáticamente las actualizaciones de Hola motor de Antimalware de Microsoft.

-   **Actualización de la plataforma de antimalware:** automáticamente las actualizaciones de Hola plataforma Microsoft Antimalware.

-   **Protección activa -** informa de los metadatos de telemetría acerca de las amenazas detectadas y recursos sospechosa tooMicrosoft tooensure Azure respuesta rápida toohello evolucionando panorama de amenazas y habilitar la entrega de firma sincrónico en tiempo real a través de Hola Microsoft Active Protection System (MAPS).

-   **Ejemplos de informes -** proporciona e informes ejemplos toohello Microsoft Antimalware service toohelp refinar servicio hello y solución de problemas de habilitar.

-   **Exclusiones:** permite la aplicación y servicio administradores tooconfigure determinados archivos, procesos y unidades de tooexclude ellos de la protección y análisis de rendimiento y otras razones.

-   **Recopilación de eventos de antimalware -** registra el estado del servicio antimalware hello, las actividades sospechosas y las acciones correctoras tomadas en el registro de eventos del sistema operativo de Hola y recopila en la cuenta de almacenamiento de Azure del cliente de Hola.

### <a name="azure-sql-database-threat-detection"></a>Detección de amenazas de Azure SQL Database

[Detección de amenazas de base de datos de SQL Azure](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) es una nueva característica de inteligencia de seguridad integrada en hello servicio de base de datos de SQL Azure. Trabajar con hello toolearn, perfil del reloj y detectar actividades anómalas de la base de datos, detección de amenazas de base de datos de SQL Azure identifica la base de datos posibles amenazas toohello.

Los responsables de seguridad u otros administradores designados pueden recibir una notificación inmediata sobre las actividades sospechosas en las bases de datos cuando se producen. Cada notificación proporciona detalles de actividad sospechosa de Hola y recomienda cómo toofurther investigar y mitigar la amenaza de Hola.

Actualmente, Detección de amenazas de Azure SQL Database detecta posibles vulnerabilidades y ataques de inyección de SQL, así como patrones de acceso anómalos a las bases de datos.

Al recibir la notificación de correo electrónico de detección de amenazas, los usuarios son capaz de toonavigate y vista Hola auditoría pertinentes registros con vínculo profundo de hello en mail Hola que se abre un visor de auditoría o preconfigurado auditoría plantilla de Excel que muestra auditoría relevantes de Hola registros de aproximadamente hora de Hola de eventos sospechosos Hola según toohello siguiente:
-   Almacenamiento de auditoría de servidor/base de datos de hello con actividades de hello anómala de la base de datos

-   Tabla de almacenamiento de información de auditoría pertinentes que se usaron en tiempo de Hola Hola toowrite auditoría del registro de eventos

-   Registros de hello después horas desde que se produce el evento de Hola de auditoría.

-   Registros de auditoría con el Id. de evento similar en tiempo de Hola de evento de hello (opcional para algunos detectores)

Los detectores de amenaza de base de datos de SQL use uno de hello siguiendo las metodologías de detección:

-   **Una detección determinista:** detecta patrones sospechosos (en función de reglas) en las consultas de cliente SQL Hola que coinciden con los ataques conocidos. Esta metodología tiene la detección de alta y baja de falsos positivos, sin embargo limitadas cobertura porque se encuentra dentro de la categoría de Hola de "atómicas detecciones".

-   **Detección de comportamiento:** defectos de la actividad anómala, que es un comportamiento anómalo de base de datos de Hola que no se ha detectado durante el saludo últimos 30 días.  Un ejemplo de actividad anómala del cliente SQL puede ser un pico de inicios de sesión/consultas erróneas, gran volumen de datos que se va a extraer, consultas canónicas inusuales y base de datos de Hola de tooaccess desconocida usa las direcciones IP

### <a name="application-gateway-web-application-firewall"></a>Firewall de aplicaciones web de Application Gateway

[Servidor de aplicaciones de Web](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) es una característica de [puerta de enlace de aplicaciones de Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) que brinda protección de aplicaciones de tooweb que usan la puerta de enlace de aplicaciones estándar [Controldeentregadelaaplicación](https://kemptechnologies.com/in/application-delivery-controllers) funciones. Servidor de aplicaciones Web para ello, los protegen contra la mayoría de hello [OWASP top 10 vulnerabilidades web comunes](https://www.owasp.org/index.php/Top_10_2010-Main)

![Firewall de aplicaciones web de Application Gateway](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Protección contra la inyección de código SQL

-   Protección contra scripts entre sitios

-   Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos

-   Protección contra infracciones del protocolo HTTP

-   Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación

-   Prevención contra bots, rastreadores y escáneres

-   Detección de errores de configuración comunes en aplicaciones (es decir, Apache, IIS, etc.)

Configurar WAFS en puerta de enlace de aplicaciones proporciona Hola después tooyou ventaja:

-   Proteger la aplicación web frente a vulnerabilidades de web y ataques sin código de toobackend de modificación.

-   Proteger web varias aplicaciones en hello mismo tiempo detrás de una puerta de enlace de la aplicación. Puerta de enlace de aplicaciones admite el hospedaje de sitios Web de too20 detrás de una sola puerta de enlace que puede protegerse frente a ataques en Internet.

-   Supervisión de las aplicaciones web de cara a los ataques mediante un informe en tiempo real generado por los registros WAF de Application Gateway.

-   Ciertos controles de cumplimiento de normas requieren con conexión a toobe de dos puntos finales protegido por una solución WAFS todos los de internet. Mediante el uso de Application Gateway con WAF habilitado, puede satisfacer estos requisitos de cumplimiento.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>Detección de anomalías: API creada con Azure Machine Learning

La Detección de anomalías es una API creada con Azure Machine Learning que resulta útil para detectar distintos tipos de patrones anómalos en los datos de series temporales. Hola API asigna una anomalía de punto de datos de tooeach de puntuación de serie temporal de hello, que puede utilizarse para generar alertas, supervisión a través de paneles o se conecta con los sistemas de vales.

Hola [API de detección de anomalías](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) puede detectar Hola siguientes tipos de anomalías en los datos de series temporales:

-   **Cambios abruptos e interrupciones:** por ejemplo, al supervisar el número de hello del servicio de tooa de errores de inicio de sesión o de desprotecciones en un sitio de comercio electrónico, picos poco habituales o DIP podrían indicar ataques de seguridad o las interrupciones del servicio.

-   **Tendencias positivas y negativas:** al supervisar el uso de la memoria en computación, por ejemplo, reducir el tamaño de memoria libre, es indicativo de una posible pérdida de memoria; al supervisar la longitud de la cola del servicio, una tendencia al alza persistente puede indicar un problema de software subyacente.

-   **Nivel de cambios y los cambios de intervalo dinámico de valores:** por ejemplo, nivel de cambios en las latencias de un servicio después de que un servicio de actualización o reducir los niveles de excepciones después de la actualización puede ser interesante toomonitor.

aprendizaje automático de Hello basada en API permite:

-   **Detección sólida y flexible:** modelos de detección de anomalías de hello permiten a los usuarios tooconfigure configuraciones de sensibilidad y detectar anomalías entre conjuntos de datos de temporada y no estacionales. Los usuarios pueden ajustar Hola detección modelo toomake Hola la detección de anomalías API menos o necesita más sensible tootheir correspondiente. Esto significaría detectar hello más o menos anomalías visibles en datos con y sin patrones estacionales.

-   **La detección oportuna y escalable:** forma tradicional de Hola de supervisión con presentes umbrales definidos por el conocimiento de dominios expertos son costosos y no es escalable toomillions de conjuntos de datos que cambian dinámicamente. modelos de detección de anomalías de Hello en esta API se aprenden y se optimizan automáticamente los modelos de los datos históricos y en tiempo real.

-   **Detección proactiva y factible:** la detección de cambios lentos en las tendencias y los niveles se puede aplicar a la detección de anomalías tempranas. señales anómala temprano Hola detectadas pueden ser toodirect usado los seres humanos tooinvestigate y actuar en áreas con problemas Hola.  Por otra parte, además de este servicio de API de detección de anomalías se pueden desarrollar modelos de análisis de causa raíz y herramientas de alerta.

detección de anomalías de Hello API es una solución eficaz y eficiente para una amplia gama de escenarios, como el estado del servicio y KPI de supervisión, IoT, la supervisión del rendimiento y la supervisión del tráfico de red. Estos son algunos escenarios populares donde esta API puede resultar útil:
- Los departamentos de TI necesitan eventos tootrack de herramientas, código de error, el registro de uso y rendimiento (CPU, memoria etc.) de una manera oportuna.

-   Sitios de comercio en línea desea tootrack las actividades del cliente, las vistas de página, clics y así sucesivamente.

-   Las empresas de servicios desean tootrack consumo de agua, gas, electricidad y otros recursos.

-   Instalación/creación de servicios de administración desea toomonitor temperatura, humedad, tráfico y así sucesivamente.

-   IoT/fabricantes desea que los datos de sensor toouse en tiempo serie toomonitor el flujo de trabajo, la calidad y así sucesivamente.

-   Proveedores de servicios, como centros de llamadas, tendencia de petición de servicio toomonitor, volumen de incidentes, deben esperan longitud de la cola y así sucesivamente.

-   Grupos de análisis de negocios desee toomonitor empresarial de KPI (por ejemplo, el volumen de ventas, mensajes de cliente, precios) anómalo movimiento en tiempo real.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) es un componente esencial de la pila de seguridad de la nube de Microsoft de Hola. Es una solución completa, que puede ayudar a su organización como mover tootake provecho de compromiso Hola de aplicaciones en la nube, pero le mantienen en el control a través de una mejor visibilidad de actividad. También ayuda a aumentar la protección de Hola de datos críticos en todas las aplicaciones de nube.

Con herramientas que le ayudan a descubrir instantáneas TI, evaluar el riesgo, aplicar directivas, investigar actividades y detener amenazas, su organización puede transferir con más seguridad toohello en la nube sin perder el control de datos críticos.

<table style="width:100%">
 <tr>
   <td>Descubra</td>
   <td>Descubra las zonas oscuras de TI con Cloud App Security. Gane visibilidad al descubrir aplicaciones, actividades, usuarios, datos y archivos del entorno de la nube. Detectar las aplicaciones de terceros que están conectadas en la nube tooyour.</td>
 </tr>
 <tr>
   <td>Investigación</td>
   <td>Investigar las aplicaciones de nube mediante herramientas forenses de nube toodeep inmersión en las aplicaciones de riesgo, los archivos en la red y usuarios específicos. Identificar patrones en datos de hello recopilados de la nube. Generar informes toomonitor en la nube.</td>

 </tr>
 <tr>
   <td>Control</td>
   <td>Mitigar el riesgo al establecer directivas y alertas tooachieve máximo control sobre el tráfico de red en la nube. Usar Cloud App Security toomigrate su toosafe de los usuarios, alternativas de aplicaciones de nube autorizadas.</td>

 </tr>
 <tr>
   <td>Protección</td>
   <td>Usar Cloud App Security toosanction o las aplicaciones, aplicar la prevención de pérdida de datos, permisos de control y de uso compartido y generar alertas e informes personalizados.</td>

 </tr>
 <tr>
   <td>Control</td>
   <td>Mitigar el riesgo al establecer directivas y alertas tooachieve máximo control sobre el tráfico de red en la nube. Usar Cloud App Security toomigrate su toosafe de los usuarios, alternativas de aplicaciones de nube autorizadas.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security integra visibilidad con la nube gracias a lo siguiente:

-   Usando Cloud Discovery toomap identificar el entorno de nube y Hola aplicaciones de nube que su organización está usando.


-   La prohibición y autorización de aplicaciones en la nube.



-   El uso de conectores de aplicaciones fáciles de implementar que aprovechan las ventajas de las API de proveedor, para ganar visibilidad y gobierno de las aplicaciones a las que se conecte.

-   La ayuda para mantener el control constante mediante la configuración y posterior ajuste permanente de las directivas.

Sobre la recopilación de datos de estos orígenes, Cloud App Security ejecuta un sofisticado análisis sobre datos Hola. Inmediatamente, le avisa tooanomalous actividades y le ofrece visibilidad en el entorno de nube. Puede configurar una directiva de seguridad de la aplicación de nube y usarlo tooprotect todo en el entorno de nube.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Funcionalidades ATD de terceros a través de Azure Marketplace

### <a name="web-application-firewall"></a>Firewall de aplicaciones web

El firewall de aplicaciones web inspecciona el tráfico web entrante y bloquea las inyecciones de SQL, el scripting entre sitios, las cargas de malware y DDoS de aplicación, así como otros ataques dirigidos a las aplicaciones web. También examina las respuestas de Hola de servidores web back-end de Hola de prevención de pérdida de datos (DLP). motor de control de acceso integrado Hola habilita las directivas de control de acceso granular de los administradores toocreate para autenticación, autorización y contabilidad (AAA), que proporciona autenticación sólida de las organizaciones y control de usuario.

**Aspectos destacados:**
-   Detecta y bloquea las inyecciones de SQL, el scripting entre sitios, las cargas de malware, el DDoS de aplicación y cualquier otro ataque contra la aplicación.

-   Autenticación y control de acceso.

-   Analiza el tráfico saliente toodetect confidencial datos y puede enmascarar o bloqueando la información de Hola se filtren.

-   Acelera la entrega de Hola de contenido de aplicación web, con capacidades como almacenamiento en caché, la compresión y otras optimizaciones de tráfico.

A continuación se presentan unos ejemplos de firewall de aplicaciones web disponibles en Azure Marketplace:

[Firewall de aplicación Web de Barracuda, servidor de aplicaciones de Web Virtual de Brocade (Brocade vWAF), Imperva SecureSphere & hello ThreatSTOP IP Firewall.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Pasos siguientes

- [Funcionalidades de detección de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Capacidades de detección avanzada del centro de seguridad de Azure le ayuda a amenazas active tooidentify dirige a los recursos de Microsoft Azure y proporciona con visión Hola había toorespond rápidamente.

- [Detección de amenazas de Azure SQL Database](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Detección de amenazas de base de datos de SQL Azure ayudó a enfrentar sus preocupaciones acerca de la base de datos posibles amenazas tootheir.
