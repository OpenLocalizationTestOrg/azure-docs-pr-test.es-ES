---
title: aaaManage sus aplicaciones en Visual Studio | Documentos de Microsoft
description: Usar Visual Studio toocreate, desarrollar, paquete, implementar y depurar los servicios y aplicaciones de Service Fabric.
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
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="d26cc-103">Utilizar la escritura de toosimplify de Visual Studio y administrar las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="d26cc-104">Puede administrar los servicios y aplicaciones de Service Fabric de Azure a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d26cc-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="d26cc-105">Una vez que se haya [configurar el entorno de desarrollo](service-fabric-get-started.md), puede utilizar aplicaciones de Service Fabric toocreate de Visual Studio, agregar servicios, o un paquete, registro e implementar aplicaciones en el clúster de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="d26cc-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="d26cc-106">Implementar la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="d26cc-107">De forma predeterminada, implementar una aplicación combina Hola siguiendo los pasos en una operación sencilla:</span><span class="sxs-lookup"><span data-stu-id="d26cc-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="d26cc-108">Crear paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d26cc-108">Creating hello application package</span></span>
2. <span data-ttu-id="d26cc-109">Almacén de imágenes de toohello de paquete de aplicación de carga Hola</span><span class="sxs-lookup"><span data-stu-id="d26cc-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="d26cc-110">Registrar el tipo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d26cc-110">Registering hello application type</span></span>
4. <span data-ttu-id="d26cc-111">Eliminación de cualquier instancia de aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="d26cc-111">Removing any running application instances</span></span>
5. <span data-ttu-id="d26cc-112">Creación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="d26cc-112">Creating an application instance</span></span>

<span data-ttu-id="d26cc-113">En Visual Studio, al presionar **F5** implementa la aplicación y adjuntar a instancias de la aplicación hello depurador tooall.</span><span class="sxs-lookup"><span data-stu-id="d26cc-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="d26cc-114">Puede usar **CTRL+F5** toodeploy una aplicación sin depurar o puede publicar tooa local o remota de clúster mediante el uso de hello perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="d26cc-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="d26cc-115">Para obtener más información, consulte [publicar un clúster remoto tooa de aplicación mediante Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d26cc-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="d26cc-116">Application Debug Mode</span><span class="sxs-lookup"><span data-stu-id="d26cc-116">Application Debug Mode</span></span>
<span data-ttu-id="d26cc-117">Visual Studio proporciona una propiedad denominada **modo de depuración de la aplicación**, que controla cómo desea que la implementación de aplicaciones de Visual Studio toohandle como parte de la depuración.</span><span class="sxs-lookup"><span data-stu-id="d26cc-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="d26cc-118">Hola tooset propiedad modo de depuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d26cc-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="d26cc-119">En hello Service Fabric aplicación del proyecto (*.sfproj) menú contextual, elija **propiedades** (o presione hello **F4** clave).</span><span class="sxs-lookup"><span data-stu-id="d26cc-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="d26cc-120">Hola **propiedades** (ventana), conjunto hello **modo de depuración de la aplicación** propiedad.</span><span class="sxs-lookup"><span data-stu-id="d26cc-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Establecer la propiedad Application Debug Mode][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="d26cc-122">Modos de depuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d26cc-122">Application Debug Modes</span></span>

1. <span data-ttu-id="d26cc-123">**Actualizar aplicación** este modo le permite cambiar de tooquickly y depurar su código y permite editar archivos web estáticos durante la depuración.</span><span class="sxs-lookup"><span data-stu-id="d26cc-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="d26cc-124">Este modo solo funciona si el clúster de desarrollo local está en [modo 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="d26cc-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="d26cc-125">**Quitar aplicación** causas Hola toobe de aplicación que se eliminan cuando finaliza la sesión de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="d26cc-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="d26cc-126">**Actualizarán automáticamente** aplicación hello continúa toorun cuando finaliza la sesión de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="d26cc-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="d26cc-127">Hello siguiente sesión de depuración tratará implementación hello como una actualización.</span><span class="sxs-lookup"><span data-stu-id="d26cc-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="d26cc-128">proceso de actualización de Hello conserva los datos que insertó en la sesión de depuración anterior.</span><span class="sxs-lookup"><span data-stu-id="d26cc-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="d26cc-129">**Mantener aplicaciones** Hola aplicación mantiene ejecutando en el clúster de hello cuando hello finaliza la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="d26cc-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="d26cc-130">Hola principio de hello siguiente sesión de depuración, se quitará la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d26cc-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="d26cc-131">Para **actualización automática** se conservan los datos mediante la aplicación de capacidades de actualización de aplicación Hola de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d26cc-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="d26cc-132">Para obtener más información sobre la actualización de aplicaciones y cómo se realiza una actualización en un entorno real, consulte [Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d26cc-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="d26cc-133">Agregar una aplicación de Service Fabric tooyour de servicio</span><span class="sxs-lookup"><span data-stu-id="d26cc-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="d26cc-134">Puede agregar nuevos servicios tooyour aplicación tooextend su funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="d26cc-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="d26cc-135">tooensure que el servicio de hello está incluido en el paquete de aplicación, agregue el servicio de Hola a través de hello **nuevo servicio de Fabric...**  elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="d26cc-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Agregar un nuevo servicio de Service Fabric][newservice]

