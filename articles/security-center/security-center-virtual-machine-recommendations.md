---
title: "aaaProtecting sus máquinas virtuales en el centro de seguridad de Azure | Documentos de Microsoft"
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger las máquinas virtuales y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Protección de las máquinas virtuales en Azure Security Center
Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.  Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y SQL.

Este artículo tratan las recomendaciones que se aplican tooVMs.  Las recomendaciones de máquinas virtuales se centran en la recopilación de datos, la aplicación de actualizaciones del sistema, el aprovisionamiento antimalware, el cifrado de los discos de máquinas virtuales y mucho más.  Uso de tabla de Hola a continuación como un toohelp de referencia comprende recomendaciones de VM disponibles hello y cada uno de ellos lo que sucederá si se aplica.

## <a name="available-vm-recommendations"></a>Recomendaciones de máquinas virtuales disponibles
| Recomendación | Description |
| --- | --- |
| [Habilitar la colección de datos de las suscripciones](security-center-enable-data-collection.md) |Se recomienda activar la recopilación de datos en la directiva de seguridad de Hola para cada una de las suscripciones y todas las máquinas virtuales (VM) en el nodo suscripciones. |
| [Habilitar el cifrado para la cuenta de Azure Storage](security-center-enable-encryption-for-storage-account.md) | Es recomendable que habilite el cifrado del servicio de Azure Storage para datos en reposo. Cifrado de servicio de almacenamiento (SSE) funciona mediante el cifrado de datos de hello cuando se escribe tooAzure almacenamiento y descifra antes de la recuperación. SSE actualmente solo está disponible para hello servicio Blob de Azure y puede usarse para blobs en bloques, blobs de página y blobs en anexos. más información, consulte toolearn [cifrado del servicio de almacenamiento de datos en reposo](../storage/common/storage-service-encryption.md).</br>SSE solo es compatible con las cuentas de almacenamiento de Resource Manager. Las cuentas de almacenamiento clásico no se admiten en este momento. Hola toounderstand clásico y modelos de implementación del Administrador de recursos, consulte [modelos de implementación de Azure](../azure-classic-rm.md). |
| [Corrección de vulnerabilidades del SO](security-center-remediate-os-vulnerabilities.md) |P. ej., recomienda alinear las configuraciones de sistema operativo con hello las reglas de configuración, se recomienda no permiten toobe contraseñas guardado. |
| [Aplicar actualizaciones del sistema](security-center-apply-system-updates.md) |Se recomienda que implemente tooVMs actualizaciones críticas y seguridad del sistema que faltan. |
| [Aplicación del control de acceso a redes Just-In-Time](security-center-just-in-time.md) | Se recomienda que aplique acceso a la máquina virtual Just-In-Time. Hola justo a la característica de tiempo está en la vista previa y disponible en hello nivel estándar del centro de seguridad. Vea [precios](security-center-pricing.md) toolearn más información acerca del centro de seguridad de los niveles de precios. |
| [Reiniciar tras actualizar el sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomienda que reinicie un proceso de máquina virtual toocomplete Hola de aplicar las actualizaciones del sistema. |
| [Instalación de Endpoint Protection](security-center-install-endpoint-protection.md) |Recomienda que aprovisione tooVMs de programas antimalware (sólo VM de Windows). |
| [Resolver alertas de estado de Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomienda resolver los errores de Endpoint Protection. |
| [Habilitar el Agente de máquina virtual](security-center-enable-vm-agent.md) |Permite toosee que las máquinas virtuales requieren Hola a agente de máquina virtual. Hola agente de máquina virtual debe instalarse en máquinas virtuales en la detección, análisis de la línea de base y los programas antimalware de revisiones de tooprovision de orden. Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace. artículo de Hello [agente de máquina virtual y extensiones: parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) proporciona información acerca de cómo tooinstall Hola agente de máquina virtual. |
| [Aplicar cifrado de discos](security-center-apply-disk-encryption.md) |Se recomienda cifrar los discos de la máquina virtual mediante Cifrado de discos de Azure (máquinas virtuales Linux y Windows). El cifrado se recomienda para hello SO y volúmenes de datos en la máquina virtual. |
| [Actualizar versión del sistema operativo](security-center-update-os-version.md) |Se recomienda actualizar la versión de sistema operativo (SO) de Hola para su servicio en la nube toohello versión más reciente disponible para la familia del SO.  toolearn más información acerca de los servicios en la nube, vea hello [Introducción a los servicios de nube](../cloud-services/cloud-services-choose-me.md). |
| [Evaluación de vulnerabilidades no instalada](security-center-vulnerability-assessment-recommendations.md) |Se recomienda instalar una solución de evaluación de vulnerabilidades en la máquina virtual. |
| [Corrección de vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Le permite toosee vulnerabilidades de sistema y las aplicaciones detectadas por la solución de evaluación de vulnerabilidades de hello instalado en la máquina virtual. |

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:

* [Protección de las aplicaciones en Azure Security Center](security-center-application-recommendations.md)
* [Protección de las redes en Azure Security Center](security-center-network-recommendations.md)
* [Protección del servicio SQL de Azure en Azure Security Center](security-center-sql-service-recommendations.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
