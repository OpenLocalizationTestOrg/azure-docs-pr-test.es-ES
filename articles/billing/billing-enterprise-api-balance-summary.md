---
title: "aaaAzure las API de empresa de facturación: equilibrio y resumen | Documentos de Microsoft"
description: "Obtenga información acerca del uso de facturación de Azure y RateCard APIs, que son visiones tooprovide usado del consumo de recursos de Azure y tendencias."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>API de informes para clientes de Enterprise: saldos y resumen

Hola saldo y API de resumen le ofrece un resumen de información sobre saldos, nuevas adquisiciones, cargos de servicios de Azure Marketplace, ajustes y cargos por encima del límite mensual.


##<a name="request"></a>Solicitud 
Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md). Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven.

|Método | URI de solicitud|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.
>

## <a name="response"></a>Response

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Definiciones de propiedad de respuesta**

|Nombre de propiedad| Tipo| Descripción
|-|-|-|
|id|cadena|Hola Id. único para la inscripción y un período de facturación específico|
|billingPeriodId|cadena |Hola Id. del período de facturación|
|currencyCode|cadena |código de divisa de Hola|
|beginningBalance|Decimal| saldo inicial de Hola Hola período de facturación|
|endingBalance|Decimal| Hola saldo final de período de facturación de hello (para períodos abiertos se actualizarán cada día)|
|newPurchases|Decimal| Cantidad total de nuevas compras|
|adjustments|Decimal| Importe total de ajuste|
|utilized|Decimal| Uso total de compromiso|
|serviceOverage|Decimal| Uso por encima del límite de servicios de Azure|
|chargesBilledSeparately|Decimal| Gastos facturados por separado|
|totalOverage|Decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|Decimal| Compromiso de servicio de Azure + uso por encima del límite total|
|azureMarketplaceServiceCharges|Decimal| Gastos totales de Azure Marketplace|
|newPurchasesDetails|Matriz de cadenas JSON de pares de nombre y valor|Lista de nuevas compras|
|adjustmentDetails|Matriz de cadenas JSON de pares de nombre y valor|Lista de ajustes (crédito promocional, crédito SIE, etc.) |


<br/>
## <a name="see-also"></a>Otras referencias

* [API de períodos de facturación](billing-enterprise-api-billing-periods.md)

* [API de detalles de uso](billing-enterprise-api-usage-detail.md) 

* [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API de hoja de precios](billing-enterprise-api-pricesheet.md)