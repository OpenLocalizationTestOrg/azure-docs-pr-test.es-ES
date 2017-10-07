---
title: aaaCreate un nuevo informe a partir de un conjunto de datos en Azure Power BI Embedded | Documentos de Microsoft
description: "Los informes de Power BI Embedded ahora se puede crear a partir de un conjunto de datos de su propia aplicación."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="41172-103">Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="41172-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="41172-104">Los informes de Power BI Embedded ahora se puede crear a partir de un conjunto de datos de su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="41172-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="41172-105">Hello método de autenticación es similar incrustar toothat del informe.</span><span class="sxs-lookup"><span data-stu-id="41172-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="41172-106">Se basa en tokens de acceso que están el conjunto de datos de tooa específico.</span><span class="sxs-lookup"><span data-stu-id="41172-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="41172-107">Los tokens que se usan para PowerBI.com los emite Azure Active Directory (AAD), mientras que los de Power BI Embedded los emite su propio servicio.</span><span class="sxs-lookup"><span data-stu-id="41172-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="41172-108">Cuando un informe incrustado, creación Hola son tokens emitidos para un conjunto de datos específico.</span><span class="sxs-lookup"><span data-stu-id="41172-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="41172-109">Símbolos (tokens) debe asociarse con hello incrustar la dirección URL en hello mismo tooensure elemento tiene un token único.</span><span class="sxs-lookup"><span data-stu-id="41172-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="41172-110">En Ordenar toocreate un informe incrustado, *Dataset.Read y Workspace.Report.Create* ámbitos deben indicarse en el token de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="41172-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="41172-111">Crear nuevo informe de access token toocreate necesarios</span><span class="sxs-lookup"><span data-stu-id="41172-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="41172-112">Power BI Embedded usa tokens de inserción, que son JSON Web Tokens con forma HMAC.</span><span class="sxs-lookup"><span data-stu-id="41172-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="41172-113">Hola tokens se firman con la clave de acceso de hello en su colección Azure Power BI Embedded de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="41172-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="41172-114">Inserte tokens, de forma predeterminada, se usa tooprovide leer solo acceso tooa informe tooembed en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="41172-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="41172-115">Los tokens de inserción se emiten para un informe concreto y se deben asociar a una dirección URL de inserción.</span><span class="sxs-lookup"><span data-stu-id="41172-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="41172-116">Tokens de acceso deben crearse en el servidor de hello como teclas de acceso de hello son tokens de hello toosign/encrypt usado.</span><span class="sxs-lookup"><span data-stu-id="41172-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="41172-117">Para obtener información acerca de cómo toocreate un token de acceso, consulte [autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="41172-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="41172-118">También puede revisar hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método.</span><span class="sxs-lookup"><span data-stu-id="41172-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="41172-119">Este es un ejemplo de este aspecto usando Hola .NET SDK para Power BI.</span><span class="sxs-lookup"><span data-stu-id="41172-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="41172-120">En este ejemplo, tenemos nuestro Id. de conjunto de datos que se desea obtener toocreat Hola nuevo informe en.</span><span class="sxs-lookup"><span data-stu-id="41172-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="41172-121">También es necesario ámbitos de hello tooadd para *Dataset.Read y Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="41172-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="41172-122">Hola *PowerBIToken clase* requiere que instale hello [Power BI Core NuGut paquete](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="41172-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="41172-123">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="41172-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="41172-124">**Código de C#**</span><span class="sxs-lookup"><span data-stu-id="41172-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="41172-125">Creación de un informe en blanco nuevo</span><span class="sxs-lookup"><span data-stu-id="41172-125">Create a new blank report</span></span>

<span data-ttu-id="41172-126">En orden toocreate un nuevo informe, crear Hola se debe proporcionar la configuración.</span><span class="sxs-lookup"><span data-stu-id="41172-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="41172-127">Debe incluir token de acceso de hello, embedURL de Hola y Hola datasetID que queremos toocreate informe Hola.</span><span class="sxs-lookup"><span data-stu-id="41172-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="41172-128">Esto requiere que instale Hola nuget [paquete de Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="41172-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="41172-129">Hola embedUrl solo será https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="41172-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="41172-130">Puede usar hello [incrustar el informe de ejemplo JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="41172-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="41172-131">También proporciona ejemplos de código para las operaciones diferentes de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="41172-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="41172-132">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="41172-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="41172-133">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="41172-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="41172-134">Al llamar a *powerbi.createReport()* hará que un lienzo en blanco en modo de edición aparecen en hello *div* elemento.</span><span class="sxs-lookup"><span data-stu-id="41172-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="41172-135">Guardado de informes nuevos</span><span class="sxs-lookup"><span data-stu-id="41172-135">Save new reports</span></span>

<span data-ttu-id="41172-136">informe Hello no se creará realmente hasta que se llama a hello **Guardar como** operación.</span><span class="sxs-lookup"><span data-stu-id="41172-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="41172-137">lo que se puede hacer desde el menú archivo o desde JavaScript.</span><span class="sxs-lookup"><span data-stu-id="41172-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="41172-138">Los informes nuevo solo se pueden crear después de llamar a **save as**.</span><span class="sxs-lookup"><span data-stu-id="41172-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="41172-139">Después de guardar, lienzo Hola seguirá mostrando el conjunto de datos de hello en informe de no hello y el modo de edición.</span><span class="sxs-lookup"><span data-stu-id="41172-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="41172-140">Necesitará el nuevo informe de tooreload hello como lo haría con cualquier otro informe.</span><span class="sxs-lookup"><span data-stu-id="41172-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="41172-141">Carga Hola nuevo informe</span><span class="sxs-lookup"><span data-stu-id="41172-141">Load hello new report</span></span>

<span data-ttu-id="41172-142">En orden toointeract con nuevo informe de hello debe tooembed en hello llamada Hola igual aplicación hello incrusta un normal de informe, es decir, un nuevo token debe emitirse específicamente para el nuevo informe de hello y, a continuación, insertar el método.</span><span class="sxs-lookup"><span data-stu-id="41172-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="41172-143">Automatizar guardar y cargar de un nuevo informe utilizando Hola "guarda" evento</span><span class="sxs-lookup"><span data-stu-id="41172-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="41172-144">Proceso de pedido tooautomate Hola de "Guardar como..." y, a continuación, cargar nuevo informe de hello hacer que el uso de Hola "Guardar" evento.</span><span class="sxs-lookup"><span data-stu-id="41172-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="41172-145">Este evento se desencadena cuando se completa Hola operación de guardado y devuelve un objeto Json que contiene identificador nuevo informe, Hola que, el nombre del informe, el identificador informe anterior, que hello (si hay alguna) y si la operación de hello era saveAs o en Guardar.</span><span class="sxs-lookup"><span data-stu-id="41172-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="41172-146">proceso de hello tooAutomate puede escuchar en el evento Hola "guarda", tomar identificador nuevo informe, Hola que, crear nuevo token de Hola e incrustar informes nuevos de hello con él.</span><span class="sxs-lookup"><span data-stu-id="41172-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="41172-147">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="41172-147">See also</span></span>

[<span data-ttu-id="41172-148">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="41172-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="41172-149">Almacenamiento de informes</span><span class="sxs-lookup"><span data-stu-id="41172-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
<span data-ttu-id="41172-150">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="41172-150">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="41172-151">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="41172-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="41172-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="41172-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="41172-153">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="41172-153">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
[<span data-ttu-id="41172-154">Paquete NuGet Power BI Core</span><span class="sxs-lookup"><span data-stu-id="41172-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="41172-155">Paquete Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="41172-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="41172-156">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="41172-156">More questions?</span></span> [<span data-ttu-id="41172-157">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="41172-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
