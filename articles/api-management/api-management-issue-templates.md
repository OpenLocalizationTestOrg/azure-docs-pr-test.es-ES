---
title: "plantillas de aaaIssue en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize Hola contenido de las páginas de problema de hello en el portal para desarrolladores de hello en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="9b9d3-103">Plantillas de problema en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="9b9d3-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="9b9d3-104">Administración de API de Azure proporciona que Hola contenido de hello toocustomize de capacidad de páginas del portal para desarrolladores con un conjunto de plantillas que configure su contenido.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9b9d3-105">Usar [DotLiquid](http://dotliquidmarkup.org/) editor hello y sintaxis de su elección, como [DotLiquid a los diseñadores](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), o cambie de tamaño un conjunto proporcionado de [los recursos de cadena](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), y [página controles](api-management-page-controls.md), tienen contenido de gran flexibilidad tooconfigure Hola de páginas de Hola como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9b9d3-106">las plantillas de Hello en esta sección permiten contenido de hello toocustomize de páginas de problema de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="9b9d3-107">Issue list</span><span class="sxs-lookup"><span data-stu-id="9b9d3-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="9b9d3-108">Plantillas predeterminadas de ejemplo se incluyen en hello siguiendo documentación, pero están toochange asunto debido toocontinuous mejoras.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="9b9d3-109">Puede ver plantillas de hello predeterminado en vivo en el portal para desarrolladores de hello desplazándose plantillas individuales toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="9b9d3-110">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="9b9d3-111"><a name="IssueList"></a> Issue list</span><span class="sxs-lookup"><span data-stu-id="9b9d3-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="9b9d3-112">Hola **lista de problemas de** plantilla permite cuerpo de hello toocustomize de página de lista de problema de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="9b9d3-113">![Lista de problemas del portal para desarrolladores](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Lista de problemas del portal para desarrolladores de APIM")</span><span class="sxs-lookup"><span data-stu-id="9b9d3-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9b9d3-114">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="9b9d3-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="9b9d3-115">Controles</span><span class="sxs-lookup"><span data-stu-id="9b9d3-115">Controls</span></span>  
 <span data-ttu-id="9b9d3-116">Hola `Issue list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9b9d3-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="9b9d3-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="9b9d3-118">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="9b9d3-118">Data model</span></span>  
  
|<span data-ttu-id="9b9d3-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9b9d3-119">Property</span></span>|<span data-ttu-id="9b9d3-120">Escriba</span><span class="sxs-lookup"><span data-stu-id="9b9d3-120">Type</span></span>|<span data-ttu-id="9b9d3-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="9b9d3-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="9b9d3-122">Issues</span><span class="sxs-lookup"><span data-stu-id="9b9d3-122">Issues</span></span>|<span data-ttu-id="9b9d3-123">Colección de entidades de [problema](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="9b9d3-124">Hola problemas toohello visible el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="9b9d3-125">Paginación</span><span class="sxs-lookup"><span data-stu-id="9b9d3-125">Paging</span></span>|<span data-ttu-id="9b9d3-126">Entidad [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="9b9d3-127">información de paginación de Hello para la colección de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="9b9d3-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="9b9d3-128">IsAuthenticated</span></span>|<span data-ttu-id="9b9d3-129">boolean</span><span class="sxs-lookup"><span data-stu-id="9b9d3-129">boolean</span></span>|<span data-ttu-id="9b9d3-130">Si el usuario actual de Hola es portal para desarrolladores de toohello con sesión iniciada.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="9b9d3-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="9b9d3-131">CanReportIssues</span></span>|<span data-ttu-id="9b9d3-132">boolean</span><span class="sxs-lookup"><span data-stu-id="9b9d3-132">boolean</span></span>|<span data-ttu-id="9b9d3-133">Si el usuario actual de hello tiene permisos toofile un problema.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="9b9d3-134">Search</span><span class="sxs-lookup"><span data-stu-id="9b9d3-134">Search</span></span>|<span data-ttu-id="9b9d3-135">string</span><span class="sxs-lookup"><span data-stu-id="9b9d3-135">string</span></span>|<span data-ttu-id="9b9d3-136">Esta propiedad está en desuso y no debe utilizarse.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="9b9d3-137">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="9b9d3-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="9b9d3-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b9d3-138">Next steps</span></span>
<span data-ttu-id="9b9d3-139">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
