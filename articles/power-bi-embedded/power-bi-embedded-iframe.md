---
title: aaaHow toouse Power BI Embedded con REST | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Power BI Embedded con REST "
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
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="732dd-103">¿Cómo toouse Power BI Embedded con REST</span><span class="sxs-lookup"><span data-stu-id="732dd-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="732dd-104">Power BI Embedded: qué es y para qué sirve</span><span class="sxs-lookup"><span data-stu-id="732dd-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="732dd-105">Información general sobre Power BI Embedded se describe en oficial de hello [sitio Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), pero vamos a echar un vistazo rápido antes de entrar en detalles de hello sobre el uso con REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="732dd-106">Es bastante sencillo.</span><span class="sxs-lookup"><span data-stu-id="732dd-106">It's quite simple, really.</span></span> <span data-ttu-id="732dd-107">Puede que desee visualizaciones de datos dinámicos de hello toouse de [Power BI](https://powerbi.microsoft.com) en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="732dd-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="732dd-108">La mayoría de las aplicaciones personalizadas necesitan datos de hello toodeliver para sus propios clientes, no necesariamente a los usuarios de su propia organización.</span><span class="sxs-lookup"><span data-stu-id="732dd-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="732dd-109">Por ejemplo, si está entrega algún servicio de la compañía A y B de la empresa, los usuarios de la compañía A solo deben ver datos de su propia empresa A. Es decir, la arquitectura multiempresa de Hola es necesario para la entrega de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="732dd-110">aplicación personalizada Hello también podría ofrecer sus propios métodos de autenticación, como autenticación de formularios, la autenticación básica etcetera...</span><span class="sxs-lookup"><span data-stu-id="732dd-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="732dd-111">A continuación, Hola incrustar solución debe colaborar con este método de autenticación existente sin ningún riesgo.</span><span class="sxs-lookup"><span data-stu-id="732dd-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="732dd-112">También es necesario para los usuarios toobe pueda toouse esas aplicaciones de ISV sin Hola compra adicional o las licencias de una suscripción de Power BI.</span><span class="sxs-lookup"><span data-stu-id="732dd-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="732dd-113">**Power BI Embedded** se ha diseñado, precisamente, para estos tipos de escenario.</span><span class="sxs-lookup"><span data-stu-id="732dd-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="732dd-114">Por lo tanto, ahora que tenemos que introducción rápida fuera de hello, vamos a profundizar algunos detalles</span><span class="sxs-lookup"><span data-stu-id="732dd-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="732dd-115">Puede usar .NET hello \(C#) o Node.js SDK, tooeasily Compile su aplicación con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="732dd-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="732dd-116">Sin embargo, en este artículo explicaremos el flujo HTTP \(incluida la autorización) de Power BI sin los SDK.</span><span class="sxs-lookup"><span data-stu-id="732dd-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="732dd-117">Descripción de este flujo, puede compilar su aplicación **con cualquier lenguaje de programación**, y puede comprender profundamente esencia Hola de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="732dd-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="732dd-118">Creación de una colección de áreas de trabajo de Power BI y obtención de la clave de acceso \(aprovisionamiento)</span><span class="sxs-lookup"><span data-stu-id="732dd-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="732dd-119">Power BI Embedded es uno de hello servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="732dd-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="732dd-120">Hola solo ISV que usa el Portal de Azure se cobra por las cuotas de uso \(por sesión de usuario cada hora), y el usuario de Hola que informe de hello vistas no está cargada o incluso requieren una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="732dd-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="732dd-121">Antes de iniciar el desarrollo de aplicaciones, debemos crear hello **colección del área de trabajo de Power BI** mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="732dd-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="732dd-122">Cada área de trabajo de Power BI Embedded es el área de trabajo de Hola para cada cliente (inquilino) y que podemos agregar muchas áreas de trabajo en cada colección de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="732dd-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="732dd-123">Hola se utiliza la misma clave de acceso de cada colección de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="732dd-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="732dd-124">En efecto, colección de área de trabajo de Hola es el límite de seguridad de Hola para Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="732dd-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="732dd-125">Cuando se termine de crear la colección de área de trabajo de hello, copie la clave de acceso de Hola desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="732dd-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="732dd-126">También podemos aprovisionar la colección del área de trabajo de Hola y obtener la clave de acceso a través de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="732dd-127">más información, consulte toolearn [API de proveedor de recursos de Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="732dd-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="732dd-128">Creación del archivo .pbix con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="732dd-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="732dd-129">A continuación, que debemos crear la conexión de datos de Hola y toobe informes incrustados.</span><span class="sxs-lookup"><span data-stu-id="732dd-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="732dd-130">Para esta tarea no hay que agregar código ni realizar trabajos de programación;</span><span class="sxs-lookup"><span data-stu-id="732dd-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="732dd-131">basta con usar Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="732dd-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="732dd-132">En este artículo, no entraremos en detalles de hello acerca de cómo toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="732dd-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="732dd-133">Si necesita más ayuda con este tema, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="732dd-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="732dd-134">En nuestro ejemplo, vamos a usar solo hello [ejemplo de análisis de minoristas](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="732dd-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="732dd-135">Creación de un área de trabajo de Power BI</span><span class="sxs-lookup"><span data-stu-id="732dd-135">Create a Power BI workspace</span></span>

