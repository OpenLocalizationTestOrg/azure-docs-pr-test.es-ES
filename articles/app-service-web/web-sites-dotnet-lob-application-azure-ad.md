---
title: "Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory | Microsoft Docs"
description: "Aprenda a crear una aplicación de línea de negocio de ASP.NET MVC en Servicio de aplicaciones de Azure que se autentica con Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="a5a5a-103">Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a5a-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="a5a5a-104">En este artículo se muestra cómo crear una aplicación de línea de negocio de .NET en [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) con la característica de [autenticación/autorización](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="a5a5a-105">También se enseña a usar la [API Graph de Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) para consultar los datos de directorio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="a5a5a-106">El inquilino de Azure Active Directory que use puede ser un directorio exclusivo de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="a5a5a-107">O bien, se puede [sincronizar con su entorno de Active Directory local](../active-directory/active-directory-aadconnect.md) para crear una experiencia de inicio de sesión única para los trabajadores locales y remotos.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="a5a5a-108">En este artículo se usa el directorio predeterminado para la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="a5a5a-109">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="a5a5a-109">What you will build</span></span>
<span data-ttu-id="a5a5a-110">Creará una aplicación crear-leer-actualizar-eliminar (CRUD) de línea de negocio simple en Aplicaciones web del Servicio de aplicaciones que realiza un seguimiento de los elementos de trabajo con las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="a5a5a-111">Autentica los usuarios contra Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a5a-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="a5a5a-112">Consulta los usuarios y grupos del directorio con la [API Graph de Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="a5a5a-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="a5a5a-113">Uso de la plantilla *Sin autenticación* de ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="a5a5a-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="a5a5a-114">Si necesita control de acceso basado en roles (RBAC) para la aplicación de línea de negocio en Azure, consulte el [siguiente paso](#next).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="a5a5a-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="a5a5a-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="a5a5a-116">Necesita lo siguiente para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="a5a5a-117">Un inquilino de Azure Active Directory con usuarios en varios grupos</span><span class="sxs-lookup"><span data-stu-id="a5a5a-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="a5a5a-118">Permisos para crear aplicaciones en el inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a5a-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="a5a5a-119">Visual Studio 2013, actualización 4 o posterior</span><span class="sxs-lookup"><span data-stu-id="a5a5a-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="a5a5a-120">SDK de Azure 2.8.1 o posterior</span><span class="sxs-lookup"><span data-stu-id="a5a5a-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="a5a5a-121">Creación e implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="a5a5a-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="a5a5a-122">En Visual Studio, haga clic en **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a5a5a-123">Seleccione **Aplicación web ASP.NET**, elija el nombre del proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="a5a5a-124">Seleccione la plantilla **MVC** y cambie a **Sin autenticación**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="a5a5a-125">Asegúrese de que **Host en la nube** está seleccionado y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="a5a5a-126">En el cuadro de diálogo **Crear App Service**, haga clic en **Agregar una cuenta** (y, en la lista desplegable, en **Agregar una cuenta**) para iniciar sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="a5a5a-127">Después de iniciar sesión, configure la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-127">Once logged in configure your web app.</span></span> <span data-ttu-id="a5a5a-128">Cree un grupo de recursos y un nuevo plan del Servicio de aplicaciones al hacer clic en el botón **Nuevo** correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="a5a5a-129">Haga clic en **Explore additional Azure services** (Explorar servicios adicionales de Azure) para continuar.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="a5a5a-130">En la pestaña **Servicios**, haga clic en **+** para agregar una base de datos SQL Database para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="a5a5a-131">En **Configurar SQL Database**, haga clic en **Nuevo** para crear una instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="a5a5a-132">En **Configurar SQL Server**, configure la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="a5a5a-133">A continuación, haga clic en **Aceptar**, **Aceptar** y **Crear** para iniciar la creación de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="a5a5a-134">En **Actividad del Servicio de aplicaciones de Azure**, verá cuándo finaliza la creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="a5a5a-135">Haga clic en **Publicar &lt;*NombreAplicación*> en esta aplicación web ahora** y, luego, en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="a5a5a-136">Cuando Visual Studio termine, la aplicación de publicación se abre en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="a5a5a-137">Configuración de la autenticación y el acceso al directorio</span><span class="sxs-lookup"><span data-stu-id="a5a5a-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="a5a5a-138">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5a5a-139">En el menú de la izquierda, haga clic en **App Services** > **&lt;*NombreAplicación*>** > **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="a5a5a-140">Active la autenticación de Azure Active Directory con un clic en **Activada** > **Azure Active Directory** > **Rápido** > **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="a5a5a-141">Haga clic en **Guardar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="a5a5a-142">Una vez guardada correctamente la configuración de autenticación, intente volver a su aplicación en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="a5a5a-143">La configuración predeterminada exige la autenticación en toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="a5a5a-144">Si aún no ha iniciado sesión, se le redirigirá a una pantalla para ello.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="a5a5a-145">Una vez iniciada la sesión, verá la aplicación protegida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="a5a5a-146">A continuación, debe habilitar el acceso a los datos del directorio.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="a5a5a-147">Vaya al [Portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="a5a5a-148">En el menú de la izquierda, haga clic en **Active Directory** > **Directorio predeterminado** > **Aplicaciones** > **&lt;*NombreAplicación*>**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="a5a5a-149">Esta es la aplicación de Azure Active Directory que crea automáticamente el Servicio de aplicaciones para habilitar la característica Autorización/autenticación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="a5a5a-150">Haga clic en **Usuarios** y en **Grupos** para asegurarse de que tiene usuarios y grupos en el directorio.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="a5a5a-151">Si no es así, cree grupos y usuarios de prueba.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="a5a5a-152">Haga clic en **Configurar** para configurar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="a5a5a-153">Desplácese hacia abajo hasta la sección **Claves** y agregue una clave al seleccionar una duración.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="a5a5a-154">A continuación, haga clic en **Permisos delegados** y seleccione **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="a5a5a-155">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="a5a5a-156">Una vez guardada la configuración, desplácese de nuevo arriba a la sección **Claves** y haga clic en el botón **Copiar** para copiar la clave de cliente.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="a5a5a-157">Si sale ahora esta página, ya no podrá volver a acceder a esta clave de cliente.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="a5a5a-158">A continuación, debe configurar la aplicación web con esta clave.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="a5a5a-159">Inicie sesión en el [Explorador de recursos de Azure](https://resources.azure.com) con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="a5a5a-160">En la parte superior de la página, haga clic en **Lectura/escritura** para realizar cambios en el Explorador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="a5a5a-161">Encuentre la configuración de autenticación de la aplicación, que se encuentra en subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="a5a5a-162">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="a5a5a-163">En el panel de edición, establezca las propiedades `clientSecret` y `additionalLoginParams` como sigue.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="a5a5a-164">Haga clic en **Put** en la parte superior para enviar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="a5a5a-165">Ahora, para probar si tiene el token de autorización para tener acceso a la API Graph de Azure Active Directory, solo tiene que ir a **https://&lt;*NombreAplicación*>.azurewebsites.net/.auth/me** en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="a5a5a-166">Si ha configurado todas las opciones correctamente, debería ver la propiedad `access_token` en la respuesta JSON.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="a5a5a-167">La ruta de dirección URL `~/.auth/me` se administra mediante la autenticación o autorización de App Service para proporcionar toda la información relacionada con la sesión autenticada.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="a5a5a-168">Para obtener más información, consulte [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a5a5a-169">La ruta de dirección URL `access_token` tiene un periodo de caducidad.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="a5a5a-170">Sin embargo, la autorización y autenticación de App Service proporciona una funcionalidad de actualización del token con `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="a5a5a-171">Para obtener más información sobre cómo utilizarlo, vea [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/)(Almacén de tokens de App Service).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="a5a5a-172">A continuación, hará algo útil con los datos del directorio.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="a5a5a-173">Funcionalidad de línea de negocio para la aplicación</span><span class="sxs-lookup"><span data-stu-id="a5a5a-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="a5a5a-174">Ahora, cree un rastreador de elementos de trabajo CRUD sencillo.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="a5a5a-175">En la carpeta ~\Models, cree un archivo de clase denominado WorkItem.cs y cambie `public class WorkItem {...}` por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="a5a5a-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="a5a5a-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="a5a5a-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="a5a5a-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="a5a5a-178">}</span><span class="sxs-lookup"><span data-stu-id="a5a5a-178">}</span></span>
   
     <span data-ttu-id="a5a5a-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="a5a5a-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="a5a5a-180">}</span><span class="sxs-lookup"><span data-stu-id="a5a5a-180">}</span></span>
