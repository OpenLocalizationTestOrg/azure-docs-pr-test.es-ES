---
title: aaaMonitor su infraestructura de identidad local en hello en la nube.
description: "Ésta es hello Azure AD Connect Health página que describe qué es y por qué debería usarlo."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Supervisar los servicios de infraestructura y la sincronización de identidad local en la nube de Hola
Mantenimiento de Connect de Azure Active Directory (Azure AD) le ayuda a supervisar y obtener información sobre su identidad local hello y la infraestructura de servicios de sincronización. Permite toomaintain un tooOffice conexión confiable 365 y Microsoft Online Services proporcionando capacidades de supervisión para los componentes clave de identidad como servidores de servicios de federación de Active Directory (AD FS), servidores de Azure AD Connect (también conocidos como el motor de sincronización), controladores de dominio de Active Directory, etcetera. También hace puntos de datos de la clave de hello acerca de estos componentes fácilmente accesible para que pueda obtener uso y otros importantes decisiones toomake de visión.

Hola información se presenta en hello [portal de Azure AD Connect Health](https://aka.ms/aadconnecthealth). En el portal de Azure AD Connect Health hello, puede ver las alertas, supervisión de rendimiento, análisis de uso y otra información. Azure AD Connect Health permite sola imagen de Hola de mantenimiento de los componentes clave de identidad en un solo lugar.

![Qué es Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

A medida que aumentan las características de hello en Azure AD Connect Health, portal de hello proporciona un único panel a través de la lente de Hola de identidad. Obtener un entorno incluso más sólido, correcto e integrado para los usuarios tooincrease sus capacidad tooget pueden realizar acciones.

## <a name="why-use-azure-ad-connect-health"></a>Motivos para usar Azure AD Connect Health
Al integrar los directorios locales con Azure AD, los usuarios son más productivos porque no hay una identidad común tooaccess tanto en la nube y recursos locales. Sin embargo, esta integración crea desafío Hola consistente en garantizar que este entorno es correcto para que los usuarios confiable pueden acceder a recursos tanto local como en hello en la nube desde cualquier dispositivo. Mantenimiento de Azure AD Connect le ayuda a supervisar y obtener información sobre la infraestructura de identidad local que está tooaccess usa Office 365 u otras aplicaciones de Azure AD. Es tan sencillo como instalar un agente en cada uno de los servidores de identidad locales.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Azure AD Connect Health para AD FS](active-directory-aadconnect-health-adfs.md)
Azure AD Connect Health para AD FS es compatible con AD FS 2.0 en Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2. También admite la supervisión de los proxy de hello AD FS o admiten servidores de proxy de aplicación web que proporcionan autenticación para acceso de extranet. Con una instalación fácil y económica de agente de mantenimiento de hello, Azure AD Connect Health para AD FS proporciona Hola siguiendo el conjunto de capacidades clave:

* Supervisión con tooknow alertas cuando los servidores de proxy de AD FS y AD FS no están en buenas condiciones
* Notificaciones de correo electrónico para alertas críticas
* Tendencias de los datos de rendimiento, que son útiles para planear la capacidad de AD FS
* Análisis de uso para inicios de sesión de AD FS con tablas dinámicas (aplicaciones, los usuarios, etc. de ubicación de red), que son útil toounderstand cómo obtener se utiliza AD FS
* Informes para AD FS, como los primeros 50 usuarios con nombre de usuario o contraseña de inicio de sesión erróneos y su última dirección IP

Hello vídeo siguiente proporciona una visión general de Azure AD Connect Health para AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health para la sincronización se supervisa y se proporciona información acerca de las sincronizaciones de Hola que se producen entre su Active Directory en local y Azure AD. Azure AD Connect Health para la sincronización proporciona Hola siguiendo el conjunto de capacidades clave:

* Supervisión con alertas tooknow cuando un servidor de Azure AD Connect, también conocido como Hola motor de sincronización, no es correcto
* Notificaciones de correo electrónico para alertas críticas
* Sincronización de la visión operativa, que incluye gráficos de latencia de las operaciones de sincronización y tendencias de distintas operaciones, como incorporaciones, actualizaciones y eliminaciones
* Vista rápida obtener información acerca de las propiedades de sincronización y el último correcta exportación tooAzure AD
* Los informes acerca de los errores de sincronización de nivel de objeto \(no requieren Azure AD Premium\)

Hello vídeo siguiente proporciona una visión general de Azure AD Connect Health para la sincronización.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Azure AD Connect Health para AD DS](active-directory-aadconnect-health-adds.md)
Azure AD Connect Health para Active Directory Domain Services (AD DS) proporciona supervisión para los controladores de dominio instalados en Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016. Hola instalación del agente de mantenimiento permite toomonitor sus instalaciones en el entorno de AD DS de la nube de Hola. Azure AD Connect Health para AD DS proporciona Hola siguiendo el conjunto de capacidades clave:

