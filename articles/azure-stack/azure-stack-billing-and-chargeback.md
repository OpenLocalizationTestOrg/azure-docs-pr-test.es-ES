---
title: "Facturación y anulación de Azure la pila aaaCustomer | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooretrieve información de uso de recursos de pila de Azure."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a>Utilización y facturación en Azure Stack

Uso representa la cantidad de Hola de los recursos utilizados por el usuario. Pila de Azure recopila información de uso para cada usuario y la usa toobill ellos. Este artículo describe cómo se facturarán a los usuarios de la pila de Azure para uso de recursos y cómo se tiene acceso a información de facturación de hello para el análisis, anulación, etcetera.

Pila de Azure contiene hello toocollect de infraestructura y los datos de uso agregadas para todos los recursos. Puede tener acceso a estos datos y exportar el sistema de facturación tooa mediante el uso de un adaptador de facturación o exportarlo tooa herramienta de inteligencia empresarial como Microsoft Power BI. Una vez exportado, esta información de facturación se utiliza para el análisis o transferidas tooa sistema de cargo al usuario.

![Modelo conceptual de un adaptador de facturación conectando Azure pila tooa aplicación de facturación](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a>¿Qué información de utilización se puede encontrar y cómo?

Los proveedores de recursos de Azure Stack como, por ejemplo, Compute, Storage y Network, generan datos de utilización a intervalos de horas para cada suscripción. datos de uso Hello contienen información acerca de recursos de hello usa como nombre del recurso, medidor de la cantidad de nombre, identificador de medidor, usados toolearn etc. acerca de los recursos de Id. de hello metros, consulte toohello [uso de preguntas más frecuentes de API](azure-stack-usage-related-faq.md) artículo. 

Después de que se han recopilado datos de uso de hello, resulta [notificado tooAzure](azure-stack-usage-reporting.md) toogenerate una factura, que se puede ver a través de hello Azure portal de facturación. Hola portal de facturación de Azure muestra los datos de uso de hello sólo de recursos facturables Hola. Además, toohello facturables recursos, pila de Azure captura datos de uso de un conjunto más amplio de recursos, que se pueden tener acceso a su entorno de pila de Azure a través de la API de REST o PowerShell. Los administradores de la nube de Azure pila pueden recuperar los datos de uso de Hola para todas las suscripciones de usuario, mientras que un usuario puede obtener solamente los detalles de uso.

## <a name="retrieve-usage-information"></a>Recuperar información de utilización

datos de uso de hello toogenerate, debe tener recursos que se ejecuta y se usa activamente sistema Hola. Si no está seguro de si tiene algún recurso que se ejecuta en Azure Marketplace de pila, implementar una máquina virtual (VM) y comprobar Hola VM supervisión hoja toomake seguro de se está ejecutando. Usar hello datos de uso de PowerShell cmdlets tooview Hola siguientes:

1. [Instale PowerShell para Azure Stack.](azure-stack-powershell-install.md)
2. * [Configurar hello Azure pila usuario](azure-stack-powershell-configure-user.md) o hello [del operador de la pila de Azure](azure-stack-powershell-configure-admin.md) entorno de PowerShell 
3. datos de uso de hello tooretrieve, usar hello [UsageAggregates Get](/powershell/module/azurerm.usageaggregates/get-usageaggregates) cmdlet de PowerShell:
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   Si hay datos de uso, se devuelve en tal y como se muestra en la siguiente captura de pantalla de hello: 
   
   ![Agregados de utilización](media/azure-stack-billing-and-chargeback/image2.png)
   
   PowerShell devuelve 1000 líneas de utilización por llamada. Puede usar más de 1.000 líneas Hola continuación parámetro tooretrieve

## <a name="next-steps"></a>Pasos siguientes

[Informe tooAzure de datos de uso de la pila de Azure](azure-stack-usage-reporting.md)

[Provider Resource Usage API](azure-stack-provider-resource-api.md) (API de utilización de recursos de proveedor)

[Tenant Resource Usage API](azure-stack-tenant-resource-usage-api.md) (API de utilización de recursos de inquilino)

[Usage-related FAQ](azure-stack-usage-related-faq.md) (P+F relacionadas con la utilización)

