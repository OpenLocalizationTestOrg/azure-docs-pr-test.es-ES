---
title: un informe en Azure Power BI Embedded aaaEmbed | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooembed un informe que se encuentra en Power BI Embedded en la aplicación."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="b6199-103">Inserción de un informe en Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b6199-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="b6199-104">Obtenga información acerca de cómo tooembed un informe que se encuentra en Power BI Embedded en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6199-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="b6199-105">Veremos cómo tooactually incrustar un informe en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6199-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="b6199-106">Aquí se asume que ya tiene un informe que existe en un área de trabajo de su colección de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b6199-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="b6199-107">Si aún no ha dado ese paso, consulte [Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6199-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="b6199-108">Puede usar .NET hello (C#) o el SDK de Node.js, junto con JavaScript, tooeasily Compile su aplicación con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b6199-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="b6199-109">Uso de toouse de claves de acceso de hello las API de REST</span><span class="sxs-lookup"><span data-stu-id="b6199-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="b6199-110">Hola de orden toocall API de REST, puede pasar clave de acceso de Hola que puede obtener de hello portal de Azure para una colección de área de trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="b6199-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="b6199-111">Para más información, consulte [Introducción a Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6199-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="b6199-112">Obtención de un identificador de informe</span><span class="sxs-lookup"><span data-stu-id="b6199-112">Get a report id</span></span>

<span data-ttu-id="b6199-113">Todos los tokens de acceso se basan en algún informe.</span><span class="sxs-lookup"><span data-stu-id="b6199-113">Every access token is based on a report.</span></span> <span data-ttu-id="b6199-114">Necesitará hello tooget determinado Id. de informe para los informes de Hola que desea tooembed.</span><span class="sxs-lookup"><span data-stu-id="b6199-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="b6199-115">Esto puede hacerse en función de las llamadas toohello [obtener informes](https://msdn.microsoft.com/library/azure/mt711510.aspx) API de REST.</span><span class="sxs-lookup"><span data-stu-id="b6199-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="b6199-116">Esto devolverá informe Hola hello y el Id. de incrustan la dirección url.</span><span class="sxs-lookup"><span data-stu-id="b6199-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="b6199-117">Esto puede hacerse mediante Hola Power BI .NET SDK o llamar directamente a API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6199-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="b6199-118">Uso de hello Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b6199-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="b6199-119">Cuando se usa Hola .NET SDK, deberá toocreate una credencial de token que se basa en la clave de acceso de hello que obtendrá de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6199-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="b6199-120">Esto requiere que instale hello [paquete API NuGet de Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="b6199-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="b6199-121">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="b6199-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="b6199-122">**Código de C#**</span><span class="sxs-lookup"><span data-stu-id="b6199-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="b6199-123">Hola de llamar a API de REST directamente</span><span class="sxs-lookup"><span data-stu-id="b6199-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="b6199-124">Creación de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="b6199-124">Create an access token</span></span>

<span data-ttu-id="b6199-125">Power BI Embedded usa tokens de inserción, que son JSON Web Tokens con forma HMAC.</span><span class="sxs-lookup"><span data-stu-id="b6199-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="b6199-126">Hola tokens se firman con la clave de acceso de hello en su colección Azure Power BI Embedded de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b6199-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="b6199-127">Inserte tokens, de forma predeterminada, se usa tooprovide leer solo acceso tooa informe tooembed en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6199-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="b6199-128">Los tokens de inserción se emiten para un informe concreto y se deben asociar a una dirección URL de inserción.</span><span class="sxs-lookup"><span data-stu-id="b6199-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="b6199-129">Tokens de acceso deben crearse en el servidor de hello como teclas de acceso de hello son tokens de hello toosign/encrypt usado.</span><span class="sxs-lookup"><span data-stu-id="b6199-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="b6199-130">Para obtener información acerca de cómo toocreate un token de acceso, consulte [autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b6199-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="b6199-131">También puede revisar hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método.</span><span class="sxs-lookup"><span data-stu-id="b6199-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="b6199-132">Este es un ejemplo de este aspecto usando Hola .NET SDK para Power BI.</span><span class="sxs-lookup"><span data-stu-id="b6199-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="b6199-133">Va a usar el Id. de informe de Hola que recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6199-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="b6199-134">Una vez Hola incrustar símbolo (token) se crea, a continuación, usará Hola acceso toogenerate clave Hola símbolo (token) que se puede utilizar desde la perspectiva de javascript de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6199-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="b6199-135">Hola *PowerBIToken clase* requiere que instale hello [Power BI Core NuGut paquete](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="b6199-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="b6199-136">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="b6199-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="b6199-137">**Código de C#**</span><span class="sxs-lookup"><span data-stu-id="b6199-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="b6199-138">Adición de tokens de tooembed de ámbitos de permiso</span><span class="sxs-lookup"><span data-stu-id="b6199-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="b6199-139">Cuando se usa tokens de insertar, puede que desee toorestrict uso de recursos de hello a que ofrecen acceso.</span><span class="sxs-lookup"><span data-stu-id="b6199-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="b6199-140">Por este motivo, puede generar un token con permisos con ámbito.</span><span class="sxs-lookup"><span data-stu-id="b6199-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="b6199-141">Para más información, consulte [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ámbitos)</span><span class="sxs-lookup"><span data-stu-id="b6199-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="b6199-142">Inserción mediante JavaScript</span><span class="sxs-lookup"><span data-stu-id="b6199-142">Embed using JavaScript</span></span>

<span data-ttu-id="b6199-143">Una vez que el token de acceso de Hola y el identificador del informe de hello, se puede incrustar informe de hello con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b6199-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="b6199-144">Esto requiere que instale Hola nuget [paquete de Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="b6199-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="b6199-145">Hola embedUrl solo será https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="b6199-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="b6199-146">Puede usar hello [incrustar el informe de ejemplo JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="b6199-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="b6199-147">También proporciona ejemplos de código para las operaciones diferentes de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="b6199-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="b6199-148">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="b6199-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="b6199-149">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b6199-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="b6199-150">Establecer tamaño de Hola de los elementos incrustados</span><span class="sxs-lookup"><span data-stu-id="b6199-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="b6199-151">informe de Hola se incrustarán automáticamente en función de tamaño de Hola de su contenedor.</span><span class="sxs-lookup"><span data-stu-id="b6199-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="b6199-152">tamaño de toooverride Hola predeterminado de hello incrusta basta con agregar un estilos de atributo o en línea de la clase CSS de ancho y alto.</span><span class="sxs-lookup"><span data-stu-id="b6199-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="b6199-153">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b6199-153">See also</span></span>

[<span data-ttu-id="b6199-154">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="b6199-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b6199-155">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b6199-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b6199-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="b6199-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
<span data-ttu-id="b6199-157">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b6199-157">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
[<span data-ttu-id="b6199-158">Paquete Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="b6199-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="b6199-159">[Paquete NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Paquete NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="b6199-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="b6199-160">Repositorio GIT PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="b6199-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="b6199-161">Repositorio GIT PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="b6199-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="b6199-162">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="b6199-162">More questions?</span></span> [<span data-ttu-id="b6199-163">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="b6199-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
