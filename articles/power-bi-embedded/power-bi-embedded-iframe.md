---
title: Procedimiento para usar Power BI Embedded con REST | Microsoft Docs
description: 'Aprenda a usar Power BI Embedded con REST. '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="11c76-103">Procedimiento para usar Power BI Embedded con REST</span><span class="sxs-lookup"><span data-stu-id="11c76-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="11c76-104">Power BI Embedded: qué es y para qué sirve</span><span class="sxs-lookup"><span data-stu-id="11c76-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="11c76-105">En el sitio oficial de [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/)puede encontrar información general sobre este servicio, pero vamos a resumir brevemente sus aspectos principales antes de adentrarnos en los detalles sobre cómo utilizarlo con REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="11c76-106">Es bastante sencillo.</span><span class="sxs-lookup"><span data-stu-id="11c76-106">It's quite simple, really.</span></span> <span data-ttu-id="11c76-107">Puede que desee usar las visualizaciones de datos dinámicos de [Power BI](https://powerbi.microsoft.com) en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="11c76-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="11c76-108">La mayoría de las aplicaciones personalizadas tienen que entregar los datos de sus propios clientes, que no tienen por qué ser usuarios de su organización.</span><span class="sxs-lookup"><span data-stu-id="11c76-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="11c76-109">Por ejemplo, si brinda algún servicio a la compañía A y B, los usuarios de la A solo deberían ver datos de su propia empresa. Es decir, deben habilitarse los servicios multiinquilino para realizar la entrega.</span><span class="sxs-lookup"><span data-stu-id="11c76-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="11c76-110">La aplicación personalizada también podría ofrecer sus propios métodos de autenticación, como la autenticación de formularios, la autenticación básica, etc.</span><span class="sxs-lookup"><span data-stu-id="11c76-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="11c76-111">Después, la solución de incrustación debe colaborar con este método de autenticación existente de forma segura.</span><span class="sxs-lookup"><span data-stu-id="11c76-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="11c76-112">También se requiere que los usuarios puedan usar estas aplicaciones de ISV sin comprar más licencias de suscripción de Power BI.</span><span class="sxs-lookup"><span data-stu-id="11c76-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="11c76-113">**Power BI Embedded** se ha diseñado, precisamente, para estos tipos de escenario.</span><span class="sxs-lookup"><span data-stu-id="11c76-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="11c76-114">Por tanto, ahora que ya hemos visto una breve introducción de este servicio, pasemos a los detalles.</span><span class="sxs-lookup"><span data-stu-id="11c76-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="11c76-115">Puede utilizar el SDK de .NET \(C#) o Node.js para compilar fácilmente una aplicación con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="11c76-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="11c76-116">Sin embargo, en este artículo explicaremos el flujo HTTP \(incluida la autorización) de Power BI sin los SDK.</span><span class="sxs-lookup"><span data-stu-id="11c76-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="11c76-117">Al entender este flujo, podrá compilar su aplicación **con cualquier lenguaje de programación** y comprender a fondo la esencia de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="11c76-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="11c76-118">Creación de una colección de áreas de trabajo de Power BI y obtención de la clave de acceso \(aprovisionamiento)</span><span class="sxs-lookup"><span data-stu-id="11c76-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="11c76-119">Power BI Embedded es uno de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="11c76-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="11c76-120">Solo al ISV que usa Azure Portal se le cobran cuotas de uso \(por sesión de usuario y hora); al usuario que ve el informe no se le cobra nada ni se le exige tener una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="11c76-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="11c76-121">Antes de comenzar a desarrollar nuestra aplicación, debemos crear la **colección de áreas de trabajo de Power BI** mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11c76-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="11c76-122">Cada área de trabajo de Power BI Embedded es también la de cada cliente (inquilino); podemos agregar numerosas áreas de trabajo en cada colección de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="11c76-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="11c76-123">En cada colección de áreas de trabajo se utiliza la misma clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="11c76-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="11c76-124">De hecho, la colección de áreas de trabajo constituye el límite de seguridad de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="11c76-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="11c76-125">Cuando termine de crear la colección de áreas de trabajo, copie la clave de acceso desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11c76-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="11c76-126">También podemos aprovisionar la colección de áreas de trabajo y obtener la clave de acceso a través de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="11c76-127">Para obtener más información, consulte [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx)(API del proveedor de recursos de Power BI).</span><span class="sxs-lookup"><span data-stu-id="11c76-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="11c76-128">Creación del archivo .pbix con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="11c76-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="11c76-129">Después, tenemos que crear la conexión de datos y los informes que vamos a incrustar.</span><span class="sxs-lookup"><span data-stu-id="11c76-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="11c76-130">Para esta tarea no hay que agregar código ni realizar trabajos de programación;</span><span class="sxs-lookup"><span data-stu-id="11c76-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="11c76-131">basta con usar Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="11c76-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="11c76-132">En este artículo, no veremos los detalles de cómo usar Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="11c76-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="11c76-133">Si necesita más ayuda con este tema, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="11c76-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="11c76-134">En nuestro ejemplo, usaremos el [ejemplo Análisis de venta directa](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="11c76-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="11c76-135">Creación de un área de trabajo de Power BI</span><span class="sxs-lookup"><span data-stu-id="11c76-135">Create a Power BI workspace</span></span>

