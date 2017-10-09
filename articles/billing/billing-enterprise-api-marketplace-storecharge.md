---
title: "aaaAzure las API de empresa de facturación: cargos de Marketplace | Documentos de Microsoft"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>API de informes para clientes de Enterprise: gastos de la tienda Marketplace

Hola Marketplace almacén cargo API devuelve Hola marketplace basada en uso cargos desglose por día de hello especifica período de facturación o fechas de inicio y finalización (no se incluyen las cuotas de una vez).

##<a name="request"></a>Solicitud 
Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md). Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven. Intervalos de tiempo personalizado se pueden especificar con inicio de Hola y finalización los parámetros de fecha que se encuentran en tiempo de hello máximo admitida Hola formato aaaa-MM-dd, duración es de 36 meses.  

|Método | URI de solicitud|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.
>

## <a name="response"></a>Response
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Definiciones de propiedad de respuesta**

|Nombre de propiedad| Tipo| Descripción
|-|-|-|
|id|cadena|Identificador único para el artículo de costo de hello marketplace|
|subscriptionGuid|Guid|Hola Guid de la suscripción|
|subscriptionName|cadena|Hola, nombre de la suscripción|
|meterId|cadena|Id. de hello genera medidor|
|usageStartDate|DateTime|Hora de inicio de registro de uso de Hola|
|usageEndDate|DateTime|Hora de finalización de registro de uso de Hola|
|offerName|cadena|nombre de la oferta de Hola|
|resourceGroup|cadena|recursos de Hello grupo|
|instanceId|cadena|Identificador de instancia|
|additionalInfo|string|Cadena JSON de información adicional|
|etiquetas|cadena|Cadena JSON de etiqueta|
|orderNumber|cadena|número de pedido de Hola|
|unitOfMeasure|cadena|Unidad de medida para el medidor de Hola|
|costCenter|cadena|Centro de costo de Hola|
|accountId|int|Id. de cuenta de Hello|
|accountName|cadena |Nombre de la cuenta de Hello|
|accountOwnerId|cadena|Hola Id. de propietario de cuenta|
|departmentId|int|departamento de Hello Id.|
|departmentName|cadena|nombre del departamento de Hola|
|publisherName|cadena|nombre del publicador Hola|
|planName|cadena|nombre del Plan de Hola|
|consumedQuantity|Decimal|Cantidad consumida durante este período|
|resourceRate|Decimal|Precio por unidad de medidor Hola|
|extendedCost|Decimal|Gasto estimado según la cantidad consumida y el costo total|
<br/>
## <a name="see-also"></a>Otras referencias

* [API de períodos de facturación](billing-enterprise-api-billing-periods.md)

* [API de detalles de uso](billing-enterprise-api-usage-detail.md) 

* [API de saldo y resumen](billing-enterprise-api-balance-summary.md)

* [API de hoja de precios](billing-enterprise-api-pricesheet.md)