---
title: "Implementación de una aplicación de WordPress en Azure Portal en cinco minutos | Microsoft Docs"
description: "Aprenda lo fácil que es ejecutar aplicaciones web en App Service mediante la implementación de una aplicación de WordPress. Vea los resultados inmediatamente."
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
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="d26a4-104">Implementación de una aplicación de WordPress en Azure Portal en cinco minutos</span><span class="sxs-lookup"><span data-stu-id="d26a4-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="d26a4-105">En este tutorial se muestra cómo implementar su primera aplicación web de [WordPress](https://wordpress.org/) en [Azure App Service](../app-service/app-service-value-prop-what-is.md) en cuestión de minutos.</span><span class="sxs-lookup"><span data-stu-id="d26a4-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Sitio de WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="d26a4-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d26a4-107">Prerequisites</span></span>
<span data-ttu-id="d26a4-108">Necesita una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d26a4-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="d26a4-109">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d26a4-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="d26a4-110">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d26a4-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="d26a4-111">Cree una aplicación de inicio y juegue con ella durante una hora como máximo; no se requiere ninguna tarjeta de crédito ni ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d26a4-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="d26a4-112">Implementación de la aplicación de WordPress</span><span class="sxs-lookup"><span data-stu-id="d26a4-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="d26a4-113">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d26a4-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d26a4-114">Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="d26a4-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="d26a4-115">Este vínculo es un acceso directo para configurar inmediatamente una nueva aplicación de WordPress en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d26a4-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="d26a4-116">En **Nombre de la aplicación**, escriba un nombre de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d26a4-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="d26a4-117">Verá una marca de verificación verde en el cuadro si el nombre es único en el dominio `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d26a4-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="d26a4-118">En **Grupo de recursos**, haga clic en **Create new** (Crear nuevo) para crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) y, luego, asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="d26a4-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="d26a4-119">En **Proveedor de base de datos**, seleccione **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="d26a4-120">Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="d26a4-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="d26a4-121">Configure el [plan de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="d26a4-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="d26a4-122">En **Plan de App Service**, escriba el nombre deseado.</span><span class="sxs-lookup"><span data-stu-id="d26a4-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="d26a4-123">En **Ubicación**, elija una ubicación para hospedar el plan.</span><span class="sxs-lookup"><span data-stu-id="d26a4-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="d26a4-124">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d26a4-125">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-125">Click **OK**.</span></span>

8. <span data-ttu-id="d26a4-126">Haga clic en **Base de datos** > **Create New** (Crear nueva).</span><span class="sxs-lookup"><span data-stu-id="d26a4-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="d26a4-127">Configure la base de datos SQL tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="d26a4-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="d26a4-128">En **Nombre de la base de datos**, escriba un nombre para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="d26a4-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="d26a4-129">En **Ubicación**, elija la misma ubicación que el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="d26a4-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="d26a4-130">Haga clic en **Plan de tarifa** y luego seleccione **Mercury** u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d26a4-131">Haga clic en **Condiciones legales** y luego en **Compra**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="d26a4-132">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-132">Click **OK**.</span></span>

9. <span data-ttu-id="d26a4-133">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-133">Click **Create**.</span></span>

    <span data-ttu-id="d26a4-134">Ahora, Azure crea la aplicación de WordPress según su configuración.</span><span class="sxs-lookup"><span data-stu-id="d26a4-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="d26a4-135">Verá la notificación **Implementación iniciada...**</span><span class="sxs-lookup"><span data-stu-id="d26a4-135">You should see a **Deployment started...** notification.</span></span>

    ![Implementación iniciada: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="d26a4-137">Inicio y administración de la aplicación web de WordPress</span><span class="sxs-lookup"><span data-stu-id="d26a4-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="d26a4-138">Cuando Azure finalice la implementación de aplicación, verá otra notificación.</span><span class="sxs-lookup"><span data-stu-id="d26a4-138">When Azure completes app deployment you see another notification.</span></span>

![La implementación finalizó correctamente: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="d26a4-140">Haga clic en la notificación.</span><span class="sxs-lookup"><span data-stu-id="d26a4-140">Click the notification.</span></span> <span data-ttu-id="d26a4-141">Si se la ha perdido, siempre puede acceder a ella haciendo clic en la campana de notificación (![Notificación siguiente: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="d26a4-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="d26a4-142">Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="d26a4-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="d26a4-143">En la parte superior de la página de introducción, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="d26a4-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Examinar: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="d26a4-145">Ahora puede ver la página de **bienvenida** de WordPress.</span><span class="sxs-lookup"><span data-stu-id="d26a4-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="d26a4-146">Configure la instalación de WordPress y ya puede comenzar a jugar.</span><span class="sxs-lookup"><span data-stu-id="d26a4-146">Configure the WordPress installation and start playing with it!</span></span>

    ![Configuración de WordPress: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="d26a4-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d26a4-148">Next steps</span></span>
* <span data-ttu-id="d26a4-149">[Creación, configuración e implementación de una aplicación web de Laravel en Azure](app-service-web-php-get-started.md): conozca las habilidades básicas que necesita para ejecutar una aplicación web de PHP en Azure, como por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d26a4-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="d26a4-150">Crear y configurar aplicaciones en Azure desde PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="d26a4-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="d26a4-151">Establecer la versión de PHP.</span><span class="sxs-lookup"><span data-stu-id="d26a4-151">Set PHP version.</span></span>
    * <span data-ttu-id="d26a4-152">Usar un archivo de inicio que no está en el directorio raíz de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26a4-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="d26a4-153">Habilitar la automatización de Composer.</span><span class="sxs-lookup"><span data-stu-id="d26a4-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="d26a4-154">Acceder a variables de entorno específico.</span><span class="sxs-lookup"><span data-stu-id="d26a4-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="d26a4-155">Solucionar errores comunes.</span><span class="sxs-lookup"><span data-stu-id="d26a4-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="d26a4-156">[Implementación del código en Azure App Service](web-sites-deploy.md): aprenda a implementar desde FTP o desde repositorios de control del código fuente.</span><span class="sxs-lookup"><span data-stu-id="d26a4-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="d26a4-157">[Incorporación de funcionalidad a su primera aplicación web](app-service-web-get-started-2.md): lleve su aplicación de Azure al siguiente nivel.</span><span class="sxs-lookup"><span data-stu-id="d26a4-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="d26a4-158">Autentique los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d26a4-158">Authenticate your users.</span></span> <span data-ttu-id="d26a4-159">Escálela según la demanda.</span><span class="sxs-lookup"><span data-stu-id="d26a4-159">Scale it based on demand.</span></span> <span data-ttu-id="d26a4-160">Configure algunas alertas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d26a4-160">Set up some performance alerts.</span></span> <span data-ttu-id="d26a4-161">Todo ello con unos cuantos clics.</span><span class="sxs-lookup"><span data-stu-id="d26a4-161">All with a few clicks.</span></span>
