---
title: "Plantillas de aplicación en Azure API Management | Microsoft Docs"
description: "Aprenda a personalizar el contenido de las páginas de aplicación del portal para desarrolladores en Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="f330d-103">Plantillas de aplicación en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f330d-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="f330d-104">Azure API Management le ofrece la posibilidad de personalizar el contenido de las páginas del portal para desarrolladores mediante un conjunto de plantillas que configuran su contenido.</span><span class="sxs-lookup"><span data-stu-id="f330d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="f330d-105">Por medio de la sintaxis [DotLiquid](http://dotliquidmarkup.org/) y el editor que prefiera, como [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) (DotLiquid para diseñadores), y un conjunto proporcionado de [recursos de cadena](api-management-template-resources.md#strings), [recursos de glifo](api-management-template-resources.md#glyphs) y [controles de página](api-management-page-controls.md) localizados, puede disponer de una gran flexibilidad para configurar el contenido de las páginas como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="f330d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="f330d-106">Las plantillas de esta sección le permiten personalizar el contenido de las páginas de Application en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="f330d-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="f330d-107">Application list</span><span class="sxs-lookup"><span data-stu-id="f330d-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="f330d-108">Aplicación</span><span class="sxs-lookup"><span data-stu-id="f330d-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="f330d-109">En la siguiente documentación se incluyen plantillas predeterminadas de ejemplo; sin embargo, están sujetas a cambios debido a mejoras continuas.</span><span class="sxs-lookup"><span data-stu-id="f330d-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="f330d-110">Puede ver las plantillas predeterminadas en vivo en el portal para desarrolladores; para ello, vaya hasta a las plantillas individuales que desee.</span><span class="sxs-lookup"><span data-stu-id="f330d-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="f330d-111">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="f330d-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="f330d-112"><a name="ProductList"></a> Application list</span><span class="sxs-lookup"><span data-stu-id="f330d-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="f330d-113">La plantilla **Application list** le permite personalizar el cuerpo de la página de lista de aplicaciones en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="f330d-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="f330d-114">![Plantillas del portal para desarrolladores de la página de lista de aplicaciones](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de lista de aplicaciones de APIM")</span><span class="sxs-lookup"><span data-stu-id="f330d-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="f330d-115">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="f330d-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="f330d-116">Controles</span><span class="sxs-lookup"><span data-stu-id="f330d-116">Controls</span></span>  
 <span data-ttu-id="f330d-117">La plantilla `Product list` puede usar los siguientes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="f330d-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="f330d-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="f330d-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="f330d-119">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="f330d-119">Data model</span></span>  
  
|<span data-ttu-id="f330d-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f330d-120">Property</span></span>|<span data-ttu-id="f330d-121">Escriba</span><span class="sxs-lookup"><span data-stu-id="f330d-121">Type</span></span>|<span data-ttu-id="f330d-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="f330d-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="f330d-123">Paginación</span><span class="sxs-lookup"><span data-stu-id="f330d-123">Paging</span></span>|<span data-ttu-id="f330d-124">Entidad [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="f330d-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="f330d-125">La información de paginación de la colección de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f330d-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="f330d-126">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f330d-126">Applications</span></span>|<span data-ttu-id="f330d-127">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="f330d-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="f330d-128">Las aplicaciones visibles para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="f330d-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="f330d-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="f330d-129">CategoryName</span></span>|<span data-ttu-id="f330d-130">string</span><span class="sxs-lookup"><span data-stu-id="f330d-130">string</span></span>|<span data-ttu-id="f330d-131">La categoría de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f330d-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="f330d-132">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="f330d-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="f330d-133"><a name="Application"></a> Application</span><span class="sxs-lookup"><span data-stu-id="f330d-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="f330d-134">La plantilla **Application** le permite personalizar el cuerpo de la página de aplicación en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="f330d-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="f330d-135">![Plantillas del portal para desarrolladores de la página de aplicación](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de aplicación de APIM")</span><span class="sxs-lookup"><span data-stu-id="f330d-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="f330d-136">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="f330d-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="f330d-137">Controles</span><span class="sxs-lookup"><span data-stu-id="f330d-137">Controls</span></span>  
 <span data-ttu-id="f330d-138">La plantilla `Application` no permite el uso de ningún [control de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="f330d-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="f330d-139">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="f330d-139">Data model</span></span>  
 <span data-ttu-id="f330d-140">Entidad [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="f330d-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="f330d-141">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="f330d-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="f330d-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f330d-142">Next steps</span></span>
<span data-ttu-id="f330d-143">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f330d-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>