<span data-ttu-id="11c76-136">Ahora que hemos terminado de realizar el aprovisionamiento, comenzaremos creando el área de trabajo del cliente en la colección de áreas de trabajo a través de las API de REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="11c76-137">La siguiente solicitud POST HTTP (REST) va a crear la nueva área de trabajo en nuestra colección de áreas de trabajo existente.</span><span class="sxs-lookup"><span data-stu-id="11c76-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="11c76-138">Se trata de [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="11c76-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="11c76-139">En nuestro ejemplo, el nombre de la colección de áreas de trabajo es **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="11c76-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="11c76-140">Solo hay que establecer la clave de acceso, que copiamos anteriormente, como **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="11c76-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="11c76-141">Como podrá comprobar, se trata de una autenticación muy sencilla.</span><span class="sxs-lookup"><span data-stu-id="11c76-141">It’s very simple authentication!</span></span>

<span data-ttu-id="11c76-142">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="11c76-143">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="11c76-144">El valor devuelto **workspaceId** se utiliza en las siguientes llamadas de API posteriores.</span><span class="sxs-lookup"><span data-stu-id="11c76-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="11c76-145">Nuestra aplicación debe conservar este valor.</span><span class="sxs-lookup"><span data-stu-id="11c76-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="11c76-146">Importación del archivo .pbix en el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="11c76-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="11c76-147">Cada informe de un área de trabajo corresponde a un solo archivo de Power BI Desktop con un conjunto de datos \(incluida la configuración de los orígenes de datos).</span><span class="sxs-lookup"><span data-stu-id="11c76-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="11c76-148">Podemos importar el archivo .pbix al área de trabajo, tal y como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="11c76-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="11c76-149">Como puede observar, podemos cargar el binario del archivo .pbix utilizando varias partes MIME en HTTP.</span><span class="sxs-lookup"><span data-stu-id="11c76-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="11c76-150">El fragmento de URI **32960a09-6366-4208-a8bb-9e0678cdbb9d** es el id. del área de trabajo, y el parámetro de consulta **datasetDisplayName** es el nombre del conjunto de datos que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="11c76-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="11c76-151">El conjunto de datos creado contiene todos los artefactos relacionados con los datos del archivo .pbix, como los datos importados, el puntero al origen de datos, etc.</span><span class="sxs-lookup"><span data-stu-id="11c76-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="11c76-152">La ejecución de esta tarea de importación puede durar unos instantes.</span><span class="sxs-lookup"><span data-stu-id="11c76-152">This import task might run for a while.</span></span> <span data-ttu-id="11c76-153">Cuando haya finalizado, nuestra aplicación puede solicitar el estado de la tarea mediante el id. de importación.</span><span class="sxs-lookup"><span data-stu-id="11c76-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="11c76-154">En nuestro ejemplo, el id. de importación es **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="11c76-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="11c76-155">El siguiente código solicita el estado con este id. de importación:</span><span class="sxs-lookup"><span data-stu-id="11c76-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="11c76-156">Si la tarea no finaliza, la respuesta HTTP podría ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="11c76-156">If the task isn't complete, the HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="11c76-157">Si la tarea finaliza, la respuesta HTTP podría ser más parecida a esta:</span><span class="sxs-lookup"><span data-stu-id="11c76-157">If the task is complete, the HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="11c76-158">Conectividad de los orígenes de datos \(y servicio multiinquilino de datos)</span><span class="sxs-lookup"><span data-stu-id="11c76-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="11c76-159">Aunque casi todos los artefactos del archivo .pbix se importan en nuestra área de trabajo, no lo hacen las credenciales de los orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="11c76-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="11c76-160">Como resultado, al utilizar el **modo DirectQuery**, no se mostrará correctamente el informe incrustado.</span><span class="sxs-lookup"><span data-stu-id="11c76-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="11c76-161">Sin embargo, al usar el **modo de importación**, podremos ver el informe usando los datos importados existentes.</span><span class="sxs-lookup"><span data-stu-id="11c76-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="11c76-162">En este caso, debemos establecer la credencial siguiendo los pasos que figuran abajo a través de llamadas REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="11c76-163">En primer lugar, debe obtener el origen de datos de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="11c76-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="11c76-164">Sabemos que el conjunto de datos **id** es el identificador que se devolvió antes.</span><span class="sxs-lookup"><span data-stu-id="11c76-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="11c76-165">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="11c76-166">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-166">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="11c76-167">Cuando obtengamos el id. del conjunto de datos y de la puerta de enlace \(consulte los identificadores **gatewayId** e **id** anteriores en el resultado devuelto), podremos cambiar la credencial de este origen de datos de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="11c76-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="11c76-168">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-168">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="11c76-169">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="11c76-170">En el entorno de producción, también podemos establecer la cadena de conexión diferente para cada área de trabajo mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="11c76-171">\(es decir, podemos separar la base de datos de cada cliente).</span><span class="sxs-lookup"><span data-stu-id="11c76-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="11c76-172">El siguiente código va a cambiar la cadena de conexión del origen de datos a través de REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="11c76-173">También podemos usar la característica de seguridad de nivel de fila de Power BI Embedded y separar los datos de cada uno de los usuarios en un informe.</span><span class="sxs-lookup"><span data-stu-id="11c76-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="11c76-174">Como resultado, podemos aprovisionar cada informe de cliente con el mismo archivo .pbix \(interfaz de usuario, etc.) y distintos orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="11c76-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="11c76-175">Si está utilizando el **modo de importación** en lugar del **modo DirectQuery**, no se podrán actualizar modelos a través de la API.</span><span class="sxs-lookup"><span data-stu-id="11c76-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="11c76-176">Además, en Power BI Embedded todavía no se admiten orígenes de datos locales a través de la puerta de enlace de Power BI.</span><span class="sxs-lookup"><span data-stu-id="11c76-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="11c76-177">Sin embargo, le recomendamos que eche un vistazo al [blog de Power BI](https://powerbi.microsoft.com/blog/) para ver las novedades y los cambios que incorporarán las futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="11c76-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="11c76-178">Autenticación y hospedaje de informes (incrustación) en nuestra página web</span><span class="sxs-lookup"><span data-stu-id="11c76-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="11c76-179">En la API de REST anterior, podemos usar la clave de acceso **AppKey** como encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="11c76-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="11c76-180">Como estas llamadas pueden controlarse en el servidor backend, se trata de un método seguro.</span><span class="sxs-lookup"><span data-stu-id="11c76-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="11c76-181">Sin embargo, cuando incrustamos el informe en nuestra página web, este tipo de información de seguridad se controlaría con JavaScript \(front-end).</span><span class="sxs-lookup"><span data-stu-id="11c76-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="11c76-182">Después, debe protegerse el valor del encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="11c76-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="11c76-183">Si un código o un usuario malintencionados averiguan nuestra clave de acceso, pueden llamar a cualquier operación con esta clave.</span><span class="sxs-lookup"><span data-stu-id="11c76-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="11c76-184">Cuando incrustamos el informe se incrusta en nuestra página web, debemos utilizar el token calculado en lugar de la clave de acceso **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="11c76-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="11c76-185">Nuestra aplicación debe crear el token JSON Web Token \(JWT) de OAuth, que consta de las notificaciones y la firma digital calculada.</span><span class="sxs-lookup"><span data-stu-id="11c76-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="11c76-186">Tal y como se muestra a continuación, este JWT de OAuth es un token de cadena codificada delimitada por puntos.</span><span class="sxs-lookup"><span data-stu-id="11c76-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="11c76-187">En primer lugar, debemos preparar el valor de entrada, que se firma más adelante.</span><span class="sxs-lookup"><span data-stu-id="11c76-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="11c76-188">Este valor es la cadena con codificación URL en formato Base64 (rfc4648) del siguiente JSON, y está delimitada por el carácter de punto \(.).</span><span class="sxs-lookup"><span data-stu-id="11c76-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="11c76-189">del informe.</span><span class="sxs-lookup"><span data-stu-id="11c76-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="11c76-190">Si quiere usar la característica de seguridad de nivel de fila (RLS) con Power BI Embedded, debe especificar también el **nombre de usuario** y los **roles** en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="11c76-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="11c76-191">Después, deberemos crear la cadena codificada en Base64 de HMAC \(la firma) con el algoritmo SHA256.</span><span class="sxs-lookup"><span data-stu-id="11c76-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="11c76-192">Este valor de entrada firmado es la cadena anterior.</span><span class="sxs-lookup"><span data-stu-id="11c76-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="11c76-193">Por último, debemos combinar la cadena de valor y la cadena de firma con el carácter de punto \(.).</span><span class="sxs-lookup"><span data-stu-id="11c76-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="11c76-194">La cadena completa es el token de aplicación para la incrustación de informes.</span><span class="sxs-lookup"><span data-stu-id="11c76-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="11c76-195">Aunque un usuario malintencionado averigüe el token de aplicación, no podrá obtener la clave de acceso original.</span><span class="sxs-lookup"><span data-stu-id="11c76-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="11c76-196">Este token de aplicación expira rápidamente.</span><span class="sxs-lookup"><span data-stu-id="11c76-196">This app token will expire quickly.</span></span>

