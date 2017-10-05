---
title: "API de facturación de Azure Enterprise - Períodos de facturació| Microsoft Docs"
description: "Obtenga información acerca de las API de informes que permiten a los clientes de Azure Enterprise extraer datos de consumo mediante programación."
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>API de informes para clientes de Enterprise: períodos de facturación

La API de períodos de facturación devuelve una lista de períodos de facturación que tienen datos de consumo para la inscripción especificada en orden cronológico inverso. Cada período contiene una propiedad que señala a la ruta de la API para los cuatro conjuntos de datos: BalanceSummary, UsageDetails, Marketplace Charges y PriceSheet. Si el período no tiene datos, la propiedad correspondiente es null. 


##<a name="request"></a>Solicitud 
Las propiedades de encabezado comunes que tienen que agregarse se especifican [aquí](billing-enterprise-api.md). 

|Método | URI de solicitud|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> Para usar la versión preliminar de la API, reemplace v2 por v1 en la dirección URL anterior.
>

## <a name="response"></a>Respuesta
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Definiciones de propiedad de respuesta**

|Nombre de propiedad| Tipo| Descripción
|-|-|-|
|billingPeriodId| cadena| El identificador único que representa un período de facturación determinado|
|billingStart| datetime| Cadena ISO 8601 que representa la fecha de inicio del período|
|billingEnd| datetime| Cadena ISO 8601 que representa la fecha de finalización del período|
|balanceSummary| cadena| La ruta de acceso de la dirección URL que se enruta a los datos de resumen de saldos para este período|
|usageDetails| cadena| La ruta de acceso de la dirección URL que se enruta a los datos de detalles de uso para este período|
|marketplaceCharges| cadena| La ruta de acceso de la dirección URL que se enruta a los datos de gastos en Marketplace para este período|
|priceSheet| cadena| La ruta de acceso de la dirección URL que se enruta a los datos de PriceSheet para este período|

<br/>
## <a name="see-also"></a>Otras referencias

* [API de saldo y resumen](billing-enterprise-api-balance-summary.md)

* [API de detalles de uso](billing-enterprise-api-usage-detail.md) 

* [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API de hoja de precios](billing-enterprise-api-pricesheet.md)