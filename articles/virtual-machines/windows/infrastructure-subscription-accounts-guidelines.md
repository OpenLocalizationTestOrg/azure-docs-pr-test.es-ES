---
title: "aaaSubscription y cuentas para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para las suscripciones y cuentas en Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Directrices de suscripción y cuentas de Azure para máquinas virtuales Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

En este artículo se centra en describir cómo tooapproach suscripción y administración de cuentas como su entorno y la base de usuarios crece.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Instrucciones de implementación de suscripciones y cuentas
Decisiones:

* ¿Qué conjunto de suscripciones y cuentas ¿necesita toohost su infraestructura o la carga de trabajo de TI?
* ¿Cómo toobreak hacia abajo Hola jerarquía toofit su organización?

Tareas:

* Definir la jerarquía de organización lógica como le gustaría toomanage desde un nivel de suscripción.
* toomatch esta jerarquía lógica, definir cuentas Hola necesarias y las suscripciones en cada cuenta.
* Crear conjunto de Hola de suscripciones y cuentas que utilizan la convención de nomenclatura.

## <a name="subscriptions-and-accounts"></a>Suscripciones y cuentas 
toowork con Azure, necesita una o varias suscripciones de Azure. Existen recursos como redes o máquinas virtuales en esas suscripciones.

* Los clientes empresariales suelen tengan una inscripción Enterprise, que es Hola recurso de más arriba en la jerarquía de Hola y está asociado tooone o más cuentas.
* Para los consumidores y los clientes sin una inscripción Enterprise, recursos de nivel superior de hello es la cuenta de hello.
* Las suscripciones son tooaccounts asociado, y puede haber una o varias suscripciones por cuenta. Registros de Azure información en el nivel de suscripción de Hola de facturación.

Pagar toohello el límite de niveles de jerarquía de dos de la relación de suscripción o cuenta de hello, es importante tooalign Hola convención de nomenclatura toohello suscripciones y cuentas de facturación necesidades. Por ejemplo, si una empresa global usa Azure, puede elegir cuenta toohave uno por cada región y se administran las suscripciones en Hola nivel región:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Por ejemplo, puede usar Hola siguiente estructura:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Si una región decide toohave más de grupo determinado de una suscripción tooa asociado, convención de nomenclatura de hello debe incorporar una tooencode de manera Hola datos adicionales en la cuenta de Hola o nombre de la suscripción de Hola. Esta organización permite corporativos facturación datos toogenerate Hola nuevos niveles de jerarquía durante la facturación de informes:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

organización de Hello podría verse como el siguiente ejemplo de Hola:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Microsoft proporciona una facturación detallada a través de un archivo descargable para una sola cuenta o para todas las cuentas de un contrato Enterprise.

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

