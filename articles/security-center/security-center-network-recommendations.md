---
title: aaaProtecting la red en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger las redes y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Protección de las redes en Azure Security Center
Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.  Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y SQL.

Este artículo tratan las recomendaciones que se aplican tooyour red.  Las recomendaciones sobre redes se centran en los firewalls de próxima generación, los grupos de seguridad de red, la configuración de reglas de tráfico entrantes y mucho más.  Uso de tabla de Hola a continuación como un toohelp de referencia comprende las recomendaciones de red disponible de Hola y lo que hace cada uno de ellos si se aplica.

## <a name="available-network-recommendations"></a>Recomendaciones sobre redes disponibles
| Recomendación | Description |
| --- | --- |
| [Agregar un firewall de próxima generación](security-center-add-next-generation-firewall.md) |Recomienda agregar un servidor de seguridad de próxima generación (NGFW) desde un tooincrease de partner de Microsoft la protección de la seguridad. |
| [Enrutar el tráfico solo a través de NGFW](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Se recomienda que configure reglas de grupo (NSG) de seguridad de red que fuerce el tráfico entrante tooyour máquina virtual a través de su NGFW. |
| [Habilitar grupos de seguridad de red en subredes o máquinas virtuales](security-center-enable-network-security-groups.md) |Recomienda habilitar NSG en subredes o máquinas virtuales. |
| [Restringir el acceso a través de puntos de conexión accesibles desde Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recomienda configurar reglas de tráfico de entrada para los NSG. |

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:

* [Protección de las máquinas virtuales en Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protección de las aplicaciones en Azure Security Center](security-center-application-recommendations.md)
* [Protección del servicio SQL de Azure en Azure Security Center](security-center-sql-service-recommendations.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
