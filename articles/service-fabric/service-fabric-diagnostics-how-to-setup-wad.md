---
title: "registros de aaaCollect con el diagnóstico de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo se registra tooset seguridad toocollect de diagnósticos de Azure desde un clúster de Service Fabric que se ejecuta en Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="03b1d-103">Recopilación de registros con Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="03b1d-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03b1d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="03b1d-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="03b1d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="03b1d-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="03b1d-106">Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="03b1d-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="03b1d-107">Tener registros de hello en una ubicación central le ayuda a analizar y solucionar problemas en el clúster o problemas en aplicaciones de Hola y servicios que se ejecutan en ese clúster.</span><span class="sxs-lookup"><span data-stu-id="03b1d-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="03b1d-108">Tooupload de una forma y recopilar registros es extensión de diagnósticos de Azure hello toouse, qué cargas registra tooAzure centros de eventos de Azure, Azure Application Insights o de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="03b1d-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="03b1d-109">Hola registros no son tan útiles directamente en el almacenamiento o en centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="03b1d-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="03b1d-110">Pero puede usar un proceso externo tooread Hola de eventos de almacenamiento y colocarlos en un producto como [análisis de registros](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="03b1d-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="03b1d-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) tiene integrado un servicio integral de análisis y búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="03b1d-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03b1d-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="03b1d-112">Prerequisites</span></span>
<span data-ttu-id="03b1d-113">Use estas herramientas tooperform algunas de las operaciones de hello en este documento:</span><span class="sxs-lookup"><span data-stu-id="03b1d-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="03b1d-114">[Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionadas con la tooAzure servicios en la nube, pero tiene buena información y ejemplos)</span><span class="sxs-lookup"><span data-stu-id="03b1d-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="03b1d-115">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="03b1d-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="03b1d-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="03b1d-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="03b1d-117">Cliente de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03b1d-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="03b1d-118">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03b1d-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="03b1d-119">Orígenes de registro que podría interesarle toocollect</span><span class="sxs-lookup"><span data-stu-id="03b1d-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="03b1d-120">**Registros de Service Fabric**: emitidos desde Hola plataforma toostandard seguimiento de eventos para Windows (ETW) y EventSource los canales.</span><span class="sxs-lookup"><span data-stu-id="03b1d-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="03b1d-121">Los registros pueden ser de uno de los varios tipos que hay:</span><span class="sxs-lookup"><span data-stu-id="03b1d-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="03b1d-122">Los eventos operativos: registros de operaciones que Hola Service Fabric realiza la plataforma.</span><span class="sxs-lookup"><span data-stu-id="03b1d-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="03b1d-123">Algunos ejemplos son la creación de aplicaciones y servicios, los cambios de estado de nodo y la información sobre la actualización.</span><span class="sxs-lookup"><span data-stu-id="03b1d-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="03b1d-124">Eventos del modelo de programación de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="03b1d-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="03b1d-125">Eventos del modelo de programación de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="03b1d-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="03b1d-126">**Eventos de aplicación**: eventos emitidos desde el código de su servicio y que se escribe mediante el uso de clase de aplicación auxiliar de hello EventSource proporcionada en las plantillas de Visual Studio de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="03b1d-127">Para obtener más información sobre cómo toowrite registros de la aplicación, consulte [Monitor y diagnosticar los servicios en una configuración de desarrollo de equipo local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="03b1d-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="03b1d-128">Implementar la extensión de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="03b1d-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="03b1d-129">Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="03b1d-130">extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique.</span><span class="sxs-lookup"><span data-stu-id="03b1d-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="03b1d-131">pasos de Hello varían ligeramente en función de si utiliza Hola portal de Azure o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="03b1d-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="03b1d-132">pasos de Hello también varían en función de si implementación hello es parte de la creación de clúster o de un clúster que ya existe.</span><span class="sxs-lookup"><span data-stu-id="03b1d-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="03b1d-133">Echemos un vistazo a los pasos de Hola para cada escenario.</span><span class="sxs-lookup"><span data-stu-id="03b1d-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="03b1d-134">Implementar la extensión de diagnósticos de hello como parte de la creación del clúster a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="03b1d-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="03b1d-135">toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, utilice panel de configuración de diagnósticos de Hola se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="03b1d-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="03b1d-136">tooenable Reliable Actors o servicios confiables recopilación de eventos, asegúrese de que diagnósticos está establecido demasiado**en** (Hola la configuración predeterminada).</span><span class="sxs-lookup"><span data-stu-id="03b1d-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="03b1d-137">Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Configuración de diagnóstico de Azure en el portal de hello para la creación de clúster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="03b1d-139">Hola equipo de soporte técnico de Azure *requiere* compatibilidad con registros toohelp resolver las solicitudes de soporte técnico que cree.</span><span class="sxs-lookup"><span data-stu-id="03b1d-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="03b1d-140">Estos registros se recopilan en tiempo real y se almacenan en una de las cuentas de almacenamiento de hello creadas en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="03b1d-141">configuración de diagnóstico de Hello configura eventos de nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="03b1d-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="03b1d-142">Estos eventos incluyen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventos, [servicios confiables](service-fabric-reliable-services-diagnostics.md) eventos y algunos toobe de eventos de Service Fabric de nivel de sistema almacenados en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="03b1d-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="03b1d-143">Productos como [Elasticsearch](https://www.elastic.co/guide/index.html) o su propio proceso puede recopilar eventos de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="03b1d-144">Actualmente no hay ningún evento de Hola de toofilter o limpiar de forma que se envía toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="03b1d-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="03b1d-145">Si no implementan un tooremove procesar los eventos de tabla de hello, tabla de hello seguirá toogrow.</span><span class="sxs-lookup"><span data-stu-id="03b1d-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="03b1d-146">Al crear un clúster mediante el portal de hello, recomendamos encarecidamente que descargue la plantilla de hello **antes de hacer clic en Aceptar** clúster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="03b1d-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="03b1d-147">Para obtener más información, consulte demasiado[configurar un clúster de Service Fabric mediante una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="03b1d-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="03b1d-148">Necesitará toomake cambios de la plantilla de hello más tarde, debido a que no puede realizar algunos cambios mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="03b1d-149">Puede exportar plantillas desde el portal de hello mediante Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="03b1d-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="03b1d-150">Sin embargo, estas plantillas pueden ser más difícil toouse porque podría tienen valores null que les falta información necesaria.</span><span class="sxs-lookup"><span data-stu-id="03b1d-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="03b1d-151">Abra el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="03b1d-151">Open your resource group.</span></span>
2. <span data-ttu-id="03b1d-152">Seleccione **configuración** panel de configuración de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="03b1d-153">Seleccione **implementaciones** panel de historial de implementación de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="03b1d-154">Seleccione un detalles de implementación toodisplay Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="03b1d-155">Seleccione **Exportar plantilla** panel de plantilla de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="03b1d-156">Seleccione **guardar toofile** tooexport un archivo .zip que contiene la plantilla de hello, parámetros y archivos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03b1d-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="03b1d-157">Después de exportar los archivos de hello, deberá toomake una modificación.</span><span class="sxs-lookup"><span data-stu-id="03b1d-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="03b1d-158">Editar archivo de parameters.json de Hola y quitar hello **adminPassword** elemento.</span><span class="sxs-lookup"><span data-stu-id="03b1d-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="03b1d-159">Esto hará que una petición de contraseña de hello al ejecutar el script de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="03b1d-160">Si estás ejecutando script de implementación de hello, puede que tenga valores de parámetro con valor nulo de toofix.</span><span class="sxs-lookup"><span data-stu-id="03b1d-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="03b1d-161">Hola toouse descarga plantilla tooupdate una configuración:</span><span class="sxs-lookup"><span data-stu-id="03b1d-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="03b1d-162">Extraer tooa carpeta de contenido de hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="03b1d-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="03b1d-163">Modificar Hola contenido tooreflect Hola nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="03b1d-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="03b1d-164">Inicie PowerShell y cambie la carpeta toohello en la que extrajo el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="03b1d-165">Ejecutar **deploy.ps1** y rellene el identificador de suscripción de hello, nombre de grupo de recursos de hello (use Hola mismo configuración el nombre de hello tooupdate) y un nombre único de implementación.</span><span class="sxs-lookup"><span data-stu-id="03b1d-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="03b1d-166">Implementar la extensión de diagnósticos de hello como parte de la creación del clúster mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="03b1d-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="03b1d-167">toocreate un clúster mediante el Administrador de recursos, necesita hello tooadd diagnósticos JSON configuración toohello el Administrador de recursos completo del clúster plantilla antes de crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="03b1d-168">Proporcionamos una plantilla de administrador de recursos de clúster de cinco VM de ejemplo con la configuración de diagnóstico agrega tooit como parte de nuestros ejemplos de la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="03b1d-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="03b1d-169">Puede ver en esta ubicación en la Galería de ejemplos de Azure hello: [clúster de cinco nodos con el ejemplo de la plantilla de administrador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="03b1d-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="03b1d-170">configuración de diagnósticos de hello toosee en plantilla de administrador de recursos de hello, archivo de azuredeploy.json de hello abierto y busque **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="03b1d-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="03b1d-171">un clúster con esta plantilla, seleccione hello toocreate **implementar tooAzure** botón está disponible en el vínculo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="03b1d-172">Como alternativa, puede descargar el ejemplo de Hola a Administrador de recursos, realizar cambios tooit y crear un clúster con la plantilla modificada hello mediante Hola `New-AzureRmResourceGroupDeployment` comando en una ventana de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="03b1d-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="03b1d-173">Vea Hola siguiente código para los parámetros de Hola que se pasan en el comando toohello.</span><span class="sxs-lookup"><span data-stu-id="03b1d-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="03b1d-174">Para obtener información detallada sobre cómo toodeploy un recurso de grupo mediante el uso de PowerShell, vea el artículo de hello [implementar un grupo de recursos con la plantilla de Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="03b1d-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="03b1d-175">Implementar el clúster existente de hello diagnósticos extensión tooan</span><span class="sxs-lookup"><span data-stu-id="03b1d-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="03b1d-176">Si tiene un clúster existente que no tiene implementado de diagnóstico, o si desea toomodify una configuración existente, puede agregar o actualizar.</span><span class="sxs-lookup"><span data-stu-id="03b1d-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="03b1d-177">Modificar plantilla de administrador de recursos de Hola que es usado toocreate Hola existente clúster o descargar plantilla de Hola desde el portal de hello, tal como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="03b1d-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="03b1d-178">Modificar el archivo de template.json de hello realizando Hola siguiente las tareas.</span><span class="sxs-lookup"><span data-stu-id="03b1d-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="03b1d-179">Agregar una nueva plantilla de toohello de recursos de almacenamiento mediante la adición de la sección de recursos toohello.</span><span class="sxs-lookup"><span data-stu-id="03b1d-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="03b1d-180">A continuación, agregue parámetros toohello sección justo después de las definiciones de la cuenta de almacenamiento de hello, entre `supportLogStorageAccountName` y `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="03b1d-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="03b1d-181">Reemplace el texto de marcador de posición de hello *aquí el nombre de cuenta de almacenamiento* con el nombre de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="03b1d-182">A continuación, actualice hello `VirtualMachineProfile` sección del archivo de template.json Hola agregando Hola siguiente código dentro de la matriz de extensiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="03b1d-183">Ser seguro tooadd una coma al principio de Hola o al final de hello, según donde se inserta.</span><span class="sxs-lookup"><span data-stu-id="03b1d-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="03b1d-184">Después de modificar el archivo de hello template.json tal como se describe, volver a publicar la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="03b1d-185">Si se ha exportado la plantilla de hello, archivo de ejecución hello deploy.ps1 vuelve a publicar plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="03b1d-186">Después de realizar la implementación, asegúrese de que el estado **ProvisioningState** sea **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="03b1d-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="03b1d-187">Actualizar los eventos de estado y la carga de toocollect de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="03b1d-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="03b1d-188">A partir de hello 5.4 versión de Service Fabric, eventos de métrica de mantenimiento y carga están disponibles para la colección.</span><span class="sxs-lookup"><span data-stu-id="03b1d-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="03b1d-189">Estos eventos reflejan los eventos generados por el sistema de hello o tu código mediante el uso de mantenimiento de Hola o cargue las API de generación de informes como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="03b1d-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="03b1d-190">Esto permite agregar y ver el estado de mantenimiento del sistema en el tiempo, y generar alertas basadas en eventos de estado de mantenimiento o carga.</span><span class="sxs-lookup"><span data-stu-id="03b1d-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="03b1d-191">tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de proveedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="03b1d-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="03b1d-192">eventos de hello toocollect, modificar tooinclude de plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="03b1d-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="03b1d-193">Actualizar toocollect de diagnóstico y carga los registros de nuevos canales EventSource</span><span class="sxs-lookup"><span data-stu-id="03b1d-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="03b1d-194">registros de toocollect tooupdate diagnósticos de nuevos canales EventSource que representan una nueva aplicación que le sobre toodeploy, realizar Hola mismos pasos en hello [sección anterior](#deploywadarm) para la configuración de diagnósticos de una existente clúster.</span><span class="sxs-lookup"><span data-stu-id="03b1d-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="03b1d-195">Actualizar hello `EtwEventSourceProviderConfiguration` sección entradas del archivo de hello template.json tooadd para actualización con Hola Hola EventSource canales nuevos antes de aplicar la configuración de hello `New-AzureRmResourceGroupDeployment` comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03b1d-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="03b1d-196">nombre de Hola Hola del origen de evento se define como parte de su código en un archivo generado por Visual Studio ServiceEventSource.cs Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="03b1d-197">Por ejemplo, si el origen de eventos se denomina Mis Eventsource, agregar Hola siguientes eventos de código tooplace Hola de mi Eventsource en una tabla denominada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="03b1d-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="03b1d-198">contadores de rendimiento de toocollect o registros de eventos, modificar plantilla de administrador de recursos de hello mediante ejemplos de hello en [crear una máquina virtual de Windows con la supervisión y el diagnóstico mediante una plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03b1d-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="03b1d-199">A continuación, volver a publicar plantilla del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="03b1d-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03b1d-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03b1d-200">Next steps</span></span>
<span data-ttu-id="03b1d-201">toounderstand con más detalle qué eventos debe buscar al solucionar problemas, consulte los eventos de diagnóstico Hola emitidos para [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) y [servicios confiables](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03b1d-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="03b1d-202">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="03b1d-202">Related articles</span></span>
* [<span data-ttu-id="03b1d-203">Obtenga información acerca de cómo toocollect los contadores de rendimiento o de registros mediante el uso de Hola extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="03b1d-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="03b1d-204">[Service Fabric solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md) (Solución de Service Fabric en Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="03b1d-204">[Service Fabric solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md)</span></span>

