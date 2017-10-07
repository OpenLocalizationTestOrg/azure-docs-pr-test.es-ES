---
title: "prácticas recomendadas de seguridad operativa aaaAzure | Documentos de Microsoft"
description: "En este artículo se proporciona un conjunto de procedimientos recomendados para la reforzar la seguridad operativa de Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Procedimientos recomendados de seguridad operativa de Azure
Seguridad operativa de Azure hace referencia toohello servicios, los controles y características disponibles toousers para proteger sus datos, aplicaciones y otros activos de Microsoft Azure. Seguridad operativa de Azure se basa en un marco que incorpora el conocimiento de hello adquirido a través de varias funciones que son único tooMicrosoft, incluidos Hola del ciclo de vida de desarrollo de seguridad de Microsoft (SDL), Hola Microsoft Security Response Center programa y conocimiento profundo del panorama de amenazas de ciberseguridad de Hola.

En este artículo se explica un conjunto de procedimientos recomendados de seguridad de las bases de datos de Azure. Estas prácticas recomendadas se derivan de nuestra experiencia con la seguridad de base de datos de Azure y experiencias de Hola de clientes como usted mismo.

Para cada procedimiento recomendado, explicaremos:
-   ¿Qué recomienda Hola
-   ¿Por qué desea tooenable este procedimiento recomendado
-   ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
- ¿Cómo puede obtener información práctica recomendada de hello tooenable

En este artículo Azure operativa recomendaciones de seguridad se basa en una opinión de consenso y capacidades de la plataforma Windows Azure y conjuntos de características, tal como aparecen en tiempo de Hola que se escribió este artículo. Las opiniones y las tecnologías que cambian con el tiempo y este artículo será esos cambios se actualizaron en un tooreflect de forma periódica.

Los procedimientos recomendados de seguridad operativa de Azure descritos en este artículo incluyen:

-   Supervisión, administración y protección de la infraestructura de nube
-   Administración de la identidad e implementación del inicio de sesión único (SSO)
-   Solicitudes de seguimiento, análisis de tendencias de uso y diagnóstico de problemas
-   Supervisión de los servicios con una solución de supervisión centralizada
-   Evitar, detectar y responder toothreats
-   Supervisión de las redes basada en un escenario integral
-   Implementación segura mediante las herramientas de DevOps comprobadas

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Supervisión, administración y protección de la infraestructura de nube
Las operaciones de TI es responsable de administrar la infraestructura de centro de datos, aplicaciones y datos, incluida la estabilidad de Hola y seguridad de estos sistemas. Sin embargo, al obtener información de seguridad a través de aumentar los complejos entornos de TI a menudo requiere toocobble reúnen datos de varios sistemas de administración y la seguridad de las organizaciones.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.

[Solución de seguridad de OMS y auditoría](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) permite tooactively de TI supervisar todos los recursos, que pueden ayudar a minimizar el impacto de Hola de incidentes de seguridad. Auditoría y seguridad de OMS tiene dominios de seguridad que pueden utilizarse para la supervisión de recursos.

Para obtener más información acerca de OMS, lea el artículo de hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp evitar, detectar y responder toothreats, [Operations Management Suite (OMS) solución de seguridad y auditoría](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) recopila y procesa los datos sobre los recursos, que incluye:

-   Registro de eventos de seguridad
-   Eventos de Seguimiento de eventos para Windows (ETW)
-   Eventos de auditoría de AppLocker
-   Registro de Firewall de Windows
-   Eventos de Advanced Threat Analytics
-   Resultados de evaluación de la línea base
-   Resultados de evaluación de antimalware
-   Resultados de la evaluación de la actualización o revisión
-   Secuencias de syslog que se habilitan de manera explícita en el agente de Hola


## <a name="manage-identity-and-implement-single-sign-on"></a>Administración de la identidad e implementación del inicio de sesión único
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft.

