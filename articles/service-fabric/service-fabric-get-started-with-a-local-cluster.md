---
title: "Implementación y actualización local de microservicios de Azure | Microsoft Docs"
description: "Aprenda a configurar un clúster local de Service Fabric, implementar una aplicación existente en él y actualizar dicha aplicación."
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
ms.openlocfilehash: 359677972c7e1fa3f7435052021ddfae5b1ed85e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="b67c9-103">Introducción a la implementación y actualización de aplicaciones en un clúster local</span><span class="sxs-lookup"><span data-stu-id="b67c9-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="b67c9-104">El SDK de Service Fabric de Azure incluye un completo entorno de desarrollo local y puede usar para empezar a trabajar rápidamente con aplicaciones de implementación y administración en un clúster local.</span><span class="sxs-lookup"><span data-stu-id="b67c9-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="b67c9-105">En este artículo, se crea un clúster local, se implementa en él una aplicación existente y, a continuación, se actualiza la aplicación a una nueva versión, y todo ello desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b67c9-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b67c9-106">En este artículo se asume que ya [configuró un entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b67c9-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="b67c9-107">Creación de un clúster local</span><span class="sxs-lookup"><span data-stu-id="b67c9-107">Create a local cluster</span></span>
<span data-ttu-id="b67c9-108">Un clúster de Service Fabric representa un conjunto de recursos de hardware en los que se pueden implementar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b67c9-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="b67c9-109">Normalmente, un clúster se compone de cualquier número entre cinco y varios miles de máquinas.</span><span class="sxs-lookup"><span data-stu-id="b67c9-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="b67c9-110">Sin embargo, el SDK de Service Fabric incluye una configuración de clúster que se puede ejecutar en una única máquina.</span><span class="sxs-lookup"><span data-stu-id="b67c9-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="b67c9-111">Es importante comprender que el clúster local de Service Fabric no es un emulador o simulador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="b67c9-112">Ejecuta el mismo código de plataforma que se encuentra en clústeres de varias máquinas.</span><span class="sxs-lookup"><span data-stu-id="b67c9-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="b67c9-113">La única diferencia es que ejecuta en una única máquina los procesos de plataforma que suelen estar dispersos en cinco máquinas.</span><span class="sxs-lookup"><span data-stu-id="b67c9-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="b67c9-114">El SDK proporciona dos maneras de configurar un clúster local: un script de Windows PowerShell y la aplicación de bandeja del sistema del Administrador de clústeres locales.</span><span class="sxs-lookup"><span data-stu-id="b67c9-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="b67c9-115">En este tutorial, usaremos el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b67c9-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="b67c9-116">Si creó un clúster local mediante la implementación de una aplicación desde Visual Studio, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="b67c9-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="b67c9-117">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b67c9-118">Ejecute el script de instalación del clúster desde la carpeta del SDK:</span><span class="sxs-lookup"><span data-stu-id="b67c9-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="b67c9-119">La instalación del clúster tardará unos instantes.</span><span class="sxs-lookup"><span data-stu-id="b67c9-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b67c9-120">Una vez finalizada la instalación, debería ver una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="b67c9-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Salida de instalación de clúster][cluster-setup-success]
   
    <span data-ttu-id="b67c9-122">Ya está listo para intentar implementar una aplicación en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b67c9-123">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="b67c9-123">Deploy an application</span></span>
