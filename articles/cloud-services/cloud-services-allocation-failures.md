---
title: "Error de asignación de servicio en la nube aaaTroubleshooting | Documentos de Microsoft"
description: "Solución de errores de asignación al implementar Servicios en la nube de Azure"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Solución de errores de asignación al implementar Servicios en la nube de Azure
## <a name="summary"></a>Resumen
Al implementar instancias tooa servicio en la nube o agregar nuevo sitio web o instancias de rol de trabajo, Windows Azure asigna recursos de proceso. En ocasiones, puede recibir errores al realizar estas operaciones, incluso antes de llegar a los límites de suscripción de Azure Hola. Este artículo explica causas Hola de algunos de los errores de asignación comunes de Hola y sugiere posibles correcciones. información de Hello también puede resultarle útil cuando planee la implementación de Hola de sus servicios.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Información de contexto: cómo funciona la asignación
servidores de Hello en centros de datos de Azure se dividen en clústeres. Se intenta una nueva solicitud de asignación de servicio en la nube en varios clústeres. Cuando primera instancia de hello es servicio de nube de implementada tooa (en almacenamiento provisional o producción), que el servicio de nube obtiene clúster tooa anclados. Ningún otro implementaciones para servicio de nube de hello tendrá lugar en hello mismo clúster. En este artículo, nos referiremos toothis como "anclado tooa clúster". Diagrama 1 a continuación ilustra el caso de hello de una asignación normal que se intenta en varios clústeres; Diagrama 2 ilustra caso de hello de una asignación que tooCluster anclado 2 ya que es donde Hola CS_1 de servicio de nube existente se hospeda.

![Diagrama de asignación](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>¿Por qué se producen errores de asignación?
Cuando una solicitud de asignación está anclado tooa clúster, hay una mayor probabilidad de errores toofind liberar recursos como grupo de recursos disponibles de hello es clúster tooa limitado. Además, si su solicitud de asignación está anclado tooa clúster pero tipo hello de recurso solicitado no es compatible con dicho clúster, se producirá un error en la solicitud incluso si el clúster de hello tiene recurso gratuito. Diagrama 3 a continuación ilustra el caso en Hola donde una asignación anclada produce un error porque Hola candidato solo clúster no tiene recursos libres. Diagrama 4 muestra caso Hola donde una asignación anclada produce un error porque no es compatible con clúster candidato solo de Hola Hola solicitado tamaño de máquina virtual, aunque el clúster de hello tiene liberar recursos.

![Error de asignaciones ancladas](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Solución de errores de asignación para servicios en la nube
### <a name="error-message"></a>Mensaje de error
Puede ver Hola mensaje de error siguiente:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Problemas comunes
Presentamos Hola comunes asignación los escenarios que provocan un asignación solicitud toobe tooa anclados solo clúster.

* A continuación, implementar tooStaging ranura: si un servicio de nube tiene una implementación en cualquier ranura, servicio de nube todo de Hola y está anclado tooa específico del clúster.  Esto significa que si una implementación ya existe en la ranura de producción de hello, a continuación, una nueva implementación de ensayo se solo pueden asignar en el mismo clúster según la zona de producción de hello de Hola. Si el clúster de hello está cerca de su capacidad, puede producir un error en la solicitud de saludo.
* Ajuste de escala: agregar nuevas instancias tooan servicio en la nube debe asignar Hola mismo clúster.  Normalmente, las solicitudes de escalado pequeño se pueden asignar, pero no siempre. Si el clúster de hello está cerca de su capacidad, puede producir un error en la solicitud de saludo.
* Grupo de afinidad: un nuevo servicio de nube vacía de tooan de implementación se puede asignar por tejido de Hola en cualquier clúster en dicha región, a menos que el servicio de nube de hello está anclado tooan grupo de afinidad. Toohello de las implementaciones se tratará el mismo grupo de afinidad en hello mismo clúster. Si el clúster de hello está cerca de su capacidad, puede producir un error en la solicitud de saludo.
* Red virtual del grupo de afinidad - redes virtuales anteriores estaban relacionados tooaffinity grupos en lugar de las regiones y servicios en la nube en estas redes virtuales sería clúster del grupo de afinidad toohello anclados. Tipo de toothis de las implementaciones de red virtual se tratará en clúster de hello anclado. Si el clúster de hello está cerca de su capacidad, puede producir un error en la solicitud de saludo.

## <a name="solutions"></a>Soluciones
1. Volver a implementar tooa nuevo servicio de nube - esta solución es probable toobe más correcta, ya que permite Hola plataforma toochoose de todos los clústeres en dicha región.

   * Implementar cargas de trabajo hello tooa nuevo servicio de nube  
   * Actualizar Hola CNAME o un registro toopoint tráfico toohello nuevo servicio en la nube
   * Una vez cero tráfico va toohello del sitio antiguo, puede eliminar servicio en la nube antiguo Hola. Esta solución debe incurrir en tiempo de inactividad cero.
2. Eliminar la producción y las ranuras de almacenamiento provisional: esta solución, conservará el nombre DNS existente, pero hará que la aplicación de tooyour de tiempo de inactividad.

   * Eliminar de producción de hello y ensayo ranuras de un servicio de nube existente para que el servicio en la nube Hola está vacía y, a continuación,
   * Cree una nueva implementación Hola existente del servicio en nube. Esto intentará volver a tooallocation en todos los clústeres en la región de Hola. Asegúrese de servicio de nube de hello no está ligada tooan grupo de afinidad.
3. Dirección IP reservada - esta solución, conservará la IP existentes de direcciones, pero hará que la aplicación de tooyour de tiempo de inactividad.  

   * Crear una dirección IP reservada para la implementación mediante Powershell.

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Siga #2 desde encima, realizar toospecify seguro Hola nueva dirección IP reservada en CSCFG del servicio de hello.
4. Quitar el grupo de afinidad para nuevas implementaciones - Ya no se recomienda utilizar grupos de afinidad. Siga los pasos para #1 anteriormente toodeploy un nuevo servicio de nube. Asegúrese de que el servicio en la nube no se encuentra en un grupo de afinidad.
5. Convertir tooa red Virtual Regional - vea [cómo toomigrate de grupos de afinidad tooa (VNet) de red Virtual Regional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
