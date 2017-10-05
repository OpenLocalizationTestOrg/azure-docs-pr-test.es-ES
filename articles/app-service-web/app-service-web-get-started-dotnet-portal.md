---
title: "Implementación de una aplicación web de Umbraco en Azure Portal en cinco minutos | Microsoft Docs"
description: "Aprenda lo fácil que es ejecutar aplicaciones web en App Service mediante la implementación de una aplicación ASP.NET de ejemplo. Vea los resultados inmediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="56166-104">Implementación de una aplicación web de Umbraco en Azure Portal en cinco minutos</span><span class="sxs-lookup"><span data-stu-id="56166-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="56166-105">Este tutorial le ayuda a implementar una aplicación web de [Umbraco](https://our.umbraco.org/) en [Azure App Service](../app-service/app-service-value-prop-what-is.md) en cuestión de minutos.</span><span class="sxs-lookup"><span data-stu-id="56166-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplicación de Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="56166-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="56166-107">Prerequisites</span></span>
<span data-ttu-id="56166-108">Necesita una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="56166-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="56166-109">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="56166-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="56166-110">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="56166-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="56166-111">Cree una aplicación de inicio y juegue con ella durante una hora como máximo; no se requiere ninguna tarjeta de crédito ni ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="56166-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="56166-112">Implementación de la aplicación ASP.NET</span><span class="sxs-lookup"><span data-stu-id="56166-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="56166-113">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56166-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="56166-114">Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="56166-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="56166-115">Este vínculo es un acceso directo para configurar inmediatamente una nueva aplicación de Umbraco en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="56166-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="56166-116">En **Nombre de la aplicación**, escriba un nombre de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56166-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="56166-117">Verá una marca de verificación verde en el cuadro si el nombre es único en el dominio `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="56166-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="56166-118">En **Grupo de recursos**, haga clic en **Create new** (Crear nuevo) para crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) y, luego, asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="56166-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="56166-119">Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="56166-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="56166-120">Configure el [plan de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="56166-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="56166-121">En **Plan de App Service**, escriba el nombre deseado.</span><span class="sxs-lookup"><span data-stu-id="56166-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="56166-122">En **Ubicación**, elija una ubicación para hospedar el plan.</span><span class="sxs-lookup"><span data-stu-id="56166-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="56166-123">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="56166-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="56166-124">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56166-124">Click **OK**.</span></span>

    <span data-ttu-id="56166-125">La configuración de CMS de Umbraco debe parecerse a la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="56166-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuración en curso: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="56166-127">Haga clic en **SQL Database** > **Crear una base de datos nueva**.</span><span class="sxs-lookup"><span data-stu-id="56166-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="56166-128">Configure la base de datos SQL tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="56166-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="56166-129">En **Nombre**, escriba un nombre, como **myBD**.</span><span class="sxs-lookup"><span data-stu-id="56166-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="56166-130">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="56166-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="56166-131">Haga clic en **Servidor de destino** > **Crear un servidor nuevo**.</span><span class="sxs-lookup"><span data-stu-id="56166-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="56166-132">Configure el servidor de base de datos tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="56166-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="56166-133">En **Nombre del servidor**, escriba un nombre para el servidor.</span><span class="sxs-lookup"><span data-stu-id="56166-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="56166-134">Verá una marca de verificación verde en el cuadro si el nombre es único en el dominio `.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="56166-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="56166-135">En **Inicio de sesión del administrador del servidor**, escriba el nombre de usuario de administrador deseado.</span><span class="sxs-lookup"><span data-stu-id="56166-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="56166-136">En **Contraseña** y **Confirmar contraseña**, escriba la contraseña deseada.</span><span class="sxs-lookup"><span data-stu-id="56166-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="56166-137">En Ubicación, seleccione la misma ubicación que usa para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56166-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="56166-138">Asegúrese de que la opción **Permitir que los servicios de Azure accedan al servidor** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="56166-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="56166-139">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="56166-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="56166-140">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="56166-140">Click **Select**.</span></span>

13. <span data-ttu-id="56166-141">Haga clic en **Configuración de aplicación web**, especifique el nombre de usuario y la contraseña de la base de datos y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56166-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="56166-142">La configuración de CMS de Umbraco debe parecerse a la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="56166-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuración finalizada: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="56166-144">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56166-144">Click **Create**.</span></span>
    
    <span data-ttu-id="56166-145">Ahora, Azure crea la aplicación de Umbraco según su configuración.</span><span class="sxs-lookup"><span data-stu-id="56166-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="56166-146">Verá la notificación **Implementación iniciada...**</span><span class="sxs-lookup"><span data-stu-id="56166-146">You should see a **Deployment started...** notification.</span></span>

    ![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="56166-148">Inicio y administración de la aplicación web de Umbraco</span><span class="sxs-lookup"><span data-stu-id="56166-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="56166-149">Cuando Azure finalice la implementación de aplicación, verá otra notificación.</span><span class="sxs-lookup"><span data-stu-id="56166-149">When Azure completes app deployment you see another notification.</span></span>

![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="56166-151">Haga clic en la notificación.</span><span class="sxs-lookup"><span data-stu-id="56166-151">Click the notification.</span></span> <span data-ttu-id="56166-152">Si se la ha perdido, siempre puede acceder a ella haciendo clic en la campana de notificación (![Notificación siguiente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="56166-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="56166-153">Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="56166-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="56166-154">En la parte superior de la página de introducción, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="56166-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Examinar: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="56166-156">Ahora puede ver la página de **bienvenida** de Umbraco.</span><span class="sxs-lookup"><span data-stu-id="56166-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="56166-157">Configure la instalación de Umbraco y ya puede comenzar a jugar.</span><span class="sxs-lookup"><span data-stu-id="56166-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Configuración de Umbraco: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="56166-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56166-159">Next steps</span></span>
* <span data-ttu-id="56166-160">[Implementación de una aplicación web creada con ASP.NET en Azure App Service mediante Visual Studio](app-service-web-get-started-dotnet.md): aprenda a crear una nueva aplicación web de Azure desde Visual Studio, con cualquiera de las plantillas de aplicación que se incluyen.</span><span class="sxs-lookup"><span data-stu-id="56166-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="56166-161">[Implementación del código en Azure App Service](web-sites-deploy.md): aprenda a implementar desde FTP o desde repositorios de control del código fuente.</span><span class="sxs-lookup"><span data-stu-id="56166-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="56166-162">[Incorporación de funcionalidad a su primera aplicación web](app-service-web-get-started-2.md): lleve su aplicación de Azure al siguiente nivel.</span><span class="sxs-lookup"><span data-stu-id="56166-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="56166-163">Autentique los usuarios.</span><span class="sxs-lookup"><span data-stu-id="56166-163">Authenticate your users.</span></span> <span data-ttu-id="56166-164">Escálela según la demanda.</span><span class="sxs-lookup"><span data-stu-id="56166-164">Scale it based on demand.</span></span> <span data-ttu-id="56166-165">Configure algunas alertas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="56166-165">Set up some performance alerts.</span></span> <span data-ttu-id="56166-166">Todo ello con unos cuantos clics.</span><span class="sxs-lookup"><span data-stu-id="56166-166">All with a few clicks.</span></span>
