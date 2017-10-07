---
title: "aaaAzure las API de empresa de facturación: PriceSheet | Documentos de Microsoft"
description: "Obtenga información acerca de hello las API de generación de informes que permiten a los datos de consumo de Azure Enterprise los clientes toopull mediante programación."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>API de informes para clientes de Enterprise: hoja de precios

Hola API de la hoja de precios ofrece tasa aplicable de Hola de cada medidor para hello dada la inscripción y el período de facturación.

##<a name="request"></a>Solicitud
Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md). Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven.

|Método | URI de solicitud|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.
>

## <a name="response"></a>Response

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Si usas Hola API de vista previa, meterId campo no está disponible.
>

**Definiciones de propiedad de respuesta**

|Nombre de propiedad| Tipo| Descripción
|-|-|-|
|id| cadena| Hola identificador único que representa un elemento determinado de PriceSheet (metros por período de facturación)|
|billingPeriodId| cadena| Hola identificador único que representa un período de facturación determinado|
|meterId| cadena| identificador de Hello para el medidor de Hola. Puede ser asignado toohello uso meterId.|
|meterName| cadena| nombre de contador de Hola|
|unitOfMeasure| cadena| Hola unidad de medida para medir el servicio de Hola|
|includedQuantity| Decimal| Cantidad que se incluye |
|partNumber| cadena| número de pieza de Hello asociada Hola medidor|
|unitPrice| Decimal| precio por unidad Hello para el medidor de Hola|
|currencyCode| cadena| código de moneda de Hola para unitPrice Hola|
<br/>
## <a name="see-also"></a>Otras referencias

* [API de períodos de facturación](billing-enterprise-api-billing-periods.md)

* [API de detalles de uso](billing-enterprise-api-usage-detail.md)

* [API de saldo y resumen](billing-enterprise-api-balance-summary.md)

* [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md)