<span data-ttu-id="732dd-136">Ahora que el aprovisionamiento de hello todo se hace, vamos a empezar a crear área de trabajo de un cliente en la colección del área de trabajo de Hola a través de las API de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="732dd-137">Hello solicitud de POST de HTTP siguiente (REST) es crear nueva área de trabajo de hello en la colección de área de trabajo existente.</span><span class="sxs-lookup"><span data-stu-id="732dd-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="732dd-138">Se trata de hello [API de área de trabajo de POST](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="732dd-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="732dd-139">En nuestro ejemplo, es el nombre de colección del área de trabajo de hello **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="732dd-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="732dd-140">Se acaba de establecer tecla de acceso de hello, que se copió anteriormente, como **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="732dd-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="732dd-141">Como podrá comprobar, se trata de una autenticación muy sencilla.</span><span class="sxs-lookup"><span data-stu-id="732dd-141">It’s very simple authentication!</span></span>

<span data-ttu-id="732dd-142">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="732dd-143">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-143">**HTTP Response**</span></span>

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

<span data-ttu-id="732dd-144">Hola devuelve **workspaceId** se usa para hello siguiendo las subsiguientes llamadas a la API.</span><span class="sxs-lookup"><span data-stu-id="732dd-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="732dd-145">Nuestra aplicación debe conservar este valor.</span><span class="sxs-lookup"><span data-stu-id="732dd-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="732dd-146">Importar archivo .pbix en el área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="732dd-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="732dd-147">Cada informe en un área de trabajo corresponde tooa único archivo de Power BI Desktop con un conjunto de datos \(incluida la configuración del origen de datos).</span><span class="sxs-lookup"><span data-stu-id="732dd-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="732dd-148">Podemos importar nuestro .pbix archivo toohello área de trabajo como se muestra en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="732dd-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="732dd-149">Como puede ver, hemos podemos cargar binario Hola de archivo .pbix con varias partes MIME en http.</span><span class="sxs-lookup"><span data-stu-id="732dd-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="732dd-150">fragmento de uri de Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** es workspaceId Hola y el parámetro de consulta **datasetDisplayName** es toocreate de nombre de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="732dd-151">Hola crear conjunto de datos contiene todos los datos relacionados con artefactos de archivo .pbix como datos importados, Hola origen de datos de puntero toohello, etcetera...</span><span class="sxs-lookup"><span data-stu-id="732dd-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="732dd-152">La ejecución de esta tarea de importación puede durar unos instantes.</span><span class="sxs-lookup"><span data-stu-id="732dd-152">This import task might run for a while.</span></span> <span data-ttu-id="732dd-153">Cuando haya finalizado, nuestra aplicación puede solicitar el estado de la tarea de hello con el Id. de importación. En nuestro ejemplo, es el Id. de importación de hello **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="732dd-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="732dd-154">siguiente Hola pide estado utilizando este identificador de importación:</span><span class="sxs-lookup"><span data-stu-id="732dd-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="732dd-155">Si no está completa la tarea hello, Hola respuesta HTTP podría ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="732dd-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

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

