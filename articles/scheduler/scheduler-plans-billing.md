---
title: "aaaPlans y facturación en el programador de Azure"
description: "Planes y facturación en Programador de Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Planes y facturación en Programador de Azure
## <a name="job-collection-plans"></a>Planes de colección de trabajos
Colecciones de trabajos son entidades facturables de hello en el programador de Azure. Las colecciones de trabajos contienen varios trabajos y vienen en tres planes que se describen a continuación: Gratis, Standard y Premium.

| **Plan de colección de trabajos** | **Nº máximo de trabajos por colección de trabajos** | **Periodicidad máxima** | **N.º máximo de colecciones de trabajo por suscripción** | **Límites** |
|:--- |:--- |:--- |:--- |:--- |
| **Gratis** |5 trabajos por colección de trabajos |Una vez por hora. No se pueden ejecutar trabajos con una frecuencia superior a una vez por hora |Se permite una suscripción de una colección de trabajos gratuita too1 |No se puede usar un [objeto de autorización saliente HTTP](scheduler-outbound-authentication.md) |
| **Standard** |50 trabajos por colección de trabajos |Una vez por minuto. No se pueden ejecutar trabajos con una frecuencia superior a una vez por minuto |Se permite una suscripción de seguridad de las colecciones de trabajos estándar too100 |Conjunto de características de acceso toofull del programador |
| **Premium P10** |50 trabajos por colección de trabajos |Una vez por minuto. No se pueden ejecutar trabajos con una frecuencia superior a una vez por minuto |Una suscripción se permite una too10, 000 colecciones de trabajos P10 Premium. <a href="mailto:wapteams@microsoft.com">Póngase en contacto con nosotros</a> para obtener más información. |Conjunto de características de acceso toofull del programador |
| **Premium P20** |1000 trabajos por colección de trabajos |Una vez por minuto. No se pueden ejecutar trabajos con una frecuencia superior a una vez por minuto |Una suscripción se permite una too10, colecciones de trabajos de Premium P20 000. <a href="mailto:wapteams@microsoft.com">Póngase en contacto con nosotros</a> para obtener más información. |Conjunto de características de acceso toofull del programador |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Actualizaciones y degradaciones de planes de colección de trabajos
Puede actualizar o degradar un plan de recopilación de trabajo en cualquier momento entre los planes de hello gratuito, estándar y Premium. Sin embargo, al degradar la colección de trabajos gratuita tooa, degradación de hello puede producir un error de uno de hello siguientes motivos:

* Una colección de trabajos gratuita ya existe en la suscripción de Hola
* Un trabajo en la colección de trabajos de hello tiene una frecuencia superior a la permitida para los trabajos en colecciones de trabajos gratuitas. periodicidad máxima Hola permitido en una colección de trabajos gratuita es una vez por hora
* Hay más de 5 trabajos en la colección de trabajos de Hola
* Un trabajo en la colección de trabajos de hello tiene una acción HTTP o HTTPS que usa un [objeto de salida de autorización de HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Planes de Azure y facturación
Las suscripciones no se cobran en colecciones de trabajos gratuitas. Si tiene más de 100 colecciones de trabajos estándar (10 facturación unidades standard), es una mejor toohave de solución para las colecciones de todos los trabajos en el plan de premium Hola.

Si tiene una colección de trabajos estándar y una colección de trabajos premium, se le facturará una unidad de facturación estándar *y* una unidad de facturación premium. Hola facturas de servicio de programador según el número de Hola de colecciones de trabajo activo que se establecen tooeither standard o premium; Esto se explica con más detalle en hello dos secciones siguientes.

## <a name="standard-billable-units"></a>Unidades facturables estándar
Una unidad facturable estándar puede incluir una too10 colecciones de trabajos estándar. Puesto que una colección de trabajos estándar puede tener hasta too50 trabajos por la colección de trabajos, una unidad de facturación estándar permite un toohave suscripción trabajo too500: seguridad de ejecuciones de trabajos de 22 millones de tooalmost al mes.

Si tiene entre 1 y 10 colecciones de trabajos estándar, se le facturará 1 unidad de facturación estándar. Si tiene entre 11 y 20 colecciones de trabajos estándar, se le facturarán 2 unidades de facturación estándar. Si tiene entre 21 y 30 colecciones de trabajos estándar, se le facturarán 3 unidades de facturación estándar.

## <a name="p10-premium-billable-units"></a>Unidades facturables premium P10
Una unidad facturable de P10 premium puede incluir una too10, colecciones de trabajos de 000 P10 premium. Puesto que una colección de trabajos de P10 premium puede tener hasta too50 trabajos por la colección de trabajos, una unidad de facturación premium permite un toohave suscripción seguridad too500, 000 trabajos: seguridad tooalmost mil millones de 22 ejecuciones de trabajos al mes.

Si tiene entre 1 y 10 000 colecciones de trabajos premium, se le facturará 1 unidad de facturación premium P10. Si tiene entre 10 001 y 20 000 colecciones de trabajos premium, se le facturarán 2 unidades de facturación premium P10.

Por lo tanto, las colecciones tienen un trabajo premium de P10 Hola misma funcionalidad como las colecciones de trabajos estándar de hello pero proporcionan un salto de precio en caso de que la aplicación requiere una gran cantidad de colecciones de trabajos.

## <a name="p20-premium-billable-units"></a>Unidades facturables premium P20
Puede incluir una unidad facturable de premium P20 seguridad too5, colecciones de trabajos de premium P20 000. Puesto que puede tener una colección de trabajos de premium P20 hasta too1, 000 trabajos para cada colección de trabajos, una unidad de facturación premium permite un toohave suscripción seguridad too5, 000 000 trabajos – seguridad tooalmost mil millones de 220 ejecuciones de trabajos al mes.

Colecciones de trabajos de premium P20 proporciona Hola mismas capacidades como colecciones de trabajos de P10 premium, pero también admite un número mayor los trabajos por la colección de trabajos y el mayor número total de trabajos globales que P10 premium permitiendo toohave mayor escalabilidad.

## <a name="billing-and-active-status"></a>Estado de facturación y activo
Colecciones de trabajos siempre están activas, a menos que toda la suscripción entra en un estado deshabilitado temporal debido a problemas de toobilling. Hello solo tooensure de manera que no se cobra una colección de trabajos es tooeither establezca toohello *libre* plan o toodelete colección de trabajos de Hola.

Aunque puede deshabilitar todos los trabajos dentro de una colección de trabajos en una sola operación, no cambia el estado de facturación de Hola de colección de trabajos de hello: colección de trabajos de hello le *todavía* facturará. De forma similar, las colecciones de trabajos vacías se consideran activas y se facturarán.

## <a name="pricing"></a>Precios
Para obtener información detallada sobre los precios, vea [Precios de Programador](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Conceptos, terminología y jerarquía de entidades de Programador de Azure](scheduler-concepts-terms.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad de Programador de Azure](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

 [Autenticación de salida de Programador de Azure](scheduler-outbound-authentication.md)

