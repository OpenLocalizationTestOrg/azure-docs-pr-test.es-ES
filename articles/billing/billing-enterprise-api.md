---
title: "aaaAzure facturación Enterprise API | Documentos de Microsoft"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Información general de API de informes para clientes de Enterprise
Hello Reporting API permiten consumo de extracción de tooprogrammatically de los clientes de Enterprise Azure y datos de facturación en herramientas de análisis de datos preferido. 

## <a name="enabling-data-access-toohello-api"></a>Habilitar la API de toohello de acceso a datos
* **Generar o recuperar la clave de API de hello** - registro de toohello Enterprise portal y seguir Hola tutorial en la Ayuda: API de informes. Hola primera sección en este artículo de ayuda explican cómo toogenerate o recuperar la clave de hello API para hello especifica inscripción.
* **Pasando claves Hola API** -clave Hola API necesita toobe pasa para cada llamada de autenticación y autorización. propiedad siguiente Hello debe toobe toohello HTTP encabezados

|Clave de encabezado de solicitud | Valor|
|-|-|
|Autorización| Especifique el valor de hello en este formato: **portador {API_KEY}** <br/> Ejemplo: bearer eyr....09|

## <a name="consumption-apis"></a>API de consumo
Está disponible un extremo de Swagger [aquí](https://consumption.azure.com/swagger/ui/index) API de Hola se describen por debajo del cual debería habilitar introspección fácil de hello API y SDK de cliente de toogenerate de capacidad de hello utilizando [AutoRest](https://github.com/Azure/AutoRest) o [ Swagger CodeGen](http://swagger.io/swagger-codegen/). Los datos a partir del 1 de mayo de 2014 están disponibles a través de esta API. 

* **Equilibrio y resumen** : hello [equilibrio y resumen API](billing-enterprise-api-balance-summary.md) ofrece un resumen de información sobre saldos, nuevas compras, cargos de servicios de Azure Marketplace, ajustes y cargos por encima del límite mensual.

* **Obtener detalles de uso** : hello [API de detalle de uso](billing-enterprise-api-usage-detail.md) ofrece un desglose diario de cantidades consumidas y gastos estimados por una inscripción. resultado de Hello también incluye información sobre instancias, medidores y departamentos. Hola API se puede consultar por período de facturación o por una apertura especificada y la fecha de finalización. 

* **Cargo de la tienda del Bazar** : hello [API cargo del almacén de Marketplace](billing-enterprise-api-marketplace-storecharge.md) devuelve desglose de cargos de marketplace basada en el uso de Hola por día para hello especifica el período de facturación o las fechas de inicio y finalización (no se incluyen las cuotas de una vez) .

* **Hoja de precios** : hello [API de la hoja de precios](billing-enterprise-api-pricesheet.md) proporciona el tipo aplicable Hola de cada medidor para hello dada la inscripción y el período de facturación. 

## <a name="helper-apis"></a>API de ayuda
 **Lista de períodos de facturación** : hello [API de períodos de facturación](billing-enterprise-api-billing-periods.md) devuelve una lista de puntos que tienen datos de consumo de hello especificada inscripción en orden cronológico inverso de facturación. Cada período contiene una propiedad que señala la ruta de la API de toohello para cuatro conjuntos de datos - BalanceSummary, UsageDetails, cargos de Marketplace y hoja de precios de Hola.


## <a name="api-response-codes"></a>Códigos de respuesta de la API  
|Código de estado de respuesta|Message|Descripción|
|-|-|-|
|200| OK|Sin errores|
|401| No autorizado| Clave de API no encontrada, no válida, expirada, etc.|
|404| No disponible| Punto de conexión de informe no encontrado|
|400| Bad Request| Parámetros no válidos: intervalos de fechas, números EA, etc.|
|500| Error de servidor| Error inesperado al procesar la solicitud| 