<span data-ttu-id="732dd-156">Si está completa la tarea hello, Hola respuesta HTTP podría ser parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="732dd-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="732dd-157">Conectividad de los orígenes de datos \(y servicio multiinquilino de datos)</span><span class="sxs-lookup"><span data-stu-id="732dd-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="732dd-158">Mientras casi todos los artefactos de hello en el archivo .pbix se importan en el área de trabajo, no son credenciales de Hola para orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="732dd-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="732dd-159">Como resultado, cuando se usa **directquerymode**, hello informes incrustados no se puede mostrar correctamente.</span><span class="sxs-lookup"><span data-stu-id="732dd-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="732dd-160">Pero, si se usa **modo de importación**, podemos ver informes de hello con los datos importados existentes Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="732dd-161">En tal caso, debemos establecemos la credencial de hello utilizando Hola siguiendo los pasos a través de llamadas de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="732dd-162">En primer lugar, debemos obtenemos el origen de datos de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="732dd-163">Sabemos que el conjunto de datos de hello **identificador** Hola previamente aparece Id. de.</span><span class="sxs-lookup"><span data-stu-id="732dd-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="732dd-164">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="732dd-165">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-165">**HTTP Response**</span></span>

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

<span data-ttu-id="732dd-166">Usar Hola devolvió el Id. de puerta de enlace y el Id. de origen de datos \(vea Hola anterior **gatewayId** y **Id. de** en hello devuelven resultados), podemos cambiar credenciales Hola de este origen de datos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="732dd-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="732dd-167">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-167">**HTTP Request**</span></span>

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

<span data-ttu-id="732dd-168">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="732dd-169">En producción, también podemos establecer cadena de conexión diferentes de Hola para cada área de trabajo mediante API de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="732dd-170">\(es decir, se puede separar base de datos de Hola para cada cliente.)</span><span class="sxs-lookup"><span data-stu-id="732dd-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="732dd-171">siguiente Hello es cambiar la cadena de conexión de Hola de origen de datos a través de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="732dd-172">O bien, se puede usar seguridad de nivel de fila en Power BI Embedded y se pueden separar los datos de Hola para los usuarios en un informe.</span><span class="sxs-lookup"><span data-stu-id="732dd-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="732dd-173">Como resultado, podemos aprovisionar cada informe de cliente con el mismo archivo .pbix \(interfaz de usuario, etc.) y distintos orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="732dd-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="732dd-174">Si usas **modo de importación** en lugar de **directquerymode**, no hay ningún modelo de toorefresh de manera a través de API.</span><span class="sxs-lookup"><span data-stu-id="732dd-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="732dd-175">Además, en Power BI Embedded todavía no se admiten orígenes de datos locales a través de la puerta de enlace de Power BI.</span><span class="sxs-lookup"><span data-stu-id="732dd-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="732dd-176">Sin embargo, realmente desea tookeep un ojo en hello [blog de Power BI](https://powerbi.microsoft.com/blog/) what's new y qué viene a continuación en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="732dd-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="732dd-177">Autenticación y hospedaje de informes (incrustación) en nuestra página web</span><span class="sxs-lookup"><span data-stu-id="732dd-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="732dd-178">En Hola anterior API de REST, podemos usar la clave de acceso hello **AppKey** como encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="732dd-179">Dado que estas llamadas pueden controlarse en el lado de servidor de back-end de hello, es seguro para la ejecución.</span><span class="sxs-lookup"><span data-stu-id="732dd-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="732dd-180">Pero, cuando se incrusta informe hello en nuestra página web, este tipo de información de seguridad tratar con JavaScript \(front-end).</span><span class="sxs-lookup"><span data-stu-id="732dd-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="732dd-181">A continuación, el valor de encabezado de autorización de hello debe estar protegido.</span><span class="sxs-lookup"><span data-stu-id="732dd-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="732dd-182">Si un código o un usuario malintencionados averiguan nuestra clave de acceso, pueden llamar a cualquier operación con esta clave.</span><span class="sxs-lookup"><span data-stu-id="732dd-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="732dd-183">Cuando se incrusta informe hello en nuestra página web, debemos usar Hola calculada símbolo (token) en lugar de la clave de acceso **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="732dd-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="732dd-184">Nuestra aplicación debe crear hello OAuth Json Web Token \(JWT) que consta de notificaciones de Hola y firma digital de hello calculada.</span><span class="sxs-lookup"><span data-stu-id="732dd-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="732dd-185">Tal y como se muestra a continuación, este JWT de OAuth es un token de cadena codificada delimitada por puntos.</span><span class="sxs-lookup"><span data-stu-id="732dd-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="732dd-186">En primer lugar, debemos preparamos el valor de entrada de hello, que está firmada más adelante.</span><span class="sxs-lookup"><span data-stu-id="732dd-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="732dd-187">Este valor es la cadena de dirección url codificada (rfc4648) de base64 de Hola de hello después de json y estos están delimitados por punto de hello \(.) caracteres.</span><span class="sxs-lookup"><span data-stu-id="732dd-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="732dd-188">Más adelante, explicaremos cómo tooget Hola Id. de informe.</span><span class="sxs-lookup"><span data-stu-id="732dd-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="732dd-189">Si queremos toouse seguridad de nivel de fila (RLS) con Power BI Embedded, debemos también especificamos **nombre de usuario** y **roles** en las notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

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

