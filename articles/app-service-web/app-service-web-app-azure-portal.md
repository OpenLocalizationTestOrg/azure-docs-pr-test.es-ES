---
title: aaaReference para navegar por hello portal de Azure
description: "Obtenga información acerca de hello experiencias de usuario diferentes para la aplicación de servicio Web entre el portal de administración de Hola y Hola Portal de Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a><span data-ttu-id="a7ab8-103">Referencia para navegar por hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab8-103">Reference for navigating hello Azure portal</span></span>
<span data-ttu-id="a7ab8-104">Sitios web de Azure ahora se llama [Aplicaciones web del Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a7ab8-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="a7ab8-105">Estamos actualizando todos nuestro tooreflect documentación este nombre cambio y tooprovide las instrucciones de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-105">We're updating all of our documentation tooreflect this name change and tooprovide instructions for hello Azure Portal.</span></span> <span data-ttu-id="a7ab8-106">Hasta que se realiza este proceso, puede usar este documento como guía para trabajar con aplicaciones Web de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-106">Until that process is done, you can use this document as a guide for working with Web Apps in hello Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a><span data-ttu-id="a7ab8-107">Hola futuro de hello Portal clásico de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab8-107">hello future of hello Azure Classic Portal</span></span>
<span data-ttu-id="a7ab8-108">Mientras que observará Hola cambios en el Portal de Azure clásico Hola de marca, ese portal está en proceso de Hola de que será reemplazada por hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-108">While you will notice hello branding changes on hello Azure Classic Portal, that portal is in hello process of being replaced by hello Azure Portal.</span></span> <span data-ttu-id="a7ab8-109">Tal y como está desapareciendo portal clásico de hello, foco de hello para el nuevo desarrollo está cambiando toohello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-109">As hello classic portal is being phased out, hello focus for new development is shifting toohello Azure Portal.</span></span> <span data-ttu-id="a7ab8-110">Todas las próximas características nuevas para las aplicaciones Web aparecerá en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-110">All upcoming new features for Web Apps will come in hello Azure Portal.</span></span> <span data-ttu-id="a7ab8-111">Empezar a usar hello Azure Portal tootake aprovechar Hola mayor que las aplicaciones Web tienen toooffer y más reciente.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-111">Start using hello Azure Portal tootake advantage of hello latest and greatest that Web Apps have toooffer.</span></span>

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="a7ab8-112">Diferencias de diseño entre Hola Portal clásico de Azure y el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab8-112">Layout differences between hello Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="a7ab8-113">En el portal clásico de hello, todos hello Azure services se muestran en hello del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-113">In hello classic portal, all hello Azure services are listed on hello left hand side.</span></span> <span data-ttu-id="a7ab8-114">La navegación en el portal clásico de hello sigue una estructura de árbol, donde inicio del servicio de Hola y navegue a cada elemento.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-114">Navigation in hello classic portal follows a tree structure, where you start from hello service and navigate into each element.</span></span> <span data-ttu-id="a7ab8-115">Esta estructura funciona bien para administrar componentes independientes.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="a7ab8-116">Si embargo, las aplicaciones integradas en Azure constituyen una colección de servicios interconectados y la estructura de árbol no es la ideal para trabajar con este tipo de colecciones.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="a7ab8-117">Hola portal de Azure hace fácil toobuild aplicaciones-to-end con componentes de varios servicios.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-117">hello Azure portal makes it easy toobuild applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="a7ab8-118">portal de Hola se organiza como *viajes*.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-118">hello portal is organized as *journeys*.</span></span> <span data-ttu-id="a7ab8-119">A *viaje* es una serie de *hojas*, que son contenedores de hello diferentes componentes.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-119">A *journey* is a series of *blades*, which are containers for hello different components.</span></span> <span data-ttu-id="a7ab8-120">Por ejemplo, establecer el escalado automático para una aplicación web es un *viaje* que toma varias hojas de tal y como se muestra en el siguiente ejemplo de Hola: Hola **sitio web** hoja (que título de hoja no se ha recibido toouse actualizada Hola terminología nueva), hello **configuración** hello y hoja **escalar horizontalmente** hoja.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in hello following example: hello **web-site** blade (that blade title has not yet been updated toouse hello new terminology), hello **Settings** blade, and hello **Scale out** blade.</span></span> <span data-ttu-id="a7ab8-121">En el ejemplo de Hola, escalado automático se va a configurar toodepend en el uso de CPU, por lo que es también un **porcentaje de CPU** hoja.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-121">In hello example, auto scaling is being set up toodepend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="a7ab8-122">Hola componentes dentro de hello *hojas* se denominan *elementos*, que el aspecto iconos.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-122">hello components within hello *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="a7ab8-123">Ejemplo de navegación: crear una aplicación web</span><span class="sxs-lookup"><span data-stu-id="a7ab8-123">Navigation example: create a web app</span></span>
<span data-ttu-id="a7ab8-124">La creación de aplicaciones web sigue siendo muy fácil.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="a7ab8-125">Hola siguiente imagen muestra hello clásico hello y portal portal side-by-side toodemonstrate que no ha cambiado mucho en número de Hola de pasos necesarios tooget una aplicación web de seguridad y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-125">hello following image shows hello classic portal and hello portal side-by-side toodemonstrate that not much has changed in hello number of steps needed tooget a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="a7ab8-126">En el portal de hello puede elegir entre tipos más comunes de Hola de las aplicaciones web, incluidas las aplicaciones de la Galería populares como WordPress.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-126">In hello portal you can choose from hello most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="a7ab8-127">Para obtener una lista completa de las aplicaciones disponibles, visite hello [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="a7ab8-127">For a full list of available applications, visit hello [Azure Marketplace].</span></span>

<span data-ttu-id="a7ab8-128">Cuando se crea una aplicación web, especificar la dirección URL, el plan de servicio de aplicaciones y ubicación en el portal de hello igual que lo haría en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-128">When you create a web app, you specify URL, App Service plan, and location in hello portal just as you do in hello classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="a7ab8-129">Además, la opción Hola portal le permite definir otras opciones de configuración comunes.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-129">In addition, hello portal lets you define other common settings.</span></span> <span data-ttu-id="a7ab8-130">Por ejemplo, [grupos de recursos](../azure-resource-manager/resource-group-overview.md) hacerla toosee simple y administrar recursos relacionados con Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple toosee and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="a7ab8-131">Ejemplo de navegación: configuración y características</span><span class="sxs-lookup"><span data-stu-id="a7ab8-131">Navigation example: settings and features</span></span>
<span data-ttu-id="a7ab8-132">Todos los valores de Hola y características ahora se agrupan lógicamente en una sola hoja, desde la que puede navegar.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-132">All hello settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="a7ab8-133">Por ejemplo, puede crear dominios personalizados haciendo clic en **los dominios personalizados y SSL** en hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-133">For example, you can create custom domains by clicking **Custom domains and SSL** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="a7ab8-134">tooset una alerta de supervisión, haga clic en **solicitudes y errores** y, a continuación, **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-134">tooset up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="a7ab8-135">Diagnósticos de tooenable, haga clic en **registros de diagnóstico** en hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-135">tooenable diagnostics, click **Diagnostics logs** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="a7ab8-136">Haga clic en configuración de la aplicación de tooconfigure **configuración de la aplicación** en hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-136">tooconfigure application settings, click **Application settings** in hello **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="a7ab8-137">Que no sea el nombre de la marca de hello, se han cambiado de nombre o agrupan de forma diferente algunas cosas en el portal de Hola toomake se toofind más fácil de ellos.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-137">Other than hello brand name, a few things in hello portal have been renamed or grouped differently toomake it easier toofind them.</span></span> <span data-ttu-id="a7ab8-138">Por ejemplo, a continuación se muestra una captura de pantalla de página correspondiente de hello para la configuración de la aplicación (**configurar**) en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-138">For example, below is a screenshot of hello corresponding page for app settings (**Configure**) in hello classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="a7ab8-139">Más recursos</span><span class="sxs-lookup"><span data-stu-id="a7ab8-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> <span data-ttu-id="a7ab8-141">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-141">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a7ab8-142">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a7ab8-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a7ab8-143">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a7ab8-143">What's changed</span></span>
* <span data-ttu-id="a7ab8-144">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a7ab8-144">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

