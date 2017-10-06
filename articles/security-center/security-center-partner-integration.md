---
title: "integración de aaaPartner en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se integra Azure Security Center con socios tooenhance seguridad general de los recursos de Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Integración de asociados en Azure Security Center

En este artículo se describe cómo se integra Azure Security Center con socios toohelp mejorar la seguridad global. Centro de seguridad ofrece una experiencia integrada en Azure y aprovecha las ventajas de hello Azure Marketplace para socios certificados y la facturación.

> [!NOTE] 
> A partir de junio de 2017, centro de seguridad utiliza Hola Microsoft Monitoring Agent toocollect y almacén de los datos. Para más información, consulte [Migración de la plataforma de Azure Security Center](security-center-platform-migration.md). información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>¿Por qué se implementan las soluciones de asociados desde Security Center?

Integración de socios de tooleverage de cuatro razones principales en el centro de seguridad son:

- **Facilidad de implementación**. Implementar una solución de socios Hola siguiente recomendación de centro de seguridad es mucho más fácil. proceso de implementación de Hello puede ser automatizada por completo mediante el uso de una topología de red y el programa de instalación predeterminada. Como alternativa, los clientes pueden elegir una opción semiautomatizada para lograr más flexibilidad y personalización.
- **Detecciones integradas**. Los eventos de seguridad de las soluciones de asociados se recopilan, agregan y aparecen automáticamente como parte de las alertas e incidentes de Security Center. Estos eventos también se fusionan con detecciones de otro tooprovide orígenes capacidades de detección de amenazas avanzadas.
- **Supervisión y administración unificadas del mantenimiento**. Los clientes pueden usar todas las soluciones de socios comerciales toomonitor de eventos de estado integrado un vistazo. Básicas de administración está disponible, el programa de instalación de tooadvanced de facilitar el acceso mediante el uso de la solución de socios de Hola.
- **Exportar tooSIEM**. Los clientes pueden exportar todo el centro de seguridad y socios en común alertas sistemas de administración de eventos (SIEM) e información de seguridad local tooon formato del evento (CEF) mediante la integración de registros de Azure (vista previa).


## <a name="partners-that-integrate-with-security-center"></a>Asociados que se integran con Security Center

Actualmente, Security Center se integra con estas soluciones:

- Protección de punto de conexión ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec y [Microsoft Antimalware para Azure Cloud Services y Virtual Machines](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Firewall de aplicaciones web ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) y [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Firewall de última generación ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) y [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Evaluación de vulnerabilidades ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Con el tiempo, el centro de seguridad expandirá número Hola de asociados dentro de estas categorías y agregar nuevas categorías. 

## <a name="deploy-a-partner-solution"></a>Implementación de una solución de asociado

Según el programa de instalación de Hola de su entorno de Azure y la directiva de seguridad de hello definidos, el centro de seguridad puede recomendar que implementar una solución de socios. Hola recomendación de centro de seguridad le guiará en proceso de Hola y seleccionar e instalar una solución de socios. Hello experiencia de implementación global puede variar, según Hola tipo de solución y el socio comercial que utiliza. Para obtener más información, vea Hola siguientes artículos:

- [Instalar Endpoint Protection](security-center-install-endpoint-protection.md)
- [Agregar un firewall de aplicaciones web](security-center-add-web-application-firewall.md)
- [Agregar un firewall de última generación](security-center-add-next-generation-firewall.md)
- [Evaluación de vulnerabilidades no instalada](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Administración de soluciones de asociados

Después de la implementación, información de tooview sobre Hola estado de solución de Hola y realizar tareas de administración básicas, hello **centro de seguridad** hoja, seleccione hello **soluciones de asociados** opción. Para información acerca de cómo administrar soluciones de asociados en Security Center, consulte [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md).

![Integración de asociados](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Soporte técnico de Symantec endpoint protection es toodiscovery limitado. No hay alertas de estado disponibles.
>

## <a name="see-also"></a>Otras referencias

En este artículo, ha aprendido cómo toointegrate partner soluciones en el centro de seguridad de Azure. toolearn más información acerca del centro de seguridad, vea Hola siguientes artículos:

* [Guía de planeamiento y operaciones de Security Center](security-center-planning-and-operations-guide.md)
* [Administrar y responder a alertas de toosecurity en el centro de seguridad](security-center-managing-and-responding-alerts.md)
* [Comprensión de las alertas de seguridad en Azure Security Center](security-center-alerts-type.md)
* [Supervisión del estado de seguridad en Security Center](security-center-monitoring.md). Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Supervisión de soluciones de asociados con Security Center](security-center-partner-solutions.md). Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md). Obtener toofrequently respuestas preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/). Encuentre artículos de blog sobre el cumplimiento y la seguridad de Azure.
