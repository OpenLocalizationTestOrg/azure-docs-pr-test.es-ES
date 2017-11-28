---
title: aaaGet iniciar PowerShell para Azure Batch | Documentos de Microsoft
description: "Una introducción rápida se toohello cmdlets de PowerShell de Azure se pueden utilizar los recursos de proceso por lotes toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="f29ca-103">Administración de recursos de Batch con cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f29ca-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="f29ca-104">Con hello cmdlets de PowerShell de lote de Azure, se puede realizar y programan muchas Hola mismas tareas que llevar a cabo con las API de lote, hello Hola portal de Azure y Hola interfaz de línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="f29ca-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="f29ca-105">Se trata de una cmdlets de toohello introducción rápida, puede usar toomanage sus cuentas de lote y trabajar con sus recursos de proceso por lotes como grupos, los trabajos y tareas.</span><span class="sxs-lookup"><span data-stu-id="f29ca-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="f29ca-106">Para obtener una lista completa de cmdlets de lote y la sintaxis de cmdlet detallados, vea hello [referencia de cmdlets de Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="f29ca-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="f29ca-107">Este artículo se basa en los cmdlets de Azure PowerShell versión 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="f29ca-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="f29ca-108">Le recomendamos que actualice su PowerShell de Azure con frecuencia tootake aprovechar las mejoras y las actualizaciones del servicio.</span><span class="sxs-lookup"><span data-stu-id="f29ca-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f29ca-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f29ca-109">Prerequisites</span></span>
<span data-ttu-id="f29ca-110">Realizar Hola siguiendo las operaciones toouse Azure PowerShell toomanage los recursos de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="f29ca-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="f29ca-111">Instalación y configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f29ca-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="f29ca-112">Ejecute hello **AzureRmAccount de inicio de sesión** cmdlet tooconnect tooyour suscripción (Hola directa de cmdlets de Azure Batch en módulo de Azure Resource Manager hello):</span><span class="sxs-lookup"><span data-stu-id="f29ca-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="f29ca-113">**Registrar con el espacio de nombres del proveedor de lote de hello**.</span><span class="sxs-lookup"><span data-stu-id="f29ca-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="f29ca-114">Esta operación solo es necesario toobe realiza **una vez por cada suscripción**.</span><span class="sxs-lookup"><span data-stu-id="f29ca-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="f29ca-115">Administrar claves y cuentas por lotes</span><span class="sxs-lookup"><span data-stu-id="f29ca-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="f29ca-116">Crear una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="f29ca-116">Create a Batch account</span></span>
<span data-ttu-id="f29ca-117">**New-AzureRmBatchAccount** crea una cuenta de Batch en un grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="f29ca-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="f29ca-118">Si ya no tiene un grupo de recursos, crear uno mediante la ejecución de hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f29ca-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="f29ca-119">Especifique uno de hello Azure regiones en hello **ubicación** parámetro, como "Central US".</span><span class="sxs-lookup"><span data-stu-id="f29ca-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="f29ca-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29ca-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="f29ca-121">A continuación, cree una cuenta de lote en grupo de recursos de hello, especificar un nombre de cuenta de hello en <*account_name*> Hola, ubicación y nombre de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="f29ca-122">Crear cuenta de lote de hello puede tardar algún tiempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f29ca-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="f29ca-123">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29ca-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="f29ca-124">cuenta de lote de Hello nombre debe ser único toohello región de Azure para el grupo de recursos de hello, contener entre 3 y 24 caracteres y usar letras minúsculas y números solo.</span><span class="sxs-lookup"><span data-stu-id="f29ca-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="f29ca-125">Obtener claves de acceso de cuenta</span><span class="sxs-lookup"><span data-stu-id="f29ca-125">Get account access keys</span></span>
<span data-ttu-id="f29ca-126">**Get-AzureRmBatchAccountKeys** muestra las teclas de acceso de hello asociadas con una cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="f29ca-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="f29ca-127">Por ejemplo, ejecute hello siguiendo las claves principal y secundaria del Hola de tooget de cuenta de hello que ha creado.</span><span class="sxs-lookup"><span data-stu-id="f29ca-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="f29ca-128">Generar una nueva clave de acceso</span><span class="sxs-lookup"><span data-stu-id="f29ca-128">Generate a new access key</span></span>
<span data-ttu-id="f29ca-129">**New-AzureBatchAccountKey** genera una nueva clave de cuenta principal o secundaria para una cuenta de Lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="f29ca-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="f29ca-130">Por ejemplo, toogenerate una nueva clave principal para la cuenta de proceso por lotes, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29ca-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="f29ca-131">toogenerate una nueva clave secundaria, especifique "Secundaria" de hello **KeyType** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f29ca-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="f29ca-132">Tener claves primarias y secundarias de hello tooregenerate por separado.</span><span class="sxs-lookup"><span data-stu-id="f29ca-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="f29ca-133">Eliminar una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="f29ca-133">Delete a Batch account</span></span>
<span data-ttu-id="f29ca-134">**Remove-AzureBatchAccount** elimina una cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="f29ca-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="f29ca-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29ca-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="f29ca-136">Cuando se le pida, confirme la cuenta de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="f29ca-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="f29ca-137">Eliminación de cuenta puede tardar algún tiempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f29ca-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="f29ca-138">Creación de un objeto BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="f29ca-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="f29ca-139">usar tooauthenticate Hola cmdlets de PowerShell de lote cuando cree y administre los grupos de proceso por lotes, los trabajos, tareas, y otros recursos, cree primero un toostore de objeto BatchAccountContext el nombre de cuenta y las claves:</span><span class="sxs-lookup"><span data-stu-id="f29ca-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="f29ca-140">Se pasa hello BatchAccountContext objeto en cmdlets que Hola de uso **BatchContext** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f29ca-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="f29ca-141">De forma predeterminada, se utiliza la clave principal de la cuenta de hello para la autenticación, pero puede seleccionar explícitamente Hola clave toouse cambiando el objeto BatchAccountContext **KeyInUse** propiedad: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="f29ca-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="f29ca-142">Creación y modificación de recursos de Lote</span><span class="sxs-lookup"><span data-stu-id="f29ca-142">Create and modify Batch resources</span></span>
<span data-ttu-id="f29ca-143">Usar cmdlets como **New-AzureBatchPool**, **New-AzureBatchJob**, y **New-AzureBatchTask** toocreate recursos bajo una cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="f29ca-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="f29ca-144">Hay correspondientes **Get -** y **Set -** propiedades de hello tooupdate de cmdlets de recursos existentes, y **Remove -** cmdlets tooremove recursos bajo una cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="f29ca-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="f29ca-145">Al utilizar muchos de estos cmdlets en suma toopassing un objeto BatchContext, necesita toocreate o pasar objetos que contienen la configuración de recursos detallado, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="f29ca-146">Vea Hola ayuda detallada de cada cmdlet para obtener ejemplos adicionales.</span><span class="sxs-lookup"><span data-stu-id="f29ca-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="f29ca-147">Crear un grupo de Lote</span><span class="sxs-lookup"><span data-stu-id="f29ca-147">Create a Batch pool</span></span>
<span data-ttu-id="f29ca-148">Al crear o actualizar un grupo de lote, seleccione Configuración del servicio de nube de Hola o configuración de máquina virtual de Hola para hello sistema operativo en hello nodos de proceso (consulte [Introducción a la característica por lotes](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="f29ca-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="f29ca-149">Si especifica la configuración del servicio de nube de hello, se crea la imagen de sus nodos de proceso con uno de hello [versiones del SO invitado de Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="f29ca-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="f29ca-150">Si se especifica la configuración de máquina virtual de hello, puede especificar uno de hello admite Linux u Hola enumerada en las imágenes de máquina virtual de Windows [máquinas virtuales de Azure Marketplace][vm_marketplace], o proporcionar un personalizado imagen que haya preparado.</span><span class="sxs-lookup"><span data-stu-id="f29ca-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="f29ca-151">Al ejecutar **New-AzureBatchPool**, pasar la configuración de sistema operativo de hello en un objeto PSCloudServiceConfiguration o PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="f29ca-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="f29ca-152">Por ejemplo, hello siguiente cmdlet crea un nuevo grupo de lote con nodos de proceso pequeñas de tamaño en la configuración del servicio de nube de hello, crea la imagen con la versión de sistema operativo más reciente de Hola de familia 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="f29ca-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="f29ca-153">En este caso, Hola **CloudServiceConfiguration** parámetro especifica hello *$configuration* variable como objeto de PSCloudServiceConfiguration Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="f29ca-154">Hola **BatchContext** parámetro especifica una variable definida anteriormente *$context* como objeto de BatchAccountContext Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="f29ca-155">número de destino de Hola de nodos de cálculo en el nuevo grupo de hello viene determinado por una fórmula de Autoescala.</span><span class="sxs-lookup"><span data-stu-id="f29ca-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="f29ca-156">En este caso, es simplemente fórmula hello **$TargetDedicated = 4**, que indica el número de Hola de nodos de proceso en el grupo de hello es 4 como máximo.</span><span class="sxs-lookup"><span data-stu-id="f29ca-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="f29ca-157">Consulta de grupos, trabajos, tareas y otros detalles</span><span class="sxs-lookup"><span data-stu-id="f29ca-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="f29ca-158">Usar cmdlets como **Get-AzureBatchPool**, **Get AzureBatchJob**, y **AzureBatchTask Get** tooquery para entidades creadas en una cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="f29ca-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="f29ca-159">Consulta de datos</span><span class="sxs-lookup"><span data-stu-id="f29ca-159">Query for data</span></span>
<span data-ttu-id="f29ca-160">Por ejemplo, usar **AzureBatchPools Get** toofind sus grupos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="f29ca-161">De forma predeterminada, esta consulta para todos los grupos en su cuenta, suponiendo que ya almacenado Hola BatchAccountContext objeto *$context*:</span><span class="sxs-lookup"><span data-stu-id="f29ca-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="f29ca-162">Uso de un filtro OData</span><span class="sxs-lookup"><span data-stu-id="f29ca-162">Use an OData filter</span></span>
<span data-ttu-id="f29ca-163">Puede proporcionar un filtro de OData mediante hello **filtro** parámetro toofind Hola solo objetos que le interesa.</span><span class="sxs-lookup"><span data-stu-id="f29ca-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="f29ca-164">Por ejemplo, puede encontrar todos los grupos cuyos id. empiecen por "myPool":</span><span class="sxs-lookup"><span data-stu-id="f29ca-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="f29ca-165">Este método no es tan flexible como "Where-Object" en una canalización local.</span><span class="sxs-lookup"><span data-stu-id="f29ca-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="f29ca-166">Sin embargo, Hola consulta obtiene envía toohello servicio por lotes directamente para que todos los filtros, se produce en el lado del servidor hello, ahorra ancho de banda de Internet.</span><span class="sxs-lookup"><span data-stu-id="f29ca-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="f29ca-167">Utilice el parámetro de Id. de Hola</span><span class="sxs-lookup"><span data-stu-id="f29ca-167">Use hello Id parameter</span></span>
<span data-ttu-id="f29ca-168">Un filtro de OData tooan alternativo es hello de toouse **identificador** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f29ca-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="f29ca-169">tooquery para un grupo específico con identificador "myPool":</span><span class="sxs-lookup"><span data-stu-id="f29ca-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="f29ca-170">Hola **identificador** parámetro admite sólo búsqueda de identificador completo, no de caracteres comodín o filtros de estilo de OData.</span><span class="sxs-lookup"><span data-stu-id="f29ca-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="f29ca-171">Use el parámetro MaxCount de hello</span><span class="sxs-lookup"><span data-stu-id="f29ca-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="f29ca-172">De forma predeterminada, cada cmdlet devuelve un máximo de 1000 objetos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="f29ca-173">Si se alcanza este límite, refinar su toobring filtro nuevo menos objetos o establecer explícitamente el máximo con hello **MaxCount** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f29ca-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="f29ca-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29ca-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="f29ca-175">establecer el límite superior de tooremove hello, **MaxCount** too0 o menos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="f29ca-176">Usar la canalización de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f29ca-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="f29ca-177">Cmdlets de proceso por lotes puede aprovechar datos de toosend de canalización de PowerShell de hello entre cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f29ca-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="f29ca-178">Esto tiene el mismo efecto que si se especifica un parámetro, pero hace que trabajar con varias entidades sea más fácil de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="f29ca-179">Por ejemplo, busque y muestre todas las tareas de su cuenta:</span><span class="sxs-lookup"><span data-stu-id="f29ca-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="f29ca-180">Reinicie todos los nodos de proceso de un grupo:</span><span class="sxs-lookup"><span data-stu-id="f29ca-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="f29ca-181">Administración de paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="f29ca-181">Application package management</span></span>
<span data-ttu-id="f29ca-182">Paquetes de aplicación proporcionan una manera simplificada toodeploy aplicaciones toohello nodos de cálculo en los grupos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="f29ca-183">Con hello cmdlets de PowerShell de lote, puede cargar y administrar paquetes de aplicaciones en su cuenta de lote e implementar nodos de toocompute de versiones de paquete.</span><span class="sxs-lookup"><span data-stu-id="f29ca-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="f29ca-184">**Cree** una aplicación:</span><span class="sxs-lookup"><span data-stu-id="f29ca-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="f29ca-185">**Agregue** un paquete de aplicación:</span><span class="sxs-lookup"><span data-stu-id="f29ca-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="f29ca-186">Conjunto hello **versión predeterminada** para la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="f29ca-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="f29ca-187">**Muestre** los paquetes de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f29ca-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="f29ca-188">**Elimine** un paquete de aplicación:</span><span class="sxs-lookup"><span data-stu-id="f29ca-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="f29ca-189">**Elimine** una aplicación:</span><span class="sxs-lookup"><span data-stu-id="f29ca-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="f29ca-190">Debe eliminar todas las versiones de paquete de aplicación de la aplicación antes de eliminar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f29ca-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="f29ca-191">Si intentas toodelete una aplicación que tiene actualmente los paquetes de aplicación, recibirá un error de 'Conflicto'.</span><span class="sxs-lookup"><span data-stu-id="f29ca-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="f29ca-192">Implementación de un paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="f29ca-192">Deploy an application package</span></span>
<span data-ttu-id="f29ca-193">Al crear un grupo, puede especificar uno o varios paquetes de aplicación para implementarlos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="f29ca-194">Cuando se especifica un paquete en el momento de creación de grupo, es el nodo de implementada tooeach como grupo de combinaciones de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="f29ca-195">También se implementan paquetes cuando un nodo se reinicia o se restablece su imagen inicial.</span><span class="sxs-lookup"><span data-stu-id="f29ca-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="f29ca-196">Especificar hello `-ApplicationPackageReference` opción al crear un grupo toodeploy nodos de un paquete toohello grupo de aplicaciones cuando se unen a grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="f29ca-197">En primer lugar, cree un **PSApplicationPackageReference** de objetos y configurarlo con la versión de identificador y el paquete de la aplicación de hello desea toodeploy toohello grupo de nodos de proceso:</span><span class="sxs-lookup"><span data-stu-id="f29ca-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="f29ca-198">Ahora crear grupo de Hola y especificar el objeto de referencia de paquete de Hola Hola argumento toohello `ApplicationPackageReferences` opción:</span><span class="sxs-lookup"><span data-stu-id="f29ca-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="f29ca-199">Puede encontrar más información sobre los paquetes de aplicación en [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f29ca-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f29ca-200">Debe [vincular una cuenta de almacenamiento de Azure](#linked-storage-account-autostorage) tooyour lote cuenta toouse paquetes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f29ca-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="f29ca-201">Actualización de los paquetes de aplicación de un grupo</span><span class="sxs-lookup"><span data-stu-id="f29ca-201">Update a pool's application packages</span></span>
<span data-ttu-id="f29ca-202">las aplicaciones de hello tooupdate asignadas tooan grupo existente, cree primero un objeto de PSApplicationPackageReference con propiedades de hello deseado (paquete y el Id. de versión de la aplicación):</span><span class="sxs-lookup"><span data-stu-id="f29ca-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="f29ca-203">A continuación, obtener grupo de hello del lote, borrar todos los paquetes existentes, agregar la nueva referencia de paquete y actualizar servicio por lotes de hello con la nueva configuración de la agrupación de hello:</span><span class="sxs-lookup"><span data-stu-id="f29ca-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="f29ca-204">Ahora ha actualizado propiedades del grupo de hello en el servicio de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29ca-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="f29ca-205">tooactually implementar Hola nueva aplicación paquete toocompute nodos de grupo de hello, sin embargo, debe reiniciar o Restablecer imagen inicial de dichos nodos.</span><span class="sxs-lookup"><span data-stu-id="f29ca-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="f29ca-206">Puede reiniciar todos los nodos de un grupo con este comando:</span><span class="sxs-lookup"><span data-stu-id="f29ca-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="f29ca-207">Puede implementar varias aplicaciones paquetes toohello nodos de proceso en un grupo.</span><span class="sxs-lookup"><span data-stu-id="f29ca-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="f29ca-208">Si lo desea demasiado*agregar* un paquete de aplicación en lugar de reemplazar los paquetes de saludo implementada actualmente, omitir hello `$pool.ApplicationPackageReferences.Clear()` línea anterior.</span><span class="sxs-lookup"><span data-stu-id="f29ca-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f29ca-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f29ca-209">Next steps</span></span>
* <span data-ttu-id="f29ca-210">Para conocer la sintaxis detallada de cmdlets y ejemplos de los mismos, consulte [Azure Batch Cmdlets](/powershell/module/azurerm.batch/#batch)(Cmdlets de Lote de Azure).</span><span class="sxs-lookup"><span data-stu-id="f29ca-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="f29ca-211">Para obtener más información acerca de las aplicaciones y paquetes de aplicaciones en el lote, vea [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f29ca-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/