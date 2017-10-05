---
title: "Creación de un nuevo informe a partir de un conjunto de datos en Azure Power BI Embedded | Microsoft Docs"
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="35005-103">Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="35005-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="35005-104">Los informes de Power BI Embedded ahora se puede crear a partir de un conjunto de datos de su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="35005-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="35005-105">El método de autenticación es similar al de la inserción de informes.</span><span class="sxs-lookup"><span data-stu-id="35005-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="35005-106">Se basa en tokens de acceso que son específicos de un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="35005-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="35005-107">Los tokens que se usan para PowerBI.com los emite Azure Active Directory (AAD), mientras que los de Power BI Embedded los emite su propio servicio.</span><span class="sxs-lookup"><span data-stu-id="35005-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="35005-108">Cuando se crea un informe insertado, los tokens emitidos son para un conjunto de datos concreto.</span><span class="sxs-lookup"><span data-stu-id="35005-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="35005-109">Los tokens deben asociarse a la dirección URL de inserción del mismo elemento para asegurarse de que cada uno de ellos tiene un token único.</span><span class="sxs-lookup"><span data-stu-id="35005-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="35005-110">Para crear un informe insertado, se deben proporcionar los ámbitos *Dataset.Read y Workspace.Report.Create* en el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="35005-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="35005-111">Creación de los tokens de acceso necesarios para crear un informe nuevo</span><span class="sxs-lookup"><span data-stu-id="35005-111">Create access token needed to create new report</span></span>

<span data-ttu-id="35005-112">Power BI Embedded usa tokens de inserción, que son JSON Web Tokens con forma HMAC.</span><span class="sxs-lookup"><span data-stu-id="35005-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="35005-113">Los tokens se firman con la clave de acceso de la colección de áreas de trabajo de Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="35005-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="35005-114">De manera predeterminada, los tokens de inserción se utilizan para proporcionar acceso de solo lectura a un informe para insertarlo en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="35005-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="35005-115">Los tokens de inserción se emiten para un informe concreto y se deben asociar a una dirección URL de inserción.</span><span class="sxs-lookup"><span data-stu-id="35005-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="35005-116">Los tokens de acceso deben crearse en el servidor, ya que las claves de acceso se utilizan para firmar o cifrar los tokens.</span><span class="sxs-lookup"><span data-stu-id="35005-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="35005-117">Para obtener información acerca de cómo crear un token de acceso, consulte [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="35005-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="35005-118">También puede revisar el método [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="35005-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="35005-119">Aquí hay un ejemplo de cómo sería si se usara el SDK de .NET de Power BI.</span><span class="sxs-lookup"><span data-stu-id="35005-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="35005-120">En este ejemplo, tenemos nuestro un id. del conjunto de datos en el deseamos crear el nuevo informe.</span><span class="sxs-lookup"><span data-stu-id="35005-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="35005-121">También es preciso agregar los ámbitos de *Dataset.Read y Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="35005-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="35005-122">La *clase PowerBIToken* requiere que instale el [paquete NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="35005-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="35005-123">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="35005-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="35005-124">**Código de C#**</span><span class="sxs-lookup"><span data-stu-id="35005-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="35005-125">Creación de un informe en blanco nuevo</span><span class="sxs-lookup"><span data-stu-id="35005-125">Create a new blank report</span></span>

<span data-ttu-id="35005-126">Para crear un informe nuevo, debe proporcionarse la configuración de creación.</span><span class="sxs-lookup"><span data-stu-id="35005-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="35005-127">Aquí se debe incluir el token de acceso y los valores de embedURL y el datasetID con los que deseamos crear el informe.</span><span class="sxs-lookup"><span data-stu-id="35005-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="35005-128">Esto requiere instalar el paquete NuGet [Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="35005-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="35005-129">El valor de embedUrl será https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="35005-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="35005-130">Puede usar el [ejemplo de inserción de informe JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="35005-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="35005-131">También proporciona ejemplos de código de las distintas operaciones que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="35005-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="35005-132">**Instalación de un paquete NuGet**</span><span class="sxs-lookup"><span data-stu-id="35005-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="35005-133">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="35005-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="35005-134">Al llamar a *powerbi.createReport()* aparecerá un lienzo en blanco en modo de edición en el elemento *div*.</span><span class="sxs-lookup"><span data-stu-id="35005-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="35005-135">Guardado de informes nuevos</span><span class="sxs-lookup"><span data-stu-id="35005-135">Save new reports</span></span>

<span data-ttu-id="35005-136">El informe no se creará hasta que llame a la operación **save as**,</span><span class="sxs-lookup"><span data-stu-id="35005-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="35005-137">lo que se puede hacer desde el menú archivo o desde JavaScript.</span><span class="sxs-lookup"><span data-stu-id="35005-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="35005-138">Los informes nuevo solo se pueden crear después de llamar a **save as**.</span><span class="sxs-lookup"><span data-stu-id="35005-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="35005-139">Después de guardar, el lienzo seguirá mostrando el conjunto de datos en modo de edición y no el informe.</span><span class="sxs-lookup"><span data-stu-id="35005-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="35005-140">Será preciso que vuelva a cargar el informe nuevo como cualquier otro informe.</span><span class="sxs-lookup"><span data-stu-id="35005-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="35005-141">Carga del nuevo informe</span><span class="sxs-lookup"><span data-stu-id="35005-141">Load the new report</span></span>

<span data-ttu-id="35005-142">Para interactuar con el nuevo informe es preciso que lo inserte de la misma manera en que la aplicación inserta un informe normal, es decir, se debe emitir un token nuevo específico para el nuevo informe y, después, llame al método de inserción.</span><span class="sxs-lookup"><span data-stu-id="35005-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="35005-143">Guardado y carga automáticos de un informe nuevo mediante el informe "guardado"</span><span class="sxs-lookup"><span data-stu-id="35005-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="35005-144">Para automatizar el proceso de "save as" y cargar el informe nuevo, puede usar el evento "guardado".</span><span class="sxs-lookup"><span data-stu-id="35005-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="35005-145">Este evento se desencadena cuando se completa la operación save y devuelve un objeto Json que contiene el identificador nuevo reportId, el nombre del informe, el reportId anterior (si hay) y si la operación fue saveAs o save.</span><span class="sxs-lookup"><span data-stu-id="35005-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="35005-146">Para automatizar el proceso puede escuchar el evento "guardado", tomar el nuevo reportId, crear el nuevo token e insertar el nuevo informe.</span><span class="sxs-lookup"><span data-stu-id="35005-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="35005-147">Consulte también</span><span class="sxs-lookup"><span data-stu-id="35005-147">See also</span></span>

[<span data-ttu-id="35005-148">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="35005-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="35005-149">Almacenamiento de informes</span><span class="sxs-lookup"><span data-stu-id="35005-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
<span data-ttu-id="35005-150">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="35005-150">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="35005-151">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="35005-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="35005-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="35005-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="35005-153">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="35005-153">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
[<span data-ttu-id="35005-154">Paquete NuGet Power BI Core</span><span class="sxs-lookup"><span data-stu-id="35005-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="35005-155">Paquete Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="35005-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="35005-156">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="35005-156">More questions?</span></span> [<span data-ttu-id="35005-157">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="35005-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)