[Azure AD](https://azure.microsoft.com/services/active-directory/) también incluye una serie completa de funcionalidades de [administración de identidades](https://docs.microsoft.com/azure/security/security-identity-management-overview), incluida la [autenticación multifactor](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), el registro de dispositivos, la administración de contraseñas de autoservicio, la administración de grupos de autoservicio, la administración de cuentas con privilegios, el control de acceso basado en roles, la supervisión del uso de aplicaciones, la auditoría enriquecida y la supervisión y alertas de seguridad.

Hola siguiendo las capacidades puede proteger las aplicaciones en la nube, optimizar los procesos de TI, reducir los costos y ayudar a garantizar que se cumplen los objetivos de cumplimiento corporativo:

-   Administración de identidades y acceso para la nube de Hola
-   Simplificar la aplicación de nube de tooany de acceso de usuario
-   Protección de las aplicaciones y los datos confidenciales
-   Habilitación del autoservicio para los empleados
-   Integración con Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Administración de identidades y acceso para la nube de Hola
Azure Active Directory (Azure AD) es una completa [solución de nube de administración de identidades y acceso](https://www.microsoft.com/cloud-platform/identity-management), que proporciona un potente conjunto de capacidades toomanage usuarios y grupos. Ayuda a proteger el acceso local tooon y aplicaciones, incluidos los servicios web de Microsoft como Office 365 y el software no sean de Microsoft como aplicaciones de servicio (SaaS) en la nube.
toolearn más protección de la identidad de tooenable en Azure AD, vea [habilitar Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Simplificar la aplicación de nube de tooany de acceso de usuario
[Habilitar inicio de sesión único](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify toothousands de acceso de usuario de aplicaciones de nube desde dispositivos Windows, Mac, iOS y Android. Los usuarios pueden iniciar aplicaciones desde un panel de acceso web personalizado o una aplicación móvil con las credenciales de la compañía. Utilice toogo de módulo de Proxy de aplicación hello Azure AD más allá de las aplicaciones de SaaS y publicar en web aplicaciones tooprovide altamente seguro remoto acceso local y el inicio de sesión único.

### <a name="protect-sensitive-data-and-applications"></a>Protección de las aplicaciones y los datos confidenciales
Habilitar [la autenticación multifactor Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent no autorizado a tooon desde la oficina y aplicaciones en la nube, proporcionando un nivel adicional de autenticación. Proteja su negocio y mitigue posibles amenazas mediante la supervisión de la seguridad, alertas e informes basados en Machine Learning que identifican patrones de acceso incoherentes.

### <a name="enable-self-service-for-your-employees"></a>Habilitación del autoservicio para los empleados
Delegar a empleados de tooyour tareas importantes, como el restablecimiento de contraseñas y la creación y administración de grupos. [Habilite el cambio y el restablecimiento de contraseñas de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), y la administración de grupos de autoservicio con Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integración con Azure Active Directory
Extender [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) y cualquier otro en local directorios tooAzure AD tooenable inicio de sesión único para todas las aplicaciones basadas en la nube. Atributos de usuario pueden ser el directorio en la nube tooyour sincronizan automáticamente desde todos los tipos de directorios locales.

toolearn más acerca de la integración de Azure Active Directory y cómo tooenable, lea el artículo de hello [integrar sus directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Solicitudes de seguimiento, análisis de tendencias de uso y diagnóstico de problemas
[Azure Storage Analytics](https://docs.microsoft.com/azure/storage/storage-analytics) realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Puede utilizar este solicitudes de tootrace de datos, analizar las tendencias de uso y diagnosticar problemas con su cuenta de almacenamiento.

Las métricas de Storage Analytics se habilitan de forma predeterminada para las nuevas cuentas de almacenamiento. Puede habilitar el registro y configurar las métricas y registro de hello portal de Azure; Para obtener más información, consulte [supervisar una cuenta de almacenamiento en el portal de Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). También puede habilitar el análisis de almacenamiento mediante programación a través de la API de REST de Hola o biblioteca de cliente de Hola. Utilizar Hola Set Service Properties operación tooenable análisis de almacenamiento por separado para cada servicio.

Para obtener una guía detallada sobre el uso de análisis de almacenamiento y otra herramientas tooidentify, diagnosticar y solucionar problemas relacionados con el almacenamiento de Azure, vea [supervisar, diagnosticar y solucionar problemas de almacenamiento de Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

toolearn más acerca de la integración de Azure Active Directory y cómo tooenable, lea el artículo de hello [habilitar y configurar el análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Servicios de supervisión
Las aplicaciones de nube son complejas y tienen muchas partes móviles. La supervisión proporciona tooensure de datos que mantiene la aplicación y en ejecución en un estado correcto. También ayuda a toostave off posibles problemas o solucionar problemas más allá de los. Además, puede usar supervisión toogain profundo información sobre los datos acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual.

### <a name="monitor-azure-resources"></a>Supervisión de los recursos de Azure
[Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) es servicio de plataforma de Hola que proporciona un único origen para la supervisión de recursos de Azure. Con el Monitor de Azure, puede visualizar, consultar, enrutar, archivar y tomar medidas sobre las métricas de Hola y registros procedentes de recursos de Azure. Puede trabajar con estos datos con la hoja de portal de Monitor de hello, [Cmdlets de PowerShell de Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [multiplataforma CLI](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), o [API de REST de Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Habilitación del escalado automático con Azure Monitor
Habilitar [escalado automático de Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) se aplica solo conjuntos de escalas de máquina de toovirtual (VMSS), servicios en la nube, planes de servicio de aplicaciones y entornos del servicio de aplicación.

### <a name="manage-roles-permissions-and-security"></a>Administración de seguridad y permisos de roles
Muchos equipos necesitan toostrictly [regular el acceso toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) datos y la configuración. Por ejemplo, si tiene los miembros del equipo que trabajan en exclusivamente de supervisión (ingenieros de soporte técnico, ingenieros de devops) o si usa un proveedor de servicios administrados, puede que desee toogrant acceso tooonly datos de supervisión al restringir su toocreate de capacidad, modificar, o eliminar los recursos.

Esto muestra cómo tooquickly aplicar un supervisión RBAC rol tooa usuario integradas en Azure o crear sus propios roles personalizados para un usuario que necesita permisos de supervisión limitados. , A continuación, describe las consideraciones de seguridad para los recursos relacionados con el Monitor de Azure y cómo puede limitar el acceso a los datos toohello contienen.

## <a name="prevent-detect-and-respond-toothreats"></a>Evitar, detectar y responder toothreats
Detección de amenazas de centro de seguridad funciona al recopilar automáticamente información de seguridad de los recursos de Azure, la red de Hola y soluciones de socios conectados. Analiza esta información, a menudo correlacionar información procedente de varios orígenes, tooidentify amenazas. En el centro de seguridad se priorizan las alertas de seguridad junto con recomendaciones sobre cómo tooremediate Hola amenaza.

-   [Configure una directiva de seguridad](https://docs.microsoft.com/azure/security-center/security-center-policies) para su suscripción de Azure.
-   Hola de uso [recomendaciones que aparecen en el centro de seguridad](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp proteger los recursos de Azure.
-   Revise y administre las [alertas de seguridad](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) actuales.

[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Hola de ayuda a evitar, detectar y responder toothreats con una mayor visibilidad de y control sobre la seguridad de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Centro de seguridad ofrece amenaza fácil de usar y eficaces capacidades de prevención, detección y respuesta que están integradas en tooAzure. Principales capacidades:

-   Conocimiento del estado de seguridad en la nube
-   Control de la seguridad en la nube
-   Implementación de soluciones de seguridad en la nube integradas de forma sencilla
-   Detección de amenazas y respuesta rápida

### <a name="understand-cloud-security-state"></a>Conocimiento del estado de seguridad en la nube
Use el centro de seguridad de Azure tooget una vista central de estado de seguridad de Hola de todos los recursos de Azure. Un vistazo, compruebe que los controles de seguridad apropiados de Hola están en vigor y configuran correctamente e identifican rápidamente los recursos, que requieren atención.

### <a name="take-control-of-cloud-security"></a>Control de la seguridad en la nube
Definir [las directivas de seguridad](https://docs.microsoft.com/azure/security-center/security-center-policies) para las suscripciones de Azure según tooyour empresa de la seguridad de nube necesidades, adaptada toohello tipo de aplicaciones o importancia de los datos de Hola en cada suscripción. Usa los propietarios de recomendaciones controlado por directivas tooguide recursos por proceso de saludo de la implementación de controles necesarios: tomar Hola conjeturas a la seguridad de la nube.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Implementación de soluciones de seguridad en la nube integradas de forma sencilla
[Habilite soluciones de seguridad](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) de Microsoft y de sus asociados, incluidos los principales firewalls del sector y antimalware. Uso simplificado de las soluciones de seguridad toodeploy aprovisionamiento, cambios de redes incluso se configuran automáticamente. Los eventos de seguridad de soluciones de asociados se recopilan también de forma automática con fines de análisis y alerta.

### <a name="detect-threats-and-respond-fast"></a>Detección de amenazas y respuesta rápida
Adelántese a las amenazas en la nube, tanto a las actuales como a las que puedan surgir, con una estrategia integrada basada en el análisis. Security Center combina la experiencia y los recursos de [inteligencia globales de Microsoft en materia de amenazas](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) con el conocimiento de los eventos relacionados con la seguridad en la nube de sus implementaciones en Azure. De este modo, le ayuda a detectar a tiempo amenazas reales y reduce los falsos positivos. Alertas de seguridad de la nube proporcionan información sobre la campaña de ataque de hello, incluidos los eventos relacionados y los recursos afectados y sugieren formas tooremediate emite y recuperarse rápidamente.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Supervisión de las redes basada en un escenario integral
Los clientes pueden crear una red integral en Azure mediante la orquestación y composición de varios recursos de red individuales como, por ejemplo, redes virtuales, ExpressRoute, Application Gateway, equilibradores de carga y muchos más. La supervisión está disponible en cada uno de los recursos de red de Hola.

[Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) es un servicio regional que le permite toomonitor y diagnosticar condiciones en un nivel de escenario de red en, a y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatización de la supervisión de la red remota con captura de paquetes
Supervisar y diagnosticar problemas de red sin inicio de sesión tooyour máquinas virtuales (VMs) mediante el Monitor de red. Desencadenador [captura de paquetes](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) mediante la configuración de alertas y obtener información sobre el rendimiento en tiempo de tooreal acceso a nivel de paquetes de saludo. Cuando vea un problema, podrá investigar en detalle para mejorar los diagnósticos.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Obtención de información detallada sobre el tráfico de la red mediante registros de flujo
Conozca al detalle el patrón de tráfico de red mediante los [registros de flujo del grupo de seguridad de red](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). La información proporcionada por los registros de flujo le ayuda a recopilar datos para el cumplimiento, la auditoría y la supervisión de su perfil de seguridad de red.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnóstico de problemas de conectividad VPN
Monitor de red proporciona Hola capacidad demasiado[diagnosticar los problemas más comunes de puerta de enlace VPN y conexiones](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Lo que no solo problema de hello tooidentify, sino también toouse Hola detallada investigar toohelp creado aún más los registros.

más información acerca de cómo toolearn tooconfigure Monitor de red y cómo tooenable, lea el artículo de hello [configurar el Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Implementación segura mediante las herramientas de DevOps comprobadas
Estas son algunas de hello prácticas DevOps lista de Azure en este espacio de Microsoft Cloud, lo que hace que las empresas y los equipos productivas y eficaces.

-   **Infraestructura como código (IaC):** infraestructura como código es un conjunto de técnicas y prácticas recomendadas, que ayudan a los profesionales de TI quitar carga Hola asociada a la compilación de hello día tooday y administración de infraestructura modular. Permite a los profesionales de TI toobuild y mantener su entorno de servidor moderna de forma similar a cómo los desarrolladores de software crear y mantienen el código de aplicación. De Azure, tenemos [Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) permite tooprovision las aplicaciones utilizando una plantilla declarativa. En una plantilla, puede implementar varios servicios junto con sus dependencias. Usar hello mismo toorepeatedly plantilla implementar la aplicación durante cada fase del ciclo de vida de aplicación Hola.
-   **La implementación e integración continua:** puede configurar los proyectos de equipo de Visual Studio Online demasiado[automáticamente compilar e implementar](https://www.visualstudio.com/docs/build/overview) tooAzure aplicaciones web o servicios en la nube. VSO implementa automáticamente los archivos binarios de hello después de realizar una compilación tooAzure después de cada comprobación de código. proceso de compilación del paquete se describen aquí Hello es toohello equivalente de comando de paquete de Visual Studio y pasos de publicación de hello son comandos de publicación toohello equivalente en Visual Studio.
-   **Administración de versiones:** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) es una excelente solución para automatizar la implementación de varias fase y administrar Hola el proceso de publicación. Crear una implementación continua administrado canalizaciones toorelease rápidamente, fácilmente y con frecuencia. Con Release Management, podemos automatizar en gran medida el proceso de lanzamiento así como tener predefinidos flujos de trabajo de aprobación. Implementar local y toohello en la nube, ampliar y personalizar según sea necesario.
-   **Supervisión del rendimiento de las aplicaciones:** detecte y resuelva los problemas, y mejore continuamente las aplicaciones. Diagnostique rápidamente cualquier problema en su aplicación activa. Sepa lo que sus usuarios hacen con ella. Configuración consiste en fácil de agregar código de Javascript y una entrada webconfig y ver resultados en minutos en el portal de Hola a todos los detalles de Hola. [Detalles de aplicaciones](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) ayuda a las empresas para la detección más rápida de problemas y corrección.
-   **Cargar pruebas & escalado automático:** podemos encontrar problemas de rendimiento en nuestra calidad de implementación de aplicación tooimprove y toomake que nuestra aplicación esté siempre disponible hacia arriba o hacia toocater toohello las necesidades del negocio. Asegúrese de que la aplicación puede controlar el tráfico para su campaña de marketing o su siguiente lanzamiento. Empiece a ejecutar [pruebas de carga](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) basadas en la nube sin invertir apenas tiempo con Visual Studio Online.

## <a name="next-steps"></a>Pasos siguientes
- Más información acerca de la [Seguridad operativa de Azure](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn más [Operations Management Suite | Seguridad y cumplimiento](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Introducción a la solución Seguridad y auditoría de Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
