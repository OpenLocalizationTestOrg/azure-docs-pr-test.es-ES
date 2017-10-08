---
title: "una aplicación web de Umbraco Hola portal de Azure en cinco minutos aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de lo fácil que es toorun las aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación de ASP.NET de ejemplo. Vea los resultados inmediatamente."
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
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="fd599-104">Implementar una aplicación web de Umbraco Hola portal de Azure en cinco minutos</span><span class="sxs-lookup"><span data-stu-id="fd599-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="fd599-105">Este tutorial le ayudará a implementar n [Umbraco](https://our.umbraco.org/) aplicación web demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) en minutos.</span><span class="sxs-lookup"><span data-stu-id="fd599-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplicación de Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="fd599-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd599-107">Prerequisites</span></span>
<span data-ttu-id="fd599-108">Necesita una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fd599-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="fd599-109">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fd599-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="fd599-110">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd599-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="fd599-111">Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.</span><span class="sxs-lookup"><span data-stu-id="fd599-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="fd599-112">Implementar la aplicación ASP.NET de hello</span><span class="sxs-lookup"><span data-stu-id="fd599-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="fd599-113">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd599-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fd599-114">Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="fd599-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="fd599-115">Este vínculo es un método abreviado tooimmediately configurar una nueva aplicación de Umbraco Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd599-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="fd599-116">En **Nombre de la aplicación**, escriba un nombre de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="fd599-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="fd599-117">Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `azurewebsites.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="fd599-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="fd599-118">En **grupo de recursos**, haga clic en **crear nuevo** toocreate un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), a continuación, asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="fd599-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="fd599-119">Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="fd599-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="fd599-120">Configurar hello [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="fd599-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="fd599-121">En **plan de servicio de aplicaciones**, nombre de tipo hello deseado.</span><span class="sxs-lookup"><span data-stu-id="fd599-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="fd599-122">En **ubicación**, elegir una ubicación toohost el plan.</span><span class="sxs-lookup"><span data-stu-id="fd599-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="fd599-123">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="fd599-124">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-124">Click **OK**.</span></span>

    <span data-ttu-id="fd599-125">La configuración de Umbraco CMS debe parecerse Hola siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="fd599-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuración en curso: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="fd599-127">Haga clic en **SQL Database** > **Crear una base de datos nueva**.</span><span class="sxs-lookup"><span data-stu-id="fd599-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="fd599-128">Configurar base de datos SQL de hello tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="fd599-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="fd599-129">En **Nombre**, escriba un nombre, como **myBD**.</span><span class="sxs-lookup"><span data-stu-id="fd599-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="fd599-130">Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="fd599-131">Haga clic en **Servidor de destino** > **Crear un servidor nuevo**.</span><span class="sxs-lookup"><span data-stu-id="fd599-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="fd599-132">Configurar el servidor de base de datos de hello tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="fd599-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="fd599-133">En **Nombre del servidor**, escriba un nombre para el servidor.</span><span class="sxs-lookup"><span data-stu-id="fd599-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="fd599-134">Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `.database.windows.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="fd599-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="fd599-135">En **inicio de sesión de administrador de servidor**, Hola tipo deseado de nombre de usuario de administrador.</span><span class="sxs-lookup"><span data-stu-id="fd599-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="fd599-136">En **contraseña** y **Confirmar contraseña**, contraseña de tipo hello deseada.</span><span class="sxs-lookup"><span data-stu-id="fd599-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="fd599-137">En ubicación, seleccione Hola la misma ubicación que utiliza para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd599-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="fd599-138">Asegúrese de que **server tooaccess de permitir que los servicios de azure** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="fd599-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="fd599-139">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="fd599-140">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-140">Click **Select**.</span></span>

13. <span data-ttu-id="fd599-141">Haga clic en **configuración de aplicación Web**, especifique el nombre de usuario de base de datos de Hola y la contraseña y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="fd599-142">La configuración de Umbraco CMS debe parecerse Hola siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="fd599-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuración finalizada: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="fd599-144">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd599-144">Click **Create**.</span></span>
    
    <span data-ttu-id="fd599-145">Ahora, Azure crea la aplicación de Umbraco según su configuración.</span><span class="sxs-lookup"><span data-stu-id="fd599-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="fd599-146">Verá la notificación **Implementación iniciada...**</span><span class="sxs-lookup"><span data-stu-id="fd599-146">You should see a **Deployment started...** notification.</span></span>

    ![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="fd599-148">Inicio y administración de la aplicación web de Umbraco</span><span class="sxs-lookup"><span data-stu-id="fd599-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="fd599-149">Cuando Azure finalice la implementación de aplicación, verá otra notificación.</span><span class="sxs-lookup"><span data-stu-id="fd599-149">When Azure completes app deployment you see another notification.</span></span>

![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="fd599-151">Haga clic en la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd599-151">Click hello notification.</span></span> <span data-ttu-id="fd599-152">Si se lo haya perdido, siempre puede acceso haciendo clic en campana de notificación de hello (![siguientes notificación - Umbraco primero en el servicio de aplicación de Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="fd599-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="fd599-153">Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="fd599-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="fd599-154">En la parte superior de Hola de página de información general de hello, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="fd599-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Examinar: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="fd599-156">Ahora puede ver Hola Umbraco **bienvenida** página.</span><span class="sxs-lookup"><span data-stu-id="fd599-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="fd599-157">Configurar una instalación de Umbraco de Hola y comenzar a jugar con él.</span><span class="sxs-lookup"><span data-stu-id="fd599-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Configuración de Umbraco: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="fd599-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd599-159">Next steps</span></span>
* <span data-ttu-id="fd599-160">[Implementar una aplicación de web ASP.NET tooAzure servicio de aplicación mediante Visual Studio](app-service-web-get-started-dotnet.md) -Descubra cómo toocreate una nueva aplicación web de Azure desde Visual Studio, con cualquiera de hello incluye plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd599-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="fd599-161">[Implementar el servicio de aplicaciones de código tooAzure](web-sites-deploy.md)-Obtenga información acerca de cómo toodeploy de FTP o de origen controlar repositorios.</span><span class="sxs-lookup"><span data-stu-id="fd599-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="fd599-162">[Agregar funcionalidad tooyour primera web aplicación](app-service-web-get-started-2.md) -lleve su aplicación de Azure toohello siguiente nivel.</span><span class="sxs-lookup"><span data-stu-id="fd599-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="fd599-163">Autentique los usuarios.</span><span class="sxs-lookup"><span data-stu-id="fd599-163">Authenticate your users.</span></span> <span data-ttu-id="fd599-164">Escálela según la demanda.</span><span class="sxs-lookup"><span data-stu-id="fd599-164">Scale it based on demand.</span></span> <span data-ttu-id="fd599-165">Configure algunas alertas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="fd599-165">Set up some performance alerts.</span></span> <span data-ttu-id="fd599-166">Todo ello con unos cuantos clics.</span><span class="sxs-lookup"><span data-stu-id="fd599-166">All with a few clicks.</span></span>
