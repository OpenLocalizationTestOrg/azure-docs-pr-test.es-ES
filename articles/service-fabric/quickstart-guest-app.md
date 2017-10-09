---
title: "aaaQuickly implementar un clúster de Azure Service Fabric de tooan de aplicación existente"
description: "Usar un toohost de clúster de Azure Service Fabric una aplicación existente de Node.js con Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="f3183-103">Hospedaje de una aplicación de Node.js en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3183-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="f3183-104">Este inicio rápido le ayudará a implementar un clúster existente de Service Fabric de tooa de aplicación (Node.js en este ejemplo) se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="f3183-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3183-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f3183-105">Prerequisites</span></span>

<span data-ttu-id="f3183-106">Antes de comenzar, asegúrese de haber [configurado el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f3183-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="f3183-107">Que incluye la instalación de SDK del servicio de Fabric de Hola y 2017 de Visual Studio o 2015.</span><span class="sxs-lookup"><span data-stu-id="f3183-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="f3183-108">También debe toohave una aplicación existente de Node.js para la implementación.</span><span class="sxs-lookup"><span data-stu-id="f3183-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="f3183-109">Esta guía de rápido usa un sitio Web en Node.js simple que se puede descargar [aquí][download-sample].</span><span class="sxs-lookup"><span data-stu-id="f3183-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="f3183-110">Extraer este archivo tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` carpeta después de crear el proyecto de hello en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="f3183-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="f3183-111">Si no tiene una suscripción a Azure, cree una [cuenta gratuita][create-account].</span><span class="sxs-lookup"><span data-stu-id="f3183-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="f3183-112">Crear servicio Hola</span><span class="sxs-lookup"><span data-stu-id="f3183-112">Create hello service</span></span>

<span data-ttu-id="f3183-113">Inicie Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="f3183-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="f3183-114">Creación de un proyecto con `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="f3183-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="f3183-115">Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="f3183-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="f3183-116">Nombre de la aplicación hello **MyGuestApp** y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3183-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f3183-117">Node.js fácilmente puede interrumpir el límite de hello 260 caracteres para rutas de acceso que tiene windows.</span><span class="sxs-lookup"><span data-stu-id="f3183-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="f3183-118">Use una ruta de acceso corta propio proyecto de hello como **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="f3183-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Cuadro de diálogo de proyecto nuevo en Visual Studio.][new-project]

<span data-ttu-id="f3183-120">Puede crear cualquier tipo de servicio de Service Fabric del cuadro de diálogo siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f3183-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="f3183-121">Para esta guía de inicio rápido, elija **Archivo ejecutable invitado**.</span><span class="sxs-lookup"><span data-stu-id="f3183-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="f3183-122">Nombre de servicio de Hola **MyGuestService** y establecer opciones de hello en hello derecho toohello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="f3183-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="f3183-123">Configuración</span><span class="sxs-lookup"><span data-stu-id="f3183-123">Setting</span></span>                   | <span data-ttu-id="f3183-124">Valor</span><span class="sxs-lookup"><span data-stu-id="f3183-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="f3183-125">Carpeta del paquete de código</span><span class="sxs-lookup"><span data-stu-id="f3183-125">Code Package Folder</span></span>       | <span data-ttu-id="f3183-126">_&lt;carpeta de Hello con la aplicación Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="f3183-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="f3183-127">Comportamiento del paquete de código</span><span class="sxs-lookup"><span data-stu-id="f3183-127">Code Package Behavior</span></span>     | <span data-ttu-id="f3183-128">Copie la carpeta contenido tooproject</span><span class="sxs-lookup"><span data-stu-id="f3183-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="f3183-129">Programa</span><span class="sxs-lookup"><span data-stu-id="f3183-129">Program</span></span>                   | <span data-ttu-id="f3183-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="f3183-130">node.exe</span></span> |
| <span data-ttu-id="f3183-131">Argumentos</span><span class="sxs-lookup"><span data-stu-id="f3183-131">Arguments</span></span>                 | <span data-ttu-id="f3183-132">server.js</span><span class="sxs-lookup"><span data-stu-id="f3183-132">server.js</span></span> |
| <span data-ttu-id="f3183-133">Carpeta de trabajo</span><span class="sxs-lookup"><span data-stu-id="f3183-133">Working Folder</span></span>            | <span data-ttu-id="f3183-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="f3183-134">CodePackage</span></span> |

<span data-ttu-id="f3183-135">Presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3183-135">Press **OK**.</span></span>

![Cuadro de diálogo de servicio nuevo en Visual Studio.][new-service]

