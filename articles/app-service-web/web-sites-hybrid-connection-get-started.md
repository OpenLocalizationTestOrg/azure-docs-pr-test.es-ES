---
title: "recursos locales de aaaAccess usando conexiones híbridas en el servicio de aplicación de Azure"
description: "Creación de una conexión entre una aplicación web en Servicio de aplicaciones de Azure y un recurso local que usa un puerto TCP estático"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="c73a2-103">Acceso a recursos locales mediante conexiones híbridas en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c73a2-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="c73a2-104">Puede conectar un recurso de local de tooany de aplicación de servicio de aplicaciones de Azure que usa un puerto TCP estático, como SQL Server, MySQL, las API Web de HTTP y mayoría de los servicios Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="c73a2-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="c73a2-105">Este artículo muestra cómo toocreate una conexión híbrida entre el servicio de aplicaciones y una base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="c73a2-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="c73a2-106">parte de las aplicaciones Web de Hola de característica de conexiones híbridas de hello solo está disponible en hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c73a2-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c73a2-107">toocreate una conexión de servicios de BizTalk, consulte [conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="c73a2-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="c73a2-108">Este contenido también aplica a aplicaciones de tooMobile en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a2-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c73a2-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c73a2-109">Prerequisites</span></span>
* <span data-ttu-id="c73a2-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a2-110">An Azure subscription.</span></span> <span data-ttu-id="c73a2-111">Para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c73a2-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="c73a2-112">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c73a2-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c73a2-113">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="c73a2-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="c73a2-114">toouse un local SQL Server o base de datos de SQL Server Express con una conexión híbrida, TCP/IP debe toobe habilitado en un puerto estático.</span><span class="sxs-lookup"><span data-stu-id="c73a2-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="c73a2-115">Se recomienda usar una instancia predeterminada en SQL Server porque usa el puerto estático 1433.</span><span class="sxs-lookup"><span data-stu-id="c73a2-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="c73a2-116">Para obtener información sobre cómo instalar y configurar SQL Server Express para usarlo con conexiones híbridas, vea [tooan conectar en SQL Server local desde un sitio web de Azure usando conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="c73a2-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="c73a2-117">equipo de Hello en el que instale a agente de administrador de conexiones híbridas local Hola que se describe más adelante en este artículo:</span><span class="sxs-lookup"><span data-stu-id="c73a2-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="c73a2-118">Debe ser capaz de tooconnect tooAzure a través del puerto 5671</span><span class="sxs-lookup"><span data-stu-id="c73a2-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="c73a2-119">Debe ser capaz de tooreach hello *hostname*:*portnumber* de su recurso local.</span><span class="sxs-lookup"><span data-stu-id="c73a2-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="c73a2-120">pasos de Hello en este artículo se supone que está usando explorador Hola desde equipo Hola que hospedará el agente de conexión híbrida de hello local.</span><span class="sxs-lookup"><span data-stu-id="c73a2-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="c73a2-121">Crear una aplicación web en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c73a2-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="c73a2-122">Si ya ha creado una aplicación web o aplicación móvil back-end en hello Portal de Azure que quiere toouse de este tutorial, puede pasar demasiado[crear una conexión híbrida y un BizTalk Service](#CreateHC) e iniciar desde allí.</span><span class="sxs-lookup"><span data-stu-id="c73a2-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="c73a2-123">En la esquina izquierda superior de Hola de hello [Portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil** > **aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![New web app][NewWebsite]
2. <span data-ttu-id="c73a2-125">En hello **aplicación Web** hoja, proporcione una dirección URL y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="c73a2-127">Después de unos segundos, se crea la aplicación web de hello y aparece su hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c73a2-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="c73a2-128">hoja de Hello es un panel puede desplazar verticalmente que le permite administrar el sitio.</span><span class="sxs-lookup"><span data-stu-id="c73a2-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="c73a2-130">sitio de hello tooverify está activo, puede hacer clic en hello **examinar** página predeterminada de icono toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Haga clic en Examinar toosee su aplicación web][Browse]
   
    ![Página de aplicación web predeterminada][DefaultWebSitePage]

<span data-ttu-id="c73a2-133">A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="c73a2-134">Creación de una conexión híbrida y un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="c73a2-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="c73a2-135">En la hoja de la aplicación web, haga clic en **Todas las configuraciones** > **Redes** > **Configurar los puntos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. <span data-ttu-id="c73a2-137">En la hoja de conexiones híbridas de hello, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="c73a2-138">Hola **agregar una conexión híbrida** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="c73a2-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="c73a2-139">Puesto que se trata de la primera conexión híbrida, Hola **conexión híbrida nueva** opción está preseleccionada y Hola **crear conexión híbrida** hoja se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c73a2-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="c73a2-141">En hello **hoja de conexión híbrida crear**:</span><span class="sxs-lookup"><span data-stu-id="c73a2-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="c73a2-142">Para **nombre**, proporcione un nombre para la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="c73a2-143">Para **Hostname**, escriba Hola nombre del equipo local de Hola que hospeda el recurso.</span><span class="sxs-lookup"><span data-stu-id="c73a2-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="c73a2-144">Para **puerto**, escriba Hola número de puerto que el recurso local utiliza (1433 para una instancia predeterminada de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c73a2-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="c73a2-145">Haga clic en **Servicio de Biz Talk**</span><span class="sxs-lookup"><span data-stu-id="c73a2-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="c73a2-146">Hola **crear servicio de BizTalk** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="c73a2-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="c73a2-147">Escriba un nombre para el servicio de BizTalk de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Crear servicio de BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="c73a2-149">Hola **crear servicio de BizTalk** hoja se cierra y se devuelven toohello **crear conexión híbrida** hoja.</span><span class="sxs-lookup"><span data-stu-id="c73a2-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="c73a2-150">En hello crear híbrida conexión hoja, haga clic **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Haga clic en Aceptar][CreateBTScomplete]
6. <span data-ttu-id="c73a2-152">Cuando se completa el proceso de hello, área de notificaciones de Hola Hola Portal le informa de que conexión Hola se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c73a2-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="c73a2-153">En la hoja de la aplicación web hello, Hola **conexiones híbridas** icono muestra ahora que se ha creado 1 conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="c73a2-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="c73a2-155">En este momento, ha completado una parte importante de la infraestructura de conexión de hello en la nube híbrida.</span><span class="sxs-lookup"><span data-stu-id="c73a2-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="c73a2-156">A continuación, creará la parte local correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c73a2-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="c73a2-157">Instalar Hola local Administrador de conexiones híbridas toocomplete Hola conexión</span><span class="sxs-lookup"><span data-stu-id="c73a2-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="c73a2-158">En la hoja de la aplicación de hello web, haga clic en **toda la configuración de** > **red** > **configurar los extremos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="c73a2-160">En hello **conexiones híbridas** hoja, hello **estado** recientemente agrega la columna de hello muestra de extremo **no conectado**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="c73a2-161">Haga clic en tooconfigure de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-161">Click hello connection tooconfigure it.</span></span>
   
    ![No conectado][NotConnected]
   
    <span data-ttu-id="c73a2-163">se abre la hoja de conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="c73a2-165">En la hoja de hello, haga clic en **el programa de instalación de agente de escucha**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="c73a2-167">Hola **propiedades de conexión híbrida** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="c73a2-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="c73a2-168">En **Administrador de conexiones híbridas local**, elija **haga clic aquí tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Haga clic aquí tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="c73a2-170">Cuadro de diálogo de advertencia de seguridad ejecutar aplicación Hola, elija **ejecutar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c73a2-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Elija toocontinue de ejecución][ApplicationRunWarning]
6. <span data-ttu-id="c73a2-172">Hola **User Account Control** cuadro de diálogo, elija **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="c73a2-174">Hola, Administrador de conexiones híbridas se descargará e instalará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c73a2-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalación][HCMInstalling]
8. <span data-ttu-id="c73a2-176">Cuando se haya completado la instalación de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-176">When hello install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="c73a2-178">En hello **conexiones híbridas** hoja, hello **estado** columna muestra ahora **conectado**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="c73a2-180">Ahora esa infraestructura de conexión híbrida Hola está completa, puede crear una aplicación híbrida que lo utilice.</span><span class="sxs-lookup"><span data-stu-id="c73a2-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="c73a2-181">Hello las secciones siguientes muestran cómo toouse una conexión híbrida con un proyecto de back-end de .NET de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="c73a2-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="c73a2-182">Configurar Hola Mobile aplicación back-end proyecto tooconnect toohello SQL Server base de datos .NET</span><span class="sxs-lookup"><span data-stu-id="c73a2-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="c73a2-183">En Servicio de aplicaciones, un proyecto de back-end .NET de Aplicaciones móviles es simplemente una aplicación web de ASP.NET con un SDK de Aplicaciones móviles adicional instalado e inicializado.</span><span class="sxs-lookup"><span data-stu-id="c73a2-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="c73a2-184">toouse la aplicación web como un back-end de aplicaciones móviles, debe [descargar e inicializar back-end de hello Mobile aplicaciones .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="c73a2-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="c73a2-185">Para las aplicaciones móviles, también necesita toodefine una cadena de conexión de base de datos de hello local y modificar Hola back-end toouse esta conexión.</span><span class="sxs-lookup"><span data-stu-id="c73a2-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="c73a2-186">En el Explorador de soluciones en Visual Studio, el archivo Web.config de hello abierto para el back-end de .NET de aplicación móvil, busque hello **connectionStrings** sección, agregue una nueva entrada de SqlClient como siguiente hello, qué toohello puntos SQL local Base de datos del servidor:</span><span class="sxs-lookup"><span data-stu-id="c73a2-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="c73a2-187">Recuerde tooreplace `<**secure_password**>` en esta cadena con la contraseña de Hola que creó para *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="c73a2-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="c73a2-188">Haga clic en **guardar** en el archivo Web.config de Visual Studio toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c73a2-189">Esta configuración de conexión se utiliza cuando se ejecuta en el equipo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="c73a2-190">Cuando se ejecuta en Azure, esta configuración es reemplazada por configuración de conexión de hello definido en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="c73a2-191">Expanda hello **modelos** carpetas y archivos de modelo de datos abierto hello, que finaliza en *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="c73a2-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="c73a2-192">Modificar hello **DbContext** toopass de constructor de instancia Hola valor `OnPremisesDBConnection` toohello base **DbContext** constructor, toohello similar siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="c73a2-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="c73a2-193">servicio de Hello ahora va a usar base de datos de hello nueva conexión toohello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c73a2-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="c73a2-194">Actualizar la cadena de conexión local de hello aplicación móvil back-end toouse Hola</span><span class="sxs-lookup"><span data-stu-id="c73a2-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="c73a2-195">A continuación, tendrá que tooadd una configuración de aplicación para esta nueva cadena de conexión para que se puede utilizar de Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a2-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="c73a2-196">Nuevo en hello [portal de Azure](https://portal.azure.com) en el código de hello web aplicación back-end de la aplicación móvil, haga clic en **toda la configuración de**, a continuación, **configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="c73a2-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="c73a2-197">Hola **configuración de aplicación Web** hoja, desplácese hacia abajo demasiado**las cadenas de conexión** y agregue un nuevo **SQL Server** cadena de conexión denominada `OnPremisesDBConnection` con un valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="c73a2-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="c73a2-198">Reemplace `<**secure_password**>` con contraseña segura de hello para la base de datos local.</span><span class="sxs-lookup"><span data-stu-id="c73a2-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Cadena de conexión de la base de datos local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="c73a2-200">Presione **guardar** conexión híbrida de toosave hello y cadena de conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="c73a2-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="c73a2-201">En este momento puede volver a publicar el proyecto de servidor de Hola y probar Hola nueva conexión con los clientes existentes de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="c73a2-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="c73a2-202">Datos se pueden leer y escritos toohello de base de datos local mediante la conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a2-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="c73a2-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c73a2-203">Next Steps</span></span>
* <span data-ttu-id="c73a2-204">Para obtener información acerca de cómo crear una aplicación web ASP.NET que utiliza una conexión híbrida, consulte [tooan conectar en SQL Server local desde un sitio web de Azure usando conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="c73a2-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="c73a2-205">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c73a2-205">Additional Resources</span></span>
[<span data-ttu-id="c73a2-206">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="c73a2-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="c73a2-207">Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="c73a2-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="c73a2-208">Sitio web de conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="c73a2-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="c73a2-209">Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="c73a2-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="c73a2-210">Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="c73a2-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="c73a2-211">Conectar tooan local de SQL Server de servicios móviles de Azure usando conexiones híbridas (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="c73a2-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="c73a2-212">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="c73a2-212">What's changed</span></span>
* <span data-ttu-id="c73a2-213">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c73a2-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
