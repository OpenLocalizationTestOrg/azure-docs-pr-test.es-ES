---
title: "problemas de aaaDeployment de preguntas más frecuentes sobre servicios de nube de Microsoft Azure | Documentos de Microsoft"
description: "Este artículo enumeran Hola preguntas más frecuentes acerca de la implementación de servicios de nube de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de implementación con Azure Cloud Services: preguntas más frecuentes (P+F)

En este artículo se incluyen preguntas frecuentes sobre problemas de implementación con [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>¿Por qué implementar un toohello de servicio de nube ranura de ensayo a veces un error con un error de asignación de recursos si ya hay una implementación existente en la ranura de producción de hello?
Si un servicio de nube tiene una implementación en cualquier ranura, servicio de nube todo de hello está anclado tooa específico del clúster. Esto significa que si una implementación ya existe en la ranura de producción de hello, una nueva implementación de ensayo solo se puede asignar en el mismo clúster según la zona de producción de hello de Hola.

Se producen errores de asignación al clúster de Hola donde se encuentra el servicio de nube no tiene suficiente física toosatisfy de recursos de proceso de la solicitud de implementación.

Como ayuda para mitigar estos errores de asignación, consulte [Error de asignación de servicio en la nube: Soluciones](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>¿Por qué produce a veces un error de asignación el escalado vertical u horizontal de la implementación de un servicio en la nube?
Cuando se implementa un servicio de nube, normalmente obtiene tooa anclados específico del clúster. Esto significa que el escalado/out una nube existente servicio debe asignar nuevas instancias en hello mismo clúster. Si clúster Hola está cerca de su capacidad u Hola deseado VM/tipo de tamaño no está disponible, puede producir un error en la solicitud de saludo.

Como ayuda para mitigar estos errores de asignación, consulte [Error de asignación de servicio en la nube: Soluciones](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>¿Por qué implementar un servicio en la nube en un grupo de afinidad a veces produce un error de asignación?
Tejido de Hola en cualquier clúster en dicha región, puede asignar un nuevo servicio de nube vacía de tooan de implementación a menos que el servicio de nube de hello está anclado tooan grupo de afinidad. Toohello de las implementaciones se tratará el mismo grupo de afinidad en hello mismo clúster. Si el clúster de hello está cerca de su capacidad, puede producir un error en la solicitud de saludo.

Como ayuda para mitigar estos errores de asignación, consulte [Error de asignación de servicio en la nube: Soluciones](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>¿Por qué cambiar tamaño de máquina virtual o agregar un nueva máquina virtual tooan existente servicio en la nube a veces produce error de asignación?
clústeres de Hello en un centro de datos pueden tener diferentes configuraciones de tipos de máquina (p. ej., una serie, serie Av2, serie D, serie Dv2, serie G, serie H, etcetera). Pero no todos los clústeres de hello tendría necesariamente todos los tipos de Hola de máquinas virtuales. Por ejemplo, si intenta tooadd una serie D servicio de nube VM tooa que ya se ha implementado en un clúster de un solo serie, experimentará un error de asignación. Esto también sucederá si intentas toochange VM SKU tamaños (por ejemplo, pasando de una serie de una serie tooa D).

Como ayuda para mitigar estos errores de asignación, consulte [Error de asignación de servicio en la nube: Soluciones](cloud-services-allocation-failures.md#solutions).

tamaños de hello toocheck disponibles en su región, consulte [Microsoft Azure: productos disponibles por región](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>¿Por qué realiza la implementación de una nube servicio algún día fail due toolimits/cuotas/restricciones en mi suscripción o el servicio?
Implementación de un servicio de nube puede fallar si recursos hello toobe necesario asignado superan predeterminado de Hola o cuota máxima permitida para su servicio en nivel de hello región/centro de datos. Para más información, consulte [Límites de Cloud Services](../azure-subscription-service-limits.md#cloud-services-limits).

También puede realizar un seguimiento Hola actual o la cuota de uso de su suscripción en el portal de hello: Portal de Azure = > suscripciones = > \<adecuados suscripción > = > "Uso + cuota".

También puede recuperar la información / consumo relacionadas con el uso de recursos a través de hello las API de facturación de Azure. Consulte [API de uso de recursos de Azure (versión preliminar)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>¿Cómo se puede cambiar tamaño de Hola de una VM de servicio en la nube implementado sin implementarla?
No se puede cambiar el tamaño de la máquina virtual de Hola de un servicio en la nube implementado sin implementarla. Hola tamaño de máquina virtual se integra en hello CSDEF, que solo se puede actualizar con una nueva implementación.

Para obtener más información, consulte [cómo tooupdate un servicio de nube](cloud-services-update-azure-service.md).

 
