---
title: "Creación de su primera aplicación web de Java en Azure"
description: "Aprenda a ejecutar aplicaciones web en App Service mediante la implementación de una aplicación básica de Java."
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="0f1f0-103">Creación de su primera aplicación web de Java en Azure</span><span class="sxs-lookup"><span data-stu-id="0f1f0-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="0f1f0-104">La característica [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) de [Azure App Service](../app-service/app-service-value-prop-what-is.md) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="0f1f0-105">Esta guía de inicio rápido muestra cómo implementar una aplicación web de Java en App Service mediante [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="0f1f0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0f1f0-108">Prerequisites</span></span>

<span data-ttu-id="0f1f0-109">Para completar esta guía de inicio rápido necesita instalar:</span><span class="sxs-lookup"><span data-stu-id="0f1f0-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="0f1f0-110">El entorno gratuito [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="0f1f0-111">Este guía de inicio rápido utiliza Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="0f1f0-112">El [kit de herramientas de Azure para Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="0f1f0-113">Creación de un proyecto web dinámico en Eclipse</span><span class="sxs-lookup"><span data-stu-id="0f1f0-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="0f1f0-114">En Eclipse, seleccione **File (Archivo)** > **New (Nuevo)** > **Dynamic Web Project (Proyecto web dinámico)**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="0f1f0-115">En el cuadro de diálogo **New Dynamic Web Project** (Nuevo proyecto web dinámico), asigne al proyecto el nombre **MyFirstJavaOnAzureWebApp** y seleccione **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Cuadro de diálogo New Dynamic Web Project (Nuevo proyecto web dinámico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="0f1f0-117">Agregar una página JSP</span><span class="sxs-lookup"><span data-stu-id="0f1f0-117">Add a JSP page</span></span>

<span data-ttu-id="0f1f0-118">Si no se muestra el Explorador de proyectos, restáurelo.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-118">If Project Explorer is not displayed, restore it.</span></span>

![Área de trabajo de Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="0f1f0-120">En el Explorador de proyectos, expanda el proyecto **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="0f1f0-121">Haga clic con el botón derecho en **WebContent** (Contenido web) y, a continuación, seleccione **New** (Nuevo) > **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menú de un nuevo archivo JSP en el Explorador de proyectos](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="0f1f0-123">En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP):</span><span class="sxs-lookup"><span data-stu-id="0f1f0-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="0f1f0-124">Asigne al archivo el nombre **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="0f1f0-125">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-125">Select **Finish**.</span></span>

  ![Cuadro de diálogo Nuevo archivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="0f1f0-127">En el archivo index.jsp, reemplace el elemento `<body></body>` por el siguiente marcado:</span><span class="sxs-lookup"><span data-stu-id="0f1f0-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="0f1f0-128">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="0f1f0-129">Publicación de la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="0f1f0-129">Publish the web app to Azure</span></span>

<span data-ttu-id="0f1f0-130">En el Explorador de proyectos, haga clic con el botón derecho en el proyecto y, a continuación, seleccione **Azure** > **Publish as Azure Web App** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menú contextual Publish as Azure Web App (Publicar como aplicación web de Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="0f1f0-132">En el cuadro de diálogo **Inicio de sesión en Azure**, mantenga la opción **Interactivo** y, a continuación, seleccione **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="0f1f0-133">Siga las instrucciones de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="0f1f0-134">Cuadro de diálogo Implementar una aplicación web</span><span class="sxs-lookup"><span data-stu-id="0f1f0-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="0f1f0-135">Una vez que haya iniciado sesión en su cuenta de Azure, aparecerá el cuadro de diálogo **Implementar una aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="0f1f0-136">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-136">Select **Create**.</span></span>

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="0f1f0-138">Cuadro de diálogo Crear servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0f1f0-138">Create App Service dialog box</span></span>

<span data-ttu-id="0f1f0-139">Aparece el cuadro de diálogo **Crear App Service** con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="0f1f0-140">El número **170602185241** que se muestra en la siguiente imagen será diferente en su cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="0f1f0-142">En el cuadro de diálogo **Crear App Service**:</span><span class="sxs-lookup"><span data-stu-id="0f1f0-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="0f1f0-143">Mantenga el nombre generado para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="0f1f0-144">Este nombre debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-144">This name must be unique across Azure.</span></span> <span data-ttu-id="0f1f0-145">El nombre forma parte de la dirección URL de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="0f1f0-146">Por ejemplo: si el nombre de la aplicación web es **MyJavaWebApp**, la dirección URL será *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="0f1f0-147">Mantenga el contenedor de web predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-147">Keep the default web container.</span></span>
* <span data-ttu-id="0f1f0-148">Seleccione una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="0f1f0-149">En la pestaña **Plan de App Service**:</span><span class="sxs-lookup"><span data-stu-id="0f1f0-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="0f1f0-150">**Crear nuevo**: mantenga el valor predeterminado, que es el nombre del plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="0f1f0-151">**Ubicación**: seleccione **Europa occidental** o una ubicación cerca de usted.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="0f1f0-152">**Plan de tarifa**: seleccione la opción gratuita.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="0f1f0-153">Para ver las características, consulte [Precios de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="0f1f0-155">Pestaña Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0f1f0-155">Resource group tab</span></span>

<span data-ttu-id="0f1f0-156">Seleccione la pestaña **Grupo de recursos**. Mantenga el valor generado de forma predeterminada para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Pestaña Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="0f1f0-158">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="0f1f0-159">El kit de herramientas de Azure crea la aplicación web y muestra un cuadro de diálogo de progreso.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Cuadro de diálogo de progreso Crear App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="0f1f0-161">Cuadro de diálogo Implementar una aplicación web</span><span class="sxs-lookup"><span data-stu-id="0f1f0-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="0f1f0-162">En el cuadro de diálogo **Implementar aplicación web**, seleccione **Implementar en el nodo raíz**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="0f1f0-163">Si tiene un servicio de aplicaciones en *wingtiptoys.azurewebsites.net* y no lo implementa en la raíz, la aplicación web denominada **MyFirstJavaOnAzureWebApp** se implementará en *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="0f1f0-165">El cuadro de diálogo muestra las selecciones de Azure, JDK y contenedor web.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="0f1f0-166">Seleccione **Implementar** para publicar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="0f1f0-167">Cuando finalice la publicación, seleccione el enlace **Publicado** en el cuadro de diálogo **Registro de actividad de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Cuadro de diálogo Registro de actividad de Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="0f1f0-169">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="0f1f0-169">Congratulations!</span></span> <span data-ttu-id="0f1f0-170">Ha implementado correctamente la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-170">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="0f1f0-173">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="0f1f0-173">Update the web app</span></span>

<span data-ttu-id="0f1f0-174">Cambie el código de ejemplo JSP a un mensaje diferente.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="0f1f0-175">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-175">Save the changes.</span></span>

<span data-ttu-id="0f1f0-176">En el Explorador de proyectos, haga clic con el botón derecho en el proyecto y, a continuación, seleccione **Azure** > **Publish as Azure Web App** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="0f1f0-177">Aparece el cuadro de diálogo **Implementar aplicación web** y muestra el App Service que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f1f0-178">Seleccione **Implementar en el nodo raíz** cada vez que publique.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="0f1f0-179">Seleccione la aplicación web y seleccione **Implementar**, que publica los cambios.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="0f1f0-180">Cuando aparezca el enlace **Publicando**, selecciónelo para ir a la aplicación web y ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="0f1f0-181">Administrar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="0f1f0-181">Manage the web app</span></span>

<span data-ttu-id="0f1f0-182">Vaya a <a href="https://portal.azure.com" target="_blank">Azure Portal</a> para ver la aplicación web que ha creado.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="0f1f0-183">Seleccione **Grupos de recursos** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-183">From the left menu, select **Resource Groups**.</span></span>

![Exploración de los grupos de recursos en el portal](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="0f1f0-185">Seleccione el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-185">Select the resource group.</span></span> <span data-ttu-id="0f1f0-186">La página muestra los recursos que ha creado en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-186">The page shows the resources that you created in this quickstart.</span></span>

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="0f1f0-188">Seleccione la aplicación web (**webapp-170602193915** en la imagen anterior).</span><span class="sxs-lookup"><span data-stu-id="0f1f0-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="0f1f0-189">Aparece la página **Información general**.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-189">The **Overview** page appears.</span></span> <span data-ttu-id="0f1f0-190">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="0f1f0-191">En ella, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="0f1f0-192">Las pestañas del lado izquierdo de la página muestran las diferentes configuraciones que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="0f1f0-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Página de App Service en Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="0f1f0-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f1f0-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f1f0-195">Asignación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="0f1f0-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
