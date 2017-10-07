---
title: Hola aaaArchive registro de actividad de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooarchive registro de la actividad de Azure para la retención a largo plazo en una cuenta de almacenamiento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Archivar hello Azure Activity Log
En este artículo se muestra cómo puede utilizar Hola portal de Azure, Cmdlets de PowerShell o CLI multiplataforma tooarchive su [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) en una cuenta de almacenamiento. Esta opción es útil si desea que tooretain el registro de actividad de más de 90 días (con control total sobre la directiva de retención de hello) para auditar, análisis estático, o una copia de seguridad. Si solo necesita tooretain sus eventos durante 90 días o menos, no es necesario tooset una cuenta de almacenamiento de archivo tooa, puesto que los eventos de registro de actividad se conservan en hello plataforma Windows Azure durante 90 días sin habilitar el archivado.

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, necesita demasiado[crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich puede archivar el registro de actividad. Se recomienda encarecidamente que no utilice una cuenta de almacenamiento existente que tiene otros, sin supervisión de los datos almacenados en ella para que puedan controlar mejor toomonitoring acceder a los datos. Sin embargo, si también va a archivar registros de diagnóstico y la cuenta de almacenamiento de tooa de métricas, puede que tenga sentido toouse esa cuenta de almacenamiento para la actividad de registro también tookeep todos los datos de supervisión en una ubicación central. cuenta de almacenamiento de Hola que use debe ser una cuenta de almacenamiento de propósito general, no una cuenta de almacenamiento de blobs. cuenta de almacenamiento de Hello no tiene toobe Hola misma suscripción que Hola emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.

## <a name="log-profile"></a>Perfil de registro
Hola tooarchive registro de actividad mediante cualquiera de los siguientes métodos de hello, Establece hello **perfil del registro** para una suscripción. define el tipo de saludo de eventos que se almacenan o transmiten Hello perfil de registro y Hola salidas: concentrador de eventos o de cuenta de almacenamiento. También define la directiva de retención de hello (número de días tooretain) para los eventos almacenados en una cuenta de almacenamiento. Si la directiva de retención de Hola se establece toozero, los eventos se almacenan indefinidamente. En caso contrario, se puede establecer tooany valor entre 1 y 2147483647. Las directivas de retención son aplicado por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminarán. Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán. [Puede leer más acerca de los perfiles de registro aquí](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Archivo Hola mediante Hola portal de registro de actividad
1. En el portal de hello, haga clic en hello **registro de actividad** vínculo de navegación del lado izquierdo de Hola. Si no ve un vínculo para hello registro de actividad, haga clic en hello **más servicios** vincular primero.
   
    ![Navegar por la hoja de registro tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. En la parte superior de Hola de hoja de hello, haga clic en **exportar**.
   
    ![Haga clic en el botón Exportar de Hola](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. En la hoja de Hola que aparece, la casilla Hola para **exportar cuenta de almacenamiento de tooa** y seleccione una cuenta de almacenamiento.
   
    ![Establecer una cuenta de almacenamiento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Con el control deslizante de Hola o cuadro de texto, defina un número de días para el que se deben mantener eventos del registro de actividad en su cuenta de almacenamiento. Si lo prefiere toohave los datos persisten en la cuenta de almacenamiento de hello indefinidamente, establezca este número toozero.
5. Haga clic en **Guardar**.

## <a name="archive-hello-activity-log-via-powershell"></a>Archivar el registro de actividad a través de PowerShell de Hola
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| StorageAccountId |No |Se debe guardar el Id. de recurso de la cuenta de almacenamiento de hello toowhich registros de actividad. |
| Ubicaciones |Sí |Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad. Puede ver una lista de todas las regiones [visite esta página](https://azure.microsoft.com/en-us/regions) o mediante [Hola API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sí |Número de días que deben retenerse los eventos, entre 1 y 2147483647. Un valor de cero almacena los registros de hello indefinidamente (indefinidamente). |
| Categorías |Sí |Lista separada por comas de las categorías de eventos que deben recopilarse. Los valores posibles son Write, Delete y Action. |

## <a name="archive-hello-activity-log-via-cli"></a>Archivar el registro de actividad mediante la CLI de Hola
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| name |Sí |Nombre de su perfil de registro. |
| storageId |No |Se debe guardar el Id. de recurso de la cuenta de almacenamiento de hello toowhich registros de actividad. |
| Ubicaciones |Sí |Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad. Puede ver una lista de todas las regiones [visite esta página](https://azure.microsoft.com/en-us/regions) o mediante [Hola API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sí |Número de días que deben retenerse los eventos, entre 1 y 2147483647. Un valor de cero almacenará los registros de hello indefinidamente (indefinidamente). |
| Categorías |Sí |Lista separada por comas de las categorías de eventos que deben recopilarse. Los valores posibles son Write, Delete y Action. |

## <a name="storage-schema-of-hello-activity-log"></a>Esquema de almacenamiento de registro de actividad de hello
Una vez que haya configurado archivado, se creará un contenedor de almacenamiento en la cuenta de almacenamiento de hello en cuanto se produce un evento de registro de actividad. blobs de Hello en el contenedor de hello siguen Hola mismo formato en hello registro de actividad y registros de diagnóstico. estructura de Hola de estos blobs es:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={año con cuatro dígitos}/m={mes con dos dígitos}/d={día con dos dígitos}/h={hora en formato de 24 horas con dos dígitos}/m=00/PT1H.json
> 
> 

Por ejemplo, un nombre de blob podría ser:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Cada blob PT1H.json contiene un blob JSON de eventos que se produjeron durante la hora de hello especificado en la dirección URL del blob hello (p. ej. h = 12). Durante Hola hora presente, los eventos son anexados toohello PT1H.json archivo cuando se producen. Hola valor de minuto (m = 00) siempre es 00, puesto que los eventos de registro de actividad se dividen en los blobs individuales por hora.

En archivo de PT1H.json hello, cada evento se almacena en la matriz de registros"hello", sigue este formato:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| Nombre del elemento | Description |
| --- | --- |
| Twitter en tiempo |Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente. |
| resourceId |Id. de recurso de hello afectado recursos. |
| operationName |Nombre de operación de Hola. |
| categoría |Categoría de acción de hello, p. ej. Write, Read, Action. |
| resultType |Hola tipo de resultado de hello, p. ej. Success, Failure, Start |
| resultSignature |Depende de tipo de recurso de Hola. |
| durationMs |Duración de la operación de hello en milisegundos |
| callerIpAddress |Dirección IP del usuario de Hola que ha realizado la operación de hello, notificación de UPN o notificación SPN según su disponibilidad. |
| correlationId |Normalmente un GUID en formato de cadena de Hola. Los eventos que comparten un correlationId pertenecen toohello misma acción. |
| identidad |Blob JSON con descripciones de notificaciones y autorización de Hola. |
| authorization |BLOB de propiedades de evento de hello RBAC. Normalmente incluye propiedades de "acción", "role" y "ámbito" Hola. |
| level |Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose" |
| location |Región de la ubicación que Hola ocurrida (o global). |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, diccionario) que se describen los detalles de Hola de evento Hola. |

> [!NOTE]
> propiedades de Hola y el uso de estas propiedades pueden variar dependiendo de recursos de Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Descargar blobs para el análisis](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Transmitir tooEvent de registro de actividad de hello centros](monitoring-stream-activity-logs-event-hubs.md)
* [Obtenga más información acerca de hello registro de actividad](monitoring-overview-activity-logs.md)

