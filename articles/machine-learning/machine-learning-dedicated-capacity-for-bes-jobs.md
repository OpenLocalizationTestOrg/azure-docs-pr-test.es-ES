---
title: "Capacidad dedicada para trabajos de servicio de ejecución de lotes de Machine Learning | Microsoft Docs"
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
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="71a0f-103">Servicio de Azure Batch para trabajos de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71a0f-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="71a0f-104">El procesamiento de grupo de lote de Machine Learning proporciona una escala administrada por el cliente para el servicio de ejecución de lotes de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71a0f-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="71a0f-105">El procesamiento por lotes clásico para aprendizaje automático tiene lugar en un entorno de varios inquilinos, lo que limita el número de trabajos simultáneos que se pueden enviar, y los trabajos se ponen en una cola que funciona según el principio de "el primero en entrar es el primero en salir".</span><span class="sxs-lookup"><span data-stu-id="71a0f-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="71a0f-106">Esta incertidumbre significa que no se puede predecir con exactitud cuándo se ejecutará el trabajo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="71a0f-107">El procesamiento de grupo de lote permite crear grupos en los que se pueden enviar trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="71a0f-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="71a0f-108">Usted controla el tamaño del grupo y a qué grupo se envía el trabajo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="71a0f-109">El trabajo BES se ejecuta en su propio espacio de procesamiento, proporcionando un rendimiento del procesamiento predecible y la capacidad para crear grupos de recursos que corresponden a la carga de procesamiento que se envía.</span><span class="sxs-lookup"><span data-stu-id="71a0f-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="71a0f-110">Cómo utilizar el procesamiento de grupo de lote</span><span class="sxs-lookup"><span data-stu-id="71a0f-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="71a0f-111">La configuración del procesamiento de grupo de lote no está actualmente disponible a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="71a0f-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="71a0f-112">Para usar el procesamiento de grupo de lote, tiene que:</span><span class="sxs-lookup"><span data-stu-id="71a0f-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="71a0f-113">Llamar a CSS para crear una cuenta de grupo de lote y obtener una dirección URL de servicio de grupo y una clave de autorización</span><span class="sxs-lookup"><span data-stu-id="71a0f-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="71a0f-114">Crear un servicio web basado en el nuevo Resource Manager y un plan de facturación</span><span class="sxs-lookup"><span data-stu-id="71a0f-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="71a0f-115">Para crear su cuenta, llame al Soporte técnico y el servicio al cliente de Microsoft (CSS) y proporcione el identificador de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="71a0f-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="71a0f-116">CSS trabajará con usted para determinar la capacidad adecuada para su escenario.</span><span class="sxs-lookup"><span data-stu-id="71a0f-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="71a0f-117">A continuación, CSS configura la cuenta con el número máximo de grupos que puede crear y el número máximo de máquinas virtuales que se pueden colocar en cada grupo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="71a0f-118">Una vez que su cuenta está configurada, se le proporciona la dirección URL del servicio de grupo y una clave de autorización.</span><span class="sxs-lookup"><span data-stu-id="71a0f-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="71a0f-119">Después de crear su cuenta, utilice la dirección URL del servicio de grupo y la clave de autorización para realizar operaciones de administración de grupo en el grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="71a0f-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Arquitectura del servicio de grupo de lote.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="71a0f-121">Cree grupos mediante una llamada a la operación Create Pool (Crear grupo) en la dirección URL de servicio de grupo que le proporcionó CSS.</span><span class="sxs-lookup"><span data-stu-id="71a0f-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="71a0f-122">Cuando cree un grupo, especifique el número de máquinas virtuales y la dirección URL de swagger.json de un servicio web de Machine Learning basado en el nuevo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71a0f-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="71a0f-123">Este servicio web se proporciona para establecer la asociación de facturación.</span><span class="sxs-lookup"><span data-stu-id="71a0f-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="71a0f-124">El servicio de grupo de lote utiliza el swagger.json para asociar el grupo a un plan de facturación.</span><span class="sxs-lookup"><span data-stu-id="71a0f-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="71a0f-125">Puede ejecutar cualquier servicio web BES, tanto basado en el nuevo Resource Manager como en el clásico, que elija en el grupo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="71a0f-126">Puede usar cualquier servicio web basado en el nuevo Resource Manager, pero tenga en cuenta que la facturación de los trabajos se cobra con respecto al plan de facturación asociado a ese servicio.</span><span class="sxs-lookup"><span data-stu-id="71a0f-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="71a0f-127">Es posible que desee crear un servicio web y un nuevo plan de facturación específicamente para ejecutar trabajos de grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="71a0f-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="71a0f-128">Para más información sobre la implementación de servicios web, vea el artículo [Implementar un servicio web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="71a0f-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="71a0f-129">Una vez que ha creado un grupo, envíe el trabajo BES usando la dirección URL de las solicitudes de lote para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="71a0f-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="71a0f-130">Puede optar por enviarlo a un grupo o al procesamiento por lotes clásico.</span><span class="sxs-lookup"><span data-stu-id="71a0f-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="71a0f-131">Para enviar un trabajo para procesamiento en un grupo de lote, agregue el siguiente parámetro en el cuerpo de la solicitud de envío del trabajo:</span><span class="sxs-lookup"><span data-stu-id="71a0f-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="71a0f-132">"AzureBatchPoolId": "&lt;ID de grupo&gt;"</span><span class="sxs-lookup"><span data-stu-id="71a0f-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="71a0f-133">Si no se agrega el parámetro, el trabajo se ejecuta en el entorno de procesamiento por lotes clásico.</span><span class="sxs-lookup"><span data-stu-id="71a0f-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="71a0f-134">Si el grupo tiene recursos disponibles, el trabajo empieza a ejecutarse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="71a0f-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="71a0f-135">Si el grupo no tiene recursos libres, el trabajo se coloca en cola hasta que un recurso esté disponible.</span><span class="sxs-lookup"><span data-stu-id="71a0f-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="71a0f-136">Si se da cuenta de que periódicamente alcanza la capacidad de los grupos y necesita una mayor capacidad, puede llamar a CSS y trabajar con un representante para aumentar las cuotas.</span><span class="sxs-lookup"><span data-stu-id="71a0f-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="71a0f-137">Solicitud de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="71a0f-137">Example Request:</span></span>

