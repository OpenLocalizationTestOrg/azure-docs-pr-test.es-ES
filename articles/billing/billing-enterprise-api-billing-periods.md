---
title: "aaaAzure Enterprise API de facturación - períodos de facturación | Documentos de Microsoft"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>API de informes para clientes de Enterprise: períodos de facturación

Hola API de períodos de facturación devuelve una lista de períodos que tienen datos de consumo para Hola de facturación especificado inscripción en orden cronológico inverso. Cada período contiene una propiedad que señala la ruta de la API de toohello para cuatro conjuntos de datos - BalanceSummary, UsageDetails, Marktplace cargos y PriceSheet de Hola. Si el período de hello no tiene datos, propiedad correspondiente de hello es null. 


##<a name="request"></a>Solicitud 
Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md). 

|Método | URI de solicitud|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.
>

## <a name="response"></a>Response
 
    
    
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
|billingPeriodId| cadena| Hola identificador único que representa un período de facturación determinado|
|billingStart| datetime| Cadena de ISO 8601 que representa la fecha de inicio del periodo de Hola|
|billingEnd| datetime| Cadena de ISO 8601 que representa la fecha de finalización del periodo de Hola|
|balanceSummary| cadena| la ruta de acceso de dirección URL de Hola que enruta los datos de resumen de Balance de toohello para este período|
|usageDetails| cadena| la ruta de acceso de dirección URL de Hola que enruta los datos de detalles de uso de toohello para este período|
|marketplaceCharges| cadena| la ruta de acceso de dirección URL de Hola que enruta los datos de cargos de Marketplace de toohello para este período|
|priceSheet| cadena| la ruta de acceso de dirección URL de Hola que enruta toohello PriceSheet datos para este período|

<br/>
## <a name="see-also"></a>Otras referencias

* [API de saldo y resumen](billing-enterprise-api-balance-summary.md)

* [API de detalles de uso](billing-enterprise-api-usage-detail.md) 

* [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API de hoja de precios](billing-enterprise-api-pricesheet.md)