<span data-ttu-id="11c76-197">Este es un ejemplo PHP de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="11c76-197">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="11c76-198">Incrustación del informe en la página web (último paso)</span><span class="sxs-lookup"><span data-stu-id="11c76-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="11c76-199">Para incrustar el informe, debe obtener la URL de incrustación y el **id.** del informe mediante la siguiente API de REST.</span><span class="sxs-lookup"><span data-stu-id="11c76-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="11c76-200">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="11c76-201">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="11c76-201">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="11c76-202">Podemos incrustar el informe en nuestra aplicación web con el token de aplicación anterior.</span><span class="sxs-lookup"><span data-stu-id="11c76-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="11c76-203">Si observamos el código de ejemplo siguiente, la primera parte es la misma que la del ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="11c76-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="11c76-204">En la última parte, este ejemplo muestra el elemento **embedUrl** \(consulte el resultado anterior) del iframe y va a publicar el token de aplicación en dicho iframe.</span><span class="sxs-lookup"><span data-stu-id="11c76-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="11c76-205">Tendrá que cambiar el valor del id. del informe a uno suyo.</span><span class="sxs-lookup"><span data-stu-id="11c76-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="11c76-206">Además, debido a un error de nuestro sistema de gestión de contenidos, la etiqueta iframe del ejemplo de código se lee literalmente.</span><span class="sxs-lookup"><span data-stu-id="11c76-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="11c76-207">Quite el texto en mayúsculas de la etiqueta si va a copiar y pegar este código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="11c76-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="11c76-208">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="11c76-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="11c76-209">En este momento, Power BI Embedded solo muestra el informe en el iframe.</span><span class="sxs-lookup"><span data-stu-id="11c76-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="11c76-210">No obstante, eche un vistazo al [blog de Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="11c76-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="11c76-211">En futuras mejoras se podrán usar nuevas API del lado cliente con la que podremos enviar información en el iframe, además de extraer datos.</span><span class="sxs-lookup"><span data-stu-id="11c76-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="11c76-212">Sin duda, una característica realmente útil.</span><span class="sxs-lookup"><span data-stu-id="11c76-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="11c76-213">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="11c76-213">See also</span></span>
* [<span data-ttu-id="11c76-214">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="11c76-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="11c76-215">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="11c76-215">More questions?</span></span> [<span data-ttu-id="11c76-216">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="11c76-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

