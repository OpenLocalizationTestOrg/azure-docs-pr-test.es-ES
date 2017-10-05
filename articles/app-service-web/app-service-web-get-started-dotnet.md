---
title: "Creación de una aplicación web ASP.NET en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo ejecutar aplicaciones web en Azure App Service mediante la implementación de la aplicación web ASP.NET predeterminada."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="f2039-103">Creación de una aplicación web ASP.NET en Azure</span><span class="sxs-lookup"><span data-stu-id="f2039-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="f2039-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="f2039-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="f2039-105">Esta guía de inicio rápido muestra cómo implementar su primera aplicación web ASP.NET en Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f2039-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="f2039-106">Cuando haya terminado, tendrá un grupo de recursos que consta de un plan de App Service y una aplicación web de Azure con una aplicación web implementada.</span><span class="sxs-lookup"><span data-stu-id="f2039-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="f2039-107">Vea el vídeo para ver este inicio rápido en acción y, a continuación, siga los pasos para publicar su primera aplicación de .NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="f2039-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f2039-108">Prerequisites</span></span>

<span data-ttu-id="f2039-109">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="f2039-109">To complete this tutorial:</span></span>

* <span data-ttu-id="f2039-110">Instalar [Visual Studio 2017](https://www.visualstudio.com/downloads/) con las cargas de trabajo siguientes:</span><span class="sxs-lookup"><span data-stu-id="f2039-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="f2039-111">**ASP.NET y desarrollo web**</span><span class="sxs-lookup"><span data-stu-id="f2039-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="f2039-112">**Desarrollo de Azure**</span><span class="sxs-lookup"><span data-stu-id="f2039-112">**Azure development**</span></span>

    ![ASP.NET y desarrollo web y desarrollo de Azure (en web y en la nube)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="f2039-114">Creación de una aplicación web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f2039-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="f2039-115">Cree un proyecto nuevo en Visual Studio seleccionando **Archivo > Nuevo > Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="f2039-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="f2039-116">En el cuadro de diálogo **Nuevo proyecto**, seleccione **Visual C# > Web > Aplicación web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f2039-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="f2039-117">Asigne a la aplicación el nombre _myFirstAzureWebApp_ y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Cuadro de diálogo Nuevo proyecto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="f2039-119">Puede implementar cualquier tipo de aplicación web de ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="f2039-120">Para esta guía de inicio rápido, seleccione la plantilla **MVC** y asegúrese de que la autenticación se establece en **Sin autenticación**.</span><span class="sxs-lookup"><span data-stu-id="f2039-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="f2039-121">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-121">Select **OK**.</span></span>

![Cuadro de diálogo New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="f2039-123">En el menú, seleccione **Depurar > Iniciar sin depurar** para ejecutar la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="f2039-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Ejecución de la aplicación de forma local](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="f2039-125">Publicación en Azure</span><span class="sxs-lookup"><span data-stu-id="f2039-125">Publish to Azure</span></span>

<span data-ttu-id="f2039-126">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **myFirstAzureWebApp** y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publicar desde el Explorador de soluciones](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="f2039-128">Asegúrese de que **Microsoft Azure App Service** está seleccionado y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publicar desde la página de información general del proyecto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="f2039-130">Con ello se abrirá el cuadro de diálogo **Crear App Service** que le ayudará a crear todos los recursos de Azure necesarios para ejecutar la aplicación web de ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="f2039-131">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="f2039-131">Sign in to Azure</span></span>

<span data-ttu-id="f2039-132">En el cuadro de diálogo **Crear App Service**, haga clic en **Agregar una cuenta** e inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="f2039-133">Si ya ha iniciado sesión, seleccione la cuenta que contiene la suscripción deseada en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="f2039-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="f2039-134">Si ya ha iniciado sesión, no seleccione **Crear** todavía.</span><span class="sxs-lookup"><span data-stu-id="f2039-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Inicio de sesión en Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="f2039-136">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f2039-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="f2039-137">Junto a **Grupo de recursos**, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="f2039-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="f2039-138">Asigne el nombre **myResourceGroup** al grupo de recursos y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="f2039-139">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="f2039-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="f2039-140">Junto a **Plan de App Service**, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="f2039-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="f2039-141">En el cuadro de diálogo **Configurar plan de App Service**, use la configuración de la tabla que sigue a la captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="f2039-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Creación de un plan de App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="f2039-143">Configuración</span><span class="sxs-lookup"><span data-stu-id="f2039-143">Setting</span></span> | <span data-ttu-id="f2039-144">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="f2039-144">Suggested Value</span></span> | <span data-ttu-id="f2039-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2039-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="f2039-146">Plan de App Service</span><span class="sxs-lookup"><span data-stu-id="f2039-146">App Service Plan</span></span>| <span data-ttu-id="f2039-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f2039-147">myAppServicePlan</span></span> | <span data-ttu-id="f2039-148">Nombre del plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="f2039-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="f2039-149">Ubicación</span><span class="sxs-lookup"><span data-stu-id="f2039-149">Location</span></span> | <span data-ttu-id="f2039-150">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="f2039-150">West Europe</span></span> | <span data-ttu-id="f2039-151">El centro de datos donde se hospeda la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2039-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="f2039-152">Tamaño</span><span class="sxs-lookup"><span data-stu-id="f2039-152">Size</span></span> | <span data-ttu-id="f2039-153">Gratuito</span><span class="sxs-lookup"><span data-stu-id="f2039-153">Free</span></span> | <span data-ttu-id="f2039-154">[Plan de tarifa](https://azure.microsoft.com/pricing/details/app-service/) determina las características de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="f2039-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="f2039-155">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="f2039-156">Creación y publicación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="f2039-156">Create and publish the web app</span></span>

<span data-ttu-id="f2039-157">En **Web App Name** (Nombre de aplicación web), escriba un nombre único de aplicación (los caracteres válidos son `a-z`, `0-9` y `-`) o acepte el nombre único generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f2039-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="f2039-158">La dirección URL de la aplicación web es `http://<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2039-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="f2039-159">Seleccione **Crear** para comenzar a crear los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-159">Select **Create** to start creating the Azure resources.</span></span>

![Configurar el nombre de la aplicación web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="f2039-161">Una vez completado el asistente, publica la aplicación web ASP.NET en Azure y, a continuación, inicia la aplicación en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f2039-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Aplicación web de ASP.NET publicada en Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="f2039-163">El nombre de aplicación web especificado en el [paso de creación y publicación](#create-and-publish-the-web-app) se usa como el prefijo de dirección URL en el formato `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f2039-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="f2039-164">Su aplicación web ASP.NET se está ejecutando en vivo en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f2039-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="f2039-165">Actualización de la aplicación y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="f2039-165">Update the app and redeploy</span></span>

<span data-ttu-id="f2039-166">Desde el **Explorador de soluciones**, abra _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="f2039-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="f2039-167">Busque la etiqueta HTML `<div class="jumbotron">` en la parte superior y reemplace el elemento entero por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="f2039-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="f2039-168">Para volver a implementar en Azure, haga clic con el botón derecho en el proyecto **myFirstAzureWebApp**, en el **Explorador de soluciones** y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="f2039-169">En la página de publicación, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f2039-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="f2039-170">Cuando se completa la publicación, Visual Studio inicia un explorador en la dirección URL de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2039-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Aplicación web actualizada de ASP.NET en Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="f2039-172">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="f2039-172">Manage the Azure web app</span></span>

<span data-ttu-id="f2039-173">Vaya a <a href="https://portal.azure.com" target="_blank">Azure Portal</a> para administrar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2039-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="f2039-174">En el menú izquierdo, seleccione **App Services** y, después, el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2039-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Navegación desde el portal a la aplicación web de Azure](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="f2039-176">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2039-176">You see your web app's Overview page.</span></span> <span data-ttu-id="f2039-177">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="f2039-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="f2039-179">El menú izquierdo proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f2039-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="f2039-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2039-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2039-181">ASP.NET con SQL Database</span><span class="sxs-lookup"><span data-stu-id="f2039-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
