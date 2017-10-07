---
title: "una aplicación de WordPress en hello portal de Azure en cinco minutos aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de lo fácil que es toorun las aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación de WordPress. Vea los resultados inmediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="e2f27-104">Implementar una aplicación de WordPress en hello portal de Azure en cinco minutos</span><span class="sxs-lookup"><span data-stu-id="e2f27-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="e2f27-105">Este tutorial muestra cómo toodeploy su primer [WordPress](https://wordpress.org/) aplicación web demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) en minutos.</span><span class="sxs-lookup"><span data-stu-id="e2f27-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Sitio de WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="e2f27-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2f27-107">Prerequisites</span></span>
<span data-ttu-id="e2f27-108">Necesita una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f27-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="e2f27-109">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e2f27-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="e2f27-110">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f27-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="e2f27-111">Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.</span><span class="sxs-lookup"><span data-stu-id="e2f27-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="e2f27-112">Implementar la aplicación de WordPress hello</span><span class="sxs-lookup"><span data-stu-id="e2f27-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="e2f27-113">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2f27-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e2f27-114">Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="e2f27-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="e2f27-115">Este vínculo es un método abreviado tooimmediately configurar una nueva aplicación de WordPress en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f27-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="e2f27-116">En **Nombre de la aplicación**, escriba un nombre de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e2f27-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="e2f27-117">Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `azurewebsites.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="e2f27-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="e2f27-118">En **grupo de recursos**, haga clic en **crear nuevo** toocreate un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), a continuación, asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="e2f27-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="e2f27-119">En **Proveedor de base de datos**, seleccione **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="e2f27-120">Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="e2f27-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="e2f27-121">Configurar hello [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="e2f27-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="e2f27-122">En **plan de servicio de aplicaciones**, nombre de tipo hello deseado.</span><span class="sxs-lookup"><span data-stu-id="e2f27-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="e2f27-123">En **ubicación**, elegir una ubicación toohost el plan.</span><span class="sxs-lookup"><span data-stu-id="e2f27-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="e2f27-124">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="e2f27-125">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-125">Click **OK**.</span></span>

8. <span data-ttu-id="e2f27-126">Haga clic en **Base de datos** > **Create New** (Crear nueva).</span><span class="sxs-lookup"><span data-stu-id="e2f27-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="e2f27-127">Configurar base de datos SQL de hello tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="e2f27-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="e2f27-128">En **Nombre de la base de datos**, escriba un nombre para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e2f27-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="e2f27-129">En **ubicación**, elija Hola la misma ubicación que Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2f27-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="e2f27-130">Haga clic en **Plan de tarifa** y luego seleccione **Mercury** u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="e2f27-131">Haga clic en **Condiciones legales** y luego en **Compra**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="e2f27-132">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-132">Click **OK**.</span></span>

9. <span data-ttu-id="e2f27-133">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-133">Click **Create**.</span></span>

    <span data-ttu-id="e2f27-134">Ahora, Azure crea la aplicación de WordPress según su configuración.</span><span class="sxs-lookup"><span data-stu-id="e2f27-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="e2f27-135">Verá la notificación **Implementación iniciada...**</span><span class="sxs-lookup"><span data-stu-id="e2f27-135">You should see a **Deployment started...** notification.</span></span>

    ![Implementación iniciada: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="e2f27-137">Inicio y administración de la aplicación web de WordPress</span><span class="sxs-lookup"><span data-stu-id="e2f27-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="e2f27-138">Cuando Azure finalice la implementación de aplicación, verá otra notificación.</span><span class="sxs-lookup"><span data-stu-id="e2f27-138">When Azure completes app deployment you see another notification.</span></span>

![La implementación finalizó correctamente: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="e2f27-140">Haga clic en la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f27-140">Click hello notification.</span></span> <span data-ttu-id="e2f27-141">Si se lo haya perdido, siempre puede acceso haciendo clic en campana de notificación de hello (![siguientes notificación - WordPress primero en el servicio de aplicación de Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="e2f27-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="e2f27-142">Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="e2f27-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="e2f27-143">En la parte superior de Hola de página de información general de hello, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="e2f27-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Examinar: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="e2f27-145">Ahora puede ver Hola WordPress **bienvenida** página.</span><span class="sxs-lookup"><span data-stu-id="e2f27-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="e2f27-146">Configurar una instalación de WordPress de Hola y comenzar a jugar con él.</span><span class="sxs-lookup"><span data-stu-id="e2f27-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Configuración de WordPress: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="e2f27-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2f27-148">Next steps</span></span>
* <span data-ttu-id="e2f27-149">[Crear, configurar e implementar una tooAzure de aplicación web de Laravel](app-service-web-php-get-started.md) -adquirir conocimientos básicos de hello, necesita toorun cualquier aplicación web PHP en Azure, como:</span><span class="sxs-lookup"><span data-stu-id="e2f27-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="e2f27-150">Crear y configurar aplicaciones en Azure desde PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="e2f27-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="e2f27-151">Establecer la versión de PHP.</span><span class="sxs-lookup"><span data-stu-id="e2f27-151">Set PHP version.</span></span>
    * <span data-ttu-id="e2f27-152">Usar un archivo de inicio que no está en el directorio de la aplicación hello raíz.</span><span class="sxs-lookup"><span data-stu-id="e2f27-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="e2f27-153">Habilitar la automatización de Composer.</span><span class="sxs-lookup"><span data-stu-id="e2f27-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="e2f27-154">Acceder a variables de entorno específico.</span><span class="sxs-lookup"><span data-stu-id="e2f27-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="e2f27-155">Solucionar errores comunes.</span><span class="sxs-lookup"><span data-stu-id="e2f27-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="e2f27-156">[Implementar el servicio de aplicaciones de código tooAzure](web-sites-deploy.md)-Obtenga información acerca de cómo toodeploy de FTP o de origen controlar repositorios.</span><span class="sxs-lookup"><span data-stu-id="e2f27-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="e2f27-157">[Agregar funcionalidad tooyour primera web aplicación](app-service-web-get-started-2.md) -lleve su aplicación de Azure toohello siguiente nivel.</span><span class="sxs-lookup"><span data-stu-id="e2f27-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="e2f27-158">Autentique los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e2f27-158">Authenticate your users.</span></span> <span data-ttu-id="e2f27-159">Escálela según la demanda.</span><span class="sxs-lookup"><span data-stu-id="e2f27-159">Scale it based on demand.</span></span> <span data-ttu-id="e2f27-160">Configure algunas alertas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e2f27-160">Set up some performance alerts.</span></span> <span data-ttu-id="e2f27-161">Todo ello con unos cuantos clics.</span><span class="sxs-lookup"><span data-stu-id="e2f27-161">All with a few clicks.</span></span>
