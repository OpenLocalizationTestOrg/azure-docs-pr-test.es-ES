---
title: "las API de facturación aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca del uso de facturación de Azure y RateCard APIs, que son visiones tooprovide usado del consumo de recursos de Azure y tendencias."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Use las API de facturación de Azure tooprogrammatically obtener información sobre el uso de Azure
Usar datos de uso y los recursos de toopull de las API de facturación de Azure en las herramientas de análisis de datos preferido. Hola, uso de recursos de Azure y RateCard APIs pueden ayudarle a predecir de forma precisa y administrar los costos. Hola API se implementan como un proveedor de recursos y la parte de la familia de Hola de API que expone hello Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>API de descarga de facturas de Azure (vista previa)
Una vez Hola [participación ha sido completada](billing-manage-access.md#opt-in), facturas de descarga con la versión de vista previa de hello [API factura](/rest/api/billing). Hola características incluyen:

* **Control de acceso basada en roles de Azure** -configurar el acceso de directivas en hello [portal de Azure](https://portal.azure.com) o a través [cmdlets de PowerShell de Azure](/powershell/azure/overview) toospecify aplicaciones o que los usuarios puede obtener acceso datos de uso de la suscripción de toohello. Los autores de llamadas deben utilizar tokens de Azure Active Directory estándar para la autenticación. Agregar Hola llamador tooeither Hola lector de facturación, lector, propietario o Colaborador rol tooget acceso toohello datos de uso para una suscripción de Azure específica.
* **Filtrado de fechas** -Hola de uso `$filter` tooget parámetro todas las facturas de hello en orden cronológico inverso por hello facturación fecha final del período. 

> [!NOTE]
> Esta característica se encuentra en la primera versión de vista previa y puede modificarse sujeto toobackward incompatible. De momento no está disponible para determinadas ofertas de suscripción (EA, CSP, AIO no admitidas) y Azure Germany.

## <a name="azure-resource-usage-api-preview"></a>API de uso de recursos de Azure (vista previa)
Hola utilice Azure [API de uso de recursos](https://msdn.microsoft.com/library/azure/mt219003) tooget los datos de consumo de Azure estimado. Hola API incluye:

* **Control de acceso basada en roles de Azure** -configurar el acceso de directivas en hello [portal de Azure](https://portal.azure.com) o a través [cmdlets de PowerShell de Azure](/powershell/azure/overview) toospecify aplicaciones o que los usuarios puede obtener acceso datos de uso de la suscripción de toohello. Los autores de llamadas deben utilizar tokens de Azure Active Directory estándar para la autenticación. Agregar Hola llamador tooeither Hola lector de facturación, lector, propietario o Colaborador rol tooget acceso toohello datos de uso para una suscripción de Azure específica.
* **Agregaciones cada hora o diarias** : los autores de llamadas pueden especificar si desean sus datos de uso de Azure en depósitos cada hora o diarios. valor predeterminado de Hello es diaria.
* **Metadatos de la instancia (incluye las etiquetas del recurso)** : obtener detalles de nivel de instancia como Hola uri de recurso completo (/ subscriptions / {Id. de suscripción} /..), Hola información del grupo de recursos y las etiquetas del recurso. Estos metadatos le ayuda a determinista y asignar mediante programación el uso por etiquetas de hello, para casos de uso como carga entre.
* **Metadatos de recursos** -detalles de recursos como nombre de medidor de hello, medidor de la categoría, subcategoría de medidor, unidad y región permiten llamador Hola una mejor comprensión de lo que se consumió. También estamos trabajando terminología de metadatos de recursos tooalign en hello portal de Azure, Azure uso CSV, CSV, de facturación de EA y otras experiencias de acceso público, toolet correlacionar los datos a través de experiencias.
* **Uso para todos los tipos de ofertas**: los datos de uso están disponibles para todos los tipos de ofertas, incluidos el pago por uso, MSDN, compromiso monetario, crédito monetario y EA.

## <a name="azure-resource-ratecard-api-preview"></a>API de RateCard de recursos de Azure (vista previa)
Hola de uso [API RateCard de recursos de Azure](https://msdn.microsoft.com/library/azure/mt219005) lista de Hola de tooget de recursos de Azure disponibles e información de precios estimado para cada uno. Hola API incluye:

* **Control de acceso basado en roles Azure** -configurar las directivas de acceso en hello [portal de Azure](https://portal.azure.com) o a través [cmdlets de PowerShell de Azure](/powershell/azure/overview) toospecify aplicaciones o que los usuarios puede obtener acceso toohello RateCard datos. Los autores de llamadas deben utilizar tokens de Azure Active Directory estándar para la autenticación. Agregar Hola llamador tooeither Hola lector, el propietario o Colaborador rol tooget acceso toohello datos de uso para una suscripción de Azure.
* **Compatibilidad con ofertas de pago por uso, MSDN, compromiso monetario y crédito monetario (no compatible con EA)**: esta API proporciona información de tarifas de nivel de oferta de Azure.  autor de llamada de Hola de esta API debe pasar las tasas y detalles de tooget información del recurso de la oferta de Hola. Estamos tasas EA tooprovide actualmente no es posible porque EA ofertas han personalizado las tasas por la inscripción. 

## <a name="scenarios"></a>Escenarios
Estos son algunos de los escenarios de Hola que son posibles con combinación de Hola de uso de Hola y Hola RateCard APIs:

* **Azure gastará durante el mes de hello** -combinación de Hola de uso de hello uso y RateCard APIs tooget una mejor percepción en la nube dedicar durante los meses de Hola. Puede analizar Hola cada hora y las estimaciones de depósitos diarias de uso y carga.
* **Configurar alertas** : usar hello uso y hello tooget RateCard APIs estimación de consumo de la nube y los cargos y configurar alertas basada en moneda o basada en recursos.
* **Predecir factura** : Get su consumo estimado y la nube invierte y aplican toopredict algoritmos de aprendizaje qué factura Hola sería final Hola de hello ciclo de facturación automático.
* **Consumo previo análisis de costos** : usar Hola API RateCard toopredict sería la cantidad de la factura para su uso esperado cuando se mueve el tooAzure de las cargas de trabajo. Si tiene cargas de trabajo existentes en otras nubes o nubes privadas, también se puede asignar su uso con hello Azure tasas tooget dedique una mejor estimación de Azure. Esto deja de estimación Hola toopivot de capacidad en la oferta y comparar y contrastar entre tipos de oferta distintos de hello más allá de pago por uso, como un compromiso monetario y crédito monetario. Hola API también le ofrece Hola capacidad toosee costo diferencias por región y permitiéndole toodo un toohelp de análisis de hipótesis costo tomar decisiones de implementación.
* **Análisis de hipótesis** -
  
  * Puede determinar si es más cargas de trabajo de toorun rentable en otra región o en otra configuración del programa Hola a recursos de Azure. Recursos de Azure los costos pueden diferir según Hola región de Azure que está usando.
  * También puede determinar si otro tipo de oferta de Azure ofrece una mejor tarifa en un recurso de Azure.
  
## <a name="partner-solutions"></a>Soluciones de socios
[Uso de Microsoft Azure y RateCard API habilitar Cloudyn tooProvide ITFM para los clientes](billing-usage-rate-card-partner-solution-cloudyn.md) describe la experiencia de integración de hello ofrecida por socios de API de facturación de Azure [Cloudyn](https://www.cloudyn.com/microsoft-azure/). En este artículo se habla sobre sus experiencias y se incluye un vídeo que muestra cómo puede utilizar Cloudyn y Hola visión tooget de las API de facturación de Azure de datos de consumo de Azure.

[Cloud Cruiser y la integración de la API de facturación de Microsoft Azure](billing-usage-rate-card-partner-solution-cloudcruiser.md) describe cómo [Express de Cloud Cruiser para Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) funciona directamente desde el portal de Windows Azure Pack (WAP) Hola. Puede administrar sin ningún problema ambos aspectos operativos y financieros de Hola de hello Microsoft hospedada o privada nube pública de Azure desde una sola interfaz de usuario.   

## <a name="next-steps"></a>Pasos siguientes
* Consulte los ejemplos de código de hello en GitHub:
  * [Ejemplo de código de API de facturas](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Ejemplo de código de API de uso](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Ejemplo de código de API de RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn más información acerca de hello Azure Resource Manager, consulte [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md). 

* Para obtener más información sobre suite Hola de herramientas dedicar toohelp es necesario obtener una descripción de la nube, consulte el artículo de Gartner hello [Guía de mercado para herramientas de administración de financieros TI (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