<span data-ttu-id="f3183-137">Visual Studio crea el proyecto de aplicación de Hola y un proyecto de servicio de actor hello y mostrarlos en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="f3183-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="f3183-138">proyecto de aplicación Hola (**MyGuestApp**) no contiene ningún código directamente.</span><span class="sxs-lookup"><span data-stu-id="f3183-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="f3183-139">En su lugar, hace referencia a un conjunto de proyectos de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3183-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="f3183-140">Además, contiene otros tres tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="f3183-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="f3183-141">**Perfiles de publicación**</span><span class="sxs-lookup"><span data-stu-id="f3183-141">**Publish profiles**</span></span>  
<span data-ttu-id="f3183-142">Preferencias en cuanto a las herramientas para los diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="f3183-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="f3183-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="f3183-143">**Scripts**</span></span>  
<span data-ttu-id="f3183-144">Script de PowerShell para implementar o actualizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f3183-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="f3183-145">**Definición de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="f3183-145">**Application definition**</span></span>  
<span data-ttu-id="f3183-146">Incluye el manifiesto de aplicación hello en *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="f3183-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="f3183-147">Archivos de parámetros de las aplicaciones asociadas están bajo *ApplicationParameters*, que definen la aplicación hello y le permiten tooconfigure específicamente para un entorno determinado.</span><span class="sxs-lookup"><span data-stu-id="f3183-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="f3183-148">Para obtener información general del contenido de Hola Hola del proyecto del servicio, consulte [Introducción a servicios de confianza](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="f3183-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="f3183-149">Configuración de las redes</span><span class="sxs-lookup"><span data-stu-id="f3183-149">Set up networking</span></span>

<span data-ttu-id="f3183-150">ejemplo de Hola aplicación Node.js nos estamos implementando utiliza el puerto **80** y necesitamos tootell Service Fabric que necesitamos que expone el puerto.</span><span class="sxs-lookup"><span data-stu-id="f3183-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="f3183-151">Abra hello **ServiceManifest.xml** archivo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3183-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="f3183-152">En parte inferior de hello del manifiesto de hello, hay una `<Resources> \ <Endpoints>` con una entrada ya definida.</span><span class="sxs-lookup"><span data-stu-id="f3183-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="f3183-153">Modificar esa entrada tooadd `Port`, `Protocol`, y `Type`.</span><span class="sxs-lookup"><span data-stu-id="f3183-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="f3183-154">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f3183-154">Deploy tooAzure</span></span>

<span data-ttu-id="f3183-155">Si presiona **F5** y ejecutar el proyecto de hello, resulta toohello implementado de clúster local.</span><span class="sxs-lookup"><span data-stu-id="f3183-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="f3183-156">Sin embargo, vamos a implementar tooAzure en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f3183-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="f3183-157">Haga doble clic en el proyecto de Hola y elija **publicar...**  que abre un tooAzure de toopublish del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3183-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Publicar el cuadro de diálogo de tooazure para un servicio de fabric][publish]

<span data-ttu-id="f3183-159">Seleccione hello **PublishProfiles\Cloud.xml** perfil de destino.</span><span class="sxs-lookup"><span data-stu-id="f3183-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="f3183-160">Si no lo ha hecho anteriormente, elija un toodeploy cuenta de Azure para.</span><span class="sxs-lookup"><span data-stu-id="f3183-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="f3183-161">Si aún no tiene ninguno, [regístrese para obtenerlo][create-account].</span><span class="sxs-lookup"><span data-stu-id="f3183-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="f3183-162">En **extremo de la conexión**, seleccione Hola toodeploy de clúster de Service Fabric a.</span><span class="sxs-lookup"><span data-stu-id="f3183-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="f3183-163">Si no tiene uno, seleccione  **&lt;crear un nuevo clúster... &gt;**  que abrirá toohello de ventana de explorador web portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3183-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="f3183-164">Para obtener más información, consulte [crear un clúster en el portal de hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f3183-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="f3183-165">Cuando se crea el clúster de Service Fabric hello, que seguro Hola de tooset **los puntos de conexión personalizado** configuración demasiado**80**.</span><span class="sxs-lookup"><span data-stu-id="f3183-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Configuración del tipo de nodo de Service Fabric con el punto de conexión personalizado][custom-endpoint]

<span data-ttu-id="f3183-167">Crear un nuevo clúster de Service Fabric tiene algunos toocomplete de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f3183-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="f3183-168">Una vez se ha creado, vaya toohello back-cuadro de diálogo Publicar y seleccione  **&lt;actualizar&gt;**.</span><span class="sxs-lookup"><span data-stu-id="f3183-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="f3183-169">Hola nuevo se encuentre en el cuadro de lista desplegable de hello; Seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="f3183-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="f3183-170">Presione **publicar** y espere Hola implementación toofinish.</span><span class="sxs-lookup"><span data-stu-id="f3183-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="f3183-171">Esta operación puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="f3183-171">This may take a few minutes.</span></span> <span data-ttu-id="f3183-172">Una vez que se complete, puede tardar unos minutos para toobe de aplicación Hola totalmente disponible.</span><span class="sxs-lookup"><span data-stu-id="f3183-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="f3183-173">Sitio Web de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="f3183-173">Test hello website</span></span>

<span data-ttu-id="f3183-174">Una vez publicado su servicio, pruébelo en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="f3183-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="f3183-175">En primer lugar, abra Hola portal de Azure y busque el servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f3183-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="f3183-176">Compruebe la hoja de información general de Hola Hola de dirección de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3183-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="f3183-177">Usar el nombre de dominio de Hola Hola _extremo de la conexión de cliente_ propiedad.</span><span class="sxs-lookup"><span data-stu-id="f3183-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="f3183-178">Por ejemplo: `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f3183-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Hoja de información general de tejido de servicio en hello portal de Azure][overview]

<span data-ttu-id="f3183-180">Navegar por la dirección de toothis donde podrá ver hello `HELLO WORLD` respuesta.</span><span class="sxs-lookup"><span data-stu-id="f3183-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f3183-181">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="f3183-181">Delete hello cluster</span></span>

<span data-ttu-id="f3183-182">No olvide toodelete todos los recursos de Hola que haya creado para este tutorial rápido, que se le cobrará por dichos recursos.</span><span class="sxs-lookup"><span data-stu-id="f3183-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3183-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3183-183">Next steps</span></span>
<span data-ttu-id="f3183-184">Más información sobre [ejecutables de invitado](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="f3183-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F