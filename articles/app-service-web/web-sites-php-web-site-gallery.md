---
title: "aaaCreate una aplicación web de WordPress en el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un nuevo Azure web app para un blog de WordPress mediante Hola Portal de Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="90f50-103">Creación de una aplicación web de WordPress en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="90f50-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="90f50-104">Este tutorial muestra cómo toodeploy un blog de WordPress del sitio de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="90f50-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="90f50-105">Cuando haya terminado con el tutorial Hola tendrá su propio sitio de blog de WordPress seguridad y ejecutan en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Sitio de WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="90f50-107">Aprenderá a realizar los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="90f50-107">You'll learn:</span></span>

* <span data-ttu-id="90f50-108">¿Cómo toofind una plantilla de aplicación Hola Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="90f50-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="90f50-109">Cómo toocreate una aplicación web en la aplicación de Azure del servicio que se basa en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="90f50-110">Cómo tooconfigure configuración de servicio de aplicaciones de Azure para hello nuevo web app y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="90f50-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="90f50-111">Hello Azure Marketplace pone a disposición una amplia gama de aplicaciones web populares desarrollado por Microsoft, compañías de terceros e iniciativas de software de código abierto.</span><span class="sxs-lookup"><span data-stu-id="90f50-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="90f50-112">las aplicaciones web Hola se basan en una amplia gama de entornos populares, como [PHP](/develop/nodejs/) en este ejemplo WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), y [Python](/develop/python/), tooname un menor número.</span><span class="sxs-lookup"><span data-stu-id="90f50-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="90f50-113">una aplicación web de hello Azure Marketplace Hola solo software que necesita es explorador Hola que usa para hello toocreate [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90f50-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="90f50-114">sitio de WordPress Hola que se implementa en este tutorial usa MySQL para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="90f50-115">Si desea que use tooinstead base de datos SQL de base de datos de hello, consulte [Nami proyecto](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="90f50-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="90f50-116">**Proyecto Nami** también está disponible a través de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="90f50-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="90f50-117">toocomplete este tutorial, necesita una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90f50-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="90f50-118">Si aún no la tiene, puede [activar los beneficios de suscripción a Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) o bien [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="90f50-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="90f50-119">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="90f50-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="90f50-120">Ahí puede crear de forma inmediata una aplicación web de corta duración para iniciarse en Servicio de aplicaciones, no se requiere tarjeta de crédito y no se establece ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="90f50-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="90f50-121">Selección de WordPress y configuración para el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="90f50-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="90f50-122">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90f50-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90f50-123">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="90f50-123">Click **New**.</span></span>
   
    ![Crear nuevo][5]
3. <span data-ttu-id="90f50-125">Busque **WordPress** y haga clic en el icono **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="90f50-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="90f50-126">Si desea toouse base de datos de SQL en lugar de MySQL, busque **Nami proyecto**.</span><span class="sxs-lookup"><span data-stu-id="90f50-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress desde la lista][7]
4. <span data-ttu-id="90f50-128">Después de leer la descripción de Hola de aplicación de WordPress hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="90f50-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Crear](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="90f50-130">Escriba un nombre para la aplicación web de hello en hello **aplicación Web** cuadro.</span><span class="sxs-lookup"><span data-stu-id="90f50-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="90f50-131">Este nombre debe ser único en el dominio azurewebsites.net de hello porque Hola URL de aplicación web de hello será {nombre}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="90f50-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="90f50-132">Si el nombre de hello especificado no es único, una marca de exclamación roja aparece en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="90f50-133">Si tiene más de una suscripción, elija Hola uno desea toouse.</span><span class="sxs-lookup"><span data-stu-id="90f50-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="90f50-134">Seleccione un **Grupo de recursos** o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="90f50-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="90f50-135">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90f50-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="90f50-136">Seleccione un **Plan de servicio de aplicaciones/Ubicación** o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="90f50-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="90f50-137">Para obtener más información sobre los planes del Servicio de aplicaciones, consulte [Información general sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="90f50-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="90f50-138">Haga clic en **base de datos**y, a continuación, en hello **nueva base de datos de MySQL** hoja proporcionar valores de hello necesario para configurar la base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="90f50-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="90f50-139">a.</span><span class="sxs-lookup"><span data-stu-id="90f50-139">a.</span></span> <span data-ttu-id="90f50-140">Escriba un nombre nuevo o deje el nombre predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="90f50-141">b.</span><span class="sxs-lookup"><span data-stu-id="90f50-141">b.</span></span> <span data-ttu-id="90f50-142">Deje hello **tipo de base de datos** establecido demasiado**Shared**.</span><span class="sxs-lookup"><span data-stu-id="90f50-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="90f50-143">c.</span><span class="sxs-lookup"><span data-stu-id="90f50-143">c.</span></span> <span data-ttu-id="90f50-144">Elija Hola misma ubicación como Hola que eligió para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="90f50-145">d.</span><span class="sxs-lookup"><span data-stu-id="90f50-145">d.</span></span> <span data-ttu-id="90f50-146">Elija un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="90f50-146">Choose a pricing tier.</span></span> <span data-ttu-id="90f50-147">Para este tutorial sirve Mercurio (gratis con un mínimo de conexiones y espacio en disco).</span><span class="sxs-lookup"><span data-stu-id="90f50-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="90f50-148">Hola **nueva base de datos de MySQL** hoja, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="90f50-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="90f50-149">Hola **WordPress** hoja, acepte los términos legales de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="90f50-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Configuración de la aplicación web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="90f50-151">Servicio de aplicaciones de Azure crea hello web app, normalmente en menos de un minuto.</span><span class="sxs-lookup"><span data-stu-id="90f50-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="90f50-152">Puede ver el progreso de Hola haciendo clic en un icono de campana hello en parte superior de Hola de página del portal Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Indicador de progreso](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="90f50-154">Inicio y administración de la aplicación web de WordPress</span><span class="sxs-lookup"><span data-stu-id="90f50-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="90f50-155">Cuando haya finalizado la creación de aplicaciones web de hello, navegue en grupo de recursos de toohello de hello Portal de Azure en el que ha creado la aplicación hello y puede ver la aplicación web de hello y base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="90f50-156">Hola recurso adicional con el icono de bombilla de hello es [Application Insights](/services/application-insights/), que proporciona servicios de supervisión de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="90f50-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="90f50-157">Hola **grupo de recursos** hoja, haga clic en línea de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Configuración de la aplicación web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="90f50-159">En la hoja de la aplicación hello Web, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="90f50-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![URL del sitio][browse]
4. <span data-ttu-id="90f50-161">Hola WordPress **bienvenida** página, escriba la información de configuración de hello requerida por WordPress y, a continuación, haga clic en **instalar WordPress**.</span><span class="sxs-lookup"><span data-stu-id="90f50-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configuración de WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="90f50-163">Inicie sesión con credenciales de Hola que creó en hello **bienvenida** página.</span><span class="sxs-lookup"><span data-stu-id="90f50-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="90f50-164">Se abre la página Panel del sitio.</span><span class="sxs-lookup"><span data-stu-id="90f50-164">Your site Dashboard page opens.</span></span>    
   
    ![Sitio de WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="90f50-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90f50-166">Next steps</span></span>
<span data-ttu-id="90f50-167">Ha visto cómo toocreate e implementar una aplicación web PHP desde la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="90f50-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="90f50-168">Para obtener más información acerca del uso de PHP en Azure, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="90f50-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="90f50-169">Para obtener más información acerca de cómo toowork con la aplicación del servicio de aplicaciones Web, vea los vínculos de hello en hello parte izquierda de la página de hello (por ventanas del explorador extensa) o al principio de Hola de página de hello (por ventanas del explorador estrechos).</span><span class="sxs-lookup"><span data-stu-id="90f50-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="90f50-170">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="90f50-170">What's changed</span></span>
* <span data-ttu-id="90f50-171">Para que un cambio de toohello Guía de tooApp servicio de sitios Web, consulte [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="90f50-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