* Supervisión de alertas toodetect cuando los controladores de dominio son correctos y enviar por correo electrónico notificaciones de alertas críticas
* panel de controladores de dominio de Hello, que proporciona una vista rápida del estado de Hola y el estado operativo de los controladores de dominio
* panel de estado de replicación de Hola que tiene información de replicación más reciente de Hola y vincula a tootroubleshooting guías cuando se detectan errores
* Rápido acceso desde cualquier lugar tooperformance gráficos de datos de contadores de rendimiento populares, que son necesarios para solucionar problemas y supervisión

Hello vídeo siguiente proporciona una visión general de Azure AD Connect Health para AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Introducción a Azure AD Connect Health
tooget a trabajar con Azure AD Connect Health, Hola uso pasos:

1. [Obtenga Azure AD Premium](../active-directory-get-started-premium.md) o [inicie una prueba](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Descargue e instale los agentes de Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) en los servidores de identidad.
3. Panel de vista hello Azure AD Connect Health en [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Recuerde que para ver datos en el panel de mantenimiento de Azure AD Connect, deberá tooinstall hello Azure AD Connect Health agentes en los servidores de destino.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Descarga e instalación de un agente de Azure AD Connect Health
* Asegúrese de que se [satisfacer los requisitos de hello](active-directory-aadconnect-health-agent-install.md#requirements) de Azure AD Connect Health.
* Introducción a Azure AD Connect Health para AD FS
    * [Descargue el agente de Azure AD Connect Health para AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Consulte las instrucciones de instalación de hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Introducción al uso de Azure AD Connect Health para la sincronización
    * [Descargue e instale la versión más reciente de Hola de Azure AD Connect](http://go.microsoft.com/fwlink/?linkid=615771). Hola agente de mantenimiento para la sincronización se instalará como parte de la instalación de hello Azure AD Connect (versión 1.0.9125.0 o superior).
* Introducción a Azure AD Connect Health para AD DS
    * [Descargue el agente de Azure AD Connect Health para AD DS](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Consulte las instrucciones de instalación de hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portal de Azure AD Connect Health
portal de Azure AD Connect Health Hello muestra vistas de alertas, supervisión de rendimiento y análisis de uso. Hola https://aka.ms/aadconnecthealth dirección URL tiene toohello hoja principal de Azure AD Connect Health. Puede considerar una hoja como una ventana. En la hoja principal de hello, consulte **inicio rápido**, servicios de Azure AD Connect Health y opciones de configuración adicionales. Vea Hola siguiente captura de pantalla y breves explicaciones que siguen la captura de pantalla de Hola. Después de implementar a agentes de hello, servicio de mantenimiento de hello identifica automáticamente los servicios de Hola que supervisa el mantenimiento de Azure AD Connect.

> [!NOTE]
> Para obtener información sobre licencias, vea hello [P+F de conectarse de Azure AD](active-directory-aadconnect-health-faq.md) o hello [página de precios de Azure AD](https://aka.ms/aadpricing).
    
![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Inicio rápido**: cuando se selecciona esta opción, Hola **inicio rápido** abre la hoja. Puede descargar el agente de Azure AD Connect Health Hola seleccionando **obtener herramientas**. También puede acceder a la documentación y aportar comentarios.
* **Los servicios de federación de Active Directory**: esta opción muestra todos los servicios de hello AD FS que Azure AD Connect Health está supervisando actualmente. Cuando se selecciona una instancia, hoja de Hola que se abre muestra información acerca de esa instancia de servicio. Esta información incluye una descripción general, propiedades, alertas, supervisión y análisis de uso. Obtenga más información sobre las capacidades de hello en [con Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (sync)**: esta opción muestra los servidores de Azure AD Connect que Azure AD Connect Health supervisa actualmente. Cuando se selecciona la entrada de hello, hoja de Hola que se abre muestra información acerca de los servidores de Azure AD Connect. Obtenga más información sobre las capacidades de hello en [con Azure AD Connect Health para la sincronización de](active-directory-aadconnect-health-sync.md).
* **Los servicios de dominio de Active Directory**: esta opción muestra todos los bosques de AD DS de Hola que Azure AD Connect Health está supervisando actualmente. Seleccione un bosque, hoja de Hola que se abre muestra información sobre ese bosque. Esta información incluye una visión general de la información esencial, panel de controladores de dominio de hello, panel de estado de replicación de hello, alertas y supervisión. Obtenga más información sobre las capacidades de hello en [con Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md).
* **Configurar**: esta sección incluye opciones de la siguiente de Hola de tooturn o desactivar:

  - Actualización automática tooautomatically actualización hello Azure AD Connect Health toohello última versión del agente: será toohello actualizan automáticamente versiones más recientes del agente de Azure AD Connect Health hello cuando están disponibles. Esta opción está habilitada de manera predeterminada.
  - Permitir que los datos de estado del directorio de Microsoft access tooyour Azure AD para solo con fines de solución de problemas: si esta opción está habilitada, Microsoft puede ver Hola los mismos datos que se ven. Esta información puede ayudar a solucionar problemas. Esta opción está deshabilitada de manera predeterminada.

## <a name="related-links"></a>Vínculos relacionados
* [Instalación del Agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
