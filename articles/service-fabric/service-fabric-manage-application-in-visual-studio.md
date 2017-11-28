---
title: "Administración de las aplicaciones en Visual Studio | Microsoft Docs"
description: Use Visual Studio para crear, desarrollar, empaquetar, implementar y depurar las aplicaciones y servicios de Service Fabric.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="1940d-103">Uso de Visual Studio para simplificar la escritura y la administración de las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="1940d-104">Puede administrar los servicios y aplicaciones de Service Fabric de Azure a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1940d-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="1940d-105">Cuando haya [configurado su entorno de desarrollo](service-fabric-get-started.md), puede usar Visual Studio para crear aplicaciones de Service Fabric, agregar servicios, o empaquetar, registrar e implementar aplicaciones en el clúster de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="1940d-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="1940d-106">Implementar la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="1940d-107">De forma predeterminada, la implementación de una aplicación combina los pasos siguientes en una operación sencilla:</span><span class="sxs-lookup"><span data-stu-id="1940d-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="1940d-108">Creación del paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="1940d-108">Creating the application package</span></span>
2. <span data-ttu-id="1940d-109">Carga del paquete de aplicación en el almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="1940d-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="1940d-110">Registro del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="1940d-110">Registering the application type</span></span>
4. <span data-ttu-id="1940d-111">Eliminación de cualquier instancia de aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="1940d-111">Removing any running application instances</span></span>
5. <span data-ttu-id="1940d-112">Creación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="1940d-112">Creating an application instance</span></span>

<span data-ttu-id="1940d-113">En Visual Studio, al presionar **F5** se implementará su aplicación y se asociará el depurador a todas las instancias de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="1940d-114">Puede usar **CTRL+F5** para implementar una aplicación sin depurar o bien, publicar en un clúster local o remoto mediante el perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="1940d-115">Para obtener más información, consulte [Publicación de una aplicación en un clúster remoto con Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1940d-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="1940d-116">Application Debug Mode</span><span class="sxs-lookup"><span data-stu-id="1940d-116">Application Debug Mode</span></span>
<span data-ttu-id="1940d-117">Visual Studio proporciona una propiedad llamada **Application Debug Mode**, que controla cómo desea que Visual Studio controle la implementación de la aplicación como parte de la depuración.</span><span class="sxs-lookup"><span data-stu-id="1940d-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="1940d-118">Establecimiento de la propiedad Application Debug Mode</span><span class="sxs-lookup"><span data-stu-id="1940d-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="1940d-119">En el menú de acceso directo del proyecto de la aplicación de Service Fabric (*.sfproj), elija **Propiedades** (o presione la tecla **F4**).</span><span class="sxs-lookup"><span data-stu-id="1940d-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="1940d-120">En la ventana **Propiedades**, establezca la propiedad **Application Debug Mode** (Modo de depuración de aplicación).</span><span class="sxs-lookup"><span data-stu-id="1940d-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Establecer la propiedad Application Debug Mode][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="1940d-122">Modos de depuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1940d-122">Application Debug Modes</span></span>

1. <span data-ttu-id="1940d-123">**Actualizar aplicación** Este modo le permite cambiar y depurar su código rápidamente y permite editar archivos web estáticos durante la depuración.</span><span class="sxs-lookup"><span data-stu-id="1940d-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="1940d-124">Este modo solo funciona si el clúster de desarrollo local está en [modo 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="1940d-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="1940d-125">**Quitar aplicación** : la aplicación se quita cuando finaliza la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="1940d-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="1940d-126">**Actualización automática** La aplicación continúa ejecutándose cuando finaliza la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="1940d-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="1940d-127">La siguiente sesión de depuración tratará la implementación como una actualización.</span><span class="sxs-lookup"><span data-stu-id="1940d-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="1940d-128">El proceso de actualización conserva todos los datos especificados en una sesión de depuración anterior.</span><span class="sxs-lookup"><span data-stu-id="1940d-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="1940d-129">**Mantener aplicación** La aplicación sigue ejecutándose en el clúster cuando finaliza la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="1940d-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="1940d-130">Al principio de la siguiente sesión de depuración, se eliminará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="1940d-131">Se conservan los datos de **Actualización automática** por medio de las funcionalidades de actualización de aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1940d-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="1940d-132">Para obtener más información sobre la actualización de aplicaciones y cómo se realiza una actualización en un entorno real, consulte [Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1940d-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="1940d-133">Agregue un servicio a su aplicación Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="1940d-134">Puede agregar nuevos servicios a su aplicación para ampliar su funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1940d-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="1940d-135">Para garantizar que el servicio se incluye en el paquete de aplicación, agregue el servicio a través del elemento de menú **Nuevo servicio del tejido...** .</span><span class="sxs-lookup"><span data-stu-id="1940d-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Agregar un nuevo servicio de Service Fabric][newservice]

<span data-ttu-id="1940d-137">Seleccione un tipo de proyecto de Service Fabric para agregarlo a la aplicación y especifique un nombre para el servicio.</span><span class="sxs-lookup"><span data-stu-id="1940d-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="1940d-138">Vea [Elección de un marco para el servicio](service-fabric-choose-framework.md) para ayudarle a decidir qué tipo de servicio quiere usar.</span><span class="sxs-lookup"><span data-stu-id="1940d-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Seleccione un tipo de proyecto de servicio de Service Fabric para agregarlo a la aplicación][addserviceproject]

<span data-ttu-id="1940d-140">El nuevo servicio se agrega a la solución y al paquete de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="1940d-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="1940d-141">Se agregarán al manifiesto de la aplicación las referencias del servicio y una instancia del servicio predeterminada, haciendo que el servicio se cree y se inicie la próxima vez que implemente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![Se agrega el nuevo servicio al manifiesto de la aplicación][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="1940d-143">Empaquetar la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-143">Package your Service Fabric application</span></span>
<span data-ttu-id="1940d-144">Para implementar la aplicación y sus servicios en un clúster, debe crear una paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="1940d-145">El paquete organiza el manifiesto de la aplicación, los manifiestos de servicio y otros archivos necesarios en un diseño específico.</span><span class="sxs-lookup"><span data-stu-id="1940d-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="1940d-146">Visual Studio configura y administra el paquete en la carpeta del proyecto de aplicación, en el directorio 'pkg'.</span><span class="sxs-lookup"><span data-stu-id="1940d-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="1940d-147">Haga clic en **Paquete** en el menú contextual **Aplicación** para crear o actualizar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1940d-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="1940d-148">Eliminación de aplicaciones y tipos de aplicación mediante Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="1940d-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="1940d-149">Puede realizar operaciones básicas de administración de clúster desde Visual Studio mediante Cloud Explorer, que se puede iniciar desde el menú **Vista** .</span><span class="sxs-lookup"><span data-stu-id="1940d-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="1940d-150">Por ejemplo, puede eliminar aplicaciones y deshacer el aprovisionamiento de tipos de aplicación en clústeres locales o remotos.</span><span class="sxs-lookup"><span data-stu-id="1940d-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Eliminación de una aplicación][removeapplication]

> [!TIP]
> <span data-ttu-id="1940d-152">Para obtener una mejor funcionalidad de administración de clúster, consulte [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1940d-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="1940d-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1940d-153">Next steps</span></span>
* [<span data-ttu-id="1940d-154">Modelo de aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="1940d-155">Implementación de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="1940d-156">Administración de los parámetros de la aplicación en varios entornos</span><span class="sxs-lookup"><span data-stu-id="1940d-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="1940d-157">Depuración de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="1940d-158">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1940d-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png