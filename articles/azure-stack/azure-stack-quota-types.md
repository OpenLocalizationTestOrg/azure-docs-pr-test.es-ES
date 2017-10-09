---
title: tipos de aaaQuota en la pila de Azure | Documentos de Microsoft
description: Revisar Hola cuotas diferentes tipos disponibles para los servicios y recursos de la pila de Azure.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: e05870603526a3e0e65d536cff98b9033524017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quota-types-in-azure-stack"></a>Tipos de cuota en Azure Stack
[Las cuotas](azure-stack-plan-offer-quota-overview.md#plans) definir límites de Hola de recursos que se puede aprovisionar o utilizar una suscripción de usuario. Por ejemplo, una cuota puede permitir un toocreate usuario seguridad toofive máquinas virtuales. Cada recurso puede tener sus propios tipos de cuotas.

## <a name="compute-quota-types"></a>Tipos de cuota de proceso
| **Tipo** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de máquinas virtuales |50 | número máximo de Hola de máquinas virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de núcleos de máquinas virtuales |100 | Hola número máximo de núcleos que puede crear una suscripción en esta ubicación (por ejemplo, una máquina virtual de A3 tiene cuatro núcleos). |
| Número máximo de conjuntos de disponibilidad |10 | número máximo de Hola de conjuntos de disponibilidad que se pueden crear en esta ubicación. |
| Número máximo de conjuntos de escalado de máquinas virtuales |100 | número máximo de Hola de conjuntos de escalas de máquina virtual que se pueden crear en esta ubicación. |

> [!NOTE]
> Las cuotas de proceso no se aplican a esta versión preliminar técnica.
> 
> 

## <a name="storage-quota-types"></a>Tipos de cuotas de almacenamiento
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Capacidad máxima (GB) |500 |Capacidad de almacenamiento total que puede consumir una suscripción en esta ubicación. |
| Número total de cuentas de almacenamiento |20 | |número máximo de Hola de cuentas de almacenamiento que se puede crear una suscripción en esta ubicación. |

## <a name="network-quota-types"></a>Tipos de cuota de red
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de direcciones IP públicas |50 |número máximo de Hola de direcciones IP públicas que puede crear una suscripción en esta ubicación. |
| Número máximo de redes virtuales |50 |número máximo de Hola de redes virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de puertas de enlace de red virtual |1 |número máximo de Hola de red virtual puertas de enlace (puertas de enlace de VPN) que puede crear una suscripción en esta ubicación. |
| Número máximo de conexiones de red |2 |número máximo de Hola de conexiones de red (punto a punto o sitio a sitio) que puede crear una suscripción a través de todas las puertas de enlace de red virtual en esta ubicación. |
| Número máximo de equilibradores de carga |50 |número máximo de Hola de equilibradores de carga que puede crear una suscripción en esta ubicación. |
| Nº máx. NIC |100 |número máximo de Hola de interfaces de red que puede crear una suscripción en esta ubicación. |
| Número máximo de grupos de seguridad de red |50 |número máximo de Hola de grupos de seguridad de red que puede crear una suscripción en esta ubicación. |

## <a name="view-an-existing-quota"></a>Visualización de una cuota existente
1. Haga clic en **Más servicios** > **Proveedores de recursos**.
2. Seleccione servicio de hello con una cuota de Hola que desea tooview.
3. Haga clic en **cuotas**y la cuota de hello seleccione desea tooview.

## <a name="next-steps"></a>Pasos siguientes
[Más información acerca de planes, ofertas y cuotas.](azure-stack-plan-offer-quota-overview.md)

[Crear cuotas durante la creación de un plan.](azure-stack-create-plan.md)
