---
title: Referencia para navegar en el portal de Azure
description: "Conozca las distintas experiencias de usuario web del Servicio de aplicaciones entre el portal de administración y el Portal de Azure."
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
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="e7174-103">Referencia para navegar en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e7174-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="e7174-104">Sitios web de Azure ahora se llama [Aplicaciones web del Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e7174-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e7174-105">Estamos actualizando toda nuestra documentación para reflejar este cambio de nombre y ofrecer instrucciones para el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="e7174-106">Hasta que este proceso se finalice, puede usar este documento como guía para trabajar con Aplicaciones web en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="e7174-107">El futuro del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e7174-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="e7174-108">Aunque observará los cambios de personalización de marca en el Portal de Azure clásico, dicho portal se está reemplazando por el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="e7174-109">Como el portal clásico va a quedar obsoleto, las novedades de desarrollo tienden a centrarse en Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="e7174-110">Todas las nuevas características de Aplicaciones web se incluirán en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="e7174-111">Comience a usar el Portal de Azure para beneficiarse de las mejores y más recientes ventajas que ofrecen las Aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e7174-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="e7174-112">Diferencias de diseño entre el Portal de Azure clásico y el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e7174-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="e7174-113">En el portal clásico, todos los servicios de Azure se muestran en la parte izquierda.</span><span class="sxs-lookup"><span data-stu-id="e7174-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="e7174-114">La navegación en este portal sigue una estructura de árbol, donde se empieza a partir del servicio y se navega a cada elemento.</span><span class="sxs-lookup"><span data-stu-id="e7174-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="e7174-115">Esta estructura funciona bien para administrar componentes independientes.</span><span class="sxs-lookup"><span data-stu-id="e7174-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="e7174-116">Si embargo, las aplicaciones integradas en Azure constituyen una colección de servicios interconectados y la estructura de árbol no es la ideal para trabajar con este tipo de colecciones.</span><span class="sxs-lookup"><span data-stu-id="e7174-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="e7174-117">El Portal de Azure facilita la compilación de aplicaciones completas con componentes de varios servicios.</span><span class="sxs-lookup"><span data-stu-id="e7174-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="e7174-118">El portal se organiza en *viajes*.</span><span class="sxs-lookup"><span data-stu-id="e7174-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="e7174-119">Un *viaje* es una serie de *hojas*, que funcionan como contenedores de los distintos componentes.</span><span class="sxs-lookup"><span data-stu-id="e7174-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="e7174-120">Por ejemplo, configurar el escalado automático para una aplicación web es un *viaje* que requiere varias hojas, como se muestra en el ejemplo siguiente: la hoja **sitio-web** (dicho título aún no se ha actualizado para usar la nueva terminología), la hoja **Configuración** y la hoja **Escalar horizontalmente**.</span><span class="sxs-lookup"><span data-stu-id="e7174-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="e7174-121">En el ejemplo, el ajuste de escala automático se configura para que dependa del uso de la CPU, por lo que también hay una hoja llamada **Porcentaje de CPU** .</span><span class="sxs-lookup"><span data-stu-id="e7174-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="e7174-122">Los componentes incluidos en las *hojas* se llaman *partes* y parecen iconos.</span><span class="sxs-lookup"><span data-stu-id="e7174-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="e7174-123">Ejemplo de navegación: crear una aplicación web</span><span class="sxs-lookup"><span data-stu-id="e7174-123">Navigation example: create a web app</span></span>
<span data-ttu-id="e7174-124">La creación de aplicaciones web sigue siendo muy fácil.</span><span class="sxs-lookup"><span data-stu-id="e7174-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="e7174-125">En la imagen siguiente se muestran el portal clásico y el portal en paralelo, para demostrar que el número de pasos necesarios para poner una aplicación web en marcha no ha cambiado significativamente.</span><span class="sxs-lookup"><span data-stu-id="e7174-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="e7174-126">En el portal puede elegir entre los tipos más comunes de aplicaciones web, incluidas conocidas aplicaciones de la galería como WordPress.</span><span class="sxs-lookup"><span data-stu-id="e7174-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="e7174-127">Para obtener una lista completa de las aplicaciones disponibles, visite [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="e7174-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="e7174-128">Al crear una aplicación web, se especifica la dirección URL, el plan del Servicio de aplicaciones y la ubicación en el portal de la misma forma que se hacía en el clásico.</span><span class="sxs-lookup"><span data-stu-id="e7174-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="e7174-129">Además, el portal permite definir otra configuración común.</span><span class="sxs-lookup"><span data-stu-id="e7174-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="e7174-130">Por ejemplo, los [grupos de recursos](../azure-resource-manager/resource-group-overview.md) simplifican la forma de ver y administrar recursos relacionados de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7174-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="e7174-131">Ejemplo de navegación: configuración y características</span><span class="sxs-lookup"><span data-stu-id="e7174-131">Navigation example: settings and features</span></span>
<span data-ttu-id="e7174-132">Todas las configuraciones y características se agrupan ahora de forma lógica en una sola hoja, a partir de la cual puede navegarse.</span><span class="sxs-lookup"><span data-stu-id="e7174-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="e7174-133">Por ejemplo, puede crear dominios personalizados si hace clic en **Dominios personalizados y SSL** en la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e7174-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="e7174-134">Para configurar una alerta de supervisión, haga clic en **Solicitudes y errores** y, a continuación, use **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="e7174-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="e7174-135">Para habilitar los diagnósticos, haga clic en **Registros de diagnóstico** en la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e7174-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="e7174-136">Para establecer la configuración de una aplicación, haga clic en **Configuración de la aplicación** en la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e7174-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="e7174-137">Aparte de la marca, algunos elementos más del portal se han cambiado de nombre o bien se han agrupado de forma distinta para encontrarlos más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="e7174-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="e7174-138">Por ejemplo, a continuación se incluye una captura de pantalla de la página correspondiente a la configuración de la aplicación (**Configurar**) en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="e7174-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="e7174-139">Más recursos</span><span class="sxs-lookup"><span data-stu-id="e7174-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="e7174-140">[Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="e7174-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="e7174-141">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e7174-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e7174-142">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="e7174-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e7174-143">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="e7174-143">What's changed</span></span>
* <span data-ttu-id="e7174-144">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e7174-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

