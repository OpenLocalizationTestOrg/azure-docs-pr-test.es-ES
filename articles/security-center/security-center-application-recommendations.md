---
title: aaaProtecting las aplicaciones en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger los recursos de Azure y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Protección de las aplicaciones en Azure Security Center
Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.  Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y SQL.

Este artículo tratan las recomendaciones que se aplican tooapplications.  Las recomendaciones sobre aplicaciones se centran en la implementación de un firewall de aplicaciones web.  Uso de tabla de Hola a continuación como un toohelp de referencia comprende las recomendaciones de aplicaciones disponibles de Hola y lo que hace cada uno de ellos si se aplica.

## <a name="available-application-recommendations"></a>Recomendaciones sobre aplicaciones disponibles
| Recomendación | Description |
| --- | --- |
| [Agregar un firewall de aplicaciones web](security-center-add-web-application-firewall.md) |Recomienda implementar un Firewall de aplicaciones web (WAF) para los puntos de conexión web. Se muestra una recomendación WAFS para cualquier IP pública (dirección IP de nivel de instancia o con equilibrio de carga) que tiene un grupo de seguridad de red asociado con puertos abiertos web entrantes (80 y 443).</br></br>Centro de seguridad, se recomienda que aprovisionar un toohelp WAFS defenderse contra los ataques que se dirige a las aplicaciones web en máquinas virtuales y en el entorno del servicio de aplicaciones. Un entorno de App Service es una opción de plan de servicio [Premium](https://azure.microsoft.com/pricing/details/app-service/) de Azure App Service que proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service. toolearn más información acerca de ASE, vea hello [documentación del entorno de servicio de aplicación](../app-service/app-service-app-service-environments-readme.md).</br></br>Puede proteger varias aplicaciones web en el centro de seguridad mediante la adición de estas implementaciones de WAFS aplicaciones tooyour existentes. |
| [Finalización de la protección de la aplicación](security-center-add-web-application-firewall.md#finalize-application-protection) |configuración de hello toocomplete de un WAFS, tráfico debe ser redirigidos toohello WAFS dispositivo. Seguir esta recomendación completa cambios de instalación necesarios de Hola. |

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:

* [Protección de las máquinas virtuales en Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protección de las redes en Azure Security Center](security-center-network-recommendations.md)
* [Protección del servicio SQL de Azure en Azure Security Center](security-center-sql-service-recommendations.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
