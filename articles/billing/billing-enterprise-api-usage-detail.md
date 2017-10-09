---
title: "aaaAzure las API de empresa de facturación: obtener detalles de uso | Documentos de Microsoft"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>API de informes para clientes de Enterprise: detalles de uso

Hola API de detalle de uso proporciona un desglose diario de cantidades consumidas y gastos estimados por una inscripción. resultado de Hello también incluye información sobre instancias, medidores y departamentos. Hola API se puede consultar por período de facturación o por una apertura especificada y la fecha de finalización. 
## <a name="consumption-apis"></a>API de consumo


##<a name="request"></a>Solicitud 
Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md). Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven. Intervalos de tiempo personalizado se pueden especificar con inicio de Hola y terminar los parámetros de fecha que se encuentran en hello formato aaaa-MM-dd. intervalo de tiempo máximo que compatibles Hello es 36 meses.  

|Método | URI de solicitud|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.
>

## <a name="response"></a>Response

> Pagar toohello volumen potencialmente grande de resultado de hello de datos se pagina conjunto. propiedad de nextLink Hello, si está presente, especifica vínculo Hola de página siguiente de Hola de datos. Si el vínculo de hello está vacío, indica que es Hola última página. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Definiciones de propiedad de respuesta**

|Nombre de propiedad| Tipo| Descripción
|-|-|-|
|id| cadena| Hola identificador único para la llamada de API de Hola. |
|data| Matriz JSON| Matriz de los detalles de uso diario para cada instance\meter Hola.|
|nextLink| cadena| Cuando hay más páginas de datos Hola nextLink puntos toohello URL tooreturn Hola página siguiente de datos. |
|accountId| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|productId| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|resourceLocationId| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|consumedServiceID| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|departmentId| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|accountOwnerEmail| cadena| Cuenta de correo electrónico del propietario de la cuenta de hello. |
|accountName| cadena| Nombre de cliente especificado de cuenta de hello. |
|serviceAdministratorId| cadena| Dirección de correo electrónico del administrador de servicios. |
|subscriptionId| int| Campo obsoleto. Presente por compatibilidad con versiones anteriores. |
|subscriptionGuid| cadena| Identificador único global para la suscripción de Hola. |
|subscriptionName| cadena| Nombre de suscripción de Hola. |
|fecha| cadena| fecha de Hello en el que ocurrió el consumo. |
|product| cadena| Detalles adicionales en el medidor de Hola. Ejemplo: A1 (VM) Windows - Este de Asia Pacífico|
|meterId| cadena| identificador de Hello para el medidor de Hola que emite el uso. |
|meterCategory| cadena| Hola servicio de la plataforma Windows Azure que se utilizó. |
|meterSubCategory| cadena| Define el tipo de servicio de Azure de Hola que puede afectar a la velocidad de Hola. Ejemplo : VM A1 (no Windows)|
|meterRegion| cadena| Identifica la ubicación de Hola de centro de datos de Hola para determinados servicios que tienen un precio en función de la ubicación de centro de datos. |
|meterName| cadena| Nombre del contador de Hola. |
|consumedQuantity| double| cantidad de Hola de medidor de Hola que se ha consumido. |
|resourceRate| double| Hola aplicable por unidad facturable. |
|cost| double| cargos de Hola que se ha incurrido para medidor Hola. |
|resourceLocation| cadena| Identifica Hola centro de datos donde se está ejecutando medidor Hola. |
|consumedService| cadena| Hola servicio de la plataforma Windows Azure que se utilizó. |
|instanceId| cadena| Este identificador es el nombre de hello del recurso de Hola u Hola completo identificador de recurso. Para más información, consulte [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources) (API de Azure Resource Manager). |
|serviceInfo1| cadena| Metadatos de servicio de Azure interno. |
|serviceInfo2| cadena| Por ejemplo, un tipo de imagen de una máquina virtual y un nombre de ISP para ExpressRoute. |
|additionalInfo| cadena| Metadatos específicos del servicio. Por ejemplo, un tipo de imagen de una máquina virtual. |
|etiquetas| cadena| Etiquetas agregadas del cliente. Para más información, consulte [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags) (Organización de los recursos de Azure con etiquetas). |
|storeServiceIdentifier| cadena| Esta columna no se utiliza. Presente por compatibilidad con versiones anteriores. |
|departmentName| cadena| Nombre del departamento de Hola. |
|costCenter| cadena| Centro de costo de Hola que está asociado el uso de Hola. |
|unitOfMeasure| cadena| Identifique la unidad Hola que se cobra servicio hello en. Por ejemplo, GB, horas, 10 000 s. |
|resourceGroup| cadena| en qué Hola medidor implementada se ejecuta en el grupo de recursos de Hola. Para más información, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Otras referencias

* [API de períodos de facturación](billing-enterprise-api-billing-periods.md)

* [API de saldo y resumen](billing-enterprise-api-balance-summary.md)

* [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API de hoja de precios](billing-enterprise-api-pricesheet.md)
