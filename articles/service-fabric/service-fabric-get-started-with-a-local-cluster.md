---
title: aaaDeploy y actualizar Azure microservicios localmente | Documentos de Microsoft
description: "Obtenga información acerca de cómo implementar un tooit de aplicación existente tooset de un clúster de Service Fabric local y, a continuación, actualizar esa aplicación."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="5246d-103">Introducción a la implementación y actualización de aplicaciones en un clúster local</span><span class="sxs-lookup"><span data-stu-id="5246d-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="5246d-104">Hello Azure Service Fabric SDK incluye un entorno de desarrollo local completa que puede usar tooquickly Introducción a la implementación y administración de aplicaciones en un clúster local.</span><span class="sxs-lookup"><span data-stu-id="5246d-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="5246d-105">En este artículo, crear un clúster local, implementar una tooit de aplicación existente y, a continuación, actualizar esa aplicación tooa nueva versión, todo ello desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5246d-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="5246d-106">En este artículo se asume que ya [configuró un entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5246d-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="5246d-107">Creación de un clúster local</span><span class="sxs-lookup"><span data-stu-id="5246d-107">Create a local cluster</span></span>
<span data-ttu-id="5246d-108">Un clúster de Service Fabric representa un conjunto de recursos de hardware en los que se pueden implementar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5246d-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="5246d-109">Por lo general, un clúster se compone de cualquier parte de cinco toomany miles de máquinas.</span><span class="sxs-lookup"><span data-stu-id="5246d-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="5246d-110">Sin embargo, Hola tejido SDK del servicio incluye una configuración de clúster que se puede ejecutar en un único equipo.</span><span class="sxs-lookup"><span data-stu-id="5246d-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="5246d-111">Es importante toounderstand que Hola clúster local de Service Fabric no es un emulador o simulador.</span><span class="sxs-lookup"><span data-stu-id="5246d-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="5246d-112">Se ejecuta Hola mismo código de plataforma que se encuentra en los clústeres de varios equipos.</span><span class="sxs-lookup"><span data-stu-id="5246d-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="5246d-113">Hola única diferencia es que se ejecuta los procesos de plataforma de Hola que normalmente se reparten entre cinco equipos en un equipo.</span><span class="sxs-lookup"><span data-stu-id="5246d-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="5246d-114">Hola SDK proporciona tooset de dos maneras de un clúster local: un Windows PowerShell hello y script el Administrador de clústeres Local system aplicación de bandeja.</span><span class="sxs-lookup"><span data-stu-id="5246d-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="5246d-115">En este tutorial, usamos el script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="5246d-116">Si creó un clúster local mediante la implementación de una aplicación desde Visual Studio, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="5246d-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="5246d-117">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="5246d-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="5246d-118">Ejecute el script de instalación de clúster de Hola desde la carpeta del SDK de hello:</span><span class="sxs-lookup"><span data-stu-id="5246d-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="5246d-119">La instalación del clúster tardará unos instantes.</span><span class="sxs-lookup"><span data-stu-id="5246d-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="5246d-120">Una vez finalizada la instalación, debería ver una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="5246d-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Salida de instalación de clúster][cluster-setup-success]
   
    <span data-ttu-id="5246d-122">Ya estás listo tootry implementación de un clúster de tooyour de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5246d-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="5246d-123">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="5246d-123">Deploy an application</span></span>
<span data-ttu-id="5246d-124">Hola tejido SDK del servicio incluye un amplio conjunto de marcos de trabajo y herramientas para crear aplicaciones para el desarrollador.</span><span class="sxs-lookup"><span data-stu-id="5246d-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="5246d-125">Si está interesado en aprender cómo las aplicaciones de toocreate en Visual Studio, vea [crear su primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5246d-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="5246d-126">En este tutorial, usará una aplicación de ejemplo existente (denominada WordCount) para que pueda centrarse en los aspectos de la administración de plataforma de Hola Hola: implementación, supervisión y actualización.</span><span class="sxs-lookup"><span data-stu-id="5246d-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="5246d-127">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="5246d-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="5246d-128">Importe el módulo de PowerShell de SDK de tejido de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="5246d-129">Crear una aplicación hello toostore de directorio que descargar e implementar, como C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="5246d-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="5246d-130">[Descargar la aplicación WordCount de hello](http://aka.ms/servicefabric-wordcountapp) ubicación toohello que ha creado.</span><span class="sxs-lookup"><span data-stu-id="5246d-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="5246d-131">Nota: explorador Microsoft Edge de hello guarda el archivo hello con un *.zip* extensión.</span><span class="sxs-lookup"><span data-stu-id="5246d-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="5246d-132">Cambiar la extensión de archivo hello demasiado*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="5246d-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="5246d-133">Conecte el clúster local toohello:</span><span class="sxs-lookup"><span data-stu-id="5246d-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="5246d-134">Cree una nueva aplicación mediante el comando de implementación del SDK de hello con un nombre y un paquete de aplicación de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="5246d-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="5246d-135">Si todo funciona correctamente, debería ver Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="5246d-135">If all goes well, you should see hello following output:</span></span>
   
    ![Implementar un clúster local de aplicación toohello][deploy-app-to-local-cluster]
7. <span data-ttu-id="5246d-137">aplicación de hello toosee en acción, inicie el Explorador de Hola y navegue demasiado[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="5246d-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="5246d-138">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5246d-138">You should see:</span></span>
   
    ![Interfaz de usuario de aplicación implementada][deployed-app-ui]
   
    <span data-ttu-id="5246d-140">Hola aplicación WordCount es sencillo.</span><span class="sxs-lookup"><span data-stu-id="5246d-140">hello WordCount application is simple.</span></span> <span data-ttu-id="5246d-141">Incluye en el cliente JavaScript toogenerate aleatorio cinco caracteres "palabras de código", que son, a continuación, retransmite toohello aplicación a través de la API Web de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5246d-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="5246d-142">Un servicio con estado realiza un número de Hola de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="5246d-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="5246d-143">Se crean particiones basadas en el primer carácter de palabra Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="5246d-144">Puede encontrar código de origen de Hola de aplicación WordCount de hello en hello [clásico Introducción ejemplos](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="5246d-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="5246d-145">aplicación Hola que implementamos contiene cuatro particiones.</span><span class="sxs-lookup"><span data-stu-id="5246d-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="5246d-146">Por lo que las palabras que empiezan con la A la G se almacenan en la primera partición de hello, palabras que empiezan con H y N se almacenan en hello segunda partición y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="5246d-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="5246d-147">Visualización de los detalles y estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5246d-147">View application details and status</span></span>
<span data-ttu-id="5246d-148">Ahora que hemos implementado aplicación hello, echemos un vistazo a algunos de los detalles de la aplicación hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5246d-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="5246d-149">Consultar todas las aplicaciones implementadas en clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="5246d-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="5246d-150">Suponiendo que sólo ha implementado la aplicación WordCount de hello, verá algo parecido a:</span><span class="sxs-lookup"><span data-stu-id="5246d-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Consultar todas las aplicaciones implementadas en PowerShell][ps-getsfapp]
2. <span data-ttu-id="5246d-152">Vaya toohello siguiente nivel mediante una consulta de conjunto de hello de servicios que se incluyen en la aplicación WordCount de hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de servicios para la aplicación hello en PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="5246d-154">aplicación Hello se compone de dos servicios, hello web front-end y servicio con estado Hola que administra palabras hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="5246d-155">Por último, busque en la lista de Hola de particiones WordCountService:</span><span class="sxs-lookup"><span data-stu-id="5246d-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Ver las particiones de servicio de hello en PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="5246d-157">Hola conjunto de comandos que utilizan, al igual que todos los comandos de PowerShell de tejido de servicio, están disponibles para los clústeres que se podrían conectar a local o remoto.</span><span class="sxs-lookup"><span data-stu-id="5246d-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="5246d-158">Para una toointeract de manera más visual con clúster de hello, puede utilizar herramienta Explorador de Service Fabric basada en web de hello desplazándose demasiado[http://localhost:19080/explorador](http://localhost:19080/Explorer) en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Ver detalles de aplicación en el Explorador de Service Fabric][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="5246d-160">toolearn más información acerca del explorador de Service Fabric, vea [visualizar el clúster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5246d-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="5246d-161">Actualizar una aplicación</span><span class="sxs-lookup"><span data-stu-id="5246d-161">Upgrade an application</span></span>
<span data-ttu-id="5246d-162">Service Fabric proporciona actualizaciones sin tiempo de inactividad mediante la supervisión de estado de saludo de la aplicación hello tal y como implementa en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="5246d-163">Realizar una actualización de hello aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="5246d-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="5246d-164">nueva versión de Hello de aplicación hello ahora cuenta solo las palabras que empiecen por una vocal.</span><span class="sxs-lookup"><span data-stu-id="5246d-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="5246d-165">Tal y como se implementa la actualización de hello, veremos dos cambios de comportamiento de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="5246d-166">En primer lugar, debe lenta tasa de hello en el que aumenta el recuento de hello, puesto que están siendo contados breves.</span><span class="sxs-lookup"><span data-stu-id="5246d-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="5246d-167">En segundo lugar, puesto que la primera partición de hello tiene las dos vocales (A y E) y todas las demás particiones sólo contienen cada, su recuento finalmente inicie toooutpace Hola otros.</span><span class="sxs-lookup"><span data-stu-id="5246d-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="5246d-168">[Descargar paquete de la versión 2 de hello WordCount](http://aka.ms/servicefabric-wordcountappv2) toohello misma ubicación donde descargó el paquete de la versión 1 de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="5246d-169">Devolver tooyour ventana de PowerShell y utilice el comando de actualización del SDK de hello tooregister Hola la nueva versión en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="5246d-170">A continuación, comience a actualizar fabric hello: / aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="5246d-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="5246d-171">Debería ver Hola siguiente de PowerShell como Hola actualización comienza.</span><span class="sxs-lookup"><span data-stu-id="5246d-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Progreso de la actualización en PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="5246d-173">Mientras está actualización hello, quizá le resulte más fácil toomonitor su estado desde el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5246d-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="5246d-174">Inicie una ventana del explorador y navegue demasiado[http://localhost:19080/explorador](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="5246d-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="5246d-175">Expanda **aplicaciones** en árbol Hola Hola izquierda, a continuación, elija **WordCount**y, finalmente, **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="5246d-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="5246d-176">En la ficha de essentials hello, verá Hola estado de actualización de hello mientras pasa a través de dominios de actualización del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Progreso de la actualización en el Explorador de Service Fabric][sfx-upgradeprogress]
   
    <span data-ttu-id="5246d-178">Tal y como se realiza la actualización de Hola a través de cada dominio, las comprobaciones de mantenimiento son realizada tooensure que aplicación hello se comporta correctamente.</span><span class="sxs-lookup"><span data-stu-id="5246d-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="5246d-179">Si vuelve a ejecutar Hola anteriormente de consulta de conjunto de hello de servicios en el tejido de hello: / aplicación WordCount, tenga en cuenta que Hola versión WordCountService cambiado pero Hola versión WordCountWebService no:</span><span class="sxs-lookup"><span data-stu-id="5246d-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar servicios de aplicación después de la actualización][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="5246d-181">Este ejemplo resalta cómo Service Fabric administra las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5246d-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="5246d-182">Modifica solo Hola conjunto de servicios (o paquetes de código o de configuración dentro de esos servicios) que han cambiado, lo que hace el proceso de Hola de actualización más rápidas y confiables.</span><span class="sxs-lookup"><span data-stu-id="5246d-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="5246d-183">Por último, devuelve el comportamiento del toohello explorador tooobserve hello de la nueva versión de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="5246d-184">Como se esperaba, Hola más lentamente que progresa de recuento y Hola primera partición termine con un poco más de volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Nueva versión de hello de vista de la aplicación hello en el Explorador de Hola][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="5246d-186">Limpiar</span><span class="sxs-lookup"><span data-stu-id="5246d-186">Cleaning up</span></span>
<span data-ttu-id="5246d-187">Antes de ajustar la, es importante tooremember que Hola clúster local es real.</span><span class="sxs-lookup"><span data-stu-id="5246d-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="5246d-188">Las aplicaciones seguirán toorun en segundo plano de hello hasta que se quiten.</span><span class="sxs-lookup"><span data-stu-id="5246d-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="5246d-189">Según la naturaleza Hola de las aplicaciones, una aplicación en ejecución puede ocupar recursos significativos en su equipo.</span><span class="sxs-lookup"><span data-stu-id="5246d-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="5246d-190">Tiene varias aplicaciones de toomanage de opciones y clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="5246d-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="5246d-191">tooremove una aplicación individual y todos de datos, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="5246d-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="5246d-192">O bien, elimine la aplicación hello de hello Service Fabric Explorer **acciones** u Hola menú contextual en la vista de lista de hello aplicación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="5246d-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Eliminación de una aplicación en el explorador de Service Fabric][sfe-delete-application]
2. <span data-ttu-id="5246d-194">Después de eliminar la aplicación hello de clúster de hello, anular el registro de las versiones 1.0.0 y 2.0.0 del tipo de aplicación WordCount Hola.</span><span class="sxs-lookup"><span data-stu-id="5246d-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="5246d-195">La eliminación quita los paquetes de aplicaciones de hello, incluidos el código de hello y configuración del clúster de hello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="5246d-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="5246d-196">O bien, en el Explorador de tejido de servicio, elija **anule tipo** para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="5246d-197">tooshut hacia abajo clúster Hola pero mantener datos de la aplicación de Hola y seguimientos, haga clic en **detener clúster Local** en la aplicación de bandeja del sistema de hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="5246d-198">por completo, haga clic en el clúster de hello toodelete **quitar clúster Local** en la aplicación de bandeja del sistema de hello.</span><span class="sxs-lookup"><span data-stu-id="5246d-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="5246d-199">Esta opción se producirá otro Hola lenta implementación próxima vez que presiones F5 en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5246d-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="5246d-200">Quitar clúster local de hello solo si no piensa toouse durante algún tiempo o si necesita recursos tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="5246d-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="5246d-201">Modo de clúster de uno y cinco nodos</span><span class="sxs-lookup"><span data-stu-id="5246d-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="5246d-202">Al desarrollar aplicaciones, a menudo se encuentra realizando iteraciones rápidas de escritura de código, depuración, cambio de código y depuración.</span><span class="sxs-lookup"><span data-stu-id="5246d-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="5246d-203">toohelp optimizar este proceso, puede ejecutar el clúster local de hello en dos modos: uno o cinco nodos.</span><span class="sxs-lookup"><span data-stu-id="5246d-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="5246d-204">Ambos modos de clúster tienen sus ventajas.</span><span class="sxs-lookup"><span data-stu-id="5246d-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="5246d-205">El modo de clúster de cinco nodos permite toowork con un clúster real.</span><span class="sxs-lookup"><span data-stu-id="5246d-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="5246d-206">Puede probar escenarios de conmutación por error, trabajar con más instancias y réplicas de los servicios.</span><span class="sxs-lookup"><span data-stu-id="5246d-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="5246d-207">Modo de clúster de un nodo es una implementación rápida toodo optimizada y el registro de servicios, toohelp rápidamente valide el código con el tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5246d-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="5246d-208">Ni el modo de clúster de un nodo ni el de cinco nodos es un emulador o un simulador.</span><span class="sxs-lookup"><span data-stu-id="5246d-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="5246d-209">clúster de desarrollo local Hola ejecuciones Hola mismo código de plataforma que se encuentra en los clústeres de varios equipos.</span><span class="sxs-lookup"><span data-stu-id="5246d-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="5246d-210">Al cambiar el modo de clúster de hello, el clúster actual Hola se quita de su sistema y se crea un nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="5246d-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="5246d-211">datos de Hello almacenados en el clúster de Hola se eliminan cuando se cambia el modo de clúster.</span><span class="sxs-lookup"><span data-stu-id="5246d-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="5246d-212">toochange Hola modo tooone clúster de nodo, seleccione **modo de clúster de conmutación** Hola Administrador de clústeres Local de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5246d-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Cambio del modo de clúster][switch-cluster-mode]

<span data-ttu-id="5246d-214">O bien, cambiar el modo de clúster de hello con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5246d-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="5246d-215">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="5246d-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="5246d-216">Ejecute el script de instalación de clúster de Hola desde la carpeta del SDK de hello:</span><span class="sxs-lookup"><span data-stu-id="5246d-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="5246d-217">La instalación del clúster tardará unos instantes.</span><span class="sxs-lookup"><span data-stu-id="5246d-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="5246d-218">Una vez finalizada la instalación, debería ver una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="5246d-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Salida de instalación de clúster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="5246d-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5246d-220">Next steps</span></span>
* <span data-ttu-id="5246d-221">Tras la implementación y actualización de algunas aplicaciones pregeneradas, puede [intentar compilar la suya propia en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5246d-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="5246d-222">Todas las acciones de hello llevadas a cabo en el clúster local de hello en este artículo pueden realizarse en un [clúster Azure](service-fabric-cluster-creation-via-portal.md) así.</span><span class="sxs-lookup"><span data-stu-id="5246d-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="5246d-223">actualización de Hola que hemos realizado en este artículo era básica.</span><span class="sxs-lookup"><span data-stu-id="5246d-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="5246d-224">Vea hello [documentación de actualización](service-fabric-application-upgrade.md) toolearn más información acerca de hello potencia y flexibilidad de las actualizaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5246d-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
