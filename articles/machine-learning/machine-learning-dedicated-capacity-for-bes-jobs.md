---
title: "aaaDedicated capacidad para trabajos de servicio de ejecución de máquina aprendizaje por lotes | Documentos de Microsoft"
description: "Información general de los servicios de Azure Batch para trabajos de Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="1bc36-103">Servicio de Azure Batch para trabajos de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1bc36-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="1bc36-104">El procesamiento de grupo de lote de aprendizaje de máquina proporciona escala administrada por el cliente para hello servicio de ejecución de lote de aprendizaje de máquina de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc36-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="1bc36-105">Clásico procesamiento por lotes de aprendizaje automático realiza en un entorno de varios inquilinos, se ponen en cola el número de hello límites de trabajos simultáneos que puede enviar y trabajos de forma primero en el primero en salir.</span><span class="sxs-lookup"><span data-stu-id="1bc36-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="1bc36-106">Esta incertidumbre significa que no se puede predecir con exactitud cuándo se ejecutará el trabajo.</span><span class="sxs-lookup"><span data-stu-id="1bc36-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="1bc36-107">Procesamiento por lotes de grupo permite grupos toocreate en el que puede enviar trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="1bc36-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="1bc36-108">Controlar tamaño Hola de grupo de Hola y se envía el trabajo de toowhich grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="1bc36-109">Se ejecuta el trabajo de BES en su propio procesamiento espacio proporcionar rendimiento del procesamiento predecible y grupos de recursos de toocreate de capacidad de Hola que corresponden toohello carga de procesamiento que se envía.</span><span class="sxs-lookup"><span data-stu-id="1bc36-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="1bc36-110">Cómo el procesamiento por lotes grupo toouse</span><span class="sxs-lookup"><span data-stu-id="1bc36-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="1bc36-111">Configuración de grupo de procesamiento por lotes no está actualmente disponible a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc36-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="1bc36-112">toouse grupo de lote de procesamiento, debe:</span><span class="sxs-lookup"><span data-stu-id="1bc36-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="1bc36-113">Llamar a CSS toocreate una cuenta de grupo de lote y obtener una dirección URL de servicio de grupo y una clave de autorización</span><span class="sxs-lookup"><span data-stu-id="1bc36-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="1bc36-114">Crear un servicio web basado en el nuevo Resource Manager y un plan de facturación</span><span class="sxs-lookup"><span data-stu-id="1bc36-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="1bc36-115">toocreate su cuenta, llame al servicio al cliente de Microsoft y soporte técnico (CSS) y proporcione el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="1bc36-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="1bc36-116">CSS funcionará con se toodetermine Hola capacidad apropiada para su escenario.</span><span class="sxs-lookup"><span data-stu-id="1bc36-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="1bc36-117">CSS, a continuación, configura la cuenta con un número máximo de grupos que puede crear y Hola número máximo de máquinas virtuales (VM) que se pueden colocar en cada grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="1bc36-118">Una vez que su cuenta está configurada, se le proporciona la dirección URL del servicio de grupo y una clave de autorización.</span><span class="sxs-lookup"><span data-stu-id="1bc36-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="1bc36-119">Después de crea su cuenta, use Hola dirección URL del servicio de grupo y la autorización tooperform clave grupo operaciones de administración en el grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="1bc36-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Arquitectura del servicio de grupo de lote.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="1bc36-121">Crear grupos mediante una llamada a operación de crear un grupo de hello en dirección URL del servicio de grupo de Hola que tooyou CSS proporcionado.</span><span class="sxs-lookup"><span data-stu-id="1bc36-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="1bc36-122">Cuando se crea un grupo, especifique número Hola de máquinas virtuales y la dirección URL de Hola de hello swagger.json de un nuevo administrador de recursos según el servicio web de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="1bc36-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="1bc36-123">Este servicio web se proporciona la asociación de facturación tooestablish Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="1bc36-124">Hola servicio del grupo de proceso por lotes utiliza grupo Hola de hello swagger.json tooassociate con un plan de facturación.</span><span class="sxs-lookup"><span data-stu-id="1bc36-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="1bc36-125">Puede ejecutar a cualquier BES servicio web, ambos nuevo administrador de recursos según y clásico, elija en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="1bc36-126">Puede usar ningún nuevo administrador de recursos en función de servicio web, pero tenga en cuenta que la facturación Hola de trabajos de Hola se cobra con respecto al plan de facturación de hello asociado a ese servicio.</span><span class="sxs-lookup"><span data-stu-id="1bc36-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="1bc36-127">Puede que desee toocreate un servicio web y la facturación nuevo plan específicamente para ejecutar trabajos de grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="1bc36-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="1bc36-128">Para más información sobre la implementación de servicios web, vea el artículo [Implementar un servicio web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="1bc36-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="1bc36-129">Una vez que ha creado un grupo, enviar Hola BES trabajo mediante Hola dirección URL de las solicitudes de lote para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="1bc36-130">Puede elegir toosubmit se tooa grupo o tooclassic el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="1bc36-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="1bc36-131">toosubmit un procesamiento de grupo de trabajo tooBatch, agregue Hola siguiendo el cuerpo de la solicitud de envío de trabajo parámetro toohello:</span><span class="sxs-lookup"><span data-stu-id="1bc36-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="1bc36-132">"AzureBatchPoolId": "&lt;ID de grupo&gt;"</span><span class="sxs-lookup"><span data-stu-id="1bc36-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="1bc36-133">Si no agrega el parámetro hello, trabajo de Hola se ejecuta en el entorno de proceso por lotes clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="1bc36-134">Si el grupo de hello tenga recursos disponibles, el trabajo de hello comienza a ejecutarse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="1bc36-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="1bc36-135">Si el grupo de hello no tiene liberar recursos, el trabajo está en cola hasta que un recurso esté disponible.</span><span class="sxs-lookup"><span data-stu-id="1bc36-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="1bc36-136">Si encuentra que con regularidad alcanzar capacidad Hola de los grupos y necesita una mayor capacidad, puede llamar a CSS y trabajar con un representante de tooincrease las cuotas.</span><span class="sxs-lookup"><span data-stu-id="1bc36-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="1bc36-137">Solicitud de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1bc36-137">Example Request:</span></span>

<span data-ttu-id="1bc36-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="1bc36-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="1bc36-139">Consideraciones al usar el procesamiento de grupo de lote</span><span class="sxs-lookup"><span data-stu-id="1bc36-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="1bc36-140">Grupo de procesamiento por lotes es un servicio facturable permanente y que requiere tooassociate, con un administrador de recursos según el plan de facturación.</span><span class="sxs-lookup"><span data-stu-id="1bc36-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="1bc36-141">Solo se factura número Hola de horas de proceso se está ejecutando el grupo de hello; independientemente del número de Hola de trabajos que se ejecutan durante ese grupo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1bc36-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="1bc36-142">Si crea un grupo, se le facturará para horas de proceso de Hola de cada máquina virtual en el grupo de hello hasta que se elimine el grupo de hello, incluso si no hay trabajos por lotes se ejecutan en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc36-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="1bc36-143">La facturación para las máquinas virtuales de Hola se inicia cuando ha terminado el aprovisionamiento y se detiene cuando se han eliminado.</span><span class="sxs-lookup"><span data-stu-id="1bc36-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="1bc36-144">Puede usar cualquiera de los planes de Hola se encuentra en hello [página de precios de aprendizaje de máquina](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="1bc36-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="1bc36-145">Ejemplo de facturación:</span><span class="sxs-lookup"><span data-stu-id="1bc36-145">Billing example:</span></span>

<span data-ttu-id="1bc36-146">Si crea un grupo de lote con 2 máquinas virtuales y lo elimina después de 24 horas, el plan de facturación se realiza con un cargo de 48 horas de proceso; independientemente de cuántos trabajos se hayan ejecutado durante ese período.</span><span class="sxs-lookup"><span data-stu-id="1bc36-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="1bc36-147">Si crea un grupo de lote con 4 máquinas virtuales y lo elimina después de 12 horas, el plan de facturación también se realiza con un cargo de 48 horas de proceso.</span><span class="sxs-lookup"><span data-stu-id="1bc36-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="1bc36-148">Se recomienda que sondear toodetermine de estado del trabajo de hello cuando se completan los trabajos.</span><span class="sxs-lookup"><span data-stu-id="1bc36-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="1bc36-149">Cuando todos los trabajos han terminado de ejecutarse, llamada Hola Resize Pool operación tooset Hola número de máquinas virtuales de hello toozero de grupo.</span><span class="sxs-lookup"><span data-stu-id="1bc36-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="1bc36-150">Si dispone de poco en recursos del grupo y necesita toocreate un nuevo grupo, por ejemplo toobill frente a un plan de facturación diferente, puede eliminar grupo hello en su lugar, cuando han terminado de ejecutar todos los trabajos.</span><span class="sxs-lookup"><span data-stu-id="1bc36-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="1bc36-151">**Use procesamiento de grupo de lote cuando**</span><span class="sxs-lookup"><span data-stu-id="1bc36-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="1bc36-152">**Use procesamiento por lotes clásico cuando**</span><span class="sxs-lookup"><span data-stu-id="1bc36-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="1bc36-153">Necesita toorun un gran número de trabajos</span><span class="sxs-lookup"><span data-stu-id="1bc36-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="1bc36-154">O</span><span class="sxs-lookup"><span data-stu-id="1bc36-154">Or</span></span><br/><span data-ttu-id="1bc36-155">Necesita tooknow que los trabajos se ejecutarán inmediatamente</span><span class="sxs-lookup"><span data-stu-id="1bc36-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="1bc36-156">O</span><span class="sxs-lookup"><span data-stu-id="1bc36-156">Or</span></span><br/><span data-ttu-id="1bc36-157">Necesita rendimiento garantizado.</span><span class="sxs-lookup"><span data-stu-id="1bc36-157">You need guaranteed throughput.</span></span> <span data-ttu-id="1bc36-158">Por ejemplo, necesita toorun un número de trabajos en un periodo de tiempo especificado y desea tooscale espera su toomeet de recursos de proceso de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="1bc36-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="1bc36-159">Tiene unos pocos trabajos para ejecutar</span><span class="sxs-lookup"><span data-stu-id="1bc36-159">You are running just a few jobs</span></span><br/><span data-ttu-id="1bc36-160">y</span><span class="sxs-lookup"><span data-stu-id="1bc36-160">And</span></span><br/> <span data-ttu-id="1bc36-161">No es necesario Hola trabajos toorun inmediatamente</span><span class="sxs-lookup"><span data-stu-id="1bc36-161">You don’t need hello jobs toorun immediately</span></span> |
