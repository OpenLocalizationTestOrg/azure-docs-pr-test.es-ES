---
title: Guardado de informes en Azure Power BI Embedded | Microsoft Docs
description: "Aprenda a guardar informes en Power BI Embedded. Para que esta operación funcione correctamente, se requieren los permisos adecuados."
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
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="90841-104">Guardado de informes en Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="90841-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="90841-105">Aprenda a guardar informes en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="90841-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="90841-106">Para que esta operación funcione correctamente, se requieren los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="90841-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="90841-107">En Power BI Embedded, es posible editar los informes existentes y guardarlos.</span><span class="sxs-lookup"><span data-stu-id="90841-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="90841-108">También se puede crear un informe nuevo y guardarlo como un nuevo informe para crear uno.</span><span class="sxs-lookup"><span data-stu-id="90841-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="90841-109">Para guardar un informe, en primer lugar hay que crear un token para el informe concreto con los ámbitos correctos:</span><span class="sxs-lookup"><span data-stu-id="90841-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="90841-110">Para habilitar la operación save, se requiere el ámbito Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="90841-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="90841-111">Para habilitar la operación save as, se requieren los ámbitos Report.Read y Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="90841-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="90841-112">Para habilitar las operaciones save y save as, se requieren Report.ReadWrite y Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="90841-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="90841-113">Para habilitar los botones de save o save as, respectivamente, correctos en el menú archivo es preciso proporcionar el permiso adecuado en la configuración de la inserción al insertar el informe:</span><span class="sxs-lookup"><span data-stu-id="90841-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="90841-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="90841-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="90841-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="90841-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="90841-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="90841-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="90841-117">El token de acceso también necesita los ámbitos adecuados.</span><span class="sxs-lookup"><span data-stu-id="90841-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="90841-118">Para más información, consulte [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ámbitos).</span><span class="sxs-lookup"><span data-stu-id="90841-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="90841-119">Inserción de informes en modo de edición</span><span class="sxs-lookup"><span data-stu-id="90841-119">Embed report in edit mode</span></span>

<span data-ttu-id="90841-120">Supongamos que desea insertar un informe en modo de edición en la aplicación; para ello, simplemente pase las propiedades correctas en la configuración de la inserción y llame a powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="90841-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="90841-121">Tendrá que suministrar permisos y una propiedad viewMode para ver los botones de save y save as en modo de edición.</span><span class="sxs-lookup"><span data-stu-id="90841-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="90841-122">Para más información, consulte [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Detalles de configuración de la inserción).</span><span class="sxs-lookup"><span data-stu-id="90841-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="90841-123">Por ejemplo, en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="90841-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="90841-124">Ahora, se insertará un informe en la aplicación en modo de edición.</span><span class="sxs-lookup"><span data-stu-id="90841-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="90841-125">Guardar informe</span><span class="sxs-lookup"><span data-stu-id="90841-125">Save report</span></span>

<span data-ttu-id="90841-126">Después de insertar el informe en modo de edición con el token y los permisos adecuados puede guardar el informe desde el menú archivo o desde Javascript:</span><span class="sxs-lookup"><span data-stu-id="90841-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="90841-127">Guardar como</span><span class="sxs-lookup"><span data-stu-id="90841-127">Save as</span></span>

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
> <span data-ttu-id="90841-128">Solo después de *save as* se crea un informe nuevo.</span><span class="sxs-lookup"><span data-stu-id="90841-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="90841-129">Después de save, el lienzo sigue mostrando el informe anterior en modo de edición, no el nuevo informe.</span><span class="sxs-lookup"><span data-stu-id="90841-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="90841-130">Necesitará insertar el nuevo informe que se creó.</span><span class="sxs-lookup"><span data-stu-id="90841-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="90841-131">Esto requiere un nuevo token de acceso, ya que se crean por informe.</span><span class="sxs-lookup"><span data-stu-id="90841-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="90841-132">Después tendrá que cargar el informe nuevo después de *save as*.</span><span class="sxs-lookup"><span data-stu-id="90841-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="90841-133">Esta operación es similar a la inserción de cualquier informe.</span><span class="sxs-lookup"><span data-stu-id="90841-133">This is similar to embedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="90841-134">Consulte también</span><span class="sxs-lookup"><span data-stu-id="90841-134">See also</span></span>

[<span data-ttu-id="90841-135">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="90841-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
<span data-ttu-id="90841-136">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="90841-136">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="90841-137">Creación de un nuevo informe a partir de un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="90841-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="90841-138">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="90841-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="90841-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="90841-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="90841-140">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="90841-140">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="90841-141">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="90841-141">More questions?</span></span> [<span data-ttu-id="90841-142">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="90841-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)

