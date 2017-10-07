---
title: "consumo de dirección IP público de aaaView en pila de Azure | Documentos de Microsoft"
description: "Los administradores pueden ver el consumo de Hola de direcciones IP públicas de una región"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 0f77be49-eafe-4886-8c58-a17061e8120f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/18/2017
ms.author: scottnap
ms.openlocfilehash: 771c011d133a030218b011cf94bbb8055f8996ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a>Visualización del consumo de direcciones IP públicas en Azure Stack
Como un administrador de la nube, puede ver el número de Hola de direcciones IP públicas que hayan sido asignadas tootenants, número de Hola de direcciones IP públicas que siguen estando disponibles para la asignación y el porcentaje de Hola de direcciones IP públicas que se han asignado en el que ubicación.

Hola **uso de grupos de IP pública** icono muestra el número total de Hola de direcciones IP públicas que se hayan consumido en todos los grupos de direcciones IP públicos en el tejido de hello, si se han utilizado para el inquilino IaaS VM instancias, tejido Servicios de infraestructura o recursos de dirección IP públicos que se crearon explícitamente los inquilinos.

Hola propósito de este icono es una idea de hello al número total de direcciones IP públicas que se hayan consumido en esta ubicación de los administradores de Azure pila toogive. lo que les ayuda a determinar si se están quedando sin algún recurso.

En hello **proveedores de recursos**, **red** hoja, hello **direcciones IP públicas** elemento de menú en **recursos del inquilino** muestra solo los usuarios direcciones IP públicas que se han *creadas de manera explícita por parte de inquilinos*. Hola como tal, número de **usado** direcciones IP públicas en hello **uso de grupos de IP pública** mosaico siempre es diferente de (mayor que) Hola número en hello **direcciones IP públicas** icono en **recursos del inquilino**.

## <a name="view-hello-public-ip-address-usage-information"></a>Ver información de uso en la dirección IP de hello pública
número total de Hola de tooview de direcciones IP públicas que se hayan consumido en la región de hello:

1. En el portal de administración de la pila de Azure de hello, haga clic en **más servicios**, en **recursos administrativos**, haga clic en **proveedores de recursos**.
2. En lista de Hola de **proveedores de recursos**, seleccione **red**.
3. Hola **red** hoja muestra hello **uso de grupos de IP pública** disponer en mosaico en hello **Introducción** sección.

![Hoja de proveedor de recursos de red](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

Tenga en cuenta que hello **usado** número representa el número de Hola de direcciones IP públicas de todos los grupos públicos de dirección IP en esa ubicación que están asignados. Hola **libre** Hola de número representa el número de direcciones IP públicas de todos los grupos de direcciones IP públicas que no se ha asignado y siguen estando disponibles. Hola **porcentaje usado** número representa el número de Hola de usar o direcciones de asignación como un porcentaje del número total de Hola de direcciones IP públicas de todos los grupos de direcciones IP públicas en esa ubicación.

## <a name="view-hello-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a>Vista Hola direcciones IP públicas que se crearon las suscripciones de inquilinos
toosee una lista de direcciones IP públicas que se crearon explícitamente las suscripciones de inquilinos en una región específica, haga clic en **direcciones IP públicas** en **recursos del inquilino**.

![Direcciones IP públicas de inquilinos](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

Puede observar que algunas direcciones IP públicas que hayan sido asignadas dinámicamente aparecen en la lista de hello pero no tiene una dirección asociada a ellos aún. Esto es porque el recurso de dirección Hola aún se ha creado en el proveedor de recursos de red, pero no en hello controladora de red.

Hola controladora de red no asigna un recurso de toothis dirección hasta que esté realmente enlazado tooan interfaz, una tarjeta de interfaz de red (NIC), un equilibrador de carga o una puerta de enlace de red virtual. Cuando la dirección IP pública hello es la interfaz de tooan enlazado, Hola controladora de red asigna una tooit de dirección IP y aparece en hello **dirección** campo.

## <a name="view-hello-public-ip-address-information-summary-table"></a>Vista Hola pública información resumen tabla de direcciones IP
Hay una serie de casos diferentes en el que se asignan direcciones IP públicas que determinan si dirección Hola aparece en una lista o en otro.

| **Caso de asignación de dirección IP pública** | **Aparece en resumen de uso** | **Aparece en lista de direcciones IP públicas de inquilinos** |
| --- | --- | --- |
| Dirección IP pública dinámica todavía no están asignados equilibrador de carga o NIC de tooan (temporal) |No |Sí |
| La dirección IP pública dinámica asignado tooan equilibrador de carga o NIC. |Sí |Sí |
| Dirección IP pública estática había asignado a tooa inquilino equilibrador de carga o NIC. |Sí |Sí |
| Estática pública IP dirección asignada tooa tejido infraestructura extremo de servicio. |Sí |No |
| Dirección IP pública implícitamente creado para instancias de VM de IaaS y usa para NAT de salida en la red virtual de Hola. Estos se crean entre bastidores de hello cada vez que un inquilino crea una instancia de máquina virtual para que las máquinas virtuales pueden enviar información a toohello Internet. |Sí |No |

## <a name="next-steps"></a>Pasos siguientes
[Administración de cuentas de almacenamiento en Azure Stack](azure-stack-manage-storage-accounts.md)