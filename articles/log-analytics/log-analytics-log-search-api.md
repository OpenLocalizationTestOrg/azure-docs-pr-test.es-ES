---
title: "API de REST de búsqueda de registro del análisis de aaaLog | Documentos de Microsoft"
description: "Esta guía proporciona un tutorial básico que describe cómo puede utilizar Hola análisis de registros buscar API de REST de hello Operations Management Suite (OMS) y se incluyen ejemplos que muestran cómo comandos de hello toouse."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>API de REST de búsqueda de registros de Log Analytics
Esta guía proporciona un tutorial básico, incluidos ejemplos de cómo puede usar Hola API de REST de búsqueda de análisis de registros. Análisis de registros es parte del programa Hola a Operations Management Suite (OMS).

> [!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, debe seguir el lenguaje de consulta heredado de toouse Hola con API de búsqueda de registro de hello tal como se describe en este artículo.  Se publicará una nueva API para áreas de trabajo actualizados y documentación de Hola se actualizará en ese momento. 

> [!NOTE]
> Análisis de registros se llamaba anteriormente visión operativa, motivo por el cual es nombre de hello usado en el proveedor de recursos de Hola.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Información general de hello API de REST de búsqueda de registros
Hola API de REST de búsqueda de análisis de registros es RESTful y son accesibles a través de hello API del Administrador de recursos de Azure. Este artículo proporcionan ejemplos de obtener acceso a las API de Hola a través de [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la invocación Hola API del Administrador de recursos de Azure. uso de Hola de ARMClient es una de muchas opciones tooaccess hello API de búsqueda de análisis de registros. Otra opción es el módulo de PowerShell de Azure de hello toouse para OperationalInsights, que incluye cmdlets para tener acceso a la búsqueda. Con estas herramientas, puede usar áreas de trabajo de hello API del Administrador de recursos de Azure toomake llamadas tooOMS y ejecutar comandos de búsqueda dentro de ellos. Hola API genera resultados de búsqueda en formato JSON, permitiéndole toouse resultados de la búsqueda de Hola de muchas formas distintas mediante programación.

Hello Azure Resource Manager se puede usar mediante una [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) hello y [API de REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn más información, revise las páginas web Hola vinculado.

> [!NOTE]
> Si utiliza un comando de agregación como `|measure count()` o `distinct`, cada llamada toosearch puede devolver hasta 500.000 registros. Las búsquedas que no incluyen un comando de agregación devuelven hasta 5000 registros.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Tutorial básico de la API de REST de búsqueda de Log Analytics
### <a name="toouse-armclient"></a>toouse ARMClient
1. Instale [Chocolatey](https://chocolatey.org/), que es un administrador de paquetes de código abierto para Windows. Abra una ventana del símbolo del sistema como administrador y, a continuación, ejecute hello siguiente comando:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Instale ARMClient con hello siguiente comando:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform una búsqueda mediante ARMClient
1. Inicie sesión con su cuenta de Microsoft o su cuenta profesional o educativa:

    ```
    armclient login
    ```

    Un inicio de sesión correcto, enumera todos los toohello de las suscripciones vinculadas dado cuenta:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Obtener áreas de trabajo de hello Operations Management Suite:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Una llamada Get correcta generaría que todas las áreas de trabajo vinculado toohello suscripción:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Cree la variable de búsqueda:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Realice búsquedas con la nueva variable de búsqueda:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Ejemplos de referencia de la API de REST de búsqueda de Log Analytics
Hello en los ejemplos siguientes muestra cómo puede usar Hola API de búsqueda.

### <a name="search---actionread"></a>Search - Action/Read
**Dirección Url de ejemplo:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Solicitud:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.

| **Propiedad** | **Descripción** |
| --- | --- |
| top |número máximo de Hola de tooreturn de resultados. |
| highlight |Contiene parámetros pre y post, usados normalmente para resaltar los campos coincidentes |
| pre |Agrega el prefijo Hola dado tooyour coincide con los campos de cadena. |
| post |Anexa Hola dado tooyour coincide con los campos de cadena. |
| query |consulta de búsqueda de Hello usa toocollect y devolver resultados. |
| start |principio de Hola Hola período de tiempo que desee toobe de resultados que se encuentra en. |
| end |final de Hola Hola período de tiempo que desee toobe de resultados que se encuentra en. |

**Respuesta:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Search/{ID} - Action/Read
**Contenido de Hola la solicitud de una búsqueda guardada:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Si la búsqueda de hello devuelve con el estado 'Pendiente', a continuación, resultados de sondeo Hola actualizado pueden realizarse a través de esta API. Después de 6 minutos, resultado de hello de la búsqueda de Hola se quitarán de la caché de Hola y se devolverá HTTP ya no existe. Si la solicitud de búsqueda inicial de hello devuelve inmediatamente un estado 'Correcto', resultados de hello no se agregan caché toohello causando este tooreturn API HTTP ya no existe si se consulta. contenido de Hola de un resultado HTTP 200 estará en el mismo formato que la solicitud de búsqueda inicial de hello solo con valores actualizados de Hola.
>
>

### <a name="saved-searches"></a>Búsquedas guardadas
**Solicitar lista de búsquedas guardadas:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Métodos admitidos: GET PUT DELETE

Métodos de colección admitidos: GET

Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.

| Propiedad | Descripción |
| --- | --- |
| Id |Identificador único de Hola. |
| Etag |**Obligatoria para la revisión**. Actualizada por el servidor en cada escritura. Valor debe ser igual toohello actual almacenado o ' *' tooupdate. 409 devuelto para valores antiguos o no válidos. |
| properties.query |**Obligatoria**. consulta de búsqueda de Hola. |
| properties.displayName |**Obligatoria**. nombre para mostrar definido por el usuario Hola de consulta de Hola. |
| properties.category |**Obligatoria**. categoría definida por el usuario Hola de consulta de Hola. |

> [!NOTE]
> Hola API de búsqueda de análisis de registros devuelve actualmente creadas por el usuario cuando se realiza un sondeo de búsquedas guardadas en un área de trabajo de búsquedas guardadas. Hola API no devuelve búsquedas guardadas proporcionadas por soluciones.
>
>

### <a name="create-saved-searches"></a>Crear búsquedas guardadas
**Solicitud:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.

### <a name="delete-saved-searches"></a>Eliminación de búsquedas guardadas
**Solicitud:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Actualización de búsquedas guardadas
 **Solicitud:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metadatos: solo JSON
Este es un campo de hello toosee manera para todos los tipos de registro para datos de hello recopilados en el área de trabajo. Por ejemplo, si desea que saber si el tipo de evento de hello tiene un campo denominado Computer, esta consulta es una manera de toocheck.

**Solicitud de campos:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Respuesta:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.

| **Propiedad** | **Descripción** |
| --- | --- |
| name |Nombre del campo. |
| DisplayName |Hola nombre para mostrar del campo de Hola. |
| type |Tipo del valor de campo de Hola Hola. |
| facetable |Combinación de las propiedades actuales ‘indexed’, ‘stored ‘y ‘facet’. |
| display |Propiedad 'display' actual. True si el campo está visible en la búsqueda. |
| ownerType |Tipos de tooonly reducida que pertenecen las IP tooonboarded. |

## <a name="optional-parameters"></a>Parámetros opcionales
Hola siguiente información describe los parámetros opcionales disponibles.

### <a name="highlighting"></a>Resaltado
parámetro de Hello "Highlight" es un parámetro opcional que se puede utilizar el subsistema de búsqueda de hello toorequest incluyen un conjunto de marcadores en la respuesta.

Estos marcadores indican Hola inicio y fin del texto resaltado que coincide con los términos de hello proporcionados en la consulta de búsqueda.
Se pueden especificar inicio hello y finalizar marcadores utilizados por el término de búsqueda toowrap Hola resaltado.

**Ejemplo de consulta de la búsqueda**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Resultado de ejemplo:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Tenga en cuenta que Hola resultado anterior contiene un mensaje de error que se ha incluido como prefijo y anexa.

## <a name="computer-groups"></a>Grupos de equipos
Los grupos de equipos son búsquedas guardadas especiales que devuelven un conjunto de equipos.  Puede usar un grupo de equipos en otros equipos de toohello de resultados de consultas toolimit hello en el grupo de Hola.  Un grupo de equipos se implementa como una búsqueda guardada con una etiqueta Grupo con un valor de Equipo.

La siguiente es una respuesta de ejemplo para un grupo de equipos.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Recuperación de grupos de equipos
Id. de un grupo de equipos, use Hola método Get con el grupo de hello tooretrieve

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Creación o actualización de un grupo de equipos
toocreate un grupo de equipos, use Hola método Put con un identificador único búsqueda guardada. Si usa un identificador de grupo de equipos existente, se modifica. Cuando se crea un grupo de equipos en el portal de análisis de registros de hello, Id. de Hola se crea de nombre y grupo de Hola.

consulta de Hello utilizada para la definición de grupo de hello debe devolver un conjunto de equipos para hello grupo toofunction correctamente.  Se recomienda que terminar la consulta con `| Distinct Computer` tooensure Hola correcta de los datos se devuelven.

definición de Hola de hello búsqueda guardada debe incluir una etiqueta con el nombre de grupo con un valor del equipo para hello búsqueda toobe clasificado como un grupo de equipos.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Eliminación de grupos de equipos
Id. de un grupo de equipos, use Hola método Delete con grupo de hello toodelete

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) consultas toobuild con campos personalizados para los criterios.
