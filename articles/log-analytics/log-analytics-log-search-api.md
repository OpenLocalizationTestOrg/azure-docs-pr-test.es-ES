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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="24d60-103">API de REST de búsqueda de registros de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="24d60-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="24d60-104">Esta guía proporciona un tutorial básico, incluidos ejemplos de cómo puede usar Hola API de REST de búsqueda de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="24d60-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="24d60-105">Análisis de registros es parte del programa Hola a Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="24d60-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="24d60-106">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, debe seguir el lenguaje de consulta heredado de toouse Hola con API de búsqueda de registro de hello tal como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="24d60-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="24d60-107">Se publicará una nueva API para áreas de trabajo actualizados y documentación de Hola se actualizará en ese momento.</span><span class="sxs-lookup"><span data-stu-id="24d60-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="24d60-108">Análisis de registros se llamaba anteriormente visión operativa, motivo por el cual es nombre de hello usado en el proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="24d60-109">Información general de hello API de REST de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="24d60-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="24d60-110">Hola API de REST de búsqueda de análisis de registros es RESTful y son accesibles a través de hello API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d60-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="24d60-111">Este artículo proporcionan ejemplos de obtener acceso a las API de Hola a través de [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la invocación Hola API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d60-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="24d60-112">uso de Hola de ARMClient es una de muchas opciones tooaccess hello API de búsqueda de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="24d60-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="24d60-113">Otra opción es el módulo de PowerShell de Azure de hello toouse para OperationalInsights, que incluye cmdlets para tener acceso a la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="24d60-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="24d60-114">Con estas herramientas, puede usar áreas de trabajo de hello API del Administrador de recursos de Azure toomake llamadas tooOMS y ejecutar comandos de búsqueda dentro de ellos.</span><span class="sxs-lookup"><span data-stu-id="24d60-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="24d60-115">Hola API genera resultados de búsqueda en formato JSON, permitiéndole toouse resultados de la búsqueda de Hola de muchas formas distintas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="24d60-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="24d60-116">Hello Azure Resource Manager se puede usar mediante una [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) hello y [API de REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="24d60-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="24d60-117">toolearn más información, revise las páginas web Hola vinculado.</span><span class="sxs-lookup"><span data-stu-id="24d60-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="24d60-118">Si utiliza un comando de agregación como `|measure count()` o `distinct`, cada llamada toosearch puede devolver hasta 500.000 registros.</span><span class="sxs-lookup"><span data-stu-id="24d60-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="24d60-119">Las búsquedas que no incluyen un comando de agregación devuelven hasta 5000 registros.</span><span class="sxs-lookup"><span data-stu-id="24d60-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="24d60-120">Tutorial básico de la API de REST de búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="24d60-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="24d60-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="24d60-121">toouse ARMClient</span></span>
1. <span data-ttu-id="24d60-122">Instale [Chocolatey](https://chocolatey.org/), que es un administrador de paquetes de código abierto para Windows.</span><span class="sxs-lookup"><span data-stu-id="24d60-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="24d60-123">Abra una ventana del símbolo del sistema como administrador y, a continuación, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="24d60-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="24d60-124">Instale ARMClient con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="24d60-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="24d60-125">tooperform una búsqueda mediante ARMClient</span><span class="sxs-lookup"><span data-stu-id="24d60-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="24d60-126">Inicie sesión con su cuenta de Microsoft o su cuenta profesional o educativa:</span><span class="sxs-lookup"><span data-stu-id="24d60-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="24d60-127">Un inicio de sesión correcto, enumera todos los toohello de las suscripciones vinculadas dado cuenta:</span><span class="sxs-lookup"><span data-stu-id="24d60-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="24d60-128">Obtener áreas de trabajo de hello Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="24d60-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="24d60-129">Una llamada Get correcta generaría que todas las áreas de trabajo vinculado toohello suscripción:</span><span class="sxs-lookup"><span data-stu-id="24d60-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="24d60-130">Cree la variable de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="24d60-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="24d60-131">Realice búsquedas con la nueva variable de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="24d60-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="24d60-132">Ejemplos de referencia de la API de REST de búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="24d60-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="24d60-133">Hello en los ejemplos siguientes muestra cómo puede usar Hola API de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="24d60-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="24d60-134">Search - Action/Read</span><span class="sxs-lookup"><span data-stu-id="24d60-134">Search - Action/Read</span></span>
<span data-ttu-id="24d60-135">**Dirección Url de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="24d60-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="24d60-136">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="24d60-136">**Request:**</span></span>

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
<span data-ttu-id="24d60-137">Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="24d60-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="24d60-138">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="24d60-138">**Property**</span></span> | <span data-ttu-id="24d60-139">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="24d60-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="24d60-140">top</span><span class="sxs-lookup"><span data-stu-id="24d60-140">top</span></span> |<span data-ttu-id="24d60-141">número máximo de Hola de tooreturn de resultados.</span><span class="sxs-lookup"><span data-stu-id="24d60-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="24d60-142">highlight</span><span class="sxs-lookup"><span data-stu-id="24d60-142">highlight</span></span> |<span data-ttu-id="24d60-143">Contiene parámetros pre y post, usados normalmente para resaltar los campos coincidentes</span><span class="sxs-lookup"><span data-stu-id="24d60-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="24d60-144">pre</span><span class="sxs-lookup"><span data-stu-id="24d60-144">pre</span></span> |<span data-ttu-id="24d60-145">Agrega el prefijo Hola dado tooyour coincide con los campos de cadena.</span><span class="sxs-lookup"><span data-stu-id="24d60-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="24d60-146">post</span><span class="sxs-lookup"><span data-stu-id="24d60-146">post</span></span> |<span data-ttu-id="24d60-147">Anexa Hola dado tooyour coincide con los campos de cadena.</span><span class="sxs-lookup"><span data-stu-id="24d60-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="24d60-148">query</span><span class="sxs-lookup"><span data-stu-id="24d60-148">query</span></span> |<span data-ttu-id="24d60-149">consulta de búsqueda de Hello usa toocollect y devolver resultados.</span><span class="sxs-lookup"><span data-stu-id="24d60-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="24d60-150">start</span><span class="sxs-lookup"><span data-stu-id="24d60-150">start</span></span> |<span data-ttu-id="24d60-151">principio de Hola Hola período de tiempo que desee toobe de resultados que se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="24d60-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="24d60-152">end</span><span class="sxs-lookup"><span data-stu-id="24d60-152">end</span></span> |<span data-ttu-id="24d60-153">final de Hola Hola período de tiempo que desee toobe de resultados que se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="24d60-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="24d60-154">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="24d60-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="24d60-155">Search/{ID} - Action/Read</span><span class="sxs-lookup"><span data-stu-id="24d60-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="24d60-156">**Contenido de Hola la solicitud de una búsqueda guardada:**</span><span class="sxs-lookup"><span data-stu-id="24d60-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="24d60-157">Si la búsqueda de hello devuelve con el estado 'Pendiente', a continuación, resultados de sondeo Hola actualizado pueden realizarse a través de esta API.</span><span class="sxs-lookup"><span data-stu-id="24d60-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="24d60-158">Después de 6 minutos, resultado de hello de la búsqueda de Hola se quitarán de la caché de Hola y se devolverá HTTP ya no existe.</span><span class="sxs-lookup"><span data-stu-id="24d60-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="24d60-159">Si la solicitud de búsqueda inicial de hello devuelve inmediatamente un estado 'Correcto', resultados de hello no se agregan caché toohello causando este tooreturn API HTTP ya no existe si se consulta.</span><span class="sxs-lookup"><span data-stu-id="24d60-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="24d60-160">contenido de Hola de un resultado HTTP 200 estará en el mismo formato que la solicitud de búsqueda inicial de hello solo con valores actualizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="24d60-161">Búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="24d60-161">Saved searches</span></span>
<span data-ttu-id="24d60-162">**Solicitar lista de búsquedas guardadas:**</span><span class="sxs-lookup"><span data-stu-id="24d60-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="24d60-163">Métodos admitidos: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="24d60-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="24d60-164">Métodos de colección admitidos: GET</span><span class="sxs-lookup"><span data-stu-id="24d60-164">Supported collection methods: GET</span></span>

<span data-ttu-id="24d60-165">Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="24d60-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="24d60-166">Propiedad</span><span class="sxs-lookup"><span data-stu-id="24d60-166">Property</span></span> | <span data-ttu-id="24d60-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="24d60-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24d60-168">Id</span><span class="sxs-lookup"><span data-stu-id="24d60-168">Id</span></span> |<span data-ttu-id="24d60-169">Identificador único de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-169">hello unique identifier.</span></span> |
| <span data-ttu-id="24d60-170">Etag</span><span class="sxs-lookup"><span data-stu-id="24d60-170">Etag</span></span> |<span data-ttu-id="24d60-171">**Obligatoria para la revisión**.</span><span class="sxs-lookup"><span data-stu-id="24d60-171">**Required for Patch**.</span></span> <span data-ttu-id="24d60-172">Actualizada por el servidor en cada escritura.</span><span class="sxs-lookup"><span data-stu-id="24d60-172">Updated by server on each write.</span></span> <span data-ttu-id="24d60-173">Valor debe ser igual toohello actual almacenado o ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="24d60-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="24d60-174">409 devuelto para valores antiguos o no válidos.</span><span class="sxs-lookup"><span data-stu-id="24d60-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="24d60-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="24d60-175">properties.query</span></span> |<span data-ttu-id="24d60-176">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="24d60-176">**Required**.</span></span> <span data-ttu-id="24d60-177">consulta de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-177">hello search query.</span></span> |
| <span data-ttu-id="24d60-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="24d60-178">properties.displayName</span></span> |<span data-ttu-id="24d60-179">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="24d60-179">**Required**.</span></span> <span data-ttu-id="24d60-180">nombre para mostrar definido por el usuario Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="24d60-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="24d60-181">properties.category</span></span> |<span data-ttu-id="24d60-182">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="24d60-182">**Required**.</span></span> <span data-ttu-id="24d60-183">categoría definida por el usuario Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="24d60-184">Hola API de búsqueda de análisis de registros devuelve actualmente creadas por el usuario cuando se realiza un sondeo de búsquedas guardadas en un área de trabajo de búsquedas guardadas.</span><span class="sxs-lookup"><span data-stu-id="24d60-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="24d60-185">Hola API no devuelve búsquedas guardadas proporcionadas por soluciones.</span><span class="sxs-lookup"><span data-stu-id="24d60-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="24d60-186">Crear búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="24d60-186">Create saved searches</span></span>
<span data-ttu-id="24d60-187">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="24d60-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="24d60-188">nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="24d60-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="24d60-189">Eliminación de búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="24d60-189">Delete saved searches</span></span>
<span data-ttu-id="24d60-190">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="24d60-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="24d60-191">Actualización de búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="24d60-191">Update saved searches</span></span>
 <span data-ttu-id="24d60-192">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="24d60-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="24d60-193">Metadatos: solo JSON</span><span class="sxs-lookup"><span data-stu-id="24d60-193">Metadata - JSON only</span></span>
<span data-ttu-id="24d60-194">Este es un campo de hello toosee manera para todos los tipos de registro para datos de hello recopilados en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="24d60-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="24d60-195">Por ejemplo, si desea que saber si el tipo de evento de hello tiene un campo denominado Computer, esta consulta es una manera de toocheck.</span><span class="sxs-lookup"><span data-stu-id="24d60-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="24d60-196">**Solicitud de campos:**</span><span class="sxs-lookup"><span data-stu-id="24d60-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="24d60-197">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="24d60-197">**Response:**</span></span>

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

<span data-ttu-id="24d60-198">Hello en la tabla siguiente describe las propiedades de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="24d60-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="24d60-199">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="24d60-199">**Property**</span></span> | <span data-ttu-id="24d60-200">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="24d60-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="24d60-201">name</span><span class="sxs-lookup"><span data-stu-id="24d60-201">name</span></span> |<span data-ttu-id="24d60-202">Nombre del campo.</span><span class="sxs-lookup"><span data-stu-id="24d60-202">Field name.</span></span> |
| <span data-ttu-id="24d60-203">DisplayName</span><span class="sxs-lookup"><span data-stu-id="24d60-203">displayName</span></span> |<span data-ttu-id="24d60-204">Hola nombre para mostrar del campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="24d60-205">type</span><span class="sxs-lookup"><span data-stu-id="24d60-205">type</span></span> |<span data-ttu-id="24d60-206">Tipo del valor de campo de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="24d60-207">facetable</span><span class="sxs-lookup"><span data-stu-id="24d60-207">facetable</span></span> |<span data-ttu-id="24d60-208">Combinación de las propiedades actuales ‘indexed’, ‘stored ‘y ‘facet’.</span><span class="sxs-lookup"><span data-stu-id="24d60-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="24d60-209">display</span><span class="sxs-lookup"><span data-stu-id="24d60-209">display</span></span> |<span data-ttu-id="24d60-210">Propiedad 'display' actual.</span><span class="sxs-lookup"><span data-stu-id="24d60-210">Current ‘display’ property.</span></span> <span data-ttu-id="24d60-211">True si el campo está visible en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="24d60-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="24d60-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="24d60-212">ownerType</span></span> |<span data-ttu-id="24d60-213">Tipos de tooonly reducida que pertenecen las IP tooonboarded.</span><span class="sxs-lookup"><span data-stu-id="24d60-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="24d60-214">Parámetros opcionales</span><span class="sxs-lookup"><span data-stu-id="24d60-214">Optional parameters</span></span>
<span data-ttu-id="24d60-215">Hola siguiente información describe los parámetros opcionales disponibles.</span><span class="sxs-lookup"><span data-stu-id="24d60-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="24d60-216">Resaltado</span><span class="sxs-lookup"><span data-stu-id="24d60-216">Highlighting</span></span>
<span data-ttu-id="24d60-217">parámetro de Hello "Highlight" es un parámetro opcional que se puede utilizar el subsistema de búsqueda de hello toorequest incluyen un conjunto de marcadores en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="24d60-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="24d60-218">Estos marcadores indican Hola inicio y fin del texto resaltado que coincide con los términos de hello proporcionados en la consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="24d60-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="24d60-219">Se pueden especificar inicio hello y finalizar marcadores utilizados por el término de búsqueda toowrap Hola resaltado.</span><span class="sxs-lookup"><span data-stu-id="24d60-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="24d60-220">**Ejemplo de consulta de la búsqueda**</span><span class="sxs-lookup"><span data-stu-id="24d60-220">**Example search query**</span></span>

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

<span data-ttu-id="24d60-221">**Resultado de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="24d60-221">**Sample result:**</span></span>

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

<span data-ttu-id="24d60-222">Tenga en cuenta que Hola resultado anterior contiene un mensaje de error que se ha incluido como prefijo y anexa.</span><span class="sxs-lookup"><span data-stu-id="24d60-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="24d60-223">Grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="24d60-223">Computer groups</span></span>
<span data-ttu-id="24d60-224">Los grupos de equipos son búsquedas guardadas especiales que devuelven un conjunto de equipos.</span><span class="sxs-lookup"><span data-stu-id="24d60-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="24d60-225">Puede usar un grupo de equipos en otros equipos de toohello de resultados de consultas toolimit hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="24d60-226">Un grupo de equipos se implementa como una búsqueda guardada con una etiqueta Grupo con un valor de Equipo.</span><span class="sxs-lookup"><span data-stu-id="24d60-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="24d60-227">La siguiente es una respuesta de ejemplo para un grupo de equipos.</span><span class="sxs-lookup"><span data-stu-id="24d60-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="24d60-228">Recuperación de grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="24d60-228">Retrieving computer groups</span></span>
<span data-ttu-id="24d60-229">Id. de un grupo de equipos, use Hola método Get con el grupo de hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="24d60-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="24d60-230">Creación o actualización de un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="24d60-230">Creating or updating a computer group</span></span>
<span data-ttu-id="24d60-231">toocreate un grupo de equipos, use Hola método Put con un identificador único búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="24d60-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="24d60-232">Si usa un identificador de grupo de equipos existente, se modifica.</span><span class="sxs-lookup"><span data-stu-id="24d60-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="24d60-233">Cuando se crea un grupo de equipos en el portal de análisis de registros de hello, Id. de Hola se crea de nombre y grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d60-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="24d60-234">consulta de Hello utilizada para la definición de grupo de hello debe devolver un conjunto de equipos para hello grupo toofunction correctamente.</span><span class="sxs-lookup"><span data-stu-id="24d60-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="24d60-235">Se recomienda que terminar la consulta con `| Distinct Computer` tooensure Hola correcta de los datos se devuelven.</span><span class="sxs-lookup"><span data-stu-id="24d60-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="24d60-236">definición de Hola de hello búsqueda guardada debe incluir una etiqueta con el nombre de grupo con un valor del equipo para hello búsqueda toobe clasificado como un grupo de equipos.</span><span class="sxs-lookup"><span data-stu-id="24d60-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="24d60-237">Eliminación de grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="24d60-237">Deleting computer groups</span></span>
<span data-ttu-id="24d60-238">Id. de un grupo de equipos, use Hola método Delete con grupo de hello toodelete</span><span class="sxs-lookup"><span data-stu-id="24d60-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="24d60-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24d60-239">Next steps</span></span>
* <span data-ttu-id="24d60-240">Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) consultas toobuild con campos personalizados para los criterios.</span><span class="sxs-lookup"><span data-stu-id="24d60-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
