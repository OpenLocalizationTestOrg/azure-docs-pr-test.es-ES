---
title: aaaToggle entre el modo de ver y editar informes en Azure Power BI Embedded | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootoggle entre el modo de ver y editar para los informes en Power BI Embedded."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="b7f77-103">Alternancia entre los modo de vista y de edición de informes en Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b7f77-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="b7f77-104">Obtenga información acerca de cómo tootoggle entre el modo de ver y editar para los informes en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b7f77-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="b7f77-105">Creación de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="b7f77-105">Creating an access token</span></span>

<span data-ttu-id="b7f77-106">Deberá toocreate un token de acceso que proporciona una vista de tooboth de capacidad de Hola y editar un informe.</span><span class="sxs-lookup"><span data-stu-id="b7f77-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="b7f77-107">tooedit y guardar un informe, deberá hello **Report.ReadWrite** permiso del token.</span><span class="sxs-lookup"><span data-stu-id="b7f77-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="b7f77-108">Para más información, consulte [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b7f77-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b7f77-109">Esto le permiten tooedit y guardar los cambios tooan de informe existente.</span><span class="sxs-lookup"><span data-stu-id="b7f77-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="b7f77-110">Si también desea que la función hello de admitir **Guardar como**, necesitará permisos adicionales de toosupply.</span><span class="sxs-lookup"><span data-stu-id="b7f77-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="b7f77-111">Para más información, consulte [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ámbitos).</span><span class="sxs-lookup"><span data-stu-id="b7f77-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="b7f77-112">Configuración de la inserción</span><span class="sxs-lookup"><span data-stu-id="b7f77-112">Embed configuration</span></span>

<span data-ttu-id="b7f77-113">Necesitará permisos de toosupply y un viewMode Hola de orden toosee guardar botón cuando está en modo de edición.</span><span class="sxs-lookup"><span data-stu-id="b7f77-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="b7f77-114">Para más información, consulte [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Detalles de configuración de la inserción).</span><span class="sxs-lookup"><span data-stu-id="b7f77-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="b7f77-115">Por ejemplo, en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="b7f77-115">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="b7f77-116">Esto indicará tooembed informe de hello en modo de vista en función del **viewMode** se establece demasiado**modelos. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="b7f77-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="b7f77-117">Modo de vista</span><span class="sxs-lookup"><span data-stu-id="b7f77-117">View mode</span></span>

<span data-ttu-id="b7f77-118">Puede usar Hola después tooswitch de JavaScript en modo de vista, si se encuentra en modo de edición.</span><span class="sxs-lookup"><span data-stu-id="b7f77-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="b7f77-119">Modo de edición</span><span class="sxs-lookup"><span data-stu-id="b7f77-119">Edit mode</span></span>

<span data-ttu-id="b7f77-120">Puede usar Hola después tooswitch de JavaScript en modo de edición, si se encuentra en la vista de modo.</span><span class="sxs-lookup"><span data-stu-id="b7f77-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="b7f77-121">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b7f77-121">See also</span></span>

[<span data-ttu-id="b7f77-122">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="b7f77-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
<span data-ttu-id="b7f77-123">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="b7f77-123">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="b7f77-124">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b7f77-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b7f77-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="b7f77-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
<span data-ttu-id="b7f77-126">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b7f77-126">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
[<span data-ttu-id="b7f77-127">Repositorio GIT PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="b7f77-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="b7f77-128">Repositorio GIT PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="b7f77-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="b7f77-129">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="b7f77-129">More questions?</span></span> [<span data-ttu-id="b7f77-130">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="b7f77-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