<span data-ttu-id="d26cc-137">Seleccione una aplicación de tooyour Service Fabric tooadd de tipo de proyecto y especifique un nombre para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d26cc-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="d26cc-138">Vea [elegir un marco de trabajo para el servicio](service-fabric-choose-framework.md) toohelp decidir qué servicio escriba toouse.</span><span class="sxs-lookup"><span data-stu-id="d26cc-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Seleccione una aplicación Service Fabric servicio proyecto tipo tooadd tooyour][addserviceproject]

<span data-ttu-id="d26cc-140">se agrega nuevo servicio de Hello tooyour solución y paquete de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="d26cc-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="d26cc-141">Hola referencias de servicio y una instancia predeterminada del servicio será toohello agregado manifiesto de aplicación, lo que ha provocado Hola servicio toobe crea e inicia Hola vuela a que implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d26cc-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![nuevo servicio de Hola se agrega el manifiesto de aplicación tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="d26cc-143">Empaquetar la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-143">Package your Service Fabric application</span></span>
<span data-ttu-id="d26cc-144">aplicación de hello toodeploy y su clúster de tooa de servicios, deberá toocreate un paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26cc-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="d26cc-145">paquete de Hello organiza manifiesto de aplicación Hola, manifiestos de servicio y otros archivos necesarios en un diseño concreto.</span><span class="sxs-lookup"><span data-stu-id="d26cc-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="d26cc-146">Visual Studio configura y administra el paquete de hello en la carpeta del proyecto de aplicación de hello, en el directorio de hello 'pkg'.</span><span class="sxs-lookup"><span data-stu-id="d26cc-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="d26cc-147">Haga clic en **paquete** de hello **aplicación** crea el menú contextual o actualizaciones Hola paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26cc-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="d26cc-148">Eliminación de aplicaciones y tipos de aplicación mediante Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="d26cc-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="d26cc-149">Puede realizar operaciones de administración de clúster básico desde Visual Studio mediante el explorador en la nube, que también se puede iniciar desde hello **vista** menú.</span><span class="sxs-lookup"><span data-stu-id="d26cc-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="d26cc-150">Por ejemplo, puede eliminar aplicaciones y deshacer el aprovisionamiento de tipos de aplicación en clústeres locales o remotos.</span><span class="sxs-lookup"><span data-stu-id="d26cc-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Eliminación de una aplicación][removeapplication]

> [!TIP]
> <span data-ttu-id="d26cc-152">Para obtener una mejor funcionalidad de administración de clúster, consulte [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d26cc-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d26cc-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d26cc-153">Next steps</span></span>
* [<span data-ttu-id="d26cc-154">Modelo de aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="d26cc-155">Implementación de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="d26cc-156">Administración de los parámetros de la aplicación en varios entornos</span><span class="sxs-lookup"><span data-stu-id="d26cc-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="d26cc-157">Depuración de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="d26cc-158">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d26cc-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png