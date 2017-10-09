---
title: "una aplicación de .NET en un tejido de servicio de contenedor tooAzure aaaDeploy | Documentos de Microsoft"
description: "Le enseña cómo toopackage una aplicación .NET en Visual Studio en un contenedor de Docker. A continuación, se implementa esta nueva aplicación de \"contenedor\" clúster de Service Fabric tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="4b4a6-104">Implementar una aplicación .NET en un tooAzure de contenedor de Windows Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4b4a6-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="4b4a6-105">Este tutorial muestra cómo toodeploy una aplicación ASP.NET existente en un contenedor de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="4b4a6-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="4b4a6-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b4a6-107">Creación de un proyecto de Docker en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b4a6-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="4b4a6-108">Inclusión de una aplicación existente en un contenedor</span><span class="sxs-lookup"><span data-stu-id="4b4a6-108">Containerize an existing application</span></span>
> * <span data-ttu-id="4b4a6-109">Configuración de la integración continua con Visual Studio y VSTS</span><span class="sxs-lookup"><span data-stu-id="4b4a6-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b4a6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4b4a6-110">Prerequisites</span></span>

1. <span data-ttu-id="4b4a6-111">Instale [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) para poder ejecutar contenedores en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="4b4a6-112">Familiarícese con hello [inicio rápido de contenedores de Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="4b4a6-113">Descargar hello [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="4b4a6-114">Instale [Azure PowerShell][link-azure-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="4b4a6-115">Instalar hello [extensión de herramientas de entrega continua para Visual Studio de 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="4b4a6-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="4b4a6-116">Cree una [suscripción de Azure][link-azure-subscription] y una [cuenta de Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="4b4a6-117">Creación de un clúster en Azure</span><span class="sxs-lookup"><span data-stu-id="4b4a6-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="4b4a6-118">Incluya la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="4b4a6-118">Containerize hello application</span></span>

<span data-ttu-id="4b4a6-119">Ahora que tiene un [clúster de Service Fabric se ejecuta en Azure](service-fabric-tutorial-create-cluster-azure-ps.md) están listo toocreate e implementar una aplicación en contenedores.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="4b4a6-120">toostart ejecuta la aplicación en un contenedor, necesitamos tooadd **soporte técnico de Docker** toohello proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="4b4a6-121">Cuando se agrega **soporte técnico de Docker** toohello aplicación, suceden dos cosas.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="4b4a6-122">En primer lugar, un _Dockerfile_ se agrega el proyecto toohello.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="4b4a6-123">Este nuevo archivo describe la forma de imagen de contenedor de hello toobe integrada.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="4b4a6-124">A continuación, segundo, un nuevo _crear docker_ se agrega el proyecto de solución toohello.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="4b4a6-125">nuevo proyecto Hello contiene algunos archivos de redacción de docker.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="4b4a6-126">Crear docker archivos pueden ser utilizado toodescribe cómo se ejecuta el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="4b4a6-127">Más información sobre cómo trabajara con las [herramientas de contenedor de Visual Studio][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="4b4a6-128">Si es Hola primera vez que se ejecutan las imágenes de contenedor de Windows en el equipo, Docker CE debe extraerlo imágenes de base de Hola para los contenedores.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="4b4a6-129">imágenes de Hola que se utilizan en este tutorial son 14 GB.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="4b4a6-130">Voy a ejecutarlo Hola después de imágenes del comando terminal toopull Hola base:</span><span class="sxs-lookup"><span data-stu-id="4b4a6-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="4b4a6-131">Agregue compatibilidad con Docker</span><span class="sxs-lookup"><span data-stu-id="4b4a6-131">Add Docker support</span></span>

<span data-ttu-id="4b4a6-132">Abra hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] archivo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="4b4a6-133">Menú contextual hello **FabrikamFiber.Web** proyecto > **agregar** > **compatibilidad con Docker**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="4b4a6-134">Agregar compatibilidad con SQL</span><span class="sxs-lookup"><span data-stu-id="4b4a6-134">Add support for SQL</span></span>

<span data-ttu-id="4b4a6-135">Esta aplicación utiliza SQL como proveedor de datos de hello, por lo que un servidor SQL server es necesario toorun Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="4b4a6-136">Haga referencia a una imagen del contenedor de SQL Server en el archivo docker-compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="4b4a6-137">En Visual Studio, abra **el Explorador de soluciones**, buscar **redactar docker**y el archivo abierto hello **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="4b4a6-138">Navegue toohello `services:` nodo, agregue un nodo denominado `db:` que define la entrada de SQL Server de hello para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="4b4a6-139">Puede utilizar cualquier servidor SQL Server que prefiera para la depuración local, siempre que sea accesible desde el host.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="4b4a6-140">Sin embargo, **localdb** no admite la comunicación `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="4b4a6-141">La ejecución de SQL Server en un contenedor no admite el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="4b4a6-142">Cuando se detiene el contenedor de hello, se borran los datos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="4b4a6-143">No utilice esta configuración para producción.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="4b4a6-144">Navegue toohello `fabrikamfiber.web:` nodo y agregar un nodo secundario denominado `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="4b4a6-145">Esto garantiza que hello `db` servicio (contenedor de SQL Server de Hola) se inicia antes de que la aplicación web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="4b4a6-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="4b4a6-146">Actualizar configuración de hello web</span><span class="sxs-lookup"><span data-stu-id="4b4a6-146">Update hello web config</span></span>

<span data-ttu-id="4b4a6-147">Nuevo en hello **FabrikamFiber.Web** del proyecto, cadena de conexión de actualización Hola Hola **web.config** toopoint toohello SQL Server en el contenedor de hello, de archivos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="4b4a6-148">Si desea toouse otro SQL Server al compilar una versión de compilación de la aplicación web, agregue otro archivo de web.release.config de tooyour de cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="4b4a6-149">Prueba del contenedor</span><span class="sxs-lookup"><span data-stu-id="4b4a6-149">Test your container</span></span>

<span data-ttu-id="4b4a6-150">Presione **F5** toorun y depuración aplicación hello en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="4b4a6-151">Borde abre la página de inicio definido de la aplicación con la dirección IP de hello del contenedor de Hola de red interna de NAT de hello (normalmente 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="4b4a6-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="4b4a6-152">vea toolearn más información acerca de la depuración de aplicaciones en contenedores con Visual Studio 2017 [este artículo][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![ejemplo de fabrikam en un contenedor][image-web-preview]

<span data-ttu-id="4b4a6-154">contenedor de Hello ahora está listo toobe genera y empaqueta en una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="4b4a6-155">Una vez que tenga la imagen de contenedor de hello integrada en su equipo, puede insertarlo tooany registro de contenedor y tire hacia abajo tooany toorun de host.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="4b4a6-156">Preparar la aplicación hello para la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="4b4a6-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="4b4a6-157">aplicación de hello tooget listo para ejecutarse en Service Fabric en Azure, necesitamos toocomplete dos pasos:</span><span class="sxs-lookup"><span data-stu-id="4b4a6-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="4b4a6-158">Exponer el puerto de Hola donde los deseamos toobe pueda tooreach nuestra aplicación web en el clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="4b4a6-159">Proporcionar una base de datos SQL preparada para producción para nuestra aplicación</span><span class="sxs-lookup"><span data-stu-id="4b4a6-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="4b4a6-160">Exponer el puerto para la aplicación hello Hola</span><span class="sxs-lookup"><span data-stu-id="4b4a6-160">Expose hello port for hello app</span></span>
<span data-ttu-id="4b4a6-161">clúster de Service Fabric Hola hemos configurado, tiene puerto *80* abre de forma predeterminada en hello equilibrador de carga de Azure, que equilibra clúster de toohello tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="4b4a6-162">Podemos exponer nuestro contenedor en este puerto mediante nuestro archivo docker.compose.yml.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="4b4a6-163">En Visual Studio, abra **el Explorador de soluciones**, buscar **redactar docker**y el archivo abierto hello **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="4b4a6-164">Modificar hello `fabrikamfiber.web:` nodo, agregar un nodo secundario denominado `ports:`.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="4b4a6-165">Agregue una entrada de cadena `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="4b4a6-166">Uso de una base de datos SQL de producción</span><span class="sxs-lookup"><span data-stu-id="4b4a6-166">Use a production SQL database</span></span>
<span data-ttu-id="4b4a6-167">Cuando se ejecutan en producción, es necesario que nuestros datos se conserven en nuestra base de datos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="4b4a6-168">Actualmente no hay ningún dato persistente de manera tooguarantee en un contenedor, por lo tanto, no se puede almacenar datos de producción en SQL Server en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="4b4a6-169">Se recomienda usar una instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="4b4a6-170">tooset seguridad y ejecutar un servidor administrado de SQL Server en Azure, visite hello [tutoriales rápidos de base de datos de SQL Azure] [ link-azure-sql] artículo.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="4b4a6-171">Recuerde toochange Hola conexión cadenas toohello SQL server en hello **web.release.config** archivo Hola **FabrikamFiber.Web** proyecto.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="4b4a6-172">Esta aplicación genera errores leves si no se puede acceder a ninguna base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="4b4a6-173">Puede elegir toogo con antelación e implementar aplicación hello con ningún servidor SQL server.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="4b4a6-174">Implementación con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4b4a6-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="4b4a6-175">tooset la implementación mediante Visual Studio Team Services, necesita hello tooinstall [extensión de herramientas de entrega continua para Visual Studio de 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="4b4a6-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="4b4a6-176">Esta extensión resulta fácil toodeploy tooAzure mediante la configuración de Visual Studio Team Services y obtener su clúster de Service Fabric tooyour de aplicación implementado.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="4b4a6-177">tooget iniciado, el código se debe hospedar en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="4b4a6-178">resto de Hola de esta sección se da por supuesto **git** se está usando.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="4b4a6-179">Configuración de un repositorio de VSTS</span><span class="sxs-lookup"><span data-stu-id="4b4a6-179">Set up a VSTS repo</span></span>
<span data-ttu-id="4b4a6-180">En la esquina inferior derecha de Hola de Visual Studio, haga clic en **agregar tooSource Control** > **Git** (o cualquier opción que prefiera).</span><span class="sxs-lookup"><span data-stu-id="4b4a6-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Presione el botón del control de código fuente de Hola][image-source-control]

<span data-ttu-id="4b4a6-182">Hola _Team Explorer_ panel, presione **publicar el repositorio de Git**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="4b4a6-183">Seleccione el nombre del repositorio VSTS y presione **Repositorio**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-183">Select your VSTS repository name and press **Repository**.</span></span>

![publicar tooVSTS de repositorio][image-publish-repo]

<span data-ttu-id="4b4a6-185">Ahora que el código está sincronizado con un repositorio de código fuente VSTS, puede configurar la integración continua y la entrega continua.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="4b4a6-186">Configuración de la entrega continua</span><span class="sxs-lookup"><span data-stu-id="4b4a6-186">Setup continuous delivery</span></span>

<span data-ttu-id="4b4a6-187">En _el Explorador de soluciones_, contextual hello **solución** > **configurar la entrega continua**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="4b4a6-188">Seleccione Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="4b4a6-189">Establecer **tipo de Host** demasiado**clúster de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="4b4a6-190">Establecer **Host de destino** toohello servicio de cluster Server tejido que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="4b4a6-191">Elija un **registro de contenedor** toopublish que el contenedor.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="4b4a6-192">Hola de uso **editar** botón toocreate un registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="4b4a6-193">Presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-193">Press **OK**.</span></span>

![Configuración de la integración continua para Service Fabric][image-setup-ci]
   
   <span data-ttu-id="4b4a6-195">Cuando se haya completado la configuración de hello, el contenedor es tooService implementado tejido.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="4b4a6-196">Cada vez que realice una inserción repositorio toohello de actualizaciones se ejecuta una versión y una nueva compilación.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4b4a6-197">Imágenes del contenedor de creación Hola tardar aproximadamente 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="4b4a6-198">clúster de Service Fabric Hola primera implementación toohello hace Hola base Windows Server Core imágenes de contenedor toobe descargado.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="4b4a6-199">descarga de Hello toma toocomplete adicional 5-10 minutos.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="4b4a6-200">Explorar aplicación de centro de llamadas de Fabrikam toohello mediante dirección url de hello del clúster: por ejemplo, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="4b4a6-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="4b4a6-201">Ahora que ha en contenedores e implementado la solución de Fabrikam Call Center hello, puede abrir hello [portal de Azure] [ link-azure-portal] y ver aplicación hello ejecutando en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="4b4a6-202">aplicación de hello tootry, abra un explorador web y vaya toohello URL del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4b4a6-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b4a6-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b4a6-203">Next steps</span></span>

<span data-ttu-id="4b4a6-204">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="4b4a6-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b4a6-205">Creación de un proyecto de Docker en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b4a6-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="4b4a6-206">Inclusión de una aplicación existente en un contenedor</span><span class="sxs-lookup"><span data-stu-id="4b4a6-206">Containerize an existing application</span></span>
> * <span data-ttu-id="4b4a6-207">Configuración de la integración continua con Visual Studio y VSTS</span><span class="sxs-lookup"><span data-stu-id="4b4a6-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
