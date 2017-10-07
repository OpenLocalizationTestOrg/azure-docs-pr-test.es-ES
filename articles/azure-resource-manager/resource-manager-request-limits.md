---
title: "límites de solicitudes del Administrador de recursos aaaAzure | Documentos de Microsoft"
description: "Describe cómo las solicitudes toouse limitación con el Administrador de recursos de Azure cuando se han alcanzado los límites de suscripción."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Limitación de solicitudes de Resource Manager
Para cada suscripción y el inquilino, límites de administrador de recursos leen las solicitudes too15, 000 por hora y escribir solicitudes too1, 200 por hora. Estos límites aplican tooeach instancia de Azure Resource Manager; Hay varias instancias de cada región de Azure y Azure Resource Manager está implementado tooall Azure regiones.  Por lo tanto, en la práctica, los límites son eficazmente mucho mayores que los mencionados anteriormente, ya que las solicitudes del usuario se ofrecen normalmente mediante muchas instancias diferentes.

Si la aplicación o el script alcanza estos límites, debe toothrottle las solicitudes. Este tema muestra cómo hello toodetermine restante solicita tiene antes de llegar al límite de Hola y cómo toorespond cuando se ha alcanzado el límite de Hola.

Cuando alcance el límite de hello, recibirá un código de estado HTTP de hello **429 demasiadas solicitudes**.

número de solicitudes de Hola es tooeither con ámbito de su suscripción o el inquilino. Si tiene varias, aplicaciones simultáneas realizar solicitudes en su suscripción, las solicitudes de Hola de esas aplicaciones se suman toodetermine número de Hola de las solicitudes restantes.

Las solicitudes de suscripción ámbito son los Hola implican pasar el identificador de suscripción, como la recuperación de grupos de recursos de hello en su suscripción. Las solicitudes del ámbito del inquilino no incluyen el identificador de suscripción, por ejemplo, al recuperar ubicaciones válidas de Azure.

## <a name="remaining-requests"></a>Solicitudes restantes
Puede determinar el número de Hola de las solicitudes restantes examinando los encabezados de respuesta. Cada solicitud incluye valores de número de Hola de restante solicitudes de lectura y escritura. Hello tabla siguiente describen los encabezados de respuesta de hello que puede examinar para esos valores:

| Encabezado de respuesta | Descripción |
| --- | --- |
| x-ms-ratelimit-Remaining-Subscription-Reads |Lecturas restantes del ámbito de la suscripción |
| x-ms-ratelimit-Remaining-Subscription-Writes |Escrituras restantes del ámbito de la suscripción |
| x-ms-ratelimit-Remaining-tenant-Reads |Lecturas restantes del ámbito del inquilino |
| x-ms-ratelimit-Remaining-tenant-Writes |Escrituras restantes del ámbito del inquilino |
| x-ms-ratelimit-Remaining-Subscription-Resource-Requests |Solicitudes de tipos de recursos restantes del ámbito de la suscripción<br /><br />Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado de Hola. El Administrador de recursos se agrega este valor en lugar de hello suscripción lecturas o escrituras. |
| x-ms-ratelimit-Remaining-Subscription-Resource-Entities-Read |Solicitudes de colección de tipos de recursos restantes del ámbito de la suscripción<br /><br />Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado de Hola. Este valor proporciona número Hola de solicitudes de colección restantes (recursos de lista). |
| x-ms-ratelimit-Remaining-tenant-Resource-Requests |Solicitudes de tipos de recurso restantes del ámbito del inquilino<br /><br />Solo se agrega este encabezado para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado de Hola. El Administrador de recursos se agrega este valor en lugar de hello inquilino lecturas o escrituras. |
| x-ms-ratelimit-Remaining-tenant-Resource-Entities-Read |Solicitudes de colección de tipos de recursos restantes del ámbito del inquilino<br /><br />Solo se agrega este encabezado para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado de Hola. |

## <a name="retrieving-hello-header-values"></a>Recuperar valores de encabezado de Hola
El proceso de recuperación de estos valores de encabezado del código o el script es igual que el de cualquier valor de encabezado. 

Por ejemplo, en **C#**, recuperar el valor del encabezado Hola desde una **HttpWebResponse** objeto denominado **respuesta** con hello siguiente código:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

En **PowerShell**, recuperar el valor del encabezado de Hola de una operación de Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

O bien, si desea toosee Hola restantes solicitudes para la depuración, puede proporcionar hello **-depurar** parámetro en su **PowerShell** cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

Que devuelve varios valores, incluidos Hola siguiente valor de respuesta:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

En **Azure CLI**, recuperar el valor del encabezado de hello mediante Hola opción más detallado.

```azurecli
azure group list -vv --json
```

Que devuelve muchos valores, incluidos Hola después de objeto:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Espera antes de enviar la solicitud siguiente
Cuando alcance el límite de solicitudes de Hola, Administrador de recursos devuelve hello **429** código de estado HTTP y un **Retry-After** valor de encabezado de Hola. Hola **Retry-After** valor especifica el número de Hola de segundos que debe esperar la aplicación (o suspensión) antes de enviar la solicitud siguiente Hola. Si se envía una solicitud antes de que haya transcurrido el valor de reintento de hello, no se procesa la solicitud y se devuelve un nuevo valor de reintento.

## <a name="next-steps"></a>Pasos siguientes

* Para más información acerca de límites y cuotas, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).
* toolearn sobre el control de solicitudes asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).
