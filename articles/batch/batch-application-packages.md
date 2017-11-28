---
title: "Instalación de paquetes de aplicaciones en nodos de proceso - Azure Batch | Microsoft Docs"
description: "Utilice la característica paquetes de aplicación de Lote de Azure para administrar fácilmente varias aplicaciones y versiones para la instalación en nodos de proceso de Lote."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="e9651-103">Implementación de aplicaciones en nodos de proceso con paquetes de aplicaciones de Batch</span><span class="sxs-lookup"><span data-stu-id="e9651-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="e9651-104">La característica de paquetes de aplicación de Lote de Azure permite administrar e implementar fácilmente aplicaciones de tareas en los nodos de proceso de un grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="e9651-105">Con paquetes de aplicación, puede cargar y administrar fácilmente varias versiones de las aplicaciones que las tareas ejecutan, incluidos los archivos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="e9651-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="e9651-106">A continuación, se pueden implementar automáticamente una o varias de estas aplicaciones en los nodos de proceso del grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="e9651-107">En este artículo, aprenderá cómo cargar y administrar paquetes de aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9651-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="e9651-108">A continuación, aprenderá a instalarlos en nodos de proceso de un grupo mediante la biblioteca de [.NET para Batch][api_net].</span><span class="sxs-lookup"><span data-stu-id="e9651-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e9651-109">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="e9651-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="e9651-110">Se admiten en los grupos de Batch creados entre el 10 de marzo de 2016 y el 5 de julio de 2017 únicamente si el grupo se creó mediante una configuración de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="e9651-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="e9651-111">Los grupos de Batch creados antes del 10 de marzo de 2016 no admiten los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e9651-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="e9651-112">Las API para crear y administrar paquetes de aplicaciones forman parte de la biblioteca [.NET de administración de lotes] [[api_net_mgmt]].</span><span class="sxs-lookup"><span data-stu-id="e9651-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="e9651-113">Las API para la instalación de paquetes de aplicaciones en un nodo de proceso forman parte de la biblioteca [.NET de lotes][api_net].</span><span class="sxs-lookup"><span data-stu-id="e9651-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="e9651-114">La característica de paquetes de aplicaciones que se describe aquí reemplaza a la característica de aplicaciones de Lote disponible en versiones anteriores del servicio.</span><span class="sxs-lookup"><span data-stu-id="e9651-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="e9651-115">Requisitos de los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-115">Application package requirements</span></span>
<span data-ttu-id="e9651-116">Para utilizar paquetes de aplicación, primero se debe [vincular una cuenta de Azure Storage](#link-a-storage-account) a su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="e9651-117">Esta característica se introdujo en la [API de REST de Batch][api_rest] versión 2015-12-01.2.2, y la correspondiente biblioteca de [.NET para Batch][api_net], versión 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="e9651-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="e9651-118">Si se trabaja con Lote, se recomienda utilizar siempre la versión más reciente de la API.</span><span class="sxs-lookup"><span data-stu-id="e9651-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="e9651-119">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="e9651-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="e9651-120">Se admiten en los grupos de Batch creados entre el 10 de marzo de 2016 y el 5 de julio de 2017 únicamente si el grupo se creó mediante una configuración de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="e9651-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="e9651-121">Los grupos de Batch creados antes del 10 de marzo de 2016 no admiten los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e9651-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="e9651-122">Acerca de las aplicaciones y los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-122">About applications and application packages</span></span>
<span data-ttu-id="e9651-123">En Lote de Azure, una *aplicación* hace referencia a un conjunto de archivos binarios con versiones que se pueden descargar automáticamente en los nodos de proceso del grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="e9651-124">Un *paquete de aplicación* hace referencia a un *conjunto específico* de dichos archivos binarios y representa una *versión* determinada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="e9651-125">![Diagrama de alto nivel de aplicaciones y paquetes de aplicación][1]</span><span class="sxs-lookup"><span data-stu-id="e9651-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="e9651-126">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e9651-126">Applications</span></span>
<span data-ttu-id="e9651-127">Una aplicación en Lote contiene uno o más paquetes de aplicación y especifica las opciones de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="e9651-128">Por ejemplo, una aplicación puede especificar la versión predeterminada del paquete de aplicación que se instala en los nodos de proceso y si sus paquetes se pueden actualizar o eliminar.</span><span class="sxs-lookup"><span data-stu-id="e9651-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="e9651-129">paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-129">Application packages</span></span>
<span data-ttu-id="e9651-130">Un paquete de aplicación es un archivo .zip que contiene los archivos binarios de la aplicación y los archivos auxiliares que se requieren para que las tareas ejecuten la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="e9651-131">Cada paquete de aplicación representa una versión específica de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="e9651-132">Los paquetes de aplicaciones se pueden especificar a niveles de grupo y de tarea.</span><span class="sxs-lookup"><span data-stu-id="e9651-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="e9651-133">Puede especificar uno o varios de estos paquetes y (opcionalmente) una versión cuando crea un grupo o tarea.</span><span class="sxs-lookup"><span data-stu-id="e9651-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="e9651-134">**paquetes de aplicación del grupo** se implementan en *cada* nodo del grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="e9651-135">Las aplicaciones se implementan cuando un nodo se une a un grupo y cuando se reinicia o se restablece la imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="e9651-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="e9651-136">Los paquetes de aplicación de grupo son adecuados cuando todos los nodos de un grupo ejecutan las tareas de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e9651-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="e9651-137">Puede especificar uno o más paquetes de aplicación cuando se crea un grupo y puede agregar o actualizar los paquetes de un grupo ya existente.</span><span class="sxs-lookup"><span data-stu-id="e9651-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="e9651-138">Si actualiza los paquetes de aplicaciones de un grupo existente, debe reiniciar los nodos para instalar el nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="e9651-139">**paquetes de aplicación de tareas** solo se implementan en un nodo de proceso programado para ejecutar una tarea, justo antes de ejecutar la línea de comandos de la tarea.</span><span class="sxs-lookup"><span data-stu-id="e9651-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="e9651-140">Si el paquete de aplicación y la versión especificados ya están en el nodo, este no se volverá a implementar y se utilizará el paquete existente.</span><span class="sxs-lookup"><span data-stu-id="e9651-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="e9651-141">Los paquetes de aplicaciones de tareas son útiles en entornos de grupo compartido, donde los distintos trabajos se ejecutan en un grupo que no se elimina cuando se completa un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e9651-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="e9651-142">Si el trabajo tiene menos tareas que nodos en el grupo, los paquetes de aplicación de las tareas pueden minimizar la transferencia de datos, ya que la aplicación se implementa solo en los nodos que ejecutan tareas.</span><span class="sxs-lookup"><span data-stu-id="e9651-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="e9651-143">Otros escenarios que pueden beneficiarse de los paquetes de aplicación de tareas son los trabajos que ejecutan una aplicación grande, pero solo para unas pocas tareas.</span><span class="sxs-lookup"><span data-stu-id="e9651-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="e9651-144">Por ejemplo, en una fase previa al procesamiento o una tarea de combinación, donde la aplicación de procesamiento previo o combinación es pesada, puede ser útil usar paquetes de aplicación de tareas.</span><span class="sxs-lookup"><span data-stu-id="e9651-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9651-145">Hay restricciones en el número de aplicaciones y paquetes de aplicación que puede haber en una cuenta de Batch, así como en el tamaño máximo del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="e9651-146">Para más información sobre estos límites, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="e9651-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="e9651-147">Ventajas de los paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-147">Benefits of application packages</span></span>
<span data-ttu-id="e9651-148">Los paquetes de aplicación pueden simplificar el código de su solución de Lote y reducir la sobrecarga requerida para administrar las aplicaciones que ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="e9651-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="e9651-149">Con los paquetes de aplicación, la tarea de inicio del grupo no tiene que especificar una larga lista de archivos de recursos individuales que se deben instalar en los nodos.</span><span class="sxs-lookup"><span data-stu-id="e9651-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="e9651-150">No es preciso administrar manualmente varias versiones de los archivos de la aplicación en Almacenamiento de Azure ni en los nodos.</span><span class="sxs-lookup"><span data-stu-id="e9651-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="e9651-151">Y tampoco es preciso preocuparse de generar [direcciones URL de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para proporcionar acceso a los archivos de su cuenta de Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e9651-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="e9651-152">Lote funciona en segundo plano con el Almacenamiento de Azure para almacenar paquetes de aplicación e implementarlos en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="e9651-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="e9651-153">El tamaño total de una tarea de inicio debe ser menor o igual a 32 768 caracteres, incluidos los archivos de recursos y las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="e9651-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="e9651-154">Si la tarea de inicio supera este límite, en este caso usar paquetes de aplicación es otra opción.</span><span class="sxs-lookup"><span data-stu-id="e9651-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="e9651-155">Puede crear también un archivo comprimido que contiene los archivos de recursos, cargarlo como un blob en Azure Storage y. después, descomprímalo en línea de comandos de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="e9651-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="e9651-156">Carga y administración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e9651-156">Upload and manage applications</span></span>
<span data-ttu-id="e9651-157">Puede usar el [Azure Portal][portal] o la biblioteca de [Batch Management .NET](batch-management-dotnet.md) para administrar los paquetes de aplicaciones en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="e9651-158">En las siguientes secciones, primero se muestra cómo vinculará primero una cuenta de Storage y, después, se analizará la incorporación de paquetes y aplicaciones y su administración con el portal.</span><span class="sxs-lookup"><span data-stu-id="e9651-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="e9651-159">Vínculo a una cuenta de Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e9651-159">Link a Storage account</span></span>
<span data-ttu-id="e9651-160">Para utilizar paquetes de aplicación, primero se debe vincular una cuenta de Almacenamiento de Azure a su cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="e9651-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="e9651-161">Si aún no ha configurado ninguna cuenta de almacenamiento, Azure Portal muestra una advertencia la primera vez que haga clic en el icono **Aplicaciones** en la hoja **Cuenta de Batch**.</span><span class="sxs-lookup"><span data-stu-id="e9651-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9651-162">Actualmente, Batch *solo* admite el tipo de cuenta de almacenamiento **de uso general**, tal y como se describe en el paso 5 de la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e9651-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e9651-163">Cuando vincula una cuenta de Azure Storage a su cuenta de Batch, *solo* se vincula una cuenta de almacenamiento de **Uso general**.</span><span class="sxs-lookup"><span data-stu-id="e9651-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="e9651-164">![Advertencia de que no hay cuentas de almacenamiento configuradas en Azure Portal][9]</span><span class="sxs-lookup"><span data-stu-id="e9651-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="e9651-165">El servicio Batch utiliza la cuenta de Storage asociada para almacenar los paquetes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="e9651-166">Una vez que haya vinculado las dos cuentas, Lote puede implementar automáticamente los paquetes almacenados en la cuenta de Almacenamiento vinculada en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="e9651-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="e9651-167">Para vincular una cuenta de Storage a su cuenta de Batch, haga clic en **Configuración de cuenta de almacenamiento** en la hoja **Advertencia**; después, en **Cuenta de almacenamiento** en la hoja **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="e9651-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="e9651-168">![Hoja Elegir de cuenta de almacenamiento en Azure Portal][10]</span><span class="sxs-lookup"><span data-stu-id="e9651-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="e9651-169">Se recomienda crear una cuenta de Storage *específicamente* para su uso con la cuenta de Batch y seleccionarla aquí.</span><span class="sxs-lookup"><span data-stu-id="e9651-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="e9651-170">Para más información sobre cómo crear una cuenta de almacenamiento, consulte la sección "Crear una cuenta de almacenamiento" en [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e9651-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e9651-171">Una vez que haya creado una cuenta de Almacenamiento, puede vincularla a su cuenta de Lote mediante la hoja **Cuenta de almacenamiento** .</span><span class="sxs-lookup"><span data-stu-id="e9651-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="e9651-172">El servicio Batch utiliza Azure Storage para almacenar los paquetes de aplicación como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="e9651-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="e9651-173">Se le [cobrará de la forma habitual][storage_pricing] por los datos de los blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="e9651-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="e9651-174">Asegúrese de considerar el tamaño y número de los paquetes de aplicación y elimine periódicamente los paquetes en desuso para minimizar los costos.</span><span class="sxs-lookup"><span data-stu-id="e9651-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="e9651-175">Visualización de las aplicaciones actuales</span><span class="sxs-lookup"><span data-stu-id="e9651-175">View current applications</span></span>
<span data-ttu-id="e9651-176">Para ver las aplicaciones en la cuenta de Batch, haga clic en el elemento de menú **Aplicaciones** situado en el menú de la izquierda de la hoja **Cuenta de Batch**.</span><span class="sxs-lookup"><span data-stu-id="e9651-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="e9651-177">![Icono Aplicaciones][2]</span><span class="sxs-lookup"><span data-stu-id="e9651-177">![Applications tile][2]</span></span>

<span data-ttu-id="e9651-178">Al seleccionar esta opción de menú, se abre la hoja **Aplicaciones**:</span><span class="sxs-lookup"><span data-stu-id="e9651-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="e9651-179">![Lista de aplicaciones][3]</span><span class="sxs-lookup"><span data-stu-id="e9651-179">![List applications][3]</span></span>

<span data-ttu-id="e9651-180">La hoja **Aplicaciones** muestra el identificador de cada aplicación de su cuenta y las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="e9651-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="e9651-181">**Paquetes**: el número de versiones asociadas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="e9651-182">**Versión predeterminada**: la versión de la aplicación que se instala si no indica ninguna versión al especificar la aplicación para un grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="e9651-183">Esta configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="e9651-183">This setting is optional.</span></span>
* <span data-ttu-id="e9651-184">**Permitir actualizaciones**: el valor que especifica si se permiten actualizaciones, eliminaciones y adiciones en el paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="e9651-185">Si se establece en **No**, las actualizaciones y eliminaciones se deshabilitan para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="e9651-186">Solo se pueden agregar versiones nuevas del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-186">Only new application package versions can be added.</span></span> <span data-ttu-id="e9651-187">El valor predeterminado es **Sí**.</span><span class="sxs-lookup"><span data-stu-id="e9651-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="e9651-188">Visualización de los detalles de una aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-188">View application details</span></span>
<span data-ttu-id="e9651-189">Para abrir la hoja que incluye los detalles de la aplicación, seleccione la aplicación en la hoja **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e9651-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="e9651-190">![Detalles de la aplicación][4]</span><span class="sxs-lookup"><span data-stu-id="e9651-190">![Application details][4]</span></span>

<span data-ttu-id="e9651-191">En la hoja de detalles de la aplicación, puede configurar los siguientes valores de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="e9651-192">**Permitir actualizaciones**: especifica si se pueden actualizar o eliminar sus paquetes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="e9651-193">Consulte "Actualización o eliminación de un paquete de aplicación" más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e9651-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="e9651-194">**Versión predeterminada**: especifique el paquete de aplicación predeterminado que se implementa en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="e9651-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="e9651-195">**Nombre para mostrar**: especifica un nombre "descriptivo" que la solución de Batch puede usar al mostrar información de la aplicación, por ejemplo, en la interfaz de usuario de un servicio que proporciona a los clientes a través de Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="e9651-196">Adición de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-196">Add a new application</span></span>
<span data-ttu-id="e9651-197">Para crear una aplicación, agregue un paquete de aplicación y especifique un identificador de aplicación nuevo y exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e9651-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="e9651-198">El primer paquete de aplicación que agregue con el nuevo identificador de aplicación también crea la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="e9651-199">Haga clic en **Agregar** en la hoja **Aplicaciones** para abrir la hoja **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e9651-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="e9651-200">![Hoja Nueva aplicación en Azure Portal][5]</span><span class="sxs-lookup"><span data-stu-id="e9651-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="e9651-201">La hoja **Nueva aplicación** proporciona los siguientes campos para especificar la configuración de la nueva aplicación y del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="e9651-202">**Id. de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="e9651-202">**Application id**</span></span>

<span data-ttu-id="e9651-203">Este campo especifica el identificador de la nueva aplicación, que está sujeto a las reglas de validación estándar de identificadores de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="e9651-204">Las reglas para proporcionar un identificador de aplicación son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="e9651-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="e9651-205">En los nodos de Windows, el identificador puede contener cualquier combinación de caracteres alfanuméricos, guiones y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="e9651-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="e9651-206">En los nodos de Linux, solo se permiten caracteres alfanuméricos y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="e9651-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="e9651-207">No pueden contener más de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e9651-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="e9651-208">Deben ser único en la cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="e9651-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="e9651-209">Conserva las mayúsculas y minúsculas, aunque no las distingue.</span><span class="sxs-lookup"><span data-stu-id="e9651-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="e9651-210">**Versión**</span><span class="sxs-lookup"><span data-stu-id="e9651-210">**Version**</span></span>

<span data-ttu-id="e9651-211">Este campo especifica la versión del paquete de aplicación que se carga.</span><span class="sxs-lookup"><span data-stu-id="e9651-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="e9651-212">Las cadenas de la versión están sujetas a las siguientes reglas de validación:</span><span class="sxs-lookup"><span data-stu-id="e9651-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="e9651-213">En los nodos de Windows, la cadena de versión puede contener cualquier combinación de caracteres alfanuméricos, guiones, caracteres de subrayado y puntos.</span><span class="sxs-lookup"><span data-stu-id="e9651-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="e9651-214">En los nodos de Linux, la cadena de versión solo puede contener caracteres alfanuméricos y de subred.</span><span class="sxs-lookup"><span data-stu-id="e9651-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="e9651-215">No pueden contener más de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e9651-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="e9651-216">Deben ser únicas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-216">Must be unique within the application.</span></span>
* <span data-ttu-id="e9651-217">Conservan las mayúsculas y minúsculas, aunque no las distinguen.</span><span class="sxs-lookup"><span data-stu-id="e9651-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="e9651-218">**Paquete de aplicación**</span><span class="sxs-lookup"><span data-stu-id="e9651-218">**Application package**</span></span>

<span data-ttu-id="e9651-219">Este campo especifica el archivo .zip que contiene los archivos binarios y los archivos auxiliares necesarios para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="e9651-220">Haga clic en el cuadro **Seleccionar un archivo** o en el icono de la carpeta a la que desee desplazarse y seleccione un archivo .zip que contenga los archivos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="e9651-221">Una vez que haya seleccionado un archivo, haga clic en **Aceptar** para iniciar la carga en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9651-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="e9651-222">Una vez completada la operación de carga, el portal muestra una notificación y cierra la hoja.</span><span class="sxs-lookup"><span data-stu-id="e9651-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="e9651-223">En función del tamaño del archivo que se va a cargar y de la velocidad de la conexión de red, esta operación puede tardar un tiempo.</span><span class="sxs-lookup"><span data-stu-id="e9651-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="e9651-224">No cierre la hoja **Nueva aplicación** antes de que se complete la operación de carga.</span><span class="sxs-lookup"><span data-stu-id="e9651-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="e9651-225">Si lo hace, se detendrá el proceso de carga.</span><span class="sxs-lookup"><span data-stu-id="e9651-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="e9651-226">Adición de un nuevo paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-226">Add a new application package</span></span>
<span data-ttu-id="e9651-227">Para agregar una nueva versión del paquete de aplicación para una aplicación existente, seleccione una aplicación en la hoja **Aplicaciones**, haga clic en **Paquetes** y en **Agregar** para abrir la hoja **Agregar paquete**.</span><span class="sxs-lookup"><span data-stu-id="e9651-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="e9651-228">![Hoja Agregar paquete de aplicación en Azure Portal][8]</span><span class="sxs-lookup"><span data-stu-id="e9651-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="e9651-229">Como puede ver, los campos coinciden con los de la hoja **Nueva aplicación**, excepto el cuadro de texto **Id. de aplicación**, que está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="e9651-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="e9651-230">Como hizo para la nueva aplicación, especifique la **Versión** del paquete nuevo, vaya al archivo .zip de su **Paquete de aplicación** y haga clic en **Aceptar** para cargar el paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="e9651-231">Actualización o eliminación de un paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="e9651-231">Update or delete an application package</span></span>
<span data-ttu-id="e9651-232">Para actualizar o eliminar un paquete de aplicación existente, abra la hoja de detalles de la aplicación, haga clic en **Paquetes** para abrir la hoja **Paquetes** y en los **puntos suspensivos** de la fila del paquete de aplicación que desee modificar, y seleccione la acción que desee realizar.</span><span class="sxs-lookup"><span data-stu-id="e9651-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="e9651-233">![Actualizar o eliminar paquete en Azure Portal][7]</span><span class="sxs-lookup"><span data-stu-id="e9651-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="e9651-234">**Actualización**</span><span class="sxs-lookup"><span data-stu-id="e9651-234">**Update**</span></span>

<span data-ttu-id="e9651-235">Al hacer clic en **Actualizar**, se muestra la hoja *Actualizar paquete*.</span><span class="sxs-lookup"><span data-stu-id="e9651-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="e9651-236">Esta hoja es similar a la hoja *New application package* (Nuevo paquete de aplicación). Sin embargo, solo está habilitado el campo de selección de paquete, lo que permite especificar un nuevo archivo ZIP para cargarlo.</span><span class="sxs-lookup"><span data-stu-id="e9651-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="e9651-237">![Hoja Actualizar paquete en Azure Portal][11]</span><span class="sxs-lookup"><span data-stu-id="e9651-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="e9651-238">**Eliminar**</span><span class="sxs-lookup"><span data-stu-id="e9651-238">**Delete**</span></span>

<span data-ttu-id="e9651-239">Al hacer clic en **Eliminar**, se le pedirá que confirme la eliminación de la versión del paquete y Lote eliminará el paquete de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9651-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="e9651-240">Si elimina la versión predeterminada de una aplicación, la configuración de la **Versión predeterminada** se quita de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="e9651-241">![Eliminar aplicación][12]</span><span class="sxs-lookup"><span data-stu-id="e9651-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="e9651-242">Instalación de aplicaciones en nodos de proceso</span><span class="sxs-lookup"><span data-stu-id="e9651-242">Install applications on compute nodes</span></span>
<span data-ttu-id="e9651-243">Ahora que ha aprendido cómo administrar paquetes de aplicación con Azure Portal, podemos analizar cómo implementarlos en los nodos de proceso y ejecutarlos con las tareas de Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="e9651-244">Instalación de paquetes de aplicación de grupos</span><span class="sxs-lookup"><span data-stu-id="e9651-244">Install pool application packages</span></span>
<span data-ttu-id="e9651-245">Para instalar un paquete de aplicación en todos los nodos de proceso de un grupo, especifique una o varias *referencias* de paquetes de aplicación para el grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="e9651-246">Los paquetes de aplicación que especifique para un grupo se instalan en cada nodo de proceso cuando este se una al grupo, además de cuando se reinicie o se restablezca la imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="e9651-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="e9651-247">En el entorno de .NET para Batch, especifique una o varias [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] al crear el grupo o para un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="e9651-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="e9651-248">La clase [ApplicationPackageReference][net_pkgref] especifica una versión y un identificador de la aplicación que se va a instalar en los nodos de proceso de un grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="e9651-249">Si, por cualquier motivo, se produce un error en una implementación del paquete de aplicación, el servicio Batch marca el nodo como [inutilizable][net_nodestate] y no se programarán tareas de ejecución en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="e9651-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="e9651-250">En este caso, debería **reiniciar** el nodo para reiniciar la implementación del paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="e9651-251">Al reiniciar el nodo, también se vuelve a habilitar la programación de tareas en el nodo.</span><span class="sxs-lookup"><span data-stu-id="e9651-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="e9651-252">Instalación de paquetes de aplicación de tareas</span><span class="sxs-lookup"><span data-stu-id="e9651-252">Install task application packages</span></span>
<span data-ttu-id="e9651-253">De forma similar a un grupo, puede especificar las *referencias* de un paquete de aplicación para una tarea.</span><span class="sxs-lookup"><span data-stu-id="e9651-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="e9651-254">Cuando una tarea está programada para ejecutarse en un nodo, el paquete se descarga y extrae justo antes de ejecutar la línea de comandos de la tarea.</span><span class="sxs-lookup"><span data-stu-id="e9651-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="e9651-255">Si el paquete y versión especificados ya están instalados en el nodo, el paquete no se descarga y se utiliza el paquete existente.</span><span class="sxs-lookup"><span data-stu-id="e9651-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="e9651-256">Para instalar un paquete de aplicación de tareas, configure la propiedad [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref]:</span><span class="sxs-lookup"><span data-stu-id="e9651-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="e9651-257">Ejecución de las aplicaciones instaladas</span><span class="sxs-lookup"><span data-stu-id="e9651-257">Execute the installed applications</span></span>
<span data-ttu-id="e9651-258">Los paquetes que ha especificado para un grupo o tarea se descargan y extraen en un directorio con nombre dentro del nodo `AZ_BATCH_ROOT_DIR` .</span><span class="sxs-lookup"><span data-stu-id="e9651-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="e9651-259">Lote también permite crear una variable de entorno que contiene la ruta de acceso al directorio con nombre.</span><span class="sxs-lookup"><span data-stu-id="e9651-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="e9651-260">Las líneas de comando de la tarea usan esta variable de entorno al hacer referencia a la aplicación en el nodo.</span><span class="sxs-lookup"><span data-stu-id="e9651-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="e9651-261">En los nodos de Windows, la variable está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9651-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="e9651-262">En los nodos de Linux, el formato es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="e9651-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="e9651-263">Los puntos (.), guiones (-) y signos de número (##) se convierten en caracteres de subrayado en la variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="e9651-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="e9651-264">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e9651-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="e9651-265">`APPLICATIONID` y `version` son los valores que corresponden a la versión de la aplicación y del paquete que ha especificado para la implementación.</span><span class="sxs-lookup"><span data-stu-id="e9651-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="e9651-266">Por ejemplo, si especificó que se debía instalar la versión 2.7 de la aplicación *blender* en los nodos de Windows, las líneas de comando de la tarea usarán esta variable de entorno para tener acceso a sus archivos:</span><span class="sxs-lookup"><span data-stu-id="e9651-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="e9651-267">En los nodos de Linux, especifique la variable de entorno con este formato:</span><span class="sxs-lookup"><span data-stu-id="e9651-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="e9651-268">Cuando carga un paquete de aplicación, puede especificar una versión predeterminada que implementar en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="e9651-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="e9651-269">Si ha especificado una versión predeterminada para una aplicación, puede omitir el sufijo de versión al hacer referencia a ella.</span><span class="sxs-lookup"><span data-stu-id="e9651-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="e9651-270">Puede especificar la versión predeterminada de la aplicación en Azure Portal, en la hoja Aplicaciones, como se muestra en [Carga y administración de aplicaciones](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="e9651-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="e9651-271">Por ejemplo, si especifica la versión "2.7" como la versión predeterminada de la aplicación *blender*, las tareas pueden hacer referencia a la siguiente variable de entorno y, después, los nodos de Windows ejecutarán la versión 2.7:</span><span class="sxs-lookup"><span data-stu-id="e9651-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="e9651-272">El siguiente fragmento de código muestra una línea de comandos de una tarea de ejemplo que inicia la versión predeterminada de la aplicación *blender* :</span><span class="sxs-lookup"><span data-stu-id="e9651-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="e9651-273">Para más información sobre la configuración del entorno del nodo de proceso, consulte el apartado [Configuración del entorno para las tareas](batch-api-basics.md#environment-settings-for-tasks) de [Información general de las características de Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e9651-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="e9651-274">Actualización de los paquetes de aplicación de un grupo</span><span class="sxs-lookup"><span data-stu-id="e9651-274">Update a pool's application packages</span></span>
<span data-ttu-id="e9651-275">Si un grupo existente ya se ha configurado con un paquete de aplicación, se puede especificar un paquete nuevo para el grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="e9651-276">Si especifica una nueva referencia de paquete para un grupo, se aplica lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9651-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="e9651-277">El servicio Batch instala el paquete recién especificado en todos los nodos nuevos que se unen al grupo y en cualquier nodo existente que se reinicie o cuya imagen inicial se restablezca.</span><span class="sxs-lookup"><span data-stu-id="e9651-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="e9651-278">Los nodos de proceso que ya estén en el grupo cuando se actualicen las referencias del paquete no instalan automáticamente el paquete de aplicación nuevo.</span><span class="sxs-lookup"><span data-stu-id="e9651-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="e9651-279">Estos nodos de proceso deben reiniciarse o se debe restablecer su imagen inicial para recibir el nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="e9651-280">Cuando se implementa un nuevo paquete, las variables de entorno creadas reflejan las nuevas referencias del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="e9651-281">En este ejemplo, el grupo existente tiene la versión 2.7 de la aplicación *blender* configurada como una de sus propiedades [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="e9651-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="e9651-282">Para actualizar los nodos del grupo con la versión 2.76b, especifique una nueva clase [ApplicationPackageReference][net_pkgref] con la nueva versión y confirme el cambio.</span><span class="sxs-lookup"><span data-stu-id="e9651-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="e9651-283">Ahora que se ha configurado la nueva versión, el servicio Batch instala la versión 2.76b en todos los nodos *nuevos* que se unan al grupo.</span><span class="sxs-lookup"><span data-stu-id="e9651-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="e9651-284">Para instalar la versión 2.76b en los nodos que *ya* están en el grupo, reinícielos o restablezca su imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="e9651-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="e9651-285">Tenga en cuenta que los nodos reiniciados conservan los archivos de las anteriores implementaciones del paquete.</span><span class="sxs-lookup"><span data-stu-id="e9651-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="e9651-286">Enumeración de las aplicaciones en una cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="e9651-286">List the applications in a Batch account</span></span>
<span data-ttu-id="e9651-287">Puede enumerar las aplicaciones y sus paquetes en una cuenta de Batch mediante el método [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries].</span><span class="sxs-lookup"><span data-stu-id="e9651-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="e9651-288">Encapsulado</span><span class="sxs-lookup"><span data-stu-id="e9651-288">Wrap up</span></span>
<span data-ttu-id="e9651-289">Con los paquetes de aplicación puede ayudar a los clientes a seleccionar las aplicaciones para sus trabajos y especificar la versión exacta que deben usar al procesar los trabajos con su servicio con Lote habilitado.</span><span class="sxs-lookup"><span data-stu-id="e9651-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="e9651-290">También puede proporcionar a los clientes la capacidad de cargar y hacer un seguimiento de sus propias aplicaciones en su servicio.</span><span class="sxs-lookup"><span data-stu-id="e9651-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9651-291">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9651-291">Next steps</span></span>
* <span data-ttu-id="e9651-292">La [API de REST de Batch][api_rest] también proporciona compatibilidad para trabajar con paquetes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9651-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="e9651-293">Por ejemplo, consulte el elemento [applicationPackageReferences][rest_add_pool_with_packages] de [Agregar un grupo a una cuenta][rest_add_pool] para especificar los paquetes que se instalan mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="e9651-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="e9651-294">Para ver detalles sobre cómo obtener información de la aplicación mediante la API de REST de Batch, consulte [Aplicaciones][rest_applications].</span><span class="sxs-lookup"><span data-stu-id="e9651-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="e9651-295">Aprenda a [administrar mediante programación cuentas y cuotas de Lote de Azure con .NET de administración de lotes](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e9651-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="e9651-296">La biblioteca [.NET de administración de Batch][api_net_mgmt] puede habilitar las características de creación y eliminación de cuentas de una aplicación o servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="e9651-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
