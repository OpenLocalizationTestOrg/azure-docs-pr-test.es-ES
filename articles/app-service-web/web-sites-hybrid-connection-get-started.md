---
title: "Acceso a recursos locales mediante conexiones híbridas en el Servicio de aplicaciones de Azure"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="a27f0-103">Acceso a recursos locales mediante conexiones híbridas en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a27f0-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="a27f0-104">Puede conectar una aplicación del Servicio de aplicaciones de Azure a cualquier recurso local que use un puerto TCP estático, como SQL Server, MySQL, API Web HTTP y la mayoría de los servicios web personalizados.</span><span class="sxs-lookup"><span data-stu-id="a27f0-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="a27f0-105">En este artículo se muestra cómo crear una conexión híbrida entre el Servicio de aplicaciones y una base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="a27f0-106">La parte Aplicaciones web de la característica Conexiones híbridas solo está disponible en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a27f0-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a27f0-107">Para crear una conexión en Servicios de BizTalk, consulte [Conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="a27f0-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="a27f0-108">Este contenido también se aplica a Aplicaciones móviles en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a27f0-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a27f0-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a27f0-109">Prerequisites</span></span>
* <span data-ttu-id="a27f0-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a27f0-110">An Azure subscription.</span></span> <span data-ttu-id="a27f0-111">Para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a27f0-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="a27f0-112">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a27f0-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a27f0-113">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a27f0-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="a27f0-114">Para usar una base de datos de SQL Server o SQL Server Express local con una conexión híbrida, es necesario habilitar TCP/IP en un puerto estático.</span><span class="sxs-lookup"><span data-stu-id="a27f0-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="a27f0-115">Se recomienda usar una instancia predeterminada en SQL Server porque usa el puerto estático 1433.</span><span class="sxs-lookup"><span data-stu-id="a27f0-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="a27f0-116">Para obtener información sobre cómo instalar y configurar SQL Server Express para su uso con conexiones híbridas, consulte [Conexión a un servidor SQL Server local desde un sitio web de Azure mediante conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="a27f0-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="a27f0-117">El equipo en el que instala el agente local de Administrador de conexiones híbridas se describe más adelante en este artículo:</span><span class="sxs-lookup"><span data-stu-id="a27f0-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="a27f0-118">Debe ser capaz de conectarse a Azure a través del puerto 5671</span><span class="sxs-lookup"><span data-stu-id="a27f0-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="a27f0-119">Debe poder establecer comunicación con el *hostname*:*número de puerto* de su recurso local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="a27f0-120">En estos pasos de este artículo se supone que usa el explorador del equipo que hospeda el agente de conexiones híbridas local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="a27f0-121">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a27f0-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="a27f0-122">Si ya ha creado un back-end de aplicación web o aplicación móvil en el Portal de Azure que desea usar en este tutorial, puede omitir este paso e ir directamente a [Creación de una conexión híbrida y un servicio de BizTalk](#CreateHC) y comenzar desde allí.</span><span class="sxs-lookup"><span data-stu-id="a27f0-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="a27f0-123">En la esquina superior izquierda de [Azure Portal](https://portal.azure.com), haga clic en **Nuevo** > **Web y móvil** > **Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![New web app][NewWebsite]
2. <span data-ttu-id="a27f0-125">En la hoja **Aplicación web**, proporcione una dirección URL y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="a27f0-127">Transcurridos unos segundos, la aplicación web se creará y aparecerá su hoja de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a27f0-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="a27f0-128">El cuadro es un panel que se desplaza en vertical y que le permite administrar su sitio.</span><span class="sxs-lookup"><span data-stu-id="a27f0-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="a27f0-130">Para comprobar que el sitio está activo, puede hacer clic en el icono **Examinar** para mostrar la página predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a27f0-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Haga clic en examinar para ver su aplicación web][Browse]
   
    ![Página de aplicación web predeterminada][DefaultWebSitePage]

<span data-ttu-id="a27f0-133">A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a27f0-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="a27f0-134">Creación de una conexión híbrida y un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="a27f0-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="a27f0-135">En la hoja de la aplicación web, haga clic en **Todas las configuraciones** > **Redes** > **Configurar los puntos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. <span data-ttu-id="a27f0-137">En la hoja de conexiones híbridas, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="a27f0-138">Se abre la hoja **Agregar una conexión híbrida** .</span><span class="sxs-lookup"><span data-stu-id="a27f0-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="a27f0-139">Dado que esta es su primera conexión híbrida, la opción **Nueva conexión híbrida** aparece preseleccionada y se abre la hoja **Crear conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="a27f0-141">En la **hoja Crear conexión híbrida**:</span><span class="sxs-lookup"><span data-stu-id="a27f0-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="a27f0-142">En **Nombre**, escriba un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="a27f0-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="a27f0-143">En **Nombre de host**, escriba el nombre del equipo local que hospeda su recurso.</span><span class="sxs-lookup"><span data-stu-id="a27f0-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="a27f0-144">En **Puerto**, escriba el número de puerto que usa su recurso local (1433 para una instancia predeterminada de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a27f0-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="a27f0-145">Haga clic en **Servicio de Biz Talk**</span><span class="sxs-lookup"><span data-stu-id="a27f0-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="a27f0-146">Se abre la hoja **Crear servicio de BizTalk** .</span><span class="sxs-lookup"><span data-stu-id="a27f0-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="a27f0-147">Escriba un nombre para el servicio de BizTalk y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Crear servicio de BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="a27f0-149">La hoja **Crear servicio de BizTalk** se cierre y vuelve a la hoja **Crear conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="a27f0-150">En la hoja Crear conexión híbrida, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Haga clic en Aceptar][CreateBTScomplete]
6. <span data-ttu-id="a27f0-152">Al finalizar el proceso, el área de notificaciones del portal le informa de que la conexión se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a27f0-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="a27f0-153">En la hoja de la aplicación web, el icono **Conexiones híbridas** ahora muestra que se creó una conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="a27f0-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="a27f0-155">Llegados a este punto, ha completado una parte importante de la infraestructura de conexión híbrida en la nube.</span><span class="sxs-lookup"><span data-stu-id="a27f0-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="a27f0-156">A continuación, creará la parte local correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a27f0-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="a27f0-157">Instalación del Administrador de conexiones híbridas local para realizar la conexión</span><span class="sxs-lookup"><span data-stu-id="a27f0-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="a27f0-158">En la hoja de la aplicación web, haga clic en **Todas las configuraciones** > **Redes** > **Configurar los puntos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="a27f0-160">En la hoja **Conexiones híbridas**, la columna **Estado** del punto de conexión agregado recientemente muestra **No conectado**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="a27f0-161">Haga clic en la conexión para configurarla.</span><span class="sxs-lookup"><span data-stu-id="a27f0-161">Click the connection to configure it.</span></span>
   
    ![No conectado][NotConnected]
   
    <span data-ttu-id="a27f0-163">Se abre el cuadro de la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="a27f0-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="a27f0-165">En la hoja, haga clic en **Configuración del agente de escucha**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="a27f0-167">Se abre la hoja **Propiedades de conexión híbrida** .</span><span class="sxs-lookup"><span data-stu-id="a27f0-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="a27f0-168">En **Administrador de conexiones híbridas local**, elija **Haga clic aquí para instalar**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Haga clic aquí para instalar][ClickToInstallHCM]
5. <span data-ttu-id="a27f0-170">En el cuadro de diálogo de advertencia de seguridad Ejecución de la aplicación, elija **Ejecutar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="a27f0-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Choose Run to continue][ApplicationRunWarning]
6. <span data-ttu-id="a27f0-172">En el cuadro de diálogo **Control de cuentas de usuario**, elija **Sí**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="a27f0-174">El Administrador de conexiones híbridas se descarga y se instala.</span><span class="sxs-lookup"><span data-stu-id="a27f0-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalación][HCMInstalling]
8. <span data-ttu-id="a27f0-176">Cuando finalice la instalación, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-176">When the install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="a27f0-178">En la hoja **Conexiones híbridas**, la columna **Estado** ahora muestra **Conectado**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="a27f0-180">Ahora que la infraestructura de conexión híbrida se ha completado, puede crear una aplicación híbrida que la utilice.</span><span class="sxs-lookup"><span data-stu-id="a27f0-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="a27f0-181">En las secciones siguientes se muestra cómo usar una conexión híbrida con un proyecto de back-end .NET de Aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="a27f0-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="a27f0-182">Configuración del proyecto de back-end .NET de la aplicación móvil para conectarse a la base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="a27f0-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="a27f0-183">En Servicio de aplicaciones, un proyecto de back-end .NET de Aplicaciones móviles es simplemente una aplicación web de ASP.NET con un SDK de Aplicaciones móviles adicional instalado e inicializado.</span><span class="sxs-lookup"><span data-stu-id="a27f0-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="a27f0-184">Para usar la aplicación web como un back-end de Aplicaciones móviles, es preciso [descargar e inicializar el SDK del back-end .NET de Aplicaciones móviles](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="a27f0-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="a27f0-185">Para Aplicaciones móviles, también necesita definir una cadena de conexión para la base de datos local y modificar el back-end para usar esta conexión.</span><span class="sxs-lookup"><span data-stu-id="a27f0-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="a27f0-186">En el Explorador de soluciones de Visual Studio, abra el archivo Web.config del back-end .NET de la aplicación móvil, busque la sección **connectionStrings** y agregue una nueva entrada de SqlClient similar a la siguiente, que apunte a la base de datos de SQL Server local:</span><span class="sxs-lookup"><span data-stu-id="a27f0-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="a27f0-187">No olvide reemplazar `<**secure_password**>` en esta cadena por la contraseña que creó para *HbyridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="a27f0-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="a27f0-188">Haga clic en **Guardar** en Visual Studio para guardar el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="a27f0-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a27f0-189">Esta configuración de conexión se usa cuando se ejecuta en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="a27f0-190">Cuando se ejecuta en Azure, esta configuración se reemplaza por la configuración de conexión definida en el portal.</span><span class="sxs-lookup"><span data-stu-id="a27f0-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="a27f0-191">Expanda la carpeta **Modelos** y abra el archivo de modelo de datos que termina con *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="a27f0-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="a27f0-192">Modifique el constructor de instancia **DbContext** para pasar el valor `OnPremisesDBConnection` al constructor **DbContext** base, de forma parecida al siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="a27f0-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="a27f0-193">El servicio usará ahora la nueva conexión a la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a27f0-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="a27f0-194">Actualización del back-end de la aplicación móvil para usar la cadena de conexión local</span><span class="sxs-lookup"><span data-stu-id="a27f0-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="a27f0-195">A continuación, deberá agregar una configuración de aplicación para esta cadena de conexión nueva para poder utilizarla desde Azure.</span><span class="sxs-lookup"><span data-stu-id="a27f0-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="a27f0-196">En [Azure Portal](https://portal.azure.com) en el código de back-end de aplicación web de la aplicación móvil, haga clic en **Toda la configuración** y luego en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="a27f0-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="a27f0-197">En la hoja **Configuración de aplicación web**, desplácese a **Cadenas de conexión** y agregue una nueva cadena de conexión de **SQL Server** denominada `OnPremisesDBConnection` con un valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="a27f0-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="a27f0-198">Sustituya `<**secure_password**>` por la contraseña segura de su base de datos local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Cadena de conexión de la base de datos local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="a27f0-200">Presione **Guardar** para guardar la conexión híbrida y la cadena de conexión que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="a27f0-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="a27f0-201">Llegados a este punto puede volver a publicar el proyecto de servidor y probar la nueva conexión con los clientes existentes de Aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="a27f0-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="a27f0-202">Mediante la conexión híbrida, se realizarán operaciones de escritura y lectura de datos en la base de datos local.</span><span class="sxs-lookup"><span data-stu-id="a27f0-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="a27f0-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a27f0-203">Next Steps</span></span>
* <span data-ttu-id="a27f0-204">Para obtener información sobre cómo crear una aplicación web de ASP.NET que use una conexión híbrida, consulte [Conexión a un servidor SQL Server local desde un sitio web de Azure mediante conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="a27f0-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="a27f0-205">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a27f0-205">Additional Resources</span></span>
[<span data-ttu-id="a27f0-206">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a27f0-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="a27f0-207">Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a27f0-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="a27f0-208">Sitio web de conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a27f0-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="a27f0-209">Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a27f0-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="a27f0-210">Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a27f0-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="a27f0-211">Conexión a un servidor SQL Server local desde Servicios móviles de Azure mediante conexiones híbridas (vídeo de Canal 9)</span><span class="sxs-lookup"><span data-stu-id="a27f0-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="a27f0-212">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a27f0-212">What's changed</span></span>
* <span data-ttu-id="a27f0-213">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a27f0-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
