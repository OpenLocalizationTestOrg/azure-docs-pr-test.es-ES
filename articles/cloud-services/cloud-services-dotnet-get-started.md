---
title: aaaGet a trabajar con ASP.NET y servicios de nube de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una aplicación de varios nivel con ASP.NET MVC y Azure. aplicación Hello se ejecuta en un servicio de nube, con el rol web y rol de trabajo. Utiliza Entity Framework, Base de datos SQL y blobs y colas de Almacenamiento de Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="2d07e-105">Introducción a Servicios en la nube de Azure y ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2d07e-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="2d07e-106">Información general</span><span class="sxs-lookup"><span data-stu-id="2d07e-106">Overview</span></span>
<span data-ttu-id="2d07e-107">Este tutorial se muestra cómo toocreate una aplicación de varios niveles .NET con un front-end, ASP.NET MVC e implementarlo tooan [servicio de nube de Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="2d07e-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="2d07e-108">Hola aplicación usa [base de datos de SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [servicio Blob de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), hello y [servicio cola de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="2d07e-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="2d07e-109">También puede [descargar el proyecto de Visual Studio de hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de hello MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="2d07e-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="2d07e-110">Hola tutorial le muestra cómo localmente, aplicación hello toobuild y ejecute cómo toodeploy lo tooAzure y Hola de ejecución en la nube y cómo toobuild desde cero.</span><span class="sxs-lookup"><span data-stu-id="2d07e-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="2d07e-111">Puede iniciar creación desde el principio y, a continuación, Hola prueba e implementar pasos más adelante si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="2d07e-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="2d07e-112">Aplicación Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="2d07e-112">Contoso Ads application</span></span>
<span data-ttu-id="2d07e-113">aplicación Hello es un tablón de anuncios publicitarios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="2d07e-114">Los usuarios crean un anuncio introduciendo texto y cargando una imagen.</span><span class="sxs-lookup"><span data-stu-id="2d07e-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="2d07e-115">Puede ver una lista de anuncios con imágenes en miniatura y pueden ver imagen a tamaño completo hello cuando selecciona un detalles de hello toosee de ad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="2d07e-117">aplicación Hello usa hello [centrada en la cola de trabajo patrón](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga de trabajo de hello intensiva de CPU de creación de proceso de miniaturas tooa back-end.</span><span class="sxs-lookup"><span data-stu-id="2d07e-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="2d07e-118">Arquitectura alternativa: sitios web y WebJobs</span><span class="sxs-lookup"><span data-stu-id="2d07e-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="2d07e-119">Este tutorial muestra cómo toorun front-end y back-end en un Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="2d07e-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="2d07e-120">Una alternativa es toorun Hola front-end en una [sitio Web de Azure](/services/web-sites/) y usar hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) característica (actualmente en versión preliminar) para hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2d07e-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="2d07e-121">Para obtener un tutorial que utiliza trabajos Web, consulte [empezar a trabajar con el SDK de WebJobs de Azure hello](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2d07e-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="2d07e-122">Para obtener información acerca de cómo los servicios toochoose Hola que mejor ajusta su escenario, consulte [comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2d07e-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2d07e-123">Temas que se abordarán</span><span class="sxs-lookup"><span data-stu-id="2d07e-123">What you'll learn</span></span>
* <span data-ttu-id="2d07e-124">¿Cómo tooenable Hola a su equipo de desarrollo de Azure mediante la instalación del SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="2d07e-125">¿Cómo toocreate un en Visual Studio en la nube proyecto de servicio con un rol web de ASP.NET MVC y un rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="2d07e-126">¿Cómo tootest Hola nube proyecto de servicio localmente, mediante el emulador de almacenamiento de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="2d07e-127">Cómo toopublish Hola nube proyecto tooan Azure servicio en la nube y pruebe el uso de una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="2d07e-128">Cómo tooupload archivos y almacenarlos en el servicio de Blob de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="2d07e-129">¿Cómo toouse Hola servicio de cola de Azure para la comunicación entre niveles.</span><span class="sxs-lookup"><span data-stu-id="2d07e-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d07e-130">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2d07e-130">Prerequisites</span></span>
<span data-ttu-id="2d07e-131">Hello tutorial se da por supuesto que comprende [servicios de nube de los conceptos básicos sobre Azure](cloud-services-choose-me.md) como *rol web* y *rol de trabajo* terminología.</span><span class="sxs-lookup"><span data-stu-id="2d07e-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="2d07e-132">También se supone que sabe cómo toowork con [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [formularios Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) proyectos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="2d07e-133">aplicación de ejemplo de Hola utiliza MVC, pero la mayoría de tutorial de hello también se aplica tooWeb formularios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="2d07e-134">Puede ejecutar la aplicación hello localmente sin una suscripción de Azure, pero necesitará una toodeploy Hola aplicación toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="2d07e-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="2d07e-135">Si aún no la tiene, puede [activar los beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) o [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="2d07e-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="2d07e-136">instrucciones del tutorial Hola trabajan con cualquiera de hello siguientes productos:</span><span class="sxs-lookup"><span data-stu-id="2d07e-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="2d07e-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2d07e-137">Visual Studio 2013</span></span>
* <span data-ttu-id="2d07e-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2d07e-138">Visual Studio 2015</span></span>
* <span data-ttu-id="2d07e-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2d07e-139">Visual Studio 2017</span></span>

<span data-ttu-id="2d07e-140">Si no tiene uno de estos, Visual Studio puede instalarse automáticamente al instalar hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="2d07e-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="2d07e-141">Arquitectura de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2d07e-141">Application architecture</span></span>
<span data-ttu-id="2d07e-142">aplicación Hello almacena anuncios en una base de datos SQL con tablas de hello toocreate Entity Framework Code First y acceder a los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="2d07e-143">Para cada anuncio Hola base de datos almacena dos direcciones URL, uno para Hola imagen a tamaño completo y otra para la miniatura de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="2d07e-145">Cuando un usuario carga una imagen, front-end de Hola que se ejecuta en un rol web almacena la imagen de hello en un [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), y almacena información de anuncios de Hola en base de datos de hello con una dirección URL que señala toohello blob.</span><span class="sxs-lookup"><span data-stu-id="2d07e-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="2d07e-146">Hola al mismo tiempo, escribe un tooan mensaje cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="2d07e-147">Un proceso de back-end que se ejecuta en un rol de trabajo periódicamente sondea Hola si hay mensajes nuevos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="2d07e-148">Cuando aparezca un mensaje nuevo, rol de trabajo de hello crea una vista en miniatura de esa imagen y actualizaciones Hola campo de base de datos de dirección URL en miniatura para que ad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="2d07e-149">Hello siguiente diagrama muestra cómo interactúan las partes de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="2d07e-151">Descargue y ejecute la solución de hello completado</span><span class="sxs-lookup"><span data-stu-id="2d07e-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="2d07e-152">Descargue y descomprima hello [completado solución](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="2d07e-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="2d07e-153">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="2d07e-154">De hello **archivo** menú elija **Abrir proyecto**, desplácese toowhere descargó solución hello y, a continuación, abra el archivo de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="2d07e-155">Presione la solución CTRL + MAYÚS + B toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="2d07e-156">De forma predeterminada, Visual Studio restaurará automáticamente contenido del paquete NuGet hello, que no se incluyó en hello *.zip* archivo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="2d07e-157">Si no se restauran los paquetes de saludo, instálelos manualmente va toohello **administrar paquetes de NuGet para la solución** cuadro de diálogo y haga clic en hello **restaurar** situado en la parte superior de hello derecha.</span><span class="sxs-lookup"><span data-stu-id="2d07e-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="2d07e-158">En **el Explorador de soluciones**, asegúrese de que **ContosoAdsCloudService** está seleccionado como proyecto de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="2d07e-159">Si está utilizando Visual Studio 2015 o versiones posteriores, cambie la cadena de conexión de SQL Server de hello en la aplicación hello *Web.config* archivo de proyecto de ContosoAdsWeb de Hola y Hola *ServiceConfiguration.Local.cscfg* archivo del proyecto de ContosoAdsCloudService Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="2d07e-160">En cada caso, cambie "(localdb) \v11.0" demasiado "(localdb) \MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="2d07e-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="2d07e-161">Presione la aplicación de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="2d07e-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="2d07e-162">Cuando se ejecuta un proyecto de servicio de nube localmente, Visual Studio, se invoca automáticamente hello Azure *emulador de proceso* y Azure *emulador de almacenamiento*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="2d07e-163">Hola de proceso utiliza emulador rol web de su equipo recursos toosimulate hello y entornos de rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="2d07e-164">emulador de almacenamiento de Hello usa un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate almacenamiento en nube de Azure de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="2d07e-165">Hello primera vez que se ejecuta un proyecto de servicio de nube, que tarda aproximadamente un minuto Hola emuladores toostart seguridad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="2d07e-166">Cuando haya finalizado de inicio del emulador, explorador predeterminado de hello abre toohello página de inicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2d07e-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="2d07e-168">Haga clic en **Crear un anuncio**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="2d07e-169">Escriba algunos datos de prueba y seleccione un *.jpg* tooupload la imagen y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="2d07e-171">aplicación Hello queda toohello página de índice, pero no muestra una vista en miniatura para nuevo anuncio de Hola dado que el procesamiento no se ha realizado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="2d07e-172">Espere unos instantes y, a continuación, actualizar la vista en miniatura de hello índice página toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Página de índice](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="2d07e-174">Haga clic en **detalles** para la imagen a tamaño completo ad toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="2d07e-176">Ha ha estado ejecutando la aplicación hello por completo en el equipo local, sin nube toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="2d07e-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="2d07e-177">emulador de almacenamiento de Hello almacena cola hello y datos de blob en una base de datos de SQL Server Express LocalDB y aplicación hello almacenan los datos de ad de hello en otra base de datos de LocalDB.</span><span class="sxs-lookup"><span data-stu-id="2d07e-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="2d07e-178">Base de datos de Entity Framework Code First Hola creada automáticamente ad Hola primera vez hello web aplicación intentó tooaccess lo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="2d07e-179">Hola pasos de la sección configurará recursos de nube de Azure toouse Hola la solución para las colas, blobs y base de datos de aplicación Hola cuando se ejecuta en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="2d07e-180">Si deseara toocontinue toorun localmente, pero usar los recursos de almacenamiento y base de datos en la nube, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="2d07e-181">Es simplemente una cuestión de configuración de las cadenas de conexión, que podrá ver cómo toodo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="2d07e-182">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="2d07e-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="2d07e-183">Deberá llevar a cabo Hola tras la aplicación de hello toorun de pasos en la nube de hello:</span><span class="sxs-lookup"><span data-stu-id="2d07e-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="2d07e-184">Cree un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="2d07e-185">Cree una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="2d07e-186">Cree una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2d07e-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="2d07e-187">Configurar Hola solución toouse la base de datos de SQL Azure cuando se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="2d07e-188">Configurar Hola solución toouse su cuenta de almacenamiento de Azure cuando se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="2d07e-189">Implementar el servicio de nube de Azure de hello proyecto tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d07e-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="2d07e-190">Crear un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="2d07e-190">Create an Azure cloud service</span></span>
<span data-ttu-id="2d07e-191">Un servicio de nube de Azure es Hola entorno Hola aplicación se ejecutará en.</span><span class="sxs-lookup"><span data-stu-id="2d07e-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="2d07e-192">En el explorador, abra hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d07e-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2d07e-193">Haga clic en **Nuevo > Proceso > Servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="2d07e-194">En el cuadro de entrada de hello DNS nombre, escriba un prefijo de dirección URL para el servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="2d07e-195">Esta dirección URL tiene toobe único.</span><span class="sxs-lookup"><span data-stu-id="2d07e-195">This URL has toobe unique.</span></span>  <span data-ttu-id="2d07e-196">Obtendrá un mensaje de error si elige el prefijo de Hola ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="2d07e-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="2d07e-197">Especifique un nuevo grupo de recursos para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="2d07e-198">Haga clic en **crear nuevo** y, a continuación, escriba un nombre en hello recursos grupo cuadro de entrada, como CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="2d07e-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="2d07e-199">Elija la región de Hola donde desea que la aplicación de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2d07e-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="2d07e-200">Este campo especifica el centro de datos en el que se hospedará el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2d07e-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="2d07e-201">Para una aplicación de producción, elegiría a clientes más cercanos tooyour hello de la región.</span><span class="sxs-lookup"><span data-stu-id="2d07e-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="2d07e-202">Para este tutorial, elija tooyou de hello región más cercana.</span><span class="sxs-lookup"><span data-stu-id="2d07e-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="2d07e-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-203">Click **Create**.</span></span>

    <span data-ttu-id="2d07e-204">En Hola después de la imagen, se crea un servicio de nube con hello CSvccontosoads.cloudapp.net de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="2d07e-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="2d07e-206">Crear una base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="2d07e-206">Create an Azure SQL database</span></span>
<span data-ttu-id="2d07e-207">Cuando la aplicación hello se ejecuta en la nube de hello, usará una base de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="2d07e-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="2d07e-208">Hola [portal de Azure](https://portal.azure.com), haga clic en **nuevo > bases de datos > base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="2d07e-209">Hola **nombre de base de datos** cuadro, escriba *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="2d07e-210">Hola **grupo de recursos**, haga clic en **utilizar existente** y grupo de recursos de hello seleccione utilizado para servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="2d07e-211">Hola después de la imagen, haga clic en **Server: configurar los valores obligatorios** y **crear un nuevo servidor**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Servidor de túnel toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="2d07e-213">O bien, si su suscripción ya tiene un servidor, puede seleccionar que el servidor de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="2d07e-214">Hola **nombre del servidor** cuadro, escriba *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="2d07e-215">Complete los campos **Nombre de inicio de sesión** y **Contraseña** con los datos de un administrador.</span><span class="sxs-lookup"><span data-stu-id="2d07e-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="2d07e-216">Si seleccionó **Crear un servidor nuevo**, no escribirá aquí un nombre y una contraseña existentes.</span><span class="sxs-lookup"><span data-stu-id="2d07e-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="2d07e-217">Que se están escribiendo un nuevo nombre y una contraseña que está definiendo ahora toouse más adelante cuando tiene acceso a la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="2d07e-218">Si ha seleccionado un servidor que creó anteriormente, se le pedirá para que ya haya creado la cuenta de usuario administrativo Hola contraseña toohello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="2d07e-219">Elija Hola mismo **ubicación** que eligió para el servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="2d07e-220">Cuando Servicios de nube de Hola y base de datos están en distintos centros de datos (regiones diferentes), aumentará la latencia y le cobrará por el ancho de banda fuera Hola data center.</span><span class="sxs-lookup"><span data-stu-id="2d07e-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="2d07e-221">El ancho de banda del centro de datos es gratuito.</span><span class="sxs-lookup"><span data-stu-id="2d07e-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="2d07e-222">Comprobar **server tooaccess de permitir que los servicios de azure**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="2d07e-223">Haga clic en **seleccione** para nuevo servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-223">Click **Select** for hello new server.</span></span>

    ![Nuevo servidor de SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="2d07e-225">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="2d07e-226">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2d07e-226">Create an Azure storage account</span></span>
<span data-ttu-id="2d07e-227">Una cuenta de almacenamiento de Azure proporciona recursos para almacenar datos de cola y blob en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="2d07e-228">En una aplicación real, normalmente crearía cuentas independientes para los datos de aplicación frente a los datos de registro, y cuentas diferentes para datos de prueba frente a datos de producción.</span><span class="sxs-lookup"><span data-stu-id="2d07e-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="2d07e-229">En este tutorial, usará solamente una cuenta.</span><span class="sxs-lookup"><span data-stu-id="2d07e-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="2d07e-230">Hola [portal de Azure](https://portal.azure.com), haga clic en **nuevo > almacenamiento > cuenta de almacenamiento: blob, archivo, tabla, cola**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="2d07e-231">Hola **nombre** cuadro, escriba un prefijo de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="2d07e-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="2d07e-232">Este texto de prefijo más Hola que se observan en el cuadro de hello será la cuenta de almacenamiento de dirección URL única de Hola tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d07e-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="2d07e-233">Si ya se ha utilizado el prefijo de Hola que escriba por otra persona, tendrá que toochoose es un prefijo diferente.</span><span class="sxs-lookup"><span data-stu-id="2d07e-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="2d07e-234">Conjunto hello **modelo de implementación** demasiado*clásico*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="2d07e-235">Conjunto hello **replicación** lista desplegable lista demasiado**almacenamiento con redundancia local**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="2d07e-236">Cuando la replicación geográfica está habilitada para una cuenta de almacenamiento, contenido de Hola almacenado está replicada tooa centro de datos secundario tooenable conmutación por error si se produce un desastre importante en la ubicación principal Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="2d07e-237">La replicación geográfica puede suponer costes adicionales.</span><span class="sxs-lookup"><span data-stu-id="2d07e-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="2d07e-238">Para las cuentas de prueba y desarrollo, generalmente no desea toopay para la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="2d07e-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="2d07e-239">Para obtener más información, consulte [Creación, administración o eliminación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="2d07e-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="2d07e-240">Hola **grupo de recursos**, haga clic en **utilizar existente** y grupo de recursos de hello seleccione utilizado para servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="2d07e-241">Conjunto hello **ubicación** toohello de lista desplegable misma región que eligió para el servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="2d07e-242">Cuando se encuentran cuenta de almacenamiento y el servicio de nube de hello en distintos centros de datos (regiones diferentes), aumentará la latencia y le cobrará por el ancho de banda fuera Hola data center.</span><span class="sxs-lookup"><span data-stu-id="2d07e-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="2d07e-243">El ancho de banda del centro de datos es gratuito.</span><span class="sxs-lookup"><span data-stu-id="2d07e-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="2d07e-244">Grupos de afinidad de Azure proporcionan una distancia de hello mecanismo toominimize entre los recursos en un centro de datos, lo que puede reducir la latencia.</span><span class="sxs-lookup"><span data-stu-id="2d07e-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="2d07e-245">Este tutorial no usa grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="2d07e-246">Para obtener más información, consulte [cómo tooCreate una afinidad de grupo en Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d07e-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="2d07e-247">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-247">Click **Create**.</span></span>

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="2d07e-249">En la imagen de hello, se crea una cuenta de almacenamiento con la dirección URL de hello `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="2d07e-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="2d07e-250">Configurar la base de datos de SQL Azure de hello solución toouse cuando se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="2d07e-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="2d07e-251">Hola proyecto web y proyecto de rol de trabajo cada hello tiene su propia cadena de conexión de base de datos y es necesario que cada base de datos de SQL Azure de toopoint toohello cuando la aplicación hello se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="2d07e-252">Usará un [transformación de Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) para el rol web de hello y una configuración de entorno de servicio de nube para rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="2d07e-253">En esta sección y la sección siguiente de hello, almacenar credenciales en archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="2d07e-254">[No almacene información confidencial en repositorios de código fuente público.](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)</span><span class="sxs-lookup"><span data-stu-id="2d07e-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="2d07e-255">En el proyecto de ContosoAdsWeb hello, abra hello *Web.Release.config* archivo de transformación para la aplicación hello *Web.config* de archivos, elimine el bloque de comentario de Hola que contiene un `<connectionStrings>` elemento y pegar Hola siguiente código en su lugar.</span><span class="sxs-lookup"><span data-stu-id="2d07e-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="2d07e-256">Deje el archivo hello abierta para su edición.</span><span class="sxs-lookup"><span data-stu-id="2d07e-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="2d07e-257">Hola [portal de Azure](https://portal.azure.com), haga clic en **bases de datos SQL** en el panel izquierdo de hello, haga clic en la base de datos de Hola que creó para este tutorial y, a continuación, haga clic en **mostrar cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Mostrar cadenas de conexión](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="2d07e-259">portal de Hello muestra las cadenas de conexión, con un marcador de posición para contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Cadenas de conexión](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="2d07e-261">Hola *Web.Release.config* transformar el archivo, elimine `{connectionstring}` y pegar en su cadena de conexión de ADO.NET de hello portal de Azure Hola de contexto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="2d07e-262">En cadena de conexión de Hola que pegó en hello *Web.Release.config* transformar el archivo, reemplace `{your_password_here}` con contraseña de Hola que creó para la base de datos SQL nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="2d07e-263">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-263">Save hello file.</span></span>  
6. <span data-ttu-id="2d07e-264">Seleccione y copie la cadena de conexión de hello (sin Hola que rodean las comillas) para su uso en hello siguiendo los pasos para configurar el proyecto de rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="2d07e-265">En **el Explorador de soluciones**, en **Roles** en el proyecto de servicio de nube de hello, haga clic en **ContosoAdsWorker** y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="2d07e-267">Haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="2d07e-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="2d07e-268">Cambio **configuración del servicio** demasiado**nube**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="2d07e-269">Seleccione hello **valor** field para hello `ContosoAdsDbConnectionString` establecer y, a continuación, pegue la cadena de conexión de Hola que copió de la sección anterior de Hola de tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="2d07e-271">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="2d07e-272">Configurar la cuenta de almacenamiento de Azure de hello solución toouse cuando se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="2d07e-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="2d07e-273">Cadenas de conexión de cuenta de almacenamiento de Azure para proyecto de rol web de Hola y proyecto de rol de trabajo de Hola se almacenan en la configuración del entorno en el proyecto de servicio de nube Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="2d07e-274">Para cada proyecto, hay un conjunto independiente de toobe de configuración que se usa cuando la aplicación hello se ejecuta localmente y cuando se ejecuta en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="2d07e-275">Se actualizará la configuración del entorno de nube de Hola para proyectos de rol web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="2d07e-276">En **el Explorador de soluciones**, haga clic en **ContosoAdsWeb** en **Roles** en hello **ContosoAdsCloudService** del proyecto y, a continuación, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="2d07e-278">Haga clic en hello **configuración** ficha. Hola **configuración del servicio** desplegable cuadro, elija **nube**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="2d07e-280">Seleccione hello **StorageConnectionString** entrada y verá un botón de puntos suspensivos (**...** ) situado en el extremo derecho de Hola de línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="2d07e-281">Haga clic en Hola Hola de tooopen de botón de puntos suspensivos **crear la cadena de conexión de la cuenta de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="2d07e-283">Hola **crear cadenas de conexión de almacenamiento** cuadro de diálogo, haga clic en **su suscripción**, elija la cuenta de almacenamiento de Hola que creó anteriormente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="2d07e-284">Si no ha iniciado sesión, se le pedirán las credenciales de la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="2d07e-286">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-286">Save your changes.</span></span>
6. <span data-ttu-id="2d07e-287">Seguimiento Hola mismo procedimiento que utilizó para hello `StorageConnectionString` Hola de tooset de cadena de conexión `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="2d07e-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="2d07e-288">Esta cadena de conexión se usa para registro.</span><span class="sxs-lookup"><span data-stu-id="2d07e-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="2d07e-289">Seguimiento Hola mismo procedimiento que utilizó para hello **ContosoAdsWeb** tooset rol ambas cadenas de conexión para hello **ContosoAdsWorker** rol.</span><span class="sxs-lookup"><span data-stu-id="2d07e-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="2d07e-290">No olvide tooset **configuración del servicio** demasiado**nube**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="2d07e-291">configuración del entorno de rol de Hola que ha configurado en hello interfaz de usuario de Visual Studio se almacena en hello siguientes archivos de proyecto de hello ContosoAdsCloudService:</span><span class="sxs-lookup"><span data-stu-id="2d07e-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="2d07e-292">*ServiceDefinition.csdef* -define los nombres de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="2d07e-293">*ServiceConfiguration.Cloud.cscfg* -proporciona valores para cuando se ejecuta la aplicación hello en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="2d07e-294">*ServiceConfiguration.Local.cscfg* -proporciona valores para la aplicación hello ejecución localmente.</span><span class="sxs-lookup"><span data-stu-id="2d07e-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="2d07e-295">Por ejemplo, hello ServiceDefinition.csdef incluye Hola siguientes definiciones:</span><span class="sxs-lookup"><span data-stu-id="2d07e-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="2d07e-296">Hello y *ServiceConfiguration.Cloud.cscfg* archivo incluye valores de hello que escribió para la configuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="2d07e-297">Hola `<Instances>` configuración especifica Hola número de máquinas virtuales que Azure ejecutará código de rol de trabajo de hello en.</span><span class="sxs-lookup"><span data-stu-id="2d07e-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="2d07e-298">Hola [pasos siguientes](#next-steps) sección incluye vínculos toomore información acerca de cómo escalar horizontalmente un servicio de nube</span><span class="sxs-lookup"><span data-stu-id="2d07e-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="2d07e-299">Implementar Hola proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="2d07e-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="2d07e-300">En **el Explorador de soluciones**, contextual hello **ContosoAdsCloudService** proyecto en la nube y, a continuación, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="2d07e-302">Hola **iniciar sesión en** paso de hello **publicar aplicación de Azure** asistente, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="2d07e-304">Hola **configuración** paso del Asistente de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="2d07e-306">Hola configuración predeterminada de hello **avanzadas** ficha son válidas para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d07e-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="2d07e-307">Para obtener información acerca de la ficha Opciones avanzadas de hello, consulte [Asistente para publicar aplicaciones de Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d07e-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="2d07e-308">Hola **resumen** paso a paso, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="2d07e-310">Hola **Azure Activity Log** ventana se abre en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="2d07e-311">Haga clic en detalles de implementación de hello flecha derecha icono tooexpand Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="2d07e-312">implementación de Hello puede tardar hasta too5 minutos o más toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2d07e-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="2d07e-314">Cuando el estado de implementación de hello finalice, haga clic en hello **dirección URL de la aplicación Web** aplicación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="2d07e-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="2d07e-315">Ahora puede probar aplicación hello por crear, ver y editar algunos de los anuncios, como lo hizo cuando se ejecuta la aplicación hello localmente.</span><span class="sxs-lookup"><span data-stu-id="2d07e-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="2d07e-316">Cuando termine de probar, eliminar o detener servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="2d07e-317">Incluso si no está utilizando el servicio de nube de hello, lo acumulados cargos porque se reservan recursos de máquina virtual para él.</span><span class="sxs-lookup"><span data-stu-id="2d07e-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="2d07e-318">Y si lo deja ejecutando, cualquiera que encuentre su dirección URL puede crear y ver anuncios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="2d07e-319">Hola [portal de Azure](https://portal.azure.com), vaya toohello **Introducción** pestaña para el servicio de nube y, a continuación, haga clic en hello **eliminar** situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="2d07e-320">Si solo desea tootemporarily impedir que otras personas tengan acceso a sitio hello, haga clic en **detener** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="2d07e-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="2d07e-321">En ese caso, seguirán aplicando costos tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="2d07e-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="2d07e-322">Puede seguir un Hola de toodelete procedimiento similar cuenta de almacenamiento y base de datos SQL cuando ya no los necesite.</span><span class="sxs-lookup"><span data-stu-id="2d07e-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="2d07e-323">Crear aplicación hello desde el principio</span><span class="sxs-lookup"><span data-stu-id="2d07e-323">Create hello application from scratch</span></span>
<span data-ttu-id="2d07e-324">Si ya ha descargado [aplicación hello completado](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), hágalo ahora.</span><span class="sxs-lookup"><span data-stu-id="2d07e-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="2d07e-325">Podrá copiar archivos de proyecto descargado de hello en nuevo proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="2d07e-326">Crear aplicación Contoso anuncios de Hola implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2d07e-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="2d07e-327">Crear una solución de Visual Studio para un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2d07e-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="2d07e-328">Actualizar y agregar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2d07e-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="2d07e-329">Establecer preferencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-329">Set project references.</span></span>
* <span data-ttu-id="2d07e-330">Configurar cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="2d07e-330">Configure connection strings.</span></span>
* <span data-ttu-id="2d07e-331">Agregar archivos de código.</span><span class="sxs-lookup"><span data-stu-id="2d07e-331">Add code files.</span></span>

<span data-ttu-id="2d07e-332">Después de crea la solución de hello, podrá revisar el código de hello que es único toocloud proyectos de servicio como blobs de Azure y colas.</span><span class="sxs-lookup"><span data-stu-id="2d07e-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="2d07e-333">Crear una solución de Visual Studio para un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="2d07e-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="2d07e-334">En Visual Studio, elija **nuevo proyecto** de hello **archivo** menú.</span><span class="sxs-lookup"><span data-stu-id="2d07e-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="2d07e-335">En panel izquierdo de Hola de hello **nuevo proyecto** cuadro de diálogo, expanda **Visual C#** y elija **nube** plantillas y, a continuación, elija hello **deserviciodenubedeAzure** plantilla.</span><span class="sxs-lookup"><span data-stu-id="2d07e-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="2d07e-336">Nombre de proyecto de Hola y solución ContosoAdsCloudService y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nuevo proyecto](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="2d07e-338">Hola **nuevo servicio de nube de Azure** diálogo cuadro, agregue un rol web y un rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="2d07e-339">Nombre de rol web de hello ContosoAdsWeb y el nombre de rol de trabajo de hello ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="2d07e-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="2d07e-340">(Utilice el icono de lápiz Hola de hello panel derecho toochange Hola nombres predeterminados de las funciones hello.)</span><span class="sxs-lookup"><span data-stu-id="2d07e-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="2d07e-342">Cuando vea hello **nuevo proyecto ASP.NET** cuadro de diálogo de rol web de hello, elija la plantilla MVC de hello y, a continuación, haga clic en **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Cambiar autenticación](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="2d07e-344">Hola **Cambiar autenticación** diálogo cuadro, elija **sin autenticación**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Sin autenticación](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="2d07e-346">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="2d07e-347">En **el Explorador de soluciones**, haga clic en la solución de hello (no de uno de los proyectos de hello) y elija **Add - nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="2d07e-348">Hola **Agregar nuevo proyecto** diálogo cuadro, elija **Windows** en **Visual C#** en Hola panel izquierdo y, a continuación, haga clic en hello **biblioteca de clases** plantilla.</span><span class="sxs-lookup"><span data-stu-id="2d07e-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="2d07e-349">Proyecto de hello Name *ContosoAdsCommon*y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="2d07e-350">Necesita tooreference Hola Entity Framework hello y contexto de modelo de datos de proyectos de rol web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="2d07e-351">Como alternativa, puede definir clases relacionadas con EF de hello en proyecto de rol web de Hola y hacer referencia a ese proyecto desde el proyecto de rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="2d07e-352">Pero en el enfoque alternativo de hello, su proyecto de rol de trabajo tendría un ensamblados de referencia de tooweb que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="2d07e-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="2d07e-353">Actualizar y agregar paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="2d07e-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="2d07e-354">Abra hello **administrar paquetes de NuGet** cuadro de diálogo de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="2d07e-355">Hola parte superior de ventana hello, seleccione **actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="2d07e-356">Busque hello *WindowsAzure.Storage* del paquete y si se encuentra en la lista de hello, selecciónela y seleccione tooupdate de proyectos web y de trabajo de hello en y, a continuación, haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="2d07e-357">biblioteca de cliente de almacenamiento de Hola se actualiza con más frecuencia que las plantillas de proyecto de Visual Studio, por lo que a menudo encontrará esa versión de hello en un toobe de necesidades de proyecto recién creado actualizado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="2d07e-358">Hola parte superior de ventana hello, seleccione **examinar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="2d07e-359">Buscar hello *EntityFramework* NuGet empaquetar e instalarlo en los tres proyectos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="2d07e-360">Buscar hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet empaquetar e instalarlo en el proyecto de rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="2d07e-361">Establecimiento de preferencias del proyecto</span><span class="sxs-lookup"><span data-stu-id="2d07e-361">Set project references</span></span>
1. <span data-ttu-id="2d07e-362">Hola ContosoAdsWeb proyecto, establecer una referencia de proyecto de ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="2d07e-363">Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **referencias** - **agregar referencias**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="2d07e-364">Hola **Administrador de referencias** cuadro de diálogo, seleccione **solución – proyectos** en hello panel izquierdo, seleccione **ContosoAdsCommon**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="2d07e-365">Hola ContosoAdsWorker proyecto, establecer una referencia de proyecto de ContosAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="2d07e-366">ContosoAdsCommon contendrá Hola datos modelo y el contexto de clase de Entity Framework, que se usará en ambos Hola front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="2d07e-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="2d07e-367">En proyectos de ContosoAdsWorker hello, establezca una referencia demasiado`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="2d07e-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="2d07e-368">Hola back-end tooconvert imágenes toothumbnails usa este ensamblado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="2d07e-369">Configurar cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="2d07e-369">Configure connection strings</span></span>
<span data-ttu-id="2d07e-370">En esta sección configurará Azure Storage y cadenas de conexión de SQL para pruebas locales.</span><span class="sxs-lookup"><span data-stu-id="2d07e-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="2d07e-371">instrucciones de implementación de Hello anteriormente en el tutorial de Hola explica cómo tooset conexión Hola cadenas para cuando hello aplicación se ejecuta en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="2d07e-372">Proyecto de ContosoAdsWeb de hello, archivo Web.config de la aplicación de hello abierto y siguiente de hello insert `connectionStrings` elemento después de hello `configSections` elemento.</span><span class="sxs-lookup"><span data-stu-id="2d07e-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="2d07e-373">Si va a usar Visual Studio 2015 o una versión superior, sustituya "v11.0" por "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="2d07e-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="2d07e-374">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-374">Save your changes.</span></span>
3. <span data-ttu-id="2d07e-375">En el proyecto de ContosoAdsCloudService hello, haga clic en ContosoAdsWeb en **Roles**y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="2d07e-377">Hola **ContosAdsWeb [rol]** ventana Propiedades, haga clic en hello **configuración** ficha y, a continuación, haga clic en **Agregar configuración**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="2d07e-378">Deje **configuración del servicio** establecido demasiado**todas las configuraciones de**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="2d07e-379">Agregue un nuevo valor llamado *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="2d07e-380">Establecer **tipo** demasiado*ConnectionString*y establezca **valor** demasiado*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="2d07e-382">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="2d07e-382">Save your changes.</span></span>
7. <span data-ttu-id="2d07e-383">Seguimiento Hola mismo tooadd procedimiento una cadena de conexión de almacenamiento de propiedades de la función ContosoAdsWorker Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="2d07e-384">Aún en hello **ContosoAdsWorker [rol]** ventana Propiedades, agregue otra cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="2d07e-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="2d07e-385">Nombre: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="2d07e-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="2d07e-386">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2d07e-386">Type: String</span></span>
   * <span data-ttu-id="2d07e-387">Valor: Pegar Hola misma cadena de conexión utilizada para el proyecto de rol web de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="2d07e-388">(el siguiente ejemplo de Hola es para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="2d07e-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="2d07e-389">No olvide toochange Hola origen de datos si se copia en este ejemplo y que está utilizando Visual Studio 2015 o superior.)</span><span class="sxs-lookup"><span data-stu-id="2d07e-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="2d07e-390">Agregar archivos de código</span><span class="sxs-lookup"><span data-stu-id="2d07e-390">Add code files</span></span>
<span data-ttu-id="2d07e-391">En esta sección, copie los archivos de código de solución de hello descargado en la nueva solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="2d07e-392">Hello las secciones siguientes se muestra y explica los elementos clave de este código.</span><span class="sxs-lookup"><span data-stu-id="2d07e-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="2d07e-393">tooadd archivos tooa proyecto o una carpeta, proyecto de Hola de menú contextual o carpeta y haga clic en **agregar** - **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="2d07e-394">Seleccione los archivos de Hola que desee y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="2d07e-395">Si se le pregunta si desea que tooreplace los archivos existentes, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="2d07e-396">En proyectos de ContosoAdsCommon hello, elimine hello *Class1.cs* de archivos y agregar en su lugar hello *Ad.cs* y *ContosoAdscontext.cs* archivos de hello descargan el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="2d07e-397">En proyecto de ContosoAdsWeb de hello, agregue Hola siguientes archivos de proyecto Hola descargado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="2d07e-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="2d07e-399">Hola *Views\Shared* carpeta:  *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="2d07e-400">Hola *Views\Home* carpeta: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="2d07e-401">Hola *controladores* carpeta: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="2d07e-402">Hola *Views\Ad* carpeta (crear carpeta de hello en primer lugar): cinco *.cshtml* archivos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="2d07e-403">En hello ContosoAdsWorker proyecto, agregue *WorkerRole.cs* de hello descargaste el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="2d07e-404">Ahora puede compilar y ejecutar la aplicación hello tal como se indica anteriormente en el tutorial de Hola y aplicación hello usará la base de datos local y los recursos de emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2d07e-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="2d07e-405">Hello las secciones siguientes explican el código de hello tooworking relacionado con Hola entorno de Azure, blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="2d07e-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="2d07e-406">Este tutorial no se explica cómo los controladores MVC toocreate y vistas mediante la técnica scaffolding, cómo toowrite código de Entity Framework que funciona con bases de datos de SQL Server o conceptos básicos de saludo de la programación asincrónica en ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="2d07e-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="2d07e-407">Para obtener información acerca de estos temas, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2d07e-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="2d07e-408">Introducción a MVC 5</span><span class="sxs-lookup"><span data-stu-id="2d07e-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="2d07e-409">Introducción a EF 6 y MVC 5</span><span class="sxs-lookup"><span data-stu-id="2d07e-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="2d07e-410">[Programación de tooasynchronous de introducción en .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="2d07e-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="2d07e-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="2d07e-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="2d07e-412">archivo de Hello Ad.cs define una enumeración de categorías de ad y una clase de entidad POCO para obtener información de ad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="2d07e-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="2d07e-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="2d07e-414">Hola ContosoAdsContext clase especifica que se utiliza la clase de Ad de hello en una colección de DbSet, que Entity Framework, se almacenará en una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2d07e-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="2d07e-415">clase Hello tiene dos constructores.</span><span class="sxs-lookup"><span data-stu-id="2d07e-415">hello class has two constructors.</span></span> <span data-ttu-id="2d07e-416">Hola primero de ellos participa en el proyecto web de Hola y especifica el nombre de Hola de una cadena de conexión que se almacena en el archivo Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="2d07e-417">segundo constructor de Hello permite toopass en la cadena de conexión real de hello utilizada por el proyecto de rol de trabajo de hello, puesto que no tiene un archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="2d07e-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="2d07e-418">Se ha visto anteriormente donde se almacenó esta cadena de conexión y podrá ver más adelante cómo código de hello recupera la cadena de conexión de hello cuando crea una instancia de clase de DbContext Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="2d07e-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="2d07e-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="2d07e-420">Código que se llama desde hello `Application_Start` método crea un *imágenes* contenedor de blobs y una *imágenes* cola si todavía no existen.</span><span class="sxs-lookup"><span data-stu-id="2d07e-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="2d07e-421">Esto garantiza que cada vez que empiece a usar una cuenta de almacenamiento, o empezar a usar el emulador de almacenamiento de hello en un equipo nuevo, cola y el contenedor de blobs necesarios Hola se creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2d07e-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="2d07e-422">Hola cuenta de almacenamiento de toohello de código obtiene acceso mediante el uso de la cadena de conexión de almacenamiento de Hola de hello *.cscfg* archivo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="2d07e-423">A continuación, obtiene una referencia toohello *imágenes* contenedor de blobs, crea el contenedor de hello si aún no existe, y establece permisos en el nuevo contenedor de Hola de acceso.</span><span class="sxs-lookup"><span data-stu-id="2d07e-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="2d07e-424">De forma predeterminada, nuevos contenedores solo permiten a los clientes con la cuenta de almacenamiento de blobs de tooaccess de credenciales.</span><span class="sxs-lookup"><span data-stu-id="2d07e-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="2d07e-425">sitio Web de Hello necesita Hola blobs toobe público para que pueden mostrar imágenes con direcciones URL que blobs de imagen toohello de punto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="2d07e-426">Un código similar Obtiene una referencia toohello *imágenes* poner en cola y crea una nueva cola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="2d07e-427">En este caso no es necesario cambios de permiso.</span><span class="sxs-lookup"><span data-stu-id="2d07e-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="2d07e-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="2d07e-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="2d07e-429">Hola *_Layout.cshtml* archivo establece el nombre de la aplicación hello en hello encabezado y pie y crea una entrada de menú "Anuncios".</span><span class="sxs-lookup"><span data-stu-id="2d07e-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="2d07e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="2d07e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="2d07e-431">Hola *Views\Home\Index.cshtml* archivo muestra los vínculos de categoría en la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="2d07e-432">vínculos de Hello pasan el valor entero Hola Hola `Category` enumeración en una página de índice de anuncios de toohello variable de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="2d07e-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="2d07e-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="2d07e-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="2d07e-434">Hola *AdController.cs* archivo, llamadas de constructor Hola Hola `InitializeStorage` objetos de biblioteca de cliente de almacenamiento de Azure de toocreate del método que proporcionan una API para trabajar con blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="2d07e-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="2d07e-435">A continuación, el código de hello Obtiene una referencia toohello *imágenes* contenedor de blob como vimos anteriormente en *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d07e-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="2d07e-436">Mientras hace eso, establece una [directiva de reintentos](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) apropiada para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2d07e-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="2d07e-437">Directiva de reintentos de retroceso exponencial de Hello predeterminada podría dejar de responder hello web app para más de un minuto en varios intentos para un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="2d07e-438">Directiva de reintentos de Hello especificada aquí espera tres segundos después de cada uno de ellos probar para una toothree intentos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="2d07e-439">Un código similar Obtiene una referencia toohello *imágenes* cola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="2d07e-440">La mayoría del código de controlador de hello es típico para trabajar con un modelo de datos de Entity Framework mediante una clase DbContext.</span><span class="sxs-lookup"><span data-stu-id="2d07e-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="2d07e-441">Una excepción es hello HttpPost `Create` método, que carga un archivo y lo guarda en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2d07e-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="2d07e-442">enlazador de modelos de Hello proporciona un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método del objeto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="2d07e-443">Si el usuario de hello seleccionó un tooupload de archivo, código de hello carga el archivo hello, lo guarda en un blob y actualiza el registro de base de datos de Ad de hello con una dirección URL que señala toohello blob.</span><span class="sxs-lookup"><span data-stu-id="2d07e-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="2d07e-444">Hello código Hola carga es Hola `UploadAndSaveBlobAsync` método.</span><span class="sxs-lookup"><span data-stu-id="2d07e-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="2d07e-445">Crea un nombre GUID para el blob de hello, cargas y archivo de hello guarda y devuelve un blob de referencia toohello guardado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="2d07e-446">Después de hello HttpPost `Create` método carga un blob y Hola de las actualizaciones de base de datos, crea un tooinform de mensaje de cola ese proceso de back-end que está lista para la vista en miniatura de conversión tooa una imagen.</span><span class="sxs-lookup"><span data-stu-id="2d07e-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="2d07e-447">Hola código de hello HttpPost `Edit` método es similar, salvo que si el usuario de hello selecciona un nuevo archivo de imagen deben eliminarse los blobs que ya existen.</span><span class="sxs-lookup"><span data-stu-id="2d07e-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="2d07e-448">el ejemplo siguiente se Hello muestra código de hello blobs se elimina cuando se elimina un anuncio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="2d07e-449">ContosoAdsWeb - Views\Ad\Index.cshtml y Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="2d07e-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="2d07e-450">Hola *Index.cshtml* archivo muestra vistas en miniatura con hello otros datos de ad.</span><span class="sxs-lookup"><span data-stu-id="2d07e-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="2d07e-451">Hola *Details.cshtml* archivo muestra la imagen a tamaño completo Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="2d07e-452">ContosoAdsWeb - Views\Ad\Create.cshtml y Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="2d07e-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="2d07e-453">Hola *Create.cshtml* y *Edit.cshtml* archivos especifican formulario codificación que permite Hola Hola de controlador tooget `HttpPostedFileBase` objeto.</span><span class="sxs-lookup"><span data-stu-id="2d07e-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="2d07e-454">Un `<input>` elemento indica Hola explorador tooprovide un cuadro de diálogo de selección de archivo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="2d07e-455">ContosoAdsWorker - WorkerRole.cs - Método OnStart</span><span class="sxs-lookup"><span data-stu-id="2d07e-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="2d07e-456">entorno de rol de trabajador de Azure de Hello llama hello `OnStart` método Hola `WorkerRole` clase al rol de trabajo de hello es introducción y llama hello `Run` método cuando hello `OnStart` método finaliza.</span><span class="sxs-lookup"><span data-stu-id="2d07e-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="2d07e-457">Hola `OnStart` método obtiene la cadena de conexión de base de datos de Hola de hello *.cscfg* archivo y lo pasa en la clase de Entity Framework DbContext toohello.</span><span class="sxs-lookup"><span data-stu-id="2d07e-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="2d07e-458">proveedor de SQLClient Hola se utiliza de forma predeterminada, por lo que el proveedor hello no tiene toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="2d07e-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="2d07e-459">Después de eso, método hello Obtiene una cuenta de almacenamiento de toohello de referencia y crea la cola y el contenedor de blobs de hello si no existen.</span><span class="sxs-lookup"><span data-stu-id="2d07e-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="2d07e-460">código de Hello para el que es toowhat similar ya vio en el rol web de hello `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="2d07e-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="2d07e-461">ContosoAdsWorker - WorkerRole.cs - Método Run</span><span class="sxs-lookup"><span data-stu-id="2d07e-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="2d07e-462">Hola `Run` método se llama cuando hello `OnStart` método finaliza su tarea de inicialización.</span><span class="sxs-lookup"><span data-stu-id="2d07e-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="2d07e-463">método Hello ejecuta un bucle infinito que inspecciona los nuevos mensajes de cola y procesa cuando vayan llegando.</span><span class="sxs-lookup"><span data-stu-id="2d07e-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="2d07e-464">Después de cada iteración del bucle de hello, si se encuentra ningún mensaje de cola, programa hello en suspensión durante un segundo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="2d07e-465">Esto impide que el rol de trabajo de hello incurrir en costes excesivos de la transacción del almacenamiento y tiempo de CPU.</span><span class="sxs-lookup"><span data-stu-id="2d07e-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="2d07e-466">Hola, equipo de asesoramiento al cliente de Microsoft cuente una historia acerca de un desarrollador que se haya olvidado tooinclude, implementado tooproduction y deja de vacaciones.</span><span class="sxs-lookup"><span data-stu-id="2d07e-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="2d07e-467">Al que obtuvo, su supervisión son más caras que las vacaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="2d07e-468">A veces contenido Hola de un mensaje de la cola provoca un error en el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="2d07e-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="2d07e-469">Esto se denomina una *mensaje dudoso*, y si simplemente se registra un error y reiniciar bucle hello, interminablemente intente tooprocess ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="2d07e-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="2d07e-470">Por lo tanto, el bloque catch de hello incluye if instrucción que comprueba toosee cuántas veces aplicación hello probada tooprocess Hola mensaje actual y si han pasado más de 5 veces, mensaje de saludo se elimina de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="2d07e-471">`ProcessQueueMessage` se llama cuando se encuentra un mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="2d07e-472">Este código lee la dirección URL de imagen de hello base de datos tooget hello, convierte la miniatura de la imagen tooa hello, guarda la miniatura de hello en un blob, actualiza la base de datos de hello con la dirección URL del blob en miniatura de Hola y elimina el mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="2d07e-473">Hola código de hello `ConvertImageToThumbnailJPG` método usa las clases en el espacio de nombres de hello System.Drawing para simplificar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d07e-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="2d07e-474">Sin embargo, las clases de hello en este espacio de nombres se diseñaron para su uso con Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="2d07e-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="2d07e-475">No se admiten para usarse en un servicio de Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d07e-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="2d07e-476">Para más información acerca de las opciones de procesamiento de imagen, consulte [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Generación de imagen dinámica) y [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Profundización en el cambio de tamaño de imágenes).</span><span class="sxs-lookup"><span data-stu-id="2d07e-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="2d07e-477">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="2d07e-477">Troubleshooting</span></span>
<span data-ttu-id="2d07e-478">En caso de que algo no funciona mientras que siga las instrucciones de hello en este tutorial, aquí se muestran algunos errores comunes y cómo tooresolve ellos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="2d07e-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="2d07e-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="2d07e-480">Hola `RoleEnvironment` objeto proporciona Azure cuando se ejecuta una aplicación en Azure o cuando se ejecuta localmente mediante Hola emulador de proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="2d07e-481">Si recibe este error cuando se ejecuta localmente, asegúrese de que haya establecido como proyecto de inicio de hello proyecto ContosoAdsCloudService de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="2d07e-482">Esta acción configura Hola proyecto toorun mediante Hola emulador de proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="2d07e-483">Uno de los aspectos de Hola Hola aplicación usa Hola RoleEnvironment de Azure para es tooget valores de cadena de conexión de Hola que se almacenan en hello *.cscfg* archivos, por lo que otra causa de esta excepción es una cadena de conexión que faltan.</span><span class="sxs-lookup"><span data-stu-id="2d07e-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="2d07e-484">Asegúrese de que ha creado configuración StorageConnectionString de Hola para tanto en la nube y las configuraciones locales en hello ContosoAdsWeb proyecto y había creado ambas cadenas de conexión para ambas configuraciones en el proyecto de ContosoAdsWorker Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="2d07e-485">Si lo hace un **buscar todos** búsqueda para StorageConnectionString en toda la solución hello, que debería verla 9 veces en 6 archivos.</span><span class="sxs-lookup"><span data-stu-id="2d07e-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="2d07e-486">No se puede reemplazar tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="2d07e-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="2d07e-487">El nuevo puerto está por debajo del valor mínimo permitido de 8080 para el protocolo http.</span><span class="sxs-lookup"><span data-stu-id="2d07e-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="2d07e-488">Intente cambiar el número de puerto de hello usa Hola proyecto de web.</span><span class="sxs-lookup"><span data-stu-id="2d07e-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="2d07e-489">Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="2d07e-490">Haga clic en hello **Web** ficha y, a continuación, cambie el número de puerto de hello en hello **dirección Url del proyecto** configuración.</span><span class="sxs-lookup"><span data-stu-id="2d07e-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="2d07e-491">Para otra alternativa que se resuelva el problema de hello, vea Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="2d07e-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="2d07e-492">Otros errores al realizar la ejecución localmente</span><span class="sxs-lookup"><span data-stu-id="2d07e-492">Other errors when running locally</span></span>
<span data-ttu-id="2d07e-493">En la nube predeterminado nuevo proyectos de servicio usan Hola de toosimulate express de emulador de proceso de Azure de hello entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d07e-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="2d07e-494">Se trata de una versión ligera de emulador de proceso completo de hello y, en algunos Hola condiciones emulador completo funcionará cuando versión express de hello no lo hace.</span><span class="sxs-lookup"><span data-stu-id="2d07e-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="2d07e-495">toochange Hola emulador completo de proyecto toouse hello, haga clic en proyecto de hello ContosoAdsCloudService y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2d07e-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="2d07e-496">Hola **propiedades** ventana, haga clic en hello **Web** ficha y, a continuación, haga clic en hello **usar emulador completo** botón de radio.</span><span class="sxs-lookup"><span data-stu-id="2d07e-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="2d07e-497">En la aplicación Hola de toorun de pedidos con el emulador completo de hello, tiene tooopen Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="2d07e-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d07e-498">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d07e-498">Next steps</span></span>
<span data-ttu-id="2d07e-499">aplicación Contoso anuncios de Hola se intencionadamente ha conservado simple para obtener un tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="2d07e-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="2d07e-500">Por ejemplo, no implementa [inyección de dependencia](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o hello [repositorio y una unidad de trabajan patrones](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), pero no ocurre así [usar una interfaz para el registro](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), no usa [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) datos toomanage cambios en el modelo o [resistencia de conexión de EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transitorio errores de red y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="2d07e-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="2d07e-501">A continuación, incluimos algunas aplicaciones de ejemplo de servicio de nube que muestran más prácticas de codificación de mundo real, enumeradas de menos complejo toomore complejo:</span><span class="sxs-lookup"><span data-stu-id="2d07e-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="2d07e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="2d07e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="2d07e-503">Un concepto similar tooContoso anuncios pero implementa más características y prácticas de codificación más reales.</span><span class="sxs-lookup"><span data-stu-id="2d07e-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="2d07e-504">[Aplicación de niveles múltiples de servicios en la nube de Azure con Tablas, Colas y Blobs.](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)Presenta las tablas de Almacenamiento de Azure, así como blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="2d07e-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="2d07e-505">Basadas en una versión anterior del SDK de Azure para.</span><span class="sxs-lookup"><span data-stu-id="2d07e-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="2d07e-506">Se basa en una versión anterior de hello Azure SDK para. NET, requerirá algunos toowork modificaciones con la versión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="2d07e-507">[Fundamentos de servicios en la nube en Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="2d07e-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="2d07e-508">Un ejemplo completo que muestra una amplia gama de procedimientos recomendados, generado por el grupo de Microsoft Patterns and Practices de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d07e-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="2d07e-509">Para obtener información general sobre el desarrollo de la nube de hello, consulte [creación de aplicaciones de nube reales con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="2d07e-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="2d07e-510">Para un almacenamiento de vídeo de introducción tooAzure procedimientos recomendados y patrones, vea [almacenamiento de Microsoft Azure: ¿qué es nuevo, prácticas recomendadas y patrones](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="2d07e-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="2d07e-511">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2d07e-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="2d07e-512">Servicios de nube de Azure, parte 1: Introducción</span><span class="sxs-lookup"><span data-stu-id="2d07e-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="2d07e-513">Cómo toomanage los servicios de nube</span><span class="sxs-lookup"><span data-stu-id="2d07e-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="2d07e-514">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2d07e-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="2d07e-515">¿Cómo toochoose una nube de proveedor de servicios</span><span class="sxs-lookup"><span data-stu-id="2d07e-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
