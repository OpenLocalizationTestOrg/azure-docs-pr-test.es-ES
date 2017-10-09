---
title: aaaIntroduction tooAzure seguridad | Documentos de Microsoft
description: "Aprenda acerca de la seguridad de Azure, sus servicios y cómo funciona."
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
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Introducción tooAzure seguridad
## <a name="overview"></a>Información general
Somos conscientes de que la seguridad es trabajo en la nube de Hola y la importancia que tiene que buscar información precisa y oportuna sobre la seguridad de Azure. Uno de hello mejor motivos toouse Azure para las aplicaciones y servicios es tootake aprovechar su amplia gama de capacidades y herramientas de seguridad. Estas herramientas y capacidades que esté soluciones seguras toocreate posibles en la plataforma Windows Azure segura de Hola. Microsoft Azure proporciona confidencialidad, integridad y disponibilidad para los datos del cliente, al mismo tiempo que hace posible una responsabilidad transparente.

toohelp le entender mejor la colección de Hola de controles de seguridad que se implementa en Microsoft Azure del cliente de Hola y las operaciones de Microsoft desde las perspectivas del, estas notas del producto "Introducción tooAzure seguridad", se escribe tooprovide un información completa sobre seguridad de hello disponible con Microsoft Azure.

### <a name="azure-platform"></a>Plataforma Azure
Azure es una plataforma de servicios en la nube pública que admite una amplia selección de sistemas operativos, lenguajes de programación, plataformas, herramientas, bases de datos y dispositivos. Puede ejecutar contenedores de Linux con integración de Docker, compilar aplicaciones con JavaScript, Python, .NET, PHP, Java, Node.js y crear back-ends para dispositivos iOS, Android y Windows.

Servicios de nube pública de Azure admiten Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza. Al compilar en, o migrar los activos de TI a, un proveedor de servicios de nube pública depende de tooprotect de capacidades de la organización sus aplicaciones y datos con controles de Hola y de servicios de hello proporcionan seguridad de hello toomanage de basados en la nube activos.

Diseño de la infraestructura de Azure de tooapplications de instalación para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus requisitos de seguridad.

Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones de su organización. Este documento explica cómo las funcionalidades de seguridad de Azure pueden ayudarle a cumplir estos requisitos.

> [!Note]
> Hola nos centramos en este documento está en controles orientado al cliente que puede usar toocustomize y aumentar la seguridad de las aplicaciones y servicios.
>
> Se proporcionan alguna información de introducción, pero para obtener información detallada sobre cómo Microsoft protege Hola plataforma Windows Azure, consulte la información proporcionada en hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Descripción breve
Inicialmente, migraciones de nube pública se controlan mediante tooinnovate de ahorro y la agilidad de costo. Durante un tiempo, se consideró la seguridad como una preocupación importante e incluso un elemento disuasorio para la migración a la nube pública. Sin embargo, seguridad de nube pública ha pasado desde un principal preocupación tooone de controladores de hello para la migración de nube. análisis razonado de Hello respecto a esto es capacidad óptima de Hola de aplicaciones de tooprotect de proveedores de servicios de nube pública de gran tamaño y los datos de Hola de activos en la nube.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus necesidades de seguridad. Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables ellos para que puedan personalizar requisitos únicos Hola de seguridad toomeet de su toomeet implementaciones el departamento de TI controlar las directivas y seguirán tooexternal normativas.

Este documento describe toosecurity de enfoque de Microsoft en la plataforma de nube de Microsoft Azure hello:
* Características de seguridad implementadas por toosecure Hola infraestructura de Azure, los datos del cliente y aplicaciones de Microsoft.
* Azure seguridad de servicios y características tooyou disponible toomanage hello seguridad de servicios de Hola y los datos dentro de las suscripciones de Azure.

## <a name="summary-azure-security-capabilities"></a>Resumen de las funcionalidades de seguridad de Azure
siguiente de la tabla de Hello proporciona una breve descripción de las características de seguridad de hello implementada por Microsoft hello toosecure infraestructura de Azure, los datos del cliente y aplicaciones seguras.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Seguridad implementa características tooSecure Hola plataforma de Azure:
Hola se enumeran características siguientes son funciones que puede revisar la garantía de hello tooprovide ese Hola que plataforma de Azure se administra de forma segura. Se han proporcionado vínculos para que vea con más detalle cómo Microsoft aborda las cuestiones de confianza del cliente en cuatro áreas: Plataforma segura, Privacidad y controles, Cumplimiento normativo y Transparencia.