2. <span data-ttu-id="a5a5a-181">Compile el proyecto para que su nuevo modelo sea accesible a la lógica de scaffolding en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="a5a5a-182">Agregue un nuevo elemento con scaffold `WorkItemsController` a la carpeta ~\Controllers (haga clic con el botón derecho en **Controladores**, seleccione **Agregar** y **Nuevo elemento con scaffold**).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="a5a5a-183">Seleccione **Controlador MVC 5 con vistas, usando Entity Framework** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="a5a5a-184">Seleccione el modelo que ha creado, haga clic en **+** y en **Agregar** para agregar un contexto de datos y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="a5a5a-185">En ~\Views\WorkItems\Create.cshtml (un elemento con scaffold automático), encuentre el método auxiliar `Html.BeginForm` y realice los siguientes cambios resaltados:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="a5a5a-186">Observe que `token` y `tenant` los usa el objeto `AadPicker` para realizar llamadas de API Graph de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="a5a5a-187">Agregará `AadPicker` más adelante.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="a5a5a-188">También puede obtener `token` y `tenant` desde el cliente con `~/.auth/me`, pero se trataría de una llamada adicional al servidor.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="a5a5a-189">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-189">For example:</span></span>
   > 
   > <span data-ttu-id="a5a5a-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="a5a5a-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="a5a5a-191">Realice los mismos cambios con ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="a5a5a-192">El objeto `AadPicker` se define en un script que se debe agregar al proyecto.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="a5a5a-193">Haga clic con el botón derecho en la carpeta ~\Scripts, seleccione **Agregar** y haga clic en **Archivo JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="a5a5a-194">Escriba `AadPickerLibrary` como nombre de archivo y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="a5a5a-195">Copie [este](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) contenido en ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="a5a5a-196">En el script, el objeto `AadPicker` llama a la [API Graph de Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) para que busque usuarios y grupos que coincidan con la entrada.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="a5a5a-197">~\Scripts\AadPickerLibrary.js también usa el [widget Autocomplete de jQuery UI](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="a5a5a-198">Por lo que necesitará agregar jQuery UI al proyecto.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="a5a5a-199">Haga clic con el botón derecho en el proyecto y haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="a5a5a-200">En el Administrador de paquetes NuGet, haga clic en Examinar, escriba **jquery-ui** en la barra de búsqueda y haga clic en **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="a5a5a-201">En el panel derecho, haga clic en **Instalar** y en **Aceptar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="a5a5a-202">Abra ~\App_Start\BundleConfig.cs y realice los cambios resaltados siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="a5a5a-203">Existen más formas productivas de administrar los archivos JavaScript y CSS en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="a5a5a-204">Sin embargo, por motivos de simplicidad solo se incluyen en los paquetes que se cargan con cada vista.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="a5a5a-205">Finalmente, en ~\Global.asax, agregue la siguiente línea de código en el método `Application_Start()`.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="a5a5a-206">`Ctrl`+`.` en cada error de resolución de nombres para corregirlo.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="a5a5a-207">Necesita esta línea de código porque la plantilla de MVC predeterminada usa la decoración <code>[ValidateAntiForgeryToken]</code> en algunas de las acciones.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="a5a5a-208">Debido al comportamiento descrito por [Brock Allen](https://twitter.com/BrockLAllen) en [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/), su HTTP POST puede generar un error de validación de token antifalsificación porque:</span><span class="sxs-lookup"><span data-stu-id="a5a5a-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="a5a5a-209">Azure Active Directory no envía http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, que el token antifalsificación requiere de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="a5a5a-210">Si Azure Active Directory está sincronizado con directorios con AD FS, la confianza de AD FS tampoco envía de manera predeterminada la notificación de http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, aunque puede configurar AD FS manualmente para enviar esta notificación.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="a5a5a-211">`ClaimTypes.NameIdentifies` especifica la notificación `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que proporciona Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="a5a5a-212">Ahora, publique los cambios.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-212">Now, publish your changes.</span></span> <span data-ttu-id="a5a5a-213">Haga clic con el botón derecho en el proyecto y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="a5a5a-214">Haga clic en **Configuración**, asegúrese de que hay una cadena de conexión a la instancia de SQL Database, seleccione **Actualizar base de datos** para realizar los cambios de esquema para el modelo y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="a5a5a-215">En el explorador, vaya a https://&lt;*NombreAplicación*>.azurewebsites.net/workitems y haga clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="a5a5a-216">Haga clic en el cuadro **AssignedToName** .</span><span class="sxs-lookup"><span data-stu-id="a5a5a-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="a5a5a-217">Ahora debería ver los usuarios y grupos desde el inquilino de Azure Active Directory en una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="a5a5a-218">Puede escribir para filtrar o utilizar la clave `Up` o `Down`; también puede hacer clic para seleccionar el usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="a5a5a-219">Haga clic en **Crear** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="a5a5a-220">A continuación, haga clic en **Editar** en el elemento de trabajo creado para observar el mismo comportamiento.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="a5a5a-221">Enhorabuena, está ejecutando una aplicación de línea de negocio en Azure con acceso al directorio.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="a5a5a-222">Con la API Graph puede hacer mucho más.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="a5a5a-223">Consulte [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Referencias de la API Graph de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="a5a5a-224">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="a5a5a-224">Next Step</span></span>
<span data-ttu-id="a5a5a-225">Si necesita control de acceso basado en roles (RBAC) para la aplicación de línea de negocio en Azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obtener un ejemplo del equipo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5a5a-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="a5a5a-226">Muestra cómo habilitar los roles para su aplicación de Azure Active Directory y, a continuación, autorizar a los usuarios con la decoración `[Authorize]` .</span><span class="sxs-lookup"><span data-stu-id="a5a5a-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="a5a5a-227">Si la aplicación de línea de negocio necesita acceso a datos locales, consulte [Acceso a recursos locales mediante conexiones híbridas en el Servicio de aplicaciones de Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a5a5a-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="a5a5a-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a5a5a-228">Further resources</span></span>
* [<span data-ttu-id="a5a5a-229">Autenticación y autorización en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a5a5a-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="a5a5a-230">Autenticación con Active Directory local en aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a5a5a-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="a5a5a-231">Creación de una aplicación de línea de negocio en Azure con autenticación de AD FS</span><span class="sxs-lookup"><span data-stu-id="a5a5a-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="a5a5a-232">App Service Auth and the Azure AD Graph API (Autenticación del Servicio de aplicaciones y la API Graph de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a5a5a-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="a5a5a-233">Ejemplos y documentación de Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a5a-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="a5a5a-234">Tipos de notificaciones y tokens admitidos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a5a-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
