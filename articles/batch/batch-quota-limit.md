---
title: "aaaService las cuotas y límites de lote de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las cuotas de lote de Azure de forma predeterminada, los límites y restricciones, y cómo aumenta la cuota de toorequest"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Límites y cuotas del servicio Lote

Como con otros servicios de Azure, hay límites en determinados recursos asociados con hello servicio por lotes. Muchos de estos límites son cuotas predeterminado que se aplican por Azure en el nivel de cuenta o suscripción de Hola. En este artículo se describen esos valores predeterminados y cómo solicitar un aumento de la cuota.

Tenga presente estas cuotas cuando diseñe y escale las cargas de trabajo de Lote. Por ejemplo, si el grupo no alcance el número de destino de Hola de nodos de proceso que ha especificado, podría ha alcanzado el límite de cuota de núcleos de Hola para su cuenta de lote o una cuota de núcleos VM regional de su suscripción.

Puede ejecutar varias cargas de trabajo por lotes en una sola cuenta de lote, o distribuir las cargas de trabajo entre las cuentas de lote que se encuentran en hello misma suscripción, pero en diferentes regiones de Azure.

Si tiene previsto cargas de trabajo de producción de toorun en lote, deberá tooincrease una o varias de las cuotas de Hola por encima del valor predeterminado de Hola. Si desea tooraise una cuota, puede abrir en línea [solicitud de soporte técnico al cliente](#increase-a-quota) sin cargo.

> [!NOTE]
> Una cuota es un límite de crédito, no una garantía de capacidad. Si tiene necesidades de capacidad a gran escala, póngase en contacto con el soporte técnico de Azure.
> 
> 

## <a name="resource-quotas"></a>Cuotas de recursos
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Cuotas en el modo de suscripción de usuario

Para una cuenta de lote con el modo de asignación de grupo establecido demasiado**suscripción usuario**, las máquinas virtuales y otros recursos, como las cuentas de almacenamiento por lotes, se crean directamente en su suscripción cuando se crea un grupo. cuota de núcleos de Hello Azure Batch no aplica a cuenta de tooan creada en este modo. En su lugar, se aplican las cuotas de hello en la suscripción de núcleos de proceso regionales y otros recursos. Aprenda más sobre estas cuotas en [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).

Al planear el uso de recursos para una cuenta creada en el modo de suscripción de usuario, Hola nota después de recursos de proceso por lotes (de núcleos de suma toocompute) son necesarias para cada 40 máquinas virtuales de Linux o 20 máquinas virtuales de Windows:

| Recurso | Cuota | Proveedor |
| --- | ---| --- |
| Una cuenta de almacenamiento | Cuentas de almacenamiento | Microsoft.Storage |
| Una dirección IP pública | Direcciones IP públicas | Microsoft.Network | 
| Una red virtual | Redes virtuales | Microsoft.Network | 
| Un grupo de seguridad de red | Grupos de seguridad de red | Microsoft.Network | 
| Un conjunto de escalado de máquinas virtuales | Conjuntos de escalado de máquina virtual | Microsoft.Compute | 
| Un equilibrador de carga | Equilibradores de carga | Microsoft.Network | 

cuota de núcleos de Hola a nivel regional o por familia de máquina virtual debe ser correspondiente toohello VM tamaño del espacio necesario para el grupo de proceso por lotes o grupos:

| Quota | Proveedor |
| --- | ---- |
| N.º total de núcleos regionales | Microsoft.Compute |
| … Núcleos de familia | Microsoft.Compute |



## <a name="other-limits"></a>Otros límites
| **Recurso** | **Límite máximo** |
| --- | --- |
| [Tareas simultáneas](batch-parallel-node-tasks.md) por nodo de proceso |4 × número de núcleos de nodo |
| [Aplicaciones](batch-application-packages.md) por cuenta de Lote |20 | |
| Paquetes de aplicación por aplicación |40 |
| Tamaño del paquete de aplicación (cada uno) |Aprox. 195 GB<sup>1</sup> |
| Tamaño máximo de la tarea de inicio | 32 768 caracteres<sup>2</sup> |

<sup>1</sup> Límite de Almacenamiento de Azure para el tamaño máximo de blob en bloques<br />
<sup>2</sup> Incluye archivos de recursos y variables de entorno

## <a name="view-batch-quotas"></a>Visualización de las cuotas de Lote
Ver las cuotas de la cuenta de lote en hello [portal de Azure][portal].

1. Seleccione **por lotes cuentas** en el portal de hello, a continuación, seleccione cuenta de lote de Hola que le interesa.
2. Seleccione **propiedades** en la hoja de menú de la cuenta de hello por lotes.
3. hoja de propiedades de Hello muestra hello **cuotas** aplicados actualmente toohello cuenta de lote
   
    ![Cuotas de la cuenta de Lote][account_quotas]

Una cuenta de lote que se crea en modo de suscripción de usuario, Hola vista relacionado con las cuotas de suscripción en hello Portal de Azure.

1. Seleccione **suscripciones**y seleccione la suscripción de Hola que estás usando para hello cuenta de lote.

2. En hello **suscripción** hoja, seleccione **uso + cuotas**.



## <a name="increase-a-quota"></a>Aumento de la cuota
Siga estos toorequest pasos aumentar una cuota para su cuenta de lote o en la suscripción con hello [portal de Azure][portal]. tipo de Hola de aumento de la cuota depende de modo de asignación de grupo de Hola de su cuenta de lote.

### <a name="increase-a-batch-cores-quota"></a>Aumento de la cuota de núcleos de Batch 

Si se creó su cuenta de lote en **por lotes servicio** modo, siga estas toorequest pasos aumento de la cuota de núcleos de proceso por lotes:

1. Seleccione hello **ayuda y soporte técnico** icono en el panel del portal u Hola signo de interrogación (**?**) en la esquina superior derecha de hello del portal de Hola.
2. Seleccione **Nueva solicitud de soporte técnico** > **Básico**.
3. En hello **Fundamentos** hoja:
   
    a. **Tipo de problema** > **Cuota**
   
    b. Seleccione su suscripción.
   
    c. **Tipo de cuota** > **Batch**
   
    d. **Plan de soporte técnico** > **Compatibilidad con cuotas (incluida)**
   
    Haga clic en **Siguiente**.
4. En hello **problema** hoja:
   
    a. Seleccione un **gravedad** según tooyour [impacto para la empresa][support_sev].
   
    b. En **detalles**, especifique cada cuota que desea toochange, nombre de cuenta de lote de Hola y límite nuevo Hola.
   
    Haga clic en **Siguiente**.
5. En hello **información de contacto** hoja:
   
    a. Seleccione un valor en **Método de contacto preferido**.
   
    b. Compruebe y escriba los detalles de contacto de hello necesario.
   
    Haga clic en **crear** solicitud de soporte técnico de toosubmit Hola.

Una vez que haya enviado la solicitud de soporte técnico, el servicio de soporte técnico de Azure se comunicará con usted. Tenga en cuenta que la finalización de la solicitud de Hola puede tardar hasta días laborables de too2.

### <a name="increase-a-subscription-cores-quota"></a>Aumento de una cuota de núcleos de suscripción

Si su cuenta de Batch se creó en el modo de **suscripción de usuario** y necesita más núcleos regionales o de familia de máquina virtual, solicite un aumento de la cuota en su suscripción. Para ver los pasos, consulte [Solicitudes de aumento de cuota de núcleos de Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Temas relacionados
* [Crear una cuenta de Azure Batch mediante Hola portal de Azure](batch-account-create-portal.md)
* [Información general de las características de Lote de Azure](batch-api-basics.md)
* [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