<span data-ttu-id="71a0f-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="71a0f-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="71a0f-139">Consideraciones al usar el procesamiento de grupo de lote</span><span class="sxs-lookup"><span data-stu-id="71a0f-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="71a0f-140">El procesamiento de grupo de lote es un servicio facturable siempre activado que requiere estar asociado a un plan de facturación basado en Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71a0f-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="71a0f-141">Solo se le facturará por el número de horas de proceso que se esté ejecutando el grupo; independientemente del número de trabajos que se ejecutan durante ese grupo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="71a0f-142">Si crea un grupo, se le facturará según las horas de proceso de cada máquina virtual en el grupo hasta que se elimina el grupo, incluso si no hay trabajos por lotes ejecutándose en el grupo.</span><span class="sxs-lookup"><span data-stu-id="71a0f-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="71a0f-143">La facturación para las máquinas virtuales se inicia cuando han terminado de aprovisionarse y se detiene cuando se han eliminado.</span><span class="sxs-lookup"><span data-stu-id="71a0f-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="71a0f-144">Puede usar cualquiera de los planes que se encuentra en la [página Machine Learning Precios](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="71a0f-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="71a0f-145">Ejemplo de facturación:</span><span class="sxs-lookup"><span data-stu-id="71a0f-145">Billing example:</span></span>

<span data-ttu-id="71a0f-146">Si crea un grupo de lote con 2 máquinas virtuales y lo elimina después de 24 horas, el plan de facturación se realiza con un cargo de 48 horas de proceso; independientemente de cuántos trabajos se hayan ejecutado durante ese período.</span><span class="sxs-lookup"><span data-stu-id="71a0f-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="71a0f-147">Si crea un grupo de lote con 4 máquinas virtuales y lo elimina después de 12 horas, el plan de facturación también se realiza con un cargo de 48 horas de proceso.</span><span class="sxs-lookup"><span data-stu-id="71a0f-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="71a0f-148">Se recomienda sondear el estado del trabajo para determinar cuándo se completan los trabajos.</span><span class="sxs-lookup"><span data-stu-id="71a0f-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="71a0f-149">Cuando se hayan acabado de ejecutar todos los trabajos, llame a la operación Resize Pool (Cambiar el tamaño del grupo) para establecer el número de máquinas virtuales en el grupo a cero.</span><span class="sxs-lookup"><span data-stu-id="71a0f-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="71a0f-150">Si no le llegan los recursos del grupo y necesita crear un nuevo grupo, por ejemplo, para facturar en un plan de facturación diferente, puede eliminar el grupo cuando haya terminado de ejecutar todos los trabajos.</span><span class="sxs-lookup"><span data-stu-id="71a0f-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="71a0f-151">**Use procesamiento de grupo de lote cuando**</span><span class="sxs-lookup"><span data-stu-id="71a0f-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="71a0f-152">**Use procesamiento por lotes clásico cuando**</span><span class="sxs-lookup"><span data-stu-id="71a0f-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="71a0f-153">Tiene que ejecutar un gran número de trabajos</span><span class="sxs-lookup"><span data-stu-id="71a0f-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="71a0f-154">O</span><span class="sxs-lookup"><span data-stu-id="71a0f-154">Or</span></span><br/><span data-ttu-id="71a0f-155">Tiene que asegurarse de que los trabajos se ejecutarán inmediatamente</span><span class="sxs-lookup"><span data-stu-id="71a0f-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="71a0f-156">O</span><span class="sxs-lookup"><span data-stu-id="71a0f-156">Or</span></span><br/><span data-ttu-id="71a0f-157">Necesita rendimiento garantizado.</span><span class="sxs-lookup"><span data-stu-id="71a0f-157">You need guaranteed throughput.</span></span> <span data-ttu-id="71a0f-158">Por ejemplo, tiene que ejecutar una serie de trabajos en un determinado período de tiempo y desea escalar horizontalmente los recursos de proceso para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="71a0f-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="71a0f-159">Tiene unos pocos trabajos para ejecutar</span><span class="sxs-lookup"><span data-stu-id="71a0f-159">You are running just a few jobs</span></span><br/><span data-ttu-id="71a0f-160">y</span><span class="sxs-lookup"><span data-stu-id="71a0f-160">And</span></span><br/> <span data-ttu-id="71a0f-161">No necesita que los trabajos se ejecuten inmediatamente</span><span class="sxs-lookup"><span data-stu-id="71a0f-161">You don’t need the jobs to run immediately</span></span> |
