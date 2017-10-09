---
title: "aaaCreate NET WebJob en el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Cree una aplicación de varios niveles utilizando ASP.NET MVC y Azure. Hola front-end ejecuta en una aplicación web en el servicio de aplicación de Azure y Hola back-end se ejecuta como un trabajo Web. aplicación Hello usa Entity Framework, base de datos de SQL y las colas de almacenamiento de Azure y blobs."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="d3916-105">Creación de un WebJob .NET en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d3916-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="d3916-106">Este tutorial muestra cómo toowrite código para una aplicación de ASP.NET MVC 5 multinivel simple que usa hello [SDK de WebJobs](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d3916-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="d3916-107">Hola propósito de hello [SDK de WebJobs](websites-webjobs-resources.md) es código de hello toosimplify que se escribe para las tareas comunes que puede realizar un trabajo Web, como procesamiento de imágenes, procesamiento de colas, agregación de RSS, mantenimiento del archivo y enviar mensajes de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d3916-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="d3916-108">Hola SDK de WebJobs tiene características integradas para trabajar con el almacenamiento de Azure y Bus de servicio, para programar tareas y control de errores y para muchos otros escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="d3916-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="d3916-109">Además, ha diseñado toobe extensible y no hay un [repositorio de código abierto para las extensiones](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="d3916-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="d3916-110">aplicación de ejemplo de Hola es un tablón de anuncios publicitarios.</span><span class="sxs-lookup"><span data-stu-id="d3916-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="d3916-111">Los usuarios pueden cargar imágenes para anuncios y un proceso de back-end convierte Hola imágenes toothumbnails.</span><span class="sxs-lookup"><span data-stu-id="d3916-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="d3916-112">página de lista de anuncios de Hola muestra vistas en miniatura de Hola y página de detalles del anuncio de Hola muestra la imagen a tamaño completo Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="d3916-113">A continuación se muestra una captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="d3916-113">Here's a screenshot:</span></span>

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="d3916-115">Esta aplicación de ejemplo funciona con [colas de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) y [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="d3916-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="d3916-116">Hello tutorial le mostrará cómo toodeploy Hola aplicación demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) y [base de datos de SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="d3916-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="d3916-117"><a id="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d3916-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="d3916-118">Hello tutorial se supone que ya sabe cómo toowork con [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) proyectos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3916-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="d3916-119">tutorial de Hello escribió originalmente para Visual Studio 2013, pero puede utilizarse con las versiones posteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3916-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="d3916-120">Si está utilizando Visual Studio 2015 o 2017, tome nota antes de ejecutar la aplicación hello localmente, debe cambiar hello `Data Source` forma parte de la cadena de conexión de SQL Server LocalDB hello en los archivos Web.config y App.config Hola de `Data Source=(localdb)\v11.0` demasiado`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="d3916-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="d3916-121"><a name="note"></a>Debe tener una cuenta de Azure toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="d3916-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="d3916-122">También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): obtenga créditos que puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan, puede mantener la cuenta de hello y usar los servicios de Azure gratuitos, como sitios Web.</span><span class="sxs-lookup"><span data-stu-id="d3916-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="d3916-123">Nunca se cargará su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.</span><span class="sxs-lookup"><span data-stu-id="d3916-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="d3916-124">Puede [activar Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): su suscripción le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="d3916-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="d3916-125">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d3916-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d3916-126">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d3916-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="d3916-127"><a id="learn"></a>Temas que se abordarán</span><span class="sxs-lookup"><span data-stu-id="d3916-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="d3916-128">Hola tutorial le muestra cómo hello toodo siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d3916-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="d3916-129">Habilitar el equipo de desarrollo de Azure mediante la instalación de hello Azure SDK (solo para usuarios de 2015 y Visual Studio 2013).</span><span class="sxs-lookup"><span data-stu-id="d3916-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="d3916-130">Cree un proyecto de aplicación de consola que se implementa automáticamente como un trabajo Web de Azure al implementar un proyecto web asociado Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="d3916-131">Probar un back-end de SDK de WebJobs localmente en el equipo de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="d3916-132">Publicar una aplicación con una aplicación web de trabajos Web back-end tooa en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d3916-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="d3916-133">Cargar archivos y almacenarlos en hello servicio Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="d3916-134">Usar hello toowork de SDK de WebJobs de Azure con blobs y colas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="d3916-135"><a id="contosoads"></a>Arquitectura de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d3916-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="d3916-136">aplicación de ejemplo de Hola utiliza hello [centrada en la cola de trabajo patrón](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga de trabajo de hello intensiva de CPU de creación de proceso de miniaturas tooa back-end.</span><span class="sxs-lookup"><span data-stu-id="d3916-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="d3916-137">aplicación Hello almacena anuncios en una base de datos SQL con tablas de hello toocreate Entity Framework Code First y acceder a los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="d3916-138">Para cada anuncio de la base de datos de hello almacena dos direcciones URL: uno para la imagen a tamaño completo hello y otro para la miniatura de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="d3916-140">Cuando un usuario carga una imagen, la aplicación web de hello almacena la imagen de hello en un [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), y almacena información de anuncios de Hola en base de datos de hello con una dirección URL que señala toohello blob.</span><span class="sxs-lookup"><span data-stu-id="d3916-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="d3916-141">Hola al mismo tiempo, escribe un tooan mensaje cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="d3916-142">En un proceso de back-end que se ejecuta como un trabajo Web de Azure, SDK de WebJobs Hola sondea Hola si hay mensajes nuevos.</span><span class="sxs-lookup"><span data-stu-id="d3916-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="d3916-143">Cuando aparezca un mensaje nuevo, Hola trabajo Web crea una vista en miniatura de esa imagen y actualizaciones Hola campo de base de datos de dirección URL en miniatura para que ad.</span><span class="sxs-lookup"><span data-stu-id="d3916-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="d3916-144">Éste es un diagrama que muestra cómo interactúan las partes de Hola de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="d3916-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="d3916-146">instrucciones del tutorial Hola aplican tooAzure SDK para .NET 2.7.1 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="d3916-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="d3916-147"><a id="storage"></a>Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d3916-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="d3916-148">Una cuenta de almacenamiento de Azure proporciona recursos para almacenar datos de cola y blob en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="d3916-149">También se usa por hello datos de registro de toostore de SDK de WebJobs para el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="d3916-150">En una aplicación real, normalmente crea cuentas independientes para los datos de aplicación frente a los datos de registro, y cuentas diferentes para los datos de prueba frente a los datos de producción.</span><span class="sxs-lookup"><span data-stu-id="d3916-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="d3916-151">En este tutorial, usará solamente una cuenta.</span><span class="sxs-lookup"><span data-stu-id="d3916-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="d3916-152">Abra hello **Explorador de servidores** ventana de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3916-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="d3916-153">Menú contextual hello **Azure** nodo y, a continuación, haga clic en **conectar tooMicrosoft suscripción de Azure...** .</span><span class="sxs-lookup"><span data-stu-id="d3916-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Conectar tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="d3916-155">Inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="d3916-156">Haga clic en **almacenamiento** en Hola nodos de Azure y, a continuación, haga clic en **crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="d3916-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Crear cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="d3916-158">Hola **crear cuenta de almacenamiento** cuadro de diálogo, escriba un nombre para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="d3916-159">debe ser el nombre de Hello debe ser único (ninguna otra cuenta de almacenamiento de Azure puede tener Hola mismo nombre).</span><span class="sxs-lookup"><span data-stu-id="d3916-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="d3916-160">Si nombre hello especificado ya está en uso, obtendrá un toochange posibilidad.</span><span class="sxs-lookup"><span data-stu-id="d3916-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="d3916-161">Hola tooaccess de dirección URL será la cuenta de almacenamiento *{name}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d3916-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="d3916-162">Conjunto hello **región o grupo de afinidad** tooyou de lista desplegable toohello región más cercana.</span><span class="sxs-lookup"><span data-stu-id="d3916-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="d3916-163">Esta configuración especifica el centro de datos de Azure que va a almacenar la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3916-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="d3916-164">En este tutorial, la opción que elija no tendrá mucha repercusión.</span><span class="sxs-lookup"><span data-stu-id="d3916-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="d3916-165">Sin embargo, para una aplicación web de producción, desea que el servidor web y la toobe de la cuenta de almacenamiento en hello mismo latencia toominimize de región y datos cargos de salida.</span><span class="sxs-lookup"><span data-stu-id="d3916-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="d3916-166">aplicación web de Hello (que creará más adelante) Centro de datos debe ser lo más parecida posibles exploradores toohello acceso a aplicación web de hello en la latencia de toominimize de orden.</span><span class="sxs-lookup"><span data-stu-id="d3916-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="d3916-167">Conjunto hello **replicación** lista desplegable lista demasiado**redundancia local**.</span><span class="sxs-lookup"><span data-stu-id="d3916-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="d3916-168">Replicación geográfica está habilitada para una cuenta de almacenamiento, contenido de hello almacenado replicada tooa centro de datos secundario tooenable conmutación por error toothat ubicación es en el caso de un desastre importante en la ubicación principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="d3916-169">La replicación geográfica puede suponer costes adicionales.</span><span class="sxs-lookup"><span data-stu-id="d3916-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="d3916-170">Para las cuentas de prueba y desarrollo, generalmente no desea toopay para la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="d3916-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="d3916-171">Para obtener más información, consulte [Creación, administración o eliminación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d3916-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="d3916-172">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d3916-172">Click **Create**.</span></span>

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="d3916-174"><a id="download"></a>Descargar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="d3916-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="d3916-175">Descargue y descomprima hello [completado solución](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="d3916-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="d3916-176">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3916-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="d3916-177">De hello **archivo** menú elija **Abrir > proyecto/solución**, desplácese toowhere descargó solución hello y, a continuación, abra el archivo de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="d3916-178">Presione la solución CTRL + MAYÚS + B toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="d3916-179">De forma predeterminada, Visual Studio restaurará automáticamente contenido del paquete NuGet hello, que no se incluyó en hello *.zip* archivo.</span><span class="sxs-lookup"><span data-stu-id="d3916-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="d3916-180">Si no se restauran los paquetes de saludo, instálelos manualmente va toohello **administrar paquetes de NuGet para la solución** cuadro de diálogo y haga clic en hello **restaurar** situado en la parte superior de hello derecha.</span><span class="sxs-lookup"><span data-stu-id="d3916-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="d3916-181">En **el Explorador de soluciones**, asegúrese de que **ContosoAdsWeb** está seleccionado como proyecto de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="d3916-182"><a id="configurestorage"></a>Configurar la cuenta de almacenamiento de toouse de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d3916-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="d3916-183">Abra la aplicación hello *Web.config* archivo hello ContosoAdsWeb proyecto.</span><span class="sxs-lookup"><span data-stu-id="d3916-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="d3916-184">archivo Hello contiene una cadena de conexión de SQL y una cadena de conexión de almacenamiento de Azure para trabajar con blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="d3916-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="d3916-185">cadena de conexión SQL Hola señala tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) base de datos.</span><span class="sxs-lookup"><span data-stu-id="d3916-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="d3916-186">cadena de conexión de almacenamiento de Hello es un ejemplo que tiene los marcadores de posición de clave de acceso y nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="d3916-187">Va a reemplazar con una cadena de conexión que tiene el nombre de Hola y la clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3916-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="d3916-188">cadena de conexión de almacenamiento de Hola se denomina AzureWebJobsStorage porque es Hola Hola de nombre de que usa el SDK de WebJobs forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d3916-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="d3916-189">Hola mismo nombre se utiliza aquí por lo que tiene valor de cadena de conexión solo tooset Hola entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="d3916-190">En **Explorador de servidores**, haga clic en la cuenta de almacenamiento en hello **almacenamiento** nodo y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="d3916-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Haga clic en propiedades de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="d3916-192">Hola **propiedades** ventana, haga clic en **claves de la cuenta de almacenamiento**y, a continuación, haga clic en el botón de puntos suspensivos Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Claves de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="d3916-194">Hola copia **cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="d3916-194">Copy hello **Connection String**.</span></span>

    ![Cuadro de diálogo Claves de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="d3916-196">Reemplace la cadena de conexión de almacenamiento de Hola Hola *Web.config* archivo con la cadena de conexión de Hola que acaba de copiar.</span><span class="sxs-lookup"><span data-stu-id="d3916-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="d3916-197">Asegúrese de que seleccionar todos los elementos dentro de comillas de hello pero sin incluir las comillas de hello antes de pegar.</span><span class="sxs-lookup"><span data-stu-id="d3916-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="d3916-198">Abra hello *App.config* archivo hello ContosoAdsWebJob proyecto.</span><span class="sxs-lookup"><span data-stu-id="d3916-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="d3916-199">Este archivo tiene dos cadenas de conexión de almacenamiento, una para los datos de aplicación y otra para registro.</span><span class="sxs-lookup"><span data-stu-id="d3916-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="d3916-200">Puede utilizar cuentas de almacenamiento independientes para los datos de aplicación y el registro, y usar [varias cuentas de almacenamiento para datos](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="d3916-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="d3916-201">Para este tutorial, usará una única cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3916-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="d3916-202">las cadenas de conexión de Hello tienen marcadores de posición para claves de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="d3916-203">De forma predeterminada, Hola SDK de WebJobs busca las cadenas de conexión denominado AzureWebJobsStorage y AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="d3916-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="d3916-204">Como alternativa, también puede [almacenar la cadena de conexión de hello pero que desee y pasa de forma explícita toohello `JobHost` objeto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="d3916-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="d3916-205">Reemplace ambas cadenas de conexión de almacenamiento con la cadena de conexión de Hola que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d3916-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="d3916-206">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="d3916-206">Save your changes.</span></span>

## <span data-ttu-id="d3916-207"><a id="run"></a>Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="d3916-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="d3916-208">toostart hello web front-end de la aplicación hello, presione CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="d3916-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="d3916-209">explorador predeterminado de Hello abre la página de inicio de toohello.</span><span class="sxs-lookup"><span data-stu-id="d3916-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="d3916-210">(proyecto de hello web se ejecuta ya se ha hecho proyecto de inicio de Hola.)</span><span class="sxs-lookup"><span data-stu-id="d3916-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Página principal de Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="d3916-212">toostart Hola trabajo Web back-end de la aplicación hello, haga clic en proyecto de ContosoAdsWebJob de hello en **el Explorador de soluciones**y, a continuación, haga clic en **depurar** > **Iniciar nueva instancia** .</span><span class="sxs-lookup"><span data-stu-id="d3916-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="d3916-213">Una ventana de la aplicación de consola se abre y muestra mensajes de registro que indica el objeto de trabajos Web SDK JobHost Hola inició toorun.</span><span class="sxs-lookup"><span data-stu-id="d3916-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Ventana de la aplicación de consola que muestra ese Hola de back-end se ejecuta](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="d3916-215">En el explorador, haga clic en **Crear un anuncio**.</span><span class="sxs-lookup"><span data-stu-id="d3916-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="d3916-216">Escriba algunos datos de prueba, seleccione un tooupload de imagen y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="d3916-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="d3916-218">aplicación Hello queda toohello página de índice, pero no muestra una vista en miniatura para nuevo anuncio de Hola dado que el procesamiento no se ha realizado.</span><span class="sxs-lookup"><span data-stu-id="d3916-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="d3916-219">Mientras tanto, después de una breve espera un mensaje de registro en la ventana de aplicación de consola de hello muestra que un mensaje de la cola se recibió y se ha procesado.</span><span class="sxs-lookup"><span data-stu-id="d3916-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Ventana de la aplicación de consola que muestra que se ha procesado un mensaje de cola](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="d3916-221">Después de ver Hola registrar mensajes en la ventana de aplicación de consola de hello, actualizar vista en miniatura de hello índice página toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Página de índice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="d3916-223">Haga clic en **detalles** para la imagen a tamaño completo ad toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="d3916-225">Ha estado ejecutando aplicación hello en el equipo local y que está usando un SQL Server, base de datos ubicada en el equipo, pero está trabajando con las colas y blobs de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="d3916-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="d3916-226">Hola pasos de la sección ejecutaremos aplicación hello en nube de hello, con una base de datos en la nube, así como en la nube blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="d3916-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="d3916-227"><a id="runincloud"></a>Ejecutar la aplicación hello en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="d3916-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="d3916-228">Deberá llevar a cabo Hola tras la aplicación de hello toorun de pasos en la nube de hello:</span><span class="sxs-lookup"><span data-stu-id="d3916-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="d3916-229">Implementar aplicaciones de tooWeb.</span><span class="sxs-lookup"><span data-stu-id="d3916-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="d3916-230">Visual Studio crea automáticamente una aplicación web en el Servicio de aplicaciones y una instancia de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d3916-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="d3916-231">Configurar toouse de aplicación web de hello en su cuenta de almacenamiento y la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="d3916-232">Después de haber creado algunos anuncios mientras se ejecuta en la nube de hello, podrá ver HOLA hola de toosee de panel de SDK de WebJobs enriquecido de características tiene toooffer de supervisión.</span><span class="sxs-lookup"><span data-stu-id="d3916-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="d3916-233">Implementar aplicaciones de tooWeb</span><span class="sxs-lookup"><span data-stu-id="d3916-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="d3916-234">Cierre el Explorador de Hola y ventana de aplicación de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="d3916-235">Siga los pasos de Hola Hola [publicar tooAzure con base de datos SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sección.</span><span class="sxs-lookup"><span data-stu-id="d3916-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="d3916-236">Después de completar los pasos para implementar hello, continúe con las tareas restantes de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d3916-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="d3916-237">Configurar toouse de aplicación web de hello su cuenta de almacenamiento y la base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d3916-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="d3916-238">Es una práctica recomendada de seguridad demasiado[evitar colocar información confidencial como cadenas de conexión en archivos que se almacenan en repositorios de código de origen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="d3916-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="d3916-239">Azure proporciona una manera toodo: puede establecer la cadena de conexión y otros valores de configuración en hello entorno de Azure y API de configuración de ASP.NET recoge estos valores de automáticamente cuando la aplicación hello se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="d3916-240">Puede establecer estos valores en Azure mediante **Explorador de servidores**, Hola Portal de Azure, Windows PowerShell, u Hola interfaz de línea de comandos entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="d3916-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="d3916-241">Para obtener más información, consulte [Funcionamiento de las cadenas de aplicación y de las cadenas de conexión](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="d3916-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="d3916-242">En esta sección, utilice **Explorador de servidores** tooset valores de cadena de conexión en Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="d3916-243">En el **Explorador de servidores**, haga clic con el botón derecho en la aplicación web en **Azure > App Service > {su grupo de recursos}** y luego haga clic en **Ver configuración**.</span><span class="sxs-lookup"><span data-stu-id="d3916-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="d3916-244">Hola **aplicación Web de Azure** ventana se abre en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="d3916-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="d3916-245">Cambiar el nombre de Hola de nombre de toohello de cadena de conexión de hello DefaultConnection elegido al configurar la base de datos SQL de Hola Hola [publicar tooAzure con base de datos SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artículo.</span><span class="sxs-lookup"><span data-stu-id="d3916-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="d3916-246">Azure crea automáticamente esta cadena de conexión cuando se creó la aplicación web de hello con una base de datos asociada, por lo que ya tiene valor de cadena de conexión adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="d3916-247">Está cambiando simplemente Hola nombre toowhat que busca el código.</span><span class="sxs-lookup"><span data-stu-id="d3916-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="d3916-248">Agregue dos cadenas de conexión nuevas, llamadas AzureWebJobsStorage y AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="d3916-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="d3916-249">Establecer tipo de base de datos de hello demasiado**personalizado**y el mismo valor que usó anteriormente para hello conjunto Hola conexión cadena valor toohello *Web.config* y *App.config* archivos.</span><span class="sxs-lookup"><span data-stu-id="d3916-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="d3916-250">(Asegúrese de incluir la cadena de conexión completa de hello, no solo tecla de acceso de hello y no incluya comillas hello).</span><span class="sxs-lookup"><span data-stu-id="d3916-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="d3916-251">Estas cadenas de conexión se utilizan por hello SDK de WebJobs, uno para los datos de aplicación y otro para el registro.</span><span class="sxs-lookup"><span data-stu-id="d3916-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="d3916-252">Como se vio anteriormente, Hola de datos de aplicación también se usa código de hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="d3916-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="d3916-253">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-253">Click **Save**.</span></span>

    ![Cadenas de conexión en el Portal de Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="d3916-255">En **Explorador de servidores**, haga clic en la aplicación web de hello y, a continuación, haga clic en **detener**.</span><span class="sxs-lookup"><span data-stu-id="d3916-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="d3916-256">Cuando se detenga la aplicación web de hello, haga clic en aplicación web de Hola de nuevo y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="d3916-257">Hola trabajo Web se inicia automáticamente cuando publica, pero se detiene al cambiar una configuración.</span><span class="sxs-lookup"><span data-stu-id="d3916-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="d3916-258">toorestart, puede reiniciar la aplicación web de Hola o reiniciar Hola trabajo Web en hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="d3916-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d3916-259">Es generalmente recomendada toorestart hello web aplicación después de un cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="d3916-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="d3916-260">Actualice la ventana del explorador de Hola que tiene la URL de la aplicación web hello en su barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="d3916-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="d3916-261">aparece la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-261">hello home page appears.</span></span>
8. <span data-ttu-id="d3916-262">Crear un anuncio, tal y como lo hizo cuando se [se ejecutaba aplicación hello localmente](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="d3916-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="d3916-263">página de índice de Hello muestra sin una miniatura al principio.</span><span class="sxs-lookup"><span data-stu-id="d3916-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="d3916-264">Actualice la página de hello después de unos segundos y aparece hello miniatura.</span><span class="sxs-lookup"><span data-stu-id="d3916-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="d3916-265">Si no aparece la miniatura de hello, puede tener toowait aproximadamente un minuto para hello toorestart de trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="d3916-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="d3916-266">Si después de un tiempo, aún no ve la miniatura de hello al actualizar página hello, Hola trabajo Web no se inicia automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d3916-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="d3916-267">En ese caso, vaya toohello **servicios de aplicaciones** hoja en hello [portal de Azure](https://portal.azure.com/), busque la aplicación web y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="d3916-268">Hola de vista panel de SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="d3916-269">Hola [portal de Azure](https://portal.azure.com/), seleccione hello **hoja de servicios de aplicaciones**, busque la aplicación web y seleccione **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="d3916-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="d3916-270">Seleccione hello **registros** ficha.</span><span class="sxs-lookup"><span data-stu-id="d3916-270">Select hello **Logs** tab.</span></span>

    ![Pestaña Registros](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="d3916-272">Una nueva pestaña de explorador abre toohello panel de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="d3916-273">panel de Hello muestra ese Hola trabajo Web se ejecuta y muestra una lista de funciones en el código que Hola que activa de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="d3916-274">Haga clic en uno de hello funciones toosee detalles sobre la ejecución.</span><span class="sxs-lookup"><span data-stu-id="d3916-274">Click one of hello functions toosee details about its execution.</span></span>

    ![Panel del SDK de WebJobs](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Panel del SDK de WebJobs](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="d3916-277">Hola **función reproducción** botón en esta página hace que Hola SDK de WebJobs framework toocall Hola función nuevo y le ofrece una función de toohello de datos que se pasan de oportunidad toochange hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="d3916-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="d3916-278">Cuando haya terminado de pruebas, considere la posibilidad de eliminar la aplicación web de hello, cuenta de almacenamiento y la instancia de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d3916-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="d3916-279">aplicación web de Hello es gratuito, pero hello cuenta de almacenamiento SQL y la instancia de base de datos generan cargos (si bien es cierto, mínimo debido toohello pequeño tamaño).</span><span class="sxs-lookup"><span data-stu-id="d3916-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="d3916-280">Además, si deja hello web aplicación en ejecución, cualquier persona que se encuentra la dirección URL puede crear y ver anuncios.</span><span class="sxs-lookup"><span data-stu-id="d3916-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="d3916-281">Eliminar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="d3916-281">Delete your web app</span></span>
<span data-ttu-id="d3916-282">En el portal de hello, vaya toohello **servicios de aplicaciones** hoja, busque y seleccione la aplicación web y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="d3916-283">Si solo desea tootemporarily impedir que otras personas tengan acceso a aplicaciones web de hello, haga clic en **detener** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d3916-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="d3916-284">En ese caso, seguirán aplicando costos tooaccrue para hello cuenta de almacenamiento y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d3916-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="d3916-285">Eliminar la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d3916-285">Delete your storage account</span></span>
<span data-ttu-id="d3916-286">toodelete su cuenta de almacenamiento, consulte [eliminar una cuenta de almacenamiento](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d3916-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="d3916-287">Eliminar la base de datos</span><span class="sxs-lookup"><span data-stu-id="d3916-287">Delete your database</span></span>
<span data-ttu-id="d3916-288">toodelete SQL de base de datos, vea hello [API de REST de base de datos de SQL Azure](https://docs.microsoft.com/rest/api/sql/) documentación.</span><span class="sxs-lookup"><span data-stu-id="d3916-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="d3916-289"><a id="create"></a>Crear aplicación hello desde el principio</span><span class="sxs-lookup"><span data-stu-id="d3916-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="d3916-290">En esta sección deberá llevar a cabo hello las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d3916-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="d3916-291">Crear una solución de Visual Studio con un proyecto web.</span><span class="sxs-lookup"><span data-stu-id="d3916-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="d3916-292">Agregue un proyecto de biblioteca de clases para los datos de hello capa de acceso que se comparte entre Hola front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="d3916-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="d3916-293">Agregue un proyecto de aplicación de consola de back-end de hello, con la implementación de trabajos Web habilitada.</span><span class="sxs-lookup"><span data-stu-id="d3916-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="d3916-294">Agregar paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3916-294">Add NuGet packages.</span></span>
* <span data-ttu-id="d3916-295">Establecer preferencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d3916-295">Set project references.</span></span>
* <span data-ttu-id="d3916-296">Copiar archivos de código y la configuración de aplicaciones de aplicación Hola descargado que trabajó en la sección anterior de Hola de tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="d3916-297">Revise las partes de Hola de código de hello que trabajan con colas y blobs de Azure y Hola SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="d3916-298">Creación de una solución de Visual Studio con un proyecto web y un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="d3916-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="d3916-299">En Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d3916-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d3916-300">Hola **nuevo proyecto** cuadro de diálogo, elija **Visual C#** > **Web** > **aplicación Web de ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="d3916-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="d3916-301">Denomine el proyecto de hello ContosoAdsWeb, asigne el nombre de solución de hello ContosoAdsWebJobsSDK (cambiar el nombre de la solución de hello si se va a colocar en hello misma carpeta que Hola descargado solución) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Nuevo proyecto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="d3916-303">Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, elija la plantilla MVC de Hola y seleccione **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="d3916-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Cambiar autenticación](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="d3916-305">Hola **Cambiar autenticación** cuadro de diálogo, elija **sin autenticación**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Sin autenticación](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="d3916-307">Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="d3916-308">Visual Studio crea la solución de Hola y un proyecto de web de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="d3916-309">En **el Explorador de soluciones**, haga clic en la solución de hello (no en proyecto de hello) y elija **agregar** > **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d3916-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="d3916-310">Hola **Agregar nuevo proyecto** cuadro de diálogo, elija **Visual C#** > **escritorio clásico de Windows** > **biblioteca de clases (. NET Marco de trabajo)** plantilla.</span><span class="sxs-lookup"><span data-stu-id="d3916-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="d3916-311">Proyecto de hello Name *ContosoAdsCommon*y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="d3916-312">Este proyecto contendrá contexto de Entity Framework de Hola y Hola data model que Hola front-end y back-end va a usar.</span><span class="sxs-lookup"><span data-stu-id="d3916-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="d3916-313">Como alternativa, podría definir las clases relacionadas con EF de hello en el proyecto web de Hola y hacer referencia a ese proyecto desde el proyecto de WebJob de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="d3916-314">Sin embargo, a continuación, su proyecto WebJob tendría un ensamblados de referencia de tooweb, que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="d3916-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="d3916-315">Incorporación de un proyecto de aplicación de consola con la implementación de WebJobs habilitada</span><span class="sxs-lookup"><span data-stu-id="d3916-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="d3916-316">Haga clic en proyecto de web hello (no Hola solución o proyecto de biblioteca de clases de hello) y, a continuación, haga clic en **agregar** > **nuevo proyecto de WebJob de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d3916-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Selección del menú Nuevo proyecto WebJob de Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="d3916-318">Hola **Agregar trabajo Web de Azure** cuadro de diálogo, escriba ContosoAdsWebJob como ambos hello **nombre del proyecto** hello y **nombre del trabajo Web**.</span><span class="sxs-lookup"><span data-stu-id="d3916-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="d3916-319">Deje **modo de trabajo Web ejecutan** establecido demasiado**ejecutar continuamente**.</span><span class="sxs-lookup"><span data-stu-id="d3916-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="d3916-320">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-320">Click **OK**.</span></span>

   <span data-ttu-id="d3916-321">Visual Studio crea una aplicación de consola que esté configurado toodeploy como un trabajo Web cada vez que implementar el proyecto web de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="d3916-322">toodo, que realiza Hola siguiente las tareas después de crear el proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="d3916-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="d3916-323">Agrega un *settings.json publicar el trabajo Web* archivo en la carpeta de propiedades del proyecto de hello trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="d3916-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="d3916-324">Agrega un *webjobs list.json* archivo en la carpeta de propiedades del proyecto de hello web.</span><span class="sxs-lookup"><span data-stu-id="d3916-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="d3916-325">Instala Hola paquete Microsoft.Web.WebJobs.Publish NuGet en proyecto de WebJob Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="d3916-326">Para obtener más información sobre estos cambios, consulte [cómo toodeploy trabajos Web mediante Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="d3916-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="d3916-327">Incorporación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="d3916-327">Add NuGet packages</span></span>
<span data-ttu-id="d3916-328">plantilla de proyecto nuevo de Hola para un proyecto de trabajo Web instala automáticamente el paquete de NuGet de SDK de WebJobs de hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="d3916-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="d3916-329">Uno de hello las dependencias del SDK de WebJobs que se instala automáticamente en el proyecto de WebJob Hola están Hola biblioteca de cliente de almacenamiento de Azure (SCL).</span><span class="sxs-lookup"><span data-stu-id="d3916-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="d3916-330">Sin embargo, debe tooadd toohello toowork de proyecto web con blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="d3916-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="d3916-331">Abra hello **administrar paquetes de NuGet** cuadro de diálogo de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="d3916-332">En el panel izquierdo de hello, seleccione **paquetes instalados**.</span><span class="sxs-lookup"><span data-stu-id="d3916-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="d3916-333">Buscar hello *el almacenamiento de Azure* del paquete y, a continuación, haga clic en **administrar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="d3916-334">Hola **seleccionar proyectos** cuadro, seleccione hello **ContosoAdsWeb** casilla de verificación y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="d3916-335">Los tres proyectos utilizan Hola Entity Framework toowork con datos de base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="d3916-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="d3916-336">En el panel izquierdo de hello, seleccione **Online**.</span><span class="sxs-lookup"><span data-stu-id="d3916-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="d3916-337">Buscar hello *EntityFramework* NuGet empaquetar e instalarlo en los tres proyectos.</span><span class="sxs-lookup"><span data-stu-id="d3916-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="d3916-338">Establecimiento de preferencias del proyecto</span><span class="sxs-lookup"><span data-stu-id="d3916-338">Set project references</span></span>
<span data-ttu-id="d3916-339">Web y proyectos de trabajo Web funcionan con la base de datos SQL de hello, por lo tanto necesitan un proyecto de ContosoAdsCommon toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="d3916-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="d3916-340">Hola ContosoAdsWeb proyecto, establecer una referencia de proyecto de ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="d3916-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="d3916-341">(Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **agregar** > **referencia**.</span><span class="sxs-lookup"><span data-stu-id="d3916-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="d3916-342">Hola **Administrador de referencias** cuadro de diálogo, seleccione **proyectos** > **solución** > **ContosoAdsCommon**y, a continuación, haga clic en **Aceptar**.)</span><span class="sxs-lookup"><span data-stu-id="d3916-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="d3916-343">proyecto de WebJob de Hola necesita referencias para trabajar con imágenes y para tener acceso a las cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="d3916-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="d3916-344">En proyectos de ContosoAdsWebJob hello, establezca una referencia demasiado`System.Drawing` y `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="d3916-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="d3916-345">Agregar archivos de configuración y de código</span><span class="sxs-lookup"><span data-stu-id="d3916-345">Add code and configuration files</span></span>
<span data-ttu-id="d3916-346">Este tutorial no muestra cómo demasiado[crear controladores MVC y vistas que usan la técnica scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), cómo demasiado[escribir código de Entity Framework que funciona con bases de datos de SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), o [Hola conceptos básicos de la programación asincrónica en ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="d3916-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="d3916-347">Por lo tanto, todo lo que sigue siendo toodo es copiar los archivos de código y la configuración de solución de hello descargado en la nueva solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="d3916-348">Después de hacerlo, hello las secciones siguientes se muestran y explican los elementos clave del código de hello.</span><span class="sxs-lookup"><span data-stu-id="d3916-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="d3916-349">tooadd archivos tooa proyecto o una carpeta, proyecto de Hola de menú contextual o carpeta y haga clic en **agregar** > **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="d3916-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="d3916-350">Hola seleccione los archivos desee y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d3916-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="d3916-351">Si se le pregunta si desea que tooreplace los archivos existentes, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d3916-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="d3916-352">En el proyecto ContosoAdsCommon de hello, elimine hello *Class1.cs* de archivos y agregar su Hola de contexto siguientes archivos de proyecto Hola descargado.</span><span class="sxs-lookup"><span data-stu-id="d3916-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d3916-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-353">*Ad.cs*</span></span>
   * <span data-ttu-id="d3916-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="d3916-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="d3916-356">En proyecto de ContosoAdsWeb de hello, agregue Hola siguientes archivos de proyecto Hola descargado.</span><span class="sxs-lookup"><span data-stu-id="d3916-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d3916-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="d3916-357">*Web.config*</span></span>
   * <span data-ttu-id="d3916-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="d3916-359">Hola *controladores* carpeta: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="d3916-360">Hola *Views\Shared* carpeta: *_Layout.cshtml* archivo</span><span class="sxs-lookup"><span data-stu-id="d3916-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="d3916-361">Hola *Views\Home* carpeta: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="d3916-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="d3916-362">Hola *Views\Ad* carpeta (crear carpeta de hello en primer lugar): cinco *.cshtml* archivos</span><span class="sxs-lookup"><span data-stu-id="d3916-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="d3916-363">En proyecto de ContosoAdsWebJob de hello, agregue Hola siguientes archivos de proyecto Hola descargado.</span><span class="sxs-lookup"><span data-stu-id="d3916-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d3916-364">*App.config* (cambiar el filtro de tipo de archivo de hello demasiado**todos los archivos**)</span><span class="sxs-lookup"><span data-stu-id="d3916-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="d3916-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-365">*Program.cs*</span></span>
   * <span data-ttu-id="d3916-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="d3916-366">*Functions.cs*</span></span>

<span data-ttu-id="d3916-367">Ahora puede compilar, ejecutar e implementar aplicación de hello tal como se indica anteriormente en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="d3916-368">Antes de hacerlo, sin embargo, detenga Hola trabajo Web que se esté ejecutando en hello primera aplicación web que se implementan en.</span><span class="sxs-lookup"><span data-stu-id="d3916-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="d3916-369">En caso contrario, ese trabajo Web procesar mensajes en cola creados localmente o por aplicación Hola que se ejecuta en una nueva aplicación web, ya que todos utilizan Hola mismo cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3916-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="d3916-370"><a id="code"></a>Revise el código de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="d3916-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="d3916-371">Hello las secciones siguientes explican el código de hello relacionados con tooworking con hello SDK de WebJobs y blobs de almacenamiento de Azure y colas.</span><span class="sxs-lookup"><span data-stu-id="d3916-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="d3916-372">Para toohello específico Hola código SDK de WebJobs, visite toohello [Program.cs y Functions.cs](#programcs) secciones.</span><span class="sxs-lookup"><span data-stu-id="d3916-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="d3916-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="d3916-374">archivo de Hello Ad.cs define una enumeración de categorías de ad y una clase de entidad POCO para obtener información de ad.</span><span class="sxs-lookup"><span data-stu-id="d3916-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="d3916-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="d3916-376">Hola ContosoAdsContext clase especifica que se utiliza la clase de Ad de hello en una colección de DbSet, que Entity Framework se almacena en una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d3916-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="d3916-377">clase Hello tiene dos constructores.</span><span class="sxs-lookup"><span data-stu-id="d3916-377">hello class has two constructors.</span></span> <span data-ttu-id="d3916-378">Hola primero participa en el proyecto web de Hola y especifica Hola nombre de una cadena de conexión que se almacena en el archivo Web.config de Hola o entorno de Azure en tiempo de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="d3916-379">segundo constructor de Hello permite toopass en la cadena de conexión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="d3916-380">Es necesario para el proyecto WebJob de hello porque no tiene un archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="d3916-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="d3916-381">Se ha visto anteriormente donde se almacenó esta cadena de conexión y podrá ver más adelante cómo código de hello recupera la cadena de conexión de hello cuando crea una instancia de clase de DbContext Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="d3916-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="d3916-383">Hola `BlobInformation` clase es toostore usa información acerca de un blob de imágenes en un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="d3916-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="d3916-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="d3916-385">Código que se llama desde hello `Application_Start` método crea un *imágenes* contenedor de blobs y una *imágenes* cola si todavía no existen.</span><span class="sxs-lookup"><span data-stu-id="d3916-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="d3916-386">Esto garantiza que cada vez que se inicia con una nueva cuenta de almacenamiento, Hola necesarias se crean automáticamente a la cola y el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="d3916-387">Hola cuenta de almacenamiento de toohello de código obtiene acceso mediante el uso de la cadena de conexión de almacenamiento de Hola de hello *Web.config* entorno de Azure en tiempo de ejecución o de archivo.</span><span class="sxs-lookup"><span data-stu-id="d3916-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="d3916-388">A continuación, obtiene una referencia toohello *imágenes* contenedor de blobs, crea el contenedor de hello si aún no existe, y establece permisos en el nuevo contenedor de Hola de acceso.</span><span class="sxs-lookup"><span data-stu-id="d3916-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="d3916-389">De forma predeterminada, nuevos contenedores de permitir que a sólo los clientes con blobs de tooaccess de credenciales de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3916-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="d3916-390">aplicación web de Hello necesita Hola blobs toobe público para que pueden mostrar imágenes con direcciones URL que blobs de imagen toohello de punto.</span><span class="sxs-lookup"><span data-stu-id="d3916-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="d3916-391">Un código similar Obtiene una referencia toohello *thumbnailrequest* poner en cola y crea una nueva cola.</span><span class="sxs-lookup"><span data-stu-id="d3916-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="d3916-392">En este caso no es necesario cambios de permiso.</span><span class="sxs-lookup"><span data-stu-id="d3916-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="d3916-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d3916-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="d3916-394">Hola *_Layout.cshtml* archivo establece el nombre de la aplicación hello en hello encabezado y pie y crea una entrada de menú "Anuncios".</span><span class="sxs-lookup"><span data-stu-id="d3916-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="d3916-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d3916-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="d3916-396">Hola *Views\Home\Index.cshtml* archivo muestra los vínculos de categoría en la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="d3916-397">vínculos de Hello pasan el valor entero Hola Hola `Category` enumeración en una página de índice de anuncios de toohello variable de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="d3916-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="d3916-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="d3916-399">Hola *AdController.cs* archivo, llamadas de constructor Hola Hola `InitializeStorage` objetos de biblioteca de cliente de almacenamiento de Azure de toocreate del método que proporcionan una API para trabajar con blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="d3916-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="d3916-400">A continuación, el código de hello Obtiene una referencia toohello *imágenes* contenedor de blob como vimos anteriormente en *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="d3916-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="d3916-401">Mientras hace eso, establece una [directiva de reintentos](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) apropiada para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d3916-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="d3916-402">Directiva de reintentos de retroceso exponencial de Hello predeterminada podría dejar de responder hello web app para más de un minuto en varios intentos para un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="d3916-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="d3916-403">Directiva de reintentos de Hello especificada aquí espera tres segundos después de cada uno de ellos probar para una toothree intentos.</span><span class="sxs-lookup"><span data-stu-id="d3916-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="d3916-404">Un código similar Obtiene una referencia toohello *imágenes* cola.</span><span class="sxs-lookup"><span data-stu-id="d3916-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="d3916-405">La mayoría del código de controlador de hello es típico para trabajar con un modelo de datos de Entity Framework mediante una clase DbContext.</span><span class="sxs-lookup"><span data-stu-id="d3916-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="d3916-406">Una excepción es hello HttpPost `Create` método, que carga un archivo y lo guarda en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="d3916-407">enlazador de modelos de Hello proporciona un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método del objeto.</span><span class="sxs-lookup"><span data-stu-id="d3916-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="d3916-408">Si el usuario de hello seleccionó un tooupload de archivo, código de hello carga el archivo hello, lo guarda en un blob y actualiza el registro de base de datos de Ad de hello con una dirección URL que señala toohello blob.</span><span class="sxs-lookup"><span data-stu-id="d3916-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="d3916-409">Hello código Hola carga es Hola `UploadAndSaveBlobAsync` método.</span><span class="sxs-lookup"><span data-stu-id="d3916-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="d3916-410">Crea un nombre GUID para el blob de hello, cargas y archivo de hello guarda y devuelve un blob de referencia toohello guardado.</span><span class="sxs-lookup"><span data-stu-id="d3916-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="d3916-411">Después de hello HttpPost `Create` método carga un blob y Hola de las actualizaciones de base de datos, crea un proceso de back-end de Hola de tooinform para cola de mensajes que una imagen está lista para la vista en miniatura de conversión tooa.</span><span class="sxs-lookup"><span data-stu-id="d3916-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="d3916-412">Hola código de hello HttpPost `Edit` método es similar, salvo que si el usuario de hello selecciona un nuevo archivo de imagen, deben eliminarse los blobs que ya existen para este anuncio.</span><span class="sxs-lookup"><span data-stu-id="d3916-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="d3916-413">Este es el código de hello que elimina los blobs cuando se elimina un anuncio:</span><span class="sxs-lookup"><span data-stu-id="d3916-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="d3916-414">ContosoAdsWeb - Views\Ad\Index.cshtml y Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="d3916-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="d3916-415">Hola *Index.cshtml* archivo muestra vistas en miniatura con hello otros datos de ad:</span><span class="sxs-lookup"><span data-stu-id="d3916-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="d3916-416">Hola *Details.cshtml* archivo muestra la imagen a tamaño completo hello:</span><span class="sxs-lookup"><span data-stu-id="d3916-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="d3916-417">ContosoAdsWeb - Views\Ad\Create.cshtml y Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="d3916-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="d3916-418">Hola *Create.cshtml* y *Edit.cshtml* archivos especifican formulario codificación que permite Hola Hola de controlador tooget `HttpPostedFileBase` objeto.</span><span class="sxs-lookup"><span data-stu-id="d3916-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="d3916-419">Un `<input>` elemento indica Hola explorador tooprovide un cuadro de diálogo de selección de archivo.</span><span class="sxs-lookup"><span data-stu-id="d3916-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="d3916-420"><a id="programcs"></a>ContosoAdsWebJob: Program.cs</span><span class="sxs-lookup"><span data-stu-id="d3916-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="d3916-421">Cuando Hola trabajo Web que se inicia, hello `Main` llamadas al método Hola SDK de WebJobs `JobHost.RunAndBlock` toobegin ejecución del método de desencadenadas funciones en el subproceso actual Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="d3916-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Método GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="d3916-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="d3916-423">Hola SDK de WebJobs llama a este método cuando se recibe un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="d3916-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="d3916-424">método Hello crea una vista en miniatura y coloca Hola miniatura de la dirección URL en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="d3916-425">Hola `QueueTrigger` atributo dirige hello toocall de SDK de WebJobs este método cuando se recibe un mensaje nuevo en la cola de thumbnailrequest Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="d3916-426">Hola `BlobInformation` objeto de mensaje de bienvenida de cola es automáticamente deserializado en hello `blobInfo` parámetro.</span><span class="sxs-lookup"><span data-stu-id="d3916-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="d3916-427">Cuando se completa el método hello, se elimina el mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="d3916-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="d3916-428">Si se produce un error en el método hello antes de completar, no se elimina el mensaje de bienvenida de cola; Después de que expire una concesión de 10 minutos, mensaje de bienvenida es toobe lanzamiento nuevo recoge y procesa.</span><span class="sxs-lookup"><span data-stu-id="d3916-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="d3916-429">Esta secuencia no se repite de manera indefinida cuando un mensaje provoca siempre una excepción.</span><span class="sxs-lookup"><span data-stu-id="d3916-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="d3916-430">Después de 5 incorrecta intentos tooprocess un mensaje, mensaje de bienvenida es tooa movida cola denominada {queuename}-dudoso.</span><span class="sxs-lookup"><span data-stu-id="d3916-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="d3916-431">Hola número máximo de intentos es configurable.</span><span class="sxs-lookup"><span data-stu-id="d3916-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="d3916-432">Hola dos `Blob` atributos proporcionan los objetos que están enlazados tooblobs: un blob de imágenes existente toohello y uno tooa nuevo en miniatura blob que crea el método hello.</span><span class="sxs-lookup"><span data-stu-id="d3916-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="d3916-433">Nombres de BLOB proceden de propiedades de hello `BlobInformation` objeto recibido en el mensaje de bienvenida de cola (`BlobName` y `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="d3916-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="d3916-434">tooget Hola todas las funcionalidades de hello biblioteca cliente de almacenamiento, puede usar hello `CloudBlockBlob` toowork de clase con los blobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="d3916-435">Si desea que el código de tooreuse que escribió toowork con `Stream` objetos, puede utilizar hello `Stream` clase.</span><span class="sxs-lookup"><span data-stu-id="d3916-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="d3916-436">Para obtener más información acerca de cómo toowrite las funciones utilizan atributos de SDK de WebJobs, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3916-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="d3916-437">¿Cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="d3916-438">¿Cómo toouse Azure blob storage con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="d3916-439">Cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="d3916-440">Cómo toouse de Bus de servicio de Azure con Hola SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="d3916-441">Si la aplicación web se ejecuta en varias máquinas virtuales, se ejecutarán simultáneamente varios trabajos Web, y en algunos casos esto puede producir en hello mismo datos procesados varias veces.</span><span class="sxs-lookup"><span data-stu-id="d3916-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="d3916-442">Esto no es un problema si usa cola integrados de hello, blob y desencadenadores de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="d3916-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="d3916-443">Hola SDK garantiza que las funciones se procesará una sola vez para cada mensaje o blob.</span><span class="sxs-lookup"><span data-stu-id="d3916-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="d3916-444">Para obtener información acerca de cómo tooimplement apagado ordenado, consulte [apagado ordenado](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="d3916-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="d3916-445">Hola código de hello `ConvertImageToThumbnailJPG` método (no mostrado) usa las clases en hello `System.Drawing` espacio de nombres para simplificar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d3916-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="d3916-446">Sin embargo, las clases de hello en este espacio de nombres se diseñaron para su uso con Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="d3916-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="d3916-447">No se admiten para usarse en un servicio de Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d3916-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="d3916-448">Para más información acerca de las opciones de procesamiento de imagen, consulte [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Generación de imagen dinámica) y [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Cambio de tamaño de imagen profunda).</span><span class="sxs-lookup"><span data-stu-id="d3916-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d3916-449">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3916-449">Next steps</span></span>
<span data-ttu-id="d3916-450">En este tutorial, ha visto una aplicación simple de varios niveles que emplea Hola SDK de WebJobs para el procesamiento de back-end.</span><span class="sxs-lookup"><span data-stu-id="d3916-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="d3916-451">En esta sección se ofrecen algunas sugerencias para obtener más información acerca de las aplicaciones de múltiples niveles de ASP.NET y WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d3916-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="d3916-452">Características que faltan</span><span class="sxs-lookup"><span data-stu-id="d3916-452">Missing features</span></span>
<span data-ttu-id="d3916-453">se ha conservado simple aplicación Hello para obtener un tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="d3916-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="d3916-454">En una aplicación del mundo real, debería implementar [inyección de dependencia](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) hello y [repositorio y una unidad de trabajan patrones](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [una interfaz para el registro](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilice [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) datos toomanage cambios en el modelo y usar [resistencia de conexión de EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage errores transitorios de red.</span><span class="sxs-lookup"><span data-stu-id="d3916-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="d3916-455">Escalado de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-455">Scaling WebJobs</span></span>
<span data-ttu-id="d3916-456">Los trabajos Web se ejecuta en hello contexto de una aplicación web y no es escalables por separado.</span><span class="sxs-lookup"><span data-stu-id="d3916-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="d3916-457">Por ejemplo, si tiene una instancia de aplicación web estándar, tiene solo una instancia de su proceso de segundo plano que se ejecuta y que está usando algunos de los recursos del servidor hello (CPU, memoria, etc.) que lo contrario estarían disponibles tooserve contenido de web.</span><span class="sxs-lookup"><span data-stu-id="d3916-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="d3916-458">Si tráfico varía según la hora del día o día de la semana, y si necesita Hola back-end de procesamiento puede esperar toodo, puede programar los trabajos Web toorun en momentos de poco tráfico.</span><span class="sxs-lookup"><span data-stu-id="d3916-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="d3916-459">Si carga Hola sigue siendo demasiado alto para esa solución, puede ejecutar Hola back-end como un trabajo Web en una aplicación web independiente dedicado para ese fin.</span><span class="sxs-lookup"><span data-stu-id="d3916-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="d3916-460">A continuación, puede escalar la aplicación web back-end con independencia de la aplicación web front-end.</span><span class="sxs-lookup"><span data-stu-id="d3916-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="d3916-461">Para obtener más información, consulte [Escalado de WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="d3916-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="d3916-462">Evitar tiempos de inactividad por tiempo de espera agotado en aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="d3916-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="d3916-463">toomake seguro sus trabajos Web se ejecuta siempre, y se ejecuta en todas las instancias de la aplicación web, tiene hello tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) característica.</span><span class="sxs-lookup"><span data-stu-id="d3916-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="d3916-464">Uso de hello SDK de WebJobs fuera de trabajos Web</span><span class="sxs-lookup"><span data-stu-id="d3916-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="d3916-465">Un programa que usa el SDK de WebJobs de hello no tiene toorun en Azure en un trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="d3916-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="d3916-466">Se puede ejecutar localmente y también se puede ejecutar en otros entornos, como por ejemplo un rol de trabajo Servicio en la nube o un servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="d3916-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="d3916-467">Sin embargo, solo puede acceder a Hola panel de SDK de WebJobs a través de una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3916-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="d3916-468">panel de hello toouse tiene tooconnect cuenta de almacenamiento de la toohello de hello web app usa al establecer una cadena de conexión de hello AzureWebJobsDashboard en hello **configurar** ficha del portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3916-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="d3916-469">A continuación, puede obtener toohello panel mediante Hola después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="d3916-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="d3916-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="d3916-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="d3916-471">Para obtener más información, consulte [obtener un panel para el desarrollo local con hello SDK de WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), pero tenga en cuenta que muestra un nombre de cadena de conexión anterior.</span><span class="sxs-lookup"><span data-stu-id="d3916-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="d3916-472">Más documentación sobre WebJobs</span><span class="sxs-lookup"><span data-stu-id="d3916-472">More WebJobs documentation</span></span>
<span data-ttu-id="d3916-473">Para obtener más información, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="d3916-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