| [Plataforma segura](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Privacidad y controles](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Cumplimiento normativo](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Transparencia](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Ciclo de desarrollo de seguridad](https://www.microsoft.com/en-us/sdl/), auditorías internas | [Administrar los datos de todo el tiempo Hola](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Centro de confianza](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Cómo Microsoft protege los datos de clientes en servicios de Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Entrenamiento de seguridad obligatorio, comprobación de antecedentes](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Control en la ubicación de los datos](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Centro de controles comunes](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Cómo Microsoft administra la ubicación de datos en los servicios de Azure](http://azuredatacentermap.azurewebsites.net/)|
| [Pruebas de penetración](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [detección de intrusiones, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [auditorías y registro](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Proporcionar acceso a datos en sus propios términos](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [lista de comprobación de diligencia vencimiento de nube servicios Hola](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Personas de Microsoft que pueden acceder a sus datos y bajo qué términos](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Centro de datos de vanguardia](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), seguridad física, [red segura](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Responde toolaw cumplimiento](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Cumplimiento por servicio, ubicación y sector](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Cómo Microsoft protege los datos de clientes en servicios de Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Respuesta a incidentes de seguridad](http://aka.ms/SecurityResponsepaper), [responsabilidad compartida](http://aka.ms/sharedresponsibility) |[Rigurosos estándares de privacidad](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Revisión de la certificación para servicios de Azure, centro de transparencia](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Características de seguridad ofrecidas por Azure tooSecure datos y aplicación
Según el modelo de servicio de nube de hello, no hay variable responsabilidad de quién es responsable de administrar la seguridad de Hola de hello aplicación o servicio. Existen capacidades en hello tooassist de plataforma de Azure que satisfacer estas responsabilidades por características integradas y por las soluciones que se pueden implementar en una suscripción de Azure de asociados.

capacidades integradas de Hola se organizan en las áreas funcionales de seis (6): las operaciones, aplicaciones, almacenamiento, red, proceso e identidad. Se proporcionan detalles adicionales sobre las características de Hola y capacidades disponibles en hello plataforma de Azure en estas áreas de seis (6) a través de la información de resumen.

## <a name="operations"></a>Operaciones
En esta sección se proporciona información adicional acerca de características fundamentales para las operaciones de seguridad y un resumen de estas funcionalidades.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Panel Seguridad y auditoría de Operations Management Suite
Hola [solución OMS seguridad y auditoría](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) proporciona una vista completa de su organización postura de seguridad de TI con [consultas de búsqueda integradas](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) para problemas importantes que requieren su atención. Hola [seguridad y auditoría](https://technet.microsoft.com/library/mt484091.aspx) panel es la pantalla principal de Hola para todo lo relacionado con toosecurity de OMS. Proporciona una visión de alto nivel sobre Hola estado de seguridad de los equipos. Hola capacidad tooview también incluye todos los eventos de hello últimas 24 horas, 7 días, o cualquier otro período de tiempo personalizado.

Además, puede configurar seguridad de OMS y cumplimiento demasiado[realizar automáticamente acciones específicas](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) cuando se detecta un evento específico.

### <a name="azure-resource-manager"></a>Administrador de recursos de Azure
[El Administrador de recursos Azure ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) permite toowork con recursos de hello en la solución como un grupo. Puede implementar, actualizar o eliminar todos los recursos de hello para la solución en una única operación coordinada. Use una [plantilla de Azure Resource Manager](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) para la implementación; esta puede funcionar en distintos entornos, como producción, pruebas y ensayo. Administrador de recursos proporciona seguridad, auditoría y etiquetado características toohelp administrar sus recursos después de la implementación.

Las implementaciones basadas en plantillas de Azure Resource Manager ayudar a mejorar la seguridad de Hola de soluciones implementadas en Azure porque controlar la configuración de seguridad estándar y puede integrarse en implementaciones basadas en plantillas estándar. Esto reduce el riesgo de Hola de errores de configuración de seguridad que puede tener lugar durante las implementaciones manuales.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) es un servicio de Application Performance Management (APM) extensible para desarrolladores web. Con Application Insights, puede supervisar sus aplicaciones web en directo y detectar automáticamente anomalías de rendimiento. Incluye análisis eficaces herramientas toohelp que diagnosticar problemas y toounderstand lleva a cabo lo que los usuarios con sus aplicaciones. Supervisa la aplicación se está ejecutando, durante las pruebas y después de haber publicado o implementarla todo el tiempo Hola.

Visión de la aplicación crea gráficos y tablas que muestran, por ejemplo, qué horas del día en que se obtiene la mayoría de los usuarios, es la aplicación siga respondiendo hello y también que cualquier externo ofrece servicios a los que depende.

Si no hay bloqueos, errores o problemas de rendimiento, puede buscar a través de los datos de telemetría de hello en causa de hello toodiagnose de detalle. Y servicio de hello envía mensajes de correo electrónico si hay algún cambio en la disponibilidad de Hola y el rendimiento de la aplicación. Una perspectiva de aplicación, por tanto, se convierte en una herramienta de seguridad muy valiosa porque ayuda con la disponibilidad de hello en hello confidencialidad, integridad y tres de seguridad de disponibilidad.

### <a name="azure-monitor"></a>Azure Monitor
[Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) ofrece visualización, consulta, enrutamiento, alertas, escalado automático y automatización en datos tanto de hello infraestructura de Azure ([registro de actividad](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) y cada recurso de Azure individual ([ Registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Puede usar Monitor de Azure tooalert en eventos relacionados con la seguridad que se generan en registros de Azure.

### <a name="log-analytics"></a>Log Analytics
[Análisis de registros](https://azure.microsoft.com/documentation/services/log-analytics/) forma parte de [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) : proporciona una solución de administración de TI locales y de infraestructura en la nube de terceros (por ejemplo, AWS) además tooAzure recursos. Se pueden enrutar datos desde el Monitor de Azure directamente tooLog análisis para que pueda ver registros y las métricas para todo el entorno en un solo lugar.

Análisis de registros pueden ser una herramienta útil en forense y otros análisis de seguridad, tal y como herramienta de hello permite tooquickly buscar a través de grandes cantidades de entradas relacionadas con la seguridad con un enfoque de consulta flexible. Además, los [registros de proxy y firewall locales se pueden exportar a Azure y poner a disposición para su análisis con Log Analytics.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[Asistente de Azure](https://docs.microsoft.com/azure/advisor/) es un consultor de nube personalizado que le ayude a toooptimize las implementaciones de Azure. Analiza la telemetría de uso y configuración de los recursos y, A continuación, recomienda soluciones toohelp mejorar hello [rendimiento](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [seguridad](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), y [alta disponibilidad](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) de sus recursos al buscar oportunidades demasiado[reducir Azure general dedican](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Azure Advisor proporciona recomendaciones de seguridad, que pueden mejorar de forma notable la posición general de seguridad para las soluciones que se implementan en Azure. Estas recomendaciones se extraen del análisis de seguridad realizado por [Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-intro)

### <a name="azure-security-center"></a>Azure Security Center
[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Hola de ayuda a evitar, detectar y responder toothreats con una mayor visibilidad de y control sobre la seguridad de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Además, Azure Security Center le ayuda con las operaciones de seguridad, al proporcionarle un único panel donde aparecen alertas y recomendaciones para las que puede actuar de inmediato. A menudo, puede corregir los problemas con un solo clic dentro de la consola de Azure Security Center Hola.
## <a name="applications"></a>Aplicaciones
sección de Hello proporciona información adicional con respecto a las características claves de aplicación seguridad e información de resumen acerca de estas capacidades.

### <a name="web-application-vulnerability-scanning"></a>Examen de vulnerabilidades para aplicaciones web
Iniciaba una de hello tooget de maneras más sencilla con las pruebas en busca de vulnerabilidades en su [aplicación de servicio de aplicaciones](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) es hello toouse [integración con Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform exploración en de vulnerabilidades de un solo clic la aplicación. Puede ver los resultados de pruebas de hello en un informe fácil de entender y obtenga información acerca de cómo toofix cada vulnerabilidad con instrucciones paso a paso.

### <a name="penetration-testing"></a>Pruebas de penetración
Si lo prefiere tooperform su propio penetración pruebas o desea toouse otro conjunto de escáner o proveedor, deberá seguir hello [proceso de aprobación de prueba de penetración Azure](https://security-forms.azure.com/penetration-testing/terms) y obtener la aprobación previa tooperform Hola deseado de penetración pruebas.

### <a name="web-application-firewall"></a>Firewall de aplicaciones web
Hola a servidor de aplicaciones web (WAFS) en [puerta de enlace de aplicaciones de Azure](https://azure.microsoft.com/services/application-gateway/) ayuda a protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL y ataques XSS, secuestro de sesión. Viene preconfigurado con protección de amenazas identificadas por hello [Abrir Web aplicación seguridad proyecto (OWASP) como Hola top 10 vulnerabilidades comunes](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticación y autorización en el Servicio de aplicaciones de Azure
[Aplicación servicio de autenticación / autorización](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) es una característica que proporciona una manera para su toosign de aplicación en los usuarios para que no tengan código toochange de backend de la aplicación hello. Proporciona una manera sencilla de tooprotect la aplicación y el trabajo con datos por usuario.

### <a name="layered-security-architecture"></a>Arquitectura de seguridad por niveles
Como los [entornos de App Service](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) proporcionan un entorno en tiempo de ejecución aislado que está implementado en una [instancia de Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), los desarrolladores pueden crear una arquitectura de seguridad por niveles que proporcione diferentes niveles de acceso a la red para cada capa de aplicación. Un deseo común es toohide API back-end de acceso general a Internet y solo se permiten toobe API llama a las aplicaciones web de nivel superior. [Grupos de seguridad (NSG) de red](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) puede utilizarse en subredes de red Virtual de Azure que contiene aplicaciones de tooAPI de acceso público de toorestrict entornos del servicio de aplicación.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Diagnóstico del servidor web y diagnóstico de aplicaciones
Aplicaciones de servicio de aplicaciones web proporcionan funcionalidad de diagnóstico para registrar información de servidor web de Hola y de aplicación web de hello. De forma lógica, estos diagnósticos se dividen en [diagnósticos del servidor web](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) y [diagnóstico de aplicaciones](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). El servidor web incluye dos avances importantes para el diagnóstico y la solución de problemas de sitios y aplicaciones.

la primera característica nueva de Hello es información de estado en tiempo real sobre los grupos de aplicaciones, los procesos de trabajo, sitios, dominios de aplicación y solicitudes en ejecución. ventajas nuevas segundo Hola se Hola eventos de seguimiento detallado que realizan el seguimiento de una solicitud a lo largo del proceso de solicitud y respuesta de hello completo.

colección de hello tooenable de estos eventos de seguimiento, IIS 7 puede ser registros de seguimiento completa captura tooautomatically configurado, en formato XML, para cualquier solicitud determinada en función de los códigos de respuesta de error o el tiempo transcurrido.

#### <a name="web-server-diagnostics"></a>Diagnósticos del servidor web
Puede habilitar o deshabilitar Hola siguientes tipos de registros:

-   Registro de errores detallado: registra información detallada de errores para códigos de estado HTTP que indican un problema (código de estado 400 o superior). Esto puede contener información que puede ayudar a determinar por qué servidor de hello devolvió el código de error de Hola.

-   Error del seguimiento de solicitud - información detallada sobre las solicitudes con error, incluidos un seguimiento de hello IIS componentes utilizados tooprocess Hola solicitud y la hora de hello realizada en cada componente. Esto puede resultar útil si está tratando de rendimiento del sitio tooincrease o aislar la causa de que un toobe específico de error HTTP devuelto.

-   Registro del servidor - obtener información acerca de las transacciones HTTP mediante el formato de archivo de registro extendido W3C de Hola de Web. Esto es útil al determinar las métricas generales de sitio como el número de Hola de las solicitudes administradas o cuántas solicitudes provienen de una dirección IP específica.

#### <a name="application-diagnostics"></a>diagnósticos de la aplicación
[Diagnósticos de la aplicación](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) le permite obtener información de toocapture generado por una aplicación web. Las aplicaciones de ASP.NET pueden usar hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) el registro de diagnósticos de aplicación de clase toolog información toohello. En Application Diagnostics, hay dos tipos principales de eventos, las relacionadas con el rendimiento de tooapplication y los relacionados con errores y errores de tooapplication. Hello errores se pueden dividir en problemas de conectividad, seguridad y de errores. Los problemas de errores son problema tooa normalmente relacionadas con código de la aplicación hello.

En Diagnóstico de aplicaciones, puede ver los eventos agrupados de las siguientes maneras:

-   Todos (muestra todos los eventos)
-   Errores de aplicación (muestra eventos de excepción)
-   Rendimiento (muestra eventos de rendimiento)

## <a name="storage"></a>Storage
sección de Hello proporciona información adicional con respecto a las características claves de almacenamiento de Azure seguridad e información de resumen acerca de estas capacidades.

### <a name="role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC)
Puede proteger su cuenta de almacenamiento con el control de acceso basado en rol (RBAC). Restringir el acceso en función de hello [necesita tooknow](https://en.wikipedia.org/wiki/Need_to_know) y [privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principios de seguridad es fundamental para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos. Estos derechos de acceso se conceden mediante la asignación de hello adecuado RBAC rol toogroups y las aplicaciones en un ámbito determinado. Puede usar [funciones integradas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), como colaborador de la cuenta de almacenamiento, tooassign privilegios toousers. Obtener acceso a claves de almacenamiento de toohello para una cuenta de almacenamiento mediante hello [Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) modelo puede controlarse a través del Control de acceso basado en roles (RBAC).

### <a name="shared-access-signature"></a>Firma de acceso compartido
A [firma de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) proporciona acceso delegado tooresources en su cuenta de almacenamiento. Hola SAS significa que puede conceder a que un cliente durante un período especificado y con un conjunto de permisos especificado limitados tooobjects permisos en su cuenta de almacenamiento. Puede conceder estos permisos limitados sin necesidad de tooshare las claves de acceso de cuenta.

### <a name="encryption-in-transit"></a>Cifrado en tránsito
Cifrado en tránsito es un mecanismo para proteger datos cuando se transmiten a través de redes. Con Azure Storage, puede proteger los datos mediante:
-   [Cifrado de nivel de transporte](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), como HTTPS para transferir datos a Almacenamiento de Azure o desde este servicio.

-   [Cifrado en el cable](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), como el [cifrado SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) para [recursos compartidos de Azure File](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   Cifrado en el cliente, datos de Hola de tooencrypt antes de que se transfieran en el almacenamiento y datos de hello toodecrypt después de que se transfiere fuera de almacenamiento.

### <a name="encryption-at-rest"></a>Cifrado en reposo
Para muchas organizaciones, el cifrado de los datos en reposo es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. Hay tres características de seguridad del almacenamiento de Azure que proporcionan cifrado de datos "en reposo":

-   [Cifrado de almacenamiento del servicio](https://docs.microsoft.com/azure/storage/storage-service-encryption) permite que el servicio de almacenamiento de hello cifrar automáticamente los datos al escribir tooAzure almacenamiento de toorequest.

-   [Cifrado en el cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) también proporciona características de Hola de cifrado en reposo.

-   [Cifrado del disco Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) permite tooencrypt discos de hello OS y discos de datos usados por una máquina virtual de IaaS.

### <a name="storage-analytics"></a>Storage Analytics
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Puede utilizar este solicitudes de tootrace de datos, analizar las tendencias de uso y diagnosticar problemas con su cuenta de almacenamiento. Análisis de almacenamiento registra información detallada acerca del servicio de almacenamiento de tooa de solicitudes correctas e incorrectas. Esta información puede ser problemas de toodiagnose con un servicio de almacenamiento y las solicitudes individuales de toomonitor usado. Las solicitudes se registran en función de la mejor opción. se registra los siguientes tipos de solicitudes autenticadas de Hello:
-   Solicitudes correctas

-   Solicitudes erróneas, incluyendo errores de tiempo de espera, de limitación, de red, de autorización, etc

-   Solicitudes que utilizan una firma de acceso compartido (SAS), incluyendo las solicitudes correctas y las erróneas

-   Datos de tooanalytics de solicitudes.

### <a name="enabling-browser-based-clients-using-cors"></a>Habilitación de clientes basados en explorador mediante CORS
[Uso compartido de recursos entre orígenes (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) es un mecanismo que permite a dominios toogive cada uno de los otros permisos para tener acceso a recursos de los demás. Hola agente de usuario envía tooensure encabezados adicionales que el código de JavaScript de hello cargado desde un determinado dominio está permitido tooaccess recursos estén ubicados en otro dominio. dominio de este último Hello, a continuación, responde con encabezados adicionales permitir o denegar el acceso al dominio original de hello tooits recursos.

Ahora admiten CORS de servicios de almacenamiento de Azure para que una vez establecidas las reglas de CORS de hello para el servicio de hello, una solicitud autenticada correctamente realizada en el servicio de Hola desde un dominio diferente sea evaluado toodetermine si se permite según las reglas de toohello que tiene especificado.
## <a name="networking"></a>Redes
sección de Hello proporciona información adicional con respecto a las características claves de red de Azure seguridad e información de resumen acerca de estas capacidades.

### <a name="network-layer-controls"></a>Controles de nivel de red
Control de acceso de red es el acto de Hola para limitar el tooand de conectividad de dispositivos específicos o subredes y representa Hola principales de seguridad de red. objetivo de Hola de control de acceso de red es toomake seguro de que las máquinas virtuales y servicios se tooonly puede tener acceso a los usuarios y dispositivos toowhich gusto accesible.

#### <a name="network-security-groups"></a>Grupos de seguridad de red
A [grupo de seguridad de red (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) es un paquete con estado básico filtrado de firewall y permite toocontrol acceso tomando como base un [5-tupla](https://www.techopedia.com/definition/28190/5-tuple). Los NSG no proporcionan inspección de nivel de aplicación ni controles de acceso autenticados. Se pueden usar tráfico toocontrol mover entre subredes dentro de una red Virtual de Azure y el tráfico entre una red Virtual de Azure y Hola Internet.

#### <a name="route-control-and-forced-tunneling"></a>Control de ruta y tunelización forzada
comportamiento de enrutamiento toocontrol de Hello capacidad en las redes virtuales de Azure es una función de control de seguridad y el acceso de red críticos. Por ejemplo, si desea toomake seguro de que todos los tooand de tráfico de red Virtual de Azure pasa ese dispositivo de seguridad virtual, necesita toobe capaz de toocontrol y personalizar el comportamiento de enrutamiento. Para ello, puede configurar rutas definidas por el usuario en Azure.

[Las rutas definidas por el usuario](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) permiten toocustomize las rutas de acceso entrantes y salientes para el tráfico de mover dentro y fuera de las máquinas virtuales individuales o subredes tooinsure Hola más segura posible de ruta. [La tunelización forzada](https://www.petri.com/azure-forced-tunneling) es un mecanismo que puede utilizar tooensure que los servicios no están permitidas tooinitiate una toodevices de conexión en hello Internet.

Esto es diferente de la que se pueda tooaccept las conexiones entrantes y, a continuación, responde toothem. Servidores front-end web necesitan toorespond toorequests desde hosts de Internet y, por lo que se permite el tráfico de origen de Internet entrante toothese servidores web y hello web puede responder.

La tunelización forzada es tooforce utilizadas el tráfico saliente toohello Internet toogo a través de servidores proxy de seguridad local y firewalls.

#### <a name="virtual-network-security-appliances"></a>Dispositivos de seguridad de red virtual
Mientras que los grupos de seguridad de red, las rutas definidas por el usuario y la tunelización forzada proporcionan un nivel de seguridad en los niveles de red y el transporte de Hola de hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), puede haber ocasiones cuando desee tooenable seguridad en los niveles superiores de pila de Hola. Puede acceder a estas características mejoradas de seguridad de red mediante una solución de dispositivo de seguridad de red de asociados de Azure. Puede encontrar Hola soluciones de seguridad de red de asociado de Azure más recientes visitando hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) y busque "seguridad" y "seguridad de red".

### <a name="azure-virtual-network"></a>Red virtual

Una red virtual (VNet) es una representación de su propia red en la nube de Hola. Es un aislamiento lógico de hello Azure fabric dedicado tooyour la suscripción de red. Puede controlar completamente bloques de direcciones IP de hello, configuración de DNS, las directivas de seguridad y tablas de rutas dentro de esta red. Puede segmentar la red virtual en subredes y colocar máquinas virtuales de IaaS de Azure o [servicios en la nube (instancias de rol de PaaS)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) en instancias de Azure Virtual Network.

Además, puede conectarse hello tooyour local red virtual con uno de hello [opciones de conectividad](https://docs.microsoft.com/azure/vpn-gateway/) disponibles en Azure. Básicamente, puede expandir su tooAzure de red, con control total sobre los bloques de direcciones IP con la ventaja de Hola de escala empresarial que proporciona Azure.

Las redes de Azure admiten diversos escenarios de acceso remoto seguro. Algunos son:

-   [Conectar estaciones de trabajo individuales tooan red Virtual de Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [Conectar tooan de red local red Virtual de Azure con una VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Conectar tooan de red local red Virtual de Azure con un vínculo WAN dedicado](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Conectar redes virtuales de Azure tooeach otros](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN Gateway
toosend el tráfico de red entre la red Virtual de Azure y el sitio local, debe crear una puerta de enlace VPN para la red Virtual de Azure. Una [puerta de enlace de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) es un tipo de puerta de enlace de red virtual que envía tráfico cifrado a través de una conexión pública. También puede utilizar el tráfico de toosend de puertas de enlace VPN entre redes virtuales de Azure a través de hello tejido de red de Azure.

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) es un vínculo WAN dedicado que le permite ampliar sus redes locales en hello nube de Microsoft a través de una conexión privada dedicada que se realiza mediante un proveedor de conectividad.

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

Con ExpressRoute, puede establecer conexiones tooMicrosoft servicios en la nube, como Microsoft Azure, Office 365 y CRM Online. La conectividad puede ser desde una red de conectividad universal (IP VPN), una red Ethernet de punto a punto, o una conexión cruzada virtual a través de un proveedor de conectividad en una instalación de ubicación compartida.

Las conexiones ExpressRoute no pasan por Hola Internet pública y, por tanto, se puede considerar más segura que las soluciones basadas en VPN. Esto permite toooffer las conexiones de ExpressRoute, más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola.


### <a name="application-gateway"></a>Application Gateway
Microsoft [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) cuenta con un [controlador de entrega de aplicaciones (ADC)](https://en.wikipedia.org/wiki/Application_delivery_controller) que se ofrece como servicio y que proporciona varias funcionalidades de equilibrio de carga de nivel 7 para la aplicación.

![Application Gateway](./media/azure-security/azure-security-fig2.png)

Permite productividad de granja de servidores web toooptimize mediante la descarga de toohello de finalización de SSL intensivo de CPU puerta de enlace de aplicaciones (también conocido como "La descarga de SSL" o "Protocolo de puente SSL"). También proporciona otras capacidades de enrutamiento de nivel 7 incluidos distribución por turnos de tráfico entrante, afinidad de sesión basado en cookies, enrutamiento basado en la ruta de acceso de direcciones URL y toohost de capacidad de hello varios sitios Web detrás de una sola puerta de enlace de la aplicación. Azure Application Gateway es un equilibrador de carga de nivel 7.

Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.

La aplicación proporciona numerosas características de controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga [SSL (Capa de sockets seguros)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell), los sondeos personalizados sobre el estado y la compatibilidad con sitios múltiples.

### <a name="web-application-firewall"></a>Firewall de aplicaciones web
Servidor de aplicaciones Web es una característica de [puerta de enlace de aplicaciones de Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) que brinda protección de aplicaciones de tooweb que usan la puerta de enlace de aplicaciones para las funciones estándar de Control de entrega de aplicaciones (ADC). Para ello, el servidor de aplicaciones Web los protegen contra la mayoría de hello OWASP top 10 web las vulnerabilidades más comunes.

![Firewall de aplicaciones web](./media/azure-security/azure-security-fig1.png)

-   Protección contra la inyección de código SQL

-   Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos

-   Protección contra infracciones del protocolo HTTP

-   Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación

-   Prevención contra bots, rastreadores y escáneres

-   Detección de errores de configuración comunes en aplicaciones (es decir, Apache, IIS, etc.)


Un tooprotect de firewall de aplicación web centralizada frente a ataques de web simplifica mucho la administración de seguridad y proporciona mejor seguridad toohello aplicación frente a amenazas de Hola de intrusiones. Una solución WAFS también puedan reaccionar de amenaza para la seguridad tooa más rápido por una vulnerabilidad conocida en una ubicación central en comparación con la protección de cada una de las aplicaciones web individuales de la aplicación de revisiones. Aplicación existente, las puertas de enlace se puede convertir tooan la puerta de enlace de aplicaciones con el servidor de aplicaciones web fácilmente.
### <a name="traffic-manager"></a>Administrador de tráfico
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) permite la distribución de hello toocontrol del tráfico de usuario para los extremos de servicio en distintos centros de datos. Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube. También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure. El Administrador de tráfico usa Hola toodirect cliente solicita toohello extremo más adecuado en función de sistema de nombres de dominio (DNS) un [método de enrutamiento del tráfico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) y estado de Hola de extremos de Hola.

Traffic Manager proporciona una gama de enrutamiento del tráfico necesidades de distintas aplicaciones de métodos toosuit, estado del extremo [supervisión](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)y la conmutación automática por error. El Administrador de tráfico es resistente toofailure, incluidos los errores de Hola de toda una región de Azure.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[El equilibrador de carga Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) entrega tooyour aplicaciones de alta disponibilidad y rendimiento de red. Se trata de un equilibrador de carga de nivel 4 (TCP y UDP) que distribuye el tráfico entrante entre las instancias de servicio correctas de los servicios que se definen en un conjunto de carga equilibrada. Azure Load Balancer puede configurarse para lo siguiente:

-   La carga de máquinas de toovirtual de Internet entrantes de equilibrar el tráfico. Esta configuración se conoce como " [equilibrio de carga con conexión a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)".

-   Equilibrar la carga del tráfico entre máquinas virtuales de una red virtual, entre máquinas virtuales de servicios en la nube o entre equipos locales y máquinas virtuales de una red virtual entre entornos locales. Esta configuración se conoce como " [equilibrio de carga interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)". 

- Reenvíe el tráfico externo tooa determinada máquina virtual

### <a name="internal-dns"></a>DNS interno
Puede administrar Hola lista de servidores DNS que usa en una red virtual en el Portal de administración de Hola o en el archivo de configuración de red de Hola. Cliente puede agregar los servidores DNS de too12 para cada red virtual. Al especificar servidores DNS, es importante tooverify lista de servidores DNS del cliente en el orden correcto de hello para el entorno del cliente. Las listas de servidores DNS no funcionan con Round Robin. Se utilizan en el orden de Hola que se especifican. Si Hola primer servidor DNS en la lista de Hola es capaz de toobe alcanzado, el cliente de hello usa ese servidor DNS independientemente de si servidor DNS de hello funciona correctamente o no. Hola toochange orden del servidor DNS para la red virtual del cliente, quitar servidores DNS de Hola de lista de Hola y agregarlos en orden de Hola que el cliente desea. DNS es compatible con los aspectos de disponibilidad de Hola de tres de seguridad de "CIA" Hola.

### <a name="azure-dns"></a>DNS de Azure
Hola [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), o DNS, es responsable de traducir (o la resolución de) un sitio Web o servicio name tooits dirección IP. [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) es un servicio de hospedaje para dominios DNS que permite resolver nombres mediante la infraestructura de Microsoft Azure. Mediante el hospedaje de los dominios en Azure, puede administrar su DNS los registros mediante Hola mismas credenciales, API, herramientas y facturación como los servicios de Azure. DNS es compatible con los aspectos de disponibilidad de Hola de tres de seguridad de "CIA" Hola.
### <a name="log-analytics-nsgs"></a>Grupos de seguridad de red de Log Analytics
Puede habilitar Hola siguientes categorías de registro de diagnóstico para los NSG:
-   Evento: Contiene entradas para lo NSG son reglas tooVMs aplicados y roles de una instancia en función de la dirección MAC. estado de Hola para que estas reglas se recopila cada 60 segundos.

-   Contador de reglas: contiene las entradas de cuántas veces cada regla NSG es toodeny aplicado o permitir el tráfico.

### <a name="azure-security-center"></a>Azure Security Center
Centro de seguridad le ayuda a evitar, detectar y responder toothreats y proporciona una mayor visibilidad y control sobre, Hola seguridad de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integradas en las suscripciones de Azure, ayuda a detectar amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad. Las recomendaciones sobre redes se centran en los firewalls, los grupos de seguridad de red, la configuración de reglas de tráfico entrante y mucho más.

Algunas recomendaciones sobre redes disponibles son las siguientes:

-   [Agregue un Firewall de generación siguiente](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) recomienda agregar un servidor de seguridad de próxima generación (NGFW) desde un tooincrease de partner de Microsoft la protección de la seguridad

-   [Enrutar el tráfico a través de NGFW solo](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) recomienda que configure reglas de seguridad de grupo (NSG) que forzar el tráfico entrante tooyour máquina virtual a través de su NGFW de red.

-   [Habilitar los grupos de seguridad de red en subredes o máquinas virtuales](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) Recomienda que habilite grupos de seguridad de red en subredes o máquinas virtuales.

-   [Restringir el acceso a través de un punto de conexión accesible desde Internet](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) Recomienda que configure las reglas de tráfico entrante para grupos de seguridad de red.


## <a name="compute"></a>Proceso

sección de Hello proporciona información adicional con respecto a las características claves de esta área e información de resumen acerca de estas capacidades.

### <a name="antimalware--antivirus"></a>Antimalware y antivirus
Con IaaS de Azure, puede usar el software antimalware de los proveedores de seguridad, como Microsoft, Symantec, Trend Micro, McAfee y Kaspersky tooprotect las máquinas virtuales desde archivos malintencionados, adware y otras amenazas. [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) para Azure Cloud Services y Virtual Machines es una funcionalidad de protección que permite identificar y eliminar virus, spyware y otro software malintencionado. Microsoft Antimalware proporciona configurable genera una alerta cuando conoce tooinstall de intentos de software malintencionado o no deseado propio o ejecutarse en los sistemas de Azure. Microsoft Antimalware también puede implementarse mediante Azure Security Center.

### <a name="hardware-security-module"></a>Módulo de seguridad de hardware
Autenticación y cifrado no mejorar la seguridad, a menos que estén protegidas propias claves de Hola. Puede simplificar la administración de Hola y seguridad de los secretos críticos y claves almacenándolos en [el almacén de claves de Azure](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). El almacén de claves proporciona Hola opción toostore las claves en los estándares de hardware seguridad tooFIPS certificada de módulos (HSM) 140-2 nivel 2. Sus claves de cifrado de SQL Server para copias de seguridad o [cifrado de datos transparente](https://msdn.microsoft.com/library/bb934049.aspx) se pueden almacenar en el Almacén de claves con otras claves y secretos de sus aplicaciones. Permisos y acceso a los elementos protegido de toothese se administran a través de [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Copia de seguridad de máquina virtual
[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) es una solución que protege los datos de su aplicación sin necesidad de realizar ninguna inversión y afrontando unos costos operativos mínimos. Errores de aplicación pueden dañar los datos y los errores humanos pueden introducir errores en las aplicaciones que pueden causar problemas de toosecurity. Con Azure Backup, las máquinas virtuales que ejecutan Windows y Linux están protegidas.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Una parte importante de su organización [negocio continuidad y recuperación ante desastres (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) estrategia es pensar en cómo se producen tookeep corporativa cargas de trabajo y aplicaciones de seguridad y ejecución cuando se planean e interrupciones imprevistas. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) ayuda a coordinar la replicación, la conmutación por error y la recuperación de aplicaciones y cargas de trabajo para que estén disponibles desde una ubicación secundaria si la ubicación principal deja de funcionar.

### <a name="sql-vm-tde"></a>TDE de máquina virtual de SQL
El [cifrado de datos transparente (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) y cifrado de nivel de columna (CLE) son características de cifrado de SQL Server. Este tipo de cifrado requiere almacén y los clientes toomanage Hola utilice para el cifrado de claves criptográficas.

Hola servicio de almacén de claves de Azure (claves) está diseñado tooimprove Hola seguridad y la administración de estas claves en una ubicación segura y altamente disponible. Hola conector de SQL Server permite a SQL Server toouse estas claves del almacén de claves de Azure.

Si está ejecutando SQL Server con equipos locales, hay pasos que puede seguir tooaccess el almacén de claves de Azure desde el equipo de SQL Server local. Pero para SQL Server en máquinas virtuales de Azure, puede ahorrar tiempo mediante el uso de la característica de integración del almacén de claves de Azure Hola. Con unos tooenable de cmdlets de PowerShell de Azure esta característica, puede automatizar Hola configuración necesaria para una VM de SQL tooaccess el almacén de claves.

### <a name="vm-disk-encryption"></a>Cifrado de discos de máquinas virtuales
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) es una nueva funcionalidad que permite cifrar los discos de las máquinas virtuales de IaaS Windows y Linux. Se aplica la característica BitLocker Hola sector estándar de Windows y la característica de DM Crypt de Hola de cifrado del volumen de tooprovide de Linux para hello OS y discos de datos de Hola. solución de Hola se integra con el almacén de claves de Azure toohelp controlar y administrar claves de cifrado del disco de Hola y secretos en su suscripción de almacén de claves. solución de Hello también garantiza que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.

### <a name="virtual-networking"></a>Redes virtuales
Las máquinas virtuales necesita conectividad de red. toosupport ese requisito, Azure requiere toobe de máquinas virtuales conectada tooan red Virtual de Azure. Red Virtual de Azure es una construcción lógica que se basa en el tejido de red físico de Azure Hola. Cada instancia de [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) lógica está aislada de todas las demás instancias de Azure Virtual Network. Este aislamiento ayuda a garantizar que el tráfico de red en sus implementaciones no es accesible tooother clientes de Microsoft Azure.

### <a name="patch-updates"></a>Actualizaciones de revisiones
Las actualizaciones de revisión proporcionar base de Hola para encontrar y corregir posibles problemas y simplificar el proceso de administración de actualizaciones de software de hello, reduciendo el número de Hola de las actualizaciones de software que se debe implementar en su empresa y aumentando la capacidad toomonitor cumplimiento de normas.

### <a name="security-policy-management-and-reporting"></a>Informes y administración de directivas de seguridad
[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) le ayuda a evitar, detectar y responder toothreats y proporciona mayor visibilidad en y control sobre, seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integradas en las suscripciones de Azure, ayuda a detectar amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

### <a name="azure-security-center"></a>Azure Security Center
Centro de seguridad le ayuda a evitar, detectar y responder toothreats con una mayor visibilidad y control sobre la seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

## <a name="identify-and-access-management"></a>Administración de identidades y acceso

La protección de los sistemas, las aplicaciones y los datos comienza por los controles de acceso basado en identidad. Hola identidad y acceso a características de administración que están integradas en servicios y productos de Microsoft business ayudar a proteger su información personal y profesional del acceso no autorizado al realizar toolegitimate disponibles a los usuarios cuando y donde que lo necesiten.

### <a name="secure-identity"></a>Protección de la identidad
Microsoft usa varias prácticas de seguridad y las tecnologías en sus productos y la identidad de toomanage de servicios y el acceso.
-   [La autenticación multifactor](https://azure.microsoft.com/services/multi-factor-authentication/) requiere toouse a los usuarios de varios métodos para el acceso, local y en la nube de Hola. Proporciona autenticación sólida con una variedad de sencillas opciones de verificación, a la vez que admite usuarios mediante un proceso de inicio de sesión simple.

-   [Microsoft Authenticator](https://aka.ms/authenticator) ofrece una experiencia de Multi-Factor Authentication fácil de usar que funciona tanto con Microsoft Azure Active Directory como con cuentas de Microsoft e incluye compatibilidad con ponibles y aprobaciones basadas en huellas digitales.

-   [Aplicación de directivas de contraseña](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) aumenta Hola seguridad de contraseñas tradicionales si se imponen requisitos de longitud y complejidad forzados rotar periódicamente, e intentos de bloqueo de cuenta después de la autenticación con errores.

-   La [autenticación basada en token](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) habilita la autenticación mediante los Servicios de federación de Active Directory (AD FS) o sistemas de tokens seguros de terceros.

-   [Control de acceso basado en roles (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) permite toogrant acceso basado en usuario de hello asignado el rol, lo que toogive fácil a los usuarios únicamente Hola una cantidad de acceso que necesitan tooperform sus tareas de trabajo. Puede personalizar RBAC según el modelo de negocio de su organización y su tolerancia al riesgo.

-   [Administración de identidad (identidad híbrida) integrada](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) permite toomaintain control de acceso de los usuarios en plataformas de centros de datos y en la nube internas, crear una identidad de usuario único para la autenticación y autorización de recursos de tooall.

### <a name="secure-apps-and-data"></a>Protección de aplicaciones y datos
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), una extensión identity and access management nube solución completa, ayuda a proteger el acceso toodata en las aplicaciones in situ y en la nube de Hola y simplifica la administración de Hola de usuarios y grupos. Combina los servicios de directorio principales, avanzada regulación de identidad, seguridad y administración de acceso de la aplicación y facilita la administración de identidades basada en directivas de toobuild de los desarrolladores en sus aplicaciones. tooenhance su Azure Active Directory, puede agregar funciones de pagadas con las ediciones de Azure Active Directory Basic, Premium P1 y P2 Premium de Hola.

| Características comunes/gratuitas     | Características de la edición Basic    |Características de la edición Premium P1 |Características de la edición Premium P2 | Azure Active Directory Join, solo características relacionadas con Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Objetos de directorio](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [usuario o grupo de administración (agregar/actualizar/eliminar) / basada en usuario aprovisionamiento, el registro de dispositivos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [inicio de sesión único (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [Self-Service Cambio de contraseña para usuarios de la nube](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [conectar (motor de sincronización que extiende local directorios tooAzure Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [seguridad / informes de uso](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Aprovisionamiento y administración del acceso basados en grupo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning),    [Restablecimiento de contraseña de autoservicio para usuarios en la nube](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users),     [Personalización de marca de la compañía (personalización de las páginas de inicio de sesión y del panel de acceso)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization),    [Proxy de aplicación](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy),    [Acuerdo de Nivel de Servicio del 99,9 %](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Administración de grupos y aplicaciones de autoservicio o incorporaciones de aplicaciones de autoservicio o grupos dinámicos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group),    [Restablecimiento de contraseñas de autoservicio, cambio o desbloqueo con escritura diferida local](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back),    [Multi-Factor Authentication (en la nube y local [servidor MFA])](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server),    [CAL de MIM + servidor MIM](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server),     [Detección de aplicaciones en la nube](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery),     [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health),     [Sustitución automática de la contraseña para cuentas de grupo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Identity Protection](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection),     [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Unirse a un tooAzure dispositivo AD, SSO de escritorio, Microsoft Passport para Azure AD, recuperación de Bitlocker de administrador](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM-inscripción automática, la recuperación de Bitlocker Self-Service, dispositivos de administradores locales adicionales tooWindows 10 a través de Azure Combinación de AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) es una característica premium de Azure Active Directory que permite las aplicaciones de nube de tooidentify que utilizan los empleados de hello en su organización.

- [Azure Active Directory Identity Protection](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) es un servicio de seguridad que usa tooprovide de capacidades de detección de anomalías de Azure Active Directory una vista consolidada en eventos de riesgos y vulnerabilidades potenciales que podrían afectar a su identidades de la organización.

- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/) permite toojoin máquinas virtuales de Azure tooa dominio sin Hola necesitan controladores de dominio de toodeploy. Los usuarios iniciar sesión en toothese máquinas virtuales usando sus credenciales corporativas de Active Directory y pueden acceder sin problemas a recursos.

- [Azure B2C Directory Active](https://azure.microsoft.com/services/active-directory-b2c/) es un servicio de administración de identidades globales y de alta disponibilidad para las aplicaciones de consumo que se puede escalar toohundreds de millones de identidades e integrar a través de móviles y web plataformas. Los clientes pueden iniciar sesión tooall las aplicaciones a través de experiencias personalizables que utilizan cuentas de medios sociales existentes, o puede crear nuevas credenciales independiente.

- [Colaboración Azure de Active Directory B2B](https://aka.ms/aad-b2b-collaboration) es una solución de integración de socios segura que admite las relaciones entre empresas habilitando a los partners tooaccess sus aplicaciones y datos corporativos selectivamente mediante el uso de sus autoadministrados identidades.

- [Azure Active Directory unirse a](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) permite tooextend nube capacidades tooWindows 10 los dispositivos para la administración centralizada. Permite a los usuarios tooconnect toohello corporativa o de la organización en la nube a través de Azure Active Directory y simplifica el acceso tooapps y recursos.

- La característica [Proxy de la aplicación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) proporciona inicio de sesión único (SSO) y acceso remoto seguro para aplicaciones web hospedadas de forma local.

## <a name="next-steps"></a>Pasos siguientes
- [Introducción a la seguridad de Microsoft Azure](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Los servicios de Azure y características que puede usar toohelp protegen los servicios y los datos dentro de Azure

- [Azure Security Center](https://azure.microsoft.com/services/security-center/)

Evitar, detectar y responder toothreats con una mayor visibilidad y control sobre la seguridad de Hola de los recursos de Azure

- [Supervisión del estado de seguridad en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Hola capacidades de supervisión de directivas de cumplimiento de toomonitor centro de seguridad de Azure.
