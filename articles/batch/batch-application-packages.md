---
title: paquetes de aplicaciones de aaaInstall en nodos de proceso - Azure Batch | Documentos de Microsoft
description: "Característica de paquetes de aplicación de uso Hola de Azure Batch tooeasily administrar varias aplicaciones y nodos de ejecución de versiones para la instalación en lote."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="19eec-103">Implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote</span><span class="sxs-lookup"><span data-stu-id="19eec-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="19eec-104">característica de paquetes de aplicación Hola de lote de Azure proporciona una administración sencilla de aplicaciones de la tarea y su toohello implementación nodos de cálculo en el grupo.</span><span class="sxs-lookup"><span data-stu-id="19eec-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="19eec-105">Con paquetes de aplicaciones, puede cargar y administrar varias versiones de aplicaciones de hello que ejecutarán sus tareas, incluidas sus archivos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="19eec-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="19eec-106">Se puede, a continuación, implementar automáticamente una o varias de estas aplicaciones toohello nodos de cálculo en el grupo.</span><span class="sxs-lookup"><span data-stu-id="19eec-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="19eec-107">En este artículo, aprenderá cómo tooupload y administrar paquetes de aplicación Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19eec-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="19eec-108">A continuación, aprenderá cómo tooinstall en un grupo de proceso nodos con hello [.NET de lotes] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="19eec-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="19eec-109">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="19eec-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="19eec-110">Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="19eec-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="19eec-111">Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19eec-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="19eec-112">las API para crear y administrar paquetes de aplicación Hello forman parte de hello [.NET de administración de lotes] [[api_net_mgmt]] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="19eec-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="19eec-113">las API para la instalación de paquetes de aplicaciones en un nodo de proceso Hello forman parte del programa Hola a [.NET de lotes] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="19eec-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="19eec-114">característica de paquetes de aplicación Hola aquí descrito reemplaza a la característica de aplicaciones de lote de hello disponible en versiones anteriores del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="19eec-115">Requisitos de los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-115">Application package requirements</span></span>
<span data-ttu-id="19eec-116">paquetes de aplicaciones de toouse, necesita demasiado[vincular una cuenta de almacenamiento de Azure](#link-a-storage-account) tooyour cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="19eec-117">Esta característica se introdujo en [API de REST de lote] [ api_rest] versión 2015-12-01.2.2 y Hola correspondiente [.NET de lotes] [ api_net] versión de la biblioteca 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="19eec-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="19eec-118">Se recomienda usar siempre la última versión de la API de hello cuando se trabaja con el lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="19eec-119">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="19eec-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="19eec-120">Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="19eec-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="19eec-121">Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19eec-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="19eec-122">Acerca de las aplicaciones y los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-122">About applications and application packages</span></span>
<span data-ttu-id="19eec-123">En el lote de Azure, un *aplicación* hace referencia tooa conjunto de archivos binarios con control de versiones que pueden ser nodos de proceso toohello automáticamente descargado en el grupo.</span><span class="sxs-lookup"><span data-stu-id="19eec-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="19eec-124">Un *paquete de aplicación* hace referencia tooa *conjunto específico* de los archivos binarios y representa un determinado *versión* de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="19eec-125">![Diagrama de alto nivel de aplicaciones y paquetes de aplicación][1]</span><span class="sxs-lookup"><span data-stu-id="19eec-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="19eec-126">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="19eec-126">Applications</span></span>
<span data-ttu-id="19eec-127">Una aplicación en el lote contiene una o más aplicaciones, paquetes y especifica las opciones de configuración para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="19eec-128">Por ejemplo, una aplicación puede especificar Hola predeterminado aplicación paquete versión tooinstall en nodos de proceso y si se pueden actualizar o eliminar sus paquetes.</span><span class="sxs-lookup"><span data-stu-id="19eec-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="19eec-129">paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-129">Application packages</span></span>
<span data-ttu-id="19eec-130">Un paquete de aplicación es un archivo .zip que contiene los archivos binarios de aplicación de Hola y archivos auxiliares necesarios para la aplicación de hello toorun de tareas.</span><span class="sxs-lookup"><span data-stu-id="19eec-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="19eec-131">Cada paquete de aplicación representa una versión específica de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="19eec-132">Puede especificar los paquetes de aplicación en los niveles de grupo y tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="19eec-133">Puede especificar uno o varios de estos paquetes y (opcionalmente) una versión cuando crea un grupo o tarea.</span><span class="sxs-lookup"><span data-stu-id="19eec-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="19eec-134">**Grupo de paquetes de aplicaciones** se implementan demasiado*cada* nodo de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="19eec-135">Las aplicaciones se implementan cuando un nodo se une a un grupo y cuando se reinicia o se restablece la imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="19eec-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="19eec-136">Los paquetes de aplicación de grupo son adecuados cuando todos los nodos de un grupo ejecutan las tareas de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="19eec-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="19eec-137">Puede especificar uno o más paquetes de aplicación cuando se crea un grupo y puede agregar o actualizar los paquetes de un grupo ya existente.</span><span class="sxs-lookup"><span data-stu-id="19eec-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="19eec-138">Si actualiza los paquetes de aplicación de un grupo existente, debe reiniciar el nuevo paquete de nodos tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="19eec-139">**Paquetes de aplicación de tareas** se implementan solo de nodos de proceso tooa toorun una tarea programada, justo antes de ejecutar línea de comandos de la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="19eec-140">Si especifica Hola versión y el paquete de aplicación ya está en el nodo de hello, no se vuelve a implementar y se utiliza el paquete existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="19eec-141">Paquetes de aplicación de tareas son útiles en entornos de grupo compartido, donde distintos trabajos que se ejecutan en un grupo y no se elimina el grupo de hello cuando se completa un trabajo.</span><span class="sxs-lookup"><span data-stu-id="19eec-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="19eec-142">Si el trabajo tiene menos tareas que los nodos de grupo de hello, paquetes de aplicaciones de la tarea pueden minimizar la transferencia de datos ya que la aplicación está implementada toohello solo nodos que se ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="19eec-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="19eec-143">Otros escenarios que pueden beneficiarse de los paquetes de aplicación de tareas son los trabajos que ejecutan una aplicación grande, pero solo para unas pocas tareas.</span><span class="sxs-lookup"><span data-stu-id="19eec-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="19eec-144">Por ejemplo, una fase previa al procesamiento o una tarea de mezcla, donde la aplicación de procesamiento previo o combinación de hello es pesado, puede beneficiarse del uso de paquetes de aplicaciones de la tarea.</span><span class="sxs-lookup"><span data-stu-id="19eec-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19eec-145">Hay restricciones en número de Hola de aplicaciones y paquetes de aplicaciones dentro de una cuenta de lote y en el tamaño de paquete de hello máxima de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="19eec-146">Vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener más información acerca de estos límites.</span><span class="sxs-lookup"><span data-stu-id="19eec-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="19eec-147">Ventajas de los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-147">Benefits of application packages</span></span>
<span data-ttu-id="19eec-148">Paquetes de aplicaciones pueden simplificar código de hello en la solución de lote y el inferior Hola sobrecarga toomanage necesario hello las aplicaciones que se ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="19eec-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="19eec-149">Con paquetes de aplicaciones, tarea de inicio de la agrupación no tiene toospecify una lista larga de tooinstall de archivos de recursos individuales en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="19eec-150">No es necesario toomanually administrar varias versiones de los archivos de aplicación en el almacenamiento de Azure, o en los nodos.</span><span class="sxs-lookup"><span data-stu-id="19eec-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="19eec-151">Y no necesita tooworry acerca de cómo generar [direcciones URL de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide acceder a los archivos de toohello en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="19eec-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="19eec-152">Procesar por lotes funciona en segundo plano de hello con paquetes de aplicaciones de almacenamiento de Azure toostore e implementarlas toocompute nodos.</span><span class="sxs-lookup"><span data-stu-id="19eec-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="19eec-153">Hello tamaño total de una tarea de inicio debe ser menor o igual too32768 caracteres, incluidos los archivos de recursos y las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="19eec-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="19eec-154">Si la tarea de inicio supera este límite, en este caso usar paquetes de aplicación es otra opción.</span><span class="sxs-lookup"><span data-stu-id="19eec-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="19eec-155">Puede crear un archivo comprimido que contiene los archivos de recursos, cargarlo como un almacenamiento de blob tooAzure y, a continuación, descomprímalo desde línea de comandos de saludo de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="19eec-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="19eec-156">Carga y administración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="19eec-156">Upload and manage applications</span></span>
<span data-ttu-id="19eec-157">Puede usar hello [portal de Azure] [ portal] o hello [.NET de administración de lotes](batch-management-dotnet.md) paquetes de aplicación de biblioteca toomanage hello en su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="19eec-158">En a continuación Hola secciones, se muestra primero cómo toolink una cuenta de almacenamiento, a continuación, analice agregando aplicaciones y paquetes y administrarlos con Hola portal.</span><span class="sxs-lookup"><span data-stu-id="19eec-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="19eec-159">Vínculo a una cuenta de Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="19eec-159">Link a Storage account</span></span>
<span data-ttu-id="19eec-160">paquetes de aplicaciones de toouse, primero debe vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="19eec-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="19eec-161">Si aún no ha configurado una cuenta de almacenamiento, hello portal de Azure muestra una advertencia hello primera vez que haga clic en hello **aplicaciones** el icono Servicios hello **cuenta de lote** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19eec-162">Procesar por lotes admite actualmente *sólo* hello **general** tipo de cuenta de almacenamiento tal como se describe en el paso 5, [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account), en [acerca de Azure las cuentas de almacenamiento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="19eec-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="19eec-163">Al vincular un tooyour de cuenta de almacenamiento de Azure cuenta de lote, se vinculan *sólo* una **general** cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="19eec-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="19eec-164">![Advertencia de que no hay cuentas de almacenamiento configuradas en Azure Portal][9]</span><span class="sxs-lookup"><span data-stu-id="19eec-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="19eec-165">Hola Hola de usos de servicio de lote había asociado toostore de cuenta de almacenamiento los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19eec-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="19eec-166">Una vez haya vinculado dos cuentas de hello, lote automáticamente puede implementar paquetes de saludo almacenados en nodos de proceso de tooyour de cuenta de almacenamiento de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="19eec-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="19eec-167">toolink un tooyour de cuenta de almacenamiento cuenta de lote, haga clic en **configuración de la cuenta de almacenamiento** en hello **advertencia** hoja y, a continuación, haga clic en **cuenta de almacenamiento** en hello **Cuenta de almacenamiento** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="19eec-168">![Hoja Elegir de cuenta de almacenamiento en Azure Portal][10]</span><span class="sxs-lookup"><span data-stu-id="19eec-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="19eec-169">Se recomienda crear una cuenta de Storage *específicamente* para su uso con la cuenta de Batch y seleccionarla aquí.</span><span class="sxs-lookup"><span data-stu-id="19eec-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="19eec-170">Para obtener más información acerca de cómo toocreate una cuenta de almacenamiento, vea "Crear una cuenta de almacenamiento" en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="19eec-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="19eec-171">Después de crear una cuenta de almacenamiento, puede, a continuación, vincúlelo tooyour cuenta de lote mediante el uso de hello **cuenta de almacenamiento** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="19eec-172">Hola servicio por lotes utiliza el almacenamiento de Azure toostore los paquetes de aplicaciones como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="19eec-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="19eec-173">Está [carga como normal] [ storage_pricing] para datos de blob de bloque de saludo.</span><span class="sxs-lookup"><span data-stu-id="19eec-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="19eec-174">Estar seguro de tamaño de hello tooconsider y el número de los paquetes de aplicaciones y quitan periódicamente los costos de toominimize de los paquetes en desuso.</span><span class="sxs-lookup"><span data-stu-id="19eec-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="19eec-175">Visualización de las aplicaciones actuales</span><span class="sxs-lookup"><span data-stu-id="19eec-175">View current applications</span></span>
<span data-ttu-id="19eec-176">las aplicaciones de hello tooview en su cuenta de lote, haga clic en hello **aplicaciones** elemento de menú en el menú de la izquierda Hola durante la visualización de hello **cuenta de lote** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="19eec-177">![Icono Aplicaciones][2]</span><span class="sxs-lookup"><span data-stu-id="19eec-177">![Applications tile][2]</span></span>

<span data-ttu-id="19eec-178">Al seleccionar esta opción de menú abre hello **aplicaciones** hoja:</span><span class="sxs-lookup"><span data-stu-id="19eec-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="19eec-179">![Lista de aplicaciones][3]</span><span class="sxs-lookup"><span data-stu-id="19eec-179">![List applications][3]</span></span>

<span data-ttu-id="19eec-180">Hola **aplicaciones** hoja muestra Hola Id. de cada aplicación en su cuenta y Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="19eec-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="19eec-181">**Paquetes**: Hola número de versiones asociadas a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="19eec-182">**Versión predeterminada**: versión de la aplicación hello instalado si no indica una versión cuando se especifica la aplicación hello para un grupo.</span><span class="sxs-lookup"><span data-stu-id="19eec-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="19eec-183">Esta configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="19eec-183">This setting is optional.</span></span>
* <span data-ttu-id="19eec-184">**Permitir actualizaciones**: valor de Hola que especifica si las actualizaciones de paquete, eliminaciones y las adiciones se permiten.</span><span class="sxs-lookup"><span data-stu-id="19eec-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="19eec-185">Si se establece demasiado**n**, paquete actualizaciones y eliminaciones se deshabilitan para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="19eec-186">Solo se pueden agregar versiones nuevas del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-186">Only new application package versions can be added.</span></span> <span data-ttu-id="19eec-187">valor predeterminado de Hello es **Sí**.</span><span class="sxs-lookup"><span data-stu-id="19eec-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="19eec-188">Visualización de los detalles de una aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-188">View application details</span></span>
<span data-ttu-id="19eec-189">hoja de hello tooopen que incluye detalles de Hola para una aplicación de la aplicación, seleccione Hola Hola **aplicaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="19eec-190">![Detalles de la aplicación][4]</span><span class="sxs-lookup"><span data-stu-id="19eec-190">![Application details][4]</span></span>

<span data-ttu-id="19eec-191">En la hoja de detalles de la aplicación de hello, puede configurar Hola siguientes opciones para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="19eec-192">**Permitir actualizaciones**: especifica si se pueden actualizar o eliminar sus paquetes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="19eec-193">Consulte "Actualización o eliminación de un paquete de aplicación" más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="19eec-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="19eec-194">**Versión predeterminada**: especificar un nodos de toocompute predeterminados toodeploy de paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="19eec-195">**Nombre para mostrar**: especificar descriptivo nombre que el lote de solución puede utilizar cuando se muestra información acerca de la aplicación hello, por ejemplo, en hello interfaz de usuario de un servicio que proporciona a los clientes de tooyour a través de lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="19eec-196">Adición de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-196">Add a new application</span></span>
<span data-ttu-id="19eec-197">toocreate una nueva aplicación, agregue un paquete de aplicación y especifique un identificador de aplicación nueva y única.</span><span class="sxs-lookup"><span data-stu-id="19eec-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="19eec-198">Hola primer paquete de la aplicación que se agrega con el nuevo identificador de aplicación Hola también crea Hola nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="19eec-199">Haga clic en **agregar** en hello **aplicaciones** Hola de hoja tooopen **nueva aplicación** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="19eec-200">![Hoja Nueva aplicación en Azure Portal][5]</span><span class="sxs-lookup"><span data-stu-id="19eec-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="19eec-201">Hola **nueva aplicación** hoja proporciona la configuración de Hola de toospecify de la nueva aplicación y el paquete de aplicación de los campos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="19eec-202">**Id. de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="19eec-202">**Application id**</span></span>

<span data-ttu-id="19eec-203">Este campo especifica el Id. de saludo de la nueva aplicación, que es de reglas de validación de Id. de lote de Azure estándares de asunto toohello.</span><span class="sxs-lookup"><span data-stu-id="19eec-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="19eec-204">reglas de Hola para proporcionar un identificador de aplicación son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="19eec-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="19eec-205">En los nodos de Windows, el identificador de hello puede contener cualquier combinación de caracteres alfanuméricos, guiones y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="19eec-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="19eec-206">En los nodos de Linux, solo se permiten caracteres alfanuméricos y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="19eec-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="19eec-207">No pueden contener más de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="19eec-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="19eec-208">Debe ser único dentro de hello cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="19eec-209">Conserva las mayúsculas y minúsculas, aunque no las distingue.</span><span class="sxs-lookup"><span data-stu-id="19eec-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="19eec-210">**Versión**</span><span class="sxs-lookup"><span data-stu-id="19eec-210">**Version**</span></span>

<span data-ttu-id="19eec-211">Este campo especifica la versión de Hola Hola del paquete de aplicación que va a cargar.</span><span class="sxs-lookup"><span data-stu-id="19eec-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="19eec-212">Cadenas de versión son toohello asunto siguiendo las reglas de validación:</span><span class="sxs-lookup"><span data-stu-id="19eec-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="19eec-213">En los nodos de Windows, la cadena de versión de Hola puede contener cualquier combinación de caracteres alfanuméricos, guiones, caracteres de subrayado y puntos.</span><span class="sxs-lookup"><span data-stu-id="19eec-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="19eec-214">En los nodos de Linux, la cadena de versión de Hola puede contener solo caracteres alfanuméricos y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="19eec-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="19eec-215">No pueden contener más de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="19eec-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="19eec-216">Debe ser único dentro de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="19eec-217">Conservan las mayúsculas y minúsculas, aunque no las distinguen.</span><span class="sxs-lookup"><span data-stu-id="19eec-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="19eec-218">**Paquete de aplicación**</span><span class="sxs-lookup"><span data-stu-id="19eec-218">**Application package**</span></span>

<span data-ttu-id="19eec-219">Este campo especifica el archivo .zip de Hola que contiene los archivos binarios de aplicación de Hola y archivos auxiliares que son de la aplicación hello tooexecute necesarios.</span><span class="sxs-lookup"><span data-stu-id="19eec-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="19eec-220">Haga clic en hello **seleccionar un archivo** cuadro o hello tooand de toobrowse del icono de carpeta seleccione un archivo .zip que contiene archivos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19eec-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="19eec-221">Después de seleccionar un archivo, haga clic en **Aceptar** toobegin Hola carga tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="19eec-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="19eec-222">Una vez completada la operación de carga de hello, portal de hello muestra una notificación y cierra la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="19eec-223">Función tamaño Hola de archivo hello que son hello y carga de velocidad de la conexión de red, esta operación puede tardar algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="19eec-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="19eec-224">No cierre hello **nueva aplicación** hoja antes de que finalice la operación de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="19eec-225">Si lo hace, se detendrá el proceso de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="19eec-226">Adición de un nuevo paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-226">Add a new application package</span></span>
<span data-ttu-id="19eec-227">tooadd una nueva versión del paquete de aplicación para una aplicación existente, seleccione una aplicación Hola **aplicaciones** hoja, haga clic en **paquetes**, a continuación, haga clic en **agregar** tooopen Hola **Agregar paquete** hoja.</span><span class="sxs-lookup"><span data-stu-id="19eec-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="19eec-228">![Hoja Agregar paquete de aplicación en Azure Portal][8]</span><span class="sxs-lookup"><span data-stu-id="19eec-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="19eec-229">Como puede ver, los campos de hello coinciden con los de hello **nueva aplicación** hoja, pero hello **Id. de aplicación** casilla está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="19eec-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="19eec-230">Tal y como lo hizo para aplicación Hola, especifique hello **versión** para el nuevo paquete, examinar tooyour **paquete de aplicación** .zip de archivos, a continuación, haga clic en **Aceptar** hello tooupload paquete.</span><span class="sxs-lookup"><span data-stu-id="19eec-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="19eec-231">Actualización o eliminación de un paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="19eec-231">Update or delete an application package</span></span>
<span data-ttu-id="19eec-232">tooupdate o eliminar un paquete de aplicación existente, hoja de detalles de hello abierto para la aplicación hello, haga clic en **paquetes** tooopen hello **paquetes** hoja, haga clic en hello **puntos suspensivos**de fila Hola Hola del paquete de aplicación que desee toomodify y seleccionar acción de Hola que desea tooperform.</span><span class="sxs-lookup"><span data-stu-id="19eec-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="19eec-233">![Actualizar o eliminar paquete en Azure Portal][7]</span><span class="sxs-lookup"><span data-stu-id="19eec-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="19eec-234">**Actualizar**</span><span class="sxs-lookup"><span data-stu-id="19eec-234">**Update**</span></span>

<span data-ttu-id="19eec-235">Al hacer clic en **actualización**, hello *paquete de actualización* hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="19eec-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="19eec-236">Esta hoja es similar toohello *nuevo paquete de aplicación* hoja, el campo de selección del paquete de hello sin embargo, solo está habilitado, lo que le toospecify un nuevo tooupload del archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="19eec-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="19eec-237">![Hoja Actualizar paquete en Azure Portal][11]</span><span class="sxs-lookup"><span data-stu-id="19eec-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="19eec-238">**Eliminar**</span><span class="sxs-lookup"><span data-stu-id="19eec-238">**Delete**</span></span>

<span data-ttu-id="19eec-239">Al hacer clic en **eliminar**, se le pedirá la eliminación de hello tooconfirm de versión del paquete de Hola y paquete Hola de eliminaciones por lotes de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="19eec-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="19eec-240">Si elimina la versión de Hola predeterminada de una aplicación, Hola **versión predeterminada** configuración se quita de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="19eec-241">![Eliminar aplicación][12]</span><span class="sxs-lookup"><span data-stu-id="19eec-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="19eec-242">Instalación de aplicaciones en nodos de proceso</span><span class="sxs-lookup"><span data-stu-id="19eec-242">Install applications on compute nodes</span></span>
<span data-ttu-id="19eec-243">Ahora que ha aprendido cómo paquetes de la aplicación toomanage con hello portal de Azure, veremos cómo toodeploy les toocompute nodos y ejecutarlos con las tareas por lotes.</span><span class="sxs-lookup"><span data-stu-id="19eec-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="19eec-244">Instalación de paquetes de aplicación de grupos</span><span class="sxs-lookup"><span data-stu-id="19eec-244">Install pool application packages</span></span>
<span data-ttu-id="19eec-245">tooinstall un paquete de aplicación en todos los nodos de cálculo en un grupo, especifique uno o más paquetes de aplicación *referencias* para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="19eec-246">paquetes de aplicación Hola que especifique para un grupo se instalan en cada nodo de ejecución cuando une a ese nodo grupo de Hola y al nodo de Hola se reinicia o se restablece la imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="19eec-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="19eec-247">En el entorno de .NET para Batch, especifique una o varias [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] al crear el grupo o para un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="19eec-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="19eec-248">Hola [ApplicationPackageReference] [ net_pkgref] clase especifica un identificador de la aplicación y la versión tooinstall en un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="19eec-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="19eec-249">Si se produce un error en una implementación de paquete de aplicación por algún motivo, marcas de servicio de lote de Hola Hola nodo [inutilizable][net_nodestate], y no las tareas se programan para su ejecución en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="19eec-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="19eec-250">En este caso, debería **reiniciar** Hola implementación de paquetes de nodo tooreinitiate Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="19eec-251">Reiniciar nodo hello también permite la programación de tareas de nuevo en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="19eec-252">Instalación de paquetes de aplicación de tareas</span><span class="sxs-lookup"><span data-stu-id="19eec-252">Install task application packages</span></span>
<span data-ttu-id="19eec-253">Grupo tooa similares, especifique el paquete de aplicación *referencias* para una tarea.</span><span class="sxs-lookup"><span data-stu-id="19eec-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="19eec-254">Cuando una tarea está programada toorun en un nodo, paquete de hello es descargado y extraído justo antes de que se ejecuta la línea de comandos de la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="19eec-255">Si una versión y el paquete especificado ya está instalado en el nodo de hello, no se descarga el paquete de Hola y se usa el paquete existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="19eec-256">tooinstall un paquete de aplicación de la tarea, configure la tarea hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propiedad:</span><span class="sxs-lookup"><span data-stu-id="19eec-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="19eec-257">Ejecutar aplicaciones de hello instalado</span><span class="sxs-lookup"><span data-stu-id="19eec-257">Execute hello installed applications</span></span>
<span data-ttu-id="19eec-258">Hello paquetes que ha especificado para un grupo o una tarea se descargan y ha extraído tooa con el nombre de directorio en hello `AZ_BATCH_ROOT_DIR` del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="19eec-259">Proceso por lotes también crea una variable de entorno que contiene hello toohello de ruta de acceso con el nombre de directorio.</span><span class="sxs-lookup"><span data-stu-id="19eec-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="19eec-260">Las líneas de comando de la tarea use esta variable de entorno cuando se hace referencia a la aplicación hello en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="19eec-261">En los nodos de Windows, variable de hello es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="19eec-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="19eec-262">En los nodos de Linux, el formato de hello es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="19eec-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="19eec-263">Puntos (.), guiones (-) y signos de número (##) son toounderscores planas en la variable de entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="19eec-264">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19eec-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="19eec-265">`APPLICATIONID`y `version` son valores que corresponden a toohello aplicación y versión del paquete que haya especificado para la implementación.</span><span class="sxs-lookup"><span data-stu-id="19eec-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="19eec-266">Por ejemplo, si especifica que la versión 2.7 de aplicación *blender* debe estar instalado en los nodos de Windows, las líneas de comando de la tarea se utilice este tooaccess de variable de entorno sus archivos:</span><span class="sxs-lookup"><span data-stu-id="19eec-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="19eec-267">En los nodos de Linux, especifique la variable de entorno de Hola en este formato:</span><span class="sxs-lookup"><span data-stu-id="19eec-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="19eec-268">Cuando se carga un paquete de aplicación, puede especificar nodos de ejecución de un tooyour de toodeploy de versión de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19eec-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="19eec-269">Si ha especificado una versión predeterminada para una aplicación, puede omitir el sufijo de la versión de hello cuando se hace referencia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19eec-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="19eec-270">Puede especificar versión de la aplicación predeterminada Hola Hola portal de Azure, en la hoja de aplicaciones de hello, tal y como se muestra en [cargar y administrar aplicaciones](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="19eec-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="19eec-271">Por ejemplo, si establece "2.7" como versión predeterminada de Hola para aplicación *blender*y hacer referencia a las tareas de hello después de variable de entorno, a continuación, los nodos de Windows ejecutarán la versión 2.7:</span><span class="sxs-lookup"><span data-stu-id="19eec-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="19eec-272">Hello fragmento de código siguiente muestra un ejemplo de línea de comando de tarea que se inicia la versión predeterminada de Hola de hello *blender* aplicación:</span><span class="sxs-lookup"><span data-stu-id="19eec-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="19eec-273">Vea [configuración del entorno para tareas](batch-api-basics.md#environment-settings-for-tasks) en hello [Introducción a la característica por lotes](batch-api-basics.md) para obtener más información acerca de la configuración de entorno del nodo de proceso.</span><span class="sxs-lookup"><span data-stu-id="19eec-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="19eec-274">Actualización de los paquetes de aplicación de un grupo</span><span class="sxs-lookup"><span data-stu-id="19eec-274">Update a pool's application packages</span></span>
<span data-ttu-id="19eec-275">Si ya ha configurado un grupo existente con un paquete de aplicación, puede especificar un nuevo paquete para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="19eec-276">Si especifica una nueva referencia de paquete para un grupo, Hola después de aplicar:</span><span class="sxs-lookup"><span data-stu-id="19eec-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="19eec-277">Hola servicio por lotes instala el paquete recién especificado de hello en todos los nodos nuevos que unirse a grupo de Hola y en cualquier nodo existente que se reinicia o se restablece la imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="19eec-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="19eec-278">Proceso de nodos que ya están en el grupo de hello al actualizar las referencias del paquete hello no instalan automáticamente el nuevo paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="19eec-279">Estos nodos deben reiniciarse o proceso tooreceive con imagen inicial restablecida Hola nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="19eec-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="19eec-280">Cuando se implementa un paquete nuevo, Hola creado variables de entorno refleja nuevas referencias de paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="19eec-281">En este ejemplo, grupo existente de hello tiene la versión 2.7 de hello *blender* aplicación configurada como uno de sus [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="19eec-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="19eec-282">nodos del grupo de tooupdate Hola con versión 2.76b, especificar un nuevo [ApplicationPackageReference] [ net_pkgref] con la nueva versión de hello y cambio de Hola de confirmación.</span><span class="sxs-lookup"><span data-stu-id="19eec-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="19eec-283">Ahora que hello nueva versión se ha configurado, Hola servicio por lotes instala versión 2.76b tooany *nueva* nodo que se une a grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="19eec-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="19eec-284">tooinstall 2.76b en nodos de Hola que sean *ya* en el grupo de hello, reiniciar o Restablecer imagen inicial de ellos.</span><span class="sxs-lookup"><span data-stu-id="19eec-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="19eec-285">Tenga en cuenta que nodos reiniciados conservan archivos Hola desde implementaciones anteriores de paquetes.</span><span class="sxs-lookup"><span data-stu-id="19eec-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="19eec-286">Enumerar las aplicaciones de hello en una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="19eec-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="19eec-287">Puede enumerar las aplicaciones de Hola y sus paquetes en una cuenta de lote mediante hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] método.</span><span class="sxs-lookup"><span data-stu-id="19eec-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="19eec-288">Encapsulado</span><span class="sxs-lookup"><span data-stu-id="19eec-288">Wrap up</span></span>
<span data-ttu-id="19eec-289">Con paquetes de aplicaciones, puede ayudar a sus clientes seleccione aplicaciones de Hola para sus tareas y especificar Hola versión exacta toouse al procesar los trabajos con el servicio de lote activado.</span><span class="sxs-lookup"><span data-stu-id="19eec-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="19eec-290">También podría proporcionan capacidad de hello para el tooupload de los clientes y realizar un seguimiento de sus propias aplicaciones en su servicio.</span><span class="sxs-lookup"><span data-stu-id="19eec-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19eec-291">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19eec-291">Next steps</span></span>
* <span data-ttu-id="19eec-292">Hola [API de REST de lote] [ api_rest] también proporciona compatibilidad con toowork con paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19eec-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="19eec-293">Por ejemplo, vea hello [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [agregar una cuenta del grupo de tooan] [ rest_add_pool] para obtener información acerca de cómo toospecify tooinstall de paquetes mediante el uso de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="19eec-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="19eec-294">Vea [aplicaciones] [ rest_applications] para obtener más información acerca de cómo tooobtain información de la aplicación mediante el uso de Hola API de REST de lote.</span><span class="sxs-lookup"><span data-stu-id="19eec-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="19eec-295">Obtenga información acerca de cómo tooprogrammatically [administrar cuentas de lote de Azure y las cuotas con .NET de administración de lotes](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="19eec-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="19eec-296">Hola [.NET de administración de lotes][api_net_mgmt] biblioteca puede habilitar características de creación y eliminación de cuenta para la aplicación de proceso por lotes o el servicio.</span><span class="sxs-lookup"><span data-stu-id="19eec-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagrama de alto nivel de paquetes de aplicación"
[2]: ./media/batch-application-packages/app_pkg_02.png "Icono Aplicaciones en Azure Portal"
[3]: ./media/batch-application-packages/app_pkg_03.png "Hoja Aplicaciones en Azure Portal"
[4]: ./media/batch-application-packages/app_pkg_04.png "Hoja Detalles de aplicación en Azure Portal"
[5]: ./media/batch-application-packages/app_pkg_05.png "Hoja Nueva aplicación en Azure Portal"
[7]: ./media/batch-application-packages/app_pkg_07.png "Lista desplegable Actualizar o eliminar paquetes en Azure Portal"
[8]: ./media/batch-application-packages/app_pkg_08.png "Hoja Nuevo paquete de aplicación en Azure Portal"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerta de ausencia de cuenta de almacenamiento vinculada"
[10]: ./media/batch-application-packages/app_pkg_10.png "Hoja Elegir de cuenta de almacenamiento en Azure Portal"
[11]: ./media/batch-application-packages/app_pkg_11.png "Hoja Actualizar paquete en Azure Portal"
[12]: ./media/batch-application-packages/app_pkg_12.png "Cuadro de diálogo de confirmación de eliminación de paquetes en Azure Portal"