<span data-ttu-id="b67c9-124">El SDK de Service Fabric incluye un amplio conjunto de marcos y herramientas para desarrolladores para crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b67c9-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="b67c9-125">Si está interesado en aprender a crear aplicaciones en Visual Studio, consulte [Creación de la primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b67c9-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="b67c9-126">En este tutorial, se usará una aplicación de ejemplo existente (llamada WordCount) de forma que puada centrarse en los aspectos de administración de la plataforma: implementación, supervisión y actualización.</span><span class="sxs-lookup"><span data-stu-id="b67c9-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="b67c9-127">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b67c9-128">Importe el módulo de PowerShell del SDK de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="b67c9-129">Cree un directorio para almacenar la aplicación que va a descargar e implementar, por ejemplo, C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="b67c9-130">[Descargue la aplicación WordCount](http://aka.ms/servicefabric-wordcountapp) en la ubicación que creó.</span><span class="sxs-lookup"><span data-stu-id="b67c9-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="b67c9-131">Nota: el explorador Microsoft Edge guarda el archivo con extensión *.zip* .</span><span class="sxs-lookup"><span data-stu-id="b67c9-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="b67c9-132">Debe cambiar la extensión del archivo a *.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="b67c9-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="b67c9-133">Conecte con el clúster local:</span><span class="sxs-lookup"><span data-stu-id="b67c9-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="b67c9-134">Cree una nueva aplicación mediante el comando de implementación del SDK, con un nombre y una ruta de acceso al paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b67c9-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b67c9-135">Si todo va bien, debería ver el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="b67c9-135">If all goes well, you should see the following output:</span></span>
   
    ![Implementación de una aplicación en el clúster local][deploy-app-to-local-cluster]
7. <span data-ttu-id="b67c9-137">Para ver la aplicación en acción, inicie el explorador y vaya a [http://localhost:8081/wordcount/índex.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="b67c9-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="b67c9-138">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b67c9-138">You should see:</span></span>
   
    ![Interfaz de usuario de aplicación implementada][deployed-app-ui]
   
    <span data-ttu-id="b67c9-140">La aplicación WordCount es sencilla.</span><span class="sxs-lookup"><span data-stu-id="b67c9-140">The WordCount application is simple.</span></span> <span data-ttu-id="b67c9-141">Incluye código JavaScript del lado cliente para generar "palabras" aleatorias de cinco caracteres, que, posteriormente, se retransmiten a la aplicación mediante ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="b67c9-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="b67c9-142">Un servicio con estado realiza el seguimiento del recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="b67c9-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="b67c9-143">Se crean particiones basadas en el primer carácter de la palabra.</span><span class="sxs-lookup"><span data-stu-id="b67c9-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="b67c9-144">El código fuente de la aplicación WordCount se puede encontrar en los [ejemplos de introducción clásicos](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="b67c9-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="b67c9-145">La aplicación que hemos implementado contiene cuatro particiones.</span><span class="sxs-lookup"><span data-stu-id="b67c9-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="b67c9-146">Por tanto las palabras que empiezan de la A a la G se almacenan en la primera partición, las que comienzan de la H a la N en la segunda partición, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="b67c9-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="b67c9-147">Visualización de los detalles y estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b67c9-147">View application details and status</span></span>
<span data-ttu-id="b67c9-148">Ahora que hemos implementado la aplicación, echemos un vistazo a algunos de los detalles de la aplicación en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b67c9-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="b67c9-149">Consulte todas las aplicaciones implementadas en el clúster:</span><span class="sxs-lookup"><span data-stu-id="b67c9-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="b67c9-150">Si solo implementó la aplicación WordCount, verá algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="b67c9-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![Consultar todas las aplicaciones implementadas en PowerShell][ps-getsfapp]
2. <span data-ttu-id="b67c9-152">Vaya al siguiente nivel, para lo que debe consultar el conjunto de servicios incluidos en la aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="b67c9-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Enumeración de servicios de la aplicación en PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="b67c9-154">La aplicación consta de dos servicios: el front-end web y el servicio con estado que administra las palabras.</span><span class="sxs-lookup"><span data-stu-id="b67c9-154">The application is made up of two services, the web front end, and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="b67c9-155">Por último, eche un vistazo a la lista de particiones de WordCountService:</span><span class="sxs-lookup"><span data-stu-id="b67c9-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Ver las particiones de servicio en PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="b67c9-157">El conjunto de comandos que ha usado, al igual que todos los comandos de PowerShell de Service Fabric, están disponibles para cualquier clúster al que se pueda conectar, tanto local como remoto.</span><span class="sxs-lookup"><span data-stu-id="b67c9-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="b67c9-158">Si desea interactuar con el clúster de una forma más visual, puede usar la herramienta Explorador de Service Fabric basada en web, para lo que debe navegar a [http://localhost:19080/Explorer](http://localhost:19080/Explorer) en el explorador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![Ver detalles de aplicación en el Explorador de Service Fabric][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="b67c9-160">Para más información acerca de Service Fabric Explorer, consulte [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b67c9-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="b67c9-161">Actualizar una aplicación</span><span class="sxs-lookup"><span data-stu-id="b67c9-161">Upgrade an application</span></span>
<span data-ttu-id="b67c9-162">Service Fabric proporciona actualizaciones sin tiempo de inactividad mediante la supervisión del estado de la aplicación cuando se implementa en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="b67c9-163">Realice una actualización de la aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="b67c9-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="b67c9-164">La nueva versión de la aplicación ahora contará solo las palabras que comiencen por vocal.</span><span class="sxs-lookup"><span data-stu-id="b67c9-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="b67c9-165">Cuando se implemente la actualización, veremos dos cambios en el comportamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b67c9-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="b67c9-166">En primer lugar, la velocidad a la que crece el recuento debe reducirse, ya que se cuentan menos palabras.</span><span class="sxs-lookup"><span data-stu-id="b67c9-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="b67c9-167">En segundo lugar, dado que la primera partición tiene dos vocales (A y E) y las restantes particiones contienen solo una, su recuento debería finalmente debería empezar a superar a los demás.</span><span class="sxs-lookup"><span data-stu-id="b67c9-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="b67c9-168">[Descargue el paquete de WordCount versión 2](http://aka.ms/servicefabric-wordcountappv2) en la misma ubicación en la que descargó el paquete de la versión 1.</span><span class="sxs-lookup"><span data-stu-id="b67c9-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="b67c9-169">Vuelva a la ventana de PowerShell y use el comando de actualización del SDK para registrar la nueva versión en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="b67c9-170">Después, empiece a actualizar la aplicación fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="b67c9-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="b67c9-171">Debería ver el siguiente resultado en PowerShell cuando comience la actualización.</span><span class="sxs-lookup"><span data-stu-id="b67c9-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![Progreso de la actualización en PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="b67c9-173">Mientras que la actualización se lleva a cabo, le resultará más fácil supervisar su estado desde el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="b67c9-174">Inicie una ventana del explorador y navegue a [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="b67c9-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="b67c9-175">Expanda **Aplicaciones** en el árbol de la izquierda, elija **WordCount** y finalmente **fabric:/WordCount**.</span><span class="sxs-lookup"><span data-stu-id="b67c9-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="b67c9-176">En la pestaña de información básica, verá el estado de la actualización mientras progresa por los dominios de actualización del clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![Progreso de la actualización en el Explorador de Service Fabric][sfx-upgradeprogress]
   
    <span data-ttu-id="b67c9-178">Mientras se realiza la actualización en cada dominio, se realizan comprobaciones de mantenimiento para asegurarse de que la aplicación se comporta correctamente.</span><span class="sxs-lookup"><span data-stu-id="b67c9-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="b67c9-179">Si vuelve a ejecutar la consulta anterior en el conjunto de servicios de la aplicación fabric:/WordCount, observará que cambió la versión de WordCountService, pero no la de WordCountWebService:</span><span class="sxs-lookup"><span data-stu-id="b67c9-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar servicios de aplicación después de la actualización][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="b67c9-181">Este ejemplo resalta cómo Service Fabric administra las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b67c9-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="b67c9-182">Toca solo el conjunto de servicios (o los paquetes de código/configuración de dichos servicios) que cambiaron, lo que hace que el proceso de actualización sea más rápido y confiable.</span><span class="sxs-lookup"><span data-stu-id="b67c9-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="b67c9-183">Por último, vuelva al explorador para observar el comportamiento de la nueva versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b67c9-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="b67c9-184">Como se esperaba, el recuento avanza más lentamente y la primera partición termina con un poco más del volumen.</span><span class="sxs-lookup"><span data-stu-id="b67c9-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![Ver la nueva versión de la aplicación en el explorador][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="b67c9-186">Limpiar</span><span class="sxs-lookup"><span data-stu-id="b67c9-186">Cleaning up</span></span>
<span data-ttu-id="b67c9-187">Antes de concluir, es importante recordar que el clúster local es real.</span><span class="sxs-lookup"><span data-stu-id="b67c9-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="b67c9-188">Las aplicaciones seguirán ejecutándose en segundo plano hasta que se quiten.</span><span class="sxs-lookup"><span data-stu-id="b67c9-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="b67c9-189">Según la naturaleza de las aplicaciones, una aplicación en ejecución puede consumir importantes recursos en su máquina.</span><span class="sxs-lookup"><span data-stu-id="b67c9-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="b67c9-190">Tiene varias opciones para administrar aplicaciones y el clúster:</span><span class="sxs-lookup"><span data-stu-id="b67c9-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="b67c9-191">Para quitar una aplicación determinada y todos sus datos, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b67c9-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b67c9-192">O bien, elimine la aplicación del menú **ACCIONES** de Service Fabric Explorer o del menú contextual en la vista de lista de aplicaciones del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="b67c9-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![Eliminación de una aplicación en el explorador de Service Fabric][sfe-delete-application]
2. <span data-ttu-id="b67c9-194">Después de eliminar la aplicación del clúster, puede anular el registro de las versiones 1.0.0 y 2.0.0 del tipo de aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="b67c9-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="b67c9-195">La eliminación quita del almacén de imágenes del clúster los paquetes de la aplicación, incluido el código y la configuración.</span><span class="sxs-lookup"><span data-stu-id="b67c9-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="b67c9-196">También puede seleccionar **Unprovision Type** (Tipo de anulación de aprovisionamiento) para la aplicación en Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b67c9-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="b67c9-197">Para cerrar el clúster pero mantener los datos y los seguimientos de la aplicación, haga clic en **Stop Local Cluster** (Detener clúster local) en la aplicación de bandeja del sistema.</span><span class="sxs-lookup"><span data-stu-id="b67c9-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="b67c9-198">Para eliminar totalmente el clúster, haga clic en **Remove Local Cluster** (Quitar clúster local) en la aplicación de la bandeja del sistema.</span><span class="sxs-lookup"><span data-stu-id="b67c9-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="b67c9-199">Esta opción generará otra implementación lenta la próxima vez que presione F5 en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b67c9-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="b67c9-200">Quite el clúster local solo si no tiene intención utilizarlo durante algún tiempo o si necesita reclamar recursos.</span><span class="sxs-lookup"><span data-stu-id="b67c9-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="b67c9-201">Modo de clúster de uno y cinco nodos</span><span class="sxs-lookup"><span data-stu-id="b67c9-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="b67c9-202">Al desarrollar aplicaciones, a menudo se encuentra realizando iteraciones rápidas de escritura de código, depuración, cambio de código y depuración.</span><span class="sxs-lookup"><span data-stu-id="b67c9-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="b67c9-203">Para ayudar a optimizar este proceso, el clúster local se puede ejecutar de dos modos: con uno o cinco nodos.</span><span class="sxs-lookup"><span data-stu-id="b67c9-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="b67c9-204">Ambos modos de clúster tienen sus ventajas.</span><span class="sxs-lookup"><span data-stu-id="b67c9-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="b67c9-205">El modo de clúster de cinco nodos le permite trabajar con un clúster real.</span><span class="sxs-lookup"><span data-stu-id="b67c9-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="b67c9-206">Puede probar escenarios de conmutación por error, trabajar con más instancias y réplicas de los servicios.</span><span class="sxs-lookup"><span data-stu-id="b67c9-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="b67c9-207">El modo de clúster de un nodo está optimizado para la implementación y el registro de servicios de forma rápida, para ayudarle a validar rápidamente el código mediante el entorno de tiempo de ejecución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="b67c9-208">Ni el modo de clúster de un nodo ni el de cinco nodos es un emulador o un simulador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="b67c9-209">El clúster de desarrollo local ejecuta el mismo código de plataforma que se encuentra en los clústeres de varias máquinas.</span><span class="sxs-lookup"><span data-stu-id="b67c9-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="b67c9-210">Al cambiar el modo de clúster, el clúster actual se quita del sistema y se crea un nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="b67c9-211">Cuando se cambia el modo de clúster, se eliminan los datos almacenados en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b67c9-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="b67c9-212">Para cambiar al modo de clúster de un nodo, seleccione **Switch Cluster Mode** (Cambiar modo de clúster) en la instancia local de Cluster Manager de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![Cambio del modo de clúster][switch-cluster-mode]

<span data-ttu-id="b67c9-214">O bien, cambie el modo de clúster mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b67c9-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="b67c9-215">Inicie una ventana nueva de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="b67c9-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b67c9-216">Ejecute el script de instalación del clúster desde la carpeta del SDK:</span><span class="sxs-lookup"><span data-stu-id="b67c9-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="b67c9-217">La instalación del clúster tardará unos instantes.</span><span class="sxs-lookup"><span data-stu-id="b67c9-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b67c9-218">Una vez finalizada la instalación, debería ver una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="b67c9-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Salida de instalación de clúster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="b67c9-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b67c9-220">Next steps</span></span>
* <span data-ttu-id="b67c9-221">Tras la implementación y actualización de algunas aplicaciones pregeneradas, puede [intentar compilar la suya propia en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b67c9-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="b67c9-222">Todas las acciones realizadas en el clúster local en este artículo se pueden realizar también en un [clúster de Azure](service-fabric-cluster-creation-via-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="b67c9-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="b67c9-223">La actualización realizada en este artículo era básica.</span><span class="sxs-lookup"><span data-stu-id="b67c9-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="b67c9-224">Consulte la [documentación de actualización](service-fabric-application-upgrade.md) para más información acerca de la eficacia y flexibilidad de las actualizaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b67c9-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

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
