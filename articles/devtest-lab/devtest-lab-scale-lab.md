---
title: "aaaScale las cuotas y límites en el laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale un laboratorio de prácticas de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Escalado de cuotas y límites en DevTest Labs
Cuando se trabaja en los laboratorios de desarrollo y pruebas, podría Observe que hay determinado toosome de límites de forma predeterminada los recursos de Azure, lo que pueden afectar al servicio de laboratorios de desarrollo y pruebas de Hola. Estos límites son los que se hace referencia tooas **cuotas**.

> [!NOTE]
> Hola servicio laboratorios de desarrollo y pruebas no impone cuotas. Las cuotas que pueden surgir son restricciones default de hello suscripción de Azure en general.

Puede usar cada recurso de Azure hasta que alcance su cuota. Cada suscripción tiene cuotas independientes y se realiza el seguimiento del uso para cada suscripción.

Por ejemplo, cada suscripción tiene una cuota predeterminada de 20 núcleos. Por lo tanto, si va a crear en el laboratorio máquinas virtuales con cuatro núcleos, solo puede crear cinco. 

[Suscripción de Azure y límites de servicio](https://docs.microsoft.com/azure/azure-subscription-service-limits) se enumeran algunas de las cuotas más comunes de Hola para recursos de Azure. Hola suelen usados en un laboratorio de recursos, y para que pueden surgir cuotas, incluir núcleos de la máquina virtual, las direcciones IP públicas, interfaz de red, discos administrados, asignación de roles RBAC y circuitos ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Visualización del uso y las cuotas
Estos pasos muestra cómo tooview Hola cuotas actuales en su suscripción a recursos específicos de Azure y toosee qué porcentaje de cada cuota ha usado.

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **facturación** de lista de Hola.
1. En la hoja de facturación de hello, seleccione una suscripción.
4. Seleccione **Uso y cuotas**.

   ![Botón Uso y cuotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Hola uso + cuotas hoja aparecerá una lista de diferentes recursos disponibles en ese porcentaje hello y suscripción de cuota de Hola que se utiliza por recurso.

   ![Cuotas y uso](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Solicitud de más recursos en la suscripción
Si alcanza un límite de cuota, límite predeterminado de Hola de un recurso en una suscripción se puede aumentar la longitud máxima tooa, tal y como se describe en [suscripción a Azure y límites de servicio](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Estos pasos muestra cómo toorequest una cuota aumentar a través de hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seleccione **Más servicios**, **Facturación**, y **Uso y cuotas**.
1. En Hola uso + hoja de cuotas, seleccione hello **solicitar aumentar** botón.

   ![Botón Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete y enviar solicitud de hello, rellene la información de hello necesario en todas las tres pestañas de hello **nueva solicitud de soporte técnico** formulario.

   ![Formulario Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Límites de Azure de descripción y aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) proporciona más información acerca de cómo ponerse en contacto con soporte técnico de Azure toorequest una cuota de aumento.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Pasos siguientes
* Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
