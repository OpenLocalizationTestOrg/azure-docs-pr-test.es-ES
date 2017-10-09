---
title: "aaaArchive registros de diagnóstico de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooarchive el diagnóstico de Azure registra para la retención a largo plazo en una cuenta de almacenamiento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Archivo de registros de diagnóstico de Azure
En este artículo, le mostramos cómo puede usar hello portal de Azure, Cmdlets de PowerShell, CLI, o tooarchive de API de REST su [registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md) en una cuenta de almacenamiento. Esta opción es útil si desea que tooretain el diagnóstico se registra con una directiva de retención opcional para auditorías, análisis estático o copia de seguridad. cuenta de almacenamiento de Hello no tiene toobe Hola misma suscripción como recurso de hello emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, necesita demasiado[crear una cuenta de almacenamiento](../storage/storage-create-storage-account.md) toowhich puede archivar los registros de diagnóstico. Se recomienda encarecidamente que no utilice una cuenta de almacenamiento existente que tiene otros, sin supervisión de los datos almacenados en ella para que puedan controlar mejor toomonitoring acceder a los datos. Sin embargo, si también va a archivar el registro de actividad y la cuenta de almacenamiento de tooa de métricas de diagnóstico, puede que tenga sentido toouse esa cuenta de almacenamiento para los registros de diagnóstico también tookeep todos los datos de supervisión en una ubicación central. cuenta de almacenamiento de Hola que use debe ser una cuenta de almacenamiento de propósito general, no una cuenta de almacenamiento de blobs.

## <a name="diagnostic-settings"></a>Configuración de diagnóstico
tooarchive el diagnóstico de registros mediante cualquiera de los siguientes métodos de hello, establezca un **configuración diagnóstico** para un recurso concreto. Una configuración de diagnóstico para un recurso define las categorías de Hola de registros y datos métricos envían tooa destino (cuenta de almacenamiento, el espacio de nombres de los centros de eventos o análisis de registros). También define la directiva de retención de hello (número de días tooretain) para los eventos de cada categoría de registro y datos de métrica almacenados en una cuenta de almacenamiento. Si una directiva de retención se establece toozero, eventos de esa categoría de registro se almacenan indefinidamente (es decir, toosay, indefinidamente). De lo contrario, una directiva de retención puede ser cualquier número de días comprendido entre 1 y 2147483647. [Puede leer más acerca de estas opciones de diagnóstico aquí](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Las directivas de retención son aplicado por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminarán. Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Registros de diagnóstico de archivo mediante el portal de Hola
1. En el portal de hello, navegue tooAzure Monitor y haga clic en **configuración de diagnóstico**

    ![Sección de supervisión de Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Si lo desea Hola lista Filtrar por tipo de recurso o grupo de recursos, a continuación, haga clic en el recurso de hello para el que le gustaría tooset una configuración de diagnóstico.

3. Si ninguna configuración existe en el recurso de Hola que ha seleccionado, son toocreate solicitada una configuración. Haga clic en "Activar diagnóstico".

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Si hay una configuración existente en el recurso de hello, verá una lista de configuraciones ya configurado en este recurso. Haga clic en "Agregar configuración de diagnóstico".

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Asigne un nombre de su configuración y casilla hello para **exportar tooStorage cuenta**, a continuación, seleccione una cuenta de almacenamiento. También puede establecer un número de días tooretain estos registros mediante el uso de hello **retención (días)** controles deslizantes. Una retención de cero días almacena los registros de hello indefinidamente.
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Haga clic en **Guardar**.

Transcurridos unos instantes, nueva configuración de hello aparece en la lista de valores para este recurso, y registros de diagnóstico son almacenamiento de archivado toothat cuenta tan pronto como se generan nuevos datos de evento.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Archivo de registros de diagnóstico mediante Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| ResourceId |Sí |Identificador de recurso del recurso de hello en el que desea que tooset una configuración de diagnóstico. |
| StorageAccountId |No |Se debe guardar el Id. de recurso de la cuenta de almacenamiento de hello toowhich registros de diagnóstico. |
| Categorías |No |Lista separada por comas de tooenable de categorías de registro. |
| habilitado |Sí |Valor booleano que indica si los diagnósticos están habilitados o deshabilitados en este recurso. |
| RetentionEnabled |No |Valor booleano que indica si está habilitada una directiva de retención en este recurso. |
| RetentionInDays |No |Número de días que deben retenerse los eventos, entre 1 y 2147483647. Un valor de cero almacena los registros de hello indefinidamente. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Registros de diagnóstico de almacenamiento a través de hello multiplataforma CLI
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| ResourceId |Sí |Identificador de recurso del recurso de hello en el que desea que tooset una configuración de diagnóstico. |
| storageId |No |Se debe guardar el Id. de recurso de registros de diagnóstico toowhich Hola cuenta de almacenamiento. |
| Categorías |No |Lista separada por comas de tooenable de categorías de registro. |
| Enabled |Sí |Valor booleano que indica si los diagnósticos están habilitados o deshabilitados en este recurso. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Registros de diagnóstico de almacenamiento a través de la API de REST de Hola
[Consulte este documento](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) para obtener información sobre cómo configurar una configuración de diagnóstico mediante Hola API de REST de Monitor de Azure.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Esquema de registros de diagnóstico en la cuenta de almacenamiento de Hola
Una vez que haya configurado archivado, se crea un contenedor de almacenamiento en la cuenta de almacenamiento de hello en cuanto se produce un evento en una de las categorías de registro de hello que ha habilitado. blobs de Hello en el contenedor de hello siguen Hola mismo dar formato a través de los registros de diagnóstico y registro de actividad de Hola. estructura de Hola de estos blobs es:

> insights-logs-{nombre de categoría de registro}/resourceId=/SUBSCRIPTIONS/{id. de suscripción}/RESOURCEGROUPS/{nombre de grupo de recursos}/PROVIDERS/{nombre de proveedor de recursos}/{tipo de recurso}/{nombre de recurso}/y={año con cuatro dígitos}/m={mes con dos dígitos}/d={día con dos dígitos}/h={hora en formato de 24 horas con dos dígitos}/m=00/PT1H.json
> 
> 

O, sencillamente,

> insights-logs-{nombre de categoría de registro}/resourceId=/{id. de recurso}/y={año con cuatro dígitos}/m={mes con dos dígitos}/d={día con dos dígitos}/h={hora en formato de 24 horas con dos dígitos}/m=00/PT1H.json
> 
> 

Por ejemplo, un nombre de blob podría ser:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Cada blob PT1H.json contiene un blob JSON de eventos que se produjeron durante la hora de hello especificado en la dirección URL del blob hello (por ejemplo, h = 12). Durante Hola hora presente, los eventos son anexados toohello PT1H.json archivo cuando se producen. Hola valor de minuto (m = 00) siempre es 00, puesto que los eventos de registro de diagnóstico se dividen en los blobs individuales por hora.

En archivo de PT1H.json hello, cada evento se almacena en la matriz de registros"hello", sigue este formato:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
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
| categoría |Categoría de registro de eventos de Hola. |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, diccionario) que se describen los detalles de Hola de evento Hola. |

> [!NOTE]
> propiedades de Hola y el uso de estas propiedades pueden variar dependiendo de recursos de Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Descargar blobs para el análisis](../storage/storage-dotnet-how-to-use-blobs.md)
* [Espacio de nombres de tooan centros de eventos de registros de flujo de diagnóstico](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Información general sobre los registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md)
