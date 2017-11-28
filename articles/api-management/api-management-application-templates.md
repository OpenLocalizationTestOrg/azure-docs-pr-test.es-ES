---
title: "plantillas de aaaApplication en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize Hola contenido de las páginas de aplicación hello en el portal para desarrolladores de hello en la administración de API de Azure."
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
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="8dc45-103">Plantillas de aplicación en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="8dc45-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="8dc45-104">Administración de API de Azure proporciona que Hola contenido de hello toocustomize de capacidad de páginas del portal para desarrolladores con un conjunto de plantillas que configure su contenido.</span><span class="sxs-lookup"><span data-stu-id="8dc45-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="8dc45-105">Usar [DotLiquid](http://dotliquidmarkup.org/) editor hello y sintaxis de su elección, como [DotLiquid a los diseñadores](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), o cambie de tamaño un conjunto proporcionado de [los recursos de cadena](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), y [página controles](api-management-page-controls.md), tienen contenido de gran flexibilidad tooconfigure Hola de páginas de Hola como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="8dc45-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="8dc45-106">las plantillas de Hello en esta sección permiten contenido de hello toocustomize de páginas de la aplicación hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc45-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="8dc45-107">Application list</span><span class="sxs-lookup"><span data-stu-id="8dc45-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="8dc45-108">Aplicación</span><span class="sxs-lookup"><span data-stu-id="8dc45-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="8dc45-109">Plantillas predeterminadas de ejemplo se incluyen en hello siguiendo documentación, pero están toochange asunto debido toocontinuous mejoras.</span><span class="sxs-lookup"><span data-stu-id="8dc45-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="8dc45-110">Puede ver plantillas de hello predeterminado en vivo en el portal para desarrolladores de hello desplazándose plantillas individuales toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="8dc45-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="8dc45-111">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="8dc45-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="8dc45-112"><a name="ProductList"></a> Application list</span><span class="sxs-lookup"><span data-stu-id="8dc45-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="8dc45-113">Hola **lista de aplicaciones** plantilla permite cuerpo de hello toocustomize de página de lista de aplicaciones de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc45-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8dc45-114">![Plantillas del portal para desarrolladores de la página de lista de aplicaciones](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de lista de aplicaciones de APIM")</span><span class="sxs-lookup"><span data-stu-id="8dc45-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8dc45-115">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="8dc45-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="8dc45-116">Controles</span><span class="sxs-lookup"><span data-stu-id="8dc45-116">Controls</span></span>  
 <span data-ttu-id="8dc45-117">Hola `Product list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8dc45-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="8dc45-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="8dc45-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="8dc45-119">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="8dc45-119">Data model</span></span>  
  
|<span data-ttu-id="8dc45-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8dc45-120">Property</span></span>|<span data-ttu-id="8dc45-121">Escriba</span><span class="sxs-lookup"><span data-stu-id="8dc45-121">Type</span></span>|<span data-ttu-id="8dc45-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="8dc45-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="8dc45-123">Paginación</span><span class="sxs-lookup"><span data-stu-id="8dc45-123">Paging</span></span>|<span data-ttu-id="8dc45-124">Entidad [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="8dc45-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="8dc45-125">información de paginación de Hello para la colección de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc45-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="8dc45-126">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8dc45-126">Applications</span></span>|<span data-ttu-id="8dc45-127">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="8dc45-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="8dc45-128">Hola aplicaciones toohello visible el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="8dc45-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="8dc45-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="8dc45-129">CategoryName</span></span>|<span data-ttu-id="8dc45-130">cadena</span><span class="sxs-lookup"><span data-stu-id="8dc45-130">string</span></span>|<span data-ttu-id="8dc45-131">categoría de Hola de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8dc45-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="8dc45-132">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="8dc45-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="8dc45-133"><a name="Application"></a> Application</span><span class="sxs-lookup"><span data-stu-id="8dc45-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="8dc45-134">Hola **aplicación** plantilla permite cuerpo de hello toocustomize de página de la aplicación hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc45-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8dc45-135">![Plantillas del portal para desarrolladores de la página de aplicación](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de aplicación de APIM")</span><span class="sxs-lookup"><span data-stu-id="8dc45-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8dc45-136">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="8dc45-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="8dc45-137">Controles</span><span class="sxs-lookup"><span data-stu-id="8dc45-137">Controls</span></span>  
 <span data-ttu-id="8dc45-138">Hola `Application` plantilla no permite el uso de Hola de cualquier [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8dc45-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="8dc45-139">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="8dc45-139">Data model</span></span>  
 <span data-ttu-id="8dc45-140">Entidad [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="8dc45-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="8dc45-141">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="8dc45-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="8dc45-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8dc45-142">Next steps</span></span>
<span data-ttu-id="8dc45-143">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8dc45-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
