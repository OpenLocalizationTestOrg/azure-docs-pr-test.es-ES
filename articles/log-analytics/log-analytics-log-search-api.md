---
title: "API de REST de búsqueda de registros de Log Analytics | Microsoft Docs"
description: "Esta guía proporciona un tutorial básico en el que se describe cómo puede usar la API de REST de búsqueda de Log Analytics en Operations Management Suite (OMS) y, además, brinda ejemplos que muestran cómo usar los comandos."
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
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="55481-103">API de REST de búsqueda de registros de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="55481-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="55481-104">Esta guía proporciona un tutorial básico, incluidos ejemplos, de cómo puede usar la API de REST de búsqueda de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="55481-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="55481-105">Log Analytics forma parte de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="55481-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="55481-106">Si el área de trabajo se ha actualizado al [nuevo lenguaje de consulta de Log Analytics](log-analytics-log-search-upgrade.md), debe continuar usando el lenguaje de consulta heredado con la API de búsqueda de registros, según se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="55481-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="55481-107">Se publicará una nueva API para áreas de trabajo actualizadas, y la documentación se actualizará en ese mismo momento.</span><span class="sxs-lookup"><span data-stu-id="55481-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="55481-108">Log Analytics se llamaba anteriormente Operational Insights, razón por la cual se utiliza este nombre en el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="55481-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="55481-109">Información general sobre la API de REST de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="55481-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="55481-110">La API de REST de búsqueda de Log Analytics es de tipo RESTful y se puede obtener acceso a ella a través de la API de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55481-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="55481-111">En este artículo se proporcionan ejemplos de acceso a la API a través de [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la invocación de la API de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55481-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="55481-112">El uso de ARMClient es una de las muchas opciones para tener acceso a la API de búsqueda de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="55481-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="55481-113">Otra opción es utilizar el módulo Azure PowerShell para Operational Insights, que incluye cmdlets para obtener acceso a la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55481-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="55481-114">Con estas herramientas, puede usar la API de Azure Resource Manager para realizar llamadas a las áreas de trabajo de OMS y ejecutar comandos de búsqueda dentro de ellas.</span><span class="sxs-lookup"><span data-stu-id="55481-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="55481-115">La API genera resultados de búsqueda en formato JSON, lo que le permite usar los resultados de búsqueda de muchas formas distintas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="55481-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="55481-116">Azure Resource Manager se puede usar mediante una [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) y la [API de REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="55481-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="55481-117">Para más información, revise las páginas web vinculadas.</span><span class="sxs-lookup"><span data-stu-id="55481-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="55481-118">Si utiliza un comando de agregación como `|measure count()` o `distinct`, cada llamada a la búsqueda puede devolver hasta 500 000 registros.</span><span class="sxs-lookup"><span data-stu-id="55481-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="55481-119">Las búsquedas que no incluyen un comando de agregación devuelven hasta 5000 registros.</span><span class="sxs-lookup"><span data-stu-id="55481-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="55481-120">Tutorial básico de la API de REST de búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="55481-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="55481-121">Para usar ARMClient</span><span class="sxs-lookup"><span data-stu-id="55481-121">To use ARMClient</span></span>
1. <span data-ttu-id="55481-122">Instale [Chocolatey](https://chocolatey.org/), que es un administrador de paquetes de código abierto para Windows.</span><span class="sxs-lookup"><span data-stu-id="55481-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="55481-123">Abra una ventana de símbolo del sistema como administrador y luego ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55481-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="55481-124">Instale ARMClient ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55481-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="55481-125">Para realizar una búsqueda mediante ARMClient</span><span class="sxs-lookup"><span data-stu-id="55481-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="55481-126">Inicie sesión con su cuenta de Microsoft o su cuenta profesional o educativa:</span><span class="sxs-lookup"><span data-stu-id="55481-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="55481-127">Si la sesión se ha iniciado correctamente, se muestran todas las suscripciones vinculadas a la cuenta especificada.</span><span class="sxs-lookup"><span data-stu-id="55481-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="55481-128">Obtenga las áreas de trabajo de Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="55481-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="55481-129">Una llamada Get correcta generaría todas las áreas de trabajo vinculadas a la suscripción:</span><span class="sxs-lookup"><span data-stu-id="55481-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

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
3. <span data-ttu-id="55481-130">Cree la variable de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="55481-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="55481-131">Realice búsquedas con la nueva variable de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="55481-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="55481-132">Ejemplos de referencia de la API de REST de búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="55481-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="55481-133">Los siguientes ejemplos muestran cómo se puede usar la API de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55481-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="55481-134">Search - Action/Read</span><span class="sxs-lookup"><span data-stu-id="55481-134">Search - Action/Read</span></span>
<span data-ttu-id="55481-135">**Dirección Url de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="55481-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="55481-136">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="55481-136">**Request:**</span></span>

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
<span data-ttu-id="55481-137">En la tabla siguiente se describen las propiedades que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="55481-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="55481-138">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="55481-138">**Property**</span></span> | <span data-ttu-id="55481-139">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="55481-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="55481-140">top</span><span class="sxs-lookup"><span data-stu-id="55481-140">top</span></span> |<span data-ttu-id="55481-141">El número máximo de resultados que se devolverán.</span><span class="sxs-lookup"><span data-stu-id="55481-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="55481-142">highlight</span><span class="sxs-lookup"><span data-stu-id="55481-142">highlight</span></span> |<span data-ttu-id="55481-143">Contiene parámetros pre y post, usados normalmente para resaltar los campos coincidentes</span><span class="sxs-lookup"><span data-stu-id="55481-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="55481-144">pre</span><span class="sxs-lookup"><span data-stu-id="55481-144">pre</span></span> |<span data-ttu-id="55481-145">Agrega la cadena especificada delante de los campos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="55481-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="55481-146">post</span><span class="sxs-lookup"><span data-stu-id="55481-146">post</span></span> |<span data-ttu-id="55481-147">Anexa la cadena especificada a los campos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="55481-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="55481-148">query</span><span class="sxs-lookup"><span data-stu-id="55481-148">query</span></span> |<span data-ttu-id="55481-149">La consulta de búsqueda que se usa para recopilar y devolver resultados.</span><span class="sxs-lookup"><span data-stu-id="55481-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="55481-150">start</span><span class="sxs-lookup"><span data-stu-id="55481-150">start</span></span> |<span data-ttu-id="55481-151">El comienzo de la ventana de tiempo en la que desea encontrar resultados.</span><span class="sxs-lookup"><span data-stu-id="55481-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="55481-152">end</span><span class="sxs-lookup"><span data-stu-id="55481-152">end</span></span> |<span data-ttu-id="55481-153">El final de la ventana de tiempo en la que desea encontrar resultados.</span><span class="sxs-lookup"><span data-stu-id="55481-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="55481-154">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="55481-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="55481-155">Search/{ID} - Action/Read</span><span class="sxs-lookup"><span data-stu-id="55481-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="55481-156">**Solicitar el contenido de una búsqueda guardada:**</span><span class="sxs-lookup"><span data-stu-id="55481-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="55481-157">Si la búsqueda se devuelve con el estado 'Pendiente', el sondeo de los resultados actualizados puede realizarse a través de esta API.</span><span class="sxs-lookup"><span data-stu-id="55481-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="55481-158">Después de seis minutos, el resultado de la búsqueda se eliminará de la caché y se devolverá HTTP Ya no existe.</span><span class="sxs-lookup"><span data-stu-id="55481-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="55481-159">Si la solicitud de búsqueda inicial devuelve un estado ‘Correcto’ inmediatamente, los resultados no se agregan a la memoria caché, lo que provocará que esta API devuelva HTTP Ya no existe si se consulta.</span><span class="sxs-lookup"><span data-stu-id="55481-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="55481-160">El contenido de un resultado HTTP 200 está en el mismo formato que la solicitud de búsqueda inicial, solo que con valores actualizados.</span><span class="sxs-lookup"><span data-stu-id="55481-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="55481-161">Búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="55481-161">Saved searches</span></span>
<span data-ttu-id="55481-162">**Solicitar lista de búsquedas guardadas:**</span><span class="sxs-lookup"><span data-stu-id="55481-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="55481-163">Métodos admitidos: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="55481-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="55481-164">Métodos de colección admitidos: GET</span><span class="sxs-lookup"><span data-stu-id="55481-164">Supported collection methods: GET</span></span>

<span data-ttu-id="55481-165">En la tabla siguiente se describen las propiedades que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="55481-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="55481-166">Propiedad</span><span class="sxs-lookup"><span data-stu-id="55481-166">Property</span></span> | <span data-ttu-id="55481-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="55481-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55481-168">Id</span><span class="sxs-lookup"><span data-stu-id="55481-168">Id</span></span> |<span data-ttu-id="55481-169">Identificador único.</span><span class="sxs-lookup"><span data-stu-id="55481-169">The unique identifier.</span></span> |
| <span data-ttu-id="55481-170">Etag</span><span class="sxs-lookup"><span data-stu-id="55481-170">Etag</span></span> |<span data-ttu-id="55481-171">**Obligatoria para la revisión**.</span><span class="sxs-lookup"><span data-stu-id="55481-171">**Required for Patch**.</span></span> <span data-ttu-id="55481-172">Actualizada por el servidor en cada escritura.</span><span class="sxs-lookup"><span data-stu-id="55481-172">Updated by server on each write.</span></span> <span data-ttu-id="55481-173">El valor debe ser igual al valor actual almacenado o ' *' para actualizar.</span><span class="sxs-lookup"><span data-stu-id="55481-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="55481-174">409 devuelto para valores antiguos o no válidos.</span><span class="sxs-lookup"><span data-stu-id="55481-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="55481-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="55481-175">properties.query</span></span> |<span data-ttu-id="55481-176">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="55481-176">**Required**.</span></span> <span data-ttu-id="55481-177">Consulta de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55481-177">The search query.</span></span> |
| <span data-ttu-id="55481-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="55481-178">properties.displayName</span></span> |<span data-ttu-id="55481-179">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="55481-179">**Required**.</span></span> <span data-ttu-id="55481-180">Nombre para mostrar definido por el usuario de la consulta.</span><span class="sxs-lookup"><span data-stu-id="55481-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="55481-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="55481-181">properties.category</span></span> |<span data-ttu-id="55481-182">**Obligatoria**.</span><span class="sxs-lookup"><span data-stu-id="55481-182">**Required**.</span></span> <span data-ttu-id="55481-183">Categoría de la consulta definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="55481-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="55481-184">Actualmente, la API de búsqueda de Log Analytics devuelve las búsquedas guardadas creadas por el usuario cuando se realiza un sondeo de búsquedas guardadas en un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55481-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="55481-185">La API no devuelve las búsquedas guardadas proporcionadas por soluciones.</span><span class="sxs-lookup"><span data-stu-id="55481-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="55481-186">Crear búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="55481-186">Create saved searches</span></span>
<span data-ttu-id="55481-187">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="55481-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="55481-188">El nombre de todas las búsquedas guardadas, programaciones y acciones creadas con Log Analytics API debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="55481-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="55481-189">Eliminación de búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="55481-189">Delete saved searches</span></span>
<span data-ttu-id="55481-190">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="55481-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="55481-191">Actualización de búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="55481-191">Update saved searches</span></span>
 <span data-ttu-id="55481-192">**Solicitud:**</span><span class="sxs-lookup"><span data-stu-id="55481-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="55481-193">Metadatos: solo JSON</span><span class="sxs-lookup"><span data-stu-id="55481-193">Metadata - JSON only</span></span>
<span data-ttu-id="55481-194">Aquí se proporciona una manera de ver los campos de todos los tipos de registro para los datos recopilados en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55481-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="55481-195">Por ejemplo, si desea saber si el tipo de evento tiene un campo denominado Computer, esta consulta es una manera de comprobarlo.</span><span class="sxs-lookup"><span data-stu-id="55481-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="55481-196">**Solicitud de campos:**</span><span class="sxs-lookup"><span data-stu-id="55481-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="55481-197">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="55481-197">**Response:**</span></span>

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

<span data-ttu-id="55481-198">En la tabla siguiente se describen las propiedades que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="55481-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="55481-199">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="55481-199">**Property**</span></span> | <span data-ttu-id="55481-200">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="55481-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="55481-201">name</span><span class="sxs-lookup"><span data-stu-id="55481-201">name</span></span> |<span data-ttu-id="55481-202">Nombre del campo.</span><span class="sxs-lookup"><span data-stu-id="55481-202">Field name.</span></span> |
| <span data-ttu-id="55481-203">DisplayName</span><span class="sxs-lookup"><span data-stu-id="55481-203">displayName</span></span> |<span data-ttu-id="55481-204">Nombre para mostrar del campo.</span><span class="sxs-lookup"><span data-stu-id="55481-204">The display name of the field.</span></span> |
| <span data-ttu-id="55481-205">type</span><span class="sxs-lookup"><span data-stu-id="55481-205">type</span></span> |<span data-ttu-id="55481-206">Tipo del valor del campo.</span><span class="sxs-lookup"><span data-stu-id="55481-206">The Type of the field value.</span></span> |
| <span data-ttu-id="55481-207">facetable</span><span class="sxs-lookup"><span data-stu-id="55481-207">facetable</span></span> |<span data-ttu-id="55481-208">Combinación de las propiedades actuales ‘indexed’, ‘stored ‘y ‘facet’.</span><span class="sxs-lookup"><span data-stu-id="55481-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="55481-209">display</span><span class="sxs-lookup"><span data-stu-id="55481-209">display</span></span> |<span data-ttu-id="55481-210">Propiedad 'display' actual.</span><span class="sxs-lookup"><span data-stu-id="55481-210">Current ‘display’ property.</span></span> <span data-ttu-id="55481-211">True si el campo está visible en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55481-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="55481-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="55481-212">ownerType</span></span> |<span data-ttu-id="55481-213">Se reduce a solo los tipos que pertenecen a las IP incorporadas.</span><span class="sxs-lookup"><span data-stu-id="55481-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="55481-214">Parámetros opcionales</span><span class="sxs-lookup"><span data-stu-id="55481-214">Optional parameters</span></span>
<span data-ttu-id="55481-215">La siguiente información describe los parámetros opcionales disponibles.</span><span class="sxs-lookup"><span data-stu-id="55481-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="55481-216">Resaltado</span><span class="sxs-lookup"><span data-stu-id="55481-216">Highlighting</span></span>
<span data-ttu-id="55481-217">El parámetro "Highlight" es un parámetro opcional que se puede usar para solicitar al subsistema de búsqueda que incluya un conjunto de marcadores en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="55481-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="55481-218">Estos marcadores indican el inicio y fin del texto resaltado que coincide con los términos que se proporcionan en la consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55481-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="55481-219">Puede especificar los marcadores de inicio y final que se usan en la búsqueda para envolver el término resaltado.</span><span class="sxs-lookup"><span data-stu-id="55481-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="55481-220">**Ejemplo de consulta de la búsqueda**</span><span class="sxs-lookup"><span data-stu-id="55481-220">**Example search query**</span></span>

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

<span data-ttu-id="55481-221">**Resultado de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="55481-221">**Sample result:**</span></span>

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

<span data-ttu-id="55481-222">Observe que el resultado anterior contiene un mensaje de error que se ha incluido como prefijo y se ha anexado.</span><span class="sxs-lookup"><span data-stu-id="55481-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="55481-223">Grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="55481-223">Computer groups</span></span>
<span data-ttu-id="55481-224">Los grupos de equipos son búsquedas guardadas especiales que devuelven un conjunto de equipos.</span><span class="sxs-lookup"><span data-stu-id="55481-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="55481-225">Puede usar un grupo de equipos en otras consultas para limitar los resultados a los equipos del grupo.</span><span class="sxs-lookup"><span data-stu-id="55481-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="55481-226">Un grupo de equipos se implementa como una búsqueda guardada con una etiqueta Grupo con un valor de Equipo.</span><span class="sxs-lookup"><span data-stu-id="55481-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="55481-227">La siguiente es una respuesta de ejemplo para un grupo de equipos.</span><span class="sxs-lookup"><span data-stu-id="55481-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="55481-228">Recuperación de grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="55481-228">Retrieving computer groups</span></span>
<span data-ttu-id="55481-229">Para recuperar un grupo de equipos, use el método Get con el identificador de grupo.</span><span class="sxs-lookup"><span data-stu-id="55481-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="55481-230">Creación o actualización de un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="55481-230">Creating or updating a computer group</span></span>
<span data-ttu-id="55481-231">Para crear un grupo de equipos, use el método Put con un identificador de búsqueda guardada único.</span><span class="sxs-lookup"><span data-stu-id="55481-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="55481-232">Si usa un identificador de grupo de equipos existente, se modifica.</span><span class="sxs-lookup"><span data-stu-id="55481-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="55481-233">Cuando crea un grupo de equipos en el portal de Log Analytics, se crea el identificador a partir del grupo y el nombre.</span><span class="sxs-lookup"><span data-stu-id="55481-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="55481-234">La consulta que se usa para la definición de grupo debe devolver un conjunto de equipos para que el grupo funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="55481-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="55481-235">Se recomienda que finalice la consulta con `| Distinct Computer` para asegurarse de que se devuelven los datos correctos.</span><span class="sxs-lookup"><span data-stu-id="55481-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="55481-236">La definición de la búsqueda guardada debe incluir una etiqueta denominada Grupo con un valor de Equipo para que la búsqueda se clasifique como un grupo de equipos.</span><span class="sxs-lookup"><span data-stu-id="55481-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="55481-237">Eliminación de grupos de equipos</span><span class="sxs-lookup"><span data-stu-id="55481-237">Deleting computer groups</span></span>
<span data-ttu-id="55481-238">Para eliminar un grupo de equipos, use el método Delete con el identificador de grupo.</span><span class="sxs-lookup"><span data-stu-id="55481-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="55481-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55481-239">Next steps</span></span>
* <span data-ttu-id="55481-240">Si desea crear consultas con campos personalizados en función de unos criterios, obtenga más información acerca de las [búsquedas de registros](log-analytics-log-searches.md) .</span><span class="sxs-lookup"><span data-stu-id="55481-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
