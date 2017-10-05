---
title: Azure Data Factory - Referencia de scripting JSON | Microsoft Docs
description: Proporciona esquemas JSON para entidades de Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="1a29d-103">Azure Data Factory - Referencia de scripting JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="1a29d-104">Este artículo proporciona ejemplos y esquemas JSON para definir entidades de Azure Data Factory (canalización, actividad, conjunto de datos y servicio vinculado).</span><span class="sxs-lookup"><span data-stu-id="1a29d-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="1a29d-105">Canalización</span><span class="sxs-lookup"><span data-stu-id="1a29d-105">Pipeline</span></span> 
<span data-ttu-id="1a29d-106">La estructura de alto nivel de una definición de canalización es como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a29d-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="1a29d-107">En la tabla siguiente se describen las propiedades dentro de las definiciones JSON de canalización:</span><span class="sxs-lookup"><span data-stu-id="1a29d-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="1a29d-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-108">Property</span></span> | <span data-ttu-id="1a29d-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-109">Description</span></span> | <span data-ttu-id="1a29d-110">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="1a29d-111">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-111">name</span></span> | <span data-ttu-id="1a29d-112">Nombre de la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-112">Name of the pipeline.</span></span> <span data-ttu-id="1a29d-113">Especifique un nombre que represente la acción que la actividad o la canalización está configurada para realizar</span><span class="sxs-lookup"><span data-stu-id="1a29d-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="1a29d-114">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="1a29d-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="1a29d-115">Debe empezar en una letra, un número o un carácter de subrayado (_)</span><span class="sxs-lookup"><span data-stu-id="1a29d-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="1a29d-116">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="1a29d-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="1a29d-117">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-117">Yes</span></span> |
| <span data-ttu-id="1a29d-118">Description</span><span class="sxs-lookup"><span data-stu-id="1a29d-118">description</span></span> |<span data-ttu-id="1a29d-119">Texto que describe para qué se usa la actividad o la canalización</span><span class="sxs-lookup"><span data-stu-id="1a29d-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="1a29d-120">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-120">No</span></span> |
| <span data-ttu-id="1a29d-121">actividades</span><span class="sxs-lookup"><span data-stu-id="1a29d-121">activities</span></span> | <span data-ttu-id="1a29d-122">Contiene una lista de actividades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-122">Contains a list of activities.</span></span> | <span data-ttu-id="1a29d-123">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-123">Yes</span></span> |
| <span data-ttu-id="1a29d-124">start</span><span class="sxs-lookup"><span data-stu-id="1a29d-124">start</span></span> |<span data-ttu-id="1a29d-125">Fecha y hora de inicio para la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="1a29d-126">Debe estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="1a29d-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="1a29d-127">Por ejemplo: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="1a29d-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="1a29d-128">Se puede especificar una hora local, por ejemplo, una hora EST.</span><span class="sxs-lookup"><span data-stu-id="1a29d-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="1a29d-129">Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.</span><span class="sxs-lookup"><span data-stu-id="1a29d-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="1a29d-130">Las propiedades start y end juntas especifican un período activo para la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="1a29d-131">Los segmentos de salida solo se producen en este período activo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="1a29d-132">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-132">No</span></span><br/><br/><span data-ttu-id="1a29d-133">Si se especifica un valor para la propiedad end, hay que especificar un valor para la propiedad start.</span><span class="sxs-lookup"><span data-stu-id="1a29d-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="1a29d-134">Las horas de inicio y finalización pueden estar vacías para crear una canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="1a29d-135">Debe especificar ambos valores para establecer un período activo para que se ejecute la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="1a29d-136">Si no especifica horas de inicio y finalización al crear una canalización, puede establecerlas más adelante mediante el cmdlet Set-AzureDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="1a29d-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="1a29d-137">end</span><span class="sxs-lookup"><span data-stu-id="1a29d-137">end</span></span> |<span data-ttu-id="1a29d-138">Fecha y hora de finalización para la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-138">End date-time for the pipeline.</span></span> <span data-ttu-id="1a29d-139">Si se especifica, debe estar en formato ISO.</span><span class="sxs-lookup"><span data-stu-id="1a29d-139">If specified must be in ISO format.</span></span> <span data-ttu-id="1a29d-140">Por ejemplo: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="1a29d-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="1a29d-141">Se puede especificar una hora local, por ejemplo, una hora EST.</span><span class="sxs-lookup"><span data-stu-id="1a29d-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="1a29d-142">Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.</span><span class="sxs-lookup"><span data-stu-id="1a29d-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="1a29d-143">Para ejecutar la canalización indefinidamente, especifique 9999-09-09 como valor de la propiedad end.</span><span class="sxs-lookup"><span data-stu-id="1a29d-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="1a29d-144">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-144">No</span></span> <br/><br/><span data-ttu-id="1a29d-145">Si se especifica un valor para la propiedad start, hay que especificar un valor para la propiedad end.</span><span class="sxs-lookup"><span data-stu-id="1a29d-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="1a29d-146">Consulte las notas para la propiedad **start** .</span><span class="sxs-lookup"><span data-stu-id="1a29d-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="1a29d-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="1a29d-147">isPaused</span></span> |<span data-ttu-id="1a29d-148">Si se establece en true, la canalización no se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="1a29d-149">Valor predeterminado = false.</span><span class="sxs-lookup"><span data-stu-id="1a29d-149">Default value = false.</span></span> <span data-ttu-id="1a29d-150">Puede utilizar esta propiedad para habilitar o deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="1a29d-151">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-151">No</span></span> |
| <span data-ttu-id="1a29d-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="1a29d-152">pipelineMode</span></span> |<span data-ttu-id="1a29d-153">El método para la programación de ejecuciones para la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="1a29d-154">Los valores permitidos son: scheduled (predeterminado).</span><span class="sxs-lookup"><span data-stu-id="1a29d-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="1a29d-155">‘Scheduled’ indica que la canalización se ejecutará en el intervalo de tiempo especificado de acuerdo con su período activo (hora de inicio y finalización).</span><span class="sxs-lookup"><span data-stu-id="1a29d-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="1a29d-156">'Onetime' indica que la canalización se ejecutará solo una vez.</span><span class="sxs-lookup"><span data-stu-id="1a29d-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="1a29d-157">Las canalizaciones creadas una sola vez no se pueden modificar ni actualizar actualmente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="1a29d-158">Consulte la sección [Canalización de una vez](data-factory-create-pipelines.md#onetime-pipeline) para más información acerca de la configuración onetime.</span><span class="sxs-lookup"><span data-stu-id="1a29d-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="1a29d-159">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-159">No</span></span> |
| <span data-ttu-id="1a29d-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="1a29d-160">expirationTime</span></span> |<span data-ttu-id="1a29d-161">Tiempo de duración después de la creación durante el que la canalización es válida y debe permanecer aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="1a29d-162">La canalización se elimina automáticamente una vez que alcanza la hora de caducidad si no tiene ninguna ejecución activa, con error o pendiente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="1a29d-163">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="1a29d-164">Actividad</span><span class="sxs-lookup"><span data-stu-id="1a29d-164">Activity</span></span> 
<span data-ttu-id="1a29d-165">La estructura de alto nivel de una actividad dentro de una definición de canalización (elemento de actividades) es como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a29d-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="1a29d-166">En la tabla siguiente se describen las propiedades dentro de la definición JSON de actividad:</span><span class="sxs-lookup"><span data-stu-id="1a29d-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="1a29d-167">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="1a29d-167">Tag</span></span> | <span data-ttu-id="1a29d-168">Description</span><span class="sxs-lookup"><span data-stu-id="1a29d-168">Description</span></span> | <span data-ttu-id="1a29d-169">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-170">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-170">name</span></span> |<span data-ttu-id="1a29d-171">Nombre de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-171">Name of the activity.</span></span> <span data-ttu-id="1a29d-172">Especifique un nombre que represente la acción que la actividad está configurada para realizar</span><span class="sxs-lookup"><span data-stu-id="1a29d-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="1a29d-173">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="1a29d-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="1a29d-174">Debe empezar en una letra, un número o un carácter de subrayado (_)</span><span class="sxs-lookup"><span data-stu-id="1a29d-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="1a29d-175">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="1a29d-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="1a29d-176">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-176">Yes</span></span> |
| <span data-ttu-id="1a29d-177">Description</span><span class="sxs-lookup"><span data-stu-id="1a29d-177">description</span></span> |<span data-ttu-id="1a29d-178">Texto que describe para qué se usa la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="1a29d-179">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-179">Yes</span></span> |
| <span data-ttu-id="1a29d-180">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-180">type</span></span> |<span data-ttu-id="1a29d-181">Especifica el tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-181">Specifies the type of the activity.</span></span> <span data-ttu-id="1a29d-182">Vea las secciones sobre [ALMACENES DE DATOS](#data-stores) y [ACTIVIDADES DE TRANSFORMACIÓN DE DATOS](#data-transformation-activities) para ver los distintos tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="1a29d-183">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-183">Yes</span></span> |
| <span data-ttu-id="1a29d-184">inputs</span><span class="sxs-lookup"><span data-stu-id="1a29d-184">inputs</span></span> |<span data-ttu-id="1a29d-185">Tablas de entrada utilizadas por la actividad </span><span class="sxs-lookup"><span data-stu-id="1a29d-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="1a29d-186">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-186">Yes</span></span> |
| <span data-ttu-id="1a29d-187">outputs</span><span class="sxs-lookup"><span data-stu-id="1a29d-187">outputs</span></span> |<span data-ttu-id="1a29d-188">Tablas de salida utilizadas por la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="1a29d-189">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-189">Yes</span></span> |
| <span data-ttu-id="1a29d-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1a29d-190">linkedServiceName</span></span> |<span data-ttu-id="1a29d-191">Nombre del servicio vinculado utilizado por la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="1a29d-192">Una actividad puede requerir que especifique el servicio vinculado que enlaza con el entorno de procesos necesario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="1a29d-193">Sí para las actividades de HDInsight, las actividades de Azure Machine Learning y las actividades del procedimiento almacenadas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="1a29d-194">No para todos los demás</span><span class="sxs-lookup"><span data-stu-id="1a29d-194">No for all others</span></span> |
| <span data-ttu-id="1a29d-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a29d-195">typeProperties</span></span> |<span data-ttu-id="1a29d-196">Propiedades en la sección typeProperties dependen del tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="1a29d-197">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-197">No</span></span> |
| <span data-ttu-id="1a29d-198">policy</span><span class="sxs-lookup"><span data-stu-id="1a29d-198">policy</span></span> |<span data-ttu-id="1a29d-199">Directivas que afectan al comportamiento en tiempo de ejecución de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="1a29d-200">Si no se especifica, se usan las directivas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="1a29d-201">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-201">No</span></span> |
| <span data-ttu-id="1a29d-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="1a29d-202">scheduler</span></span> |<span data-ttu-id="1a29d-203">La propiedad "scheduler" se utiliza para definir la programación deseada para la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="1a29d-204">Sus subpropiedades son las mismas que las de la [propiedad availability de un conjunto de datos](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="1a29d-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="1a29d-205">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="1a29d-206">Directivas</span><span class="sxs-lookup"><span data-stu-id="1a29d-206">Policies</span></span>
<span data-ttu-id="1a29d-207">Las directivas afectan al comportamiento en tiempo de ejecución de una actividad, concretamente cuando se procesa el segmento de una tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="1a29d-208">En la tabla siguiente se proporciona los detalles.</span><span class="sxs-lookup"><span data-stu-id="1a29d-208">The following table provides the details.</span></span>

| <span data-ttu-id="1a29d-209">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-209">Property</span></span> | <span data-ttu-id="1a29d-210">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-210">Permitted values</span></span> | <span data-ttu-id="1a29d-211">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-211">Default Value</span></span> | <span data-ttu-id="1a29d-212">Description</span><span class="sxs-lookup"><span data-stu-id="1a29d-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-213">simultaneidad</span><span class="sxs-lookup"><span data-stu-id="1a29d-213">concurrency</span></span> |<span data-ttu-id="1a29d-214">Entero </span><span class="sxs-lookup"><span data-stu-id="1a29d-214">Integer</span></span> <br/><br/><span data-ttu-id="1a29d-215">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="1a29d-215">Max value: 10</span></span> |<span data-ttu-id="1a29d-216">1</span><span class="sxs-lookup"><span data-stu-id="1a29d-216">1</span></span> |<span data-ttu-id="1a29d-217">Número de ejecuciones simultáneas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="1a29d-218">Determina el número de ejecuciones paralelas de la actividad que pueden tener lugar en distintos segmentos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="1a29d-219">Por ejemplo, si una actividad tiene que recorrer un gran conjunto de datos disponibles, tener un valor mayor de simultaneidad acelera el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="1a29d-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="1a29d-220">executionPriorityOrder</span></span> |<span data-ttu-id="1a29d-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="1a29d-221">NewestFirst</span></span><br/><br/><span data-ttu-id="1a29d-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="1a29d-222">OldestFirst</span></span> |<span data-ttu-id="1a29d-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="1a29d-223">OldestFirst</span></span> |<span data-ttu-id="1a29d-224">Determina el orden de los segmentos de datos que se están procesando.</span><span class="sxs-lookup"><span data-stu-id="1a29d-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="1a29d-225">Por ejemplo, si tiene 2 segmentos (que tienen lugar uno a las 4 p.m. y el otro a las 5 p.m.) y ambos están pendientes de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1a29d-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="1a29d-226">Si establece que executionPriorityOrder sea NewestFirst, se procesará primero el segmento de las 5 p.m.</span><span class="sxs-lookup"><span data-stu-id="1a29d-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="1a29d-227">De forma similar, si establece que executionPriorityORder sea OldestFIrst, se procesará el segmento de las 4 p.m.</span><span class="sxs-lookup"><span data-stu-id="1a29d-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="1a29d-228">retry</span><span class="sxs-lookup"><span data-stu-id="1a29d-228">retry</span></span> |<span data-ttu-id="1a29d-229">Entero </span><span class="sxs-lookup"><span data-stu-id="1a29d-229">Integer</span></span><br/><br/><span data-ttu-id="1a29d-230">El valor máximo permitido es 10</span><span class="sxs-lookup"><span data-stu-id="1a29d-230">Max value can be 10</span></span> |<span data-ttu-id="1a29d-231">0</span><span class="sxs-lookup"><span data-stu-id="1a29d-231">0</span></span> |<span data-ttu-id="1a29d-232">Número de reintentos antes de que el procesamiento de datos del segmento se marque como error.</span><span class="sxs-lookup"><span data-stu-id="1a29d-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="1a29d-233">La ejecución de la actividad de un segmento de datos se vuelve a intentar hasta el número de reintentos especificado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="1a29d-234">El reintento se realiza tan pronto como sea posible después del error.</span><span class="sxs-lookup"><span data-stu-id="1a29d-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="1a29d-235">timeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-235">timeout</span></span> |<span data-ttu-id="1a29d-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1a29d-236">TimeSpan</span></span> |<span data-ttu-id="1a29d-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1a29d-237">00:00:00</span></span> |<span data-ttu-id="1a29d-238">Tiempo de espera para la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-238">Timeout for the activity.</span></span> <span data-ttu-id="1a29d-239">Ejemplo: 00:10:00 (implica un tiempo de espera de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="1a29d-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="1a29d-240">Si un valor no se especifica o es 0, el tiempo de espera es infinito.</span><span class="sxs-lookup"><span data-stu-id="1a29d-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="1a29d-241">Si el tiempo de procesamiento de los datos en un segmento supera el valor de tiempo de espera, se cancela y el sistema vuelve a intentar el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="1a29d-242">El número de reintentos depende de la propiedad retry.</span><span class="sxs-lookup"><span data-stu-id="1a29d-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="1a29d-243">Si se excede el tiempo de espera, el estado será TimedOut.</span><span class="sxs-lookup"><span data-stu-id="1a29d-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="1a29d-244">delay</span><span class="sxs-lookup"><span data-stu-id="1a29d-244">delay</span></span> |<span data-ttu-id="1a29d-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1a29d-245">TimeSpan</span></span> |<span data-ttu-id="1a29d-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1a29d-246">00:00:00</span></span> |<span data-ttu-id="1a29d-247">Especifica el retraso antes de iniciar el procesamiento de los datos del segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="1a29d-248">La ejecución de la actividad de un segmento de datos se inicia una vez que transcurra el retraso más allá del tiempo de ejecución esperado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="1a29d-249">Ejemplo: 00:10:00 (implica un retraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="1a29d-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="1a29d-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="1a29d-250">longRetry</span></span> |<span data-ttu-id="1a29d-251">Entero </span><span class="sxs-lookup"><span data-stu-id="1a29d-251">Integer</span></span><br/><br/><span data-ttu-id="1a29d-252">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="1a29d-252">Max value: 10</span></span> |<span data-ttu-id="1a29d-253">1</span><span class="sxs-lookup"><span data-stu-id="1a29d-253">1</span></span> |<span data-ttu-id="1a29d-254">Número de reintentos largos antes de que la ejecución de los segmentos produzca error.</span><span class="sxs-lookup"><span data-stu-id="1a29d-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="1a29d-255">Los intentos de longRetry se espacian de acuerdo a longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="1a29d-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="1a29d-256">Por tanto, si necesita especificar un tiempo entre reintentos, utilice longRetry.</span><span class="sxs-lookup"><span data-stu-id="1a29d-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="1a29d-257">Si se especifican Retry y longRetry, cada intento de longRetry incluirá el número de intentos de Retry y el número máximo de intentos será Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="1a29d-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="1a29d-258">Por ejemplo, si tenemos la siguiente configuración en la directiva de la actividad:</span><span class="sxs-lookup"><span data-stu-id="1a29d-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="1a29d-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="1a29d-259">Retry: 3</span></span><br/><span data-ttu-id="1a29d-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="1a29d-260">longRetry: 2</span></span><br/><span data-ttu-id="1a29d-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="1a29d-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="1a29d-262">Se supone que existe un solo segmento para ejecutar (el estado es En espera) y la ejecución de la actividad no se puede realizar nunca.</span><span class="sxs-lookup"><span data-stu-id="1a29d-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="1a29d-263">Inicialmente habría tres intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1a29d-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="1a29d-264">Después de cada intento, el estado del segmento sería Retry.</span><span class="sxs-lookup"><span data-stu-id="1a29d-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="1a29d-265">Después de los 3 primeros intentos, el estado del segmento sería LongRetry.</span><span class="sxs-lookup"><span data-stu-id="1a29d-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="1a29d-266">Después de una hora (es decir, el valor de longRetryInteval), se produciría otro conjunto de 3 intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1a29d-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="1a29d-267">Después de eso, el estado del segmento sería Failed y ya no se realizarían más intentos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="1a29d-268">Por tanto, en total se realizaron 6 intentos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="1a29d-269">Si una ejecución se realiza correctamente, el estado del segmento sería Ready y no se realizaría ningún otro reintento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="1a29d-270">longRetry puede usarse en situaciones donde llegan datos dependientes a horas no deterministas o el entorno general en el que se produce el procesamiento de datos es poco confiable.</span><span class="sxs-lookup"><span data-stu-id="1a29d-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="1a29d-271">En esos casos es posible que realizar reintentos uno tras otro no ayude, mientras que hacerlo después de un intervalo de tiempo puede generar el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="1a29d-272">Advertencia: No establezca valores altos para longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="1a29d-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="1a29d-273">Normalmente, los valores más altos implican otros problemas sistémicos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="1a29d-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="1a29d-274">longRetryInterval</span></span> |<span data-ttu-id="1a29d-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1a29d-275">TimeSpan</span></span> |<span data-ttu-id="1a29d-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1a29d-276">00:00:00</span></span> |<span data-ttu-id="1a29d-277">El retraso entre reintentos largos</span><span class="sxs-lookup"><span data-stu-id="1a29d-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="1a29d-278">Sección typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a29d-278">typeProperties section</span></span>
<span data-ttu-id="1a29d-279">La sección typeProperties es diferente para cada actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="1a29d-280">Las actividades de transformación tienen las propiedades del tipo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="1a29d-281">Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="1a29d-282">La **actividad de copia** tiene dos subsecciones en la sección typeProperties: **origen** y **receptor**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="1a29d-283">Vea la sección [Almacenes de datos](#data-stores) en este artículo para consultar ejemplos JSON que muestran cómo utilizar datos de un almacén como un origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="1a29d-284">Canalización de copia de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-284">Sample copy pipeline</span></span>
<span data-ttu-id="1a29d-285">En la canalización de ejemplo siguiente, hay una actividad del tipo **Copy** in the **actividades** .</span><span class="sxs-lookup"><span data-stu-id="1a29d-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="1a29d-286">En este ejemplo, [Copiar actividad](data-factory-data-movement-activities.md) copia datos desde un Azure Blob Storage en una Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a29d-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="1a29d-287">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="1a29d-287">Note the following points:</span></span>

* <span data-ttu-id="1a29d-288">En la sección de actividades, solo hay una actividad con **type** establecido en **Copy**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="1a29d-289">La entrada de la actividad está establecida en **InputDataset**, mientras que la salida está establecida en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="1a29d-290">En la sección **typeProperties**, **BlobSource** se especifica como el tipo de origen y **SqlSink** como el tipo de receptor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="1a29d-291">Vea la sección [Almacenes de datos](#data-stores) en este artículo para consultar ejemplos JSON que muestran cómo utilizar datos de un almacén como un origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="1a29d-292">Para obtener un tutorial completo de creación de esta canalización, vea [Tutorial: Copiar datos desde Blob Storage a SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="1a29d-293">Canalización de transformación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-293">Sample transformation pipeline</span></span>
<span data-ttu-id="1a29d-294">En la canalización de ejemplo siguiente, hay una actividad del tipo **HDInsightHive** in the **actividades** .</span><span class="sxs-lookup"><span data-stu-id="1a29d-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="1a29d-295">En este ejemplo, el [actividad de HDInsight Hive](data-factory-hive-activity.md) transforma los datos de Azure Blob Storage mediante la ejecución de un archivo de script de Hive en un clúster de Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a29d-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="1a29d-296">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="1a29d-296">Note the following points:</span></span> 

* <span data-ttu-id="1a29d-297">En la sección de actividades, solo hay una actividad con **type** establecido en **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="1a29d-298">El archivo de script de Hive, **partitionweblogs.hql**, se almacena en la cuenta de Azure Storage (especificada por la propiedad scriptLinkedService, llamada **AzureStorageLinkedService**) en una carpeta denominada **script** del contenedor **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="1a29d-299">La sección **defines** se usa para especificar la configuración de tiempo de ejecución que se pasa al script de Hive como valores de configuración de Hive (por ejemplo, `${hiveconf:inputtable}` y `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="1a29d-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="1a29d-300">Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="1a29d-301">Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: Compilar su primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="1a29d-302">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-302">Linked service</span></span>
<span data-ttu-id="1a29d-303">La estructura de alto nivel de una definición de servicio vinculado es como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a29d-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="1a29d-304">En la tabla siguiente se describen las propiedades dentro de la definición JSON de actividad:</span><span class="sxs-lookup"><span data-stu-id="1a29d-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="1a29d-305">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-305">Property</span></span> | <span data-ttu-id="1a29d-306">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-306">Description</span></span> | <span data-ttu-id="1a29d-307">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="1a29d-308">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-308">name</span></span> | <span data-ttu-id="1a29d-309">Nombre del servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-309">Name of the linked service.</span></span> | <span data-ttu-id="1a29d-310">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-310">Yes</span></span> | 
| <span data-ttu-id="1a29d-311">propiedades - tipo</span><span class="sxs-lookup"><span data-stu-id="1a29d-311">properties - type</span></span> | <span data-ttu-id="1a29d-312">Tipo de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-312">Type of the linked service.</span></span> <span data-ttu-id="1a29d-313">Por ejemplo: Azure Storage o Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a29d-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="1a29d-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a29d-314">typeProperties</span></span> | <span data-ttu-id="1a29d-315">La sección typeProperties tiene elementos que son diferentes para cada almacén de datos o entorno de proceso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="1a29d-316">Vea la sección [Almacenes de datos](#datastores) para todos los servicios vinculados de almacén de datos y [Entornos de proceso](#compute-environments) para todos los servicios vinculados de proceso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="1a29d-317">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-317">Dataset</span></span> 
<span data-ttu-id="1a29d-318">Un conjunto de datos en Data Factory de Azure se define como sigue:</span><span class="sxs-lookup"><span data-stu-id="1a29d-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="1a29d-319">La tabla siguiente describe las propiedades del JSON anterior:</span><span class="sxs-lookup"><span data-stu-id="1a29d-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="1a29d-320">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-320">Property</span></span> | <span data-ttu-id="1a29d-321">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-321">Description</span></span> | <span data-ttu-id="1a29d-322">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-322">Required</span></span> | <span data-ttu-id="1a29d-323">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-324">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-324">name</span></span> | <span data-ttu-id="1a29d-325">Nombre del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-325">Name of the dataset.</span></span> <span data-ttu-id="1a29d-326">Consulte [Azure Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para ver este tipo de reglas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="1a29d-327">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-327">Yes</span></span> |<span data-ttu-id="1a29d-328">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-328">NA</span></span> |
| <span data-ttu-id="1a29d-329">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-329">type</span></span> | <span data-ttu-id="1a29d-330">Tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-330">Type of the dataset.</span></span> <span data-ttu-id="1a29d-331">Especifique uno de los tipos admitidos por Data Factory de Azure (por ejemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="1a29d-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="1a29d-332">Vea la sección [ALMACENES DE DATOS](#data-stores) para todos los almacenes de datos y tipos de conjuntos de datos admitidos en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="1a29d-333">structure</span><span class="sxs-lookup"><span data-stu-id="1a29d-333">structure</span></span> | <span data-ttu-id="1a29d-334">Esquema del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-334">Schema of the dataset.</span></span> <span data-ttu-id="1a29d-335">Contiene las columnas, sus tipos, etc.</span><span class="sxs-lookup"><span data-stu-id="1a29d-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="1a29d-336">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-336">No</span></span> |<span data-ttu-id="1a29d-337">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-337">NA</span></span> |
| <span data-ttu-id="1a29d-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a29d-338">typeProperties</span></span> | <span data-ttu-id="1a29d-339">Propiedades correspondientes al tipo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="1a29d-340">Vea la sección [ALMACENES DE DATOS](#data-stores) para consultar los tipos admitidos y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="1a29d-341">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-341">Yes</span></span> |<span data-ttu-id="1a29d-342">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-342">NA</span></span> |
| <span data-ttu-id="1a29d-343">external</span><span class="sxs-lookup"><span data-stu-id="1a29d-343">external</span></span> | <span data-ttu-id="1a29d-344">Marca booleana para especificar si un conjunto de datos es generado explícitamente por una canalización de la factoría de datos o no.</span><span class="sxs-lookup"><span data-stu-id="1a29d-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="1a29d-345">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-345">No</span></span> |<span data-ttu-id="1a29d-346">false</span><span class="sxs-lookup"><span data-stu-id="1a29d-346">false</span></span> |
| <span data-ttu-id="1a29d-347">availability</span><span class="sxs-lookup"><span data-stu-id="1a29d-347">availability</span></span> | <span data-ttu-id="1a29d-348">Define la ventana de procesamiento o el modelo de segmentación para la producción del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="1a29d-349">Consulte el artículo [Programación y ejecución](data-factory-scheduling-and-execution.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="1a29d-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="1a29d-350">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-350">Yes</span></span> |<span data-ttu-id="1a29d-351">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-351">NA</span></span> |
| <span data-ttu-id="1a29d-352">policy</span><span class="sxs-lookup"><span data-stu-id="1a29d-352">policy</span></span> |<span data-ttu-id="1a29d-353">Define los criterios o la condición que deben cumplir los segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="1a29d-354">Para más información, consulte la sección [Directiva del conjunto de datos](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="1a29d-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="1a29d-355">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-355">No</span></span> |<span data-ttu-id="1a29d-356">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-356">NA</span></span> |

<span data-ttu-id="1a29d-357">Cada columna de la sección **Estructura** contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="1a29d-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="1a29d-358">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-358">Property</span></span> | <span data-ttu-id="1a29d-359">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-359">Description</span></span> | <span data-ttu-id="1a29d-360">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-361">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-361">name</span></span> |<span data-ttu-id="1a29d-362">Nombre de la columna.</span><span class="sxs-lookup"><span data-stu-id="1a29d-362">Name of the column.</span></span> |<span data-ttu-id="1a29d-363">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-363">Yes</span></span> |
| <span data-ttu-id="1a29d-364">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-364">type</span></span> |<span data-ttu-id="1a29d-365">Tipo de datos de la columna.</span><span class="sxs-lookup"><span data-stu-id="1a29d-365">Data type of the column.</span></span>  |<span data-ttu-id="1a29d-366">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-366">No</span></span> |
| <span data-ttu-id="1a29d-367">culture</span><span class="sxs-lookup"><span data-stu-id="1a29d-367">culture</span></span> |<span data-ttu-id="1a29d-368">Referencia cultural basada en .NET que se usará cuando se especifica el tipo y sea un tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="1a29d-369">El valor predeterminado es `en-us`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-369">Default is `en-us`.</span></span> |<span data-ttu-id="1a29d-370">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-370">No</span></span> |
| <span data-ttu-id="1a29d-371">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-371">format</span></span> |<span data-ttu-id="1a29d-372">Cadena de formato que se usará cuando se especifica el tipo y sea un tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="1a29d-373">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-373">No</span></span> |

<span data-ttu-id="1a29d-374">En el ejemplo siguiente, el conjunto de datos tiene tres columnas (`slicetimestamp`, `projectname` y `pageviews`) cuyos tipos son String, String y Decimal respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="1a29d-375">La tabla siguiente describe las propiedades que puede utilizar en la sección de **disponibilidad**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="1a29d-376">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-376">Property</span></span> | <span data-ttu-id="1a29d-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-377">Description</span></span> | <span data-ttu-id="1a29d-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-378">Required</span></span> | <span data-ttu-id="1a29d-379">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-380">frequency</span><span class="sxs-lookup"><span data-stu-id="1a29d-380">frequency</span></span> |<span data-ttu-id="1a29d-381">Especifica la unidad de tiempo para la producción de segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="1a29d-382"><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="1a29d-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="1a29d-383">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-383">Yes</span></span> |<span data-ttu-id="1a29d-384">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-384">NA</span></span> |
| <span data-ttu-id="1a29d-385">interval</span><span class="sxs-lookup"><span data-stu-id="1a29d-385">interval</span></span> |<span data-ttu-id="1a29d-386">Especifica un multiplicador para frecuencia</span><span class="sxs-lookup"><span data-stu-id="1a29d-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="1a29d-387">”Frequency x interval” determina la frecuencia con la que se produce el segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="1a29d-388">Si necesita segmentar el conjunto de datos cada hora, establezca <b>frequency</b> en <b>hour</b> e <b>interval</b> en <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="1a29d-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="1a29d-389"><b>Nota:</b> Si especifica Frequency como Minute, se recomienda establecer interval en no menos de 15.</span><span class="sxs-lookup"><span data-stu-id="1a29d-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="1a29d-390">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-390">Yes</span></span> |<span data-ttu-id="1a29d-391">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-391">NA</span></span> |
| <span data-ttu-id="1a29d-392">style</span><span class="sxs-lookup"><span data-stu-id="1a29d-392">style</span></span> |<span data-ttu-id="1a29d-393">Especifica si el segmento debe producirse al principio o al final del intervalo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="1a29d-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="1a29d-394">StartOfInterval</span></span></li><li><span data-ttu-id="1a29d-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="1a29d-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="1a29d-396">Si frequency se establece en Month y style se establece en EndOfInterval, el segmento se produce el último día del mes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="1a29d-397">Si style se establece en StartOfInterval, el segmento se produce el primer día del mes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="1a29d-398">Si frequency se establece en Day y style se establece en EndOfInterval, el segmento se produce la última hora del día.</span><span class="sxs-lookup"><span data-stu-id="1a29d-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="1a29d-399">Si frequency se establece en Hour y style se establece en EndOfInterval, el segmento se produce al final de la hora.</span><span class="sxs-lookup"><span data-stu-id="1a29d-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="1a29d-400">Por ejemplo, para un segmento para el período de 1 p.m. – 2 p.m., el segmento se producirá a las 2 p.m.</span><span class="sxs-lookup"><span data-stu-id="1a29d-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="1a29d-401">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-401">No</span></span> |<span data-ttu-id="1a29d-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="1a29d-402">EndOfInterval</span></span> |
| <span data-ttu-id="1a29d-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="1a29d-403">anchorDateTime</span></span> |<span data-ttu-id="1a29d-404">Define la posición absoluta en el tiempo usada por el programador para calcular los límites del segmento de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="1a29d-405"><b>Nota:</b> Si AnchorDateTime tiene partes de fecha más pormenorizadas que la frecuencia, estas se omitirán.</span><span class="sxs-lookup"><span data-stu-id="1a29d-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="1a29d-406">Por ejemplo, si el valor de <b>interval</b> es <b>hourly</b> (frequency: hour e interval: 1) y <b>AnchorDateTime</b> contiene <b>minutes and seconds</b>, las partes <b>minutes and seconds</b> de AnchorDateTime no se tienen en cuenta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="1a29d-407">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-407">No</span></span> |<span data-ttu-id="1a29d-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="1a29d-408">01/01/0001</span></span> |
| <span data-ttu-id="1a29d-409">Offset</span><span class="sxs-lookup"><span data-stu-id="1a29d-409">offset</span></span> |<span data-ttu-id="1a29d-410">Intervalo de tiempo en función del cual se desplazan el inicio y el final de todos los segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="1a29d-411"><b>Nota:</b> Si se especifican anchorDateTime y offset, el resultado es el desplazamiento combinado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="1a29d-412">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-412">No</span></span> |<span data-ttu-id="1a29d-413">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-413">NA</span></span> |

<span data-ttu-id="1a29d-414">La sección de disponibilidad siguiente especifica que el conjunto de datos de salida se produce cada hora (o) que el conjunto de datos de entrada está disponible cada hora:</span><span class="sxs-lookup"><span data-stu-id="1a29d-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="1a29d-415">En la sección **policy** de la definición del conjunto de datos se definen los criterios o condiciones que deben cumplir los segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="1a29d-416">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="1a29d-416">Policy Name</span></span> | <span data-ttu-id="1a29d-417">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-417">Description</span></span> | <span data-ttu-id="1a29d-418">Aplicado a</span><span class="sxs-lookup"><span data-stu-id="1a29d-418">Applied To</span></span> | <span data-ttu-id="1a29d-419">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-419">Required</span></span> | <span data-ttu-id="1a29d-420">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1a29d-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="1a29d-421">minimumSizeMB</span></span> |<span data-ttu-id="1a29d-422">Valida que los datos de un **blob de Azure** cumplen los requisitos de tamaño mínimo (en megabytes).</span><span class="sxs-lookup"><span data-stu-id="1a29d-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="1a29d-423">blob de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-423">Azure Blob</span></span> |<span data-ttu-id="1a29d-424">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-424">No</span></span> |<span data-ttu-id="1a29d-425">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-425">NA</span></span> |
| <span data-ttu-id="1a29d-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="1a29d-426">minimumRows</span></span> |<span data-ttu-id="1a29d-427">Valida que los datos de una **base de datos SQL de Azure** o una **tabla de Azure** contienen el número mínimo de filas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="1a29d-428">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-428">Azure SQL Database</span></span></li><li><span data-ttu-id="1a29d-429">tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-429">Azure Table</span></span></li></ul> |<span data-ttu-id="1a29d-430">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-430">No</span></span> |<span data-ttu-id="1a29d-431">N/D</span><span class="sxs-lookup"><span data-stu-id="1a29d-431">NA</span></span> |

<span data-ttu-id="1a29d-432">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1a29d-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="1a29d-433">A menos que se esté produciendo un conjunto de datos mediante Data Factory de Azure, debe marcarse como **external**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="1a29d-434">Generalmente, esta configuración se aplicará a las entradas de la primera actividad de una canalización a menos que se desee usar el encadenamiento de actividades o canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="1a29d-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="1a29d-435">name</span><span class="sxs-lookup"><span data-stu-id="1a29d-435">Name</span></span> | <span data-ttu-id="1a29d-436">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-436">Description</span></span> | <span data-ttu-id="1a29d-437">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-437">Required</span></span> | <span data-ttu-id="1a29d-438">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="1a29d-439">dataDelay</span></span> |<span data-ttu-id="1a29d-440">Tiempo de retraso de la comprobación de la disponibilidad de los datos externos para el segmento especificado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="1a29d-441">Por ejemplo, si los datos están disponibles cada hora, la comprobación de si los datos externos están realmente disponibles y si el segmento correspondiente está preparado puede retrasarse mediante dataDelay.</span><span class="sxs-lookup"><span data-stu-id="1a29d-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="1a29d-442">Solo se aplica a la hora actual.</span><span class="sxs-lookup"><span data-stu-id="1a29d-442">Only applies to the present time.</span></span>  <span data-ttu-id="1a29d-443">Por ejemplo, si es la 1:00 p.m. y este valor es de 10 minutos, la validación se inicia a la 1:10 p.m.</span><span class="sxs-lookup"><span data-stu-id="1a29d-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="1a29d-444">Esta configuración no afecta a los segmentos en el pasado; los segmentos para los que se cumple Slice End Time + dataDelay < Now se procesan sin ningún retraso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="1a29d-445">Las horas posteriores a las 23:59 horas se deben especificar con el formato `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="1a29d-446">Por ejemplo, para especificar 24 horas, no use 24:00:00; en su lugar, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="1a29d-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="1a29d-447">Si usa 24:00:00, se tratará como 24 días (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="1a29d-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="1a29d-448">Para 1 día y 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="1a29d-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="1a29d-449">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-449">No</span></span> |<span data-ttu-id="1a29d-450">0</span><span class="sxs-lookup"><span data-stu-id="1a29d-450">0</span></span> |
| <span data-ttu-id="1a29d-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="1a29d-451">retryInterval</span></span> |<span data-ttu-id="1a29d-452">El tiempo de espera entre un error y el siguiente reintento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="1a29d-453">Si se produce un error en el intento, el siguiente se realizará después del valor especificado en retryInterval.</span><span class="sxs-lookup"><span data-stu-id="1a29d-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="1a29d-454">Si ahora es la 1:00 p. m., empezaremos el primer intento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="1a29d-455">Si la duración para completar la primera comprobación de validación es 1 minuto y la operación produce un error, el siguiente reintento será a la 1:00 + 1 minuto (duración) + 1 minuto (intervalo de reintento) = 1:02 p. m.</span><span class="sxs-lookup"><span data-stu-id="1a29d-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="1a29d-456">En el caso de los segmentos en el pasado, no habrá ningún retraso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="1a29d-457">El reintento se producirá inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-457">The retry happens immediately.</span></span> |<span data-ttu-id="1a29d-458">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-458">No</span></span> |<span data-ttu-id="1a29d-459">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="1a29d-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="1a29d-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-460">retryTimeout</span></span> |<span data-ttu-id="1a29d-461">El tiempo de espera de cada reintento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="1a29d-462">Si esta propiedad se establece en 10 minutos, la validación se debe completar en 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="1a29d-463">Si la validación tarda más de 10 minutos en realizarse, el reintento agotará el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="1a29d-464">Si se agota el tiempo de espera de todos los intentos de validación, el segmento se marcará como TimedOut.</span><span class="sxs-lookup"><span data-stu-id="1a29d-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="1a29d-465">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-465">No</span></span> |<span data-ttu-id="1a29d-466">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="1a29d-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="1a29d-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="1a29d-467">maximumRetry</span></span> |<span data-ttu-id="1a29d-468">Número de veces que se va a comprobar la disponibilidad de los datos externos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="1a29d-469">El valor máximo permitido es 10.</span><span class="sxs-lookup"><span data-stu-id="1a29d-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="1a29d-470">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-470">No</span></span> |<span data-ttu-id="1a29d-471">3</span><span class="sxs-lookup"><span data-stu-id="1a29d-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="1a29d-472">ALMACENES DE DATOS</span><span class="sxs-lookup"><span data-stu-id="1a29d-472">DATA STORES</span></span>
<span data-ttu-id="1a29d-473">En la sección [Servicio vinculado](#linked-service) se proporcionan descripciones de los elementos JSON que son comunes para todos los tipos de servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="1a29d-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="1a29d-474">Esta sección proporciona detalles sobre los elementos JSON que son específicos de cada almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="1a29d-475">En la sección [Conjunto de datos](#dataset) se proporcionan descripciones de los elementos JSON que son comunes para todos los tipos de conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="1a29d-476">Esta sección proporciona detalles sobre los elementos JSON que son específicos de cada almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="1a29d-477">En la sección [Actividad](#activity) se proporcionan descripciones de los elementos JSON que son comunes para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="1a29d-478">En esta sección se proporcionan detalles sobre los elementos JSON que son específicos para cada almacén de datos cuando se utiliza como un origen/receptor en una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="1a29d-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="1a29d-479">Haga clic en el vínculo del almacén del que le interesa ver los esquemas JSON para el servicio vinculado, el conjunto de datos y el origen/receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="1a29d-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="1a29d-480">Categoría</span><span class="sxs-lookup"><span data-stu-id="1a29d-480">Category</span></span> | <span data-ttu-id="1a29d-481">Almacén de datos</span><span class="sxs-lookup"><span data-stu-id="1a29d-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="1a29d-482">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="1a29d-482">**Azure**</span></span> |[<span data-ttu-id="1a29d-483">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="1a29d-484">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="1a29d-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a29d-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="1a29d-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1a29d-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="1a29d-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a29d-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="1a29d-488">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="1a29d-489">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="1a29d-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="1a29d-490">**Bases de datos**</span><span class="sxs-lookup"><span data-stu-id="1a29d-490">**Databases**</span></span> |[<span data-ttu-id="1a29d-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="1a29d-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="1a29d-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="1a29d-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="1a29d-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="1a29d-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="1a29d-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="1a29d-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="1a29d-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a29d-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="1a29d-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a29d-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="1a29d-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a29d-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="1a29d-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="1a29d-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="1a29d-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="1a29d-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="1a29d-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="1a29d-501">**NoSQL**</span></span> |[<span data-ttu-id="1a29d-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="1a29d-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="1a29d-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="1a29d-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="1a29d-504">**Archivo**</span><span class="sxs-lookup"><span data-stu-id="1a29d-504">**File**</span></span> |[<span data-ttu-id="1a29d-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="1a29d-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="1a29d-506">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="1a29d-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="1a29d-507">FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="1a29d-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="1a29d-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="1a29d-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="1a29d-510">**Otros**</span><span class="sxs-lookup"><span data-stu-id="1a29d-510">**Others**</span></span> |[<span data-ttu-id="1a29d-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="1a29d-512">OData</span><span class="sxs-lookup"><span data-stu-id="1a29d-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="1a29d-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="1a29d-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="1a29d-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="1a29d-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="1a29d-515">Tabla web</span><span class="sxs-lookup"><span data-stu-id="1a29d-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="1a29d-516">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-517">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-517">Linked service</span></span>
<span data-ttu-id="1a29d-518">Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="1a29d-519">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="1a29d-520">Para vincular la cuenta de Azure Storage a una instancia de Data Factory mediante una **clave de cuenta**, cree un servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="1a29d-521">Para definir un servicio vinculado de Azure Storage, establezca el **tipo** del servicio vinculado en **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="1a29d-522">Después, puede especificar las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-523">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-523">Property</span></span> | <span data-ttu-id="1a29d-524">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-524">Description</span></span> | <span data-ttu-id="1a29d-525">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-526">connectionString</span></span> |<span data-ttu-id="1a29d-527">Especifique la información necesaria para conectarse a Almacenamiento de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="1a29d-528">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="1a29d-529">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="1a29d-530">Servicio vinculado de SAS de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1a29d-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="1a29d-531">El servicio vinculado de SAS de Almacenamiento de Azure le permite vincular una cuenta de Almacenamiento de Azure a una Factoría de datos de Azure con una Firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="1a29d-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="1a29d-532">Proporciona a la instancia de Data Factory acceso restringido o limitado por el tiempo a todos los recursos o a algunos específicos (blob o contenedor) del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="1a29d-533">Para vincular la cuenta de Azure Storage a una instancia de Data Factory mediante una Firma de acceso compartido, cree un servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="1a29d-534">Para definir un servicio vinculado de SAS de Azure Storage, establezca el **tipo** del servicio vinculado en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="1a29d-535">Después, puede especificar las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="1a29d-536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-536">Property</span></span> | <span data-ttu-id="1a29d-537">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-537">Description</span></span> | <span data-ttu-id="1a29d-538">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="1a29d-539">sasUri</span></span> |<span data-ttu-id="1a29d-540">Especifique el URI de Firma de acceso compartido a los recursos de Almacenamiento de Azure como blob, contenedor o tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="1a29d-541">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="1a29d-542">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="1a29d-543">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-544">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-544">Dataset</span></span>
<span data-ttu-id="1a29d-545">Para definir un conjunto de datos de Azure Blob, establezca el **tipo** del conjunto de datos en **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="1a29d-546">Después, especifique las siguientes propiedades específicas de Azure Blob en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-547">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-547">Property</span></span> | <span data-ttu-id="1a29d-548">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-548">Description</span></span> | <span data-ttu-id="1a29d-549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-550">folderPath</span></span> |<span data-ttu-id="1a29d-551">Ruta de acceso para el contenedor y la carpeta en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="1a29d-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="1a29d-552">Ejemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="1a29d-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="1a29d-553">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-553">Yes</span></span> |
| <span data-ttu-id="1a29d-554">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-554">fileName</span></span> |<span data-ttu-id="1a29d-555">Nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="1a29d-555">Name of the blob.</span></span> <span data-ttu-id="1a29d-556">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="1a29d-557">Si especifica fileName, la actividad (incluida la copia) funciona en el blob específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="1a29d-558">Cuando no se especifica fileName, la copia incluirá todos los blobs de folderPath para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="1a29d-559">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo tendría este formato:Data.<Guid>.txt (por ejemplo: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1a29d-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1a29d-560">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-560">No</span></span> |
| <span data-ttu-id="1a29d-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-561">partitionedBy</span></span> |<span data-ttu-id="1a29d-562">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="1a29d-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="1a29d-563">Puede usarla para especificar un folderPath dinámico y un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="1a29d-564">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-565">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-565">No</span></span> |
| <span data-ttu-id="1a29d-566">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-566">format</span></span> | <span data-ttu-id="1a29d-567">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-568">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-569">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-570">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-571">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-571">No</span></span> |
| <span data-ttu-id="1a29d-572">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-572">compression</span></span> | <span data-ttu-id="1a29d-573">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-574">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-575">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-576">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-577">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-578">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="1a29d-579">Para más información, consulte el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="1a29d-580">BlobSource en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="1a29d-581">Si va a copiar datos desde Azure Blob Storage, establezca el **tipo de origen** de la actividad de copia en **BlobSource** y especifique las siguientes propiedades en la sección **origen **:</span><span class="sxs-lookup"><span data-stu-id="1a29d-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="1a29d-582">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-582">Property</span></span> | <span data-ttu-id="1a29d-583">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-583">Description</span></span> | <span data-ttu-id="1a29d-584">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-584">Allowed values</span></span> | <span data-ttu-id="1a29d-585">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-586">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-586">recursive</span></span> |<span data-ttu-id="1a29d-587">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-588">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="1a29d-588">True (default value), False</span></span> |<span data-ttu-id="1a29d-589">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="1a29d-590">Ejemplo: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="1a29d-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="1a29d-591">BlobSink en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="1a29d-592">Si va a copiar datos a Azure Blob Storage, establezca el **tipo de receptor** de la actividad de copia en **BlobSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-593">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-593">Property</span></span> | <span data-ttu-id="1a29d-594">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-594">Description</span></span> | <span data-ttu-id="1a29d-595">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-595">Allowed values</span></span> | <span data-ttu-id="1a29d-596">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1a29d-597">copyBehavior</span></span> |<span data-ttu-id="1a29d-598">Define el comportamiento de copia cuando el origen es BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="1a29d-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="1a29d-599"><b>PreserveHierarchy:</b> conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="1a29d-600">La ruta de acceso relativa del archivo de origen que apunta a la carpeta de origen es idéntica a la ruta de acceso relativa del archivo de destino que apunta a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="1a29d-601"><b>FlattenHierarchy:</b> todos los archivos de la carpeta de origen están en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="1a29d-602">Los archivos de destino tienen un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="1a29d-603"><b>MergeFiles: (valor predeterminado)</b> combina todos los archivos de la carpeta de origen en un solo archivo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="1a29d-604">Si se especifica el nombre de archivo/blob, el nombre de archivo combinado sería el nombre especificado; de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="1a29d-605">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="1a29d-606">Ejemplo: BlobSink</span><span class="sxs-lookup"><span data-stu-id="1a29d-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-607">Para obtener más información, vea el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="1a29d-608">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-609">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-609">Linked service</span></span>
<span data-ttu-id="1a29d-610">Para definir un servicio vinculado de Azure Data Lake Store, establezca el tipo de servicio vinculado en **AzureDataLakeStore** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-611">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-611">Property</span></span> | <span data-ttu-id="1a29d-612">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-612">Description</span></span> | <span data-ttu-id="1a29d-613">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-614">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-614">type</span></span> | <span data-ttu-id="1a29d-615">La propiedad type debe establecerse en: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="1a29d-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="1a29d-616">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-616">Yes</span></span> |
| <span data-ttu-id="1a29d-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="1a29d-617">dataLakeStoreUri</span></span> | <span data-ttu-id="1a29d-618">Especifica información sobre la cuenta de Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1a29d-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="1a29d-619">Tiene el siguiente formato: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="1a29d-620">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-620">Yes</span></span> |
| <span data-ttu-id="1a29d-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1a29d-621">subscriptionId</span></span> | <span data-ttu-id="1a29d-622">Identificador de suscripción de Azure al que pertenece Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a29d-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="1a29d-623">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="1a29d-623">Required for sink</span></span> |
| <span data-ttu-id="1a29d-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1a29d-624">resourceGroupName</span></span> | <span data-ttu-id="1a29d-625">Nombre del grupo de recursos de Azure al que pertenece Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a29d-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="1a29d-626">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="1a29d-626">Required for sink</span></span> |
| <span data-ttu-id="1a29d-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="1a29d-627">servicePrincipalId</span></span> | <span data-ttu-id="1a29d-628">Especifique el id. de cliente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-628">Specify the application's client ID.</span></span> | <span data-ttu-id="1a29d-629">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="1a29d-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="1a29d-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="1a29d-630">servicePrincipalKey</span></span> | <span data-ttu-id="1a29d-631">Especifique la clave de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-631">Specify the application's key.</span></span> | <span data-ttu-id="1a29d-632">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="1a29d-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="1a29d-633">tenant</span><span class="sxs-lookup"><span data-stu-id="1a29d-633">tenant</span></span> | <span data-ttu-id="1a29d-634">Especifique la información del inquilino (nombre de dominio o identificador de inquilino) en el que reside la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="1a29d-635">Para recuperarlo, mantenga el puntero del mouse en la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1a29d-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="1a29d-636">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="1a29d-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="1a29d-637">authorization</span><span class="sxs-lookup"><span data-stu-id="1a29d-637">authorization</span></span> | <span data-ttu-id="1a29d-638">Haga clic en el botón **Autorizar** de **Data Factory Editor** y escriba sus credenciales; de esta forma, se asigna la dirección URL de autorización generada automáticamente a esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="1a29d-639">Sí (para la autenticación de credenciales de usuario)</span><span class="sxs-lookup"><span data-stu-id="1a29d-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="1a29d-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="1a29d-640">sessionId</span></span> | <span data-ttu-id="1a29d-641">Id. de sesión de OAuth de la sesión de autorización de OAuth.</span><span class="sxs-lookup"><span data-stu-id="1a29d-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="1a29d-642">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="1a29d-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="1a29d-643">Esta configuración se genera automáticamente al usar el Editor de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="1a29d-644">Sí (para la autenticación de credenciales de usuario)</span><span class="sxs-lookup"><span data-stu-id="1a29d-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="1a29d-645">Ejemplo: uso de la autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="1a29d-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="1a29d-646">Ejemplo: uso de la autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="1a29d-647">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-648">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-648">Dataset</span></span>
<span data-ttu-id="1a29d-649">Para definir un conjunto de datos de Azure Data Lake Store, establezca el **tipo** del conjunto de datos en **AzureDataLakeStore** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-650">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-650">Property</span></span> | <span data-ttu-id="1a29d-651">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-651">Description</span></span> | <span data-ttu-id="1a29d-652">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-653">folderPath</span></span> |<span data-ttu-id="1a29d-654">Ruta de acceso al contenedor y a la carpeta del almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1a29d-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="1a29d-655">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-655">Yes</span></span> |
| <span data-ttu-id="1a29d-656">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-656">fileName</span></span> |<span data-ttu-id="1a29d-657">Nombre del archivo en el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1a29d-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="1a29d-658">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="1a29d-659">Si especifica fileName, la actividad (incluida la copia) funciona en el archivo específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="1a29d-660">Cuando no se especifica fileName, la copia incluirá todos los archivos de folderPath para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="1a29d-661">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo tendría este formato:Data<Guid>.txt (por ejemplo: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1a29d-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1a29d-662">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-662">No</span></span> |
| <span data-ttu-id="1a29d-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-663">partitionedBy</span></span> |<span data-ttu-id="1a29d-664">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="1a29d-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="1a29d-665">Puede usarla para especificar un folderPath dinámico y un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="1a29d-666">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-667">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-667">No</span></span> |
| <span data-ttu-id="1a29d-668">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-668">format</span></span> | <span data-ttu-id="1a29d-669">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-670">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-671">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-672">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-673">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-673">No</span></span> |
| <span data-ttu-id="1a29d-674">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-674">compression</span></span> | <span data-ttu-id="1a29d-675">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-676">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-677">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-678">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-679">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-680">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-681">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="1a29d-682">Origen de Azure Data Lake Store en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-683">Si va a copiar datos desde Azure Data Lake Store, establezca el **tipo de origen** de la actividad de copia en **AzureDataLakeStoreSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="1a29d-684">**AzureDataLakeStoreSource** admite las siguientes propiedades **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="1a29d-685">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-685">Property</span></span> | <span data-ttu-id="1a29d-686">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-686">Description</span></span> | <span data-ttu-id="1a29d-687">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-687">Allowed values</span></span> | <span data-ttu-id="1a29d-688">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-689">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-689">recursive</span></span> |<span data-ttu-id="1a29d-690">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-691">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="1a29d-691">True (default value), False</span></span> |<span data-ttu-id="1a29d-692">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="1a29d-693">Ejemplo: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="1a29d-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-694">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="1a29d-695">Receptor de Azure Data Lake Store en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-696">Si va a copiar datos a Azure Data Lake Store, establezca el **tipo de receptor** de la actividad de copia en **AzureDataLakeStoreSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-697">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-697">Property</span></span> | <span data-ttu-id="1a29d-698">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-698">Description</span></span> | <span data-ttu-id="1a29d-699">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-699">Allowed values</span></span> | <span data-ttu-id="1a29d-700">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1a29d-701">copyBehavior</span></span> |<span data-ttu-id="1a29d-702">Especifica el comportamiento de copia.</span><span class="sxs-lookup"><span data-stu-id="1a29d-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="1a29d-703"><b>PreserveHierarchy:</b> conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="1a29d-704">La ruta de acceso relativa del archivo de origen que apunta a la carpeta de origen es idéntica a la ruta de acceso relativa del archivo de destino que apunta a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="1a29d-705"><b>FlattenHierarchy:</b> todos los archivos de la carpeta de origen se crean en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="1a29d-706">Los archivos de destino se crean con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="1a29d-707"><b>MergeFiles:</b> combina todos los archivos de la carpeta de origen en un archivo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="1a29d-708">Si se especifica el nombre de archivo/blob, el nombre de archivo combinado sería el nombre especificado; de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="1a29d-709">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="1a29d-710">Ejemplo: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="1a29d-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-711">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="1a29d-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a29d-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="1a29d-713">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-713">Linked service</span></span>
<span data-ttu-id="1a29d-714">Para definir un servicio vinculado de Azure Cosmos DB, establezca el **tipo** del servicio vinculado en **DocumentDb** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-715">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="1a29d-715">**Property**</span></span> | <span data-ttu-id="1a29d-716">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1a29d-716">**Description**</span></span> | <span data-ttu-id="1a29d-717">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="1a29d-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-718">connectionString</span></span> |<span data-ttu-id="1a29d-719">Especifique la información necesaria para conectarse a la base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="1a29d-720">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-721">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="1a29d-722">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-723">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-723">Dataset</span></span>
<span data-ttu-id="1a29d-724">Para definir un conjunto de datos de Azure Cosmos DB, establezca el **tipo** del conjunto de datos en **DocumentDbCollection** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-725">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="1a29d-725">**Property**</span></span> | <span data-ttu-id="1a29d-726">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1a29d-726">**Description**</span></span> | <span data-ttu-id="1a29d-727">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="1a29d-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="1a29d-728">collectionName</span></span> |<span data-ttu-id="1a29d-729">Nombre de la colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="1a29d-730">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-731">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="1a29d-732">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="1a29d-733">Origen de la colección de Azure Cosmos DB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-734">Si va a copiar datos desde Azure Cosmos DB, establezca el **tipo de origen** de la actividad de copia en **DocumentDbCollectionSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-735">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="1a29d-735">**Property**</span></span> | <span data-ttu-id="1a29d-736">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1a29d-736">**Description**</span></span> | <span data-ttu-id="1a29d-737">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="1a29d-737">**Allowed values**</span></span> | <span data-ttu-id="1a29d-738">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="1a29d-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-739">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-739">query</span></span> |<span data-ttu-id="1a29d-740">Especifique la consulta para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-740">Specify the query to read data.</span></span> |<span data-ttu-id="1a29d-741">Cadena de consulta admitida por Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="1a29d-742">Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="1a29d-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="1a29d-743">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-743">No</span></span> <br/><br/><span data-ttu-id="1a29d-744">Si no se especifica, la instrucción SQL que se ejecuta: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="1a29d-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="1a29d-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="1a29d-745">nestingSeparator</span></span> |<span data-ttu-id="1a29d-746">Carácter especial para indicar que el documento está anidado</span><span class="sxs-lookup"><span data-stu-id="1a29d-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="1a29d-747">Cualquier carácter.</span><span class="sxs-lookup"><span data-stu-id="1a29d-747">Any character.</span></span> <br/><br/><span data-ttu-id="1a29d-748">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="1a29d-749">Azure Data Factory permite al usuario indicar la jerarquía a través de nestingSeparator que es "."</span><span class="sxs-lookup"><span data-stu-id="1a29d-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="1a29d-750">en los ejemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-750">in the above examples.</span></span> <span data-ttu-id="1a29d-751">Con el separador, la actividad de copia generará el objeto "Name" con tres elementos secundarios First, Middle y Last, según "Name.First", "Name.Middle" y "Name.Last" en la definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="1a29d-752">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-753">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="1a29d-754">Receptor de la colección de Azure Cosmos DB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-755">Si va a copiar datos a Azure Cosmos DB, establezca el **tipo de receptor** de la actividad de copia en **DocumentDbCollectionSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-756">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="1a29d-756">**Property**</span></span> | <span data-ttu-id="1a29d-757">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1a29d-757">**Description**</span></span> | <span data-ttu-id="1a29d-758">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="1a29d-758">**Allowed values**</span></span> | <span data-ttu-id="1a29d-759">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="1a29d-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="1a29d-760">nestingSeparator</span></span> |<span data-ttu-id="1a29d-761">Un carácter especial en el nombre de columna de origen que indica que el documento anidado es necesario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="1a29d-762">En el ejemplo anterior: `Name.First` en la tabla de salida produce la siguiente estructura JSON en el documento de Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="1a29d-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="1a29d-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="1a29d-763">"Name": {</span></span><br/>    <span data-ttu-id="1a29d-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="1a29d-764">"First": "John"</span></span><br/><span data-ttu-id="1a29d-765">},</span><span class="sxs-lookup"><span data-stu-id="1a29d-765">},</span></span> |<span data-ttu-id="1a29d-766">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="1a29d-767">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="1a29d-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="1a29d-768">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="1a29d-769">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="1a29d-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="1a29d-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-770">writeBatchSize</span></span> |<span data-ttu-id="1a29d-771">Número de solicitudes paralelas al servicio de Azure Cosmos DB para crear documentos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="1a29d-772">Puede ajustar el rendimiento cuando se copian datos en Azure Cosmos DB, y viceversa, mediante esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="1a29d-773">Puede esperar un rendimiento mejor al aumentar writeBatchSize porque se envían más solicitudes paralelas a Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="1a29d-774">Sin embargo, deberá evitar una limitación de solicitudes que puede generar el mensaje de error: "La tasa de solicitudes es grande".</span><span class="sxs-lookup"><span data-stu-id="1a29d-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="1a29d-775">La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una colección mejor (por ejemplo, S3) para obtener el máximo rendimiento disponible (2500 unidades de solicitudes por segundo).</span><span class="sxs-lookup"><span data-stu-id="1a29d-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="1a29d-776">Entero </span><span class="sxs-lookup"><span data-stu-id="1a29d-776">Integer</span></span> |<span data-ttu-id="1a29d-777">No (valor predeterminado: 5)</span><span class="sxs-lookup"><span data-stu-id="1a29d-777">No (default: 5)</span></span> |
| <span data-ttu-id="1a29d-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-778">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-779">Tiempo de espera para que la operación se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="1a29d-780">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-780">timespan</span></span><br/><br/> <span data-ttu-id="1a29d-781">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="1a29d-782">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-783">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="1a29d-784">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="1a29d-785">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-786">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-786">Linked service</span></span>
<span data-ttu-id="1a29d-787">Para definir un servicio vinculado de Azure SQL Database, establezca el **tipo** de servicio vinculado en **AzureSqlDatabase** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-788">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-788">Property</span></span> | <span data-ttu-id="1a29d-789">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-789">Description</span></span> | <span data-ttu-id="1a29d-790">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-791">connectionString</span></span> |<span data-ttu-id="1a29d-792">Especifique la información necesaria para conectarse a la instancia de Base de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="1a29d-793">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-794">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="1a29d-795">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-796">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-796">Dataset</span></span>
<span data-ttu-id="1a29d-797">Para definir un conjunto de datos de Azure SQL Database, establezca el **tipo** de conjunto de datos en **AzureSqlTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-798">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-798">Property</span></span> | <span data-ttu-id="1a29d-799">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-799">Description</span></span> | <span data-ttu-id="1a29d-800">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-801">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-801">tableName</span></span> |<span data-ttu-id="1a29d-802">Nombre de la tabla o vista en la instancia de Azure SQL Database a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="1a29d-803">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-804">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="1a29d-805">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="1a29d-806">Origen de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-807">Si va a copiar datos desde Azure SQL Database, establezca el **tipo de origen** de la actividad de copia en **SqlSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-808">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-808">Property</span></span> | <span data-ttu-id="1a29d-809">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-809">Description</span></span> | <span data-ttu-id="1a29d-810">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-810">Allowed values</span></span> | <span data-ttu-id="1a29d-811">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1a29d-812">sqlReaderQuery</span></span> |<span data-ttu-id="1a29d-813">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-813">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-814">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-814">SQL query string.</span></span> <span data-ttu-id="1a29d-815">Ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-816">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-816">No</span></span> |
| <span data-ttu-id="1a29d-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="1a29d-818">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="1a29d-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="1a29d-819">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-819">Name of the stored procedure.</span></span> |<span data-ttu-id="1a29d-820">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-820">No</span></span> |
| <span data-ttu-id="1a29d-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-821">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-822">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1a29d-823">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-823">Name/value pairs.</span></span> <span data-ttu-id="1a29d-824">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1a29d-825">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-826">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="1a29d-827">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="1a29d-828">Receptor de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-829">Si va a copiar datos a Azure SQL Database, establezca el **tipo de receptor** de la actividad de copia en **SqlSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-830">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-830">Property</span></span> | <span data-ttu-id="1a29d-831">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-831">Description</span></span> | <span data-ttu-id="1a29d-832">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-832">Allowed values</span></span> | <span data-ttu-id="1a29d-833">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-834">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-835">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1a29d-836">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-836">timespan</span></span><br/><br/> <span data-ttu-id="1a29d-837">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="1a29d-838">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-838">No</span></span> |
| <span data-ttu-id="1a29d-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-839">writeBatchSize</span></span> |<span data-ttu-id="1a29d-840">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1a29d-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="1a29d-841">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="1a29d-841">Integer (number of rows)</span></span> |<span data-ttu-id="1a29d-842">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="1a29d-842">No (default: 10000)</span></span> |
| <span data-ttu-id="1a29d-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1a29d-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1a29d-844">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="1a29d-845">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-845">A query statement.</span></span> |<span data-ttu-id="1a29d-846">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-846">No</span></span> |
| <span data-ttu-id="1a29d-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1a29d-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="1a29d-848">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="1a29d-849">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="1a29d-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="1a29d-850">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-850">No</span></span> |
| <span data-ttu-id="1a29d-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="1a29d-852">Nombre del procedimiento almacenado que actualiza e inserta (operación de upsert) datos en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="1a29d-853">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-853">Name of the stored procedure.</span></span> |<span data-ttu-id="1a29d-854">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-854">No</span></span> |
| <span data-ttu-id="1a29d-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-855">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-856">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1a29d-857">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-857">Name/value pairs.</span></span> <span data-ttu-id="1a29d-858">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1a29d-859">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-859">No</span></span> |
| <span data-ttu-id="1a29d-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="1a29d-860">sqlWriterTableType</span></span> |<span data-ttu-id="1a29d-861">Especifique el nombre del tipo de tabla que se usará en el procedimiento almacenado anterior.</span><span class="sxs-lookup"><span data-stu-id="1a29d-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="1a29d-862">La actividad de copia dispone que los datos que se mueven estén disponibles en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="1a29d-863">El código de procedimiento almacenado puede combinar los datos copiados con datos existentes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="1a29d-864">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-864">A table type name.</span></span> |<span data-ttu-id="1a29d-865">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-866">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-867">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="1a29d-868">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-869">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-869">Linked service</span></span>
<span data-ttu-id="1a29d-870">Para definir un servicio vinculado de Azure SQL Data Warehouse, establezca el **tipo** de servicio vinculado en **AzureSqlDW** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-871">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-871">Property</span></span> | <span data-ttu-id="1a29d-872">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-872">Description</span></span> | <span data-ttu-id="1a29d-873">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-874">connectionString</span></span> |<span data-ttu-id="1a29d-875">Especifique la información necesaria para conectarse a la instancia de Almacenamiento de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="1a29d-876">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="1a29d-877">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="1a29d-878">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-879">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-879">Dataset</span></span>
<span data-ttu-id="1a29d-880">Para definir un conjunto de datos de Azure SQL Data Warehouse, establezca el **tipo** de conjunto de datos en **AzureSqlDWTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-881">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-881">Property</span></span> | <span data-ttu-id="1a29d-882">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-882">Description</span></span> | <span data-ttu-id="1a29d-883">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-884">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-884">tableName</span></span> |<span data-ttu-id="1a29d-885">Nombre de la tabla o vista en la base de datos de Azure SQL Data Warehouse a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="1a29d-886">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-887">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-888">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="1a29d-889">Origen de SQL DW en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-890">Si va a copiar datos desde Azure SQL Data Warehouse, establezca el **tipo de origen** de la actividad de copia en **SqlDWSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-891">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-891">Property</span></span> | <span data-ttu-id="1a29d-892">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-892">Description</span></span> | <span data-ttu-id="1a29d-893">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-893">Allowed values</span></span> | <span data-ttu-id="1a29d-894">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1a29d-895">sqlReaderQuery</span></span> |<span data-ttu-id="1a29d-896">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-896">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-897">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-897">SQL query string.</span></span> <span data-ttu-id="1a29d-898">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-899">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-899">No</span></span> |
| <span data-ttu-id="1a29d-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="1a29d-901">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="1a29d-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="1a29d-902">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-902">Name of the stored procedure.</span></span> |<span data-ttu-id="1a29d-903">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-903">No</span></span> |
| <span data-ttu-id="1a29d-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-904">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-905">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1a29d-906">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-906">Name/value pairs.</span></span> <span data-ttu-id="1a29d-907">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1a29d-908">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-909">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-910">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="1a29d-911">Receptor de SQL DW en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-912">Si va a copiar datos a Azure SQL Data Warehouse, establezca el **tipo de receptor** de la actividad de copia en **SqlDWSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-913">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-913">Property</span></span> | <span data-ttu-id="1a29d-914">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-914">Description</span></span> | <span data-ttu-id="1a29d-915">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-915">Allowed values</span></span> | <span data-ttu-id="1a29d-916">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1a29d-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1a29d-918">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="1a29d-919">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-919">A query statement.</span></span> |<span data-ttu-id="1a29d-920">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-920">No</span></span> |
| <span data-ttu-id="1a29d-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="1a29d-921">allowPolyBase</span></span> |<span data-ttu-id="1a29d-922">Indica si se usa PolyBase (si procede) en lugar del mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="1a29d-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="1a29d-923">**El uso de PolyBase es el método recomendado para cargar datos en SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="1a29d-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="1a29d-924">True </span><span class="sxs-lookup"><span data-stu-id="1a29d-924">True</span></span> <br/><span data-ttu-id="1a29d-925">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="1a29d-925">False (default)</span></span> |<span data-ttu-id="1a29d-926">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-926">No</span></span> |
| <span data-ttu-id="1a29d-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="1a29d-927">polyBaseSettings</span></span> |<span data-ttu-id="1a29d-928">Un grupo de propiedades que se pueden especificar si el valor de la propiedad **allowPolybase** está establecido en **true**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="1a29d-929">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-929">No</span></span> |
| <span data-ttu-id="1a29d-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="1a29d-930">rejectValue</span></span> |<span data-ttu-id="1a29d-931">Especifica el número o porcentaje de filas que se pueden rechazar antes de que se produzca un error en la consulta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="1a29d-932">Más información sobre las opciones de rechazo de PolyBase en la sección **Argumentos** del tema [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) [CREAR UNA TABLA EXTERNA (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="1a29d-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="1a29d-933">0 (predeterminado), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="1a29d-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="1a29d-934">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-934">No</span></span> |
| <span data-ttu-id="1a29d-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="1a29d-935">rejectType</span></span> |<span data-ttu-id="1a29d-936">Especifica si se indica la opción rejectValue como un valor literal o un porcentaje.</span><span class="sxs-lookup"><span data-stu-id="1a29d-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="1a29d-937">Valor (predeterminado), Porcentaje</span><span class="sxs-lookup"><span data-stu-id="1a29d-937">Value (default), Percentage</span></span> |<span data-ttu-id="1a29d-938">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-938">No</span></span> |
| <span data-ttu-id="1a29d-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="1a29d-939">rejectSampleValue</span></span> |<span data-ttu-id="1a29d-940">Determina el número de filas que se van a recuperar antes de que PolyBase vuelva a calcular el porcentaje de filas rechazadas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="1a29d-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="1a29d-941">1, 2, …</span></span> |<span data-ttu-id="1a29d-942">Sí, si el valor de **rejectType** es **percentage**</span><span class="sxs-lookup"><span data-stu-id="1a29d-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="1a29d-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="1a29d-943">useTypeDefault</span></span> |<span data-ttu-id="1a29d-944">Especifica cómo administrar los valores que faltan en archivos de texto delimitados cuando PolyBase recupera datos del archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="1a29d-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="1a29d-945">Más información sobre esta propiedad en la sección de argumentos de [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a29d-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="1a29d-946">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="1a29d-946">True, False (default)</span></span> |<span data-ttu-id="1a29d-947">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-947">No</span></span> |
| <span data-ttu-id="1a29d-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-948">writeBatchSize</span></span> |<span data-ttu-id="1a29d-949">Inserta datos en la tabla SQL cuando el tamaño del búfer alcance writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="1a29d-950">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="1a29d-950">Integer (number of rows)</span></span> |<span data-ttu-id="1a29d-951">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="1a29d-951">No (default: 10000)</span></span> |
| <span data-ttu-id="1a29d-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-952">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-953">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1a29d-954">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-954">timespan</span></span><br/><br/> <span data-ttu-id="1a29d-955">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="1a29d-956">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-957">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-958">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="1a29d-959">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-960">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-960">Linked service</span></span>
<span data-ttu-id="1a29d-961">Para definir un servicio vinculado de Azure Search, establezca el **tipo** de servicio vinculado en **AzureSearch** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-962">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-962">Property</span></span> | <span data-ttu-id="1a29d-963">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-963">Description</span></span> | <span data-ttu-id="1a29d-964">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="1a29d-965">URL</span><span class="sxs-lookup"><span data-stu-id="1a29d-965">url</span></span> | <span data-ttu-id="1a29d-966">La URL del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1a29d-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="1a29d-967">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-967">Yes</span></span> |
| <span data-ttu-id="1a29d-968">key</span><span class="sxs-lookup"><span data-stu-id="1a29d-968">key</span></span> | <span data-ttu-id="1a29d-969">La clave de administración del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1a29d-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="1a29d-970">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-971">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="1a29d-972">Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-973">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-973">Dataset</span></span>
<span data-ttu-id="1a29d-974">Para definir un conjunto de datos de Azure Search, establezca el **tipo** de conjunto de datos en **AzureSearchIndex** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-975">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-975">Property</span></span> | <span data-ttu-id="1a29d-976">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-976">Description</span></span> | <span data-ttu-id="1a29d-977">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="1a29d-978">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-978">type</span></span> | <span data-ttu-id="1a29d-979">La propiedad type debe establecerse en **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="1a29d-980">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-980">Yes</span></span> |
| <span data-ttu-id="1a29d-981">indexName</span><span class="sxs-lookup"><span data-stu-id="1a29d-981">indexName</span></span> | <span data-ttu-id="1a29d-982">Nombre del índice de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1a29d-982">Name of the Azure Search index.</span></span> <span data-ttu-id="1a29d-983">Data Factory no crea el índice.</span><span class="sxs-lookup"><span data-stu-id="1a29d-983">Data Factory does not create the index.</span></span> <span data-ttu-id="1a29d-984">El índice debe existir en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1a29d-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="1a29d-985">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-986">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="1a29d-987">Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="1a29d-988">Receptor del índice de Azure Search en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-989">Si va a copiar datos a Azure Search, establezca el **tipo de receptor** de la actividad de copia en **AzureSearchIndexSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-990">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-990">Property</span></span> | <span data-ttu-id="1a29d-991">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-991">Description</span></span> | <span data-ttu-id="1a29d-992">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-992">Allowed values</span></span> | <span data-ttu-id="1a29d-993">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="1a29d-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="1a29d-994">WriteBehavior</span></span> | <span data-ttu-id="1a29d-995">Especifica si, cuando ya haya un documento en el índice, se realizará una operación de combinación o de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="1a29d-996">Combinar (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="1a29d-996">Merge (default)</span></span><br/><span data-ttu-id="1a29d-997">Cargar</span><span class="sxs-lookup"><span data-stu-id="1a29d-997">Upload</span></span>| <span data-ttu-id="1a29d-998">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-998">No</span></span> |
| <span data-ttu-id="1a29d-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-999">WriteBatchSize</span></span> | <span data-ttu-id="1a29d-1000">Carga datos en el índice de Azure Search cuando el tamaño del búfer alcanza el valor de WriteBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="1a29d-1001">De 1 a 1000.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1001">1 to 1,000.</span></span> <span data-ttu-id="1a29d-1002">El valor predeterminado es 1000.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1002">Default value is 1000.</span></span> | <span data-ttu-id="1a29d-1003">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1004">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1005">Para obtener más información, vea el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="1a29d-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="1a29d-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1007">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1007">Linked service</span></span>
<span data-ttu-id="1a29d-1008">Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="1a29d-1009">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="1a29d-1010">Para vincular la cuenta de Azure Storage a una instancia de Data Factory mediante una **clave de cuenta**, cree un servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="1a29d-1011">Para definir un servicio vinculado de Azure Storage, establezca el **tipo** del servicio vinculado en **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="1a29d-1012">Después, puede especificar las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1013">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1013">Property</span></span> | <span data-ttu-id="1a29d-1014">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1014">Description</span></span> | <span data-ttu-id="1a29d-1015">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-1016">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-1016">type</span></span> |<span data-ttu-id="1a29d-1017">La propiedad type debe establecerse en: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="1a29d-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="1a29d-1018">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1018">Yes</span></span> |
| <span data-ttu-id="1a29d-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-1019">connectionString</span></span> |<span data-ttu-id="1a29d-1020">Especifique la información necesaria para conectarse a Almacenamiento de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="1a29d-1021">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1021">Yes</span></span> |

<span data-ttu-id="1a29d-1022">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1a29d-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="1a29d-1023">Servicio vinculado de SAS de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1a29d-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="1a29d-1024">El servicio vinculado de SAS de Almacenamiento de Azure le permite vincular una cuenta de Almacenamiento de Azure a una Factoría de datos de Azure con una Firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="1a29d-1025">Proporciona a la instancia de Data Factory acceso restringido o limitado por el tiempo a todos los recursos o a algunos específicos (blob o contenedor) del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="1a29d-1026">Para vincular la cuenta de Azure Storage a una instancia de Data Factory mediante una Firma de acceso compartido, cree un servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="1a29d-1027">Para definir un servicio vinculado de SAS de Azure Storage, establezca el **tipo** del servicio vinculado en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="1a29d-1028">Después, puede especificar las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="1a29d-1029">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1029">Property</span></span> | <span data-ttu-id="1a29d-1030">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1030">Description</span></span> | <span data-ttu-id="1a29d-1031">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-1032">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-1032">type</span></span> |<span data-ttu-id="1a29d-1033">La propiedad type debe establecerse en: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="1a29d-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="1a29d-1034">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1034">Yes</span></span> |
| <span data-ttu-id="1a29d-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="1a29d-1035">sasUri</span></span> |<span data-ttu-id="1a29d-1036">Especifique el URI de Firma de acceso compartido a los recursos de Almacenamiento de Azure como blob, contenedor o tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="1a29d-1037">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1037">Yes</span></span> |

<span data-ttu-id="1a29d-1038">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1a29d-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="1a29d-1039">Para más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1040">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1040">Dataset</span></span>
<span data-ttu-id="1a29d-1041">Para definir un conjunto de datos de Azure Table, establezca el **tipo** de conjunto de datos en **AzureTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1042">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1042">Property</span></span> | <span data-ttu-id="1a29d-1043">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1043">Description</span></span> | <span data-ttu-id="1a29d-1044">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1045">tableName</span></span> |<span data-ttu-id="1a29d-1046">Nombre de la tabla en la instancia de Base de datos de tablas de Azure a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="1a29d-1047">Sí.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1047">Yes.</span></span> <span data-ttu-id="1a29d-1048">Cuando se especifica un elemento tableName sin azureTableSourceQuery, se copian todos los registros de la tabla en el destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="1a29d-1049">Si también se especifica azureTableSourceQuery, los registros de la tabla que satisfacen los requisitos de la consulta se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1050">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1051">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="1a29d-1052">Origen de Azure Table en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1053">Si va a copiar datos desde Azure Table Storage, establezca el **tipo de origen** de la actividad de copia en **AzureTableSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1054">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1054">Property</span></span> | <span data-ttu-id="1a29d-1055">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1055">Description</span></span> | <span data-ttu-id="1a29d-1056">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1056">Allowed values</span></span> | <span data-ttu-id="1a29d-1057">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="1a29d-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="1a29d-1059">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1060">Cadena de consulta de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1060">Azure table query string.</span></span> <span data-ttu-id="1a29d-1061">Consulte los ejemplos en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1061">See examples in the next section.</span></span> |<span data-ttu-id="1a29d-1062">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1062">No.</span></span> <span data-ttu-id="1a29d-1063">Cuando se especifica un elemento tableName sin azureTableSourceQuery, se copian todos los registros de la tabla en el destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="1a29d-1064">Si también se especifica azureTableSourceQuery, los registros de la tabla que satisfacen los requisitos de la consulta se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="1a29d-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="1a29d-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="1a29d-1066">Indica si se omite la excepción de la tabla inexistente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="1a29d-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="1a29d-1067">TRUE</span></span><br/><span data-ttu-id="1a29d-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="1a29d-1068">FALSE</span></span> |<span data-ttu-id="1a29d-1069">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1070">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1071">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="1a29d-1072">Receptor de Azure Table en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-1073">Si va a copiar datos a Azure Table Storage, establezca el **tipo de receptor** de la actividad de copia en **AzureTableSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-1074">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1074">Property</span></span> | <span data-ttu-id="1a29d-1075">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1075">Description</span></span> | <span data-ttu-id="1a29d-1076">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1076">Allowed values</span></span> | <span data-ttu-id="1a29d-1077">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="1a29d-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="1a29d-1079">Valor predeterminado de la clave de la partición que puede usar el receptor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="1a29d-1080">Valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1080">A string value.</span></span> |<span data-ttu-id="1a29d-1081">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1081">No</span></span> |
| <span data-ttu-id="1a29d-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="1a29d-1083">Especifique el nombre de la columna cuyos valores se usan como claves de partición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="1a29d-1084">Si no se especifica, se utiliza AzureTableDefaultPartitionKeyValue como clave de la partición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="1a29d-1085">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1085">A column name.</span></span> |<span data-ttu-id="1a29d-1086">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1086">No</span></span> |
| <span data-ttu-id="1a29d-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="1a29d-1088">Especifique el nombre de la columna cuyos valores se usan como claves de fila.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="1a29d-1089">Si no se especifica, use un GUID para cada fila.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="1a29d-1090">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1090">A column name.</span></span> |<span data-ttu-id="1a29d-1091">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1091">No</span></span> |
| <span data-ttu-id="1a29d-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1092">azureTableInsertType</span></span> |<span data-ttu-id="1a29d-1093">Modo de insertar datos en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="1a29d-1094">Esta propiedad controla si los valores de las filas existentes en la tabla de salida con claves de partición y de fila coincidentes se van a reemplazar o a combinar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="1a29d-1095">Consulte los temas [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Insertar o combinar entidad) e [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Insertar o remplazar entidad) para más información sobre cómo funcionan estas opciones (combinación y reemplazo).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="1a29d-1096">Esta configuración se aplica en el nivel de fila, no en el nivel de tabla, y ninguna opción elimina filas de la tabla de salida que no existan en la entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="1a29d-1097">merge (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1097">merge (default)</span></span><br/><span data-ttu-id="1a29d-1098">replace</span><span class="sxs-lookup"><span data-stu-id="1a29d-1098">replace</span></span> |<span data-ttu-id="1a29d-1099">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1099">No</span></span> |
| <span data-ttu-id="1a29d-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-1100">writeBatchSize</span></span> |<span data-ttu-id="1a29d-1101">Inserta datos en la tabla de Azure cuando se alcanza el valor de writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="1a29d-1102">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1102">Integer (number of rows)</span></span> |<span data-ttu-id="1a29d-1103">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="1a29d-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-1104">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-1105">Inserta datos en la tabla de Azure cuando se alcanza el valor de writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="1a29d-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-1106">timespan</span></span><br/><br/><span data-ttu-id="1a29d-1107">Ejemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="1a29d-1108">No (el valor predeterminado de intervalo de tiempo del cliente de almacenamiento es 90 segundos)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="1a29d-1110">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="1a29d-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="1a29d-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1112">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1112">Linked service</span></span>
<span data-ttu-id="1a29d-1113">Para definir un servicio vinculado de Amazon Redshift, establezca el **tipo** de servicio vinculado en **AmazonRedshift** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1114">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1114">Property</span></span> | <span data-ttu-id="1a29d-1115">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1115">Description</span></span> | <span data-ttu-id="1a29d-1116">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1117">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1117">server</span></span> |<span data-ttu-id="1a29d-1118">Dirección IP o nombre de host del servidor de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="1a29d-1119">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1119">Yes</span></span> |
| <span data-ttu-id="1a29d-1120">puerto</span><span class="sxs-lookup"><span data-stu-id="1a29d-1120">port</span></span> |<span data-ttu-id="1a29d-1121">El número del puerto TCP que el servidor de Amazon Redshift utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="1a29d-1122">No, valor predeterminado: 5439</span><span class="sxs-lookup"><span data-stu-id="1a29d-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="1a29d-1123">database</span><span class="sxs-lookup"><span data-stu-id="1a29d-1123">database</span></span> |<span data-ttu-id="1a29d-1124">Nombre de la base de datos de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="1a29d-1125">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1125">Yes</span></span> |
| <span data-ttu-id="1a29d-1126">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1126">username</span></span> |<span data-ttu-id="1a29d-1127">Nombre del usuario que tiene acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="1a29d-1128">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1128">Yes</span></span> |
| <span data-ttu-id="1a29d-1129">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1129">password</span></span> |<span data-ttu-id="1a29d-1130">Contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1130">Password for the user account.</span></span> |<span data-ttu-id="1a29d-1131">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1132">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="1a29d-1133">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1134">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1134">Dataset</span></span>
<span data-ttu-id="1a29d-1135">Para definir un conjunto de datos de Amazon Redshift, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1136">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1136">Property</span></span> | <span data-ttu-id="1a29d-1137">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1137">Description</span></span> | <span data-ttu-id="1a29d-1138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1139">tableName</span></span> |<span data-ttu-id="1a29d-1140">Nombre de la tabla en la base de datos de Amazon Redshift a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="1a29d-1141">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-1142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="1a29d-1143">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1144">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="1a29d-1145">Si va a copiar datos desde Amazon Redshift, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1146">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1146">Property</span></span> | <span data-ttu-id="1a29d-1147">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1147">Description</span></span> | <span data-ttu-id="1a29d-1148">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1148">Allowed values</span></span> | <span data-ttu-id="1a29d-1149">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1150">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1150">query</span></span> |<span data-ttu-id="1a29d-1151">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1152">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1152">SQL query string.</span></span> <span data-ttu-id="1a29d-1153">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-1154">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1155">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="1a29d-1156">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="1a29d-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="1a29d-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1158">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1158">Linked service</span></span>
<span data-ttu-id="1a29d-1159">Para definir un servicio vinculado de IBM DB2, establezca el **tipo** de servicio vinculado en **OnPremisesDB2** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1160">Property</span></span> | <span data-ttu-id="1a29d-1161">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1161">Description</span></span> | <span data-ttu-id="1a29d-1162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1163">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1163">server</span></span> |<span data-ttu-id="1a29d-1164">Nombre del servidor DB2.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="1a29d-1165">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1165">Yes</span></span> |
| <span data-ttu-id="1a29d-1166">database</span><span class="sxs-lookup"><span data-stu-id="1a29d-1166">database</span></span> |<span data-ttu-id="1a29d-1167">Nombre de la base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="1a29d-1168">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1168">Yes</span></span> |
| <span data-ttu-id="1a29d-1169">schema</span><span class="sxs-lookup"><span data-stu-id="1a29d-1169">schema</span></span> |<span data-ttu-id="1a29d-1170">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1170">Name of the schema in the database.</span></span> <span data-ttu-id="1a29d-1171">El nombre del esquema distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="1a29d-1172">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1172">No</span></span> |
| <span data-ttu-id="1a29d-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1173">authenticationType</span></span> |<span data-ttu-id="1a29d-1174">Tipo de autenticación usado para conectarse a la base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="1a29d-1175">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1a29d-1176">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1176">Yes</span></span> |
| <span data-ttu-id="1a29d-1177">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1177">username</span></span> |<span data-ttu-id="1a29d-1178">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="1a29d-1179">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1179">No</span></span> |
| <span data-ttu-id="1a29d-1180">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1180">password</span></span> |<span data-ttu-id="1a29d-1181">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-1182">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1182">No</span></span> |
| <span data-ttu-id="1a29d-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1183">gatewayName</span></span> |<span data-ttu-id="1a29d-1184">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos DB2 local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="1a29d-1185">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1186">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="1a29d-1187">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1188">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1188">Dataset</span></span>
<span data-ttu-id="1a29d-1189">Para definir un conjunto de datos de DB2, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="1a29d-1190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1190">Property</span></span> | <span data-ttu-id="1a29d-1191">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1191">Description</span></span> | <span data-ttu-id="1a29d-1192">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1193">tableName</span></span> |<span data-ttu-id="1a29d-1194">Nombre de la tabla en la instancia de base de datos DB2 a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="1a29d-1195">tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="1a29d-1196">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="1a29d-1197">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1198">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1199">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1200">Si va a copiar datos desde IBM DB2, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1201">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1201">Property</span></span> | <span data-ttu-id="1a29d-1202">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1202">Description</span></span> | <span data-ttu-id="1a29d-1203">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1203">Allowed values</span></span> | <span data-ttu-id="1a29d-1204">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1205">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1205">query</span></span> |<span data-ttu-id="1a29d-1206">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1207">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1207">SQL query string.</span></span> <span data-ttu-id="1a29d-1208">Por ejemplo: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="1a29d-1209">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1210">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="1a29d-1211">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="1a29d-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1213">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1213">Linked service</span></span>
<span data-ttu-id="1a29d-1214">Para definir un servicio vinculado de MySQL, establezca el **tipo** de servicio vinculado en **OnPremisesMySql** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1215">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1215">Property</span></span> | <span data-ttu-id="1a29d-1216">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1216">Description</span></span> | <span data-ttu-id="1a29d-1217">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1218">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1218">server</span></span> |<span data-ttu-id="1a29d-1219">Nombre del servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="1a29d-1220">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1220">Yes</span></span> |
| <span data-ttu-id="1a29d-1221">database</span><span class="sxs-lookup"><span data-stu-id="1a29d-1221">database</span></span> |<span data-ttu-id="1a29d-1222">Nombre de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="1a29d-1223">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1223">Yes</span></span> |
| <span data-ttu-id="1a29d-1224">schema</span><span class="sxs-lookup"><span data-stu-id="1a29d-1224">schema</span></span> |<span data-ttu-id="1a29d-1225">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="1a29d-1226">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1226">No</span></span> |
| <span data-ttu-id="1a29d-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1227">authenticationType</span></span> |<span data-ttu-id="1a29d-1228">Tipo de autenticación usado para conectarse a la Base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="1a29d-1229">Los valores posibles son: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="1a29d-1230">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1230">Yes</span></span> |
| <span data-ttu-id="1a29d-1231">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1231">username</span></span> |<span data-ttu-id="1a29d-1232">Especifique el nombre de usuario para conectarse a la base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="1a29d-1233">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1233">Yes</span></span> |
| <span data-ttu-id="1a29d-1234">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1234">password</span></span> |<span data-ttu-id="1a29d-1235">Especifique la contraseña de la cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="1a29d-1236">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1236">Yes</span></span> |
| <span data-ttu-id="1a29d-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1237">gatewayName</span></span> |<span data-ttu-id="1a29d-1238">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la Base de datos MySQL local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="1a29d-1239">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1240">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-1241">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1242">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1242">Dataset</span></span>
<span data-ttu-id="1a29d-1243">Para definir un conjunto de datos de MySQL, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1244">Property</span></span> | <span data-ttu-id="1a29d-1245">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1245">Description</span></span> | <span data-ttu-id="1a29d-1246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1247">tableName</span></span> |<span data-ttu-id="1a29d-1248">Nombre de la tabla en la instancia de la Base de datos MySQL a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="1a29d-1249">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1250">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="1a29d-1251">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1252">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1253">Si va a copiar datos desde una base de datos MySQL, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1254">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1254">Property</span></span> | <span data-ttu-id="1a29d-1255">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1255">Description</span></span> | <span data-ttu-id="1a29d-1256">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1256">Allowed values</span></span> | <span data-ttu-id="1a29d-1257">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1258">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1258">query</span></span> |<span data-ttu-id="1a29d-1259">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1260">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1260">SQL query string.</span></span> <span data-ttu-id="1a29d-1261">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-1262">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-1263">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1264">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="1a29d-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="1a29d-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-1266">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1266">Linked service</span></span>
<span data-ttu-id="1a29d-1267">Para definir un servicio vinculado de Oracle, establezca el **tipo** de servicio vinculado en **OnPremisesOracle** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1268">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1268">Property</span></span> | <span data-ttu-id="1a29d-1269">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1269">Description</span></span> | <span data-ttu-id="1a29d-1270">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1271">driverType</span></span> | <span data-ttu-id="1a29d-1272">Especifique qué controlador usar para copiar datos en bases de datos de Oracle o desde ellas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="1a29d-1273">Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="1a29d-1274">Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="1a29d-1275">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1275">No</span></span> |
| <span data-ttu-id="1a29d-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-1276">connectionString</span></span> | <span data-ttu-id="1a29d-1277">Especifique la información necesaria para conectarse a la instancia de Base de datos de Oracle para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="1a29d-1278">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1278">Yes</span></span> |
| <span data-ttu-id="1a29d-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1279">gatewayName</span></span> | <span data-ttu-id="1a29d-1280">Nombre de la puerta de enlace que se usa para conectarse al servidor de Oracle local</span><span class="sxs-lookup"><span data-stu-id="1a29d-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="1a29d-1281">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1282">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="1a29d-1283">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1284">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1284">Dataset</span></span>
<span data-ttu-id="1a29d-1285">Para definir un conjunto de datos de Oracle, establezca el **tipo** de conjunto de datos en **OracleTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1286">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1286">Property</span></span> | <span data-ttu-id="1a29d-1287">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1287">Description</span></span> | <span data-ttu-id="1a29d-1288">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1289">tableName</span></span> |<span data-ttu-id="1a29d-1290">Nombre de la tabla en la instancia de Base de datos de Oracle a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="1a29d-1291">No (si se especifica **oracleReaderQuery** de **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1292">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="1a29d-1293">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="1a29d-1294">Origen de Oracle en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1295">Si va a copiar datos desde una base de datos de Oracle, establezca el **tipo de origen** de la actividad de copia en **OracleSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1296">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1296">Property</span></span> | <span data-ttu-id="1a29d-1297">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1297">Description</span></span> | <span data-ttu-id="1a29d-1298">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1298">Allowed values</span></span> | <span data-ttu-id="1a29d-1299">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1a29d-1300">oracleReaderQuery</span></span> |<span data-ttu-id="1a29d-1301">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1302">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1302">SQL query string.</span></span> <span data-ttu-id="1a29d-1303">Por ejemplo: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="1a29d-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="1a29d-1304">Si no se especifica, la instrucción SQL que se ejecuta: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="1a29d-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="1a29d-1305">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1306">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1307">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="1a29d-1308">Receptor de Oracle en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-1309">Si va a copiar datos a una base de datos de Oracle, establezca el **tipo de receptor** de la actividad de copia en **OracleSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-1310">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1310">Property</span></span> | <span data-ttu-id="1a29d-1311">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1311">Description</span></span> | <span data-ttu-id="1a29d-1312">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1312">Allowed values</span></span> | <span data-ttu-id="1a29d-1313">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-1314">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-1315">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1a29d-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-1316">timespan</span></span><br/><br/> <span data-ttu-id="1a29d-1317">Ejemplo: 00:30:00 (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="1a29d-1318">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1318">No</span></span> |
| <span data-ttu-id="1a29d-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-1319">writeBatchSize</span></span> |<span data-ttu-id="1a29d-1320">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="1a29d-1321">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1321">Integer (number of rows)</span></span> |<span data-ttu-id="1a29d-1322">No (valor predeterminado: 100)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1322">No (default: 100)</span></span> |
| <span data-ttu-id="1a29d-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1a29d-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1a29d-1324">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="1a29d-1325">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1325">A query statement.</span></span> |<span data-ttu-id="1a29d-1326">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1326">No</span></span> |
| <span data-ttu-id="1a29d-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="1a29d-1328">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="1a29d-1329">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="1a29d-1330">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1331">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="1a29d-1332">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="1a29d-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1334">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1334">Linked service</span></span>
<span data-ttu-id="1a29d-1335">Para definir un servicio vinculado de PostgreSQL, establezca el **tipo** de servicio vinculado en **OnPremisesPostgreSql** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1336">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1336">Property</span></span> | <span data-ttu-id="1a29d-1337">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1337">Description</span></span> | <span data-ttu-id="1a29d-1338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1339">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1339">server</span></span> |<span data-ttu-id="1a29d-1340">Nombre del servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="1a29d-1341">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1341">Yes</span></span> |
| <span data-ttu-id="1a29d-1342">database</span><span class="sxs-lookup"><span data-stu-id="1a29d-1342">database</span></span> |<span data-ttu-id="1a29d-1343">Nombre de la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="1a29d-1344">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1344">Yes</span></span> |
| <span data-ttu-id="1a29d-1345">schema</span><span class="sxs-lookup"><span data-stu-id="1a29d-1345">schema</span></span> |<span data-ttu-id="1a29d-1346">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1346">Name of the schema in the database.</span></span> <span data-ttu-id="1a29d-1347">El nombre del esquema distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="1a29d-1348">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1348">No</span></span> |
| <span data-ttu-id="1a29d-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1349">authenticationType</span></span> |<span data-ttu-id="1a29d-1350">Tipo de autenticación usado para conectarse a la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="1a29d-1351">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1a29d-1352">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1352">Yes</span></span> |
| <span data-ttu-id="1a29d-1353">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1353">username</span></span> |<span data-ttu-id="1a29d-1354">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="1a29d-1355">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1355">No</span></span> |
| <span data-ttu-id="1a29d-1356">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1356">password</span></span> |<span data-ttu-id="1a29d-1357">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-1358">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1358">No</span></span> |
| <span data-ttu-id="1a29d-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1359">gatewayName</span></span> |<span data-ttu-id="1a29d-1360">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos de PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="1a29d-1361">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1362">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="1a29d-1363">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1364">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1364">Dataset</span></span>
<span data-ttu-id="1a29d-1365">Para definir un conjunto de datos de PostgreSQL, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1366">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1366">Property</span></span> | <span data-ttu-id="1a29d-1367">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1367">Description</span></span> | <span data-ttu-id="1a29d-1368">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1369">tableName</span></span> |<span data-ttu-id="1a29d-1370">Nombre de la tabla en la instancia de Base de datos de PostgreSQL a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="1a29d-1371">tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="1a29d-1372">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1373">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="1a29d-1374">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1375">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1376">Si va a copiar datos desde una base de datos PostgreSQL, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1377">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1377">Property</span></span> | <span data-ttu-id="1a29d-1378">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1378">Description</span></span> | <span data-ttu-id="1a29d-1379">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1379">Allowed values</span></span> | <span data-ttu-id="1a29d-1380">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1381">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1381">query</span></span> |<span data-ttu-id="1a29d-1382">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1383">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1383">SQL query string.</span></span> <span data-ttu-id="1a29d-1384">Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="1a29d-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="1a29d-1385">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1386">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1387">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="1a29d-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a29d-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-1389">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1389">Linked service</span></span>
<span data-ttu-id="1a29d-1390">Para definir un servicio vinculado de SAP Business Warehouse (BW), establezca el **tipo** de servicio vinculado en **SapBw** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="1a29d-1391">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1391">Property</span></span> | <span data-ttu-id="1a29d-1392">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1392">Description</span></span> | <span data-ttu-id="1a29d-1393">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1393">Allowed values</span></span> | <span data-ttu-id="1a29d-1394">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1a29d-1395">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1395">server</span></span> | <span data-ttu-id="1a29d-1396">Nombre del servidor en el que reside la instancia de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="1a29d-1397">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1397">string</span></span> | <span data-ttu-id="1a29d-1398">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1398">Yes</span></span>
<span data-ttu-id="1a29d-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="1a29d-1399">systemNumber</span></span> | <span data-ttu-id="1a29d-1400">Número del sistema de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="1a29d-1401">Número decimal de dos dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="1a29d-1402">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1402">Yes</span></span>
<span data-ttu-id="1a29d-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="1a29d-1403">clientId</span></span> | <span data-ttu-id="1a29d-1404">Identificador del cliente en el sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="1a29d-1405">Número decimal de tres dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="1a29d-1406">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1406">Yes</span></span>
<span data-ttu-id="1a29d-1407">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1407">username</span></span> | <span data-ttu-id="1a29d-1408">Nombre del usuario que tiene acceso al servidor SAP</span><span class="sxs-lookup"><span data-stu-id="1a29d-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="1a29d-1409">cadena</span><span class="sxs-lookup"><span data-stu-id="1a29d-1409">string</span></span> | <span data-ttu-id="1a29d-1410">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1410">Yes</span></span>
<span data-ttu-id="1a29d-1411">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1411">password</span></span> | <span data-ttu-id="1a29d-1412">Contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1412">Password for the user.</span></span> | <span data-ttu-id="1a29d-1413">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1413">string</span></span> | <span data-ttu-id="1a29d-1414">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1414">Yes</span></span>
<span data-ttu-id="1a29d-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1415">gatewayName</span></span> | <span data-ttu-id="1a29d-1416">Nombre de la puerta de enlace que debe usar el servicio Data Factory para conectarse a la instancia de SAP BW local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="1a29d-1417">cadena</span><span class="sxs-lookup"><span data-stu-id="1a29d-1417">string</span></span> | <span data-ttu-id="1a29d-1418">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1418">Yes</span></span>
<span data-ttu-id="1a29d-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1419">encryptedCredential</span></span> | <span data-ttu-id="1a29d-1420">La cadena de credenciales cifrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1420">The encrypted credential string.</span></span> | <span data-ttu-id="1a29d-1421">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1421">string</span></span> | <span data-ttu-id="1a29d-1422">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-1423">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="1a29d-1424">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1425">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1425">Dataset</span></span>
<span data-ttu-id="1a29d-1426">Para definir un conjunto de datos de SAP BW, establezca el **tipo** de conjunto de datos en **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="1a29d-1427">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP BW de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="1a29d-1428">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="1a29d-1429">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1430">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1431">Si va a copiar datos desde SAP Business Warehouse, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1432">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1432">Property</span></span> | <span data-ttu-id="1a29d-1433">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1433">Description</span></span> | <span data-ttu-id="1a29d-1434">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1434">Allowed values</span></span> | <span data-ttu-id="1a29d-1435">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1436">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1436">query</span></span> | <span data-ttu-id="1a29d-1437">Especifica la consulta MDX para leer datos de la instancia de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="1a29d-1438">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1438">MDX query.</span></span> | <span data-ttu-id="1a29d-1439">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1440">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1441">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="1a29d-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a29d-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1443">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1443">Linked service</span></span>
<span data-ttu-id="1a29d-1444">Para definir un servicio vinculado de SAP HANA, establezca el **tipo** de servicio vinculado en **SapHana** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="1a29d-1445">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1445">Property</span></span> | <span data-ttu-id="1a29d-1446">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1446">Description</span></span> | <span data-ttu-id="1a29d-1447">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1447">Allowed values</span></span> | <span data-ttu-id="1a29d-1448">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1a29d-1449">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1449">server</span></span> | <span data-ttu-id="1a29d-1450">Nombre del servidor en el que reside la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="1a29d-1451">Si el servidor usa un puerto personalizado, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="1a29d-1452">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1452">string</span></span> | <span data-ttu-id="1a29d-1453">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1453">Yes</span></span>
<span data-ttu-id="1a29d-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1454">authenticationType</span></span> | <span data-ttu-id="1a29d-1455">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1455">Type of authentication.</span></span> | <span data-ttu-id="1a29d-1456">cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1456">string.</span></span> <span data-ttu-id="1a29d-1457">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="1a29d-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="1a29d-1458">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1458">Yes</span></span> 
<span data-ttu-id="1a29d-1459">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1459">username</span></span> | <span data-ttu-id="1a29d-1460">Nombre del usuario que tiene acceso al servidor SAP</span><span class="sxs-lookup"><span data-stu-id="1a29d-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="1a29d-1461">cadena</span><span class="sxs-lookup"><span data-stu-id="1a29d-1461">string</span></span> | <span data-ttu-id="1a29d-1462">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1462">Yes</span></span>
<span data-ttu-id="1a29d-1463">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1463">password</span></span> | <span data-ttu-id="1a29d-1464">Contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1464">Password for the user.</span></span> | <span data-ttu-id="1a29d-1465">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1465">string</span></span> | <span data-ttu-id="1a29d-1466">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1466">Yes</span></span>
<span data-ttu-id="1a29d-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1467">gatewayName</span></span> | <span data-ttu-id="1a29d-1468">Nombre de la puerta de enlace que debe usar el servicio Data Factory para conectarse a la instancia de SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="1a29d-1469">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1469">string</span></span> | <span data-ttu-id="1a29d-1470">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1470">Yes</span></span>
<span data-ttu-id="1a29d-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1471">encryptedCredential</span></span> | <span data-ttu-id="1a29d-1472">La cadena de credenciales cifrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1472">The encrypted credential string.</span></span> | <span data-ttu-id="1a29d-1473">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1473">string</span></span> | <span data-ttu-id="1a29d-1474">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-1475">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="1a29d-1476">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="1a29d-1477">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1477">Dataset</span></span>
<span data-ttu-id="1a29d-1478">Para definir un conjunto de datos de SAP HANA, establezca el **tipo** de conjunto de datos en **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="1a29d-1479">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="1a29d-1480">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="1a29d-1481">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1482">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1483">Si va a copiar datos desde un almacén de datos de SAP HANA, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1484">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1484">Property</span></span> | <span data-ttu-id="1a29d-1485">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1485">Description</span></span> | <span data-ttu-id="1a29d-1486">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1486">Allowed values</span></span> | <span data-ttu-id="1a29d-1487">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1488">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1488">query</span></span> | <span data-ttu-id="1a29d-1489">Especifica la consulta SQL para leer datos de la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="1a29d-1490">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1490">SQL query.</span></span> | <span data-ttu-id="1a29d-1491">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-1492">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1493">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="1a29d-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1495">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1495">Linked service</span></span>
<span data-ttu-id="1a29d-1496">Se crea un servicio vinculado de tipo **OnPremisesSqlServer** para vincular una base de datos SQL Server local a una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="1a29d-1497">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="1a29d-1498">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio SQL Server vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="1a29d-1499">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1499">Property</span></span> | <span data-ttu-id="1a29d-1500">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1500">Description</span></span> | <span data-ttu-id="1a29d-1501">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1502">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-1502">type</span></span> |<span data-ttu-id="1a29d-1503">La propiedad type se debe establecer en **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="1a29d-1504">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1504">Yes</span></span> |
| <span data-ttu-id="1a29d-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-1505">connectionString</span></span> |<span data-ttu-id="1a29d-1506">Especifique la información de connectionString necesaria para conectarse a la Base de datos SQL Server local mediante autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="1a29d-1507">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1507">Yes</span></span> |
| <span data-ttu-id="1a29d-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1508">gatewayName</span></span> |<span data-ttu-id="1a29d-1509">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la Base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="1a29d-1510">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1510">Yes</span></span> |
| <span data-ttu-id="1a29d-1511">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1511">username</span></span> |<span data-ttu-id="1a29d-1512">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="1a29d-1513">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="1a29d-1514">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1514">No</span></span> |
| <span data-ttu-id="1a29d-1515">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1515">password</span></span> |<span data-ttu-id="1a29d-1516">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-1517">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1517">No</span></span> |

<span data-ttu-id="1a29d-1518">Puede cifrar las credenciales con el cmdlet **New-AzureRmDataFactoryEncryptValue** y usarlas en la cadena de conexión, como se muestra en el ejemplo siguiente (propiedad **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="1a29d-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="1a29d-1519">Ejemplo: JSON para usar autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="1a29d-1520">Ejemplo: JSON para usar autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="1a29d-1521">Si se especifican el nombre de usuario y la contraseña, la puerta de enlace los usará para suplantar la cuenta de usuario especificada para conectarse a la Base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="1a29d-1522">En caso contrario, la puerta de enlace se conectará directamente a SQL Server con el contexto de seguridad de puerta de enlace (su cuenta de inicio).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="1a29d-1523">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1524">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1524">Dataset</span></span>
<span data-ttu-id="1a29d-1525">Para definir un conjunto de datos de SQL Server, establezca el **tipo** de conjunto de datos en **SqlServerTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1526">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1526">Property</span></span> | <span data-ttu-id="1a29d-1527">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1527">Description</span></span> | <span data-ttu-id="1a29d-1528">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1529">tableName</span></span> |<span data-ttu-id="1a29d-1530">Nombre de la tabla en la instancia de base de datos de SQL Server a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="1a29d-1531">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1532">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1533">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="1a29d-1534">Origen de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1535">Si va a copiar datos de una base de datos SQL Server, establezca el **tipo de origen** de la actividad de copia en **SqlSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1536">Property</span></span> | <span data-ttu-id="1a29d-1537">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1537">Description</span></span> | <span data-ttu-id="1a29d-1538">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1538">Allowed values</span></span> | <span data-ttu-id="1a29d-1539">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1a29d-1540">sqlReaderQuery</span></span> |<span data-ttu-id="1a29d-1541">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1542">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1542">SQL query string.</span></span> <span data-ttu-id="1a29d-1543">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="1a29d-1544">Es posible hacer referencia a varias tablas de la base de datos a la que hace referencia el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="1a29d-1545">Si no se especifica, la instrucción SQL que se ejecuta: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="1a29d-1546">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1546">No</span></span> |
| <span data-ttu-id="1a29d-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="1a29d-1548">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="1a29d-1549">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="1a29d-1550">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1550">No</span></span> |
| <span data-ttu-id="1a29d-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-1551">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-1552">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1a29d-1553">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1553">Name/value pairs.</span></span> <span data-ttu-id="1a29d-1554">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1a29d-1555">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1555">No</span></span> |

<span data-ttu-id="1a29d-1556">Si se especifica **sqlReaderQuery** para SqlSource, la actividad de copia ejecuta la consulta en el origen de Base de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="1a29d-1557">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="1a29d-1558">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura se usan para crear una consulta Select para ejecutarla en Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="1a29d-1559">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="1a29d-1560">Cuando use **sqlReaderStoredProcedureName**, necesitará especificar un valor para la propiedad **tableName** del conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="1a29d-1561">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="1a29d-1562">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1563">En este ejemplo, **sqlReaderQuery** se especifica para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="1a29d-1564">La actividad de copia ejecuta esta consulta en el origen de Base de datos de SQL Server para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="1a29d-1565">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="1a29d-1566">sqlReaderQuery puede hacer referencia a varias tablas de la base de datos a la que hace referencia el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="1a29d-1567">No se limita exclusivamente a la tabla establecida como typeProperty tableName del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="1a29d-1568">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura se usan para crear una consulta Select para ejecutarla en Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="1a29d-1569">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="1a29d-1570">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="1a29d-1571">Receptor de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-1572">Si va a copiar datos a una base de datos SQL Server, establezca el **tipo de receptor** de la actividad de copia en **SqlSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-1573">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1573">Property</span></span> | <span data-ttu-id="1a29d-1574">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1574">Description</span></span> | <span data-ttu-id="1a29d-1575">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1575">Allowed values</span></span> | <span data-ttu-id="1a29d-1576">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-1577">writeBatchTimeout</span></span> |<span data-ttu-id="1a29d-1578">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1a29d-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="1a29d-1579">timespan</span></span><br/><br/> <span data-ttu-id="1a29d-1580">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="1a29d-1581">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1581">No</span></span> |
| <span data-ttu-id="1a29d-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-1582">writeBatchSize</span></span> |<span data-ttu-id="1a29d-1583">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="1a29d-1584">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1584">Integer (number of rows)</span></span> |<span data-ttu-id="1a29d-1585">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="1a29d-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1a29d-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1a29d-1587">Especifique la consulta para que la actividad de copia se ejecute de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="1a29d-1588">Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="1a29d-1589">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1589">A query statement.</span></span> |<span data-ttu-id="1a29d-1590">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1590">No</span></span> |
| <span data-ttu-id="1a29d-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="1a29d-1592">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="1a29d-1593">Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="1a29d-1594">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="1a29d-1595">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1595">No</span></span> |
| <span data-ttu-id="1a29d-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="1a29d-1597">Nombre del procedimiento almacenado que actualiza e inserta (operación de upsert) datos en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="1a29d-1598">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="1a29d-1599">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1599">No</span></span> |
| <span data-ttu-id="1a29d-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-1600">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-1601">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="1a29d-1602">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1602">Name/value pairs.</span></span> <span data-ttu-id="1a29d-1603">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="1a29d-1604">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1604">No</span></span> |
| <span data-ttu-id="1a29d-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1605">sqlWriterTableType</span></span> |<span data-ttu-id="1a29d-1606">Especifique el nombre del tipo de tabla que se usará en el procedimiento almacenado anterior.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="1a29d-1607">La actividad de copia dispone que los datos que se mueven estén disponibles en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="1a29d-1608">El código de procedimiento almacenado puede combinar los datos copiados con datos existentes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="1a29d-1609">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1609">A table type name.</span></span> |<span data-ttu-id="1a29d-1610">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1611">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1611">Example</span></span>
<span data-ttu-id="1a29d-1612">La canalización contiene una actividad de copia que está configurada para usar estos conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1a29d-1613">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1614">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="1a29d-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="1a29d-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1616">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1616">Linked service</span></span>
<span data-ttu-id="1a29d-1617">Para definir un servicio vinculado de Sybase, establezca el **tipo** de servicio vinculado en **OnPremisesSybase** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1618">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1618">Property</span></span> | <span data-ttu-id="1a29d-1619">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1619">Description</span></span> | <span data-ttu-id="1a29d-1620">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1621">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1621">server</span></span> |<span data-ttu-id="1a29d-1622">Nombre del servidor de Sybase.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="1a29d-1623">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1623">Yes</span></span> |
| <span data-ttu-id="1a29d-1624">database</span><span class="sxs-lookup"><span data-stu-id="1a29d-1624">database</span></span> |<span data-ttu-id="1a29d-1625">Nombre de la base de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="1a29d-1626">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1626">Yes</span></span> |
| <span data-ttu-id="1a29d-1627">schema</span><span class="sxs-lookup"><span data-stu-id="1a29d-1627">schema</span></span> |<span data-ttu-id="1a29d-1628">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="1a29d-1629">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1629">No</span></span> |
| <span data-ttu-id="1a29d-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1630">authenticationType</span></span> |<span data-ttu-id="1a29d-1631">Tipo de autenticación usado para conectarse a la base de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="1a29d-1632">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1a29d-1633">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1633">Yes</span></span> |
| <span data-ttu-id="1a29d-1634">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1634">username</span></span> |<span data-ttu-id="1a29d-1635">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="1a29d-1636">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1636">No</span></span> |
| <span data-ttu-id="1a29d-1637">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1637">password</span></span> |<span data-ttu-id="1a29d-1638">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-1639">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1639">No</span></span> |
| <span data-ttu-id="1a29d-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1640">gatewayName</span></span> |<span data-ttu-id="1a29d-1641">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos de Sybase local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="1a29d-1642">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1643">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="1a29d-1644">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1645">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1645">Dataset</span></span>
<span data-ttu-id="1a29d-1646">Para definir un conjunto de datos de Sybase, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1647">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1647">Property</span></span> | <span data-ttu-id="1a29d-1648">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1648">Description</span></span> | <span data-ttu-id="1a29d-1649">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1650">tableName</span></span> |<span data-ttu-id="1a29d-1651">Nombre de la tabla en la instancia de Base de datos Sybase a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="1a29d-1652">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1653">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1654">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1655">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1656">Si va a copiar datos desde una base de datos de Sybase, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1657">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1657">Property</span></span> | <span data-ttu-id="1a29d-1658">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1658">Description</span></span> | <span data-ttu-id="1a29d-1659">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1659">Allowed values</span></span> | <span data-ttu-id="1a29d-1660">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1661">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1661">query</span></span> |<span data-ttu-id="1a29d-1662">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1663">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1663">SQL query string.</span></span> <span data-ttu-id="1a29d-1664">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-1665">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1666">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1667">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="1a29d-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="1a29d-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1669">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1669">Linked service</span></span>
<span data-ttu-id="1a29d-1670">Para definir un servicio vinculado de Teradata, establezca el **tipo** de servicio vinculado en **OnPremisesTeradata** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1671">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1671">Property</span></span> | <span data-ttu-id="1a29d-1672">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1672">Description</span></span> | <span data-ttu-id="1a29d-1673">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1674">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1674">server</span></span> |<span data-ttu-id="1a29d-1675">Nombre del servidor de Teradata.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="1a29d-1676">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1676">Yes</span></span> |
| <span data-ttu-id="1a29d-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1677">authenticationType</span></span> |<span data-ttu-id="1a29d-1678">Tipo de autenticación usado para conectarse a la base de datos Teradata.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="1a29d-1679">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1a29d-1680">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1680">Yes</span></span> |
| <span data-ttu-id="1a29d-1681">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1681">username</span></span> |<span data-ttu-id="1a29d-1682">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="1a29d-1683">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1683">No</span></span> |
| <span data-ttu-id="1a29d-1684">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1684">password</span></span> |<span data-ttu-id="1a29d-1685">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-1686">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1686">No</span></span> |
| <span data-ttu-id="1a29d-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1687">gatewayName</span></span> |<span data-ttu-id="1a29d-1688">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos Teradata local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="1a29d-1689">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1690">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="1a29d-1691">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1692">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1692">Dataset</span></span>
<span data-ttu-id="1a29d-1693">Para definir un conjunto de datos de blob de Teradata, establezca el **tipo** de conjunto de datos en **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="1a29d-1694">Actualmente, no hay ninguna propiedad de tipo compatible con el conjunto de datos de Teradata.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="1a29d-1695">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1696">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-1697">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1698">Si va a copiar datos desde una base de datos de Teradata, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1699">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1699">Property</span></span> | <span data-ttu-id="1a29d-1700">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1700">Description</span></span> | <span data-ttu-id="1a29d-1701">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1701">Allowed values</span></span> | <span data-ttu-id="1a29d-1702">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1703">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1703">query</span></span> |<span data-ttu-id="1a29d-1704">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1705">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1705">SQL query string.</span></span> <span data-ttu-id="1a29d-1706">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-1707">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1708">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="1a29d-1709">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="1a29d-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="1a29d-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-1711">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1711">Linked service</span></span>
<span data-ttu-id="1a29d-1712">Para definir un servicio vinculado de Cassandra, establezca el **tipo** de servicio vinculado en **OnPremisesCassandra** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1713">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1713">Property</span></span> | <span data-ttu-id="1a29d-1714">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1714">Description</span></span> | <span data-ttu-id="1a29d-1715">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1716">host</span><span class="sxs-lookup"><span data-stu-id="1a29d-1716">host</span></span> |<span data-ttu-id="1a29d-1717">Una o varias direcciones IP o nombres de host de los servidores de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="1a29d-1718">Especifica una lista de direcciones IP o nombres de host separada por comas para conectar con todos los servidores a la vez.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="1a29d-1719">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1719">Yes</span></span> |
| <span data-ttu-id="1a29d-1720">puerto</span><span class="sxs-lookup"><span data-stu-id="1a29d-1720">port</span></span> |<span data-ttu-id="1a29d-1721">Puerto TCP que el servidor de Cassandra utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="1a29d-1722">No. El valor predeterminado es 9042.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="1a29d-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1723">authenticationType</span></span> |<span data-ttu-id="1a29d-1724">Básica o anónima</span><span class="sxs-lookup"><span data-stu-id="1a29d-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="1a29d-1725">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1725">Yes</span></span> |
| <span data-ttu-id="1a29d-1726">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1726">username</span></span> |<span data-ttu-id="1a29d-1727">Especifique el nombre de usuario de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="1a29d-1728">Sí, si el valor de authenticationType es Basic.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="1a29d-1729">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1729">password</span></span> |<span data-ttu-id="1a29d-1730">Especifique la contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1730">Specify password for the user account.</span></span> |<span data-ttu-id="1a29d-1731">Sí, si el valor de authenticationType es Basic.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="1a29d-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1732">gatewayName</span></span> |<span data-ttu-id="1a29d-1733">Nombre de la puerta de enlace que se va a utilizar en la conexión con la base de datos de Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="1a29d-1734">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1734">Yes</span></span> |
| <span data-ttu-id="1a29d-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1735">encryptedCredential</span></span> |<span data-ttu-id="1a29d-1736">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="1a29d-1737">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1738">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-1739">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-1740">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1740">Dataset</span></span>
<span data-ttu-id="1a29d-1741">Para definir un conjunto de datos de Cassandra, establezca el **tipo** de conjunto de datos en **CassandraTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1742">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1742">Property</span></span> | <span data-ttu-id="1a29d-1743">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1743">Description</span></span> | <span data-ttu-id="1a29d-1744">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="1a29d-1745">keyspace</span></span> |<span data-ttu-id="1a29d-1746">Nombre del espacio de claves o esquema de la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="1a29d-1747">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="1a29d-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1748">tableName</span></span> |<span data-ttu-id="1a29d-1749">Nombre de la tabla de la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="1a29d-1750">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1751">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1752">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="1a29d-1753">Origen de Cassandra en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1754">Si va a copiar datos desde Cassandra, establezca el **tipo de origen** de la actividad de copia en **CassandraSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1755">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1755">Property</span></span> | <span data-ttu-id="1a29d-1756">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1756">Description</span></span> | <span data-ttu-id="1a29d-1757">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1757">Allowed values</span></span> | <span data-ttu-id="1a29d-1758">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1759">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1759">query</span></span> |<span data-ttu-id="1a29d-1760">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1761">Consulta SQL-92 o consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="1a29d-1762">Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="1a29d-1763">Cuando utilice una consulta SQL, especifique **nombre de espacio de claves.nombre de tabla** para representar la tabla que quiere consultar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="1a29d-1764">No (si tableName y el espacio de claves del conjunto de datos están definidos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="1a29d-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="1a29d-1765">consistencyLevel</span></span> |<span data-ttu-id="1a29d-1766">El nivel de coherencia establece el número de réplicas que deben responder a una solicitud de lectura antes de que se devuelvan datos a la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="1a29d-1767">Cassandra comprueba el número de réplicas especificado para que los datos satisfagan la solicitud de lectura.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="1a29d-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="1a29d-1769">Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="1a29d-1770">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1770">No.</span></span> <span data-ttu-id="1a29d-1771">El valor predeterminado es ONE.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1772">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-1773">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="1a29d-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="1a29d-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-1775">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1775">Linked service</span></span>
<span data-ttu-id="1a29d-1776">Para definir un servicio vinculado de MongoDB, establezca el **tipo** de servicio vinculado en **OnPremisesMongoDB** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1777">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1777">Property</span></span> | <span data-ttu-id="1a29d-1778">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1778">Description</span></span> | <span data-ttu-id="1a29d-1779">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1780">server</span><span class="sxs-lookup"><span data-stu-id="1a29d-1780">server</span></span> |<span data-ttu-id="1a29d-1781">Dirección IP o nombre de host del servidor de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="1a29d-1782">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1782">Yes</span></span> |
| <span data-ttu-id="1a29d-1783">puerto</span><span class="sxs-lookup"><span data-stu-id="1a29d-1783">port</span></span> |<span data-ttu-id="1a29d-1784">Puerto TCP que el servidor de MongoDB utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="1a29d-1785">Valor predeterminado opcional: 27017</span><span class="sxs-lookup"><span data-stu-id="1a29d-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="1a29d-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-1786">authenticationType</span></span> |<span data-ttu-id="1a29d-1787">Básica o anónima.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="1a29d-1788">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1788">Yes</span></span> |
| <span data-ttu-id="1a29d-1789">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1789">username</span></span> |<span data-ttu-id="1a29d-1790">Cuenta de usuario para tener acceso a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="1a29d-1791">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="1a29d-1792">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1792">password</span></span> |<span data-ttu-id="1a29d-1793">Contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1793">Password for the user.</span></span> |<span data-ttu-id="1a29d-1794">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="1a29d-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="1a29d-1795">authSource</span></span> |<span data-ttu-id="1a29d-1796">Nombre de la base de datos de MongoDB que desea usar para comprobar las credenciales de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="1a29d-1797">Opcional (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="1a29d-1798">Valor predeterminado: se utiliza la cuenta de administrador y la base de datos especificada mediante la propiedad databaseName.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="1a29d-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1799">databaseName</span></span> |<span data-ttu-id="1a29d-1800">Nombre de la base de datos de MongoDB a la que desea acceder.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="1a29d-1801">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1801">Yes</span></span> |
| <span data-ttu-id="1a29d-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1802">gatewayName</span></span> |<span data-ttu-id="1a29d-1803">Nombre de la puerta de enlace que accede al almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="1a29d-1804">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1804">Yes</span></span> |
| <span data-ttu-id="1a29d-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1805">encryptedCredential</span></span> |<span data-ttu-id="1a29d-1806">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="1a29d-1807">Opcional</span><span class="sxs-lookup"><span data-stu-id="1a29d-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1808">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-1809">Para obtener más información, vea el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1810">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1810">Dataset</span></span>
<span data-ttu-id="1a29d-1811">Para definir un conjunto de datos de MongoDB, establezca el **tipo** del conjunto de datos en **MongoDbCollection** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1812">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1812">Property</span></span> | <span data-ttu-id="1a29d-1813">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1813">Description</span></span> | <span data-ttu-id="1a29d-1814">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1815">collectionName</span></span> |<span data-ttu-id="1a29d-1816">Nombre de la colección en la base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="1a29d-1817">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1818">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="1a29d-1819">Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="1a29d-1820">Origen de MongoDB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1821">Si va a copiar datos desde MongoDB, establezca el **tipo de origen** de la actividad de copia en **MongoDbSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1822">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1822">Property</span></span> | <span data-ttu-id="1a29d-1823">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1823">Description</span></span> | <span data-ttu-id="1a29d-1824">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1824">Allowed values</span></span> | <span data-ttu-id="1a29d-1825">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1826">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-1826">query</span></span> |<span data-ttu-id="1a29d-1827">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-1828">Cadena de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1828">SQL-92 query string.</span></span> <span data-ttu-id="1a29d-1829">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-1830">No (si se especifica **collectionName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1831">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1832">Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="1a29d-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="1a29d-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-1834">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1834">Linked service</span></span>
<span data-ttu-id="1a29d-1835">Para definir un servicio vinculado de Amazon S3, establezca el **tipo** de servicio vinculado en **AwsAccessKey** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-1836">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1836">Property</span></span> | <span data-ttu-id="1a29d-1837">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1837">Description</span></span> | <span data-ttu-id="1a29d-1838">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1838">Allowed values</span></span> | <span data-ttu-id="1a29d-1839">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="1a29d-1840">accessKeyID</span></span> |<span data-ttu-id="1a29d-1841">Id. de la clave de acceso secreta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1841">ID of the secret access key.</span></span> |<span data-ttu-id="1a29d-1842">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1842">string</span></span> |<span data-ttu-id="1a29d-1843">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1843">Yes</span></span> |
| <span data-ttu-id="1a29d-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="1a29d-1844">secretAccessKey</span></span> |<span data-ttu-id="1a29d-1845">La propia clave de acceso secreta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1845">The secret access key itself.</span></span> |<span data-ttu-id="1a29d-1846">Cadena secreta cifrada</span><span class="sxs-lookup"><span data-stu-id="1a29d-1846">Encrypted secret string</span></span> |<span data-ttu-id="1a29d-1847">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-1848">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="1a29d-1849">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1850">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1850">Dataset</span></span>
<span data-ttu-id="1a29d-1851">Para definir un conjunto de datos de Amazon S3, establezca el **tipo** de conjunto de datos en **AmazonS3** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1852">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1852">Property</span></span> | <span data-ttu-id="1a29d-1853">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1853">Description</span></span> | <span data-ttu-id="1a29d-1854">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1854">Allowed values</span></span> | <span data-ttu-id="1a29d-1855">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1856">bucketName</span></span> |<span data-ttu-id="1a29d-1857">Nombre del depósito de S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1857">The S3 bucket name.</span></span> |<span data-ttu-id="1a29d-1858">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1858">String</span></span> |<span data-ttu-id="1a29d-1859">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1859">Yes</span></span> |
| <span data-ttu-id="1a29d-1860">key</span><span class="sxs-lookup"><span data-stu-id="1a29d-1860">key</span></span> |<span data-ttu-id="1a29d-1861">La clave del objeto S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1861">The S3 object key.</span></span> |<span data-ttu-id="1a29d-1862">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1862">String</span></span> |<span data-ttu-id="1a29d-1863">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1863">No</span></span> |
| <span data-ttu-id="1a29d-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="1a29d-1864">prefix</span></span> |<span data-ttu-id="1a29d-1865">Prefijo de la clave del objeto S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="1a29d-1866">Se seleccionan objetos cuyas claves comienzan por este prefijo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="1a29d-1867">Se aplica solo cuando la clave está vacía.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="1a29d-1868">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1868">String</span></span> |<span data-ttu-id="1a29d-1869">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1869">No</span></span> |
| <span data-ttu-id="1a29d-1870">versión</span><span class="sxs-lookup"><span data-stu-id="1a29d-1870">version</span></span> |<span data-ttu-id="1a29d-1871">La versión del objeto S3 si está habilitado el control de versiones de S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="1a29d-1872">string</span><span class="sxs-lookup"><span data-stu-id="1a29d-1872">String</span></span> |<span data-ttu-id="1a29d-1873">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1873">No</span></span> |
| <span data-ttu-id="1a29d-1874">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-1874">format</span></span> | <span data-ttu-id="1a29d-1875">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-1876">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-1877">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-1878">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-1879">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1879">No</span></span> | |
| <span data-ttu-id="1a29d-1880">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-1880">compression</span></span> | <span data-ttu-id="1a29d-1881">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-1882">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-1883">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-1884">Para más información, consulte [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de archivo y compresión en Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-1885">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="1a29d-1886">bucketName + key especifica la ubicación del objeto S3, donde bucket es el contenedor raíz de los objetos S3 y key es la ruta de acceso completa al objeto S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="1a29d-1887">Ejemplo: Conjunto de datos de ejemplo con prefijo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="1a29d-1888">Ejemplo: Conjunto de datos de ejemplo (con versión)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="1a29d-1889">Ejemplo: Rutas de acceso dinámicas para S3</span><span class="sxs-lookup"><span data-stu-id="1a29d-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="1a29d-1890">En el ejemplo, usamos valores fijos para las propiedades key y bucketName en el conjunto de datos de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="1a29d-1891">Puede hacer que Data Factory calcule estas propiedades dinámicamente en tiempo de ejecución mediante variables del sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="1a29d-1892">Y lo mismo puede hacer para la propiedad prefix de un conjunto de datos de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="1a29d-1893">Consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) para ver una lista de funciones y variables admitidas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="1a29d-1894">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="1a29d-1895">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1896">Si va a copiar datos desde Amazon S3, establezca el **tipo de origen** de la actividad de copia en **FileSystemSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="1a29d-1897">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1897">Property</span></span> | <span data-ttu-id="1a29d-1898">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1898">Description</span></span> | <span data-ttu-id="1a29d-1899">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1899">Allowed values</span></span> | <span data-ttu-id="1a29d-1900">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-1901">recursive</span></span> |<span data-ttu-id="1a29d-1902">Especifica si se mostrarán objetos S3 de manera recursiva en el directorio.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="1a29d-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="1a29d-1903">true/false</span></span> |<span data-ttu-id="1a29d-1904">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-1905">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-1906">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="1a29d-1907">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-1908">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1908">Linked service</span></span>
<span data-ttu-id="1a29d-1909">Un sistema de archivos local se puede vincular a una factoría de datos de Azure con el servicio vinculado del **servidor de archivos local**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="1a29d-1910">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado del servidor de archivos local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="1a29d-1911">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1911">Property</span></span> | <span data-ttu-id="1a29d-1912">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1912">Description</span></span> | <span data-ttu-id="1a29d-1913">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1914">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-1914">type</span></span> |<span data-ttu-id="1a29d-1915">Asegúrese de que la propiedad type esté establecida en **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="1a29d-1916">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1916">Yes</span></span> |
| <span data-ttu-id="1a29d-1917">host</span><span class="sxs-lookup"><span data-stu-id="1a29d-1917">host</span></span> |<span data-ttu-id="1a29d-1918">Especifica la ruta de acceso raíz de la carpeta que quiere copiar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="1a29d-1919">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1a29d-1920">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="1a29d-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="1a29d-1921">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1921">Yes</span></span> |
| <span data-ttu-id="1a29d-1922">userid</span><span class="sxs-lookup"><span data-stu-id="1a29d-1922">userid</span></span> |<span data-ttu-id="1a29d-1923">Especifique el identificador del usuario que tiene acceso al servidor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="1a29d-1924">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="1a29d-1925">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-1925">password</span></span> |<span data-ttu-id="1a29d-1926">Especifique la contraseña del usuario (identificador de usuario).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="1a29d-1927">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="1a29d-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1928">encryptedCredential</span></span> |<span data-ttu-id="1a29d-1929">Especifique las credenciales cifradas que puede obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="1a29d-1930">No (si opta por especificar el identificador de usuario y la contraseña en texto sin formato)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="1a29d-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1931">gatewayName</span></span> |<span data-ttu-id="1a29d-1932">Especifica el nombre de la puerta de enlace que debe usar Data Factory para conectarse al servidor de archivos local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="1a29d-1933">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="1a29d-1934">Definiciones de ruta de acceso a la carpeta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="1a29d-1935">Escenario</span><span class="sxs-lookup"><span data-stu-id="1a29d-1935">Scenario</span></span> | <span data-ttu-id="1a29d-1936">Host en definición de servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-1936">Host in linked service definition</span></span> | <span data-ttu-id="1a29d-1937">folderPath en definición de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1938">Carpeta local en la máquina de Data Management Gateway:: </span><span class="sxs-lookup"><span data-stu-id="1a29d-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="1a29d-1939">Ejemplos: D:\\\* o D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="1a29d-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="1a29d-1940">D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="1a29d-1941">localhost (para versiones anteriores a Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="1a29d-1942">\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="1a29d-1943">D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="1a29d-1944">Carpeta compartida remota: </span><span class="sxs-lookup"><span data-stu-id="1a29d-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="1a29d-1945">Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="1a29d-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="1a29d-1946">\\\\\\\\myserver\\\\</span><span class="sxs-lookup"><span data-stu-id="1a29d-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="1a29d-1947">.\\\\ o carpeta\\\\subcarpeta</span><span class="sxs-lookup"><span data-stu-id="1a29d-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="1a29d-1948">Ejemplo: uso de nombre de usuario y contraseña en texto sin formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="1a29d-1949">Ejemplo: uso de encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-1950">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-1951">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-1951">Dataset</span></span>
<span data-ttu-id="1a29d-1952">Para definir un conjunto de datos del sistema de archivos, establezca el **tipo** de conjunto de datos en **FileShare** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-1953">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1953">Property</span></span> | <span data-ttu-id="1a29d-1954">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1954">Description</span></span> | <span data-ttu-id="1a29d-1955">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-1956">folderPath</span></span> |<span data-ttu-id="1a29d-1957">Especifica la subruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="1a29d-1958">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="1a29d-1959">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="1a29d-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1a29d-1960">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1a29d-1961">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-1961">Yes</span></span> |
| <span data-ttu-id="1a29d-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-1962">fileName</span></span> |<span data-ttu-id="1a29d-1963">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1a29d-1964">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1a29d-1965">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo generado está en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="1a29d-1966">`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="1a29d-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="1a29d-1967">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1967">No</span></span> |
| <span data-ttu-id="1a29d-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1a29d-1968">fileFilter</span></span> |<span data-ttu-id="1a29d-1969">Especifique el filtro que se va a usar para seleccionar un subconjunto de archivos de folderPath, en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="1a29d-1970">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1a29d-1971">Ejemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="1a29d-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="1a29d-1972">Ejemplo 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="1a29d-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="1a29d-1973">Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="1a29d-1974">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1974">No</span></span> |
| <span data-ttu-id="1a29d-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-1975">partitionedBy</span></span> |<span data-ttu-id="1a29d-1976">Puede usar partitionedBy para especificar un valor dinámico de folderPath/fileName para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="1a29d-1977">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-1978">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1978">No</span></span> |
| <span data-ttu-id="1a29d-1979">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-1979">format</span></span> | <span data-ttu-id="1a29d-1980">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-1981">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-1982">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-1983">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-1984">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1984">No</span></span> |
| <span data-ttu-id="1a29d-1985">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-1985">compression</span></span> | <span data-ttu-id="1a29d-1986">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-1987">Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-1988">consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-1989">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1a29d-1990">No se puede usar fileName y fileFilter a la vez.</span><span class="sxs-lookup"><span data-stu-id="1a29d-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-1991">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-1992">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="1a29d-1993">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-1994">Si va a copiar datos desde el sistema de archivos, establezca el **tipo de origen** de la actividad de copia en **FileSystemSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-1995">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-1995">Property</span></span> | <span data-ttu-id="1a29d-1996">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-1996">Description</span></span> | <span data-ttu-id="1a29d-1997">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-1997">Allowed values</span></span> | <span data-ttu-id="1a29d-1998">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-1999">recursive</span></span> |<span data-ttu-id="1a29d-2000">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-2001">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2001">True, False (default)</span></span> |<span data-ttu-id="1a29d-2002">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2003">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="1a29d-2004">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="1a29d-2005">Receptor de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="1a29d-2006">Si va a copiar datos al sistema de archivos, establezca el **tipo de receptor** de la actividad de copia en **FileSystemSink** y especifique las siguientes propiedades en la sección **receptor**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="1a29d-2007">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2007">Property</span></span> | <span data-ttu-id="1a29d-2008">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2008">Description</span></span> | <span data-ttu-id="1a29d-2009">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2009">Allowed values</span></span> | <span data-ttu-id="1a29d-2010">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1a29d-2011">copyBehavior</span></span> |<span data-ttu-id="1a29d-2012">Define el comportamiento de copia cuando el origen es BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="1a29d-2013">**PreserveHierarchy:**: conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="1a29d-2014">Es decir, la ruta de acceso relativa del archivo de origen a la carpeta de origen es la misma que la ruta de acceso relativa del archivo de destino a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="1a29d-2015">**FlattenHierarchy:** todos los archivos de la carpeta de origen se crean en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="1a29d-2016">Los archivos de destino se crean con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="1a29d-2017">**MergeFiles**: combina todos los archivos de la carpeta de origen en un archivo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="1a29d-2018">Si se especifica el nombre o el nombre del blob, el nombre de archivo combinado es el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="1a29d-2019">De lo contrario, es un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="1a29d-2020">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2020">No</span></span> |
<span data-ttu-id="1a29d-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="1a29d-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-2022">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-2023">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="1a29d-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-2025">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2025">Linked service</span></span>
<span data-ttu-id="1a29d-2026">Para definir un servicio vinculado de FTP, establezca el **tipo** de servicio vinculado en **FtpServer** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2027">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2027">Property</span></span> | <span data-ttu-id="1a29d-2028">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2028">Description</span></span> | <span data-ttu-id="1a29d-2029">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2029">Required</span></span> | <span data-ttu-id="1a29d-2030">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2031">host</span><span class="sxs-lookup"><span data-stu-id="1a29d-2031">host</span></span> |<span data-ttu-id="1a29d-2032">Nombre o dirección IP del servidor FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="1a29d-2033">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="1a29d-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2034">authenticationType</span></span> |<span data-ttu-id="1a29d-2035">Especificar el tipo de autenticación</span><span class="sxs-lookup"><span data-stu-id="1a29d-2035">Specify authentication type</span></span> |<span data-ttu-id="1a29d-2036">yes</span><span class="sxs-lookup"><span data-stu-id="1a29d-2036">Yes</span></span> |<span data-ttu-id="1a29d-2037">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="1a29d-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="1a29d-2038">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2038">username</span></span> |<span data-ttu-id="1a29d-2039">Usuario que tiene acceso al servidor FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="1a29d-2040">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="1a29d-2041">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2041">password</span></span> |<span data-ttu-id="1a29d-2042">Contraseña para el usuario (nombre de usuario)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2042">Password for the user (username)</span></span> |<span data-ttu-id="1a29d-2043">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="1a29d-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2044">encryptedCredential</span></span> |<span data-ttu-id="1a29d-2045">Credenciales cifradas para acceder al servidor FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="1a29d-2046">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="1a29d-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2047">gatewayName</span></span> |<span data-ttu-id="1a29d-2048">Nombre de la puerta de enlace de administración de datos para conectarse a un servidor FTP local</span><span class="sxs-lookup"><span data-stu-id="1a29d-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="1a29d-2049">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="1a29d-2050">puerto</span><span class="sxs-lookup"><span data-stu-id="1a29d-2050">port</span></span> |<span data-ttu-id="1a29d-2051">Puerto en el que escucha el servidor FTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="1a29d-2052">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2052">No</span></span> |<span data-ttu-id="1a29d-2053">21</span><span class="sxs-lookup"><span data-stu-id="1a29d-2053">21</span></span> |
| <span data-ttu-id="1a29d-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="1a29d-2054">enableSsl</span></span> |<span data-ttu-id="1a29d-2055">Especificar si desea usar FTP a través del canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="1a29d-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="1a29d-2056">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2056">No</span></span> |<span data-ttu-id="1a29d-2057">true</span><span class="sxs-lookup"><span data-stu-id="1a29d-2057">true</span></span> |
| <span data-ttu-id="1a29d-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1a29d-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="1a29d-2059">Especificar si desea habilitar la validación de certificados de servidor SSL al usar FTP sobre el canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="1a29d-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="1a29d-2060">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2060">No</span></span> |<span data-ttu-id="1a29d-2061">true</span><span class="sxs-lookup"><span data-stu-id="1a29d-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="1a29d-2062">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="1a29d-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="1a29d-2063">Ejemplo: Uso de nombre de usuario y contraseña en texto sin formato para la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1a29d-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="1a29d-2064">Ejemplo: Uso de puerto, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1a29d-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="1a29d-2065">Ejemplo: Uso de encryptedCredential para la autenticación y la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="1a29d-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="1a29d-2066">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-2067">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2067">Dataset</span></span>
<span data-ttu-id="1a29d-2068">Para definir un conjunto de datos de FTP, establezca el **tipo** de conjunto de datos en **FileShare** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2069">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2069">Property</span></span> | <span data-ttu-id="1a29d-2070">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2070">Description</span></span> | <span data-ttu-id="1a29d-2071">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-2072">folderPath</span></span> |<span data-ttu-id="1a29d-2073">Subruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2073">Sub path to the folder.</span></span> <span data-ttu-id="1a29d-2074">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1a29d-2075">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="1a29d-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1a29d-2076">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1a29d-2077">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2077">Yes</span></span> 
| <span data-ttu-id="1a29d-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2078">fileName</span></span> |<span data-ttu-id="1a29d-2079">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1a29d-2080">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1a29d-2081">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo generado estaría en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="1a29d-2082">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1a29d-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1a29d-2083">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2083">No</span></span> |
| <span data-ttu-id="1a29d-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1a29d-2084">fileFilter</span></span> |<span data-ttu-id="1a29d-2085">Especifique el filtro que se va a usar para seleccionar un subconjunto de archivos de folderPath, en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="1a29d-2086">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1a29d-2087">Ejemplos 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="1a29d-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="1a29d-2088">Ejemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="1a29d-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="1a29d-2089">fileFilter es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="1a29d-2090">Esta propiedad no es compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="1a29d-2091">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2091">No</span></span> |
| <span data-ttu-id="1a29d-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-2092">partitionedBy</span></span> |<span data-ttu-id="1a29d-2093">partitionedBy se puede usar para especificar un valor de folderPath dinámico, un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="1a29d-2094">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-2095">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2095">No</span></span> |
| <span data-ttu-id="1a29d-2096">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-2096">format</span></span> | <span data-ttu-id="1a29d-2097">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-2098">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-2099">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-2100">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-2101">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2101">No</span></span> |
| <span data-ttu-id="1a29d-2102">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-2102">compression</span></span> | <span data-ttu-id="1a29d-2103">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-2104">Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-2105">Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-2106">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2106">No</span></span> |
| <span data-ttu-id="1a29d-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="1a29d-2107">useBinaryTransfer</span></span> |<span data-ttu-id="1a29d-2108">Especifica si se usará el modo de transferencia binario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="1a29d-2109">Su valor es true para el modo binario y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="1a29d-2110">Valor predeterminado: true.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2110">Default value: True.</span></span> <span data-ttu-id="1a29d-2111">Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="1a29d-2112">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1a29d-2113">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-2114">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1a29d-2115">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="1a29d-2116">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2117">Si va a copiar datos desde un servidor FTP, establezca el **tipo de origen** de la actividad de copia en **FileSystemSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2118">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2118">Property</span></span> | <span data-ttu-id="1a29d-2119">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2119">Description</span></span> | <span data-ttu-id="1a29d-2120">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2120">Allowed values</span></span> | <span data-ttu-id="1a29d-2121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-2122">recursive</span></span> |<span data-ttu-id="1a29d-2123">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-2124">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2124">True, False (default)</span></span> |<span data-ttu-id="1a29d-2125">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2126">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-2127">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="1a29d-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="1a29d-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-2129">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2129">Linked service</span></span>
<span data-ttu-id="1a29d-2130">Para definir un servicio vinculado de HDFS, establezca el **tipo** de servicio vinculado en **Hdfs** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2131">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2131">Property</span></span> | <span data-ttu-id="1a29d-2132">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2132">Description</span></span> | <span data-ttu-id="1a29d-2133">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2134">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2134">type</span></span> |<span data-ttu-id="1a29d-2135">La propiedad type debe establecerse en: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="1a29d-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="1a29d-2136">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2136">Yes</span></span> |
| <span data-ttu-id="1a29d-2137">URL</span><span class="sxs-lookup"><span data-stu-id="1a29d-2137">Url</span></span> |<span data-ttu-id="1a29d-2138">Dirección URL a HDFS</span><span class="sxs-lookup"><span data-stu-id="1a29d-2138">URL to the HDFS</span></span> |<span data-ttu-id="1a29d-2139">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2139">Yes</span></span> |
| <span data-ttu-id="1a29d-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2140">authenticationType</span></span> |<span data-ttu-id="1a29d-2141">Anónima o Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="1a29d-2142">Para usar la **autenticación Kerberos** para el conector HDFS, consulte [esta sección](#use-kerberos-authentication-for-hdfs-connector) a fin de configurar el entorno local en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="1a29d-2143">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2143">Yes</span></span> |
| <span data-ttu-id="1a29d-2144">userName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2144">userName</span></span> |<span data-ttu-id="1a29d-2145">Nombre de usuario para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="1a29d-2146">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="1a29d-2147">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2147">password</span></span> |<span data-ttu-id="1a29d-2148">Contraseña para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="1a29d-2149">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="1a29d-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2150">gatewayName</span></span> |<span data-ttu-id="1a29d-2151">Nombre de la puerta de enlace que el servicio Factoría de datos debe usar para conectarse a HDFS.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="1a29d-2152">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2152">Yes</span></span> |
| <span data-ttu-id="1a29d-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2153">encryptedCredential</span></span> |<span data-ttu-id="1a29d-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) de la credencial de acceso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="1a29d-2155">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="1a29d-2156">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="1a29d-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="1a29d-2157">Ejemplo: Uso de autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-2158">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-2159">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2159">Dataset</span></span>
<span data-ttu-id="1a29d-2160">Para definir un conjunto de datos de HDFS, establezca el **tipo** de conjunto de datos en **FileShare** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2161">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2161">Property</span></span> | <span data-ttu-id="1a29d-2162">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2162">Description</span></span> | <span data-ttu-id="1a29d-2163">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-2164">folderPath</span></span> |<span data-ttu-id="1a29d-2165">Ruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2165">Path to the folder.</span></span> <span data-ttu-id="1a29d-2166">Ejemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="1a29d-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="1a29d-2167">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1a29d-2168">Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="1a29d-2169">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1a29d-2170">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2170">Yes</span></span> |
| <span data-ttu-id="1a29d-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2171">fileName</span></span> |<span data-ttu-id="1a29d-2172">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1a29d-2173">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1a29d-2174">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo generado estaría en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="1a29d-2175">Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1a29d-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1a29d-2176">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2176">No</span></span> |
| <span data-ttu-id="1a29d-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-2177">partitionedBy</span></span> |<span data-ttu-id="1a29d-2178">partitionedBy se puede usar para especificar un valor de folderPath dinámico, un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="1a29d-2179">Por ejemplo, folderPath se parametriza para cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-2180">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2180">No</span></span> |
| <span data-ttu-id="1a29d-2181">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-2181">format</span></span> | <span data-ttu-id="1a29d-2182">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-2183">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-2184">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-2185">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-2186">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2186">No</span></span> |
| <span data-ttu-id="1a29d-2187">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-2187">compression</span></span> | <span data-ttu-id="1a29d-2188">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-2189">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-2190">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-2191">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-2192">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1a29d-2193">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-2194">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1a29d-2195">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="1a29d-2196">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2197">Si va a copiar datos desde HDFS, establezca el **tipo de origen** de la actividad de copia en **FileSystemSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="1a29d-2198">**FileSystemSource** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="1a29d-2199">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2199">Property</span></span> | <span data-ttu-id="1a29d-2200">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2200">Description</span></span> | <span data-ttu-id="1a29d-2201">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2201">Allowed values</span></span> | <span data-ttu-id="1a29d-2202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-2203">recursive</span></span> |<span data-ttu-id="1a29d-2204">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-2205">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2205">True, False (default)</span></span> |<span data-ttu-id="1a29d-2206">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2207">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-2208">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="1a29d-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-2210">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2210">Linked service</span></span>
<span data-ttu-id="1a29d-2211">Para definir un servicio vinculado de SFTP, establezca el **tipo** de servicio vinculado en **Sftp** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2212">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2212">Property</span></span> | <span data-ttu-id="1a29d-2213">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2213">Description</span></span> | <span data-ttu-id="1a29d-2214">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2215">host</span><span class="sxs-lookup"><span data-stu-id="1a29d-2215">host</span></span> | <span data-ttu-id="1a29d-2216">Nombre o dirección IP del servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="1a29d-2217">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2217">Yes</span></span> |
| <span data-ttu-id="1a29d-2218">puerto</span><span class="sxs-lookup"><span data-stu-id="1a29d-2218">port</span></span> |<span data-ttu-id="1a29d-2219">Puerto en el que escucha el servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="1a29d-2220">El valor predeterminado es 21.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2220">The default value is: 21</span></span> |<span data-ttu-id="1a29d-2221">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2221">No</span></span> |
| <span data-ttu-id="1a29d-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2222">authenticationType</span></span> |<span data-ttu-id="1a29d-2223">Especifique el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2223">Specify authentication type.</span></span> <span data-ttu-id="1a29d-2224">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="1a29d-2225">Consulte las secciones [Uso de autenticación básica](#using-basic-authentication) y [Uso de autenticación de clave pública SSH](#using-ssh-public-key-authentication) sobre más propiedades y ejemplos JSON respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="1a29d-2226">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2226">Yes</span></span> |
| <span data-ttu-id="1a29d-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="1a29d-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="1a29d-2228">Especifique si desea omitir la validación de claves de host.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="1a29d-2229">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2229">No.</span></span> <span data-ttu-id="1a29d-2230">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2230">The default value: false</span></span> |
| <span data-ttu-id="1a29d-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="1a29d-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="1a29d-2232">Especifique la huella dactilar de la clave de host.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="1a29d-2233">Sí, si `skipHostKeyValidation` está establecido en false.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="1a29d-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2234">gatewayName</span></span> |<span data-ttu-id="1a29d-2235">Nombre de la puerta de enlace de administración de datos para conectarse a un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="1a29d-2236">Sí, si va a copiar datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="1a29d-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2237">encryptedCredential</span></span> | <span data-ttu-id="1a29d-2238">Credenciales cifradas para acceder al servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="1a29d-2239">Se generan automáticamente cuando se especifica la autenticación básica (nombre de usuario + contraseña) o la autenticación SshPublicKey (nombre de usuario + ruta de acceso o contenido de la clave privada) en el Asistente para copiar o el cuadro de diálogo emergente ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="1a29d-2240">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2240">No.</span></span> <span data-ttu-id="1a29d-2241">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="1a29d-2242">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1a29d-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="1a29d-2243">Para usar la autenticación básica, establezca `authenticationType` como `Basic`, y especifique las siguientes propiedades además de las genéricas del conector SFTP descritas en la última sección:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="1a29d-2244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2244">Property</span></span> | <span data-ttu-id="1a29d-2245">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2245">Description</span></span> | <span data-ttu-id="1a29d-2246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2247">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2247">username</span></span> | <span data-ttu-id="1a29d-2248">Usuario que tiene acceso al servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="1a29d-2249">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2249">Yes</span></span> |
| <span data-ttu-id="1a29d-2250">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2250">password</span></span> | <span data-ttu-id="1a29d-2251">Contraseña para el usuario (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2251">Password for the user (username).</span></span> | <span data-ttu-id="1a29d-2252">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="1a29d-2253">Ejemplo: Autenticación básica con credenciales cifradas**</span><span class="sxs-lookup"><span data-stu-id="1a29d-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="1a29d-2254">Uso de autenticación de clave pública SSH:**</span><span class="sxs-lookup"><span data-stu-id="1a29d-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="1a29d-2255">Para usar la autenticación básica, establezca `authenticationType` como `SshPublicKey`, y especifique las siguientes propiedades además de las genéricas del conector SFTP descritas en la última sección:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="1a29d-2256">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2256">Property</span></span> | <span data-ttu-id="1a29d-2257">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2257">Description</span></span> | <span data-ttu-id="1a29d-2258">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2259">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2259">username</span></span> |<span data-ttu-id="1a29d-2260">Usuario que tiene acceso al servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="1a29d-2261">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2261">Yes</span></span> |
| <span data-ttu-id="1a29d-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-2262">privateKeyPath</span></span> | <span data-ttu-id="1a29d-2263">Especifique una ruta de acceso absoluta al archivo de clave privada al que pueda acceder la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="1a29d-2264">Especifique `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="1a29d-2265">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="1a29d-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="1a29d-2266">privateKeyContent</span></span> | <span data-ttu-id="1a29d-2267">Una cadena serializada del contenido de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="1a29d-2268">El Asistente para copiar puede leer el archivo de clave privada y extraer automáticamente el contenido de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="1a29d-2269">Si va a usar cualquier otra herramienta o SDK, utilice en su lugar la propiedad privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="1a29d-2270">Especifique `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="1a29d-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="1a29d-2271">passPhrase</span></span> | <span data-ttu-id="1a29d-2272">Especifique la contraseña o la frase de contraseña para descifrar la clave privada si el archivo de clave está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="1a29d-2273">Sí, si el archivo de clave privada está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="1a29d-2274">Ejemplo: Autenticación de SshPublicKey mediante contenido de clave privada**</span><span class="sxs-lookup"><span data-stu-id="1a29d-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="1a29d-2275">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-2276">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2276">Dataset</span></span>
<span data-ttu-id="1a29d-2277">Para definir un conjunto de datos de SFTP, establezca el **tipo** de conjunto de datos en **FileShare** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2278">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2278">Property</span></span> | <span data-ttu-id="1a29d-2279">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2279">Description</span></span> | <span data-ttu-id="1a29d-2280">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-2281">folderPath</span></span> |<span data-ttu-id="1a29d-2282">Subruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2282">Sub path to the folder.</span></span> <span data-ttu-id="1a29d-2283">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1a29d-2284">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="1a29d-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1a29d-2285">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1a29d-2286">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2286">Yes</span></span> |
| <span data-ttu-id="1a29d-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2287">fileName</span></span> |<span data-ttu-id="1a29d-2288">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1a29d-2289">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1a29d-2290">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo generado estaría en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="1a29d-2291">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1a29d-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1a29d-2292">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2292">No</span></span> |
| <span data-ttu-id="1a29d-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1a29d-2293">fileFilter</span></span> |<span data-ttu-id="1a29d-2294">Especifique el filtro que se va a usar para seleccionar un subconjunto de archivos de folderPath, en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="1a29d-2295">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1a29d-2296">Ejemplos 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="1a29d-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="1a29d-2297">Ejemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="1a29d-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="1a29d-2298">fileFilter es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="1a29d-2299">Esta propiedad no es compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="1a29d-2300">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2300">No</span></span> |
| <span data-ttu-id="1a29d-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1a29d-2301">partitionedBy</span></span> |<span data-ttu-id="1a29d-2302">partitionedBy se puede usar para especificar un valor de folderPath dinámico, un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="1a29d-2303">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1a29d-2304">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2304">No</span></span> |
| <span data-ttu-id="1a29d-2305">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-2305">format</span></span> | <span data-ttu-id="1a29d-2306">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-2307">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1a29d-2308">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1a29d-2309">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1a29d-2310">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2310">No</span></span> |
| <span data-ttu-id="1a29d-2311">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-2311">compression</span></span> | <span data-ttu-id="1a29d-2312">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-2313">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-2314">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-2315">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-2316">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2316">No</span></span> |
| <span data-ttu-id="1a29d-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="1a29d-2317">useBinaryTransfer</span></span> |<span data-ttu-id="1a29d-2318">Especifica si se usará el modo de transferencia binario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="1a29d-2319">Su valor es true para el modo binario y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="1a29d-2320">Valor predeterminado: true.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2320">Default value: True.</span></span> <span data-ttu-id="1a29d-2321">Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="1a29d-2322">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1a29d-2323">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-2324">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1a29d-2325">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="1a29d-2326">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2327">Si va a copiar datos desde un origen SFTP, establezca el **tipo de origen** de la actividad de copia en **FileSystemSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2328">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2328">Property</span></span> | <span data-ttu-id="1a29d-2329">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2329">Description</span></span> | <span data-ttu-id="1a29d-2330">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2330">Allowed values</span></span> | <span data-ttu-id="1a29d-2331">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="1a29d-2332">recursive</span></span> |<span data-ttu-id="1a29d-2333">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="1a29d-2334">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2334">True, False (default)</span></span> |<span data-ttu-id="1a29d-2335">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="1a29d-2336">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-2337">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="1a29d-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="1a29d-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-2339">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2339">Linked service</span></span>
<span data-ttu-id="1a29d-2340">Para definir un servicio vinculado de HTTP, establezca el **tipo** de servicio vinculado en **Http** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2341">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2341">Property</span></span> | <span data-ttu-id="1a29d-2342">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2342">Description</span></span> | <span data-ttu-id="1a29d-2343">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2344">URL</span><span class="sxs-lookup"><span data-stu-id="1a29d-2344">url</span></span> | <span data-ttu-id="1a29d-2345">Dirección URL base para el servidor web</span><span class="sxs-lookup"><span data-stu-id="1a29d-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="1a29d-2346">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2346">Yes</span></span> |
| <span data-ttu-id="1a29d-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2347">authenticationType</span></span> | <span data-ttu-id="1a29d-2348">Especifica el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2348">Specifies the authentication type.</span></span> <span data-ttu-id="1a29d-2349">Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="1a29d-2350">Consulte en las secciones después de esta tabla más propiedades y ejemplos de JSON para esos tipos de autenticación respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="1a29d-2351">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2351">Yes</span></span> |
| <span data-ttu-id="1a29d-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1a29d-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="1a29d-2353">Especifique si desea habilitar la validación del certificado SSL de servidor si el origen es el servidor web HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="1a29d-2354">No, el valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2354">No, default is true</span></span> |
| <span data-ttu-id="1a29d-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2355">gatewayName</span></span> | <span data-ttu-id="1a29d-2356">Nombre de la instancia de Data Management Gateway para conectarse a un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="1a29d-2357">Sí si va a copiar datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="1a29d-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2358">encryptedCredential</span></span> | <span data-ttu-id="1a29d-2359">Credenciales cifradas para acceder al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="1a29d-2360">Generadas automáticamente cuando se configura la información de autenticación en el Asistente para copia o en el cuadro de diálogo emergente de ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="1a29d-2361">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2361">No.</span></span> <span data-ttu-id="1a29d-2362">Se aplica solo cuando se copian datos desde un servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="1a29d-2363">Ejemplo: Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="1a29d-2364">Establezca `authenticationType` como `Basic`, `Digest` o `Windows`, y especifique las siguientes propiedades además de las genéricas del conector HTTP descritas antes:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="1a29d-2365">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2365">Property</span></span> | <span data-ttu-id="1a29d-2366">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2366">Description</span></span> | <span data-ttu-id="1a29d-2367">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2368">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2368">username</span></span> | <span data-ttu-id="1a29d-2369">Nombre de usuario para acceder al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="1a29d-2370">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2370">Yes</span></span> |
| <span data-ttu-id="1a29d-2371">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2371">password</span></span> | <span data-ttu-id="1a29d-2372">Contraseña para el usuario (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2372">Password for the user (username).</span></span> | <span data-ttu-id="1a29d-2373">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="1a29d-2374">Ejemplo: Uso de la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1a29d-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="1a29d-2375">Para usar la autenticación básica, establezca `authenticationType` como `ClientCertificate`, y especifique las siguientes propiedades además de las genéricas del conector HTTP descritas antes:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="1a29d-2376">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2376">Property</span></span> | <span data-ttu-id="1a29d-2377">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2377">Description</span></span> | <span data-ttu-id="1a29d-2378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="1a29d-2379">embeddedCertData</span></span> | <span data-ttu-id="1a29d-2380">El contenido con codificación Base64 de datos binarios del archivo de intercambio de información personal (PFX).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="1a29d-2381">Especifique `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="1a29d-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="1a29d-2382">certThumbprint</span></span> | <span data-ttu-id="1a29d-2383">La huella digital del certificado que se instaló en el almacén de certificados de la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="1a29d-2384">Se aplica solo cuando se copian datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="1a29d-2385">Especifique `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="1a29d-2386">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2386">password</span></span> | <span data-ttu-id="1a29d-2387">Contraseña asociada con el certificado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="1a29d-2388">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2388">No</span></span> |

<span data-ttu-id="1a29d-2389">Si utiliza `certThumbprint` para la autenticación y el certificado está instalado en el almacén personal del equipo local, necesita conceder el permiso de lectura al servicio de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="1a29d-2390">Inicie Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="1a29d-2391">Agregue el complemento **Certificados** que tenga como destino **Equipo local**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="1a29d-2392">Expanda **Certificados**, **Personal** y haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="1a29d-2393">Haga clic con el botón derecho en el certificado del almacén personal y seleccione **Todas las tareas**->**Administrar claves privadas**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="1a29d-2394">En la pestaña **Seguridad**, agregue la cuenta de usuario en que se ejecuta el servicio de host de Data Management Gateway con acceso de lectura al certificado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="1a29d-2395">**Ejemplo: Uso del certificado de cliente:** Este servicio vinculado vincula la instancia de Data Factory a un servidor de web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="1a29d-2396">Utiliza un certificado de cliente que está instalado en la máquina con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="1a29d-2397">Ejemplo: Uso del certificado de cliente en un archivo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="1a29d-2398">Este servicio vinculado vincula su factoría de datos a un servidor de web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="1a29d-2399">Utiliza un archivo de certificado de cliente en la máquina con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="1a29d-2400">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-2401">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2401">Dataset</span></span>
<span data-ttu-id="1a29d-2402">Para definir un conjunto de datos de HTTP, establezca el **tipo** de conjunto de datos en **Http** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2403">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2403">Property</span></span> | <span data-ttu-id="1a29d-2404">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2404">Description</span></span> | <span data-ttu-id="1a29d-2405">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="1a29d-2406">relativeUrl</span></span> | <span data-ttu-id="1a29d-2407">Dirección URL relativa al recurso que contiene los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="1a29d-2408">Cuando no se especifica la ruta de acceso, se solo se usa la dirección URL especificada en la definición de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="1a29d-2409">Para construir la dirección URL dinámica, puede usar [funciones de Data Factory y variables del sistema](data-factory-functions-variables.md); por ejemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="1a29d-2410">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2410">No</span></span> |
| <span data-ttu-id="1a29d-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="1a29d-2411">requestMethod</span></span> | <span data-ttu-id="1a29d-2412">Método HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2412">Http method.</span></span> <span data-ttu-id="1a29d-2413">Los valores permitidos son **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="1a29d-2414">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2414">No.</span></span> <span data-ttu-id="1a29d-2415">El valor predeterminado es `GET`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="1a29d-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="1a29d-2416">additionalHeaders</span></span> | <span data-ttu-id="1a29d-2417">Encabezados de solicitud HTTP adicionales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="1a29d-2418">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2418">No</span></span> |
| <span data-ttu-id="1a29d-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="1a29d-2419">requestBody</span></span> | <span data-ttu-id="1a29d-2420">Cuerpo de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2420">Body for HTTP request.</span></span> | <span data-ttu-id="1a29d-2421">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2421">No</span></span> |
| <span data-ttu-id="1a29d-2422">formato</span><span class="sxs-lookup"><span data-stu-id="1a29d-2422">format</span></span> | <span data-ttu-id="1a29d-2423">Si desea simplemente **recuperar los datos del punto de conexión HTTP tal cual** sin analizarlos, omita esta configuración de formato.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="1a29d-2424">Si desea analizar el contenido de la respuesta HTTP durante la copia, se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1a29d-2425">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="1a29d-2426">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2426">No</span></span> |
| <span data-ttu-id="1a29d-2427">compresión</span><span class="sxs-lookup"><span data-stu-id="1a29d-2427">compression</span></span> | <span data-ttu-id="1a29d-2428">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1a29d-2429">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1a29d-2430">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1a29d-2431">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1a29d-2432">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="1a29d-2433">Ejemplo: Uso del método GET (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="1a29d-2434">Ejemplo: Uso del método POST</span><span class="sxs-lookup"><span data-stu-id="1a29d-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="1a29d-2435">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="1a29d-2436">Origen de HTTP en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2437">Si va a copiar datos desde un origen HTTP, establezca el **tipo de origen** de la actividad de copia en **HttpSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2438">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2438">Property</span></span> | <span data-ttu-id="1a29d-2439">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2439">Description</span></span> | <span data-ttu-id="1a29d-2440">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="1a29d-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="1a29d-2441">httpRequestTimeout</span></span> | <span data-ttu-id="1a29d-2442">El tiempo que la solicitud HTTP espera (TimeSpan) a obtener una respuesta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="1a29d-2443">Es el tiempo de espera para obtener una respuesta, no para leer los datos de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="1a29d-2444">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2444">No.</span></span> <span data-ttu-id="1a29d-2445">Valor predeterminado: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="1a29d-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-2446">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-2447">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="1a29d-2448">OData</span><span class="sxs-lookup"><span data-stu-id="1a29d-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-2449">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2449">Linked service</span></span>
<span data-ttu-id="1a29d-2450">Para definir un servicio vinculado de OData, establezca el **tipo** de servicio vinculado en **OData** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2451">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2451">Property</span></span> | <span data-ttu-id="1a29d-2452">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2452">Description</span></span> | <span data-ttu-id="1a29d-2453">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2454">URL</span><span class="sxs-lookup"><span data-stu-id="1a29d-2454">url</span></span> |<span data-ttu-id="1a29d-2455">Dirección URL del servicio de OData.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2455">Url of the OData service.</span></span> |<span data-ttu-id="1a29d-2456">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2456">Yes</span></span> |
| <span data-ttu-id="1a29d-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2457">authenticationType</span></span> |<span data-ttu-id="1a29d-2458">Tipo de autenticación que se usa para conectarse al origen de OData.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="1a29d-2459">Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="1a29d-2460">Para OData local, los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1a29d-2461">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2461">Yes</span></span> |
| <span data-ttu-id="1a29d-2462">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2462">username</span></span> |<span data-ttu-id="1a29d-2463">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="1a29d-2464">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="1a29d-2465">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2465">password</span></span> |<span data-ttu-id="1a29d-2466">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-2467">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="1a29d-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2468">authorizedCredential</span></span> |<span data-ttu-id="1a29d-2469">Si está usando OAuth, haga clic en el botón **Autorizar** del Editor o el Asistente para copiar de Data Factory y escriba su credencial. Después, el valor de esta propiedad se generará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="1a29d-2470">Sí (solo si usa la autenticación OAuth)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="1a29d-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2471">gatewayName</span></span> |<span data-ttu-id="1a29d-2472">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse al servicio de OData local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="1a29d-2473">Especifique solo si va a copiar datos del origen de OData local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="1a29d-2474">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="1a29d-2475">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1a29d-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="1a29d-2476">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="1a29d-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="1a29d-2477">Ejemplo: Uso de la autenticación de Windows para acceder al origen de OData local</span><span class="sxs-lookup"><span data-stu-id="1a29d-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="1a29d-2478">Ejemplo: Uso de la autenticación OAuth para tener acceso al origen de OData en la nube</span><span class="sxs-lookup"><span data-stu-id="1a29d-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="1a29d-2479">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="1a29d-2480">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2480">Dataset</span></span>
<span data-ttu-id="1a29d-2481">Para definir un conjunto de datos de OData , establezca el **tipo** de conjunto de datos en **ODataResource** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2482">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2482">Property</span></span> | <span data-ttu-id="1a29d-2483">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2483">Description</span></span> | <span data-ttu-id="1a29d-2484">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2485">path</span><span class="sxs-lookup"><span data-stu-id="1a29d-2485">path</span></span> |<span data-ttu-id="1a29d-2486">Ruta de acceso al recurso de OData</span><span class="sxs-lookup"><span data-stu-id="1a29d-2486">Path to the OData resource</span></span> |<span data-ttu-id="1a29d-2487">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2488">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="1a29d-2489">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-2490">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2491">Si va a copiar datos desde un origen de OData, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2492">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2492">Property</span></span> | <span data-ttu-id="1a29d-2493">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2493">Description</span></span> | <span data-ttu-id="1a29d-2494">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2494">Example</span></span> | <span data-ttu-id="1a29d-2495">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2496">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-2496">query</span></span> |<span data-ttu-id="1a29d-2497">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="1a29d-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="1a29d-2499">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2500">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="1a29d-2501">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="1a29d-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="1a29d-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-2503">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2503">Linked service</span></span>
<span data-ttu-id="1a29d-2504">Para definir un servicio vinculado de ODBC, establezca el **tipo** de servicio vinculado en **OnPremisesOdbc** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2505">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2505">Property</span></span> | <span data-ttu-id="1a29d-2506">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2506">Description</span></span> | <span data-ttu-id="1a29d-2507">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-2508">connectionString</span></span> |<span data-ttu-id="1a29d-2509">La parte de la credencial de no acceso de la cadena de conexión, así como una credencial cifrada opcional.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="1a29d-2510">Vea ejemplos en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2510">See examples in the following sections.</span></span> |<span data-ttu-id="1a29d-2511">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2511">Yes</span></span> |
| <span data-ttu-id="1a29d-2512">credential</span><span class="sxs-lookup"><span data-stu-id="1a29d-2512">credential</span></span> |<span data-ttu-id="1a29d-2513">La parte de la credencial de acceso de la cadena de conexión especificada en formato de valor de propiedad específico del controlador.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="1a29d-2514">Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="1a29d-2515">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2515">No</span></span> |
| <span data-ttu-id="1a29d-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2516">authenticationType</span></span> |<span data-ttu-id="1a29d-2517">Tipo de autenticación que se usa para conectarse al almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="1a29d-2518">Los valores posibles son: Anonymous y Basic.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="1a29d-2519">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2519">Yes</span></span> |
| <span data-ttu-id="1a29d-2520">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2520">username</span></span> |<span data-ttu-id="1a29d-2521">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="1a29d-2522">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2522">No</span></span> |
| <span data-ttu-id="1a29d-2523">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2523">password</span></span> |<span data-ttu-id="1a29d-2524">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-2525">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2525">No</span></span> |
| <span data-ttu-id="1a29d-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2526">gatewayName</span></span> |<span data-ttu-id="1a29d-2527">Nombre de la puerta de enlace que el servicio Factoría de datos debe usar para conectarse al almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="1a29d-2528">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="1a29d-2529">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1a29d-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="1a29d-2530">Ejemplo: Uso de la autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="1a29d-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="1a29d-2531">Las credenciales se pueden cifrar mediante el cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (versión 1.0 de Azure PowerShell) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (versión 0.9 o una versión anterior de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="1a29d-2532">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="1a29d-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="1a29d-2533">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-2534">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2534">Dataset</span></span>
<span data-ttu-id="1a29d-2535">Para definir un conjunto de datos de ODBC, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2536">Property</span></span> | <span data-ttu-id="1a29d-2537">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2537">Description</span></span> | <span data-ttu-id="1a29d-2538">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2539">tableName</span></span> |<span data-ttu-id="1a29d-2540">Nombre de la tabla en el almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="1a29d-2541">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="1a29d-2542">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-2543">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-2544">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2545">Si va a copiar datos desde un almacén de datos de ODBC, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2546">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2546">Property</span></span> | <span data-ttu-id="1a29d-2547">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2547">Description</span></span> | <span data-ttu-id="1a29d-2548">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2548">Allowed values</span></span> | <span data-ttu-id="1a29d-2549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2550">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-2550">query</span></span> |<span data-ttu-id="1a29d-2551">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-2552">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2552">SQL query string.</span></span> <span data-ttu-id="1a29d-2553">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="1a29d-2554">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2555">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="1a29d-2556">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="1a29d-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="1a29d-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="1a29d-2558">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2558">Linked service</span></span>
<span data-ttu-id="1a29d-2559">Para definir un servicio vinculado de Salesforce, establezca el **tipo** de servicio vinculado en **Salesforce** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2560">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2560">Property</span></span> | <span data-ttu-id="1a29d-2561">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2561">Description</span></span> | <span data-ttu-id="1a29d-2562">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="1a29d-2563">environmentUrl</span></span> | <span data-ttu-id="1a29d-2564">Especifique la URL de la instancia de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="1a29d-2565">- La dirección predeterminada es "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1a29d-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="1a29d-2566">- Para copiar los datos desde el espacio aislado, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1a29d-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="1a29d-2567">- Para copiar datos del dominio personalizado, especifique, por ejemplo, "https://[dominio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1a29d-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="1a29d-2568">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2568">No</span></span> |
| <span data-ttu-id="1a29d-2569">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2569">username</span></span> |<span data-ttu-id="1a29d-2570">Especifique el nombre de usuario de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="1a29d-2571">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2571">Yes</span></span> |
| <span data-ttu-id="1a29d-2572">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2572">password</span></span> |<span data-ttu-id="1a29d-2573">Especifique la contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="1a29d-2574">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2574">Yes</span></span> |
| <span data-ttu-id="1a29d-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="1a29d-2575">securityToken</span></span> |<span data-ttu-id="1a29d-2576">Especifique el token de seguridad para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="1a29d-2577">Consulte [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtención de un token de seguridad) para ver instrucciones sobre cómo restablecer u obtener un token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="1a29d-2578">Para más información acerca de los tokens de seguridad en general, consulte [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Seguridad y la API).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="1a29d-2579">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2580">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="1a29d-2581">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-2582">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2582">Dataset</span></span>
<span data-ttu-id="1a29d-2583">Para definir un conjunto de datos de Salesforce, establezca el **tipo** de conjunto de datos en **RelationalTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2584">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2584">Property</span></span> | <span data-ttu-id="1a29d-2585">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2585">Description</span></span> | <span data-ttu-id="1a29d-2586">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2587">tableName</span></span> |<span data-ttu-id="1a29d-2588">Nombre de la tabla de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="1a29d-2589">No (si se especifica una **consulta** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2590">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a29d-2591">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="1a29d-2592">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2593">Si va a copiar datos desde Salesforce, establezca el **tipo de origen** de la actividad de copia en **RelationalSource** y especifique las siguientes propiedades en la sección **origen**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="1a29d-2594">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2594">Property</span></span> | <span data-ttu-id="1a29d-2595">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2595">Description</span></span> | <span data-ttu-id="1a29d-2596">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2596">Allowed values</span></span> | <span data-ttu-id="1a29d-2597">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a29d-2598">query</span><span class="sxs-lookup"><span data-stu-id="1a29d-2598">query</span></span> |<span data-ttu-id="1a29d-2599">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="1a29d-2600">Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="1a29d-2601">Por ejemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="1a29d-2602">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2603">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="1a29d-2604">La parte "__c" del nombre de la API es necesaria para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="1a29d-2605">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="1a29d-2606">Datos web</span><span class="sxs-lookup"><span data-stu-id="1a29d-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2607">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2607">Linked service</span></span>
<span data-ttu-id="1a29d-2608">Para definir un servicio vinculado de Web, establezca el **tipo** de servicio vinculado en **Web** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2609">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2609">Property</span></span> | <span data-ttu-id="1a29d-2610">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2610">Description</span></span> | <span data-ttu-id="1a29d-2611">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2612">URL</span><span class="sxs-lookup"><span data-stu-id="1a29d-2612">Url</span></span> |<span data-ttu-id="1a29d-2613">Dirección URL para el origen de Web</span><span class="sxs-lookup"><span data-stu-id="1a29d-2613">URL to the Web source</span></span> |<span data-ttu-id="1a29d-2614">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2614">Yes</span></span> |
| <span data-ttu-id="1a29d-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2615">authenticationType</span></span> |<span data-ttu-id="1a29d-2616">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2616">Anonymous.</span></span> |<span data-ttu-id="1a29d-2617">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="1a29d-2618">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="1a29d-2619">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="1a29d-2620">Dataset</span><span class="sxs-lookup"><span data-stu-id="1a29d-2620">Dataset</span></span>
<span data-ttu-id="1a29d-2621">Para definir un conjunto de datos de Web, establezca el **tipo** de conjunto de datos en **WebTable** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="1a29d-2622">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2622">Property</span></span> | <span data-ttu-id="1a29d-2623">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2623">Description</span></span> | <span data-ttu-id="1a29d-2624">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-2625">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2625">type</span></span> |<span data-ttu-id="1a29d-2626">Tipo del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2626">type of the dataset.</span></span> <span data-ttu-id="1a29d-2627">Debe establecerse en **WebTable**</span><span class="sxs-lookup"><span data-stu-id="1a29d-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="1a29d-2628">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2628">Yes</span></span> |
| <span data-ttu-id="1a29d-2629">path</span><span class="sxs-lookup"><span data-stu-id="1a29d-2629">path</span></span> |<span data-ttu-id="1a29d-2630">Dirección URL relativa al recurso que contiene la tabla.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="1a29d-2631">No.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2631">No.</span></span> <span data-ttu-id="1a29d-2632">Cuando no se especifica la ruta de acceso, se solo se usa la dirección URL especificada en la definición de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="1a29d-2633">index</span><span class="sxs-lookup"><span data-stu-id="1a29d-2633">index</span></span> |<span data-ttu-id="1a29d-2634">Índice de la tabla en el recurso.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2634">The index of the table in the resource.</span></span> <span data-ttu-id="1a29d-2635">Consulte la sección [Obtención de índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) para saber los pasos necesarios para obtener el índice de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="1a29d-2636">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="1a29d-2637">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1a29d-2638">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="1a29d-2639">Origen de Web en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="1a29d-2640">Si va a copiar datos de una tabla web, establezca el **tipo de origen** de la actividad de copia en **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="1a29d-2641">En este momento, cuando el origen de la actividad de copia es de tipo **WebSource**, no se admite ninguna propiedad adicional.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="1a29d-2642">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="1a29d-2643">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="1a29d-2644">ENTORNOS DE PROCESO</span><span class="sxs-lookup"><span data-stu-id="1a29d-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="1a29d-2645">En la tabla siguiente se enumeran entornos de proceso compatibles con Data Factory y las actividades de transformación que se pueden ejecutar en ellos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="1a29d-2646">Haga clic en el vínculo del proceso que le interesa para ver los esquemas JSON del servicio vinculado para vincularlo a una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="1a29d-2647">Entorno de procesos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2647">Compute environment</span></span> | <span data-ttu-id="1a29d-2648">Actividades</span><span class="sxs-lookup"><span data-stu-id="1a29d-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="1a29d-2649">[Clúster de HDInsight a petición](#on-demand-azure-hdinsight-cluster) o [clúster HDInsight propio](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="1a29d-2650">[Actividad personalizada de .NET](#net-custom-activity), [actividad de Hive](#hdinsight-hive-activity), [actividad de Pig](#hdinsight-pig-activity, [actividad de MapReduce](#hdinsight-mapreduce-activity), [actividad de streaming de Hadoop](#hdinsight-streaming-activityd) y [actividad de Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="1a29d-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="1a29d-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="1a29d-2652">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="1a29d-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="1a29d-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a29d-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="1a29d-2654">[Actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="1a29d-2655">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="1a29d-2656">U-SQL de análisis con Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="1a29d-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1) y [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="1a29d-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="1a29d-2658">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="1a29d-2659">Clúster de Azure HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="1a29d-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="1a29d-2660">El servicio Factoría de datos de Azure crea automáticamente un clúster de HDInsight basado en Windows/Linux a petición para procesar los datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="1a29d-2661">El clúster se crea en la misma región que la cuenta de almacenamiento (propiedad linkedServiceName en JSON) asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="1a29d-2662">Puede ejecutar las siguientes actividades de transformación en este servicio vinculado: [actividad personalizada de .NET](#net-custom-activity), [actividad de Hive](#hdinsight-hive-activity), [actividad de Pig](#hdinsight-pig-activity, [actividad de MapReduce](#hdinsight-mapreduce-activity), [actividad de streaming de Hadoop](#hdinsight-streaming-activityd) y [actividad de Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2663">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2663">Linked service</span></span> 
<span data-ttu-id="1a29d-2664">En la siguiente tabla se ofrecen descripciones de las propiedades que se usan en la definición de JSON en Azure de un servicio vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="1a29d-2665">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2665">Property</span></span> | <span data-ttu-id="1a29d-2666">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2666">Description</span></span> | <span data-ttu-id="1a29d-2667">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2668">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2668">type</span></span> |<span data-ttu-id="1a29d-2669">La propiedad type se debe establecer en **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="1a29d-2670">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2670">Yes</span></span> |
| <span data-ttu-id="1a29d-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="1a29d-2671">clusterSize</span></span> |<span data-ttu-id="1a29d-2672">Número de nodos de datos o trabajo del clúster</span><span class="sxs-lookup"><span data-stu-id="1a29d-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="1a29d-2673">El clúster de HDInsight se crea con dos nodos principales junto con el número de nodos de trabajo que haya especificado para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="1a29d-2674">Los nodos son de tamaño Standard_D3 con 4 núcleos, por lo que un clúster de nodos de 4 trabajos necesitará 24 núcleos (4\*4 = 16 para nodos de trabajo, más 2\*4 = 8 para nodos principales).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="1a29d-2675">Consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para más información acerca del nivel Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="1a29d-2676">yes</span><span class="sxs-lookup"><span data-stu-id="1a29d-2676">Yes</span></span> |
| <span data-ttu-id="1a29d-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="1a29d-2677">timetolive</span></span> |<span data-ttu-id="1a29d-2678">El tiempo de inactividad permitido para el clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="1a29d-2679">Especifica cuánto tiempo permanece activo el clúster de HDInsight a petición después de la finalización de una ejecución de actividad si no hay ningún otro trabajo activo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="1a29d-2680">Por ejemplo, si una ejecución de actividad tarda 6 minutos y timetolive está establecido en 5 minutos, el clúster permanece activo durante 5 minutos después de los 6 minutos de procesamiento de la ejecución de actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="1a29d-2681">Si se realiza otra ejecución de actividad con un margen de 6 minutos, la procesa el mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="1a29d-2682">Crear un clúster de HDInsight a petición es una operación costosa (podría tardar un poco); use esta configuración si es necesario para mejorar el rendimiento de una factoría de datos mediante la reutilización de un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="1a29d-2683">Si establece el valor de timetolive en 0, el clúster se elimina en cuanto se procesa la ejecución de actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="1a29d-2684">Por otra parte, si establece un valor alto, el clúster puede permanecer inactivo innecesariamente, lo que conlleva unos costos elevados.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="1a29d-2685">Por lo tanto, es importante que establezca el valor adecuado en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="1a29d-2686">Varias canalizaciones pueden compartir la misma instancia del clúster de HDInsight a petición si el valor de la propiedad timetolive está correctamente configurado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="1a29d-2687">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2687">Yes</span></span> |
| <span data-ttu-id="1a29d-2688">versión</span><span class="sxs-lookup"><span data-stu-id="1a29d-2688">version</span></span> |<span data-ttu-id="1a29d-2689">Versión del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="1a29d-2690">Para obtener más información, consulte [Versiones admitidas de HDInsight en Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="1a29d-2691">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2691">No</span></span> |
| <span data-ttu-id="1a29d-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2692">linkedServiceName</span></span> |<span data-ttu-id="1a29d-2693">El servicio vinculado de Almacenamiento de Azure que usará el clúster a petición para almacenar y procesar datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="1a29d-2694">Actualmente, no se puede crear un clúster de HDInsight a petición que utilice una instancia de Azure Data Lake Store como almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="1a29d-2695">Si desea almacenar los datos de resultados del procesamiento de HDInsight en una instancia de Azure Data Lake Store, utilice una actividad de copia para copiar los datos desde Azure Blob Storage a Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="1a29d-2696">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2696">Yes</span></span> |
| <span data-ttu-id="1a29d-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="1a29d-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="1a29d-2698">Especifica cuentas de almacenamiento adicionales para el servicio vinculado de HDInsight, de forma que el servicio Factoría de datos pueda registrarlas en su nombre.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="1a29d-2699">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2699">No</span></span> |
| <span data-ttu-id="1a29d-2700">osType</span><span class="sxs-lookup"><span data-stu-id="1a29d-2700">osType</span></span> |<span data-ttu-id="1a29d-2701">Tipo de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2701">Type of operating system.</span></span> <span data-ttu-id="1a29d-2702">Los valores permitidos son: Windows (predeterminado) y Linux</span><span class="sxs-lookup"><span data-stu-id="1a29d-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="1a29d-2703">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2703">No</span></span> |
| <span data-ttu-id="1a29d-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="1a29d-2705">Nombre del servicio vinculado de SQL de Azure que apunta a la base de datos de HCatalog.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="1a29d-2706">El clúster de HDInsight a petición se creará usando la base de datos SQL de Azure como metaalmacén.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="1a29d-2707">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="1a29d-2708">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2708">JSON example</span></span>
<span data-ttu-id="1a29d-2709">En el siguiente JSON se define un servicio vinculado de HDInsight a petición basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="1a29d-2710">El servicio Data Factory crea automáticamente un clúster de HDInsight **basado en Linux** al procesar un segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="1a29d-2711">Para más información, vea [Servicios vinculados de procesos](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="1a29d-2712">Clúster de Azure HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="1a29d-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="1a29d-2713">Puede crear un servicio vinculado de HDInsight de Azure para registrar su propio clúster de HDInsight con la Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="1a29d-2714">Puede ejecutar las siguientes actividades de transformación de datos en este servicio vinculado: [actividad personalizada de .NET](#net-custom-activity), [actividad de Hive](#hdinsight-hive-activity), [actividad de Pig](#hdinsight-pig-activity, [actividad de MapReduce](#hdinsight-mapreduce-activity), [actividad de streaming de Hadoop](#hdinsight-streaming-activityd) y [actividad de Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2715">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2715">Linked service</span></span>
<span data-ttu-id="1a29d-2716">En la siguiente tabla se ofrecen descripciones de las propiedades que se usan en la definición de JSON en Azure de un servicio vinculado de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="1a29d-2717">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2717">Property</span></span> | <span data-ttu-id="1a29d-2718">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2718">Description</span></span> | <span data-ttu-id="1a29d-2719">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2720">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2720">type</span></span> |<span data-ttu-id="1a29d-2721">La propiedad type se debe establecer en **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="1a29d-2722">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2722">Yes</span></span> |
| <span data-ttu-id="1a29d-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="1a29d-2723">clusterUri</span></span> |<span data-ttu-id="1a29d-2724">El URI del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="1a29d-2725">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2725">Yes</span></span> |
| <span data-ttu-id="1a29d-2726">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2726">username</span></span> |<span data-ttu-id="1a29d-2727">Especifique el nombre de usuario que se usará para conectarse a un clúster de HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="1a29d-2728">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2728">Yes</span></span> |
| <span data-ttu-id="1a29d-2729">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2729">password</span></span> |<span data-ttu-id="1a29d-2730">Especifique la contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2730">Specify password for the user account.</span></span> |<span data-ttu-id="1a29d-2731">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2731">Yes</span></span> |
| <span data-ttu-id="1a29d-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2732">linkedServiceName</span></span> | <span data-ttu-id="1a29d-2733">Nombre del servicio vinculado para Azure Storage que hace referencia al almacenamiento Azure Blob Storage que usa el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="1a29d-2734">Actualmente, no se puede especificar un servicio vinculado de Azure Data Lake Store para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="1a29d-2735">Puede acceder a los datos de Azure Data Lake Store desde scripts de Pig/Hive si el clúster de HDInsight tiene acceso a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="1a29d-2736">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2736">Yes</span></span> |

<span data-ttu-id="1a29d-2737">Para conocer las versiones de los clústeres de HDInsight admitidas, consulte [Versiones compatibles con HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="1a29d-2738">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="1a29d-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="1a29d-2739">Azure Batch</span></span>
<span data-ttu-id="1a29d-2740">Puede crear un servicio vinculado de Azure Batch para registrar un grupo de Batch de máquinas virtuales (VM) en una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="1a29d-2741">Puede ejecutar actividades personalizadas .NET con Lote de Azure o HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="1a29d-2742">Puede ejecutar una [actividad personalizada de .NET](#net-custom-activity) en este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2743">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2743">Linked service</span></span>
<span data-ttu-id="1a29d-2744">En la siguiente tabla se ofrecen descripciones de las propiedades que se usan en la definición de JSON en Azure de un servicio vinculado de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="1a29d-2745">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2745">Property</span></span> | <span data-ttu-id="1a29d-2746">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2746">Description</span></span> | <span data-ttu-id="1a29d-2747">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2748">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2748">type</span></span> |<span data-ttu-id="1a29d-2749">La propiedad type se debe establecer en **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="1a29d-2750">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2750">Yes</span></span> |
| <span data-ttu-id="1a29d-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2751">accountName</span></span> |<span data-ttu-id="1a29d-2752">Nombre de la cuenta de Lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="1a29d-2753">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2753">Yes</span></span> |
| <span data-ttu-id="1a29d-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="1a29d-2754">accessKey</span></span> |<span data-ttu-id="1a29d-2755">Clave de acceso de la cuenta de Lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="1a29d-2756">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2756">Yes</span></span> |
| <span data-ttu-id="1a29d-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2757">poolName</span></span> |<span data-ttu-id="1a29d-2758">Nombre del grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="1a29d-2759">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2759">Yes</span></span> |
| <span data-ttu-id="1a29d-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2760">linkedServiceName</span></span> |<span data-ttu-id="1a29d-2761">Nombre del servicio vinculado de Almacenamiento de Azure asociado a este servicio vinculado de Lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="1a29d-2762">Este servicio vinculado se usa para los archivos de almacenamiento provisional necesarios para ejecutar la actividad y almacenar los registros de ejecución de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="1a29d-2763">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="1a29d-2764">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="1a29d-2765">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-2765">Azure Machine Learning</span></span>
<span data-ttu-id="1a29d-2766">Un servicio vinculado de Azure Machine Learning se crea para registrar un punto de conexión de puntuación por lotes de Machine Learning en una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="1a29d-2767">Se pueden ejecutar dos actividades de transformación de datos en este servicio vinculado: [actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2768">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2768">Linked service</span></span>
<span data-ttu-id="1a29d-2769">En la siguiente tabla se ofrecen descripciones de las propiedades que se usan en la definición de JSON en Azure de un servicio vinculado de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="1a29d-2770">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2770">Property</span></span> | <span data-ttu-id="1a29d-2771">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2771">Description</span></span> | <span data-ttu-id="1a29d-2772">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2773">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2773">Type</span></span> |<span data-ttu-id="1a29d-2774">La propiedad type se debe establecer en: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="1a29d-2775">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2775">Yes</span></span> |
| <span data-ttu-id="1a29d-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="1a29d-2776">mlEndpoint</span></span> |<span data-ttu-id="1a29d-2777">La dirección URL de puntuación por lotes.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2777">The batch scoring URL.</span></span> |<span data-ttu-id="1a29d-2778">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2778">Yes</span></span> |
| <span data-ttu-id="1a29d-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="1a29d-2779">apiKey</span></span> |<span data-ttu-id="1a29d-2780">La API del modelo de área de trabajo publicado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="1a29d-2781">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="1a29d-2782">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="1a29d-2783">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="1a29d-2784">Cree un servicio vinculado con **Análisis con Azure Data Lake** para vincular un servicio de proceso de Análisis con Azure Data Lake a un generador de datos de Azure antes de usar la [actividad U-SQL de Análisis con Data Lake](data-factory-usql-activity.md) en una canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="1a29d-2785">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2785">Linked service</span></span>

<span data-ttu-id="1a29d-2786">En la siguiente tabla se ofrecen descripciones de las propiedades que se usan en la definición de JSON de un servicio vinculado de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="1a29d-2787">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2787">Property</span></span> | <span data-ttu-id="1a29d-2788">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2788">Description</span></span> | <span data-ttu-id="1a29d-2789">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2790">Type</span></span> |<span data-ttu-id="1a29d-2791">La propiedad type se debe establecer en: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="1a29d-2792">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2792">Yes</span></span> |
| <span data-ttu-id="1a29d-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2793">accountName</span></span> |<span data-ttu-id="1a29d-2794">Nombre de la cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="1a29d-2795">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2795">Yes</span></span> |
| <span data-ttu-id="1a29d-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="1a29d-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="1a29d-2797">Identificador URI de Análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="1a29d-2798">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2798">No</span></span> |
| <span data-ttu-id="1a29d-2799">authorization</span><span class="sxs-lookup"><span data-stu-id="1a29d-2799">authorization</span></span> |<span data-ttu-id="1a29d-2800">El código de autorización se recupera automáticamente después de hacer clic en el botón **Autorizar** situado en el Editor de Factoría de datos y de completar el inicio de sesión de OAuth.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="1a29d-2801">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2801">Yes</span></span> |
| <span data-ttu-id="1a29d-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1a29d-2802">subscriptionId</span></span> |<span data-ttu-id="1a29d-2803">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-2803">Azure subscription id</span></span> |<span data-ttu-id="1a29d-2804">No (si no se especifica, se usa la suscripción de Data Factory).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="1a29d-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2805">resourceGroupName</span></span> |<span data-ttu-id="1a29d-2806">Nombre del grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2806">Azure resource group name</span></span> |<span data-ttu-id="1a29d-2807">No (si no se especifica, se usa el grupo de recursos de la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="1a29d-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="1a29d-2808">sessionId</span></span> |<span data-ttu-id="1a29d-2809">Identificador de sesión de la sesión de autorización de OAuth.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="1a29d-2810">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="1a29d-2811">Si usa Data Factory Editor, este identificador se genera automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="1a29d-2812">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="1a29d-2813">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2813">JSON example</span></span>
<span data-ttu-id="1a29d-2814">En el ejemplo siguiente se proporciona la definición de JSON de un servicio vinculado de Análisis con Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="1a29d-2815">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-2815">Azure SQL Database</span></span>
<span data-ttu-id="1a29d-2816">Cree un servicio vinculado de Azure SQL y úselo con la [actividad de procedimiento almacenado](#stored-procedure-activity) para invocar un procedimiento almacenado desde una canalización de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2817">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2817">Linked service</span></span>
<span data-ttu-id="1a29d-2818">Para definir un servicio vinculado de Azure SQL Database, establezca el **tipo** de servicio vinculado en **AzureSqlDatabase** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2819">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2819">Property</span></span> | <span data-ttu-id="1a29d-2820">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2820">Description</span></span> | <span data-ttu-id="1a29d-2821">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-2822">connectionString</span></span> |<span data-ttu-id="1a29d-2823">Especifique la información necesaria para conectarse a la instancia de Base de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="1a29d-2824">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="1a29d-2825">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="1a29d-2826">Vea el artículo [Conector SQL de Azure](data-factory-azure-sql-connector.md#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="1a29d-2827">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="1a29d-2828">Cree un servicio vinculado de Almacenamiento de datos SQL y úselo con la [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) para invocar un procedimiento almacenado desde una canalización de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2829">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2829">Linked service</span></span>
<span data-ttu-id="1a29d-2830">Para definir un servicio vinculado de Azure SQL Data Warehouse, establezca el **tipo** de servicio vinculado en **AzureSqlDW** y especifique las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="1a29d-2831">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2831">Property</span></span> | <span data-ttu-id="1a29d-2832">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2832">Description</span></span> | <span data-ttu-id="1a29d-2833">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-2834">connectionString</span></span> |<span data-ttu-id="1a29d-2835">Especifique la información necesaria para conectarse a la instancia de Almacenamiento de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="1a29d-2836">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="1a29d-2837">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="1a29d-2838">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="1a29d-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a29d-2839">SQL Server</span></span> 
<span data-ttu-id="1a29d-2840">Cree un servicio vinculado de SQL Server y úselo con la [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) para invocar un procedimiento almacenado desde una canalización de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="1a29d-2841">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2841">Linked service</span></span>
<span data-ttu-id="1a29d-2842">Se crea un servicio vinculado de tipo **OnPremisesSqlServer** para vincular una base de datos SQL Server local a una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="1a29d-2843">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="1a29d-2844">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio SQL Server vinculado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="1a29d-2845">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2845">Property</span></span> | <span data-ttu-id="1a29d-2846">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2846">Description</span></span> | <span data-ttu-id="1a29d-2847">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2848">type</span><span class="sxs-lookup"><span data-stu-id="1a29d-2848">type</span></span> |<span data-ttu-id="1a29d-2849">La propiedad type se debe establecer en **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="1a29d-2850">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2850">Yes</span></span> |
| <span data-ttu-id="1a29d-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a29d-2851">connectionString</span></span> |<span data-ttu-id="1a29d-2852">Especifique la información de connectionString necesaria para conectarse a la Base de datos SQL Server local mediante autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="1a29d-2853">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2853">Yes</span></span> |
| <span data-ttu-id="1a29d-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a29d-2854">gatewayName</span></span> |<span data-ttu-id="1a29d-2855">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la Base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="1a29d-2856">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2856">Yes</span></span> |
| <span data-ttu-id="1a29d-2857">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1a29d-2857">username</span></span> |<span data-ttu-id="1a29d-2858">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="1a29d-2859">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="1a29d-2860">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2860">No</span></span> |
| <span data-ttu-id="1a29d-2861">contraseña</span><span class="sxs-lookup"><span data-stu-id="1a29d-2861">password</span></span> |<span data-ttu-id="1a29d-2862">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a29d-2863">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2863">No</span></span> |

<span data-ttu-id="1a29d-2864">Puede cifrar las credenciales con el cmdlet **New-AzureRmDataFactoryEncryptValue** y usarlas en la cadena de conexión, como se muestra en el ejemplo siguiente (propiedad **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="1a29d-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="1a29d-2865">Ejemplo: JSON para usar autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="1a29d-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="1a29d-2866">Ejemplo: JSON para usar autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="1a29d-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="1a29d-2867">Si se especifican el nombre de usuario y la contraseña, la puerta de enlace los usará para suplantar la cuenta de usuario especificada para conectarse a la Base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="1a29d-2868">En caso contrario, la puerta de enlace se conectará directamente a SQL Server con el contexto de seguridad de puerta de enlace (su cuenta de inicio).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="1a29d-2869">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="1a29d-2870">ACTIVIDADES DE TRANSFORMACIÓN DE DATOS</span><span class="sxs-lookup"><span data-stu-id="1a29d-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="1a29d-2871">Actividad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2871">Activity</span></span> | <span data-ttu-id="1a29d-2872">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="1a29d-2873">Actividad de Hive de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="1a29d-2874">La actividad de Hive de HDInsight en una canalización de Data Factory ejecuta consultas de Hive en su propio clúster de HDInsight o en uno a petición basado en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="1a29d-2875">Actividad de Pig de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="1a29d-2876">La actividad de Pig de HDInsight en una canalización de Data Factory ejecuta consultas de Pig en su propio clúster de HDInsight o en uno a petición basado en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="1a29d-2877">Actividad de MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="1a29d-2878">La actividad MapReduce de HDInsight en una canalización de Data Factory ejecuta programas de MapReduce en su propio clúster de HDInsight o en uno basado en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="1a29d-2879">Actividad de streaming de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="1a29d-2880">La actividad de streaming de HDInsight en una canalización de Data Factory ejecuta programas de streaming de Hadoop en su propio clúster de HDInsight o en uno basado en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="1a29d-2881">Actividad de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="1a29d-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="1a29d-2882">La actividad de Spark de HDInsight en una canalización de Data Factory ejecuta consultas de Spark en su propio clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="1a29d-2883">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a29d-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="1a29d-2884">Azure Data Factory permite crear fácilmente canalizaciones que utilizan un servicio web de Azure Machine Learning publicado para realizar análisis predictivos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="1a29d-2885">Mediante la actividad de ejecución de Batch en una canalización de Azure Data Factory, puede invocar un servicio web Machine Learning para realizar predicciones sobre los datos en el lote.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="1a29d-2886">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a29d-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="1a29d-2887">Pasado algún tiempo, los modelos predictivos en los experimentos de puntuación de Machine Learning tienen que volver a entrenarse con nuevos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="1a29d-2888">Después de terminar con el nuevo entrenamiento, tendrá que actualizar el servicio web de puntuación con el modelo de Machine Learning que volvió a entrenar.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="1a29d-2889">Puede usar la Actividad de recursos de actualización para actualizar el servicio web con el modelo recién entrenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="1a29d-2890">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="1a29d-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="1a29d-2891">Puede usar la actividad de procedimiento almacenado en una canalización de Data Factory para invocar un procedimiento almacenado en uno de los siguientes almacenes de datos: Azure SQL Database, Azure SQL Data Warehouse y Base de datos de SQL Server en su empresa o en una VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="1a29d-2892">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1a29d-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="1a29d-2893">La actividad de U-SQL de Data Lake Analytics ejecuta un script de U-SQL en un clúster de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="1a29d-2894">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="1a29d-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="1a29d-2895">Si necesita transformar datos de algún modo no compatible con Data Factory, puede crear una actividad personalizada con su propia lógica de procesamiento de datos y usarla en la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="1a29d-2896">Puede configurar una actividad de .NET personalizada para ejecutarse mediante un servicio Azure Batch o un clúster de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="1a29d-2897">Actividad de Hive de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="1a29d-2898">Puede especificar las siguientes propiedades en una definición JSON de actividad de Hive.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="1a29d-2899">La propiedad de tipo de la actividad debe ser: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="1a29d-2900">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-2901">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en HDInsightHive:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="1a29d-2902">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2902">Property</span></span> | <span data-ttu-id="1a29d-2903">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2903">Description</span></span> | <span data-ttu-id="1a29d-2904">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2905">script</span><span class="sxs-lookup"><span data-stu-id="1a29d-2905">script</span></span> |<span data-ttu-id="1a29d-2906">Especifica el script de Hive en línea</span><span class="sxs-lookup"><span data-stu-id="1a29d-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="1a29d-2907">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2907">No</span></span> |
| <span data-ttu-id="1a29d-2908">script path</span><span class="sxs-lookup"><span data-stu-id="1a29d-2908">script path</span></span> |<span data-ttu-id="1a29d-2909">Almacena el script de Hive en un almacenamiento de blobs de Azure y proporciona la ruta de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="1a29d-2910">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="1a29d-2911">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2911">Both cannot be used together.</span></span> <span data-ttu-id="1a29d-2912">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="1a29d-2913">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2913">No</span></span> |
| <span data-ttu-id="1a29d-2914">define los campos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2914">defines</span></span> |<span data-ttu-id="1a29d-2915">Especifique parámetros como pares de clave y valor para referencia en el script de Hive con 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="1a29d-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="1a29d-2916">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2916">No</span></span> |

<span data-ttu-id="1a29d-2917">Estas propiedades de tipo son específicas de la actividad de Hive.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="1a29d-2918">Otras propiedades (fuera de la sección typeProperties) son compatibles con todas las actividades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="1a29d-2919">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2919">JSON example</span></span>
<span data-ttu-id="1a29d-2920">El siguiente fragmento JSON define una actividad de Hive de HDInsight en una canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="1a29d-2921">Para más información, consulte el artículo [Actividad de Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="1a29d-2922">Actividad de Pig de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="1a29d-2923">Puede especificar las siguientes propiedades en una definición JSON de actividad de Pig.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="1a29d-2924">La propiedad de tipo de la actividad debe ser: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="1a29d-2925">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-2926">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en HDInsightPig:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="1a29d-2927">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2927">Property</span></span> | <span data-ttu-id="1a29d-2928">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2928">Description</span></span> | <span data-ttu-id="1a29d-2929">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2930">script</span><span class="sxs-lookup"><span data-stu-id="1a29d-2930">script</span></span> |<span data-ttu-id="1a29d-2931">Especifica el script de Pig en línea</span><span class="sxs-lookup"><span data-stu-id="1a29d-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="1a29d-2932">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2932">No</span></span> |
| <span data-ttu-id="1a29d-2933">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="1a29d-2933">script path</span></span> |<span data-ttu-id="1a29d-2934">Almacena el script de Pig en un almacenamiento de blobs de Azure y proporciona la ruta de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="1a29d-2935">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="1a29d-2936">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2936">Both cannot be used together.</span></span> <span data-ttu-id="1a29d-2937">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="1a29d-2938">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2938">No</span></span> |
| <span data-ttu-id="1a29d-2939">define los campos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2939">defines</span></span> |<span data-ttu-id="1a29d-2940">Especifique parámetros como pares de clave y valor para referencia en el script de Pig</span><span class="sxs-lookup"><span data-stu-id="1a29d-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="1a29d-2941">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2941">No</span></span> |

<span data-ttu-id="1a29d-2942">Estas propiedades de tipo son específicas de la actividad de Pig.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="1a29d-2943">Otras propiedades (fuera de la sección typeProperties) son compatibles con todas las actividades.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="1a29d-2944">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="1a29d-2945">Para más información, consulte el artículo [Actividad de Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="1a29d-2946">Actividad de MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="1a29d-2947">Puede especificar las siguientes propiedades en una definición JSON de actividad de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="1a29d-2948">La propiedad de tipo de la actividad debe ser: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="1a29d-2949">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-2950">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en HDInsightMapReduce:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="1a29d-2951">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2951">Property</span></span> | <span data-ttu-id="1a29d-2952">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2952">Description</span></span> | <span data-ttu-id="1a29d-2953">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="1a29d-2954">jarLinkedService</span></span> | <span data-ttu-id="1a29d-2955">Nombre del servicio vinculado de Azure Storage que contiene el archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="1a29d-2956">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2956">Yes</span></span> |
| <span data-ttu-id="1a29d-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="1a29d-2957">jarFilePath</span></span> | <span data-ttu-id="1a29d-2958">Ruta de acceso al archivo JAR en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="1a29d-2959">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2959">Yes</span></span> | 
| <span data-ttu-id="1a29d-2960">className</span><span class="sxs-lookup"><span data-stu-id="1a29d-2960">className</span></span> | <span data-ttu-id="1a29d-2961">Nombre de la clase principal en el archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="1a29d-2962">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-2962">Yes</span></span> | 
| <span data-ttu-id="1a29d-2963">argumentos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2963">arguments</span></span> | <span data-ttu-id="1a29d-2964">Una lista de argumentos separados por comas para el programa de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="1a29d-2965">En tiempo de ejecución, verá unos argumentos adicionales (por ejemplo, mapreduce.job.tags) desde el marco de trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="1a29d-2966">Para diferenciar sus argumentos con los argumentos de MapReduce, considere el uso tanto de opción como de valor como argumentos, tal como se muestra en el siguiente ejemplo (-s, --input, --output, etc., son opciones seguidas inmediatamente por sus valores).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="1a29d-2967">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="1a29d-2968">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="1a29d-2969">Para más información, consulte el artículo [Actividad de MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="1a29d-2970">Actividad de streaming de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a29d-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="1a29d-2971">Puede especificar las siguientes propiedades en una definición JSON de actividad de streaming de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="1a29d-2972">La propiedad de tipo de la actividad debe ser: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="1a29d-2973">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-2974">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en HDInsightStreaming:</span><span class="sxs-lookup"><span data-stu-id="1a29d-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="1a29d-2975">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-2975">Property</span></span> | <span data-ttu-id="1a29d-2976">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="1a29d-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="1a29d-2977">mapper</span></span> | <span data-ttu-id="1a29d-2978">Nombre del archivo ejecutable del asignador.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2978">Name of the mapper executable.</span></span> <span data-ttu-id="1a29d-2979">En el ejemplo, cat.exe es el ejecutable del asignador.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="1a29d-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="1a29d-2980">reducer</span></span> | <span data-ttu-id="1a29d-2981">Nombre del archivo ejecutable del reductor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2981">Name of the reducer executable.</span></span> <span data-ttu-id="1a29d-2982">En el ejemplo, wc.exe es el ejecutable del reductor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="1a29d-2983">input</span><span class="sxs-lookup"><span data-stu-id="1a29d-2983">input</span></span> | <span data-ttu-id="1a29d-2984">Archivo de entrada (incluida la ubicación) del asignador.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="1a29d-2985">En el ejemplo: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blobs, example/data/Gutenberg es la carpeta y davinci.txt es el blob.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="1a29d-2986">output</span><span class="sxs-lookup"><span data-stu-id="1a29d-2986">output</span></span> | <span data-ttu-id="1a29d-2987">Archivo de salida (incluida la ubicación) del reductor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="1a29d-2988">La salida del trabajo de streaming de Hadoop se escribirá en la ubicación especificada para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="1a29d-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="1a29d-2989">filePaths</span></span> | <span data-ttu-id="1a29d-2990">Rutas de acceso a los archivos ejecutables del asignador y del reductor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="1a29d-2991">En el ejemplo: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blobs, example/apps es la carpeta y wc.exe es el ejecutable.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="1a29d-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="1a29d-2992">fileLinkedService</span></span> | <span data-ttu-id="1a29d-2993">Servicio vinculado de Azure Storage que representa el almacenamiento de Azure que contiene los archivos especificados en la sección filePaths.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="1a29d-2994">argumentos</span><span class="sxs-lookup"><span data-stu-id="1a29d-2994">arguments</span></span> | <span data-ttu-id="1a29d-2995">Una lista de argumentos separados por comas para el programa de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="1a29d-2996">En tiempo de ejecución, verá unos argumentos adicionales (por ejemplo, mapreduce.job.tags) desde el marco de trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="1a29d-2997">Para diferenciar sus argumentos con los argumentos de MapReduce, considere el uso tanto de opción como de valor como argumentos, tal como se muestra en el siguiente ejemplo (-s, --input, --output, etc., son opciones seguidas inmediatamente por sus valores).</span><span class="sxs-lookup"><span data-stu-id="1a29d-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="1a29d-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="1a29d-2998">getDebugInfo</span></span> | <span data-ttu-id="1a29d-2999">Un elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="1a29d-2999">An optional element.</span></span> <span data-ttu-id="1a29d-3000">Cuando se establece en Failure, los registros solo se descargan en caso de error.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="1a29d-3001">Cuando se establece en All, los registros se descargan siempre, sea cual sea el estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="1a29d-3002">Debe especificar un conjunto de datos de salida para la actividad de streaming de Hadoop en la propiedad **outputs**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="1a29d-3003">Este conjunto de datos puede ser simplemente un conjunto de datos ficticio que es necesario para la programación de la canalización (por hora, diaria, etc.).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="1a29d-3004">Si la actividad no adopta una entrada, puede omitir la especificación de un conjunto de datos de entrada para la actividad en la propiedad **entradas**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="1a29d-3005">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="1a29d-3006">Para más información, consulte el artículo [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="1a29d-3007">Actividad de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="1a29d-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="1a29d-3008">Puede especificar las siguientes propiedades en una definición JSON de actividad de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="1a29d-3009">La propiedad de tipo de la actividad debe ser: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="1a29d-3010">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-3011">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en HDInsightSpark:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="1a29d-3012">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3012">Property</span></span> | <span data-ttu-id="1a29d-3013">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3013">Description</span></span> | <span data-ttu-id="1a29d-3014">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="1a29d-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-3015">rootPath</span></span> | <span data-ttu-id="1a29d-3016">Contenedor de blobs de Azure y la carpeta que contiene el archivo de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="1a29d-3017">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="1a29d-3018">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3018">Yes</span></span> |
| <span data-ttu-id="1a29d-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="1a29d-3019">entryFilePath</span></span> | <span data-ttu-id="1a29d-3020">Ruta de acceso relativa a la carpeta raíz del código o el paquete de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="1a29d-3021">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3021">Yes</span></span> |
| <span data-ttu-id="1a29d-3022">className</span><span class="sxs-lookup"><span data-stu-id="1a29d-3022">className</span></span> | <span data-ttu-id="1a29d-3023">Clase principal de Spark o Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="1a29d-3024">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3024">No</span></span> | 
| <span data-ttu-id="1a29d-3025">argumentos</span><span class="sxs-lookup"><span data-stu-id="1a29d-3025">arguments</span></span> | <span data-ttu-id="1a29d-3026">Lista de argumentos de línea de comandos del programa de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="1a29d-3027">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3027">No</span></span> | 
| <span data-ttu-id="1a29d-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="1a29d-3028">proxyUser</span></span> | <span data-ttu-id="1a29d-3029">Cuenta de usuario de suplantación para ejecutar el programa de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="1a29d-3030">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3030">No</span></span> | 
| <span data-ttu-id="1a29d-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="1a29d-3031">sparkConfig</span></span> | <span data-ttu-id="1a29d-3032">Propiedades de configuración de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3032">Spark configuration properties.</span></span> | <span data-ttu-id="1a29d-3033">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3033">No</span></span> | 
| <span data-ttu-id="1a29d-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="1a29d-3034">getDebugInfo</span></span> | <span data-ttu-id="1a29d-3035">Especifica si se copian los archivos de registro de Spark en el almacenamiento de Azure que usa el clúster de HDInsight que especifica sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="1a29d-3036">Valores permitidos: Ninguno, Siempre o Error.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="1a29d-3037">Valor predeterminado: Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3037">Default value: None.</span></span> | <span data-ttu-id="1a29d-3038">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3038">No</span></span> | 
| <span data-ttu-id="1a29d-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="1a29d-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="1a29d-3040">El servicio vinculado de Azure Storage que contiene los registros, las dependencias y los archivos de trabajos de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="1a29d-3041">Si no especifica un valor para esta propiedad, se usa el almacenamiento asociado con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="1a29d-3042">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="1a29d-3043">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="1a29d-3044">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3044">Note the following points:</span></span> 

- <span data-ttu-id="1a29d-3045">La propiedad de **tipo** se establece en **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="1a29d-3046">El valor de **rootPath** se establece en **adfspark\\pyFiles**, donde adfspark es el contenedor de Azure Blob y pyFiles es la carpeta adecuada en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="1a29d-3047">En este ejemplo, la instancia de Azure Blob Storage es la que está asociada con el clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="1a29d-3048">Puede cargar el archivo en un almacenamiento de Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="1a29d-3049">Si lo hace, cree un servicio vinculado de Azure Storage para vincular esa cuenta de almacenamiento con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="1a29d-3050">A continuación, especifique el nombre del servicio vinculado como un valor de la propiedad **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="1a29d-3051">Consulte las [propiedades de la actividad de Spark](#spark-activity-properties) para más detalles sobre esta y otras propiedades que admite la actividad de Spark.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="1a29d-3052">El valor de **entryFilePath** se establece en **test.py**, que es el archivo de Python.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="1a29d-3053">La propiedad **getDebugInfo** está establecida en **Siempre**, lo que significa que siempre se generan archivos de registro (acierto o error).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="1a29d-3054">Se recomienda que no establezca esta propiedad como Siempre en un entorno de producción, a menos que esté solucionando un problema.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="1a29d-3055">La sección de **salida** tiene un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="1a29d-3056">Debe especificar un conjunto de datos de salida, incluso si el programa de Spark no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="1a29d-3057">El conjunto de datos de salida impulsa la programación de la canalización (cada hora, cada día, etc.).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="1a29d-3058">Para más información sobre la actividad, consulte el artículo [Actividad de Spark](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="1a29d-3059">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a29d-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="1a29d-3060">Puede especificar las siguientes propiedades en una definición JSON de actividad de ejecución de lotes de Azure ML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="1a29d-3061">La propiedad de tipo de la actividad debe ser: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="1a29d-3062">Debe crear primero un servicio vinculado de Azure Machine Learning y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-3063">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en AzureMLBatchExecution:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="1a29d-3064">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3064">Property</span></span> | <span data-ttu-id="1a29d-3065">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3065">Description</span></span> | <span data-ttu-id="1a29d-3066">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="1a29d-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="1a29d-3067">webServiceInput</span></span> | <span data-ttu-id="1a29d-3068">El conjunto de datos que se pasará como entrada para el servicio web de Azure ML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="1a29d-3069">Este conjunto de datos también debe incluirse en las entradas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="1a29d-3070">Use webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="1a29d-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="1a29d-3071">webServiceInputs</span></span> | <span data-ttu-id="1a29d-3072">Especifique los conjuntos de datos que se van a pasar como entradas en el servicio web de Azure ML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="1a29d-3073">Si el servicio web toma varias entradas, use la propiedad webServiceInputs en lugar de usar webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="1a29d-3074">Los conjuntos de datos a los que hace referencia **webServiceInputs** también deben incluirse en las **entradas** de la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="1a29d-3075">Use webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="1a29d-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="1a29d-3076">webServiceOutputs</span></span> | <span data-ttu-id="1a29d-3077">Los conjuntos de datos que se asignan como salidas para el servicio web de Azure ML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="1a29d-3078">El servicio web devuelve los datos de salida en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="1a29d-3079">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3079">Yes</span></span> | 
<span data-ttu-id="1a29d-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-3080">globalParameters</span></span> | <span data-ttu-id="1a29d-3081">Especifique valores para los parámetros del servicio web en esta sección.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="1a29d-3082">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="1a29d-3083">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3083">JSON example</span></span>
<span data-ttu-id="1a29d-3084">En este ejemplo, la actividad tiene el conjunto de datos **MLSqlInput** como entrada y **MLSqlOutput** como salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="1a29d-3085">**MLSqlInput** se pasa como entrada al servicio web mediante la propiedad JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="1a29d-3086">**MLSqlOutput** se pasa como salida al servicio web mediante la propiedad JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="1a29d-3087">En el ejemplo JSON, el servicio web Azure Machine Learning implementado usa un módulo lector y otro escritor para leer y escribir datos desde y hacia una base de datos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="1a29d-3088">Este servicio web expone los cuatro parámetros siguientes: nombre de servidor de base de datos, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="1a29d-3089">Solo las entradas y salidas de la actividad AzureMLBatchExecution pueden pasarse como parámetros al servicio web.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="1a29d-3090">Por ejemplo, en el fragmento JSON anterior, MLSqlInput es una entrada a la actividad AzureMLBatchExecution, que se pasa como entrada al servicio web mediante el parámetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="1a29d-3091">Actividad de recursos de actualización de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a29d-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="1a29d-3092">Puede especificar las siguientes propiedades en una definición JSON de actividad de recursos de actualización de Azure ML.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="1a29d-3093">La propiedad de tipo de la actividad debe ser: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="1a29d-3094">Debe crear primero un servicio vinculado de Azure Machine Learning y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-3095">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en AzureMLUpdateResource:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="1a29d-3096">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3096">Property</span></span> | <span data-ttu-id="1a29d-3097">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3097">Description</span></span> | <span data-ttu-id="1a29d-3098">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="1a29d-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="1a29d-3099">trainedModelName</span></span> | <span data-ttu-id="1a29d-3100">Nombre del modelo reentrenado</span><span class="sxs-lookup"><span data-stu-id="1a29d-3100">Name of the retrained model.</span></span> | <span data-ttu-id="1a29d-3101">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3101">Yes</span></span> |  
<span data-ttu-id="1a29d-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="1a29d-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="1a29d-3103">Conjunto de datos que apunta al archivo iLearner devuelto por la operación de reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="1a29d-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="1a29d-3104">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="1a29d-3105">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3105">JSON example</span></span>
<span data-ttu-id="1a29d-3106">La canalización tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="1a29d-3107">La actividad Ejecución de lotes de Azure Machine Learning toma los datos de entrenamiento como entrada y genera como resultado un archivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="1a29d-3108">La actividad invoca el servicio web de entrenamiento (el experimento de entrenamiento expuesto como servicio web) con los datos de entrenamiento de entrada y recibe el archivo ilearner desde el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="1a29d-3109">El placeholderBlob es simplemente un conjunto de datos de salida ficticio que el servicio de Factoría de datos de Azure necesita para ejecutar la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="1a29d-3110">Actividad U-SQL de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a29d-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="1a29d-3111">Puede especificar las siguientes propiedades en una definición JSON de actividad de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="1a29d-3112">La propiedad de tipo de la actividad debe ser: **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="1a29d-3113">Debe crear un servicio vinculado de Azure Data Lake Analytics y especificar el nombre de este como un valor para la propiedad **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-3114">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en DataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="1a29d-3115">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3115">Property</span></span> | <span data-ttu-id="1a29d-3116">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3116">Description</span></span> | <span data-ttu-id="1a29d-3117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="1a29d-3118">scriptPath</span></span> |<span data-ttu-id="1a29d-3119">Ruta de acceso a la carpeta que contiene el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="1a29d-3120">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="1a29d-3121">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="1a29d-3121">No (if you use script)</span></span> |
| <span data-ttu-id="1a29d-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="1a29d-3122">scriptLinkedService</span></span> |<span data-ttu-id="1a29d-3123">Servicio vinculado que se vincula al almacenamiento que contiene el script para la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="1a29d-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="1a29d-3124">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="1a29d-3124">No (if you use script)</span></span> |
| <span data-ttu-id="1a29d-3125">script</span><span class="sxs-lookup"><span data-stu-id="1a29d-3125">script</span></span> |<span data-ttu-id="1a29d-3126">Especifique el script en línea en lugar de scriptPath y scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="1a29d-3127">Por ejemplo: "script": "Prueba CREAR BASE DE DATOS".</span><span class="sxs-lookup"><span data-stu-id="1a29d-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="1a29d-3128">No (si usa scriptPath y scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="1a29d-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="1a29d-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="1a29d-3129">degreeOfParallelism</span></span> |<span data-ttu-id="1a29d-3130">Número máximo de nodos que se usará de forma simultánea para ejecutar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="1a29d-3131">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3131">No</span></span> |
| <span data-ttu-id="1a29d-3132">prioridad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3132">priority</span></span> |<span data-ttu-id="1a29d-3133">Determina qué trabajos de todos los están en cola deben seleccionarse para ejecutarse primero.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="1a29d-3134">Cuanto menor sea el número, mayor será la prioridad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="1a29d-3135">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3135">No</span></span> |
| <span data-ttu-id="1a29d-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-3136">parameters</span></span> |<span data-ttu-id="1a29d-3137">Parámetros del script SQL U</span><span class="sxs-lookup"><span data-stu-id="1a29d-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="1a29d-3138">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="1a29d-3139">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="1a29d-3140">Para más información, consulte [Actividad de U-SQL de Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="1a29d-3141">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="1a29d-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="1a29d-3142">Puede especificar las siguientes propiedades en una definición JSON de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="1a29d-3143">La propiedad de tipo de la actividad debe ser: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="1a29d-3144">Debe crear uno de los siguientes servicios vinculados y especificar el nombre de este como un valor para la propiedad **linkedServiceName**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="1a29d-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a29d-3145">SQL Server</span></span> 
- <span data-ttu-id="1a29d-3146">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-3146">Azure SQL Database</span></span>
- <span data-ttu-id="1a29d-3147">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1a29d-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="1a29d-3148">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en SqlServerStoredProcedure:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="1a29d-3149">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3149">Property</span></span> | <span data-ttu-id="1a29d-3150">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3150">Description</span></span> | <span data-ttu-id="1a29d-3151">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a29d-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a29d-3152">storedProcedureName</span></span> |<span data-ttu-id="1a29d-3153">Especifique el nombre del procedimiento almacenado en la Base de datos SQL de Azure o en el Almacenamiento de datos SQL de Azure que se representa mediante el servicio vinculado que usa la tabla de salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="1a29d-3154">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3154">Yes</span></span> |
| <span data-ttu-id="1a29d-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a29d-3155">storedProcedureParameters</span></span> |<span data-ttu-id="1a29d-3156">Especifique valores para los parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="1a29d-3157">Si necesita pasar null para un parámetro, use la sintaxis: "param1": null (todo en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="1a29d-3158">Vea el ejemplo siguiente para aprender el uso de esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="1a29d-3159">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3159">No</span></span> |

<span data-ttu-id="1a29d-3160">Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para que se ejecute la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="1a29d-3161">El conjunto de datos de entrada no se puede usar en el procedimiento almacenado como parámetro.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="1a29d-3162">Solo se utiliza para comprobar la dependencia antes de iniciar la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="1a29d-3163">Debe especificar un conjunto de datos para una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="1a29d-3164">El conjunto de datos de salida especifica la **programación** para la actividad de procedimiento almacenada (por hora, semanal, mensual, etc.).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="1a29d-3165">El conjunto de datos de salida debe utilizar un **servicio vinculado** que haga referencia a una Base de datos SQL de Azure, un Almacenamiento de datos SQL o una base de datos de SQL Server donde desee que el procedimiento almacenado se ejecute.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="1a29d-3166">El conjunto de datos de salida puede usarse como una forma de pasar el resultado del procedimiento almacenado para su posterior procesamiento por otra actividad ([encadenamiento de actividades](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) en la canalización.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="1a29d-3167">Sin embargo, Data Factory no escribe automáticamente la salida de un procedimiento almacenado en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="1a29d-3168">Es el procedimiento almacenado el que escribe en una tabla SQL a la que apunta el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="1a29d-3169">En algunos casos, el conjunto de datos de salida puede ser un **conjunto de datos ficticio**, que solo se utilice para especificar la programación para ejecutar la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="1a29d-3170">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="1a29d-3171">Para más información, consulte el artículo [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="1a29d-3172">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="1a29d-3172">.NET custom activity</span></span>
<span data-ttu-id="1a29d-3173">Puede especificar las siguientes propiedades en una definición JSON de actividad personalizada de .NET.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="1a29d-3174">La propiedad de tipo de la actividad debe ser: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="1a29d-3175">Debe crear un servicio vinculado de Azure HDInsight o un servicio vinculado de Azure Batch y especificar el nombre de dicho servicio vinculado como un valor para la propiedad **linkedServiceName**:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="1a29d-3176">Se admiten las siguientes propiedades en la sección **typeProperties** cuando se establece el tipo de actividad en DotNetActivity:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="1a29d-3177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1a29d-3177">Property</span></span> | <span data-ttu-id="1a29d-3178">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a29d-3178">Description</span></span> | <span data-ttu-id="1a29d-3179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a29d-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1a29d-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="1a29d-3180">AssemblyName</span></span> | <span data-ttu-id="1a29d-3181">Nombre del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3181">Name of the assembly.</span></span> <span data-ttu-id="1a29d-3182">En el ejemplo, es: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="1a29d-3183">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3183">Yes</span></span> |
| <span data-ttu-id="1a29d-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="1a29d-3184">EntryPoint</span></span> |<span data-ttu-id="1a29d-3185">Nombre de la clase que implementa la interfaz IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="1a29d-3186">En el ejemplo, es: **MyDotNetActivityNS.MyDotNetActivity**, donde MyDotNetActivityNS es el espacio de nombres y MyDotNetActivity es la clase.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="1a29d-3187">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3187">Yes</span></span> | 
| <span data-ttu-id="1a29d-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="1a29d-3188">PackageLinkedService</span></span> | <span data-ttu-id="1a29d-3189">Nombre del servicio vinculado de Azure Storage que apunta a una instancia de Blob Storage que contiene el archivo ZIP de la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="1a29d-3190">En el ejemplo, es: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="1a29d-3191">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3191">Yes</span></span> |
| <span data-ttu-id="1a29d-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="1a29d-3192">PackageFile</span></span> | <span data-ttu-id="1a29d-3193">Nombre del archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3193">Name of the zip file.</span></span> <span data-ttu-id="1a29d-3194">En el ejemplo, es: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="1a29d-3195">Sí</span><span class="sxs-lookup"><span data-stu-id="1a29d-3195">Yes</span></span> |
| <span data-ttu-id="1a29d-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="1a29d-3196">extendedProperties</span></span> | <span data-ttu-id="1a29d-3197">Propiedades extendidas que puede definir y pasar a código .NET.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="1a29d-3198">En este ejemplo, la variable **SliceStart** se establece en un valor basado en la variable del sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1a29d-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="1a29d-3199">No</span><span class="sxs-lookup"><span data-stu-id="1a29d-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="1a29d-3200">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1a29d-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="1a29d-3201">Para obtener información detallada, vea el artículo [Uso de actividades personalizadas en Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1a29d-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1a29d-3202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a29d-3202">Next Steps</span></span>
<span data-ttu-id="1a29d-3203">Vea los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="1a29d-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="1a29d-3204">Tutorial: crear una canalización con la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1a29d-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="1a29d-3205">Tutorial: crear una canalización con la actividad de hive</span><span class="sxs-lookup"><span data-stu-id="1a29d-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)