---
title: "aaaCreate su primera aplicación web de Java en Azure"
description: "Obtenga información acerca de cómo toorun aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación básica de Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="d6acf-103">Creación de su primera aplicación web de Java en Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="d6acf-104">Hola [aplicaciones Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) característica de [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) proporciona un servicio de hospedaje web muy escalable, aplicación de revisiones automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d6acf-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="d6acf-105">Este tutorial rápido muestra cómo toodeploy un Java web tooApp servicio de aplicación mediante el uso de hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="d6acf-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="d6acf-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6acf-108">Prerequisites</span></span>

<span data-ttu-id="d6acf-109">toocomplete este tutorial rápido, instalar:</span><span class="sxs-lookup"><span data-stu-id="d6acf-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="d6acf-110">Hola libre [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d6acf-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="d6acf-111">Este guía de inicio rápido utiliza Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="d6acf-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="d6acf-112">Hola [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="d6acf-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="d6acf-113">Creación de un proyecto web dinámico en Eclipse</span><span class="sxs-lookup"><span data-stu-id="d6acf-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="d6acf-114">En Eclipse, seleccione **File (Archivo)** > **New (Nuevo)** > **Dynamic Web Project (Proyecto web dinámico)**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="d6acf-115">Hola **nueva Dynamic Web Project** cuadro de diálogo, proyecto de hello name **MyFirstJavaOnAzureWebApp**y seleccione **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Cuadro de diálogo New Dynamic Web Project (Nuevo proyecto web dinámico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="d6acf-117">Agregar una página JSP</span><span class="sxs-lookup"><span data-stu-id="d6acf-117">Add a JSP page</span></span>

<span data-ttu-id="d6acf-118">Si no se muestra el Explorador de proyectos, restáurelo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-118">If Project Explorer is not displayed, restore it.</span></span>

![Área de trabajo de Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="d6acf-120">En el Explorador de proyectos, expanda hello **MyFirstJavaOnAzureWebApp** proyecto.</span><span class="sxs-lookup"><span data-stu-id="d6acf-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="d6acf-121">Haga clic con el botón derecho en **WebContent** (Contenido web) y, a continuación, seleccione **New** (Nuevo) > **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="d6acf-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menú de un nuevo archivo JSP en el Explorador de proyectos](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="d6acf-123">Hola **New JSP File** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="d6acf-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="d6acf-124">Archivo de nombre hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="d6acf-125">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-125">Select **Finish**.</span></span>

  ![Cuadro de diálogo Nuevo archivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="d6acf-127">En el archivo index.jsp de hello, reemplace hello `<body></body>` elemento con hello sigue marcado:</span><span class="sxs-lookup"><span data-stu-id="d6acf-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="d6acf-128">Guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="d6acf-129">Publicar hello web app tooAzure</span><span class="sxs-lookup"><span data-stu-id="d6acf-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="d6acf-130">En el Explorador de proyectos, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como aplicación Web de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menú contextual Publish as Azure Web App (Publicar como aplicación web de Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="d6acf-132">Hola **inicio de sesión en Azure** cuadro de diálogo, mantener hello **Interactive** opción y, a continuación, seleccione **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="d6acf-133">Siga instrucciones de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="d6acf-134">Cuadro de diálogo Implementar una aplicación web</span><span class="sxs-lookup"><span data-stu-id="d6acf-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="d6acf-135">Una vez que haya iniciado sesión tooyour cuenta de Azure, Hola **implementar aplicación de Web** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="d6acf-136">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-136">Select **Create**.</span></span>

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="d6acf-138">Cuadro de diálogo Crear servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d6acf-138">Create App Service dialog box</span></span>

<span data-ttu-id="d6acf-139">Hola **crear servicio en la aplicación** aparece el cuadro de diálogo con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="d6acf-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="d6acf-140">Hola número **170602185241** se muestra en hello después de imagen es diferente en el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="d6acf-142">Hola **crear servicio en la aplicación** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="d6acf-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="d6acf-143">Mantenga el nombre de hello generado para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="d6acf-144">Este nombre debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-144">This name must be unique across Azure.</span></span> <span data-ttu-id="d6acf-145">Hola nombre forma parte de la dirección URL de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="d6acf-146">Por ejemplo: si es el nombre de la aplicación hello **MyJavaWebApp**, Hola dirección URL es *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="d6acf-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="d6acf-147">Mantenga el contenedor de web predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-147">Keep hello default web container.</span></span>
* <span data-ttu-id="d6acf-148">Seleccione una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="d6acf-149">En hello **plan de servicio de aplicaciones** ficha:</span><span class="sxs-lookup"><span data-stu-id="d6acf-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="d6acf-150">**Cree una nueva**: mantener predeterminado de hello, que es el nombre de Hola de hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d6acf-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="d6acf-151">**Ubicación**: seleccione **Europa occidental** o una ubicación cerca de usted.</span><span class="sxs-lookup"><span data-stu-id="d6acf-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="d6acf-152">**Nivel de precios**: seleccione Hola opción disponible.</span><span class="sxs-lookup"><span data-stu-id="d6acf-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="d6acf-153">Para ver las características, consulte [Precios de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="d6acf-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="d6acf-155">Pestaña Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d6acf-155">Resource group tab</span></span>

<span data-ttu-id="d6acf-156">Seleccione hello **grupo de recursos** ficha. Mantenga el valor de generada de manera predeterminada de Hola Hola para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d6acf-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Pestaña Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="d6acf-158">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="d6acf-159">Hola Kit de herramientas de Azure crea la aplicación web de hello y muestra un cuadro de diálogo de progreso.</span><span class="sxs-lookup"><span data-stu-id="d6acf-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Cuadro de diálogo de progreso Crear App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="d6acf-161">Cuadro de diálogo Implementar una aplicación web</span><span class="sxs-lookup"><span data-stu-id="d6acf-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="d6acf-162">Hola **implementar aplicación de Web** cuadro de diálogo, seleccione **implementar tooroot**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="d6acf-163">Si tiene un servicio de aplicaciones en *wingtiptoys.azurewebsites.net* y no se implementan toohello raíz, aplicación web de hello denominado **MyFirstJavaOnAzureWebApp** se implementa demasiado *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="d6acf-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="d6acf-165">cuadro de diálogo Hola Hola se muestra en Azure, JDK y las selecciones de contenedor de web.</span><span class="sxs-lookup"><span data-stu-id="d6acf-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="d6acf-166">Seleccione **implementar** toopublish hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="d6acf-167">Cuando finalice la publicación de hello, seleccione hello **publicada** vínculo Hola **Azure Activity Log** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Cuadro de diálogo Registro de actividad de Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="d6acf-169">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d6acf-169">Congratulations!</span></span> <span data-ttu-id="d6acf-170">Ha implementado correctamente su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d6acf-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="d6acf-173">Actualizar la aplicación web de Hola</span><span class="sxs-lookup"><span data-stu-id="d6acf-173">Update hello web app</span></span>

<span data-ttu-id="d6acf-174">Cambiar Hola ejemplo código JSP tooa mensaje diferente.</span><span class="sxs-lookup"><span data-stu-id="d6acf-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="d6acf-175">Guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-175">Save hello changes.</span></span>

<span data-ttu-id="d6acf-176">En el Explorador de proyectos, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como aplicación Web de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="d6acf-177">Hola **implementar aplicación de Web** aparece el cuadro de diálogo y muestra Hola servicio de aplicaciones que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d6acf-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6acf-178">Seleccione **implementar tooroot** cada vez que publique.</span><span class="sxs-lookup"><span data-stu-id="d6acf-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="d6acf-179">Seleccione la aplicación web de hello y seleccione **implementar**, que publica los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="d6acf-180">Cuando Hola **publicación** vínculo aparece, seleccione aplicación web de toobrowse toohello y ver los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="d6acf-181">Administrar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="d6acf-181">Manage hello web app</span></span>

<span data-ttu-id="d6acf-182">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toosee hello web aplicación que ha creado.</span><span class="sxs-lookup"><span data-stu-id="d6acf-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="d6acf-183">En el menú izquierdo de hello, seleccione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-183">From hello left menu, select **Resource Groups**.</span></span>

![Grupos de tooresource de exploración del portal](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="d6acf-185">Seleccione el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6acf-185">Select hello resource group.</span></span> <span data-ttu-id="d6acf-186">página de Hello muestra los recursos de Hola que creó en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="d6acf-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="d6acf-188">Seleccione hello web app (**170602193915 webapp** Hola anterior imagen).</span><span class="sxs-lookup"><span data-stu-id="d6acf-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="d6acf-189">Hola **Introducción** aparecerá la página.</span><span class="sxs-lookup"><span data-stu-id="d6acf-189">hello **Overview** page appears.</span></span> <span data-ttu-id="d6acf-190">Esta página proporciona una visión de cómo está haciendo la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d6acf-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="d6acf-191">En ella, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="d6acf-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="d6acf-192">Hola a la izquierda Hola de página Hola pestañas: Hola diferentes configuraciones que se pueden abrir.</span><span class="sxs-lookup"><span data-stu-id="d6acf-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Página de App Service en Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="d6acf-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6acf-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6acf-195">Asignación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="d6acf-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