<span data-ttu-id="732dd-190">A continuación, debemos crear cadena codificada en base64 de Hola de HMAC \(firma hello) con el algoritmo SHA256.</span><span class="sxs-lookup"><span data-stu-id="732dd-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="732dd-191">Este valor de entrada con signo es cadena anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="732dd-192">Por último, se deben combinar valor de entrada de Hola y cadena de firma con punto \(.) caracteres.</span><span class="sxs-lookup"><span data-stu-id="732dd-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="732dd-193">cadena de Hello completado es token de aplicación Hola Hola inserción de informes.</span><span class="sxs-lookup"><span data-stu-id="732dd-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="732dd-194">Incluso si un usuario malintencionado detectan un token de aplicación hello, no pueden obtener clave de acceso original de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="732dd-195">Este token de aplicación expira rápidamente.</span><span class="sxs-lookup"><span data-stu-id="732dd-195">This app token will expire quickly.</span></span>

<span data-ttu-id="732dd-196">Este es un ejemplo PHP de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="732dd-196">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is hello apptoken)
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

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="732dd-197">Por último, incrustar informes de hello en la página web de Hola</span><span class="sxs-lookup"><span data-stu-id="732dd-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="732dd-198">Para incrustar el informe, debemos obtener Hola incrustar la dirección url y el informe **identificador** mediante Hola después de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="732dd-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="732dd-199">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="732dd-200">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="732dd-200">**HTTP Response**</span></span>

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

<span data-ttu-id="732dd-201">Se puedan incrustar informes de hello en nuestra aplicación web con token de aplicación anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="732dd-202">Si miramos siguiente código de ejemplo Hola, parte anterior hello es Hola igual que el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="732dd-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="732dd-203">En la última parte de hello, este ejemplo muestra hello **embedUrl** \(ver Hola de resultados anterior) en Hola iframe y está enviando el token de aplicación hello en hello iframe.</span><span class="sxs-lookup"><span data-stu-id="732dd-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="732dd-204">Necesitará tooone toochange Hola informe Id. valor de su elección.</span><span class="sxs-lookup"><span data-stu-id="732dd-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="732dd-205">Además, debido a errores de tooa en nuestro sistema de administración de contenido, se lee literalmente etiqueta de iframe de hello en el ejemplo de código de hello.</span><span class="sxs-lookup"><span data-stu-id="732dd-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="732dd-206">Quitar texto hello limitado de etiqueta de hello si copia y pega este código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="732dd-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="732dd-207">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="732dd-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="732dd-208">En este momento, Power BI Embedded solo muestra hello informe en hello iframe.</span><span class="sxs-lookup"><span data-stu-id="732dd-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="732dd-209">Pero, esté atento hello [Blog de Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="732dd-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="732dd-210">Mejoras futuras pudieron utilizar cliente nueva API que se Permítanos enviar información en hello iframe así como para obtener información de. Sin duda, una característica realmente útil.</span><span class="sxs-lookup"><span data-stu-id="732dd-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="732dd-211">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="732dd-211">See also</span></span>
* [<span data-ttu-id="732dd-212">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="732dd-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="732dd-213">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="732dd-213">More questions?</span></span> [<span data-ttu-id="732dd-214">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="732dd-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

