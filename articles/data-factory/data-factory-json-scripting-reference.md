---
title: "aaaAzure factoría de datos: referencia de scripts JSON | Documentos de Microsoft"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="149d7-103">Azure Data Factory - Referencia de scripting JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="149d7-104">Este artículo proporciona ejemplos y esquemas JSON para definir entidades de Azure Data Factory (canalización, actividad, conjunto de datos y servicio vinculado).</span><span class="sxs-lookup"><span data-stu-id="149d7-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="149d7-105">Canalización</span><span class="sxs-lookup"><span data-stu-id="149d7-105">Pipeline</span></span> 
<span data-ttu-id="149d7-106">estructura de alto nivel de Hola para una definición de la canalización es como sigue:</span><span class="sxs-lookup"><span data-stu-id="149d7-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="149d7-107">Tabla siguiente describe las propiedades de hello dentro de la canalización de hello definición JSON:</span><span class="sxs-lookup"><span data-stu-id="149d7-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="149d7-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-108">Property</span></span> | <span data-ttu-id="149d7-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-109">Description</span></span> | <span data-ttu-id="149d7-110">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="149d7-111">name</span><span class="sxs-lookup"><span data-stu-id="149d7-111">name</span></span> | <span data-ttu-id="149d7-112">Nombre de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-112">Name of hello pipeline.</span></span> <span data-ttu-id="149d7-113">Especifique un nombre que representa la acción de Hola que Hola actividad o canalización es toodo configurado</span><span class="sxs-lookup"><span data-stu-id="149d7-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="149d7-114">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="149d7-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="149d7-115">Debe empezar en una letra, un número o un carácter de subrayado (_)</span><span class="sxs-lookup"><span data-stu-id="149d7-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="149d7-116">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="149d7-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="149d7-117">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-117">Yes</span></span> |
| <span data-ttu-id="149d7-118">description</span><span class="sxs-lookup"><span data-stu-id="149d7-118">description</span></span> |<span data-ttu-id="149d7-119">Texto que describe qué actividad hello o canalización se usa para</span><span class="sxs-lookup"><span data-stu-id="149d7-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="149d7-120">No</span><span class="sxs-lookup"><span data-stu-id="149d7-120">No</span></span> |
| <span data-ttu-id="149d7-121">actividades</span><span class="sxs-lookup"><span data-stu-id="149d7-121">activities</span></span> | <span data-ttu-id="149d7-122">Contiene una lista de actividades.</span><span class="sxs-lookup"><span data-stu-id="149d7-122">Contains a list of activities.</span></span> | <span data-ttu-id="149d7-123">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-123">Yes</span></span> |
| <span data-ttu-id="149d7-124">start</span><span class="sxs-lookup"><span data-stu-id="149d7-124">start</span></span> |<span data-ttu-id="149d7-125">Fecha y hora de inicio de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="149d7-126">Debe estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="149d7-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="149d7-127">Por ejemplo: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="149d7-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="149d7-128">Es posible toospecify una hora local, por ejemplo una hora EST.</span><span class="sxs-lookup"><span data-stu-id="149d7-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="149d7-129">Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.</span><span class="sxs-lookup"><span data-stu-id="149d7-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="149d7-130">Hello propiedades start y end juntos especifican el período activo de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="149d7-131">Los segmentos de salida solo se producen en este período activo.</span><span class="sxs-lookup"><span data-stu-id="149d7-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="149d7-132">No</span><span class="sxs-lookup"><span data-stu-id="149d7-132">No</span></span><br/><br/><span data-ttu-id="149d7-133">Si especifica un valor para la propiedad de finalización de hello, debe especificar el valor de propiedad de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="149d7-134">Hello horas de inicio y finalización tanto pueden ser toocreate vacía una canalización.</span><span class="sxs-lookup"><span data-stu-id="149d7-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="149d7-135">Debe especificar ambos valores tooset un período activo de hello canalización toorun.</span><span class="sxs-lookup"><span data-stu-id="149d7-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="149d7-136">Si no especifica horas de inicio y finalización al crear una canalización, puede establecerlas mediante cmdlet Hola conjunto AzureRmDataFactoryPipelineActivePeriod más tarde.</span><span class="sxs-lookup"><span data-stu-id="149d7-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="149d7-137">end</span><span class="sxs-lookup"><span data-stu-id="149d7-137">end</span></span> |<span data-ttu-id="149d7-138">Fecha y hora de final de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="149d7-139">Si se especifica, debe estar en formato ISO.</span><span class="sxs-lookup"><span data-stu-id="149d7-139">If specified must be in ISO format.</span></span> <span data-ttu-id="149d7-140">Por ejemplo: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="149d7-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="149d7-141">Es posible toospecify una hora local, por ejemplo una hora EST.</span><span class="sxs-lookup"><span data-stu-id="149d7-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="149d7-142">Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.</span><span class="sxs-lookup"><span data-stu-id="149d7-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="149d7-143">canalización de hello toorun indefinidamente, especifique 9999-09-09 como valor de hello para la propiedad de finalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="149d7-144">No</span><span class="sxs-lookup"><span data-stu-id="149d7-144">No</span></span> <br/><br/><span data-ttu-id="149d7-145">Si especifica un valor para la propiedad de inicio de hello, debe especificar el valor de propiedad de finalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="149d7-146">Vea las notas de hello **iniciar** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="149d7-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="149d7-147">isPaused</span></span> |<span data-ttu-id="149d7-148">Si no se ejecuta la canalización de conjunto tootrue Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="149d7-149">Valor predeterminado = false.</span><span class="sxs-lookup"><span data-stu-id="149d7-149">Default value = false.</span></span> <span data-ttu-id="149d7-150">Puede usar esta propiedad tooenable o deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="149d7-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="149d7-151">No</span><span class="sxs-lookup"><span data-stu-id="149d7-151">No</span></span> |
| <span data-ttu-id="149d7-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="149d7-152">pipelineMode</span></span> |<span data-ttu-id="149d7-153">método Hello para la programación se ejecuta para la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="149d7-154">Los valores permitidos son: scheduled (predeterminado).</span><span class="sxs-lookup"><span data-stu-id="149d7-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="149d7-155">'Programada' indica que esa canalización Hola se ejecuta en un intervalo de tiempo especificado según el período activo de tooits (hora de inicio y final).</span><span class="sxs-lookup"><span data-stu-id="149d7-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="149d7-156">'Tendrá que repetir' indica que esa canalización Hola se ejecuta solo una vez.</span><span class="sxs-lookup"><span data-stu-id="149d7-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="149d7-157">Las canalizaciones creadas una sola vez no se pueden modificar ni actualizar actualmente.</span><span class="sxs-lookup"><span data-stu-id="149d7-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="149d7-158">Consulte la sección [Canalización de una vez](data-factory-create-pipelines.md#onetime-pipeline) para más información acerca de la configuración onetime.</span><span class="sxs-lookup"><span data-stu-id="149d7-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="149d7-159">No</span><span class="sxs-lookup"><span data-stu-id="149d7-159">No</span></span> |
| <span data-ttu-id="149d7-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="149d7-160">expirationTime</span></span> |<span data-ttu-id="149d7-161">Duración de tiempo después de la creación de qué Hola canalización es válida y debe permanecer aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="149d7-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="149d7-162">Si no tiene ningún activo, error, o pendientes se ejecuta, la canalización de Hola se elimina automáticamente una vez que llega la hora de expiración de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="149d7-163">No</span><span class="sxs-lookup"><span data-stu-id="149d7-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="149d7-164">Actividad</span><span class="sxs-lookup"><span data-stu-id="149d7-164">Activity</span></span> 
<span data-ttu-id="149d7-165">estructura de alto nivel de Hola para una actividad dentro de una definición de canalización (elemento de actividades) es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="149d7-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="149d7-166">Tabla siguiente describen las propiedades de hello dentro de la actividad de hello definición JSON:</span><span class="sxs-lookup"><span data-stu-id="149d7-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="149d7-167">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="149d7-167">Tag</span></span> | <span data-ttu-id="149d7-168">Description</span><span class="sxs-lookup"><span data-stu-id="149d7-168">Description</span></span> | <span data-ttu-id="149d7-169">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-170">name</span><span class="sxs-lookup"><span data-stu-id="149d7-170">name</span></span> |<span data-ttu-id="149d7-171">Nombre de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-171">Name of hello activity.</span></span> <span data-ttu-id="149d7-172">Especifique un nombre que representa la acción Hola actividad hello configura toodo</span><span class="sxs-lookup"><span data-stu-id="149d7-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="149d7-173">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="149d7-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="149d7-174">Debe empezar en una letra, un número o un carácter de subrayado (_)</span><span class="sxs-lookup"><span data-stu-id="149d7-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="149d7-175">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="149d7-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="149d7-176">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-176">Yes</span></span> |
| <span data-ttu-id="149d7-177">description</span><span class="sxs-lookup"><span data-stu-id="149d7-177">description</span></span> |<span data-ttu-id="149d7-178">Texto que describe qué actividad Hola se usa para.</span><span class="sxs-lookup"><span data-stu-id="149d7-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="149d7-179">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-179">Yes</span></span> |
| <span data-ttu-id="149d7-180">type</span><span class="sxs-lookup"><span data-stu-id="149d7-180">type</span></span> |<span data-ttu-id="149d7-181">Especifica el tipo de saludo de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="149d7-182">Vea hello [almacenes de datos](#data-stores) y [las actividades de transformación de datos](#data-transformation-activities) secciones para diferentes tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="149d7-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="149d7-183">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-183">Yes</span></span> |
| <span data-ttu-id="149d7-184">inputs</span><span class="sxs-lookup"><span data-stu-id="149d7-184">inputs</span></span> |<span data-ttu-id="149d7-185">Tablas de entrada utilizadas por actividad hello</span><span class="sxs-lookup"><span data-stu-id="149d7-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="149d7-186">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-186">Yes</span></span> |
| <span data-ttu-id="149d7-187">outputs</span><span class="sxs-lookup"><span data-stu-id="149d7-187">outputs</span></span> |<span data-ttu-id="149d7-188">Tablas de salida utilizadas por actividad hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="149d7-189">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-189">Yes</span></span> |
| <span data-ttu-id="149d7-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="149d7-190">linkedServiceName</span></span> |<span data-ttu-id="149d7-191">Nombre del servicio de hello vinculado utilizado por actividad hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="149d7-192">Una actividad puede requerir que especifique servicio Hola vinculado que se vincula el entorno de proceso necesarios toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="149d7-193">Sí para las actividades de HDInsight, las actividades de Azure Machine Learning y las actividades del procedimiento almacenadas.</span><span class="sxs-lookup"><span data-stu-id="149d7-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="149d7-194">No para todos los demás</span><span class="sxs-lookup"><span data-stu-id="149d7-194">No for all others</span></span> |
| <span data-ttu-id="149d7-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="149d7-195">typeProperties</span></span> |<span data-ttu-id="149d7-196">Propiedades de hello typeProperties sección dependen del tipo de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="149d7-197">No</span><span class="sxs-lookup"><span data-stu-id="149d7-197">No</span></span> |
| <span data-ttu-id="149d7-198">policy</span><span class="sxs-lookup"><span data-stu-id="149d7-198">policy</span></span> |<span data-ttu-id="149d7-199">Directivas que afectan al comportamiento de tiempo de ejecución de Hola de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="149d7-200">Si no se especifica, se usan las directivas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="149d7-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="149d7-201">No</span><span class="sxs-lookup"><span data-stu-id="149d7-201">No</span></span> |
| <span data-ttu-id="149d7-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="149d7-202">scheduler</span></span> |<span data-ttu-id="149d7-203">propiedad "programador" es usado toodefine deseado de programación para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="149d7-204">Sus subpropiedades se Hola igual que los de Hola Hola [propiedad de disponibilidad en un conjunto de datos](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="149d7-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="149d7-205">No</span><span class="sxs-lookup"><span data-stu-id="149d7-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="149d7-206">Directivas</span><span class="sxs-lookup"><span data-stu-id="149d7-206">Policies</span></span>
<span data-ttu-id="149d7-207">Las directivas afectan al comportamiento de tiempo de ejecución de Hola de una actividad, específicamente cuando se procesa el sector de Hola de una tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="149d7-208">Hello en la tabla siguiente proporciona detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="149d7-209">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-209">Property</span></span> | <span data-ttu-id="149d7-210">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-210">Permitted values</span></span> | <span data-ttu-id="149d7-211">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-211">Default Value</span></span> | <span data-ttu-id="149d7-212">Description</span><span class="sxs-lookup"><span data-stu-id="149d7-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-213">simultaneidad</span><span class="sxs-lookup"><span data-stu-id="149d7-213">concurrency</span></span> |<span data-ttu-id="149d7-214">Entero </span><span class="sxs-lookup"><span data-stu-id="149d7-214">Integer</span></span> <br/><br/><span data-ttu-id="149d7-215">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="149d7-215">Max value: 10</span></span> |<span data-ttu-id="149d7-216">1</span><span class="sxs-lookup"><span data-stu-id="149d7-216">1</span></span> |<span data-ttu-id="149d7-217">Número de ejecuciones simultáneas de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="149d7-218">Determina el número de Hola de ejecuciones paralelas que pueden ocurrir en distintos sectores.</span><span class="sxs-lookup"><span data-stu-id="149d7-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="149d7-219">Por ejemplo, si una actividad tiene toogo a través de un conjunto grande de datos disponibles, que tienen un valor mayor de simultaneidad acelera el procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="149d7-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="149d7-220">executionPriorityOrder</span></span> |<span data-ttu-id="149d7-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="149d7-221">NewestFirst</span></span><br/><br/><span data-ttu-id="149d7-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="149d7-222">OldestFirst</span></span> |<span data-ttu-id="149d7-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="149d7-223">OldestFirst</span></span> |<span data-ttu-id="149d7-224">Determina Hola orden de los segmentos de datos que se están procesando.</span><span class="sxs-lookup"><span data-stu-id="149d7-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="149d7-225">Por ejemplo, si tiene 2 segmentos (que tienen lugar uno a las 4 p.m. y el otro a las 5 p.m.) y ambos están pendientes de ejecución.</span><span class="sxs-lookup"><span data-stu-id="149d7-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="149d7-226">Si establece hello executionPriorityOrder toobe NewestFirst, segmento de Hola a las 5 P.M. se procesa en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="149d7-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="149d7-227">De forma similar si establece hello executionPriorityORder toobe OldestFIrst, segmento de Hola a las 4 P.M. se procesa.</span><span class="sxs-lookup"><span data-stu-id="149d7-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="149d7-228">retry</span><span class="sxs-lookup"><span data-stu-id="149d7-228">retry</span></span> |<span data-ttu-id="149d7-229">Entero </span><span class="sxs-lookup"><span data-stu-id="149d7-229">Integer</span></span><br/><br/><span data-ttu-id="149d7-230">El valor máximo permitido es 10</span><span class="sxs-lookup"><span data-stu-id="149d7-230">Max value can be 10</span></span> |<span data-ttu-id="149d7-231">0</span><span class="sxs-lookup"><span data-stu-id="149d7-231">0</span></span> |<span data-ttu-id="149d7-232">Número de reintentos antes del procesamiento de datos de hello para el segmento de Hola se marca como completada con errores.</span><span class="sxs-lookup"><span data-stu-id="149d7-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="149d7-233">Ejecución de actividad para un segmento de datos se vuelve a intentar la toohello especificada número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="149d7-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="149d7-234">Hola reintento se realiza tan pronto como sea posible después de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="149d7-235">timeout</span><span class="sxs-lookup"><span data-stu-id="149d7-235">timeout</span></span> |<span data-ttu-id="149d7-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="149d7-236">TimeSpan</span></span> |<span data-ttu-id="149d7-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="149d7-237">00:00:00</span></span> |<span data-ttu-id="149d7-238">Tiempo de espera para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-238">Timeout for hello activity.</span></span> <span data-ttu-id="149d7-239">Ejemplo: 00:10:00 (implica un tiempo de espera de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="149d7-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="149d7-240">Si un valor no se especifica o es 0, el tiempo de espera de hello es infinito.</span><span class="sxs-lookup"><span data-stu-id="149d7-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="149d7-241">Si el tiempo de procesamiento de datos de hello en un sector supera el valor de tiempo de espera de hello, que se cancele y sistema de hello trata el procesamiento de hello tooretry.</span><span class="sxs-lookup"><span data-stu-id="149d7-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="149d7-242">número de Hola de reintentos depende de la propiedad de reintento de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="149d7-243">Cuando se produce el tiempo de espera, el estado de Hola se establece tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="149d7-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="149d7-244">delay</span><span class="sxs-lookup"><span data-stu-id="149d7-244">delay</span></span> |<span data-ttu-id="149d7-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="149d7-245">TimeSpan</span></span> |<span data-ttu-id="149d7-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="149d7-246">00:00:00</span></span> |<span data-ttu-id="149d7-247">Especificar el retraso de hello antes del procesamiento de datos de segmento Hola se inicia.</span><span class="sxs-lookup"><span data-stu-id="149d7-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="149d7-248">se inicia la ejecución de Hola de actividad para un segmento de datos una vez Hola retraso pasado Hola espera el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="149d7-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="149d7-249">Ejemplo: 00:10:00 (implica un retraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="149d7-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="149d7-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="149d7-250">longRetry</span></span> |<span data-ttu-id="149d7-251">Entero </span><span class="sxs-lookup"><span data-stu-id="149d7-251">Integer</span></span><br/><br/><span data-ttu-id="149d7-252">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="149d7-252">Max value: 10</span></span> |<span data-ttu-id="149d7-253">1</span><span class="sxs-lookup"><span data-stu-id="149d7-253">1</span></span> |<span data-ttu-id="149d7-254">número de Hola de reintentos largos intentos antes de que se error al ejecutar el segmento Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="149d7-255">Los intentos de longRetry se espacian de acuerdo a longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="149d7-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="149d7-256">Por lo que si necesita toospecify un tiempo entre los reintentos, utilice longRetry.</span><span class="sxs-lookup"><span data-stu-id="149d7-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="149d7-257">Si se especifican Retry y longRetry, cada intento de longRetry incluye los intentos de reintento y número máximo de Hola de intentos es reintento * longRetry.</span><span class="sxs-lookup"><span data-stu-id="149d7-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="149d7-258">Por ejemplo, si tenemos Hola después de la configuración de directiva de actividad de hello:</span><span class="sxs-lookup"><span data-stu-id="149d7-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="149d7-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="149d7-259">Retry: 3</span></span><br/><span data-ttu-id="149d7-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="149d7-260">longRetry: 2</span></span><br/><span data-ttu-id="149d7-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="149d7-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="149d7-262">Suponemos que hay solo un tooexecute de segmento (estado de espera) y ejecución de la actividad de Hola se produce un error cada vez.</span><span class="sxs-lookup"><span data-stu-id="149d7-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="149d7-263">Inicialmente habría tres intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="149d7-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="149d7-264">Después de cada intento, estado del sector Hola sería Retry.</span><span class="sxs-lookup"><span data-stu-id="149d7-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="149d7-265">Después de 3 primeros intentos superan el tiempo de espera, estado del sector Hola sería LongRetry.</span><span class="sxs-lookup"><span data-stu-id="149d7-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="149d7-266">Después de una hora (es decir, el valor de longRetryInteval), se produciría otro conjunto de 3 intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="149d7-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="149d7-267">Después de eso, el estado del sector de hello podría ser Failed y no podría realizarse ningún reintento más.</span><span class="sxs-lookup"><span data-stu-id="149d7-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="149d7-268">Por tanto, en total se realizaron 6 intentos.</span><span class="sxs-lookup"><span data-stu-id="149d7-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="149d7-269">Si cualquier ejecución se realiza correctamente, el estado del sector de hello sería Ready y no se realiza ningún reintento más.</span><span class="sxs-lookup"><span data-stu-id="149d7-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="149d7-270">longRetry puede utilizarse en situaciones donde llegan datos dependientes en momentos no determinista o hello entorno general es inestable en el procesamiento de datos que se produce.</span><span class="sxs-lookup"><span data-stu-id="149d7-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="149d7-271">En tales casos, no es útil realizar reintentos uno tras otro y hacerlo después de un intervalo de tiempo provoca Hola deseado de salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="149d7-272">Advertencia: No establezca valores altos para longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="149d7-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="149d7-273">Normalmente, los valores más altos implican otros problemas sistémicos.</span><span class="sxs-lookup"><span data-stu-id="149d7-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="149d7-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="149d7-274">longRetryInterval</span></span> |<span data-ttu-id="149d7-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="149d7-275">TimeSpan</span></span> |<span data-ttu-id="149d7-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="149d7-276">00:00:00</span></span> |<span data-ttu-id="149d7-277">retraso de Hello entre reintentos largos</span><span class="sxs-lookup"><span data-stu-id="149d7-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="149d7-278">Sección typeProperties</span><span class="sxs-lookup"><span data-stu-id="149d7-278">typeProperties section</span></span>
<span data-ttu-id="149d7-279">sección de typeProperties Hello es diferente para cada actividad.</span><span class="sxs-lookup"><span data-stu-id="149d7-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="149d7-280">Las actividades de transformación tienen propiedades de tipo hello solo.</span><span class="sxs-lookup"><span data-stu-id="149d7-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="149d7-281">Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización.</span><span class="sxs-lookup"><span data-stu-id="149d7-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="149d7-282">**Actividad de copia** tiene dos subsecciones de sección de Hola typeProperties: **origen** y **receptor**.</span><span class="sxs-lookup"><span data-stu-id="149d7-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="149d7-283">Vea [almacenes de datos](#data-stores) sección en este artículo para JSON ejemplos que muestran cómo almacenar toouse datos como un origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="149d7-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="149d7-284">Canalización de copia de ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-284">Sample copy pipeline</span></span>
<span data-ttu-id="149d7-285">Hola después de canalización de ejemplo, hay una actividad de tipo **copia** en hello **actividades** sección.</span><span class="sxs-lookup"><span data-stu-id="149d7-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="149d7-286">En este ejemplo, Hola [actividad de copia](data-factory-data-movement-activities.md) copia datos de una base de datos de SQL Azure del tooan de almacenamiento Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="149d7-287">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="149d7-287">Note hello following points:</span></span>

* <span data-ttu-id="149d7-288">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="149d7-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="149d7-289">Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="149d7-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="149d7-290">Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="149d7-291">Vea [almacenes de datos](#data-stores) sección en este artículo para JSON ejemplos que muestran cómo almacenar toouse datos como un origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="149d7-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="149d7-292">Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="149d7-293">Canalización de transformación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-293">Sample transformation pipeline</span></span>
<span data-ttu-id="149d7-294">Hola después de canalización de ejemplo, hay una actividad de tipo **HDInsightHive** en hello **actividades** sección.</span><span class="sxs-lookup"><span data-stu-id="149d7-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="149d7-295">En este ejemplo, Hola [actividad de HDInsight Hive](data-factory-hive-activity.md) transforma los datos de un almacenamiento de blobs de Azure mediante la ejecución de un archivo de script de Hive en un clúster de Hadoop de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="149d7-296">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="149d7-296">Note hello following points:</span></span> 

* <span data-ttu-id="149d7-297">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="149d7-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="149d7-298">archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **AzureStorageLinkedService**) y en  **secuencia de comandos** carpeta en el contenedor de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="149d7-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="149d7-299">Hola **define** sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="149d7-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="149d7-300">Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización.</span><span class="sxs-lookup"><span data-stu-id="149d7-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="149d7-301">Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: generar los datos primera canalización tooprocess con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="149d7-302">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-302">Linked service</span></span>
<span data-ttu-id="149d7-303">estructura de alto nivel de Hola para una definición de servicio vinculado es como sigue:</span><span class="sxs-lookup"><span data-stu-id="149d7-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="149d7-304">Tabla siguiente describen las propiedades de hello dentro de la actividad de hello definición JSON:</span><span class="sxs-lookup"><span data-stu-id="149d7-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="149d7-305">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-305">Property</span></span> | <span data-ttu-id="149d7-306">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-306">Description</span></span> | <span data-ttu-id="149d7-307">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="149d7-308">name</span><span class="sxs-lookup"><span data-stu-id="149d7-308">name</span></span> | <span data-ttu-id="149d7-309">Nombre del servicio de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-309">Name of hello linked service.</span></span> | <span data-ttu-id="149d7-310">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-310">Yes</span></span> | 
| <span data-ttu-id="149d7-311">propiedades - tipo</span><span class="sxs-lookup"><span data-stu-id="149d7-311">properties - type</span></span> | <span data-ttu-id="149d7-312">Tipo de servicio de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-312">Type of hello linked service.</span></span> <span data-ttu-id="149d7-313">Por ejemplo: Azure Storage o Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="149d7-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="149d7-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="149d7-314">typeProperties</span></span> | <span data-ttu-id="149d7-315">sección de typeProperties Hello tiene elementos que son diferentes para cada almacén de datos o el entorno de proceso.</span><span class="sxs-lookup"><span data-stu-id="149d7-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="149d7-316">Vea [almacenes de datos](#datastores) sección para todos los datos de hello almacenan servicios vinculados y [proceso entornos](#compute-environments) para hello todos los servicios vinculados de proceso</span><span class="sxs-lookup"><span data-stu-id="149d7-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="149d7-317">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-317">Dataset</span></span> 
<span data-ttu-id="149d7-318">Un conjunto de datos en Data Factory de Azure se define como sigue:</span><span class="sxs-lookup"><span data-stu-id="149d7-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="149d7-319">Hello en la tabla siguiente describe propiedades Hola anterior JSON:</span><span class="sxs-lookup"><span data-stu-id="149d7-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="149d7-320">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-320">Property</span></span> | <span data-ttu-id="149d7-321">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-321">Description</span></span> | <span data-ttu-id="149d7-322">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-322">Required</span></span> | <span data-ttu-id="149d7-323">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-324">name</span><span class="sxs-lookup"><span data-stu-id="149d7-324">name</span></span> | <span data-ttu-id="149d7-325">Nombre del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-325">Name of hello dataset.</span></span> <span data-ttu-id="149d7-326">Consulte [Azure Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para ver este tipo de reglas.</span><span class="sxs-lookup"><span data-stu-id="149d7-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="149d7-327">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-327">Yes</span></span> |<span data-ttu-id="149d7-328">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-328">NA</span></span> |
| <span data-ttu-id="149d7-329">type</span><span class="sxs-lookup"><span data-stu-id="149d7-329">type</span></span> | <span data-ttu-id="149d7-330">Tipo de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-330">Type of hello dataset.</span></span> <span data-ttu-id="149d7-331">Especifique uno de los tipos de hello compatibles con Data Factory de Azure (por ejemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="149d7-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="149d7-332">Vea [almacenes de datos](#data-stores) sección de Hola a todos los tipos de conjunto de datos admitidos por el generador de datos y almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="149d7-333">structure</span><span class="sxs-lookup"><span data-stu-id="149d7-333">structure</span></span> | <span data-ttu-id="149d7-334">Esquema del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-334">Schema of hello dataset.</span></span> <span data-ttu-id="149d7-335">Contiene las columnas, sus tipos, etc.</span><span class="sxs-lookup"><span data-stu-id="149d7-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="149d7-336">No</span><span class="sxs-lookup"><span data-stu-id="149d7-336">No</span></span> |<span data-ttu-id="149d7-337">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-337">NA</span></span> |
| <span data-ttu-id="149d7-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="149d7-338">typeProperties</span></span> | <span data-ttu-id="149d7-339">Propiedades que corresponden toohello el tipo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="149d7-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="149d7-340">Vea la sección [ALMACENES DE DATOS](#data-stores) para consultar los tipos admitidos y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="149d7-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="149d7-341">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-341">Yes</span></span> |<span data-ttu-id="149d7-342">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-342">NA</span></span> |
| <span data-ttu-id="149d7-343">external</span><span class="sxs-lookup"><span data-stu-id="149d7-343">external</span></span> | <span data-ttu-id="149d7-344">Un valor booleano marca toospecify si una canalización del generador de datos explícitamente genera un conjunto de datos o no.</span><span class="sxs-lookup"><span data-stu-id="149d7-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="149d7-345">No</span><span class="sxs-lookup"><span data-stu-id="149d7-345">No</span></span> |<span data-ttu-id="149d7-346">false</span><span class="sxs-lookup"><span data-stu-id="149d7-346">false</span></span> |
| <span data-ttu-id="149d7-347">availability</span><span class="sxs-lookup"><span data-stu-id="149d7-347">availability</span></span> | <span data-ttu-id="149d7-348">Define Hola Hola segmentar el modelo para la producción de hello conjunto de datos o la ventana de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="149d7-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="149d7-349">Para obtener detalles sobre el conjunto de datos de hello segmentar el modelo, vea [ejecución y programación](data-factory-scheduling-and-execution.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="149d7-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="149d7-350">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-350">Yes</span></span> |<span data-ttu-id="149d7-351">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-351">NA</span></span> |
| <span data-ttu-id="149d7-352">policy</span><span class="sxs-lookup"><span data-stu-id="149d7-352">policy</span></span> |<span data-ttu-id="149d7-353">Define los criterios de Hola o condición de Hola que deben cumplir los segmentos del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="149d7-354">Para más información, consulte la sección [Directiva del conjunto de datos](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="149d7-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="149d7-355">No</span><span class="sxs-lookup"><span data-stu-id="149d7-355">No</span></span> |<span data-ttu-id="149d7-356">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-356">NA</span></span> |

<span data-ttu-id="149d7-357">Cada columna de hello **estructura** sección contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="149d7-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="149d7-358">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-358">Property</span></span> | <span data-ttu-id="149d7-359">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-359">Description</span></span> | <span data-ttu-id="149d7-360">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-361">name</span><span class="sxs-lookup"><span data-stu-id="149d7-361">name</span></span> |<span data-ttu-id="149d7-362">Nombre de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-362">Name of hello column.</span></span> |<span data-ttu-id="149d7-363">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-363">Yes</span></span> |
| <span data-ttu-id="149d7-364">type</span><span class="sxs-lookup"><span data-stu-id="149d7-364">type</span></span> |<span data-ttu-id="149d7-365">Tipo de datos de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-365">Data type of hello column.</span></span>  |<span data-ttu-id="149d7-366">No</span><span class="sxs-lookup"><span data-stu-id="149d7-366">No</span></span> |
| <span data-ttu-id="149d7-367">culture</span><span class="sxs-lookup"><span data-stu-id="149d7-367">culture</span></span> |<span data-ttu-id="149d7-368">Toobe de referencia cultural que se usa cuando el tipo se especifica y es de tipo .NET basadas en .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="149d7-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="149d7-369">El valor predeterminado es `en-us`.</span><span class="sxs-lookup"><span data-stu-id="149d7-369">Default is `en-us`.</span></span> |<span data-ttu-id="149d7-370">No</span><span class="sxs-lookup"><span data-stu-id="149d7-370">No</span></span> |
| <span data-ttu-id="149d7-371">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-371">format</span></span> |<span data-ttu-id="149d7-372">Dar formato a toobe de cadena que se usa cuando el tipo se especifica y es de tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="149d7-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="149d7-373">No</span><span class="sxs-lookup"><span data-stu-id="149d7-373">No</span></span> |

<span data-ttu-id="149d7-374">En el siguiente ejemplo de Hola, conjunto de datos de hello tiene tres columnas `slicetimestamp`, `projectname`, y `pageviews` y son del tipo: cadena, cadena y Decimal respectivamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="149d7-375">Hello tabla siguiente describen propiedades que puede utilizar en hello **disponibilidad** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="149d7-376">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-376">Property</span></span> | <span data-ttu-id="149d7-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-377">Description</span></span> | <span data-ttu-id="149d7-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-378">Required</span></span> | <span data-ttu-id="149d7-379">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-380">frequency</span><span class="sxs-lookup"><span data-stu-id="149d7-380">frequency</span></span> |<span data-ttu-id="149d7-381">Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="149d7-382"><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="149d7-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="149d7-383">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-383">Yes</span></span> |<span data-ttu-id="149d7-384">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-384">NA</span></span> |
| <span data-ttu-id="149d7-385">interval</span><span class="sxs-lookup"><span data-stu-id="149d7-385">interval</span></span> |<span data-ttu-id="149d7-386">Especifica un multiplicador para frecuencia</span><span class="sxs-lookup"><span data-stu-id="149d7-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="149d7-387">"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera.</span><span class="sxs-lookup"><span data-stu-id="149d7-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="149d7-388">Si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="149d7-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="149d7-389"><b>Tenga en cuenta</b>: si especifica frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15</span><span class="sxs-lookup"><span data-stu-id="149d7-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="149d7-390">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-390">Yes</span></span> |<span data-ttu-id="149d7-391">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-391">NA</span></span> |
| <span data-ttu-id="149d7-392">style</span><span class="sxs-lookup"><span data-stu-id="149d7-392">style</span></span> |<span data-ttu-id="149d7-393">Especifica si se debe generar segmento hello en hello inicio/final del intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="149d7-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="149d7-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="149d7-394">StartOfInterval</span></span></li><li><span data-ttu-id="149d7-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="149d7-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="149d7-396">Si se establece la frecuencia de tooMonth y se establece el estilo tooEndOfInterval, Hola segmento se genera Hola último día del mes.</span><span class="sxs-lookup"><span data-stu-id="149d7-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="149d7-397">Si se establece tooStartOfInterval en estilo de hello, Hola segmento se genera en hello primer día del mes.</span><span class="sxs-lookup"><span data-stu-id="149d7-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="149d7-398">Si se establece la frecuencia de tooDay y se establece el estilo tooEndOfInterval, segmento de Hola se genera en la última hora del día de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="149d7-399">Si se establece la frecuencia de tooHour y se establece el estilo tooEndOfInterval, segmento de Hola se genera al final de Hola de hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="149d7-400">Por ejemplo, para un intervalo durante el período de 1 P.M. – 2 P.M., segmento de Hola se genera a las 2 P.M..</span><span class="sxs-lookup"><span data-stu-id="149d7-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="149d7-401">No</span><span class="sxs-lookup"><span data-stu-id="149d7-401">No</span></span> |<span data-ttu-id="149d7-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="149d7-402">EndOfInterval</span></span> |
| <span data-ttu-id="149d7-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="149d7-403">anchorDateTime</span></span> |<span data-ttu-id="149d7-404">Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de programador toocompute conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="149d7-405"><b>Tenga en cuenta</b>: si hello AnchorDateTime tiene Dateparts más granulares que la frecuencia de hello, hello partes más pormenorizadas se omiten.</span><span class="sxs-lookup"><span data-stu-id="149d7-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="149d7-406">Por ejemplo, si hello <b>intervalo</b> es <b>cada hora</b> (frecuencia: hora e intervalo: 1) hello y <b>AnchorDateTime</b> contiene <b>minutos y segundos</b>, a continuación, Hola <b>minutos y segundos</b> partes de hello AnchorDateTime se omiten.</span><span class="sxs-lookup"><span data-stu-id="149d7-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="149d7-407">No</span><span class="sxs-lookup"><span data-stu-id="149d7-407">No</span></span> |<span data-ttu-id="149d7-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="149d7-408">01/01/0001</span></span> |
| <span data-ttu-id="149d7-409">Offset</span><span class="sxs-lookup"><span data-stu-id="149d7-409">offset</span></span> |<span data-ttu-id="149d7-410">Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="149d7-411"><b>Tenga en cuenta</b>: si se especifican anchorDateTime y offset, resultado de hello es Hola combinan MAYÚS.</span><span class="sxs-lookup"><span data-stu-id="149d7-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="149d7-412">No</span><span class="sxs-lookup"><span data-stu-id="149d7-412">No</span></span> |<span data-ttu-id="149d7-413">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-413">NA</span></span> |

<span data-ttu-id="149d7-414">Hola pasos de la sección de disponibilidad especifica ese conjunto de datos de salida de hello es generado por hora (o) proporcionados por el conjunto de datos está disponible por hora:</span><span class="sxs-lookup"><span data-stu-id="149d7-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="149d7-415">Hola **directiva** sección de definición de conjunto de datos define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="149d7-416">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="149d7-416">Policy Name</span></span> | <span data-ttu-id="149d7-417">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-417">Description</span></span> | <span data-ttu-id="149d7-418">Aplica demasiado</span><span class="sxs-lookup"><span data-stu-id="149d7-418">Applied too</span></span>| <span data-ttu-id="149d7-419">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-419">Required</span></span> | <span data-ttu-id="149d7-420">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="149d7-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="149d7-421">minimumSizeMB</span></span> |<span data-ttu-id="149d7-422">Valida datos hello en un **blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes).</span><span class="sxs-lookup"><span data-stu-id="149d7-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="149d7-423">Blob de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-423">Azure Blob</span></span> |<span data-ttu-id="149d7-424">No</span><span class="sxs-lookup"><span data-stu-id="149d7-424">No</span></span> |<span data-ttu-id="149d7-425">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-425">NA</span></span> |
| <span data-ttu-id="149d7-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="149d7-426">minimumRows</span></span> |<span data-ttu-id="149d7-427">Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas.</span><span class="sxs-lookup"><span data-stu-id="149d7-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="149d7-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="149d7-428">Azure SQL Database</span></span></li><li><span data-ttu-id="149d7-429">tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-429">Azure Table</span></span></li></ul> |<span data-ttu-id="149d7-430">No</span><span class="sxs-lookup"><span data-stu-id="149d7-430">No</span></span> |<span data-ttu-id="149d7-431">N/D</span><span class="sxs-lookup"><span data-stu-id="149d7-431">NA</span></span> |

<span data-ttu-id="149d7-432">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="149d7-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="149d7-433">A menos que se esté produciendo un conjunto de datos mediante Data Factory de Azure, debe marcarse como **external**.</span><span class="sxs-lookup"><span data-stu-id="149d7-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="149d7-434">Esta configuración normalmente aplica toohello entradas de la primera actividad en una canalización a menos que se está usando la actividad o el encadenamiento de canalización.</span><span class="sxs-lookup"><span data-stu-id="149d7-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="149d7-435">Nombre</span><span class="sxs-lookup"><span data-stu-id="149d7-435">Name</span></span> | <span data-ttu-id="149d7-436">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-436">Description</span></span> | <span data-ttu-id="149d7-437">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-437">Required</span></span> | <span data-ttu-id="149d7-438">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="149d7-439">dataDelay</span></span> |<span data-ttu-id="149d7-440">Comprobación de hello toodelay tiempo en la disponibilidad de Hola de datos externos de Hola para hello dado segmento.</span><span class="sxs-lookup"><span data-stu-id="149d7-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="149d7-441">Por ejemplo, si Hola los datos están disponibles cada hora, datos externos de hello comprobación toosee Hola están disponibles y es el segmento correspondiente de Hola se puede retrasar listo utilizando dataDelay.</span><span class="sxs-lookup"><span data-stu-id="149d7-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="149d7-442">Solo se aplica toohello la hora actual.</span><span class="sxs-lookup"><span data-stu-id="149d7-442">Only applies toohello present time.</span></span>  <span data-ttu-id="149d7-443">Por ejemplo, si es 1:00 P.M. y este valor es 10 minutos, validación de hello comienza en 1:10 P.M..</span><span class="sxs-lookup"><span data-stu-id="149d7-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="149d7-444">Esta configuración no afecta los segmentos en hello anterior (segmentos con hora de finalización de segmento + dataDelay < ahora) se procesan sin ningún retraso.</span><span class="sxs-lookup"><span data-stu-id="149d7-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="149d7-445">Tiempo mayor que 23:59 horas necesitan toospecified con hello `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="149d7-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="149d7-446">Por ejemplo, toospecify 24 horas, no utilice 24:00:00; en su lugar, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="149d7-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="149d7-447">Si usa 24:00:00, se tratará como 24 días (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="149d7-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="149d7-448">Para 1 día y 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="149d7-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="149d7-449">No</span><span class="sxs-lookup"><span data-stu-id="149d7-449">No</span></span> |<span data-ttu-id="149d7-450">0</span><span class="sxs-lookup"><span data-stu-id="149d7-450">0</span></span> |
| <span data-ttu-id="149d7-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="149d7-451">retryInterval</span></span> |<span data-ttu-id="149d7-452">tiempo de espera de Hello entre un error y Hola siguiente reintento.</span><span class="sxs-lookup"><span data-stu-id="149d7-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="149d7-453">Si se produce un error en un bloque try, el siguiente intento de hello es después retryInterval.</span><span class="sxs-lookup"><span data-stu-id="149d7-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="149d7-454">Si es 1:00 P.M., comenzaremos Hola primer intento.</span><span class="sxs-lookup"><span data-stu-id="149d7-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="149d7-455">Si Hola duración toocomplete Hola primera comprobación de validación es 1 minuto y error en la operación hello, Hola siguiente reintento es a 1:00 + 1 min (duración) + 1 min (intervalo de reintento) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="149d7-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="149d7-456">Para los segmentos en hello anterior, no hay ningún retraso.</span><span class="sxs-lookup"><span data-stu-id="149d7-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="149d7-457">reintento de Hello ocurre inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-457">hello retry happens immediately.</span></span> |<span data-ttu-id="149d7-458">No</span><span class="sxs-lookup"><span data-stu-id="149d7-458">No</span></span> |<span data-ttu-id="149d7-459">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="149d7-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="149d7-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-460">retryTimeout</span></span> |<span data-ttu-id="149d7-461">tiempo de espera de Hola para cada reintento.</span><span class="sxs-lookup"><span data-stu-id="149d7-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="149d7-462">Si se establece esta propiedad too10 minutos, Hola validación necesidades toobe completar en 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="149d7-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="149d7-463">Si se tarda más tiempo que la validación de hello tooperform de 10 minutos, Hola vuelva a intentar agota el tiempo.</span><span class="sxs-lookup"><span data-stu-id="149d7-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="149d7-464">Si se agota el tiempo todos los intentos para la validación de hello, segmento de Hola se marca como TimedOut.</span><span class="sxs-lookup"><span data-stu-id="149d7-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="149d7-465">No</span><span class="sxs-lookup"><span data-stu-id="149d7-465">No</span></span> |<span data-ttu-id="149d7-466">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="149d7-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="149d7-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="149d7-467">maximumRetry</span></span> |<span data-ttu-id="149d7-468">Número de veces toocheck para disponibilidad Hola de datos externos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="149d7-469">Hola permite el valor máximo es 10.</span><span class="sxs-lookup"><span data-stu-id="149d7-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="149d7-470">No</span><span class="sxs-lookup"><span data-stu-id="149d7-470">No</span></span> |<span data-ttu-id="149d7-471">3</span><span class="sxs-lookup"><span data-stu-id="149d7-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="149d7-472">ALMACENES DE DATOS</span><span class="sxs-lookup"><span data-stu-id="149d7-472">DATA STORES</span></span>
<span data-ttu-id="149d7-473">Hola [servicio vinculado](#linked-service) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de los servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="149d7-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="149d7-474">Esta sección proporciona detalles acerca de los elementos JSON que son el almacén de datos tooeach específica.</span><span class="sxs-lookup"><span data-stu-id="149d7-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="149d7-475">Hola [conjunto de datos](#dataset) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="149d7-476">Esta sección proporciona detalles acerca de los elementos JSON que son el almacén de datos tooeach específica.</span><span class="sxs-lookup"><span data-stu-id="149d7-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="149d7-477">Hola [actividad](#activity) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de actividades.</span><span class="sxs-lookup"><span data-stu-id="149d7-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="149d7-478">Esta sección proporciona detalles sobre los elementos JSON que son almacén de datos tooeach específica cuando se utiliza como un origen/receptor de una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="149d7-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="149d7-479">Haga clic en el vínculo de hello para la tienda de hello está interesado en esquemas JSON de hello toosee para servicios vinculados, conjunto de datos y Hola origen/receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="149d7-480">Categoría</span><span class="sxs-lookup"><span data-stu-id="149d7-480">Category</span></span> | <span data-ttu-id="149d7-481">Almacén de datos</span><span class="sxs-lookup"><span data-stu-id="149d7-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="149d7-482">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="149d7-482">**Azure**</span></span> |[<span data-ttu-id="149d7-483">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="149d7-484">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="149d7-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="149d7-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="149d7-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="149d7-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="149d7-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="149d7-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="149d7-488">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="149d7-489">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="149d7-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="149d7-490">**Bases de datos**</span><span class="sxs-lookup"><span data-stu-id="149d7-490">**Databases**</span></span> |[<span data-ttu-id="149d7-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="149d7-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="149d7-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="149d7-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="149d7-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="149d7-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="149d7-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="149d7-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="149d7-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="149d7-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="149d7-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="149d7-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="149d7-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="149d7-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="149d7-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="149d7-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="149d7-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="149d7-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="149d7-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="149d7-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="149d7-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="149d7-501">**NoSQL**</span></span> |[<span data-ttu-id="149d7-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="149d7-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="149d7-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="149d7-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="149d7-504">**Archivo**</span><span class="sxs-lookup"><span data-stu-id="149d7-504">**File**</span></span> |[<span data-ttu-id="149d7-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="149d7-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="149d7-506">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="149d7-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="149d7-507">FTP</span><span class="sxs-lookup"><span data-stu-id="149d7-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="149d7-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="149d7-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="149d7-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="149d7-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="149d7-510">**Otros**</span><span class="sxs-lookup"><span data-stu-id="149d7-510">**Others**</span></span> |[<span data-ttu-id="149d7-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="149d7-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="149d7-512">OData</span><span class="sxs-lookup"><span data-stu-id="149d7-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="149d7-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="149d7-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="149d7-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="149d7-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="149d7-515">Tabla web</span><span class="sxs-lookup"><span data-stu-id="149d7-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="149d7-516">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-517">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-517">Linked service</span></span>
<span data-ttu-id="149d7-518">Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="149d7-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="149d7-519">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="149d7-520">toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de hello **clave de cuenta**, cree un servicio vinculado de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="149d7-521">el servicio conjunto Hola vinculado de toodefine un almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="149d7-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="149d7-522">A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-523">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-523">Property</span></span> | <span data-ttu-id="149d7-524">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-524">Description</span></span> | <span data-ttu-id="149d7-525">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-526">connectionString</span></span> |<span data-ttu-id="149d7-527">Especifique la información necesaria tooconnect tooAzure almacenamiento para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="149d7-528">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="149d7-529">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="149d7-530">Servicio vinculado de SAS de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="149d7-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="149d7-531">Hola SAS de almacenamiento de Azure vinculada servicio permite toolink un generador de datos de Azure tooan cuenta de almacenamiento de Azure mediante una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="149d7-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="149d7-532">Proporciona factoría de datos de hello con acceso restringido tiempo enlazadas a recursos de tooall/específicos (blob o el contenedor) en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="149d7-533">toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de la firma de acceso compartido, cree un servicio de SAS de almacenamiento de Azure vinculada.</span><span class="sxs-lookup"><span data-stu-id="149d7-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="149d7-534">el servicio conjunto Hola vinculado de toodefine una SAS de almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="149d7-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="149d7-535">A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="149d7-536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-536">Property</span></span> | <span data-ttu-id="149d7-537">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-537">Description</span></span> | <span data-ttu-id="149d7-538">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="149d7-539">sasUri</span></span> |<span data-ttu-id="149d7-540">Especificar recursos de almacenamiento de Azure de toohello de URI de firma de acceso compartido como blob, contenedor o tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="149d7-541">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="149d7-542">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-542">Example</span></span>

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

<span data-ttu-id="149d7-543">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-544">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-544">Dataset</span></span>
<span data-ttu-id="149d7-545">toodefine un conjunto de datos Blob de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="149d7-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="149d7-546">A continuación, especifique Hola siguientes propiedades específicas del Blob de Azure en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-547">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-547">Property</span></span> | <span data-ttu-id="149d7-548">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-548">Description</span></span> | <span data-ttu-id="149d7-549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-550">folderPath</span></span> |<span data-ttu-id="149d7-551">Contenedor de toohello de ruta de acceso y la carpeta en el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="149d7-552">Ejemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="149d7-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="149d7-553">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-553">Yes</span></span> |
| <span data-ttu-id="149d7-554">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-554">fileName</span></span> |<span data-ttu-id="149d7-555">Nombre del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-555">Name of hello blob.</span></span> <span data-ttu-id="149d7-556">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="149d7-557">Si especifica un nombre de archivo, funciona de la actividad (incluida la copia) de hello en Hola Blob en cuestión.</span><span class="sxs-lookup"><span data-stu-id="149d7-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="149d7-558">Cuando no se especifica el nombre de archivo, copia incluye todos los Blobs en folderPath hello para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="149d7-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="149d7-559">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos. <Guid>.txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="149d7-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="149d7-560">No</span><span class="sxs-lookup"><span data-stu-id="149d7-560">No</span></span> |
| <span data-ttu-id="149d7-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-561">partitionedBy</span></span> |<span data-ttu-id="149d7-562">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="149d7-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="149d7-563">Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="149d7-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="149d7-564">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-565">No</span><span class="sxs-lookup"><span data-stu-id="149d7-565">No</span></span> |
| <span data-ttu-id="149d7-566">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-566">format</span></span> | <span data-ttu-id="149d7-567">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-568">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-569">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-570">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-571">No</span><span class="sxs-lookup"><span data-stu-id="149d7-571">No</span></span> |
| <span data-ttu-id="149d7-572">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-572">compression</span></span> | <span data-ttu-id="149d7-573">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-574">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-575">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="149d7-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-576">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-577">No</span><span class="sxs-lookup"><span data-stu-id="149d7-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-578">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-578">Example</span></span>

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


<span data-ttu-id="149d7-579">Para más información, consulte el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="149d7-580">BlobSource en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="149d7-581">Si va a copiar datos desde un almacenamiento de blobs de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**BlobSource**y especifique después propiedades Hola ** origen ** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="149d7-582">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-582">Property</span></span> | <span data-ttu-id="149d7-583">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-583">Description</span></span> | <span data-ttu-id="149d7-584">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-584">Allowed values</span></span> | <span data-ttu-id="149d7-585">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-586">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-586">recursive</span></span> |<span data-ttu-id="149d7-587">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-588">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="149d7-588">True (default value), False</span></span> |<span data-ttu-id="149d7-589">No</span><span class="sxs-lookup"><span data-stu-id="149d7-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="149d7-590">Ejemplo: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="149d7-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="149d7-591">BlobSink en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="149d7-592">Si va a copiar datos tooan almacenamiento de blobs de Azure, establezca hello **tipo de receptor** de hello actividad de copia demasiado**BlobSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-593">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-593">Property</span></span> | <span data-ttu-id="149d7-594">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-594">Description</span></span> | <span data-ttu-id="149d7-595">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-595">Allowed values</span></span> | <span data-ttu-id="149d7-596">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="149d7-597">copyBehavior</span></span> |<span data-ttu-id="149d7-598">Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="149d7-599"><b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="149d7-600">ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="149d7-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="149d7-601"><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola están en hello primero niveles de carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="149d7-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="149d7-602">archivos de destino de Hello tienen nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="149d7-603"><b>MergeFiles (valor predeterminado):</b> combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="149d7-604">Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="149d7-605">No</span><span class="sxs-lookup"><span data-stu-id="149d7-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="149d7-606">Ejemplo: BlobSink</span><span class="sxs-lookup"><span data-stu-id="149d7-606">Example: BlobSink</span></span>

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

<span data-ttu-id="149d7-607">Para obtener más información, vea el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="149d7-608">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-609">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-609">Linked service</span></span>
<span data-ttu-id="149d7-610">toodefine un servicio de almacén de Azure Data Lake vinculado, Establece el tipo de saludo de hello servicio vinculado demasiado**AzureDataLakeStore**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-611">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-611">Property</span></span> | <span data-ttu-id="149d7-612">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-612">Description</span></span> | <span data-ttu-id="149d7-613">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-614">type</span><span class="sxs-lookup"><span data-stu-id="149d7-614">type</span></span> | <span data-ttu-id="149d7-615">propiedad de tipo Hello debe establecerse en: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="149d7-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="149d7-616">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-616">Yes</span></span> |
| <span data-ttu-id="149d7-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="149d7-617">dataLakeStoreUri</span></span> | <span data-ttu-id="149d7-618">Especifique la información sobre Hola cuenta de almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="149d7-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="149d7-619">Se encuentra en hello siguiendo el formato: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="149d7-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="149d7-620">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-620">Yes</span></span> |
| <span data-ttu-id="149d7-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="149d7-621">subscriptionId</span></span> | <span data-ttu-id="149d7-622">Suscripción de Azure identificador toowhich almacén de Data Lake pertenece.</span><span class="sxs-lookup"><span data-stu-id="149d7-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="149d7-623">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="149d7-623">Required for sink</span></span> |
| <span data-ttu-id="149d7-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="149d7-624">resourceGroupName</span></span> | <span data-ttu-id="149d7-625">Toowhich de nombre de grupo de recursos de Azure almacén de Data Lake pertenece.</span><span class="sxs-lookup"><span data-stu-id="149d7-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="149d7-626">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="149d7-626">Required for sink</span></span> |
| <span data-ttu-id="149d7-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="149d7-627">servicePrincipalId</span></span> | <span data-ttu-id="149d7-628">Especifique el identificador de cliente de. la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="149d7-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="149d7-629">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="149d7-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="149d7-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="149d7-630">servicePrincipalKey</span></span> | <span data-ttu-id="149d7-631">Especifique la clave de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-631">Specify hello application's key.</span></span> | <span data-ttu-id="149d7-632">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="149d7-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="149d7-633">tenant</span><span class="sxs-lookup"><span data-stu-id="149d7-633">tenant</span></span> | <span data-ttu-id="149d7-634">Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="149d7-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="149d7-635">Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="149d7-636">Sí (para la autenticación de entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="149d7-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="149d7-637">authorization</span><span class="sxs-lookup"><span data-stu-id="149d7-637">authorization</span></span> | <span data-ttu-id="149d7-638">Haga clic en **Authorize** botón en hello **Editor de generador de datos** y escriba sus credenciales que asigna la propiedad de hello autogenerada autorización URL toothis.</span><span class="sxs-lookup"><span data-stu-id="149d7-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="149d7-639">Sí (para la autenticación de credenciales de usuario)</span><span class="sxs-lookup"><span data-stu-id="149d7-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="149d7-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="149d7-640">sessionId</span></span> | <span data-ttu-id="149d7-641">Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="149d7-642">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="149d7-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="149d7-643">Esta configuración se genera automáticamente al usar el Editor de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="149d7-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="149d7-644">Sí (para la autenticación de credenciales de usuario)</span><span class="sxs-lookup"><span data-stu-id="149d7-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="149d7-645">Ejemplo: uso de la autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="149d7-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="149d7-646">Ejemplo: uso de la autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="149d7-647">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-648">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-648">Dataset</span></span>
<span data-ttu-id="149d7-649">toodefine un conjunto de datos de almacén de Azure Data Lake conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureDataLakeStore**y especifique Hola propiedades Hola siguientes **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-650">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-650">Property</span></span> | <span data-ttu-id="149d7-651">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-651">Description</span></span> | <span data-ttu-id="149d7-652">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-653">folderPath</span></span> |<span data-ttu-id="149d7-654">Contenedor de toohello de ruta de acceso y la carpeta en hello Azure Data Lake almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="149d7-655">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-655">Yes</span></span> |
| <span data-ttu-id="149d7-656">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-656">fileName</span></span> |<span data-ttu-id="149d7-657">Nombre del archivo de hello en el almacén de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="149d7-658">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="149d7-659">Si especifica un nombre de archivo, actividad de hello (incluida la copia) funciona en archivos específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="149d7-660">Cuando no se especifica el nombre de archivo, copia incluye todos los archivos en folderPath hello para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="149d7-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="149d7-661">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos. <Guid>.txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="149d7-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="149d7-662">No</span><span class="sxs-lookup"><span data-stu-id="149d7-662">No</span></span> |
| <span data-ttu-id="149d7-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-663">partitionedBy</span></span> |<span data-ttu-id="149d7-664">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="149d7-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="149d7-665">Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="149d7-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="149d7-666">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-667">No</span><span class="sxs-lookup"><span data-stu-id="149d7-667">No</span></span> |
| <span data-ttu-id="149d7-668">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-668">format</span></span> | <span data-ttu-id="149d7-669">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-670">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-671">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-672">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-673">No</span><span class="sxs-lookup"><span data-stu-id="149d7-673">No</span></span> |
| <span data-ttu-id="149d7-674">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-674">compression</span></span> | <span data-ttu-id="149d7-675">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-676">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-677">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="149d7-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-678">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-679">No</span><span class="sxs-lookup"><span data-stu-id="149d7-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-680">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-680">Example</span></span>
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

<span data-ttu-id="149d7-681">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="149d7-682">Origen de Azure Data Lake Store en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="149d7-683">Si va a copiar datos desde un almacén de Data Lake de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**AzureDataLakeStoreSource**y especificar después de propiedades en hello **origen**  sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="149d7-684">**AzureDataLakeStoreSource** admite Hola propiedades siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="149d7-685">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-685">Property</span></span> | <span data-ttu-id="149d7-686">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-686">Description</span></span> | <span data-ttu-id="149d7-687">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-687">Allowed values</span></span> | <span data-ttu-id="149d7-688">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-689">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-689">recursive</span></span> |<span data-ttu-id="149d7-690">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-691">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="149d7-691">True (default value), False</span></span> |<span data-ttu-id="149d7-692">No</span><span class="sxs-lookup"><span data-stu-id="149d7-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="149d7-693">Ejemplo: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="149d7-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="149d7-694">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="149d7-695">Receptor de Azure Data Lake Store en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-696">Si va a copiar el almacén de datos tooan Azure Data Lake, establezca hello **tipo de receptor** de hello actividad de copia demasiado**AzureDataLakeStoreSink**y especificar después de propiedades en hello **receptor**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-697">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-697">Property</span></span> | <span data-ttu-id="149d7-698">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-698">Description</span></span> | <span data-ttu-id="149d7-699">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-699">Allowed values</span></span> | <span data-ttu-id="149d7-700">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="149d7-701">copyBehavior</span></span> |<span data-ttu-id="149d7-702">Especifica el comportamiento de la copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="149d7-703"><b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="149d7-704">ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="149d7-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="149d7-705"><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="149d7-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="149d7-706">archivos de destino de Hola se crean con el nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="149d7-707"><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="149d7-708">Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="149d7-709">No</span><span class="sxs-lookup"><span data-stu-id="149d7-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="149d7-710">Ejemplo: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="149d7-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="149d7-711">Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="149d7-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="149d7-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="149d7-713">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-713">Linked service</span></span>
<span data-ttu-id="149d7-714">toodefine una base de datos de Azure Cosmos el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**DocumentDb**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-715">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="149d7-715">**Property**</span></span> | <span data-ttu-id="149d7-716">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="149d7-716">**Description**</span></span> | <span data-ttu-id="149d7-717">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="149d7-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-718">connectionString</span></span> |<span data-ttu-id="149d7-719">Especifique la información necesaria de base de datos de tooconnect tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="149d7-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="149d7-720">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-721">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-721">Example</span></span>

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
<span data-ttu-id="149d7-722">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-723">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-723">Dataset</span></span>
<span data-ttu-id="149d7-724">toodefine un conjunto de datos de la base de datos de Azure Cosmos, conjunto hello **tipo** del conjunto de datos de hello demasiado**DocumentDbCollection**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-725">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="149d7-725">**Property**</span></span> | <span data-ttu-id="149d7-726">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="149d7-726">**Description**</span></span> | <span data-ttu-id="149d7-727">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="149d7-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="149d7-728">collectionName</span></span> |<span data-ttu-id="149d7-729">Nombre de la colección de la base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="149d7-730">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-731">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-731">Example</span></span>

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
<span data-ttu-id="149d7-732">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="149d7-733">Origen de la colección de Azure Cosmos DB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="149d7-734">Si va a copiar datos desde una base de datos de Azure Cosmos, establezca hello **tipo de origen de** de hello actividad de copia demasiado**DocumentDbCollectionSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-735">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="149d7-735">**Property**</span></span> | <span data-ttu-id="149d7-736">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="149d7-736">**Description**</span></span> | <span data-ttu-id="149d7-737">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="149d7-737">**Allowed values**</span></span> | <span data-ttu-id="149d7-738">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="149d7-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-739">query</span><span class="sxs-lookup"><span data-stu-id="149d7-739">query</span></span> |<span data-ttu-id="149d7-740">Especifique los datos de hello consulta tooread.</span><span class="sxs-lookup"><span data-stu-id="149d7-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="149d7-741">Cadena de consulta admitida por Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="149d7-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="149d7-742">Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="149d7-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="149d7-743">No</span><span class="sxs-lookup"><span data-stu-id="149d7-743">No</span></span> <br/><br/><span data-ttu-id="149d7-744">Si no se especifica, Hola instrucción SQL que se ejecuta:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="149d7-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="149d7-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="149d7-745">nestingSeparator</span></span> |<span data-ttu-id="149d7-746">Tooindicate de carácter especial que Hola documento está anidada</span><span class="sxs-lookup"><span data-stu-id="149d7-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="149d7-747">Cualquier carácter.</span><span class="sxs-lookup"><span data-stu-id="149d7-747">Any character.</span></span> <br/><br/><span data-ttu-id="149d7-748">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="149d7-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="149d7-749">Factoría de datos de Azure permite jerarquía toodenote de usuario a través de nestingSeparator, que es "."</span><span class="sxs-lookup"><span data-stu-id="149d7-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="149d7-750">Hola por encima de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="149d7-750">in hello above examples.</span></span> <span data-ttu-id="149d7-751">Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="149d7-752">No</span><span class="sxs-lookup"><span data-stu-id="149d7-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-753">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="149d7-754">Receptor de la colección de Azure Cosmos DB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-755">Si va a copiar datos tooAzure Cosmos DB, establezca hello **tipo de receptor** de hello actividad de copia demasiado**DocumentDbCollectionSink**y especificar después de propiedades en hello **receptor**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-756">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="149d7-756">**Property**</span></span> | <span data-ttu-id="149d7-757">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="149d7-757">**Description**</span></span> | <span data-ttu-id="149d7-758">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="149d7-758">**Allowed values**</span></span> | <span data-ttu-id="149d7-759">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="149d7-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="149d7-760">nestingSeparator</span></span> |<span data-ttu-id="149d7-761">Se necesita un carácter especial en hello tooindicate de nombre de columna de origen que anidados de documento.</span><span class="sxs-lookup"><span data-stu-id="149d7-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="149d7-762">Por ejemplo anteriormente: `Name.First` en la salida de hello tabla genera Hola siguiendo la estructura JSON en el documento de base de datos de Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="149d7-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="149d7-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="149d7-763">"Name": {</span></span><br/>    <span data-ttu-id="149d7-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="149d7-764">"First": "John"</span></span><br/><span data-ttu-id="149d7-765">},</span><span class="sxs-lookup"><span data-stu-id="149d7-765">},</span></span> |<span data-ttu-id="149d7-766">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="149d7-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="149d7-767">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="149d7-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="149d7-768">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="149d7-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="149d7-769">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="149d7-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="149d7-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-770">writeBatchSize</span></span> |<span data-ttu-id="149d7-771">Número de paralelo solicita documentos de toocreate de servicio de base de datos de Cosmos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="149d7-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="149d7-772">Puede ajustar el rendimiento de hello cuando se copian datos de base de datos de Azure Cosmos mediante esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="149d7-773">Puede esperar un rendimiento mejor al aumentar el valor writeBatchSize porque se envían más solicitudes paralelas tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="149d7-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="149d7-774">Sin embargo deberá tooavoid limitación que puede producir mensajes de bienvenida del error: "Solicitud velocidad es grande".</span><span class="sxs-lookup"><span data-stu-id="149d7-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="149d7-775">La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una mejor hello toohave de colección (por ejemplo, S3) mayoría rendimiento disponible (2500 solicitud unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="149d7-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="149d7-776">Entero</span><span class="sxs-lookup"><span data-stu-id="149d7-776">Integer</span></span> |<span data-ttu-id="149d7-777">No (valor predeterminado: 5)</span><span class="sxs-lookup"><span data-stu-id="149d7-777">No (default: 5)</span></span> |
| <span data-ttu-id="149d7-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-778">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-779">Tiempo de espera para hello operación toocomplete antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="149d7-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="149d7-780">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-780">timespan</span></span><br/><br/> <span data-ttu-id="149d7-781">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="149d7-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="149d7-782">No</span><span class="sxs-lookup"><span data-stu-id="149d7-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-783">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="149d7-784">Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="149d7-785">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-786">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-786">Linked service</span></span>
<span data-ttu-id="149d7-787">toodefine una base de datos de SQL Azure vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**AzureSqlDatabase**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-788">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-788">Property</span></span> | <span data-ttu-id="149d7-789">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-789">Description</span></span> | <span data-ttu-id="149d7-790">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-791">connectionString</span></span> |<span data-ttu-id="149d7-792">Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="149d7-793">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-794">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-794">Example</span></span>
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

<span data-ttu-id="149d7-795">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-796">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-796">Dataset</span></span>
<span data-ttu-id="149d7-797">toodefine un conjunto de datos de la base de datos de SQL Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSqlTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-798">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-798">Property</span></span> | <span data-ttu-id="149d7-799">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-799">Description</span></span> | <span data-ttu-id="149d7-800">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-801">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-801">tableName</span></span> |<span data-ttu-id="149d7-802">Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Azure Hola que servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="149d7-803">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-804">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-804">Example</span></span>

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
<span data-ttu-id="149d7-805">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="149d7-806">Origen de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="149d7-807">Si va a copiar datos desde una base de datos de SQL Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-808">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-808">Property</span></span> | <span data-ttu-id="149d7-809">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-809">Description</span></span> | <span data-ttu-id="149d7-810">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-810">Allowed values</span></span> | <span data-ttu-id="149d7-811">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="149d7-812">sqlReaderQuery</span></span> |<span data-ttu-id="149d7-813">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-814">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-814">SQL query string.</span></span> <span data-ttu-id="149d7-815">Ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-816">No</span><span class="sxs-lookup"><span data-stu-id="149d7-816">No</span></span> |
| <span data-ttu-id="149d7-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="149d7-818">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="149d7-819">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="149d7-820">No</span><span class="sxs-lookup"><span data-stu-id="149d7-820">No</span></span> |
| <span data-ttu-id="149d7-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-821">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-822">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="149d7-823">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="149d7-823">Name/value pairs.</span></span> <span data-ttu-id="149d7-824">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="149d7-825">No</span><span class="sxs-lookup"><span data-stu-id="149d7-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-826">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-826">Example</span></span>

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
<span data-ttu-id="149d7-827">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="149d7-828">Receptor de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-829">Si va a copiar datos tooAzure base de datos SQL, establezca hello **tipo de receptor** de hello actividad de copia demasiado**SqlSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-830">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-830">Property</span></span> | <span data-ttu-id="149d7-831">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-831">Description</span></span> | <span data-ttu-id="149d7-832">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-832">Allowed values</span></span> | <span data-ttu-id="149d7-833">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-834">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-835">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="149d7-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="149d7-836">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-836">timespan</span></span><br/><br/> <span data-ttu-id="149d7-837">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="149d7-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="149d7-838">No</span><span class="sxs-lookup"><span data-stu-id="149d7-838">No</span></span> |
| <span data-ttu-id="149d7-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-839">writeBatchSize</span></span> |<span data-ttu-id="149d7-840">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="149d7-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="149d7-841">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="149d7-841">Integer (number of rows)</span></span> |<span data-ttu-id="149d7-842">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="149d7-842">No (default: 10000)</span></span> |
| <span data-ttu-id="149d7-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="149d7-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="149d7-844">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="149d7-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="149d7-845">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="149d7-845">A query statement.</span></span> |<span data-ttu-id="149d7-846">No</span><span class="sxs-lookup"><span data-stu-id="149d7-846">No</span></span> |
| <span data-ttu-id="149d7-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="149d7-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="149d7-848">Especifique un nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="149d7-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="149d7-849">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="149d7-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="149d7-850">No</span><span class="sxs-lookup"><span data-stu-id="149d7-850">No</span></span> |
| <span data-ttu-id="149d7-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="149d7-852">Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="149d7-853">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="149d7-854">No</span><span class="sxs-lookup"><span data-stu-id="149d7-854">No</span></span> |
| <span data-ttu-id="149d7-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-855">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-856">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="149d7-857">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="149d7-857">Name/value pairs.</span></span> <span data-ttu-id="149d7-858">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="149d7-859">No</span><span class="sxs-lookup"><span data-stu-id="149d7-859">No</span></span> |
| <span data-ttu-id="149d7-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="149d7-860">sqlWriterTableType</span></span> |<span data-ttu-id="149d7-861">Especifique un toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="149d7-862">Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="149d7-863">Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="149d7-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="149d7-864">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-864">A table type name.</span></span> |<span data-ttu-id="149d7-865">No</span><span class="sxs-lookup"><span data-stu-id="149d7-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-866">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-866">Example</span></span>

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

<span data-ttu-id="149d7-867">Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="149d7-868">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-869">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-869">Linked service</span></span>
<span data-ttu-id="149d7-870">toodefine un almacenamiento de datos de SQL Azure vinculado servicio, conjunto de hello **tipo** de hello servicio vinculado demasiado**AzureSqlDW**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-871">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-871">Property</span></span> | <span data-ttu-id="149d7-872">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-872">Description</span></span> | <span data-ttu-id="149d7-873">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-874">connectionString</span></span> |<span data-ttu-id="149d7-875">Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="149d7-876">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="149d7-877">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-877">Example</span></span>

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

<span data-ttu-id="149d7-878">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-879">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-879">Dataset</span></span>
<span data-ttu-id="149d7-880">toodefine un conjunto de datos de almacenamiento de datos de SQL Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSqlDWTable**y especifique Hola propiedades Hola siguientes **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-881">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-881">Property</span></span> | <span data-ttu-id="149d7-882">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-882">Description</span></span> | <span data-ttu-id="149d7-883">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-884">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-884">tableName</span></span> |<span data-ttu-id="149d7-885">Nombre de tabla de Hola o vista de base de datos de almacenamiento de datos de SQL Azure de Hola Hola servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="149d7-886">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-887">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-887">Example</span></span>

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

<span data-ttu-id="149d7-888">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="149d7-889">Origen de SQL DW en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="149d7-890">Si va a copiar datos desde almacenamiento de datos de SQL Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlDWSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-891">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-891">Property</span></span> | <span data-ttu-id="149d7-892">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-892">Description</span></span> | <span data-ttu-id="149d7-893">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-893">Allowed values</span></span> | <span data-ttu-id="149d7-894">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="149d7-895">sqlReaderQuery</span></span> |<span data-ttu-id="149d7-896">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-897">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-897">SQL query string.</span></span> <span data-ttu-id="149d7-898">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-899">No</span><span class="sxs-lookup"><span data-stu-id="149d7-899">No</span></span> |
| <span data-ttu-id="149d7-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="149d7-901">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="149d7-902">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="149d7-903">No</span><span class="sxs-lookup"><span data-stu-id="149d7-903">No</span></span> |
| <span data-ttu-id="149d7-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-904">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-905">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="149d7-906">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="149d7-906">Name/value pairs.</span></span> <span data-ttu-id="149d7-907">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="149d7-908">No</span><span class="sxs-lookup"><span data-stu-id="149d7-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-909">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-909">Example</span></span>

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

<span data-ttu-id="149d7-910">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="149d7-911">Receptor de SQL DW en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-912">Si va a copiar datos tooAzure almacenamiento de datos SQL, establezca hello **tipo de receptor** de hello actividad de copia demasiado**SqlDWSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-913">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-913">Property</span></span> | <span data-ttu-id="149d7-914">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-914">Description</span></span> | <span data-ttu-id="149d7-915">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-915">Allowed values</span></span> | <span data-ttu-id="149d7-916">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="149d7-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="149d7-918">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="149d7-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="149d7-919">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="149d7-919">A query statement.</span></span> |<span data-ttu-id="149d7-920">No</span><span class="sxs-lookup"><span data-stu-id="149d7-920">No</span></span> |
| <span data-ttu-id="149d7-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="149d7-921">allowPolyBase</span></span> |<span data-ttu-id="149d7-922">Indica si toouse PolyBase (si procede) en lugar de mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="149d7-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="149d7-923">**El uso de PolyBase es Hola recomendado de forma que los datos tooload en almacenamiento de datos de SQL.**</span><span class="sxs-lookup"><span data-stu-id="149d7-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="149d7-924">True</span><span class="sxs-lookup"><span data-stu-id="149d7-924">True</span></span> <br/><span data-ttu-id="149d7-925">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="149d7-925">False (default)</span></span> |<span data-ttu-id="149d7-926">No</span><span class="sxs-lookup"><span data-stu-id="149d7-926">No</span></span> |
| <span data-ttu-id="149d7-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="149d7-927">polyBaseSettings</span></span> |<span data-ttu-id="149d7-928">Un grupo de propiedades que se pueden especificar cuando hello **allowPolybase** propiedad se establece demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="149d7-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="149d7-929">No</span><span class="sxs-lookup"><span data-stu-id="149d7-929">No</span></span> |
| <span data-ttu-id="149d7-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="149d7-930">rejectValue</span></span> |<span data-ttu-id="149d7-931">Especifica el número de Hola o porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="149d7-932">Obtener más información acerca de hello PolyBase rechazan opciones Hola **argumentos** sección de [crear tabla externa (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="149d7-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="149d7-933">0 (predeterminado), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="149d7-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="149d7-934">No</span><span class="sxs-lookup"><span data-stu-id="149d7-934">No</span></span> |
| <span data-ttu-id="149d7-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="149d7-935">rejectType</span></span> |<span data-ttu-id="149d7-936">Especifica si se especifica la opción de hello rejectValue como un valor literal o un porcentaje.</span><span class="sxs-lookup"><span data-stu-id="149d7-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="149d7-937">Valor (predeterminado), Porcentaje</span><span class="sxs-lookup"><span data-stu-id="149d7-937">Value (default), Percentage</span></span> |<span data-ttu-id="149d7-938">No</span><span class="sxs-lookup"><span data-stu-id="149d7-938">No</span></span> |
| <span data-ttu-id="149d7-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="149d7-939">rejectSampleValue</span></span> |<span data-ttu-id="149d7-940">Determina el número de Hola de tooretrieve filas antes de hello PolyBase vuelve a calcular el porcentaje de Hola de filas rechazados.</span><span class="sxs-lookup"><span data-stu-id="149d7-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="149d7-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="149d7-941">1, 2, …</span></span> |<span data-ttu-id="149d7-942">Sí, si el valor de **rejectType** es **percentage**</span><span class="sxs-lookup"><span data-stu-id="149d7-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="149d7-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="149d7-943">useTypeDefault</span></span> |<span data-ttu-id="149d7-944">Especifica cómo toohandle valores que falten en archivos delimitados por texto cuando PolyBase recupera datos de archivo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="149d7-945">Más información acerca de esta propiedad desde la sección de argumentos de hello en [crear EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="149d7-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="149d7-946">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="149d7-946">True, False (default)</span></span> |<span data-ttu-id="149d7-947">No</span><span class="sxs-lookup"><span data-stu-id="149d7-947">No</span></span> |
| <span data-ttu-id="149d7-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-948">writeBatchSize</span></span> |<span data-ttu-id="149d7-949">Inserta los datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="149d7-950">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="149d7-950">Integer (number of rows)</span></span> |<span data-ttu-id="149d7-951">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="149d7-951">No (default: 10000)</span></span> |
| <span data-ttu-id="149d7-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-952">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-953">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="149d7-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="149d7-954">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-954">timespan</span></span><br/><br/> <span data-ttu-id="149d7-955">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="149d7-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="149d7-956">No</span><span class="sxs-lookup"><span data-stu-id="149d7-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-957">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-957">Example</span></span>

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

<span data-ttu-id="149d7-958">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="149d7-959">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-960">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-960">Linked service</span></span>
<span data-ttu-id="149d7-961">el servicio conjunto Hola vinculado de toodefine una búsqueda de Azure **tipo** de hello servicio vinculado demasiado**AzureSearch**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-962">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-962">Property</span></span> | <span data-ttu-id="149d7-963">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-963">Description</span></span> | <span data-ttu-id="149d7-964">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="149d7-965">url</span><span class="sxs-lookup"><span data-stu-id="149d7-965">url</span></span> | <span data-ttu-id="149d7-966">Dirección URL de hello servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="149d7-967">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-967">Yes</span></span> |
| <span data-ttu-id="149d7-968">key</span><span class="sxs-lookup"><span data-stu-id="149d7-968">key</span></span> | <span data-ttu-id="149d7-969">Clave de administrador de hello servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="149d7-970">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-971">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-971">Example</span></span>

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

<span data-ttu-id="149d7-972">Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-973">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-973">Dataset</span></span>
<span data-ttu-id="149d7-974">toodefine un conjunto de datos de búsqueda de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSearchIndex**y especifique Hola propiedades Hola siguientes **typeProperties** sección :</span><span class="sxs-lookup"><span data-stu-id="149d7-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-975">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-975">Property</span></span> | <span data-ttu-id="149d7-976">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-976">Description</span></span> | <span data-ttu-id="149d7-977">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="149d7-978">type</span><span class="sxs-lookup"><span data-stu-id="149d7-978">type</span></span> | <span data-ttu-id="149d7-979">se debe establecer propiedad de tipo Hello demasiado**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="149d7-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="149d7-980">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-980">Yes</span></span> |
| <span data-ttu-id="149d7-981">indexName</span><span class="sxs-lookup"><span data-stu-id="149d7-981">indexName</span></span> | <span data-ttu-id="149d7-982">Nombre del índice de búsqueda de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="149d7-983">Factoría de datos no crea el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="149d7-984">índice de Hello debe existir en la búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="149d7-985">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-986">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-986">Example</span></span>

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

<span data-ttu-id="149d7-987">Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="149d7-988">Receptor del índice de Azure Search en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-989">Si va a copiar el índice de búsqueda de Azure de tooan de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**AzureSearchIndexSink**y especificar después de propiedades en hello **receptor**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-990">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-990">Property</span></span> | <span data-ttu-id="149d7-991">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-991">Description</span></span> | <span data-ttu-id="149d7-992">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-992">Allowed values</span></span> | <span data-ttu-id="149d7-993">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="149d7-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="149d7-994">WriteBehavior</span></span> | <span data-ttu-id="149d7-995">Especifica si toomerge o reemplazar cuando un documento ya existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="149d7-996">Combinar (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="149d7-996">Merge (default)</span></span><br/><span data-ttu-id="149d7-997">Cargar</span><span class="sxs-lookup"><span data-stu-id="149d7-997">Upload</span></span>| <span data-ttu-id="149d7-998">No</span><span class="sxs-lookup"><span data-stu-id="149d7-998">No</span></span> |
| <span data-ttu-id="149d7-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-999">WriteBatchSize</span></span> | <span data-ttu-id="149d7-1000">Carga datos en el índice de búsqueda de Azure de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="149d7-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="149d7-1001">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="149d7-1001">1 too1,000.</span></span> <span data-ttu-id="149d7-1002">El valor predeterminado es 1000.</span><span class="sxs-lookup"><span data-stu-id="149d7-1002">Default value is 1000.</span></span> | <span data-ttu-id="149d7-1003">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1004">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1004">Example</span></span>

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

<span data-ttu-id="149d7-1005">Para obtener más información, vea el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="149d7-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="149d7-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1007">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1007">Linked service</span></span>
<span data-ttu-id="149d7-1008">Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="149d7-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="149d7-1009">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="149d7-1010">toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de hello **clave de cuenta**, cree un servicio vinculado de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="149d7-1011">el servicio conjunto Hola vinculado de toodefine un almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="149d7-1012">A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1013">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1013">Property</span></span> | <span data-ttu-id="149d7-1014">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1014">Description</span></span> | <span data-ttu-id="149d7-1015">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-1016">type</span><span class="sxs-lookup"><span data-stu-id="149d7-1016">type</span></span> |<span data-ttu-id="149d7-1017">propiedad de tipo Hello debe establecerse en: **azurestorage.**</span><span class="sxs-lookup"><span data-stu-id="149d7-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="149d7-1018">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1018">Yes</span></span> |
| <span data-ttu-id="149d7-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-1019">connectionString</span></span> |<span data-ttu-id="149d7-1020">Especifique la información necesaria tooconnect tooAzure almacenamiento para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="149d7-1021">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1021">Yes</span></span> |

<span data-ttu-id="149d7-1022">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="149d7-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="149d7-1023">Servicio vinculado de SAS de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="149d7-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="149d7-1024">Hola SAS de almacenamiento de Azure vinculada servicio permite toolink un generador de datos de Azure tooan cuenta de almacenamiento de Azure mediante una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="149d7-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="149d7-1025">Proporciona factoría de datos de hello con acceso restringido tiempo enlazadas a recursos de tooall/específicos (blob o el contenedor) en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="149d7-1026">toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de la firma de acceso compartido, cree un servicio de SAS de almacenamiento de Azure vinculada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="149d7-1027">el servicio conjunto Hola vinculado de toodefine una SAS de almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="149d7-1028">A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="149d7-1029">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1029">Property</span></span> | <span data-ttu-id="149d7-1030">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1030">Description</span></span> | <span data-ttu-id="149d7-1031">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-1032">type</span><span class="sxs-lookup"><span data-stu-id="149d7-1032">type</span></span> |<span data-ttu-id="149d7-1033">propiedad de tipo Hello debe establecerse en: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="149d7-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="149d7-1034">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1034">Yes</span></span> |
| <span data-ttu-id="149d7-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="149d7-1035">sasUri</span></span> |<span data-ttu-id="149d7-1036">Especificar recursos de almacenamiento de Azure de toohello de URI de firma de acceso compartido como blob, contenedor o tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="149d7-1037">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1037">Yes</span></span> |

<span data-ttu-id="149d7-1038">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="149d7-1038">**Example:**</span></span>

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

<span data-ttu-id="149d7-1039">Para más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1040">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1040">Dataset</span></span>
<span data-ttu-id="149d7-1041">toodefine un conjunto de datos de la tabla de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1042">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1042">Property</span></span> | <span data-ttu-id="149d7-1043">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1043">Description</span></span> | <span data-ttu-id="149d7-1044">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1045">tableName</span></span> |<span data-ttu-id="149d7-1046">Nombre de tabla de hello en la instancia de base de datos de tabla de Azure de Hola que servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="149d7-1047">Sí.</span><span class="sxs-lookup"><span data-stu-id="149d7-1047">Yes.</span></span> <span data-ttu-id="149d7-1048">Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="149d7-1049">Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1050">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1050">Example</span></span>

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

<span data-ttu-id="149d7-1051">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="149d7-1052">Origen de Azure Table en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1053">Si va a copiar datos desde el almacenamiento de tabla de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**AzureTableSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1054">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1054">Property</span></span> | <span data-ttu-id="149d7-1055">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1055">Description</span></span> | <span data-ttu-id="149d7-1056">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1056">Allowed values</span></span> | <span data-ttu-id="149d7-1057">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="149d7-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="149d7-1059">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1060">Cadena de consulta de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-1060">Azure table query string.</span></span> <span data-ttu-id="149d7-1061">Vea los ejemplos en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1061">See examples in hello next section.</span></span> |<span data-ttu-id="149d7-1062">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-1062">No.</span></span> <span data-ttu-id="149d7-1063">Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="149d7-1064">Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="149d7-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="149d7-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="149d7-1066">Indica si debe Hola excepción de tabla no existe.</span><span class="sxs-lookup"><span data-stu-id="149d7-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="149d7-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="149d7-1067">TRUE</span></span><br/><span data-ttu-id="149d7-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="149d7-1068">FALSE</span></span> |<span data-ttu-id="149d7-1069">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1070">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1070">Example</span></span>

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

<span data-ttu-id="149d7-1071">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="149d7-1072">Receptor de Azure Table en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-1073">Si va a copiar datos tooAzure almacenamiento de tabla, establecer hello **tipo de receptor** de hello actividad de copia demasiado**AzureTableSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-1074">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1074">Property</span></span> | <span data-ttu-id="149d7-1075">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1075">Description</span></span> | <span data-ttu-id="149d7-1076">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1076">Allowed values</span></span> | <span data-ttu-id="149d7-1077">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="149d7-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="149d7-1079">Partición clave valor predeterminado que se puede usar en el receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="149d7-1080">Valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="149d7-1080">A string value.</span></span> |<span data-ttu-id="149d7-1081">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1081">No</span></span> |
| <span data-ttu-id="149d7-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="149d7-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="149d7-1083">Especifique el nombre de columna de hello cuyos valores se usan como claves de partición.</span><span class="sxs-lookup"><span data-stu-id="149d7-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="149d7-1084">Si no se especifica, AzureTableDefaultPartitionKeyValue se usa como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="149d7-1085">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="149d7-1085">A column name.</span></span> |<span data-ttu-id="149d7-1086">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1086">No</span></span> |
| <span data-ttu-id="149d7-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="149d7-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="149d7-1088">Especifique el nombre de columna de hello cuyos valores de columna se utilizan como clave de fila.</span><span class="sxs-lookup"><span data-stu-id="149d7-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="149d7-1089">Si no se especifica, use un GUID para cada fila.</span><span class="sxs-lookup"><span data-stu-id="149d7-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="149d7-1090">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="149d7-1090">A column name.</span></span> |<span data-ttu-id="149d7-1091">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1091">No</span></span> |
| <span data-ttu-id="149d7-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="149d7-1092">azureTableInsertType</span></span> |<span data-ttu-id="149d7-1093">datos de tooinsert de modo de saludo en tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="149d7-1094">Esta propiedad controla si las filas existentes en la tabla de salida de hello con claves de partición y fila coincidentes tienen sus valores reemplazará o se combinará.</span><span class="sxs-lookup"><span data-stu-id="149d7-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="149d7-1095">toolearn acerca de cómo funcionan estas configuraciones (combinación y reemplazo), consulte [Insert o Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) y [insertar o reemplazar entidades](https://msdn.microsoft.com/library/azure/hh452242.aspx) temas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="149d7-1096">Esta configuración se aplica a nivel de fila de hello, no nivel de tabla de hello, y ninguna de estas opciones eliminan las filas de tabla de salida de hello que no existen en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="149d7-1097">merge (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="149d7-1097">merge (default)</span></span><br/><span data-ttu-id="149d7-1098">replace</span><span class="sxs-lookup"><span data-stu-id="149d7-1098">replace</span></span> |<span data-ttu-id="149d7-1099">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1099">No</span></span> |
| <span data-ttu-id="149d7-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-1100">writeBatchSize</span></span> |<span data-ttu-id="149d7-1101">Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="149d7-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="149d7-1102">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="149d7-1102">Integer (number of rows)</span></span> |<span data-ttu-id="149d7-1103">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="149d7-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="149d7-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-1104">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-1105">Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="149d7-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-1106">timespan</span></span><br/><br/><span data-ttu-id="149d7-1107">Ejemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="149d7-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="149d7-1108">No (valor de tiempo de espera predeterminado toostorage cliente predeterminado 90 seg)</span><span class="sxs-lookup"><span data-stu-id="149d7-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1109">Example</span></span>

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
<span data-ttu-id="149d7-1110">Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="149d7-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="149d7-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1112">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1112">Linked service</span></span>
<span data-ttu-id="149d7-1113">toodefine un Amazon Redshift el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**AmazonRedshift**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1114">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1114">Property</span></span> | <span data-ttu-id="149d7-1115">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1115">Description</span></span> | <span data-ttu-id="149d7-1116">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1117">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1117">server</span></span> |<span data-ttu-id="149d7-1118">IP dirección o nombre de host del servidor de Amazon Redshift Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="149d7-1119">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1119">Yes</span></span> |
| <span data-ttu-id="149d7-1120">puerto</span><span class="sxs-lookup"><span data-stu-id="149d7-1120">port</span></span> |<span data-ttu-id="149d7-1121">número de Hola de puerto TCP Hola Hola Amazon Redshift server usa toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="149d7-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="149d7-1122">No, valor predeterminado: 5439</span><span class="sxs-lookup"><span data-stu-id="149d7-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="149d7-1123">database</span><span class="sxs-lookup"><span data-stu-id="149d7-1123">database</span></span> |<span data-ttu-id="149d7-1124">Nombre de base de datos de Amazon Redshift Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="149d7-1125">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1125">Yes</span></span> |
| <span data-ttu-id="149d7-1126">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1126">username</span></span> |<span data-ttu-id="149d7-1127">Nombre de usuario que tenga la base de datos de access toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="149d7-1128">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1128">Yes</span></span> |
| <span data-ttu-id="149d7-1129">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1129">password</span></span> |<span data-ttu-id="149d7-1130">Contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1130">Password for hello user account.</span></span> |<span data-ttu-id="149d7-1131">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1132">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1132">Example</span></span>

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

<span data-ttu-id="149d7-1133">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1134">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1134">Dataset</span></span>
<span data-ttu-id="149d7-1135">toodefine un conjunto de datos de Amazon Redshift conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1136">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1136">Property</span></span> | <span data-ttu-id="149d7-1137">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1137">Description</span></span> | <span data-ttu-id="149d7-1138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1139">tableName</span></span> |<span data-ttu-id="149d7-1140">Nombre de tabla de hello en base de datos de Amazon Redshift de hello servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="149d7-1141">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-1142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1142">Example</span></span>

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
<span data-ttu-id="149d7-1143">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1144">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="149d7-1145">Si va a copiar datos de Amazon Redshift, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1146">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1146">Property</span></span> | <span data-ttu-id="149d7-1147">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1147">Description</span></span> | <span data-ttu-id="149d7-1148">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1148">Allowed values</span></span> | <span data-ttu-id="149d7-1149">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1150">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1150">query</span></span> |<span data-ttu-id="149d7-1151">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1152">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1152">SQL query string.</span></span> <span data-ttu-id="149d7-1153">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-1154">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1155">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1155">Example</span></span>

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
<span data-ttu-id="149d7-1156">Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="149d7-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="149d7-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1158">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1158">Linked service</span></span>
<span data-ttu-id="149d7-1159">el servicio conjunto Hola vinculado de toodefine un IBM DB2 **tipo** de hello servicio vinculado demasiado**OnPremisesDB2**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1160">Property</span></span> | <span data-ttu-id="149d7-1161">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1161">Description</span></span> | <span data-ttu-id="149d7-1162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1163">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1163">server</span></span> |<span data-ttu-id="149d7-1164">Nombre del servidor de hello DB2.</span><span class="sxs-lookup"><span data-stu-id="149d7-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="149d7-1165">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1165">Yes</span></span> |
| <span data-ttu-id="149d7-1166">database</span><span class="sxs-lookup"><span data-stu-id="149d7-1166">database</span></span> |<span data-ttu-id="149d7-1167">Nombre de base de datos de DB2 Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="149d7-1168">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1168">Yes</span></span> |
| <span data-ttu-id="149d7-1169">schema</span><span class="sxs-lookup"><span data-stu-id="149d7-1169">schema</span></span> |<span data-ttu-id="149d7-1170">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="149d7-1171">nombre del esquema Hola distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="149d7-1172">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1172">No</span></span> |
| <span data-ttu-id="149d7-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1173">authenticationType</span></span> |<span data-ttu-id="149d7-1174">Tipo de autenticación que utiliza la base de datos de DB2 tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="149d7-1175">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="149d7-1176">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1176">Yes</span></span> |
| <span data-ttu-id="149d7-1177">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1177">username</span></span> |<span data-ttu-id="149d7-1178">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="149d7-1179">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1179">No</span></span> |
| <span data-ttu-id="149d7-1180">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1180">password</span></span> |<span data-ttu-id="149d7-1181">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-1182">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1182">No</span></span> |
| <span data-ttu-id="149d7-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1183">gatewayName</span></span> |<span data-ttu-id="149d7-1184">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de DB2 de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="149d7-1185">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1186">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1186">Example</span></span>
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
<span data-ttu-id="149d7-1187">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1188">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1188">Dataset</span></span>
<span data-ttu-id="149d7-1189">conjunto de datos de DB2 toodefine, Hola de conjunto **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="149d7-1190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1190">Property</span></span> | <span data-ttu-id="149d7-1191">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1191">Description</span></span> | <span data-ttu-id="149d7-1192">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1193">tableName</span></span> |<span data-ttu-id="149d7-1194">Nombre de tabla de hello en la instancia de base de datos DB2 de Hola que servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="149d7-1195">Hola tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="149d7-1196">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="149d7-1197">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1197">Example</span></span>
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

<span data-ttu-id="149d7-1198">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1199">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1200">Si va a copiar datos de IBM DB2, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1201">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1201">Property</span></span> | <span data-ttu-id="149d7-1202">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1202">Description</span></span> | <span data-ttu-id="149d7-1203">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1203">Allowed values</span></span> | <span data-ttu-id="149d7-1204">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1205">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1205">query</span></span> |<span data-ttu-id="149d7-1206">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1207">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1207">SQL query string.</span></span> <span data-ttu-id="149d7-1208">Por ejemplo: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="149d7-1209">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1210">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1210">Example</span></span>
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
<span data-ttu-id="149d7-1211">Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="149d7-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="149d7-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1213">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1213">Linked service</span></span>
<span data-ttu-id="149d7-1214">toodefine MySQL el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesMySql**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1215">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1215">Property</span></span> | <span data-ttu-id="149d7-1216">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1216">Description</span></span> | <span data-ttu-id="149d7-1217">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1218">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1218">server</span></span> |<span data-ttu-id="149d7-1219">Nombre del servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="149d7-1220">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1220">Yes</span></span> |
| <span data-ttu-id="149d7-1221">database</span><span class="sxs-lookup"><span data-stu-id="149d7-1221">database</span></span> |<span data-ttu-id="149d7-1222">Nombre de base de datos de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="149d7-1223">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1223">Yes</span></span> |
| <span data-ttu-id="149d7-1224">schema</span><span class="sxs-lookup"><span data-stu-id="149d7-1224">schema</span></span> |<span data-ttu-id="149d7-1225">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="149d7-1226">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1226">No</span></span> |
| <span data-ttu-id="149d7-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1227">authenticationType</span></span> |<span data-ttu-id="149d7-1228">Tipo de autenticación que utiliza la base de datos de MySQL tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="149d7-1229">Los valores posibles son: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="149d7-1230">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1230">Yes</span></span> |
| <span data-ttu-id="149d7-1231">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1231">username</span></span> |<span data-ttu-id="149d7-1232">Especifique la base de datos MySQL toohello de tooconnect de nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="149d7-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="149d7-1233">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1233">Yes</span></span> |
| <span data-ttu-id="149d7-1234">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1234">password</span></span> |<span data-ttu-id="149d7-1235">Especifique la contraseña de cuenta de usuario de hello especificada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="149d7-1236">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1236">Yes</span></span> |
| <span data-ttu-id="149d7-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1237">gatewayName</span></span> |<span data-ttu-id="149d7-1238">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de MySQL de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="149d7-1239">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1240">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1240">Example</span></span>

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

<span data-ttu-id="149d7-1241">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1242">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1242">Dataset</span></span>
<span data-ttu-id="149d7-1243">toodefine un conjunto de datos MySQL, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1244">Property</span></span> | <span data-ttu-id="149d7-1245">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1245">Description</span></span> | <span data-ttu-id="149d7-1246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1247">tableName</span></span> |<span data-ttu-id="149d7-1248">Nombre de tabla de Hola Hola instancia de base de datos MySQL que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="149d7-1249">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1250">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1250">Example</span></span>

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
<span data-ttu-id="149d7-1251">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1252">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1253">Si va a copiar datos desde una base de datos MySQL, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1254">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1254">Property</span></span> | <span data-ttu-id="149d7-1255">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1255">Description</span></span> | <span data-ttu-id="149d7-1256">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1256">Allowed values</span></span> | <span data-ttu-id="149d7-1257">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1258">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1258">query</span></span> |<span data-ttu-id="149d7-1259">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1260">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1260">SQL query string.</span></span> <span data-ttu-id="149d7-1261">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-1262">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-1263">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1263">Example</span></span>
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

<span data-ttu-id="149d7-1264">Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="149d7-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="149d7-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-1266">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1266">Linked service</span></span>
<span data-ttu-id="149d7-1267">toodefine de Oracle vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**OnPremisesOracle**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1268">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1268">Property</span></span> | <span data-ttu-id="149d7-1269">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1269">Description</span></span> | <span data-ttu-id="149d7-1270">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="149d7-1271">driverType</span></span> | <span data-ttu-id="149d7-1272">Especificar qué controlador toouse toocopy datos / tooOracle base de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="149d7-1273">Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="149d7-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="149d7-1274">Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores.</span><span class="sxs-lookup"><span data-stu-id="149d7-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="149d7-1275">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1275">No</span></span> |
| <span data-ttu-id="149d7-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-1276">connectionString</span></span> | <span data-ttu-id="149d7-1277">Especifique la información necesaria la instancia de base de datos de Oracle toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="149d7-1278">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1278">Yes</span></span> |
| <span data-ttu-id="149d7-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1279">gatewayName</span></span> | <span data-ttu-id="149d7-1280">Nombre de puerta de enlace de Hola que es usado tooconnect toohello servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="149d7-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="149d7-1281">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1282">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1282">Example</span></span>
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

<span data-ttu-id="149d7-1283">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1284">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1284">Dataset</span></span>
<span data-ttu-id="149d7-1285">toodefine un conjunto de datos de Oracle, conjunto hello **tipo** del conjunto de datos de hello demasiado**OracleTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1286">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1286">Property</span></span> | <span data-ttu-id="149d7-1287">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1287">Description</span></span> | <span data-ttu-id="149d7-1288">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1289">tableName</span></span> |<span data-ttu-id="149d7-1290">Nombre de tabla de Hola Hola base de datos de Oracle que Hola servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="149d7-1291">No (si se especifica **oracleReaderQuery** de **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1292">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1292">Example</span></span>

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
<span data-ttu-id="149d7-1293">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="149d7-1294">Origen de Oracle en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1295">Si va a copiar datos desde una base de datos de Oracle, establezca hello **tipo de origen de** de hello actividad de copia demasiado**OracleSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1296">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1296">Property</span></span> | <span data-ttu-id="149d7-1297">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1297">Description</span></span> | <span data-ttu-id="149d7-1298">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1298">Allowed values</span></span> | <span data-ttu-id="149d7-1299">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="149d7-1300">oracleReaderQuery</span></span> |<span data-ttu-id="149d7-1301">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1302">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1302">SQL query string.</span></span> <span data-ttu-id="149d7-1303">Por ejemplo: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="149d7-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="149d7-1304">Si no se especifica, Hola instrucción SQL que se ejecuta:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="149d7-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="149d7-1305">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1306">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1306">Example</span></span>

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

<span data-ttu-id="149d7-1307">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="149d7-1308">Receptor de Oracle en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-1309">Si va a copiar la base de datos de Oracle de tooam de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**OracleSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-1310">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1310">Property</span></span> | <span data-ttu-id="149d7-1311">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1311">Description</span></span> | <span data-ttu-id="149d7-1312">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1312">Allowed values</span></span> | <span data-ttu-id="149d7-1313">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-1314">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-1315">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="149d7-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="149d7-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-1316">timespan</span></span><br/><br/> <span data-ttu-id="149d7-1317">Ejemplo: 00:30:00 (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="149d7-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="149d7-1318">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1318">No</span></span> |
| <span data-ttu-id="149d7-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-1319">writeBatchSize</span></span> |<span data-ttu-id="149d7-1320">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="149d7-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="149d7-1321">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="149d7-1321">Integer (number of rows)</span></span> |<span data-ttu-id="149d7-1322">No (valor predeterminado: 100)</span><span class="sxs-lookup"><span data-stu-id="149d7-1322">No (default: 100)</span></span> |
| <span data-ttu-id="149d7-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="149d7-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="149d7-1324">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="149d7-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="149d7-1325">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="149d7-1325">A query statement.</span></span> |<span data-ttu-id="149d7-1326">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1326">No</span></span> |
| <span data-ttu-id="149d7-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="149d7-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="149d7-1328">Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="149d7-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="149d7-1329">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="149d7-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="149d7-1330">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1331">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1331">Example</span></span>
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
<span data-ttu-id="149d7-1332">Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="149d7-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="149d7-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1334">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1334">Linked service</span></span>
<span data-ttu-id="149d7-1335">toodefine un PostgreSQL el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesPostgreSql**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1336">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1336">Property</span></span> | <span data-ttu-id="149d7-1337">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1337">Description</span></span> | <span data-ttu-id="149d7-1338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1339">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1339">server</span></span> |<span data-ttu-id="149d7-1340">Nombre del servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="149d7-1341">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1341">Yes</span></span> |
| <span data-ttu-id="149d7-1342">database</span><span class="sxs-lookup"><span data-stu-id="149d7-1342">database</span></span> |<span data-ttu-id="149d7-1343">Nombre de base de datos de PostgreSQL Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="149d7-1344">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1344">Yes</span></span> |
| <span data-ttu-id="149d7-1345">schema</span><span class="sxs-lookup"><span data-stu-id="149d7-1345">schema</span></span> |<span data-ttu-id="149d7-1346">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="149d7-1347">nombre del esquema Hola distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="149d7-1348">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1348">No</span></span> |
| <span data-ttu-id="149d7-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1349">authenticationType</span></span> |<span data-ttu-id="149d7-1350">Tipo de autenticación que utiliza la base de datos de PostgreSQL tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="149d7-1351">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="149d7-1352">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1352">Yes</span></span> |
| <span data-ttu-id="149d7-1353">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1353">username</span></span> |<span data-ttu-id="149d7-1354">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="149d7-1355">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1355">No</span></span> |
| <span data-ttu-id="149d7-1356">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1356">password</span></span> |<span data-ttu-id="149d7-1357">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-1358">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1358">No</span></span> |
| <span data-ttu-id="149d7-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1359">gatewayName</span></span> |<span data-ttu-id="149d7-1360">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de PostgreSQL local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="149d7-1361">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1362">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1362">Example</span></span>

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
<span data-ttu-id="149d7-1363">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1364">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1364">Dataset</span></span>
<span data-ttu-id="149d7-1365">toodefine un conjunto de datos PostgreSQL conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1366">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1366">Property</span></span> | <span data-ttu-id="149d7-1367">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1367">Description</span></span> | <span data-ttu-id="149d7-1368">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1369">tableName</span></span> |<span data-ttu-id="149d7-1370">Nombre de tabla de Hola Hola instancia de base de datos PostgreSQL que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="149d7-1371">Hola tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="149d7-1372">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1373">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1373">Example</span></span>
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
<span data-ttu-id="149d7-1374">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1375">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1376">Si va a copiar datos desde una base de datos PostgreSQL, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1377">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1377">Property</span></span> | <span data-ttu-id="149d7-1378">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1378">Description</span></span> | <span data-ttu-id="149d7-1379">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1379">Allowed values</span></span> | <span data-ttu-id="149d7-1380">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1381">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1381">query</span></span> |<span data-ttu-id="149d7-1382">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1383">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1383">SQL query string.</span></span> <span data-ttu-id="149d7-1384">Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="149d7-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="149d7-1385">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1386">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1386">Example</span></span>

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

<span data-ttu-id="149d7-1387">Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="149d7-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="149d7-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-1389">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1389">Linked service</span></span>
<span data-ttu-id="149d7-1390">toodefine un almacenamiento de negocios de SAP (BW) el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**SapBw**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="149d7-1391">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1391">Property</span></span> | <span data-ttu-id="149d7-1392">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1392">Description</span></span> | <span data-ttu-id="149d7-1393">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1393">Allowed values</span></span> | <span data-ttu-id="149d7-1394">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="149d7-1395">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1395">server</span></span> | <span data-ttu-id="149d7-1396">Nombre del servidor de hello en qué Hola SAP BW reside la instancia.</span><span class="sxs-lookup"><span data-stu-id="149d7-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="149d7-1397">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1397">string</span></span> | <span data-ttu-id="149d7-1398">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1398">Yes</span></span>
<span data-ttu-id="149d7-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="149d7-1399">systemNumber</span></span> | <span data-ttu-id="149d7-1400">Número de sistema de hello sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="149d7-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="149d7-1401">Número decimal de dos dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="149d7-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="149d7-1402">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1402">Yes</span></span>
<span data-ttu-id="149d7-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="149d7-1403">clientId</span></span> | <span data-ttu-id="149d7-1404">Identificador de cliente del cliente de Hola Hola sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="149d7-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="149d7-1405">Número decimal de tres dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="149d7-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="149d7-1406">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1406">Yes</span></span>
<span data-ttu-id="149d7-1407">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1407">username</span></span> | <span data-ttu-id="149d7-1408">Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="149d7-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="149d7-1409">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1409">string</span></span> | <span data-ttu-id="149d7-1410">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1410">Yes</span></span>
<span data-ttu-id="149d7-1411">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1411">password</span></span> | <span data-ttu-id="149d7-1412">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1412">Password for hello user.</span></span> | <span data-ttu-id="149d7-1413">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1413">string</span></span> | <span data-ttu-id="149d7-1414">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1414">Yes</span></span>
<span data-ttu-id="149d7-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1415">gatewayName</span></span> | <span data-ttu-id="149d7-1416">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP BW de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="149d7-1417">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1417">string</span></span> | <span data-ttu-id="149d7-1418">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1418">Yes</span></span>
<span data-ttu-id="149d7-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1419">encryptedCredential</span></span> | <span data-ttu-id="149d7-1420">Hola cifra la cadena de credenciales.</span><span class="sxs-lookup"><span data-stu-id="149d7-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="149d7-1421">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1421">string</span></span> | <span data-ttu-id="149d7-1422">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-1423">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1423">Example</span></span>

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

<span data-ttu-id="149d7-1424">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1425">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1425">Dataset</span></span>
<span data-ttu-id="149d7-1426">toodefine un conjunto de datos de SAP BW, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="149d7-1427">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP BW de Hola de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="149d7-1428">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1428">Example</span></span>

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
<span data-ttu-id="149d7-1429">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1430">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1431">Si va a copiar datos de SAP Business Warehouse, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1432">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1432">Property</span></span> | <span data-ttu-id="149d7-1433">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1433">Description</span></span> | <span data-ttu-id="149d7-1434">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1434">Allowed values</span></span> | <span data-ttu-id="149d7-1435">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1436">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1436">query</span></span> | <span data-ttu-id="149d7-1437">Especifica Hola MDX consultar tooread datos de instancia de SAP BW Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="149d7-1438">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="149d7-1438">MDX query.</span></span> | <span data-ttu-id="149d7-1439">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1440">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1440">Example</span></span>

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

<span data-ttu-id="149d7-1441">Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="149d7-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="149d7-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1443">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1443">Linked service</span></span>
<span data-ttu-id="149d7-1444">toodefine un SAP HANA el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**SapHana**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="149d7-1445">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1445">Property</span></span> | <span data-ttu-id="149d7-1446">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1446">Description</span></span> | <span data-ttu-id="149d7-1447">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1447">Allowed values</span></span> | <span data-ttu-id="149d7-1448">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="149d7-1449">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1449">server</span></span> | <span data-ttu-id="149d7-1450">Nombre del servidor de hello en qué Hola SAP HANA reside la instancia.</span><span class="sxs-lookup"><span data-stu-id="149d7-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="149d7-1451">Si el servidor usa un puerto personalizado, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="149d7-1452">string</span><span class="sxs-lookup"><span data-stu-id="149d7-1452">string</span></span> | <span data-ttu-id="149d7-1453">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1453">Yes</span></span>
<span data-ttu-id="149d7-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1454">authenticationType</span></span> | <span data-ttu-id="149d7-1455">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="149d7-1455">Type of authentication.</span></span> | <span data-ttu-id="149d7-1456">cadena.</span><span class="sxs-lookup"><span data-stu-id="149d7-1456">string.</span></span> <span data-ttu-id="149d7-1457">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="149d7-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="149d7-1458">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1458">Yes</span></span> 
<span data-ttu-id="149d7-1459">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1459">username</span></span> | <span data-ttu-id="149d7-1460">Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="149d7-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="149d7-1461">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1461">string</span></span> | <span data-ttu-id="149d7-1462">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1462">Yes</span></span>
<span data-ttu-id="149d7-1463">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1463">password</span></span> | <span data-ttu-id="149d7-1464">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1464">Password for hello user.</span></span> | <span data-ttu-id="149d7-1465">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1465">string</span></span> | <span data-ttu-id="149d7-1466">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1466">Yes</span></span>
<span data-ttu-id="149d7-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1467">gatewayName</span></span> | <span data-ttu-id="149d7-1468">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP HANA de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="149d7-1469">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1469">string</span></span> | <span data-ttu-id="149d7-1470">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1470">Yes</span></span>
<span data-ttu-id="149d7-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1471">encryptedCredential</span></span> | <span data-ttu-id="149d7-1472">Hola cifra la cadena de credenciales.</span><span class="sxs-lookup"><span data-stu-id="149d7-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="149d7-1473">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1473">string</span></span> | <span data-ttu-id="149d7-1474">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-1475">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1475">Example</span></span>

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
<span data-ttu-id="149d7-1476">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="149d7-1477">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1477">Dataset</span></span>
<span data-ttu-id="149d7-1478">toodefine un conjunto de datos SAP HANA, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="149d7-1479">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de Hola de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="149d7-1480">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1480">Example</span></span>

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
<span data-ttu-id="149d7-1481">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1482">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1483">Si va a copiar datos desde un almacén de datos de SAP HANA, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1484">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1484">Property</span></span> | <span data-ttu-id="149d7-1485">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1485">Description</span></span> | <span data-ttu-id="149d7-1486">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1486">Allowed values</span></span> | <span data-ttu-id="149d7-1487">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1488">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1488">query</span></span> | <span data-ttu-id="149d7-1489">Especifica Hola SQL permite consultar tooread datos de instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="149d7-1490">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1490">SQL query.</span></span> | <span data-ttu-id="149d7-1491">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-1492">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1492">Example</span></span>


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

<span data-ttu-id="149d7-1493">Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="149d7-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="149d7-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1495">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1495">Linked service</span></span>
<span data-ttu-id="149d7-1496">Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="149d7-1497">Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="149d7-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="149d7-1498">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="149d7-1499">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1499">Property</span></span> | <span data-ttu-id="149d7-1500">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1500">Description</span></span> | <span data-ttu-id="149d7-1501">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1502">type</span><span class="sxs-lookup"><span data-stu-id="149d7-1502">type</span></span> |<span data-ttu-id="149d7-1503">propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="149d7-1504">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1504">Yes</span></span> |
| <span data-ttu-id="149d7-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-1505">connectionString</span></span> |<span data-ttu-id="149d7-1506">Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="149d7-1507">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1507">Yes</span></span> |
| <span data-ttu-id="149d7-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1508">gatewayName</span></span> |<span data-ttu-id="149d7-1509">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="149d7-1510">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1510">Yes</span></span> |
| <span data-ttu-id="149d7-1511">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1511">username</span></span> |<span data-ttu-id="149d7-1512">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="149d7-1513">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="149d7-1514">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1514">No</span></span> |
| <span data-ttu-id="149d7-1515">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1515">password</span></span> |<span data-ttu-id="149d7-1516">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-1517">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1517">No</span></span> |

<span data-ttu-id="149d7-1518">Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):</span><span class="sxs-lookup"><span data-stu-id="149d7-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="149d7-1519">Ejemplo: JSON para usar autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="149d7-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="149d7-1520">Ejemplo: JSON para usar autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="149d7-1521">Si se especifiquen el nombre de usuario y contraseña, puerta de enlace usa hello tooimpersonate base de datos de usuario especificado cuenta tooconnect toohello local SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="149d7-1522">En caso contrario, la puerta de enlace conecta toohello SQL Server directamente con el contexto de seguridad de Hola de puerta de enlace (su cuenta de inicio).</span><span class="sxs-lookup"><span data-stu-id="149d7-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="149d7-1523">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1524">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1524">Dataset</span></span>
<span data-ttu-id="149d7-1525">toodefine un conjunto de datos de SQL Server, conjunto de hello **tipo** del conjunto de datos de hello demasiado**SqlServerTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1526">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1526">Property</span></span> | <span data-ttu-id="149d7-1527">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1527">Description</span></span> | <span data-ttu-id="149d7-1528">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1529">tableName</span></span> |<span data-ttu-id="149d7-1530">Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Server de Hola que servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="149d7-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="149d7-1531">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1532">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1532">Example</span></span>
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

<span data-ttu-id="149d7-1533">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="149d7-1534">Origen de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1535">Si va a copiar datos desde una base de datos de SQL Server, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1536">Property</span></span> | <span data-ttu-id="149d7-1537">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1537">Description</span></span> | <span data-ttu-id="149d7-1538">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1538">Allowed values</span></span> | <span data-ttu-id="149d7-1539">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="149d7-1540">sqlReaderQuery</span></span> |<span data-ttu-id="149d7-1541">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1542">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1542">SQL query string.</span></span> <span data-ttu-id="149d7-1543">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="149d7-1544">Puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="149d7-1545">Si no se especifica, Hola instrucción SQL ejecutada: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="149d7-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="149d7-1546">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1546">No</span></span> |
| <span data-ttu-id="149d7-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="149d7-1548">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="149d7-1549">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="149d7-1550">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1550">No</span></span> |
| <span data-ttu-id="149d7-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-1551">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-1552">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="149d7-1553">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="149d7-1553">Name/value pairs.</span></span> <span data-ttu-id="149d7-1554">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="149d7-1555">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1555">No</span></span> |

<span data-ttu-id="149d7-1556">Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Server origen tooget.</span><span class="sxs-lookup"><span data-stu-id="149d7-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="149d7-1557">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="149d7-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="149d7-1558">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="149d7-1559">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="149d7-1560">Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="149d7-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="149d7-1561">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="149d7-1562">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1562">Example</span></span>
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

<span data-ttu-id="149d7-1563">En este ejemplo, **sqlReaderQuery** se especifica para hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="149d7-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="149d7-1564">Hola actividad de copia ejecuta esta consulta contra Hola datos de saludo de tooget de origen de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="149d7-1565">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="149d7-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="149d7-1566">Hola sqlReaderQuery puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="149d7-1567">No es limitado tooonly Hola tabla establecido como Hola typeProperty de nombre de tabla del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="149d7-1568">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="149d7-1569">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="149d7-1570">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="149d7-1571">Receptor de SQL en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-1572">Si va a copiar la base de datos de SQL Server de tooa de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**SqlSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-1573">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1573">Property</span></span> | <span data-ttu-id="149d7-1574">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1574">Description</span></span> | <span data-ttu-id="149d7-1575">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1575">Allowed values</span></span> | <span data-ttu-id="149d7-1576">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-1577">writeBatchTimeout</span></span> |<span data-ttu-id="149d7-1578">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="149d7-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="149d7-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="149d7-1579">timespan</span></span><br/><br/> <span data-ttu-id="149d7-1580">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="149d7-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="149d7-1581">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1581">No</span></span> |
| <span data-ttu-id="149d7-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="149d7-1582">writeBatchSize</span></span> |<span data-ttu-id="149d7-1583">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="149d7-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="149d7-1584">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="149d7-1584">Integer (number of rows)</span></span> |<span data-ttu-id="149d7-1585">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="149d7-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="149d7-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="149d7-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="149d7-1587">Especificar la consulta para tooexecute de actividad de copia que se limpian los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="149d7-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="149d7-1588">Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información.</span><span class="sxs-lookup"><span data-stu-id="149d7-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="149d7-1589">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="149d7-1589">A query statement.</span></span> |<span data-ttu-id="149d7-1590">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1590">No</span></span> |
| <span data-ttu-id="149d7-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="149d7-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="149d7-1592">Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="149d7-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="149d7-1593">Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información.</span><span class="sxs-lookup"><span data-stu-id="149d7-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="149d7-1594">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="149d7-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="149d7-1595">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1595">No</span></span> |
| <span data-ttu-id="149d7-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="149d7-1597">Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="149d7-1598">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="149d7-1599">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1599">No</span></span> |
| <span data-ttu-id="149d7-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-1600">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-1601">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="149d7-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="149d7-1602">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="149d7-1602">Name/value pairs.</span></span> <span data-ttu-id="149d7-1603">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="149d7-1604">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1604">No</span></span> |
| <span data-ttu-id="149d7-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="149d7-1605">sqlWriterTableType</span></span> |<span data-ttu-id="149d7-1606">Especifique toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="149d7-1607">Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="149d7-1608">Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="149d7-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="149d7-1609">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="149d7-1609">A table type name.</span></span> |<span data-ttu-id="149d7-1610">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1611">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1611">Example</span></span>
<span data-ttu-id="149d7-1612">canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="149d7-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="149d7-1613">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="149d7-1614">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="149d7-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="149d7-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1616">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1616">Linked service</span></span>
<span data-ttu-id="149d7-1617">toodefine un Sybase vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**OnPremisesSybase**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1618">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1618">Property</span></span> | <span data-ttu-id="149d7-1619">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1619">Description</span></span> | <span data-ttu-id="149d7-1620">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1621">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1621">server</span></span> |<span data-ttu-id="149d7-1622">Nombre del servidor de Sybase Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="149d7-1623">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1623">Yes</span></span> |
| <span data-ttu-id="149d7-1624">database</span><span class="sxs-lookup"><span data-stu-id="149d7-1624">database</span></span> |<span data-ttu-id="149d7-1625">Nombre de base de datos de Sybase Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="149d7-1626">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1626">Yes</span></span> |
| <span data-ttu-id="149d7-1627">schema</span><span class="sxs-lookup"><span data-stu-id="149d7-1627">schema</span></span> |<span data-ttu-id="149d7-1628">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="149d7-1629">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1629">No</span></span> |
| <span data-ttu-id="149d7-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1630">authenticationType</span></span> |<span data-ttu-id="149d7-1631">Tipo de autenticación usa tooconnect toohello bases de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="149d7-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="149d7-1632">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="149d7-1633">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1633">Yes</span></span> |
| <span data-ttu-id="149d7-1634">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1634">username</span></span> |<span data-ttu-id="149d7-1635">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="149d7-1636">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1636">No</span></span> |
| <span data-ttu-id="149d7-1637">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1637">password</span></span> |<span data-ttu-id="149d7-1638">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-1639">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1639">No</span></span> |
| <span data-ttu-id="149d7-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1640">gatewayName</span></span> |<span data-ttu-id="149d7-1641">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Sybase local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="149d7-1642">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1643">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1643">Example</span></span>
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

<span data-ttu-id="149d7-1644">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1645">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1645">Dataset</span></span>
<span data-ttu-id="149d7-1646">toodefine un conjunto de datos de Sybase, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1647">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1647">Property</span></span> | <span data-ttu-id="149d7-1648">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1648">Description</span></span> | <span data-ttu-id="149d7-1649">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1650">tableName</span></span> |<span data-ttu-id="149d7-1651">Nombre de tabla de Hola Hola instancia de base de datos de Sybase que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="149d7-1652">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1653">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1653">Example</span></span>

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

<span data-ttu-id="149d7-1654">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1655">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1656">Si va a copiar datos desde una base de datos de Sybase, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1657">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1657">Property</span></span> | <span data-ttu-id="149d7-1658">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1658">Description</span></span> | <span data-ttu-id="149d7-1659">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1659">Allowed values</span></span> | <span data-ttu-id="149d7-1660">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1661">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1661">query</span></span> |<span data-ttu-id="149d7-1662">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1663">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1663">SQL query string.</span></span> <span data-ttu-id="149d7-1664">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-1665">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1666">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1666">Example</span></span>

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

<span data-ttu-id="149d7-1667">Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="149d7-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="149d7-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1669">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1669">Linked service</span></span>
<span data-ttu-id="149d7-1670">toodefine un Teradata el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesTeradata**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1671">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1671">Property</span></span> | <span data-ttu-id="149d7-1672">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1672">Description</span></span> | <span data-ttu-id="149d7-1673">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1674">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1674">server</span></span> |<span data-ttu-id="149d7-1675">Nombre del servidor de Teradata Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="149d7-1676">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1676">Yes</span></span> |
| <span data-ttu-id="149d7-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1677">authenticationType</span></span> |<span data-ttu-id="149d7-1678">Tipo de autenticación que utiliza la base de datos de Teradata tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="149d7-1679">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="149d7-1680">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1680">Yes</span></span> |
| <span data-ttu-id="149d7-1681">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1681">username</span></span> |<span data-ttu-id="149d7-1682">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="149d7-1683">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1683">No</span></span> |
| <span data-ttu-id="149d7-1684">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1684">password</span></span> |<span data-ttu-id="149d7-1685">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-1686">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1686">No</span></span> |
| <span data-ttu-id="149d7-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1687">gatewayName</span></span> |<span data-ttu-id="149d7-1688">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Teradata local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="149d7-1689">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1690">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1690">Example</span></span>
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

<span data-ttu-id="149d7-1691">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1692">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1692">Dataset</span></span>
<span data-ttu-id="149d7-1693">toodefine un conjunto de datos Teradata Blob, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="149d7-1694">Actualmente, no hay ninguna propiedad de tipo compatible con el conjunto de datos de hello Teradata.</span><span class="sxs-lookup"><span data-stu-id="149d7-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="149d7-1695">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1695">Example</span></span>
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

<span data-ttu-id="149d7-1696">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-1697">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1698">Si va a copiar datos desde una base de datos de Teradata, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1699">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1699">Property</span></span> | <span data-ttu-id="149d7-1700">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1700">Description</span></span> | <span data-ttu-id="149d7-1701">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1701">Allowed values</span></span> | <span data-ttu-id="149d7-1702">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1703">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1703">query</span></span> |<span data-ttu-id="149d7-1704">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1705">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1705">SQL query string.</span></span> <span data-ttu-id="149d7-1706">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-1707">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1708">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1708">Example</span></span>

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

<span data-ttu-id="149d7-1709">Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="149d7-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="149d7-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-1711">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1711">Linked service</span></span>
<span data-ttu-id="149d7-1712">toodefine un Casandra el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesCassandra**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1713">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1713">Property</span></span> | <span data-ttu-id="149d7-1714">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1714">Description</span></span> | <span data-ttu-id="149d7-1715">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1716">host</span><span class="sxs-lookup"><span data-stu-id="149d7-1716">host</span></span> |<span data-ttu-id="149d7-1717">Una o varias direcciones IP o nombres de host de los servidores de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="149d7-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="149d7-1718">Especifique una lista separada por comas de direcciones IP o servidores de tooall de tooconnect de nombres de host al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="149d7-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="149d7-1719">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1719">Yes</span></span> |
| <span data-ttu-id="149d7-1720">puerto</span><span class="sxs-lookup"><span data-stu-id="149d7-1720">port</span></span> |<span data-ttu-id="149d7-1721">Hola el puerto TCP que Hola server Casandra utiliza toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="149d7-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="149d7-1722">No. El valor predeterminado es 9042.</span><span class="sxs-lookup"><span data-stu-id="149d7-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="149d7-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1723">authenticationType</span></span> |<span data-ttu-id="149d7-1724">Básica o anónima</span><span class="sxs-lookup"><span data-stu-id="149d7-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="149d7-1725">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1725">Yes</span></span> |
| <span data-ttu-id="149d7-1726">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1726">username</span></span> |<span data-ttu-id="149d7-1727">Especifique el nombre de usuario para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="149d7-1728">Sí, si authenticationType se establece tooBasic.</span><span class="sxs-lookup"><span data-stu-id="149d7-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="149d7-1729">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1729">password</span></span> |<span data-ttu-id="149d7-1730">Especifique la contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="149d7-1731">Sí, si authenticationType se establece tooBasic.</span><span class="sxs-lookup"><span data-stu-id="149d7-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="149d7-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1732">gatewayName</span></span> |<span data-ttu-id="149d7-1733">nombre de Hola de puerta de enlace de Hola que es la base de datos de uso tooconnect toohello local Casandra.</span><span class="sxs-lookup"><span data-stu-id="149d7-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="149d7-1734">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1734">Yes</span></span> |
| <span data-ttu-id="149d7-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1735">encryptedCredential</span></span> |<span data-ttu-id="149d7-1736">Credencial cifrada por la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="149d7-1737">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1738">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1738">Example</span></span>

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

<span data-ttu-id="149d7-1739">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-1740">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1740">Dataset</span></span>
<span data-ttu-id="149d7-1741">toodefine un conjunto de datos Casandra conjunto hello **tipo** del conjunto de datos de hello demasiado**CassandraTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1742">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1742">Property</span></span> | <span data-ttu-id="149d7-1743">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1743">Description</span></span> | <span data-ttu-id="149d7-1744">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="149d7-1745">keyspace</span></span> |<span data-ttu-id="149d7-1746">Nombre de keyspace de Hola o esquema de base de datos de Casandra.</span><span class="sxs-lookup"><span data-stu-id="149d7-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="149d7-1747">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="149d7-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="149d7-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-1748">tableName</span></span> |<span data-ttu-id="149d7-1749">Nombre de tabla de hello en la base de datos de Casandra.</span><span class="sxs-lookup"><span data-stu-id="149d7-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="149d7-1750">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="149d7-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1751">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1751">Example</span></span>

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

<span data-ttu-id="149d7-1752">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="149d7-1753">Origen de Cassandra en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1754">Si va a copiar datos desde Casandra, establezca hello **tipo de origen de** de hello actividad de copia demasiado**CassandraSource**y especificar después de propiedades en hello **origen** sección :</span><span class="sxs-lookup"><span data-stu-id="149d7-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1755">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1755">Property</span></span> | <span data-ttu-id="149d7-1756">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1756">Description</span></span> | <span data-ttu-id="149d7-1757">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1757">Allowed values</span></span> | <span data-ttu-id="149d7-1758">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1759">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1759">query</span></span> |<span data-ttu-id="149d7-1760">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1761">Consulta SQL-92 o consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="149d7-1762">Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL).</span><span class="sxs-lookup"><span data-stu-id="149d7-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="149d7-1763">Al usar una consulta SQL, especifique **keyspace name.table nombre** tabla de hello toorepresent desea tooquery.</span><span class="sxs-lookup"><span data-stu-id="149d7-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="149d7-1764">No (si tableName y el espacio de claves del conjunto de datos están definidos).</span><span class="sxs-lookup"><span data-stu-id="149d7-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="149d7-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="149d7-1765">consistencyLevel</span></span> |<span data-ttu-id="149d7-1766">el nivel de coherencia de Hello especifica cuántas réplicas debe responder tooa solicitud de lectura antes de devolver la aplicación de cliente de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="149d7-1767">Comprobaciones de Casandra Hola número de réplicas especificado para la solicitud de lectura de hello toosatisfy de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="149d7-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="149d7-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="149d7-1769">Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos).</span><span class="sxs-lookup"><span data-stu-id="149d7-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="149d7-1770">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-1770">No.</span></span> <span data-ttu-id="149d7-1771">El valor predeterminado es ONE.</span><span class="sxs-lookup"><span data-stu-id="149d7-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1772">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="149d7-1773">Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="149d7-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="149d7-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-1775">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1775">Linked service</span></span>
<span data-ttu-id="149d7-1776">toodefine un MongoDB el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesMongoDB**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1777">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1777">Property</span></span> | <span data-ttu-id="149d7-1778">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1778">Description</span></span> | <span data-ttu-id="149d7-1779">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1780">Servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-1780">server</span></span> |<span data-ttu-id="149d7-1781">IP dirección o nombre de host del servidor de MongoDB Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="149d7-1782">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1782">Yes</span></span> |
| <span data-ttu-id="149d7-1783">puerto</span><span class="sxs-lookup"><span data-stu-id="149d7-1783">port</span></span> |<span data-ttu-id="149d7-1784">El puerto TCP que Hola MongoDB server usa toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="149d7-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="149d7-1785">Valor predeterminado opcional: 27017</span><span class="sxs-lookup"><span data-stu-id="149d7-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="149d7-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-1786">authenticationType</span></span> |<span data-ttu-id="149d7-1787">Básica o anónima.</span><span class="sxs-lookup"><span data-stu-id="149d7-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="149d7-1788">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1788">Yes</span></span> |
| <span data-ttu-id="149d7-1789">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-1789">username</span></span> |<span data-ttu-id="149d7-1790">Tooaccess de cuenta de usuario MongoDB.</span><span class="sxs-lookup"><span data-stu-id="149d7-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="149d7-1791">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="149d7-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="149d7-1792">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1792">password</span></span> |<span data-ttu-id="149d7-1793">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1793">Password for hello user.</span></span> |<span data-ttu-id="149d7-1794">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="149d7-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="149d7-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="149d7-1795">authSource</span></span> |<span data-ttu-id="149d7-1796">Nombre de base de datos de MongoDB de Hola que quiere toouse toocheck sus credenciales de autenticación.</span><span class="sxs-lookup"><span data-stu-id="149d7-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="149d7-1797">Opcional (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="149d7-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="149d7-1798">valor predeterminado: utiliza la cuenta de administrador de Hola y base de datos de hello especificada mediante la propiedad databaseName.</span><span class="sxs-lookup"><span data-stu-id="149d7-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="149d7-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="149d7-1799">databaseName</span></span> |<span data-ttu-id="149d7-1800">Nombre de base de datos de MongoDB de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="149d7-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="149d7-1801">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1801">Yes</span></span> |
| <span data-ttu-id="149d7-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1802">gatewayName</span></span> |<span data-ttu-id="149d7-1803">Nombre de puerta de enlace de Hola que tiene acceso a almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="149d7-1804">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1804">Yes</span></span> |
| <span data-ttu-id="149d7-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1805">encryptedCredential</span></span> |<span data-ttu-id="149d7-1806">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="149d7-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="149d7-1807">Opcional</span><span class="sxs-lookup"><span data-stu-id="149d7-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1808">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="149d7-1809">Para obtener más información, vea el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1810">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1810">Dataset</span></span>
<span data-ttu-id="149d7-1811">toodefine un conjunto de datos MongoDB, conjunto hello **tipo** del conjunto de datos de hello demasiado**MongoDbCollection**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1812">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1812">Property</span></span> | <span data-ttu-id="149d7-1813">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1813">Description</span></span> | <span data-ttu-id="149d7-1814">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="149d7-1815">collectionName</span></span> |<span data-ttu-id="149d7-1816">Nombre de colección de hello en la base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="149d7-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="149d7-1817">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1818">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1818">Example</span></span>

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

<span data-ttu-id="149d7-1819">Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="149d7-1820">Origen de MongoDB en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1821">Si va a copiar datos de MongoDB, establezca hello **tipo de origen de** de hello actividad de copia demasiado**MongoDbSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1822">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1822">Property</span></span> | <span data-ttu-id="149d7-1823">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1823">Description</span></span> | <span data-ttu-id="149d7-1824">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1824">Allowed values</span></span> | <span data-ttu-id="149d7-1825">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1826">query</span><span class="sxs-lookup"><span data-stu-id="149d7-1826">query</span></span> |<span data-ttu-id="149d7-1827">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-1828">Cadena de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="149d7-1828">SQL-92 query string.</span></span> <span data-ttu-id="149d7-1829">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-1830">No (si se especifica **collectionName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="149d7-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1831">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1831">Example</span></span>

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

<span data-ttu-id="149d7-1832">Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="149d7-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="149d7-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-1834">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1834">Linked service</span></span>
<span data-ttu-id="149d7-1835">toodefine un S3 Amazon el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**AwsAccessKey**y especificar después de propiedades en hello **typeProperties** sección :</span><span class="sxs-lookup"><span data-stu-id="149d7-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-1836">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1836">Property</span></span> | <span data-ttu-id="149d7-1837">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1837">Description</span></span> | <span data-ttu-id="149d7-1838">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1838">Allowed values</span></span> | <span data-ttu-id="149d7-1839">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="149d7-1840">accessKeyID</span></span> |<span data-ttu-id="149d7-1841">Id. de clave de acceso de los secretos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="149d7-1842">cadena</span><span class="sxs-lookup"><span data-stu-id="149d7-1842">string</span></span> |<span data-ttu-id="149d7-1843">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1843">Yes</span></span> |
| <span data-ttu-id="149d7-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="149d7-1844">secretAccessKey</span></span> |<span data-ttu-id="149d7-1845">clave de acceso de los secretos de Hello propio.</span><span class="sxs-lookup"><span data-stu-id="149d7-1845">hello secret access key itself.</span></span> |<span data-ttu-id="149d7-1846">Cadena secreta cifrada</span><span class="sxs-lookup"><span data-stu-id="149d7-1846">Encrypted secret string</span></span> |<span data-ttu-id="149d7-1847">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-1848">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1848">Example</span></span>
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

<span data-ttu-id="149d7-1849">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1850">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1850">Dataset</span></span>
<span data-ttu-id="149d7-1851">conjunto de datos de toodefine un S3 de Amazon, conjunto hello **tipo** del conjunto de datos de hello demasiado**AmazonS3**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1852">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1852">Property</span></span> | <span data-ttu-id="149d7-1853">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1853">Description</span></span> | <span data-ttu-id="149d7-1854">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1854">Allowed values</span></span> | <span data-ttu-id="149d7-1855">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="149d7-1856">bucketName</span></span> |<span data-ttu-id="149d7-1857">nombre del depósito de Hello S3.</span><span class="sxs-lookup"><span data-stu-id="149d7-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="149d7-1858">String</span><span class="sxs-lookup"><span data-stu-id="149d7-1858">String</span></span> |<span data-ttu-id="149d7-1859">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1859">Yes</span></span> |
| <span data-ttu-id="149d7-1860">key</span><span class="sxs-lookup"><span data-stu-id="149d7-1860">key</span></span> |<span data-ttu-id="149d7-1861">clave del objeto Hola S3.</span><span class="sxs-lookup"><span data-stu-id="149d7-1861">hello S3 object key.</span></span> |<span data-ttu-id="149d7-1862">String</span><span class="sxs-lookup"><span data-stu-id="149d7-1862">String</span></span> |<span data-ttu-id="149d7-1863">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1863">No</span></span> |
| <span data-ttu-id="149d7-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="149d7-1864">prefix</span></span> |<span data-ttu-id="149d7-1865">Prefijo para la clave del objeto Hola S3.</span><span class="sxs-lookup"><span data-stu-id="149d7-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="149d7-1866">Se seleccionan objetos cuyas claves comienzan por este prefijo.</span><span class="sxs-lookup"><span data-stu-id="149d7-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="149d7-1867">Se aplica solo cuando la clave está vacía.</span><span class="sxs-lookup"><span data-stu-id="149d7-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="149d7-1868">string</span><span class="sxs-lookup"><span data-stu-id="149d7-1868">String</span></span> |<span data-ttu-id="149d7-1869">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1869">No</span></span> |
| <span data-ttu-id="149d7-1870">versión</span><span class="sxs-lookup"><span data-stu-id="149d7-1870">version</span></span> |<span data-ttu-id="149d7-1871">versión de Hola del objeto de S3 si está habilitado el control de versiones de S3.</span><span class="sxs-lookup"><span data-stu-id="149d7-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="149d7-1872">String</span><span class="sxs-lookup"><span data-stu-id="149d7-1872">String</span></span> |<span data-ttu-id="149d7-1873">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1873">No</span></span> |
| <span data-ttu-id="149d7-1874">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-1874">format</span></span> | <span data-ttu-id="149d7-1875">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-1876">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-1877">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-1878">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-1879">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1879">No</span></span> | |
| <span data-ttu-id="149d7-1880">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-1880">compression</span></span> | <span data-ttu-id="149d7-1881">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-1882">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-1883">Hola admitida niveles son: **óptimo** y **más rápido**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-1884">Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-1885">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="149d7-1886">bucketName + clave especifica la ubicación de Hola Hola S3 de objeto de donde depósitos es el contenedor de raíz de Hola para S3 objetos y la clave es objeto de tooS3 de ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="149d7-1887">Ejemplo: Conjunto de datos de ejemplo con prefijo</span><span class="sxs-lookup"><span data-stu-id="149d7-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="149d7-1888">Ejemplo: Conjunto de datos de ejemplo (con versión)</span><span class="sxs-lookup"><span data-stu-id="149d7-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="149d7-1889">Ejemplo: Rutas de acceso dinámicas para S3</span><span class="sxs-lookup"><span data-stu-id="149d7-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="149d7-1890">En el ejemplo de Hola, utilizamos valores fijos para las propiedades de clave y bucketName en el conjunto de datos de hello S3 de Amazon.</span><span class="sxs-lookup"><span data-stu-id="149d7-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="149d7-1891">Puede tener factoría de datos calcular clave hello y bucketName dinámicamente en tiempo de ejecución mediante el uso de variables del sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="149d7-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="149d7-1892">Puede hacer Hola mismo para la propiedad de prefijo de Hola de un conjunto de datos de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="149d7-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="149d7-1893">Consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) para ver una lista de funciones y variables admitidas.</span><span class="sxs-lookup"><span data-stu-id="149d7-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="149d7-1894">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="149d7-1895">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1896">Si va a copiar datos de Amazon S3, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección :</span><span class="sxs-lookup"><span data-stu-id="149d7-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="149d7-1897">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1897">Property</span></span> | <span data-ttu-id="149d7-1898">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1898">Description</span></span> | <span data-ttu-id="149d7-1899">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1899">Allowed values</span></span> | <span data-ttu-id="149d7-1900">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-1901">recursive</span></span> |<span data-ttu-id="149d7-1902">Especifica si toorecursively lista S3 objetos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="149d7-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="149d7-1903">true/false</span></span> |<span data-ttu-id="149d7-1904">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-1905">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1905">Example</span></span>


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

<span data-ttu-id="149d7-1906">Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="149d7-1907">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="149d7-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-1908">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1908">Linked service</span></span>
<span data-ttu-id="149d7-1909">Puede vincular un generador de datos de Azure local tooan de sistema de archivo con hello **servidor de archivos local** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="149d7-1910">Hello en la tabla siguiente proporciona descripciones para los elementos JSON que sean específico toohello servicio servidor de archivos local vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="149d7-1911">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1911">Property</span></span> | <span data-ttu-id="149d7-1912">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1912">Description</span></span> | <span data-ttu-id="149d7-1913">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1914">type</span><span class="sxs-lookup"><span data-stu-id="149d7-1914">type</span></span> |<span data-ttu-id="149d7-1915">Asegúrese de que la propiedad de tipo hello está establecido demasiado**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="149d7-1916">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1916">Yes</span></span> |
| <span data-ttu-id="149d7-1917">host</span><span class="sxs-lookup"><span data-stu-id="149d7-1917">host</span></span> |<span data-ttu-id="149d7-1918">Especifica la ruta de acceso de raíz de Hola de carpeta de Hola que desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="149d7-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="149d7-1919">Utilice el carácter de escape de hello ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="149d7-1920">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="149d7-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="149d7-1921">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1921">Yes</span></span> |
| <span data-ttu-id="149d7-1922">userid</span><span class="sxs-lookup"><span data-stu-id="149d7-1922">userid</span></span> |<span data-ttu-id="149d7-1923">Especifique el identificador de Hola Hola del usuario de que tiene acceso toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="149d7-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="149d7-1924">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="149d7-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="149d7-1925">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-1925">password</span></span> |<span data-ttu-id="149d7-1926">Especifique la contraseña de hello para el usuario de hello (userid).</span><span class="sxs-lookup"><span data-stu-id="149d7-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="149d7-1927">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="149d7-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="149d7-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1928">encryptedCredential</span></span> |<span data-ttu-id="149d7-1929">Especifique las credenciales de hello cifrada que pueden obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="149d7-1930">No (si elige toospecify identificador de usuario y una contraseña en texto sin formato)</span><span class="sxs-lookup"><span data-stu-id="149d7-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="149d7-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-1931">gatewayName</span></span> |<span data-ttu-id="149d7-1932">Especifica el nombre de Hola de puerta de enlace de Hola que factoría de datos debe usar el servidor de archivos de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="149d7-1933">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="149d7-1934">Definiciones de ruta de acceso a la carpeta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="149d7-1935">Escenario</span><span class="sxs-lookup"><span data-stu-id="149d7-1935">Scenario</span></span> | <span data-ttu-id="149d7-1936">Host en definición de servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-1936">Host in linked service definition</span></span> | <span data-ttu-id="149d7-1937">folderPath en definición de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="149d7-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1938">Carpeta local en la máquina de Data Management Gateway:: </span><span class="sxs-lookup"><span data-stu-id="149d7-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="149d7-1939">Ejemplos: D:\\\* o D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="149d7-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="149d7-1940">D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="149d7-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="149d7-1941">localhost (para versiones anteriores a Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="149d7-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="149d7-1942">\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="149d7-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="149d7-1943">D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0)</span><span class="sxs-lookup"><span data-stu-id="149d7-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="149d7-1944">Carpeta compartida remota: </span><span class="sxs-lookup"><span data-stu-id="149d7-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="149d7-1945">Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="149d7-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="149d7-1946">\\\\\\\\myserver\\\\</span><span class="sxs-lookup"><span data-stu-id="149d7-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="149d7-1947">.\\\\ o carpeta\\\\subcarpeta</span><span class="sxs-lookup"><span data-stu-id="149d7-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="149d7-1948">Ejemplo: uso de nombre de usuario y contraseña en texto sin formato</span><span class="sxs-lookup"><span data-stu-id="149d7-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="149d7-1949">Ejemplo: uso de encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="149d7-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="149d7-1950">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-1951">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-1951">Dataset</span></span>
<span data-ttu-id="149d7-1952">toodefine un conjunto de datos del sistema de archivos, conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-1953">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1953">Property</span></span> | <span data-ttu-id="149d7-1954">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1954">Description</span></span> | <span data-ttu-id="149d7-1955">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-1956">folderPath</span></span> |<span data-ttu-id="149d7-1957">Especifica la carpeta de hello subruta toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="149d7-1958">Utilice el carácter de escape de hello ' \' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="149d7-1959">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="149d7-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="149d7-1960">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="149d7-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="149d7-1961">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-1961">Yes</span></span> |
| <span data-ttu-id="149d7-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-1962">fileName</span></span> |<span data-ttu-id="149d7-1963">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="149d7-1964">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="149d7-1965">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de Hola del archivo hello generado es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="149d7-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="149d7-1966">`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="149d7-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="149d7-1967">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1967">No</span></span> |
| <span data-ttu-id="149d7-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="149d7-1968">fileFilter</span></span> |<span data-ttu-id="149d7-1969">Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="149d7-1970">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="149d7-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="149d7-1971">Ejemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="149d7-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="149d7-1972">Ejemplo 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="149d7-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="149d7-1973">Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="149d7-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="149d7-1974">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1974">No</span></span> |
| <span data-ttu-id="149d7-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-1975">partitionedBy</span></span> |<span data-ttu-id="149d7-1976">Puede usar partitionedBy toospecify dinámica folderPath/nombre de archivo para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="149d7-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="149d7-1977">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-1978">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1978">No</span></span> |
| <span data-ttu-id="149d7-1979">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-1979">format</span></span> | <span data-ttu-id="149d7-1980">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-1981">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-1982">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-1983">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-1984">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1984">No</span></span> |
| <span data-ttu-id="149d7-1985">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-1985">compression</span></span> | <span data-ttu-id="149d7-1986">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-1987">Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido).</span><span class="sxs-lookup"><span data-stu-id="149d7-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-1988">consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-1989">No</span><span class="sxs-lookup"><span data-stu-id="149d7-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="149d7-1990">No se puede usar fileName y fileFilter a la vez.</span><span class="sxs-lookup"><span data-stu-id="149d7-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-1991">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-1991">Example</span></span>

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

<span data-ttu-id="149d7-1992">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="149d7-1993">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="149d7-1994">Si va a copiar datos de sistema de archivos, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-1995">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-1995">Property</span></span> | <span data-ttu-id="149d7-1996">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-1996">Description</span></span> | <span data-ttu-id="149d7-1997">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-1997">Allowed values</span></span> | <span data-ttu-id="149d7-1998">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-1999">recursive</span></span> |<span data-ttu-id="149d7-2000">Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-2001">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="149d7-2001">True, False (default)</span></span> |<span data-ttu-id="149d7-2002">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2003">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2003">Example</span></span>

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
<span data-ttu-id="149d7-2004">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="149d7-2005">Receptor de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="149d7-2006">Si va a copiar datos tooFile sistema, establezca hello **tipo de receptor** de hello actividad de copia demasiado**FileSystemSink**y especificar después de propiedades en hello **receptor** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="149d7-2007">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2007">Property</span></span> | <span data-ttu-id="149d7-2008">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2008">Description</span></span> | <span data-ttu-id="149d7-2009">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2009">Allowed values</span></span> | <span data-ttu-id="149d7-2010">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="149d7-2011">copyBehavior</span></span> |<span data-ttu-id="149d7-2012">Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="149d7-2013">**PreserveHierarchy:** conserva la jerarquía de archivos de hello en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="149d7-2014">Es decir, ruta de acceso relativa de Hola de carpeta de origen de toohello de archivo de origen de hello es Hola igual a la ruta de acceso relativa de Hola de carpeta de destino de toohello de archivo de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="149d7-2015">**FlattenHierarchy:** todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="149d7-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="149d7-2016">archivos de destino de Hola se crean con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="149d7-2017">**MergeFiles:** combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="149d7-2018">Si se especifica el nombre de blob/nombre de archivo de hello, nombre de archivo combinado de hello es nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="149d7-2019">De lo contrario, es un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="149d7-2020">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2020">No</span></span> |
<span data-ttu-id="149d7-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="149d7-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-2022">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2022">Example</span></span>

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

<span data-ttu-id="149d7-2023">Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="149d7-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="149d7-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-2025">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2025">Linked service</span></span>
<span data-ttu-id="149d7-2026">toodefine FTP el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**FtpServer**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2027">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2027">Property</span></span> | <span data-ttu-id="149d7-2028">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2028">Description</span></span> | <span data-ttu-id="149d7-2029">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2029">Required</span></span> | <span data-ttu-id="149d7-2030">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149d7-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2031">host</span><span class="sxs-lookup"><span data-stu-id="149d7-2031">host</span></span> |<span data-ttu-id="149d7-2032">Nombre o dirección IP del servidor FTP de Hola</span><span class="sxs-lookup"><span data-stu-id="149d7-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="149d7-2033">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="149d7-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2034">authenticationType</span></span> |<span data-ttu-id="149d7-2035">Especificar el tipo de autenticación</span><span class="sxs-lookup"><span data-stu-id="149d7-2035">Specify authentication type</span></span> |<span data-ttu-id="149d7-2036">yes</span><span class="sxs-lookup"><span data-stu-id="149d7-2036">Yes</span></span> |<span data-ttu-id="149d7-2037">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="149d7-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="149d7-2038">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2038">username</span></span> |<span data-ttu-id="149d7-2039">Usuario que tiene acceso toohello FTP server</span><span class="sxs-lookup"><span data-stu-id="149d7-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="149d7-2040">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="149d7-2041">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2041">password</span></span> |<span data-ttu-id="149d7-2042">Contraseña de usuario de hello (nombre de usuario)</span><span class="sxs-lookup"><span data-stu-id="149d7-2042">Password for hello user (username)</span></span> |<span data-ttu-id="149d7-2043">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="149d7-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-2044">encryptedCredential</span></span> |<span data-ttu-id="149d7-2045">Servidor FTP de credenciales cifradas tooaccess Hola</span><span class="sxs-lookup"><span data-stu-id="149d7-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="149d7-2046">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="149d7-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2047">gatewayName</span></span> |<span data-ttu-id="149d7-2048">Nombre de puerta de enlace tooconnect tooan de hello Data Management Gateway servidor FTP local</span><span class="sxs-lookup"><span data-stu-id="149d7-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="149d7-2049">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="149d7-2050">puerto</span><span class="sxs-lookup"><span data-stu-id="149d7-2050">port</span></span> |<span data-ttu-id="149d7-2051">Puerto en qué Hola FTP está escuchando el servidor</span><span class="sxs-lookup"><span data-stu-id="149d7-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="149d7-2052">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2052">No</span></span> |<span data-ttu-id="149d7-2053">21</span><span class="sxs-lookup"><span data-stu-id="149d7-2053">21</span></span> |
| <span data-ttu-id="149d7-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="149d7-2054">enableSsl</span></span> |<span data-ttu-id="149d7-2055">Especifique si toouse FTP a través de canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="149d7-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="149d7-2056">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2056">No</span></span> |<span data-ttu-id="149d7-2057">true</span><span class="sxs-lookup"><span data-stu-id="149d7-2057">true</span></span> |
| <span data-ttu-id="149d7-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="149d7-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="149d7-2059">Especifica si, cuando se utiliza FTP a través de canal SSL/TLS, se validación de certificado de servidor SSL de tooenable</span><span class="sxs-lookup"><span data-stu-id="149d7-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="149d7-2060">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2060">No</span></span> |<span data-ttu-id="149d7-2061">true</span><span class="sxs-lookup"><span data-stu-id="149d7-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="149d7-2062">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="149d7-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="149d7-2063">Ejemplo: Uso de nombre de usuario y contraseña en texto sin formato para la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="149d7-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="149d7-2064">Ejemplo: Uso de puerto, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="149d7-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="149d7-2065">Ejemplo: Uso de encryptedCredential para la autenticación y la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="149d7-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="149d7-2066">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-2067">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2067">Dataset</span></span>
<span data-ttu-id="149d7-2068">conjunto de datos de toodefine FTP, conjunto de Hola **tipo** del conjunto de datos de Hola demasiado**recurso compartido de archivos**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2069">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2069">Property</span></span> | <span data-ttu-id="149d7-2070">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2070">Description</span></span> | <span data-ttu-id="149d7-2071">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-2072">folderPath</span></span> |<span data-ttu-id="149d7-2073">Carpeta de toohello de ruta de acceso de Sub.</span><span class="sxs-lookup"><span data-stu-id="149d7-2073">Sub path toohello folder.</span></span> <span data-ttu-id="149d7-2074">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="149d7-2075">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="149d7-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="149d7-2076">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="149d7-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="149d7-2077">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2077">Yes</span></span> 
| <span data-ttu-id="149d7-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-2078">fileName</span></span> |<span data-ttu-id="149d7-2079">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="149d7-2080">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="149d7-2081">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato:</span><span class="sxs-lookup"><span data-stu-id="149d7-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="149d7-2082">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="149d7-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="149d7-2083">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2083">No</span></span> |
| <span data-ttu-id="149d7-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="149d7-2084">fileFilter</span></span> |<span data-ttu-id="149d7-2085">Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="149d7-2086">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="149d7-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="149d7-2087">Ejemplos 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="149d7-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="149d7-2088">Ejemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="149d7-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="149d7-2089">fileFilter es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="149d7-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="149d7-2090">Esta propiedad no es compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="149d7-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="149d7-2091">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2091">No</span></span> |
| <span data-ttu-id="149d7-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-2092">partitionedBy</span></span> |<span data-ttu-id="149d7-2093">partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="149d7-2094">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-2095">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2095">No</span></span> |
| <span data-ttu-id="149d7-2096">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-2096">format</span></span> | <span data-ttu-id="149d7-2097">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-2098">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-2099">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-2100">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-2101">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2101">No</span></span> |
| <span data-ttu-id="149d7-2102">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-2102">compression</span></span> | <span data-ttu-id="149d7-2103">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-2104">Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido).</span><span class="sxs-lookup"><span data-stu-id="149d7-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-2105">Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-2106">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2106">No</span></span> |
| <span data-ttu-id="149d7-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="149d7-2107">useBinaryTransfer</span></span> |<span data-ttu-id="149d7-2108">Especifica si se usará el modo de transferencia binario.</span><span class="sxs-lookup"><span data-stu-id="149d7-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="149d7-2109">Su valor es true para el modo binario y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="149d7-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="149d7-2110">Valor predeterminado: true.</span><span class="sxs-lookup"><span data-stu-id="149d7-2110">Default value: True.</span></span> <span data-ttu-id="149d7-2111">Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="149d7-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="149d7-2112">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="149d7-2113">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-2114">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="149d7-2115">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="149d7-2116">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2117">Si va a copiar datos desde un servidor FTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2118">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2118">Property</span></span> | <span data-ttu-id="149d7-2119">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2119">Description</span></span> | <span data-ttu-id="149d7-2120">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2120">Allowed values</span></span> | <span data-ttu-id="149d7-2121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-2122">recursive</span></span> |<span data-ttu-id="149d7-2123">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-2124">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="149d7-2124">True, False (default)</span></span> |<span data-ttu-id="149d7-2125">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2126">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2126">Example</span></span>

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

<span data-ttu-id="149d7-2127">Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="149d7-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="149d7-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-2129">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2129">Linked service</span></span>
<span data-ttu-id="149d7-2130">toodefine un HDFS el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Hdfs**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2131">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2131">Property</span></span> | <span data-ttu-id="149d7-2132">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2132">Description</span></span> | <span data-ttu-id="149d7-2133">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2134">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2134">type</span></span> |<span data-ttu-id="149d7-2135">propiedad de tipo Hello debe establecerse en: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="149d7-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="149d7-2136">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2136">Yes</span></span> |
| <span data-ttu-id="149d7-2137">URL</span><span class="sxs-lookup"><span data-stu-id="149d7-2137">Url</span></span> |<span data-ttu-id="149d7-2138">Dirección URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="149d7-2138">URL toohello HDFS</span></span> |<span data-ttu-id="149d7-2139">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2139">Yes</span></span> |
| <span data-ttu-id="149d7-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2140">authenticationType</span></span> |<span data-ttu-id="149d7-2141">Anónima o Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="149d7-2142">toouse **la autenticación Kerberos** para conector HDFS, consulte demasiado[en esta sección](#use-kerberos-authentication-for-hdfs-connector) tooset del entorno local en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="149d7-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="149d7-2143">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2143">Yes</span></span> |
| <span data-ttu-id="149d7-2144">userName</span><span class="sxs-lookup"><span data-stu-id="149d7-2144">userName</span></span> |<span data-ttu-id="149d7-2145">Nombre de usuario para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="149d7-2146">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="149d7-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="149d7-2147">contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2147">password</span></span> |<span data-ttu-id="149d7-2148">Contraseña para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="149d7-2149">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="149d7-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="149d7-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2150">gatewayName</span></span> |<span data-ttu-id="149d7-2151">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="149d7-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="149d7-2152">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2152">Yes</span></span> |
| <span data-ttu-id="149d7-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-2153">encryptedCredential</span></span> |<span data-ttu-id="149d7-2154">[Nueva AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) salida de credenciales de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="149d7-2155">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="149d7-2156">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="149d7-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="149d7-2157">Ejemplo: Uso de autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="149d7-2158">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-2159">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2159">Dataset</span></span>
<span data-ttu-id="149d7-2160">toodefine un conjunto de datos HDFS conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2161">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2161">Property</span></span> | <span data-ttu-id="149d7-2162">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2162">Description</span></span> | <span data-ttu-id="149d7-2163">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-2164">folderPath</span></span> |<span data-ttu-id="149d7-2165">Carpeta de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="149d7-2165">Path toohello folder.</span></span> <span data-ttu-id="149d7-2166">Ejemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="149d7-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="149d7-2167">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="149d7-2168">Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="149d7-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="149d7-2169">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="149d7-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="149d7-2170">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2170">Yes</span></span> |
| <span data-ttu-id="149d7-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-2171">fileName</span></span> |<span data-ttu-id="149d7-2172">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="149d7-2173">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="149d7-2174">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato:</span><span class="sxs-lookup"><span data-stu-id="149d7-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="149d7-2175">Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="149d7-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="149d7-2176">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2176">No</span></span> |
| <span data-ttu-id="149d7-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-2177">partitionedBy</span></span> |<span data-ttu-id="149d7-2178">partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="149d7-2179">Por ejemplo, folderPath se parametriza para cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-2180">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2180">No</span></span> |
| <span data-ttu-id="149d7-2181">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-2181">format</span></span> | <span data-ttu-id="149d7-2182">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-2183">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-2184">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-2185">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-2186">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2186">No</span></span> |
| <span data-ttu-id="149d7-2187">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-2187">compression</span></span> | <span data-ttu-id="149d7-2188">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-2189">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-2190">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-2191">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-2192">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="149d7-2193">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-2194">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2194">Example</span></span>

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

<span data-ttu-id="149d7-2195">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="149d7-2196">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2197">Si va a copiar datos desde HDFS, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="149d7-2198">**FileSystemSource** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="149d7-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="149d7-2199">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2199">Property</span></span> | <span data-ttu-id="149d7-2200">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2200">Description</span></span> | <span data-ttu-id="149d7-2201">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2201">Allowed values</span></span> | <span data-ttu-id="149d7-2202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-2203">recursive</span></span> |<span data-ttu-id="149d7-2204">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-2205">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="149d7-2205">True, False (default)</span></span> |<span data-ttu-id="149d7-2206">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2207">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2207">Example</span></span>

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

<span data-ttu-id="149d7-2208">Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="149d7-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="149d7-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-2210">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2210">Linked service</span></span>
<span data-ttu-id="149d7-2211">toodefine un SFTP el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Sftp**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2212">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2212">Property</span></span> | <span data-ttu-id="149d7-2213">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2213">Description</span></span> | <span data-ttu-id="149d7-2214">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2215">host</span><span class="sxs-lookup"><span data-stu-id="149d7-2215">host</span></span> | <span data-ttu-id="149d7-2216">Nombre o dirección IP del servidor SFTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="149d7-2217">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2217">Yes</span></span> |
| <span data-ttu-id="149d7-2218">puerto</span><span class="sxs-lookup"><span data-stu-id="149d7-2218">port</span></span> |<span data-ttu-id="149d7-2219">Puerto en qué Hola SFTP servidor está escuchando.</span><span class="sxs-lookup"><span data-stu-id="149d7-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="149d7-2220">es el valor predeterminado de Hello: 21</span><span class="sxs-lookup"><span data-stu-id="149d7-2220">hello default value is: 21</span></span> |<span data-ttu-id="149d7-2221">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2221">No</span></span> |
| <span data-ttu-id="149d7-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2222">authenticationType</span></span> |<span data-ttu-id="149d7-2223">Especifique el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="149d7-2223">Specify authentication type.</span></span> <span data-ttu-id="149d7-2224">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="149d7-2225">Consulte demasiado[mediante la autenticación básica](#using-basic-authentication) y [utilizando SSH autenticación de clave pública](#using-ssh-public-key-authentication) secciones en más propiedades y ejemplos JSON, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="149d7-2226">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2226">Yes</span></span> |
| <span data-ttu-id="149d7-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="149d7-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="149d7-2228">Especificar si tooskip validación de clave de host.</span><span class="sxs-lookup"><span data-stu-id="149d7-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="149d7-2229">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2229">No.</span></span> <span data-ttu-id="149d7-2230">Hola valor predeterminado: false</span><span class="sxs-lookup"><span data-stu-id="149d7-2230">hello default value: false</span></span> |
| <span data-ttu-id="149d7-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="149d7-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="149d7-2232">Especifique la huella dactilar de Hola de clave de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="149d7-2233">Sí si hello `skipHostKeyValidation` se establece toofalse.</span><span class="sxs-lookup"><span data-stu-id="149d7-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="149d7-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2234">gatewayName</span></span> |<span data-ttu-id="149d7-2235">Nombre de hello Data Management Gateway tooconnect tooan local servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="149d7-2236">Sí, si va a copiar datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="149d7-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-2237">encryptedCredential</span></span> | <span data-ttu-id="149d7-2238">Servidor de credenciales cifradas tooaccess Hola SFTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="149d7-2239">Generado automáticamente cuando se especifica la autenticación básica (nombre de usuario y contraseña) o SshPublicKey (nombre de usuario + ruta de acceso de clave privada o contenido) en copia asistente o hello ClickOnce cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="149d7-2240">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2240">No.</span></span> <span data-ttu-id="149d7-2241">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="149d7-2242">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="149d7-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="149d7-2243">establecer la autenticación básica toouse, `authenticationType` como `Basic`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:</span><span class="sxs-lookup"><span data-stu-id="149d7-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="149d7-2244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2244">Property</span></span> | <span data-ttu-id="149d7-2245">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2245">Description</span></span> | <span data-ttu-id="149d7-2246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2247">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2247">username</span></span> | <span data-ttu-id="149d7-2248">Usuario que tiene el servidor de acceso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="149d7-2249">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2249">Yes</span></span> |
| <span data-ttu-id="149d7-2250">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2250">password</span></span> | <span data-ttu-id="149d7-2251">Contraseña de usuario de hello (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="149d7-2251">Password for hello user (username).</span></span> | <span data-ttu-id="149d7-2252">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="149d7-2253">Ejemplo: Autenticación básica con credenciales cifradas**</span><span class="sxs-lookup"><span data-stu-id="149d7-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="149d7-2254">Uso de autenticación de clave pública SSH:**</span><span class="sxs-lookup"><span data-stu-id="149d7-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="149d7-2255">establecer la autenticación básica toouse, `authenticationType` como `SshPublicKey`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:</span><span class="sxs-lookup"><span data-stu-id="149d7-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="149d7-2256">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2256">Property</span></span> | <span data-ttu-id="149d7-2257">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2257">Description</span></span> | <span data-ttu-id="149d7-2258">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2259">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2259">username</span></span> |<span data-ttu-id="149d7-2260">Usuario que tiene el servidor de acceso toohello SFTP</span><span class="sxs-lookup"><span data-stu-id="149d7-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="149d7-2261">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2261">Yes</span></span> |
| <span data-ttu-id="149d7-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="149d7-2262">privateKeyPath</span></span> | <span data-ttu-id="149d7-2263">Especifique la ruta de acceso absoluta toohello archivo de clave privada que puede tener acceso esa puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="149d7-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="149d7-2264">Especifique cualquier hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="149d7-2265">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="149d7-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="149d7-2266">privateKeyContent</span></span> | <span data-ttu-id="149d7-2267">Una cadena serializada de contenido de clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="149d7-2268">Hola Asistente para copiar puede leer el archivo de clave privada de Hola y extraer contenido de clave privada de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="149d7-2269">Si está utilizando cualquier otra herramienta/SDK, use en su lugar la propiedad privateKeyPath de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="149d7-2270">Especifique cualquier hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="149d7-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="149d7-2271">passPhrase</span></span> | <span data-ttu-id="149d7-2272">Especificar clave privada de hello paso contraseña/frase toodecrypt Hola si el archivo de clave de hello está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="149d7-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="149d7-2273">Sí, si el archivo de clave privada de hello está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="149d7-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="149d7-2274">Ejemplo: Autenticación de SshPublicKey mediante contenido de clave privada**</span><span class="sxs-lookup"><span data-stu-id="149d7-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="149d7-2275">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-2276">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2276">Dataset</span></span>
<span data-ttu-id="149d7-2277">toodefine un conjunto de datos SFTP, conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2278">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2278">Property</span></span> | <span data-ttu-id="149d7-2279">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2279">Description</span></span> | <span data-ttu-id="149d7-2280">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="149d7-2281">folderPath</span></span> |<span data-ttu-id="149d7-2282">Carpeta de toohello de ruta de acceso de Sub.</span><span class="sxs-lookup"><span data-stu-id="149d7-2282">Sub path toohello folder.</span></span> <span data-ttu-id="149d7-2283">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="149d7-2284">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="149d7-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="149d7-2285">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="149d7-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="149d7-2286">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2286">Yes</span></span> |
| <span data-ttu-id="149d7-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="149d7-2287">fileName</span></span> |<span data-ttu-id="149d7-2288">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="149d7-2289">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="149d7-2290">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato:</span><span class="sxs-lookup"><span data-stu-id="149d7-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="149d7-2291">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="149d7-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="149d7-2292">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2292">No</span></span> |
| <span data-ttu-id="149d7-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="149d7-2293">fileFilter</span></span> |<span data-ttu-id="149d7-2294">Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="149d7-2295">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="149d7-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="149d7-2296">Ejemplos 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="149d7-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="149d7-2297">Ejemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="149d7-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="149d7-2298">fileFilter es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="149d7-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="149d7-2299">Esta propiedad no es compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="149d7-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="149d7-2300">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2300">No</span></span> |
| <span data-ttu-id="149d7-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="149d7-2301">partitionedBy</span></span> |<span data-ttu-id="149d7-2302">partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="149d7-2303">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="149d7-2304">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2304">No</span></span> |
| <span data-ttu-id="149d7-2305">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-2305">format</span></span> | <span data-ttu-id="149d7-2306">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-2307">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="149d7-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="149d7-2308">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="149d7-2309">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="149d7-2310">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2310">No</span></span> |
| <span data-ttu-id="149d7-2311">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-2311">compression</span></span> | <span data-ttu-id="149d7-2312">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-2313">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-2314">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-2315">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-2316">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2316">No</span></span> |
| <span data-ttu-id="149d7-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="149d7-2317">useBinaryTransfer</span></span> |<span data-ttu-id="149d7-2318">Especifica si se usará el modo de transferencia binario.</span><span class="sxs-lookup"><span data-stu-id="149d7-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="149d7-2319">Su valor es true para el modo binario y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="149d7-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="149d7-2320">Valor predeterminado: true.</span><span class="sxs-lookup"><span data-stu-id="149d7-2320">Default value: True.</span></span> <span data-ttu-id="149d7-2321">Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="149d7-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="149d7-2322">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="149d7-2323">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-2324">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="149d7-2325">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="149d7-2326">Origen de Sistema de archivos en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2327">Si va a copiar datos desde un origen SFTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2328">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2328">Property</span></span> | <span data-ttu-id="149d7-2329">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2329">Description</span></span> | <span data-ttu-id="149d7-2330">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2330">Allowed values</span></span> | <span data-ttu-id="149d7-2331">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="149d7-2332">recursive</span></span> |<span data-ttu-id="149d7-2333">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="149d7-2334">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="149d7-2334">True, False (default)</span></span> |<span data-ttu-id="149d7-2335">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="149d7-2336">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2336">Example</span></span>

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

<span data-ttu-id="149d7-2337">Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="149d7-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="149d7-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-2339">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2339">Linked service</span></span>
<span data-ttu-id="149d7-2340">el servicio conjunto Hola vinculado de toodefine un HTTP **tipo** de hello servicio vinculado demasiado**Http**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2341">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2341">Property</span></span> | <span data-ttu-id="149d7-2342">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2342">Description</span></span> | <span data-ttu-id="149d7-2343">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2344">url</span><span class="sxs-lookup"><span data-stu-id="149d7-2344">url</span></span> | <span data-ttu-id="149d7-2345">Basar la dirección URL toohello servidor Web</span><span class="sxs-lookup"><span data-stu-id="149d7-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="149d7-2346">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2346">Yes</span></span> |
| <span data-ttu-id="149d7-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2347">authenticationType</span></span> | <span data-ttu-id="149d7-2348">Especifica el tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="149d7-2349">Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="149d7-2350">Consulte toosections por debajo de esta tabla en más propiedades y ejemplos JSON para esos tipos de autenticación, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="149d7-2351">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2351">Yes</span></span> |
| <span data-ttu-id="149d7-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="149d7-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="149d7-2353">Especifique si el servidor de tooenable SSL la validación de certificados si el origen es el servidor de Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="149d7-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="149d7-2354">No, el valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="149d7-2354">No, default is true</span></span> |
| <span data-ttu-id="149d7-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2355">gatewayName</span></span> | <span data-ttu-id="149d7-2356">Nombre de hello Data Management Gateway tooconnect tooan local de origen HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="149d7-2357">Sí si va a copiar datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="149d7-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-2358">encryptedCredential</span></span> | <span data-ttu-id="149d7-2359">Credenciales cifradas tooaccess Hola extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="149d7-2360">Generado automáticamente al configurar la información de autenticación de hello en copia asistente o hello ClickOnce cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="149d7-2361">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2361">No.</span></span> <span data-ttu-id="149d7-2362">Se aplica solo cuando se copian datos desde un servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="149d7-2363">Ejemplo: Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="149d7-2364">Establecer `authenticationType` como `Basic`, `Digest`, o `Windows`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="149d7-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="149d7-2365">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2365">Property</span></span> | <span data-ttu-id="149d7-2366">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2366">Description</span></span> | <span data-ttu-id="149d7-2367">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2368">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2368">username</span></span> | <span data-ttu-id="149d7-2369">Nombre de usuario tooaccess Hola extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="149d7-2370">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2370">Yes</span></span> |
| <span data-ttu-id="149d7-2371">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2371">password</span></span> | <span data-ttu-id="149d7-2372">Contraseña de usuario de hello (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="149d7-2372">Password for hello user (username).</span></span> | <span data-ttu-id="149d7-2373">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="149d7-2374">Ejemplo: Uso de la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="149d7-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="149d7-2375">establecer la autenticación básica toouse, `authenticationType` como `ClientCertificate`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="149d7-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="149d7-2376">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2376">Property</span></span> | <span data-ttu-id="149d7-2377">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2377">Description</span></span> | <span data-ttu-id="149d7-2378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="149d7-2379">embeddedCertData</span></span> | <span data-ttu-id="149d7-2380">contenido codificado en Base64 Hola de datos binarios del archivo de intercambio de información Personal (PFX) Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="149d7-2381">Especifique cualquier hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="149d7-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="149d7-2382">certThumbprint</span></span> | <span data-ttu-id="149d7-2383">Hola huella digital del certificado de Hola que se instaló en el almacén de certificados de la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="149d7-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="149d7-2384">Se aplica solo cuando se copian datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="149d7-2385">Especifique cualquier hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="149d7-2386">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2386">password</span></span> | <span data-ttu-id="149d7-2387">Contraseña asociada con el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="149d7-2388">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2388">No</span></span> |

<span data-ttu-id="149d7-2389">Si usa `certThumbprint` para hello y autenticación de certificado está instalado en el almacén personal de hello del equipo local de hello, necesita que el servicio de puerta de enlace de toohello de toogrant Hola permiso de lectura:</span><span class="sxs-lookup"><span data-stu-id="149d7-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="149d7-2390">Inicie Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="149d7-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="149d7-2391">Agregar hello **certificados** complemento ese Hola destinos **equipo Local**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="149d7-2392">Expanda **Certificados**, **Personal** y haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="149d7-2393">Haga clic en certificado Hola almacén personal de Hola y seleccione **todas las tareas**->**administrar claves privadas...**</span><span class="sxs-lookup"><span data-stu-id="149d7-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="149d7-2394">En hello **seguridad** ficha, agregue la cuenta de usuario de hello en que se ejecuta el servicio de Host de Data Management Gateway con certificado de toohello de acceso de lectura de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="149d7-2395">**Ejemplo: usar el certificado de cliente:** esto vinculado vínculos de servicio el servidor de web HTTP de datos generador tooan local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="149d7-2396">Utiliza un certificado de cliente que se instala en la máquina de hello con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="149d7-2397">Ejemplo: Uso del certificado de cliente en un archivo</span><span class="sxs-lookup"><span data-stu-id="149d7-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="149d7-2398">Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="149d7-2399">Utiliza un archivo de certificado de cliente en la máquina de hello con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="149d7-2400">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-2401">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2401">Dataset</span></span>
<span data-ttu-id="149d7-2402">conjunto de datos de toodefine un HTTP, conjunto hello **tipo** del conjunto de datos de hello demasiado**Http**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2403">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2403">Property</span></span> | <span data-ttu-id="149d7-2404">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2404">Description</span></span> | <span data-ttu-id="149d7-2405">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="149d7-2406">relativeUrl</span></span> | <span data-ttu-id="149d7-2407">Un recurso de toohello de dirección URL relativo al que contiene los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="149d7-2408">Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="149d7-2409">dirección URL dinámica tooconstruct, puede usar [funciones de factoría de datos y las variables del sistema](data-factory-functions-variables.md), ejemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="149d7-2410">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2410">No</span></span> |
| <span data-ttu-id="149d7-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="149d7-2411">requestMethod</span></span> | <span data-ttu-id="149d7-2412">Método HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2412">Http method.</span></span> <span data-ttu-id="149d7-2413">Los valores permitidos son **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="149d7-2414">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2414">No.</span></span> <span data-ttu-id="149d7-2415">El valor predeterminado es `GET`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="149d7-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="149d7-2416">additionalHeaders</span></span> | <span data-ttu-id="149d7-2417">Encabezados de solicitud HTTP adicionales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="149d7-2418">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2418">No</span></span> |
| <span data-ttu-id="149d7-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="149d7-2419">requestBody</span></span> | <span data-ttu-id="149d7-2420">Cuerpo de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2420">Body for HTTP request.</span></span> | <span data-ttu-id="149d7-2421">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2421">No</span></span> |
| <span data-ttu-id="149d7-2422">formato</span><span class="sxs-lookup"><span data-stu-id="149d7-2422">format</span></span> | <span data-ttu-id="149d7-2423">Si desea que toosimply **recuperar datos de Hola de extremo HTTP como-es** sin analizarlo, omita esta configuración de formato.</span><span class="sxs-lookup"><span data-stu-id="149d7-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="149d7-2424">Si desea tooparse Hola HTTP respuesta contenido durante la copia, se admite los siguientes tipos de formato de Hola: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="149d7-2425">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="149d7-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="149d7-2426">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2426">No</span></span> |
| <span data-ttu-id="149d7-2427">compresión</span><span class="sxs-lookup"><span data-stu-id="149d7-2427">compression</span></span> | <span data-ttu-id="149d7-2428">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="149d7-2429">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="149d7-2430">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="149d7-2431">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="149d7-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="149d7-2432">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="149d7-2433">Ejemplo: usar el método de hello GET (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="149d7-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="149d7-2434">Ejemplo: utilizar el método POST de Hola</span><span class="sxs-lookup"><span data-stu-id="149d7-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="149d7-2435">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="149d7-2436">Origen de HTTP en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2437">Si va a copiar datos desde un origen HTTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**HttpSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2438">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2438">Property</span></span> | <span data-ttu-id="149d7-2439">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2439">Description</span></span> | <span data-ttu-id="149d7-2440">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="149d7-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="149d7-2441">httpRequestTimeout</span></span> | <span data-ttu-id="149d7-2442">Hola (TimeSpan) de tiempo de espera de solicitud tooget una respuesta de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="149d7-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="149d7-2443">Es tooget Hola de tiempo de espera una respuesta, datos de respuesta no Hola el tooread del tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="149d7-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="149d7-2444">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2444">No.</span></span> <span data-ttu-id="149d7-2445">Valor predeterminado: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="149d7-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-2446">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="149d7-2447">Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="149d7-2448">OData</span><span class="sxs-lookup"><span data-stu-id="149d7-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-2449">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2449">Linked service</span></span>
<span data-ttu-id="149d7-2450">toodefine una OData el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OData**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2451">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2451">Property</span></span> | <span data-ttu-id="149d7-2452">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2452">Description</span></span> | <span data-ttu-id="149d7-2453">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2454">url</span><span class="sxs-lookup"><span data-stu-id="149d7-2454">url</span></span> |<span data-ttu-id="149d7-2455">Dirección URL del servicio OData Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2455">Url of hello OData service.</span></span> |<span data-ttu-id="149d7-2456">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2456">Yes</span></span> |
| <span data-ttu-id="149d7-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2457">authenticationType</span></span> |<span data-ttu-id="149d7-2458">Tipo de autenticación usa tooconnect toohello OData origen.</span><span class="sxs-lookup"><span data-stu-id="149d7-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="149d7-2459">Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="149d7-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="149d7-2460">Para OData local, los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="149d7-2461">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2461">Yes</span></span> |
| <span data-ttu-id="149d7-2462">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2462">username</span></span> |<span data-ttu-id="149d7-2463">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="149d7-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="149d7-2464">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="149d7-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="149d7-2465">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2465">password</span></span> |<span data-ttu-id="149d7-2466">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-2467">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="149d7-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="149d7-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="149d7-2468">authorizedCredential</span></span> |<span data-ttu-id="149d7-2469">Si usa OAuth, haga clic en **Authorize** botón en hello Asistente para copiar de factoría de datos o el Editor y escriba sus credenciales, valor de Hola de esta propiedad será generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="149d7-2470">Sí (solo si usa la autenticación OAuth)</span><span class="sxs-lookup"><span data-stu-id="149d7-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="149d7-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2471">gatewayName</span></span> |<span data-ttu-id="149d7-2472">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el servicio de OData de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="149d7-2473">Especifique solo si va a copiar datos del origen de OData local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="149d7-2474">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="149d7-2475">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="149d7-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="149d7-2476">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="149d7-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="149d7-2477">Ejemplo: Uso de la autenticación de Windows para acceder al origen de OData local</span><span class="sxs-lookup"><span data-stu-id="149d7-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="149d7-2478">Ejemplo: Uso de la autenticación OAuth para tener acceso al origen de OData en la nube</span><span class="sxs-lookup"><span data-stu-id="149d7-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="149d7-2479">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="149d7-2480">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2480">Dataset</span></span>
<span data-ttu-id="149d7-2481">toodefine un conjunto de datos OData, conjunto hello **tipo** del conjunto de datos de hello demasiado**ODataResource**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2482">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2482">Property</span></span> | <span data-ttu-id="149d7-2483">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2483">Description</span></span> | <span data-ttu-id="149d7-2484">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2485">path</span><span class="sxs-lookup"><span data-stu-id="149d7-2485">path</span></span> |<span data-ttu-id="149d7-2486">Ruta de acceso toohello recurso de OData</span><span class="sxs-lookup"><span data-stu-id="149d7-2486">Path toohello OData resource</span></span> |<span data-ttu-id="149d7-2487">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2488">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2488">Example</span></span>

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

<span data-ttu-id="149d7-2489">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-2490">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2491">Si va a copiar datos desde un origen OData, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2492">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2492">Property</span></span> | <span data-ttu-id="149d7-2493">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2493">Description</span></span> | <span data-ttu-id="149d7-2494">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2494">Example</span></span> | <span data-ttu-id="149d7-2495">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2496">query</span><span class="sxs-lookup"><span data-stu-id="149d7-2496">query</span></span> |<span data-ttu-id="149d7-2497">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="149d7-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="149d7-2499">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2500">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2500">Example</span></span>

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

<span data-ttu-id="149d7-2501">Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="149d7-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="149d7-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-2503">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2503">Linked service</span></span>
<span data-ttu-id="149d7-2504">toodefine un ODBC el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesOdbc**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2505">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2505">Property</span></span> | <span data-ttu-id="149d7-2506">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2506">Description</span></span> | <span data-ttu-id="149d7-2507">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-2508">connectionString</span></span> |<span data-ttu-id="149d7-2509">parte de credencial de acceso no Hola de cadena de conexión de Hola y opcional cifra credenciales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="149d7-2510">Vea los ejemplos de hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="149d7-2511">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2511">Yes</span></span> |
| <span data-ttu-id="149d7-2512">credential</span><span class="sxs-lookup"><span data-stu-id="149d7-2512">credential</span></span> |<span data-ttu-id="149d7-2513">Hola credencial parte de acceso a cadena de conexión de hello especificada en formato de valores de propiedad específicos del controlador.</span><span class="sxs-lookup"><span data-stu-id="149d7-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="149d7-2514">Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="149d7-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="149d7-2515">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2515">No</span></span> |
| <span data-ttu-id="149d7-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2516">authenticationType</span></span> |<span data-ttu-id="149d7-2517">Tipo de autenticación que utiliza el almacén de datos ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="149d7-2518">Los valores posibles son: Anonymous y Basic.</span><span class="sxs-lookup"><span data-stu-id="149d7-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="149d7-2519">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2519">Yes</span></span> |
| <span data-ttu-id="149d7-2520">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2520">username</span></span> |<span data-ttu-id="149d7-2521">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="149d7-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="149d7-2522">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2522">No</span></span> |
| <span data-ttu-id="149d7-2523">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2523">password</span></span> |<span data-ttu-id="149d7-2524">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-2525">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2525">No</span></span> |
| <span data-ttu-id="149d7-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2526">gatewayName</span></span> |<span data-ttu-id="149d7-2527">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el almacén de datos ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="149d7-2528">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="149d7-2529">Ejemplo: Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="149d7-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="149d7-2530">Ejemplo: Uso de la autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="149d7-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="149d7-2531">Puede cifrar las credenciales de hello con hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versión de PowerShell de Azure) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versión o una anterior de hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="149d7-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="149d7-2532">Ejemplo: Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="149d7-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="149d7-2533">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-2534">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2534">Dataset</span></span>
<span data-ttu-id="149d7-2535">toodefine un conjunto de datos ODBC, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2536">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2536">Property</span></span> | <span data-ttu-id="149d7-2537">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2537">Description</span></span> | <span data-ttu-id="149d7-2538">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-2539">tableName</span></span> |<span data-ttu-id="149d7-2540">Nombre de tabla de hello en el almacén de datos ODBC Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="149d7-2541">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="149d7-2542">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2542">Example</span></span>

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

<span data-ttu-id="149d7-2543">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-2544">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2545">Si va a copiar datos desde un almacén de datos ODBC, establecer hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2546">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2546">Property</span></span> | <span data-ttu-id="149d7-2547">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2547">Description</span></span> | <span data-ttu-id="149d7-2548">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2548">Allowed values</span></span> | <span data-ttu-id="149d7-2549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2550">query</span><span class="sxs-lookup"><span data-stu-id="149d7-2550">query</span></span> |<span data-ttu-id="149d7-2551">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-2552">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-2552">SQL query string.</span></span> <span data-ttu-id="149d7-2553">Por ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="149d7-2554">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2555">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2555">Example</span></span>

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

<span data-ttu-id="149d7-2556">Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="149d7-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="149d7-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="149d7-2558">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2558">Linked service</span></span>
<span data-ttu-id="149d7-2559">toodefine un Salesforce el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Salesforce**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2560">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2560">Property</span></span> | <span data-ttu-id="149d7-2561">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2561">Description</span></span> | <span data-ttu-id="149d7-2562">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="149d7-2563">environmentUrl</span></span> | <span data-ttu-id="149d7-2564">Especifique la instancia de la dirección URL de Salesforce de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="149d7-2565">- La dirección predeterminada es "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="149d7-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="149d7-2566">-toocopy datos de espacio aislado, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="149d7-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="149d7-2567">-toocopy datos de dominio personalizado, especifique, por ejemplo, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="149d7-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="149d7-2568">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2568">No</span></span> |
| <span data-ttu-id="149d7-2569">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2569">username</span></span> |<span data-ttu-id="149d7-2570">Especifique un nombre de usuario de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="149d7-2571">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2571">Yes</span></span> |
| <span data-ttu-id="149d7-2572">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2572">password</span></span> |<span data-ttu-id="149d7-2573">Especifique una contraseña para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="149d7-2574">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2574">Yes</span></span> |
| <span data-ttu-id="149d7-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="149d7-2575">securityToken</span></span> |<span data-ttu-id="149d7-2576">Especifique un token de seguridad para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="149d7-2577">Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/obtener un token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="149d7-2578">en general, vea toolearn acerca de los tokens de seguridad [API hello y seguridad](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="149d7-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="149d7-2579">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2580">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2580">Example</span></span>

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

<span data-ttu-id="149d7-2581">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-2582">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2582">Dataset</span></span>
<span data-ttu-id="149d7-2583">toodefine un conjunto de datos de Salesforce, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2584">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2584">Property</span></span> | <span data-ttu-id="149d7-2585">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2585">Description</span></span> | <span data-ttu-id="149d7-2586">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="149d7-2587">tableName</span></span> |<span data-ttu-id="149d7-2588">Nombre de tabla de hello en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="149d7-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="149d7-2589">No (si se especifica una **consulta** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="149d7-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2590">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2590">Example</span></span>

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

<span data-ttu-id="149d7-2591">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="149d7-2592">Origen relacional en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2593">Si va a copiar datos de Salesforce, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="149d7-2594">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2594">Property</span></span> | <span data-ttu-id="149d7-2595">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2595">Description</span></span> | <span data-ttu-id="149d7-2596">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="149d7-2596">Allowed values</span></span> | <span data-ttu-id="149d7-2597">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="149d7-2598">query</span><span class="sxs-lookup"><span data-stu-id="149d7-2598">query</span></span> |<span data-ttu-id="149d7-2599">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="149d7-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="149d7-2600">Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="149d7-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="149d7-2601">Por ejemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="149d7-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="149d7-2602">No (si hello **tableName** de hello **conjunto de datos** se especifica)</span><span class="sxs-lookup"><span data-stu-id="149d7-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2603">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="149d7-2604">parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="149d7-2605">Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="149d7-2606">Datos web</span><span class="sxs-lookup"><span data-stu-id="149d7-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2607">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2607">Linked service</span></span>
<span data-ttu-id="149d7-2608">el servicio conjunto Hola vinculado de toodefine un sitio Web **tipo** de hello servicio vinculado demasiado**Web**y especificar después de propiedades en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2609">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2609">Property</span></span> | <span data-ttu-id="149d7-2610">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2610">Description</span></span> | <span data-ttu-id="149d7-2611">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2612">URL</span><span class="sxs-lookup"><span data-stu-id="149d7-2612">Url</span></span> |<span data-ttu-id="149d7-2613">Origen de dirección URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="149d7-2613">URL toohello Web source</span></span> |<span data-ttu-id="149d7-2614">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2614">Yes</span></span> |
| <span data-ttu-id="149d7-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="149d7-2615">authenticationType</span></span> |<span data-ttu-id="149d7-2616">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="149d7-2616">Anonymous.</span></span> |<span data-ttu-id="149d7-2617">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="149d7-2618">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2618">Example</span></span>


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

<span data-ttu-id="149d7-2619">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="149d7-2620">Dataset</span><span class="sxs-lookup"><span data-stu-id="149d7-2620">Dataset</span></span>
<span data-ttu-id="149d7-2621">toodefine un conjunto de datos Web, conjunto hello **tipo** del conjunto de datos de hello demasiado**WebTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="149d7-2622">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2622">Property</span></span> | <span data-ttu-id="149d7-2623">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2623">Description</span></span> | <span data-ttu-id="149d7-2624">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-2625">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2625">type</span></span> |<span data-ttu-id="149d7-2626">Tipo de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2626">type of hello dataset.</span></span> <span data-ttu-id="149d7-2627">debe establecerse demasiado**WebTable**</span><span class="sxs-lookup"><span data-stu-id="149d7-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="149d7-2628">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2628">Yes</span></span> |
| <span data-ttu-id="149d7-2629">path</span><span class="sxs-lookup"><span data-stu-id="149d7-2629">path</span></span> |<span data-ttu-id="149d7-2630">Un recurso de toohello de dirección URL relativo al que contiene la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="149d7-2631">No.</span><span class="sxs-lookup"><span data-stu-id="149d7-2631">No.</span></span> <span data-ttu-id="149d7-2632">Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="149d7-2633">index</span><span class="sxs-lookup"><span data-stu-id="149d7-2633">index</span></span> |<span data-ttu-id="149d7-2634">índice de Hola de tabla de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="149d7-2635">Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="149d7-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="149d7-2636">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="149d7-2637">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2637">Example</span></span>

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

<span data-ttu-id="149d7-2638">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="149d7-2639">Origen de Web en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="149d7-2640">Si va a copiar datos de una tabla de web, establezca hello **tipo de origen de** de hello actividad de copia demasiado**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="149d7-2641">Actualmente, al origen de hello en la actividad de copia es de tipo **WebSource**, no se admiten propiedades adicionales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="149d7-2642">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="149d7-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="149d7-2643">Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="149d7-2644">ENTORNOS DE PROCESO</span><span class="sxs-lookup"><span data-stu-id="149d7-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="149d7-2645">Hello tabla siguiente enumeran los entornos de proceso Hola compatibles con actividades de transformación de hello y factoría de datos que se pueden ejecutar en ellos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="149d7-2646">Haga clic en el vínculo de hello para el proceso de hello está interesado en esquemas JSON de hello toosee para toolink de servicio vinculado tooa factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="149d7-2647">Entorno de procesos</span><span class="sxs-lookup"><span data-stu-id="149d7-2647">Compute environment</span></span> | <span data-ttu-id="149d7-2648">Actividades</span><span class="sxs-lookup"><span data-stu-id="149d7-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="149d7-2649">[Clúster de HDInsight a petición](#on-demand-azure-hdinsight-cluster) o [clúster HDInsight propio](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="149d7-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="149d7-2650">[Actividad personalizada de .NET](#net-custom-activity), [actividad de Hive](#hdinsight-hive-activity), [actividad de Pig](#hdinsight-pig-activity, [actividad de MapReduce](#hdinsight-mapreduce-activity), [actividad de streaming de Hadoop](#hdinsight-streaming-activityd) y [actividad de Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="149d7-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="149d7-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="149d7-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="149d7-2652">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="149d7-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="149d7-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="149d7-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="149d7-2654">[Actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="149d7-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="149d7-2655">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="149d7-2656">U-SQL de análisis con Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="149d7-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1) y [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="149d7-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="149d7-2658">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="149d7-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="149d7-2659">Clúster de Azure HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="149d7-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="149d7-2660">Hola servicio Data Factory de Azure puede crear automáticamente un basadas en Windows/Linux a petición HDInsight tooprocess datos del clúster.</span><span class="sxs-lookup"><span data-stu-id="149d7-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="149d7-2661">clúster Hola se crea en la misma región que la cuenta de almacenamiento de hello (propiedad linkedServiceName en hello JSON) asociada a clúster Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="149d7-2662">Puede ejecutar Hola seguir las actividades de transformación de este servicio vinculado: [actividad personalizada .NET](#net-custom-activity), [Hive actividad](#hdinsight-hive-activity), [actividad de Pig] (#-pig-actividad de hdinsight, [actividad MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming actividad](#hdinsight-streaming-activityd), [inspirará actividad](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="149d7-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2663">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2663">Linked service</span></span> 
<span data-ttu-id="149d7-2664">Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio de vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="149d7-2665">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2665">Property</span></span> | <span data-ttu-id="149d7-2666">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2666">Description</span></span> | <span data-ttu-id="149d7-2667">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2668">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2668">type</span></span> |<span data-ttu-id="149d7-2669">se debe establecer propiedad de tipo Hello demasiado**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="149d7-2670">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2670">Yes</span></span> |
| <span data-ttu-id="149d7-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="149d7-2671">clusterSize</span></span> |<span data-ttu-id="149d7-2672">Número de nodos de trabajador/datos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="149d7-2673">clúster de HDInsight de Hola se crea con 2 nodos principales junto con el número de Hola de nodos de trabajador que especifique para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="149d7-2674">nodos de Hello son de tamaño Standard_D3 que tiene 4 núcleos, por lo que un clúster de nodo de 4 trabajo tiene 24 núcleos (4\*para nodos de trabajador, además de 2 núcleos, 4 = 16\*4 = 8 núcleos para nodos principales).</span><span class="sxs-lookup"><span data-stu-id="149d7-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="149d7-2675">Vea [Hadoop basado en Linux crear clústeres de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obtener más información acerca del nivel de hello Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="149d7-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="149d7-2676">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2676">Yes</span></span> |
| <span data-ttu-id="149d7-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="149d7-2677">timetolive</span></span> |<span data-ttu-id="149d7-2678">Hola permitido de tiempo de inactividad para el clúster de HDInsight a petición Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="149d7-2679">Especifica cuánto tiempo permanece activo clúster de HDInsight a petición Hola tras la finalización de una actividad que se ejecutan si no hay otros trabajos activos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="149d7-2680">Por ejemplo, si la ejecución de una actividad tiene 6 minutos y timetolive es establecer too5 minutos, Hola clúster permanece activo durante 5 minutos después de hello 6 minutos de procesamiento de ejecución de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="149d7-2681">Si se ejecuta otra actividad que se ejecute con la ventana de 6 minutos hello, que se procesa por hello mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="149d7-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="149d7-2682">Creación de un clúster de HDInsight a petición es una operación costosa (podría tardar un poco), por lo que use esta opción como sea necesario tooimprove de rendimiento de una factoría de datos mediante la reutilización de un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="149d7-2683">Si establece too0 de valor timetolive, clúster Hola se elimina en cuanto ejecuta actividad hello procesados.</span><span class="sxs-lookup"><span data-stu-id="149d7-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="149d7-2684">En hello otra parte, si establece un valor alto, clúster de hello puede permanecer inactivo innecesariamente resultante en altos costos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="149d7-2685">Por lo tanto, es importante que establezca el valor adecuado de hello según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="149d7-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="149d7-2686">Pueden compartir varias canalizaciones Hola la misma instancia de clúster de HDInsight a petición de hello si el valor de la propiedad timetolive Hola está configurado correctamente</span><span class="sxs-lookup"><span data-stu-id="149d7-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="149d7-2687">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2687">Yes</span></span> |
| <span data-ttu-id="149d7-2688">versión</span><span class="sxs-lookup"><span data-stu-id="149d7-2688">version</span></span> |<span data-ttu-id="149d7-2689">Versión Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149d7-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="149d7-2690">Para obtener más información, consulte [Versiones admitidas de HDInsight en Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="149d7-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="149d7-2691">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2691">No</span></span> |
| <span data-ttu-id="149d7-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="149d7-2692">linkedServiceName</span></span> |<span data-ttu-id="149d7-2693">Almacenamiento de Azure vinculada toobe servicio utilizado por clúster de petición de Hola para almacenar y procesar datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="149d7-2694">Actualmente, no se puede crear un clúster de HDInsight a petición que utiliza un almacén de Azure Data Lake como almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="149d7-2695">Si desea que los datos del resultado de hello toostore de HDInsight de procesamiento en un almacén de Data Lake de Azure, use una actividad de copia toocopy Hola de datos de almacenamiento de blobs de Azure de hello toohello almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="149d7-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="149d7-2696">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2696">Yes</span></span> |
| <span data-ttu-id="149d7-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="149d7-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="149d7-2698">Especifica las cuentas de almacenamiento adicional para hello HDInsight el servicio vinculado para que el servicio de factoría de datos de hello puede registrar en su nombre.</span><span class="sxs-lookup"><span data-stu-id="149d7-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="149d7-2699">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2699">No</span></span> |
| <span data-ttu-id="149d7-2700">osType</span><span class="sxs-lookup"><span data-stu-id="149d7-2700">osType</span></span> |<span data-ttu-id="149d7-2701">Tipo de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="149d7-2701">Type of operating system.</span></span> <span data-ttu-id="149d7-2702">Los valores permitidos son: Windows (predeterminado) y Linux</span><span class="sxs-lookup"><span data-stu-id="149d7-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="149d7-2703">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2703">No</span></span> |
| <span data-ttu-id="149d7-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="149d7-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="149d7-2705">nombre de Hola de SQL Azure vinculado esa base de datos de HCatalog toohello de punto de servicio.</span><span class="sxs-lookup"><span data-stu-id="149d7-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="149d7-2706">clúster de HDInsight a petición Hola se crea mediante el uso de base de datos de SQL Azure hello como Hola tienda de metadatos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="149d7-2707">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="149d7-2708">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2708">JSON example</span></span>
<span data-ttu-id="149d7-2709">Hola después de JSON define un servicio de vinculado de HDInsight a petición basadas en Linux.</span><span class="sxs-lookup"><span data-stu-id="149d7-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="149d7-2710">Hola servicio factoría de datos crea automáticamente un **basados en Linux** clúster de HDInsight al procesar un segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="149d7-2711">Para más información, vea [Servicios vinculados de procesos](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="149d7-2712">Clúster de Azure HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="149d7-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="149d7-2713">Puede crear su propio clúster de HDInsight de un tooregister de servicio vinculado de HDInsight de Azure con factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="149d7-2714">Puede ejecutar Hola siguiendo las actividades de transformación de datos en este servicio vinculado: [actividad personalizada .NET](#net-custom-activity), [Hive actividad](#hdinsight-hive-activity), [actividad de Pig] (#-pig-actividad de hdinsight, [MapReduce actividad](#hdinsight-mapreduce-activity), [Hadoop streaming actividad](#hdinsight-streaming-activityd), [inspirará actividad](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="149d7-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2715">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2715">Linked service</span></span>
<span data-ttu-id="149d7-2716">Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="149d7-2717">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2717">Property</span></span> | <span data-ttu-id="149d7-2718">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2718">Description</span></span> | <span data-ttu-id="149d7-2719">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2720">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2720">type</span></span> |<span data-ttu-id="149d7-2721">se debe establecer propiedad de tipo Hello demasiado**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="149d7-2722">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2722">Yes</span></span> |
| <span data-ttu-id="149d7-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="149d7-2723">clusterUri</span></span> |<span data-ttu-id="149d7-2724">Hola URI Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149d7-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="149d7-2725">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2725">Yes</span></span> |
| <span data-ttu-id="149d7-2726">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2726">username</span></span> |<span data-ttu-id="149d7-2727">Especificar nombre de Hola de hello usuario toobe usa clúster de HDInsight de tooconnect tooan existente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="149d7-2728">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2728">Yes</span></span> |
| <span data-ttu-id="149d7-2729">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2729">password</span></span> |<span data-ttu-id="149d7-2730">Especifique la contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="149d7-2731">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2731">Yes</span></span> |
| <span data-ttu-id="149d7-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="149d7-2732">linkedServiceName</span></span> | <span data-ttu-id="149d7-2733">Nombre del servicio vinculado de almacenamiento de Azure que hace referencia el almacenamiento de blobs de Azure toohello hello usa Hola clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149d7-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="149d7-2734">Actualmente, no se puede especificar un servicio vinculado de Azure Data Lake Store para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="149d7-2735">Puede tener acceso a datos en el almacén de Azure Data Lake Hola desde scripts de Pig/Hive si el clúster de HDInsight de hello tiene acceso toohello almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="149d7-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="149d7-2736">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2736">Yes</span></span> |

<span data-ttu-id="149d7-2737">Para conocer las versiones de los clústeres de HDInsight admitidas, consulte [Versiones compatibles con HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="149d7-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="149d7-2738">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="149d7-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="149d7-2739">Azure Batch</span></span>
<span data-ttu-id="149d7-2740">Puede crear un grupo de procesos de máquinas virtuales (VM) de un tooregister de servicio vinculado Azure Batch con una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="149d7-2741">Puede ejecutar actividades personalizadas .NET con Lote de Azure o HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="149d7-2742">Puede ejecutar una [actividad personalizada de .NET](#net-custom-activity) en este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2743">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2743">Linked service</span></span>
<span data-ttu-id="149d7-2744">Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="149d7-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="149d7-2745">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2745">Property</span></span> | <span data-ttu-id="149d7-2746">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2746">Description</span></span> | <span data-ttu-id="149d7-2747">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2748">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2748">type</span></span> |<span data-ttu-id="149d7-2749">se debe establecer propiedad de tipo Hello demasiado**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="149d7-2750">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2750">Yes</span></span> |
| <span data-ttu-id="149d7-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="149d7-2751">accountName</span></span> |<span data-ttu-id="149d7-2752">Nombre de cuenta de Azure Batch Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="149d7-2753">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2753">Yes</span></span> |
| <span data-ttu-id="149d7-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="149d7-2754">accessKey</span></span> |<span data-ttu-id="149d7-2755">Clave de acceso de hello cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="149d7-2756">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2756">Yes</span></span> |
| <span data-ttu-id="149d7-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="149d7-2757">poolName</span></span> |<span data-ttu-id="149d7-2758">Nombre del grupo de Hola de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="149d7-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="149d7-2759">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2759">Yes</span></span> |
| <span data-ttu-id="149d7-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="149d7-2760">linkedServiceName</span></span> |<span data-ttu-id="149d7-2761">Nombre del servicio vinculado de almacenamiento de Azure asociado a este servicio vinculado Azure Batch Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="149d7-2762">Este servicio vinculado se usa para archivos de almacenamiento provisional actividad de hello toorun y almacenar los registros de ejecución de actividad de hello necesarios.</span><span class="sxs-lookup"><span data-stu-id="149d7-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="149d7-2763">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="149d7-2764">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="149d7-2765">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-2765">Azure Machine Learning</span></span>
<span data-ttu-id="149d7-2766">Crear un tooregister de servicio vinculado de aprendizaje de automático de Azure de un lote de aprendizaje automático, la puntuación del punto de conexión con una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="149d7-2767">Se pueden ejecutar dos actividades de transformación de datos en este servicio vinculado: [actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="149d7-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2768">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2768">Linked service</span></span>
<span data-ttu-id="149d7-2769">Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado de aprendizaje de automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="149d7-2770">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2770">Property</span></span> | <span data-ttu-id="149d7-2771">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2771">Description</span></span> | <span data-ttu-id="149d7-2772">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2773">Tipo</span><span class="sxs-lookup"><span data-stu-id="149d7-2773">Type</span></span> |<span data-ttu-id="149d7-2774">propiedad de tipo Hello debe establecerse en: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="149d7-2775">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2775">Yes</span></span> |
| <span data-ttu-id="149d7-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="149d7-2776">mlEndpoint</span></span> |<span data-ttu-id="149d7-2777">dirección URL de puntuación de lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="149d7-2778">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2778">Yes</span></span> |
| <span data-ttu-id="149d7-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="149d7-2779">apiKey</span></span> |<span data-ttu-id="149d7-2780">Hola publica API del modelo de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="149d7-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="149d7-2781">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="149d7-2782">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="149d7-2783">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="149d7-2784">Crear un **análisis de Azure Data Lake** vinculado servicio toolink un generador de datos de Azure de tooan de servicio de análisis de Azure Data Lake proceso antes de usar hello [actividad de Data Lake Analytics U-SQL](data-factory-usql-activity.md) en una canalización .</span><span class="sxs-lookup"><span data-stu-id="149d7-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="149d7-2785">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2785">Linked service</span></span>

<span data-ttu-id="149d7-2786">Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de JSON de Hola de un servicio de análisis de Azure Data Lake vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="149d7-2787">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2787">Property</span></span> | <span data-ttu-id="149d7-2788">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2788">Description</span></span> | <span data-ttu-id="149d7-2789">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="149d7-2790">Type</span></span> |<span data-ttu-id="149d7-2791">propiedad de tipo Hello debe establecerse en: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="149d7-2792">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2792">Yes</span></span> |
| <span data-ttu-id="149d7-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="149d7-2793">accountName</span></span> |<span data-ttu-id="149d7-2794">Nombre de la cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="149d7-2795">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2795">Yes</span></span> |
| <span data-ttu-id="149d7-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="149d7-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="149d7-2797">Identificador URI de Análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="149d7-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="149d7-2798">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2798">No</span></span> |
| <span data-ttu-id="149d7-2799">authorization</span><span class="sxs-lookup"><span data-stu-id="149d7-2799">authorization</span></span> |<span data-ttu-id="149d7-2800">Código de autorización se recupera automáticamente después de hacer clic **Authorize** botón en hello Editor de generador de datos y el inicio de sesión de completando hello OAuth.</span><span class="sxs-lookup"><span data-stu-id="149d7-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="149d7-2801">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2801">Yes</span></span> |
| <span data-ttu-id="149d7-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="149d7-2802">subscriptionId</span></span> |<span data-ttu-id="149d7-2803">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-2803">Azure subscription id</span></span> |<span data-ttu-id="149d7-2804">No (si no se especifica, suscripción de Hola se usa la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="149d7-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="149d7-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="149d7-2805">resourceGroupName</span></span> |<span data-ttu-id="149d7-2806">Nombre del grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2806">Azure resource group name</span></span> |<span data-ttu-id="149d7-2807">No (si no se especifica, el grupo de recursos de Hola se usa la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="149d7-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="149d7-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="149d7-2808">sessionId</span></span> |<span data-ttu-id="149d7-2809">Id. de sesión de sesión de autorización de OAuth de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="149d7-2810">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="149d7-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="149d7-2811">Cuando usas Hola Editor de generador de datos, este identificador es generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="149d7-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="149d7-2812">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="149d7-2813">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2813">JSON example</span></span>
<span data-ttu-id="149d7-2814">Hola de ejemplo siguiente proporciona la definición de JSON para un servicio de análisis de Azure Data Lake vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="149d7-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="149d7-2815">Azure SQL Database</span></span>
<span data-ttu-id="149d7-2816">Crear un servicio vinculado de SQL Azure y usarlo con hello [actividad de procedimiento almacenado](#stored-procedure-activity) tooinvoke un procedimiento almacenado desde una canalización del generador de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2817">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2817">Linked service</span></span>
<span data-ttu-id="149d7-2818">toodefine una base de datos de SQL Azure vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**AzureSqlDatabase**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2819">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2819">Property</span></span> | <span data-ttu-id="149d7-2820">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2820">Description</span></span> | <span data-ttu-id="149d7-2821">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-2822">connectionString</span></span> |<span data-ttu-id="149d7-2823">Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="149d7-2824">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="149d7-2825">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2825">JSON example</span></span>

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

<span data-ttu-id="149d7-2826">Vea el artículo [Conector SQL de Azure](data-factory-azure-sql-connector.md#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="149d7-2827">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="149d7-2828">Crear un servicio de almacenamiento de datos de SQL Azure vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2829">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2829">Linked service</span></span>
<span data-ttu-id="149d7-2830">toodefine un almacenamiento de datos de SQL Azure vinculado servicio, conjunto de hello **tipo** de hello servicio vinculado demasiado**AzureSqlDW**y especificar después de propiedades en hello **typeProperties**sección:</span><span class="sxs-lookup"><span data-stu-id="149d7-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="149d7-2831">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2831">Property</span></span> | <span data-ttu-id="149d7-2832">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2832">Description</span></span> | <span data-ttu-id="149d7-2833">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-2834">connectionString</span></span> |<span data-ttu-id="149d7-2835">Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="149d7-2836">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="149d7-2837">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2837">JSON example</span></span>

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

<span data-ttu-id="149d7-2838">Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="149d7-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="149d7-2839">SQL Server</span></span> 
<span data-ttu-id="149d7-2840">Crear un servicio de SQL Server vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="149d7-2841">Servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="149d7-2841">Linked service</span></span>
<span data-ttu-id="149d7-2842">Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="149d7-2843">Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="149d7-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="149d7-2844">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="149d7-2845">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2845">Property</span></span> | <span data-ttu-id="149d7-2846">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2846">Description</span></span> | <span data-ttu-id="149d7-2847">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2848">type</span><span class="sxs-lookup"><span data-stu-id="149d7-2848">type</span></span> |<span data-ttu-id="149d7-2849">propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="149d7-2850">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2850">Yes</span></span> |
| <span data-ttu-id="149d7-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="149d7-2851">connectionString</span></span> |<span data-ttu-id="149d7-2852">Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="149d7-2853">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2853">Yes</span></span> |
| <span data-ttu-id="149d7-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="149d7-2854">gatewayName</span></span> |<span data-ttu-id="149d7-2855">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="149d7-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="149d7-2856">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2856">Yes</span></span> |
| <span data-ttu-id="149d7-2857">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="149d7-2857">username</span></span> |<span data-ttu-id="149d7-2858">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="149d7-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="149d7-2859">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="149d7-2860">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2860">No</span></span> |
| <span data-ttu-id="149d7-2861">Contraseña</span><span class="sxs-lookup"><span data-stu-id="149d7-2861">password</span></span> |<span data-ttu-id="149d7-2862">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="149d7-2863">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2863">No</span></span> |

<span data-ttu-id="149d7-2864">Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):</span><span class="sxs-lookup"><span data-stu-id="149d7-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="149d7-2865">Ejemplo: JSON para usar autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="149d7-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="149d7-2866">Ejemplo: JSON para usar autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="149d7-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="149d7-2867">Si se especifiquen el nombre de usuario y contraseña, puerta de enlace usa hello tooimpersonate base de datos de usuario especificado cuenta tooconnect toohello local SQL Server.</span><span class="sxs-lookup"><span data-stu-id="149d7-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="149d7-2868">En caso contrario, la puerta de enlace conecta toohello SQL Server directamente con el contexto de seguridad de Hola de puerta de enlace (su cuenta de inicio).</span><span class="sxs-lookup"><span data-stu-id="149d7-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="149d7-2869">Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="149d7-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="149d7-2870">ACTIVIDADES DE TRANSFORMACIÓN DE DATOS</span><span class="sxs-lookup"><span data-stu-id="149d7-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="149d7-2871">Actividad</span><span class="sxs-lookup"><span data-stu-id="149d7-2871">Activity</span></span> | <span data-ttu-id="149d7-2872">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="149d7-2873">Actividad de Hive de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="149d7-2874">Hola actividad de HDInsight Hive en una canalización de factoría de datos ejecuta consultas de Hive por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="149d7-2875">Actividad de Pig de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="149d7-2876">Hola actividad de HDInsight Pig en una canalización de factoría de datos ejecuta consultas de Pig por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="149d7-2877">Actividad de MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="149d7-2878">Hola actividad de HDInsight MapReduce en una canalización de factoría de datos ejecuta programas de MapReduce por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="149d7-2879">Actividad de streaming de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="149d7-2880">Hola actividad de transmisión por secuencias de HDInsight en una canalización de factoría de datos ejecuta programas de Streaming de Hadoop por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.</span><span class="sxs-lookup"><span data-stu-id="149d7-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="149d7-2881">Actividad de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="149d7-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="149d7-2882">Hola actividad de HDInsight Spark en una canalización de factoría de datos ejecuta programas de Spark en su propio clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149d7-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="149d7-2883">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="149d7-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="149d7-2884">Azure factoría de datos permite tooeasily crear canalizaciones que usan un aprendizaje automático de Azure publicada web service para realizar análisis predictivos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="149d7-2885">Hola la actividad de ejecución por lotes en una canalización de factoría de datos de Azure se pueden invocar un predicciones de toomake de servicio de web de aprendizaje automático en los datos de hello en lote.</span><span class="sxs-lookup"><span data-stu-id="149d7-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="149d7-2886">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="149d7-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="149d7-2887">Con el tiempo, los modelos de predicción de Hola Hola aprendizaje automático de experimentos puntuación necesitan toobe volver a entrenar con nueva entrada de conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="149d7-2888">Cuando termine con reciclaje, desea hello tooupdate la puntuación del servicio web con hello volver a entrenar el modelo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="149d7-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="149d7-2889">Puede usar servicio web de actualización de recursos de actividad tooupdate Hola Hola con hello recién entrenado modelo.</span><span class="sxs-lookup"><span data-stu-id="149d7-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="149d7-2890">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="149d7-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="149d7-2891">Puede usar la actividad de procedimiento almacenado de hello en un tooinvoke de canalización de factoría de datos en un procedimiento almacenado en uno de hello siguientes almacenes de datos: SQL de Azure, almacenamiento de datos de SQL Azure, base de datos de SQL Server en su empresa o una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="149d7-2892">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="149d7-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="149d7-2893">La actividad de U-SQL de Data Lake Analytics ejecuta un script de U-SQL en un clúster de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="149d7-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="149d7-2894">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="149d7-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="149d7-2895">Si necesita datos de tootransform de forma que no es compatible con la factoría de datos, puede crear una actividad personalizada con su propia lógica de procesamiento de datos y usar actividad hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="149d7-2896">Puede configurar Hola personalizada .NET actividad toorun mediante un servicio Azure Batch o un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="149d7-2897">Actividad de Hive de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="149d7-2898">Puede especificar Hola propiedades en una definición de JSON de actividad de Hive siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="149d7-2899">debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="149d7-2900">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-2901">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightHive de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="149d7-2902">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2902">Property</span></span> | <span data-ttu-id="149d7-2903">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2903">Description</span></span> | <span data-ttu-id="149d7-2904">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2905">script</span><span class="sxs-lookup"><span data-stu-id="149d7-2905">script</span></span> |<span data-ttu-id="149d7-2906">Especifique el script de Hive de hello en línea</span><span class="sxs-lookup"><span data-stu-id="149d7-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="149d7-2907">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2907">No</span></span> |
| <span data-ttu-id="149d7-2908">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="149d7-2908">script path</span></span> |<span data-ttu-id="149d7-2909">Hola de almacén en el almacenamiento de blobs de Azure de script de Hive y proporcionar Hola ruta toohello al archivo.</span><span class="sxs-lookup"><span data-stu-id="149d7-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="149d7-2910">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="149d7-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="149d7-2911">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="149d7-2911">Both cannot be used together.</span></span> <span data-ttu-id="149d7-2912">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="149d7-2913">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2913">No</span></span> |
| <span data-ttu-id="149d7-2914">define los campos</span><span class="sxs-lookup"><span data-stu-id="149d7-2914">defines</span></span> |<span data-ttu-id="149d7-2915">Especificar parámetros como pares clave/valor para hacer referencia a dentro de script de Hive hello mediante 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="149d7-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="149d7-2916">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2916">No</span></span> |

<span data-ttu-id="149d7-2917">Estas propiedades de tipo son toohello específico de actividad de Hive.</span><span class="sxs-lookup"><span data-stu-id="149d7-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="149d7-2918">Otras propiedades (fuera de la sección de hello typeProperties) son compatibles con todas las actividades.</span><span class="sxs-lookup"><span data-stu-id="149d7-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="149d7-2919">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2919">JSON example</span></span>
<span data-ttu-id="149d7-2920">Hola después JSON define una actividad de Hive de HDInsight en una canalización.</span><span class="sxs-lookup"><span data-stu-id="149d7-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="149d7-2921">Para más información, consulte el artículo [Actividad de Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="149d7-2922">Actividad de Pig de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="149d7-2923">Puede especificar Hola propiedades en una definición de JSON de la actividad de Pig siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="149d7-2924">debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="149d7-2925">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-2926">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightPig de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="149d7-2927">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2927">Property</span></span> | <span data-ttu-id="149d7-2928">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2928">Description</span></span> | <span data-ttu-id="149d7-2929">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2930">script</span><span class="sxs-lookup"><span data-stu-id="149d7-2930">script</span></span> |<span data-ttu-id="149d7-2931">Especifique el script de Pig de hello en línea</span><span class="sxs-lookup"><span data-stu-id="149d7-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="149d7-2932">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2932">No</span></span> |
| <span data-ttu-id="149d7-2933">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="149d7-2933">script path</span></span> |<span data-ttu-id="149d7-2934">Almacenar el script de Pig hello en el almacenamiento de blobs de Azure y proporcionar Hola ruta toohello al archivo.</span><span class="sxs-lookup"><span data-stu-id="149d7-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="149d7-2935">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="149d7-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="149d7-2936">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="149d7-2936">Both cannot be used together.</span></span> <span data-ttu-id="149d7-2937">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="149d7-2938">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2938">No</span></span> |
| <span data-ttu-id="149d7-2939">define los campos</span><span class="sxs-lookup"><span data-stu-id="149d7-2939">defines</span></span> |<span data-ttu-id="149d7-2940">Especificar parámetros como pares clave/valor para hacer referencia a dentro de hello script de Pig</span><span class="sxs-lookup"><span data-stu-id="149d7-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="149d7-2941">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2941">No</span></span> |

<span data-ttu-id="149d7-2942">Estas propiedades de tipo son toohello específico de actividad de Pig.</span><span class="sxs-lookup"><span data-stu-id="149d7-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="149d7-2943">Otras propiedades (fuera de la sección de hello typeProperties) son compatibles con todas las actividades.</span><span class="sxs-lookup"><span data-stu-id="149d7-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="149d7-2944">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2944">JSON example</span></span>

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

<span data-ttu-id="149d7-2945">Para más información, consulte el artículo [Actividad de Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="149d7-2946">Actividad de MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="149d7-2947">Puede especificar Hola propiedades en una definición de JSON de actividad MapReduce siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="149d7-2948">debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="149d7-2949">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-2950">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightMapReduce de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="149d7-2951">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2951">Property</span></span> | <span data-ttu-id="149d7-2952">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2952">Description</span></span> | <span data-ttu-id="149d7-2953">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="149d7-2954">jarLinkedService</span></span> | <span data-ttu-id="149d7-2955">Nombre del programa Hola a servicio de almacenamiento de Azure que contiene el archivo JAR de Hola Hola vinculado.</span><span class="sxs-lookup"><span data-stu-id="149d7-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="149d7-2956">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2956">Yes</span></span> |
| <span data-ttu-id="149d7-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="149d7-2957">jarFilePath</span></span> | <span data-ttu-id="149d7-2958">Ruta de acceso toohello JAR el archivo en hello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="149d7-2959">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2959">Yes</span></span> | 
| <span data-ttu-id="149d7-2960">className</span><span class="sxs-lookup"><span data-stu-id="149d7-2960">className</span></span> | <span data-ttu-id="149d7-2961">Nombre de clase principal de hello en el archivo JAR de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="149d7-2962">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-2962">Yes</span></span> | 
| <span data-ttu-id="149d7-2963">argumentos</span><span class="sxs-lookup"><span data-stu-id="149d7-2963">arguments</span></span> | <span data-ttu-id="149d7-2964">Una lista de argumentos separados por comas para el programa de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="149d7-2965">En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="149d7-2966">toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores)</span><span class="sxs-lookup"><span data-stu-id="149d7-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="149d7-2967">No</span><span class="sxs-lookup"><span data-stu-id="149d7-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="149d7-2968">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="149d7-2969">Para más información, consulte el artículo [Actividad de MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="149d7-2970">Actividad de streaming de HDInsight</span><span class="sxs-lookup"><span data-stu-id="149d7-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="149d7-2971">Puede especificar Hola propiedades en una definición de JSON de actividad de Streaming de Hadoop siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="149d7-2972">debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="149d7-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="149d7-2973">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-2974">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightStreaming de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="149d7-2975">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-2975">Property</span></span> | <span data-ttu-id="149d7-2976">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="149d7-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="149d7-2977">mapper</span></span> | <span data-ttu-id="149d7-2978">Nombre del ejecutable de asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="149d7-2979">En el ejemplo de Hola, cat.exe es el asignador de hello ejecutable.</span><span class="sxs-lookup"><span data-stu-id="149d7-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="149d7-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="149d7-2980">reducer</span></span> | <span data-ttu-id="149d7-2981">Nombre del reductor Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="149d7-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="149d7-2982">En el ejemplo de Hola, wc.exe es reductor Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="149d7-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="149d7-2983">input</span><span class="sxs-lookup"><span data-stu-id="149d7-2983">input</span></span> | <span data-ttu-id="149d7-2984">Archivo de entrada (incluida la ubicación) para el asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="149d7-2985">En el ejemplo de Hola: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blob de hello, ejemplo/data/Gutenberg es la carpeta de Hola y davinci.txt es blob Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="149d7-2986">output</span><span class="sxs-lookup"><span data-stu-id="149d7-2986">output</span></span> | <span data-ttu-id="149d7-2987">Archivo de salida (incluida la ubicación) para el reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="149d7-2988">salida de Hello de trabajo de Streaming de Hadoop de Hola se escribe ubicación toohello especificado para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="149d7-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="149d7-2989">filePaths</span></span> | <span data-ttu-id="149d7-2990">Rutas de acceso para los ejecutables de asignador y reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="149d7-2991">En el ejemplo de Hola: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blob de hello, example/apps es la carpeta de Hola y wc.exe es ejecutable hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="149d7-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="149d7-2992">fileLinkedService</span></span> | <span data-ttu-id="149d7-2993">Servicio vinculado de almacenamiento Azure que representa el almacenamiento de Azure que contiene archivos de hello especificados en la sección de filePaths Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="149d7-2994">argumentos</span><span class="sxs-lookup"><span data-stu-id="149d7-2994">arguments</span></span> | <span data-ttu-id="149d7-2995">Una lista de argumentos separados por comas para el programa de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="149d7-2996">En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="149d7-2997">toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores)</span><span class="sxs-lookup"><span data-stu-id="149d7-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="149d7-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="149d7-2998">getDebugInfo</span></span> | <span data-ttu-id="149d7-2999">Un elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="149d7-2999">An optional element.</span></span> <span data-ttu-id="149d7-3000">Cuando se establece tooFailure, registros de Hola se descargan solo en caso de error.</span><span class="sxs-lookup"><span data-stu-id="149d7-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="149d7-3001">Cuando se establece tooAll, registros siempre se descargan independientemente del estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="149d7-3002">Debe especificar un conjunto de datos de salida de hello Hadoop Streaming Activity para hello **genera** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="149d7-3003">Este conjunto de datos puede ser simplemente un dataset ficticio que es necesario toodrive Hola canalización programación (etcetera diariamente, cada hora,.).</span><span class="sxs-lookup"><span data-stu-id="149d7-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="149d7-3004">Si la actividad hello no toma una entrada, puede omitir especifica un conjunto de datos de entrada de la actividad de Hola de hello **entradas** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="149d7-3005">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3005">JSON example</span></span>

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

<span data-ttu-id="149d7-3006">Para más información, consulte el artículo [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="149d7-3007">Actividad de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="149d7-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="149d7-3008">Puede especificar Hola propiedades en una definición de JSON de la actividad de Spark siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="149d7-3009">debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="149d7-3010">Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-3011">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightSpark de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="149d7-3012">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3012">Property</span></span> | <span data-ttu-id="149d7-3013">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3013">Description</span></span> | <span data-ttu-id="149d7-3014">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="149d7-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="149d7-3015">rootPath</span></span> | <span data-ttu-id="149d7-3016">contenedor de blobs de Azure de Hola y la carpeta que contiene el archivo de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="149d7-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="149d7-3017">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="149d7-3018">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3018">Yes</span></span> |
| <span data-ttu-id="149d7-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="149d7-3019">entryFilePath</span></span> | <span data-ttu-id="149d7-3020">Carpeta de raíz de toohello de ruta de acceso relativa del programa Hola Spark/paquete de código.</span><span class="sxs-lookup"><span data-stu-id="149d7-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="149d7-3021">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3021">Yes</span></span> |
| <span data-ttu-id="149d7-3022">className</span><span class="sxs-lookup"><span data-stu-id="149d7-3022">className</span></span> | <span data-ttu-id="149d7-3023">Clase principal de Spark o Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="149d7-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="149d7-3024">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3024">No</span></span> | 
| <span data-ttu-id="149d7-3025">argumentos</span><span class="sxs-lookup"><span data-stu-id="149d7-3025">arguments</span></span> | <span data-ttu-id="149d7-3026">Una lista de programas de Spark de toohello argumentos de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="149d7-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="149d7-3027">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3027">No</span></span> | 
| <span data-ttu-id="149d7-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="149d7-3028">proxyUser</span></span> | <span data-ttu-id="149d7-3029">programa de Spark hello tooexecute de tooimpersonate de la cuenta de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="149d7-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="149d7-3030">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3030">No</span></span> | 
| <span data-ttu-id="149d7-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="149d7-3031">sparkConfig</span></span> | <span data-ttu-id="149d7-3032">Propiedades de configuración de Spark.</span><span class="sxs-lookup"><span data-stu-id="149d7-3032">Spark configuration properties.</span></span> | <span data-ttu-id="149d7-3033">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3033">No</span></span> | 
| <span data-ttu-id="149d7-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="149d7-3034">getDebugInfo</span></span> | <span data-ttu-id="149d7-3035">Especifica cuando los archivos de registro de hello Spark son copiado toohello utilizado por el clúster de HDInsight de almacenamiento de Azure (o) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="149d7-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="149d7-3036">Valores permitidos: Ninguno, Siempre o Error.</span><span class="sxs-lookup"><span data-stu-id="149d7-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="149d7-3037">Valor predeterminado: Ninguno.</span><span class="sxs-lookup"><span data-stu-id="149d7-3037">Default value: None.</span></span> | <span data-ttu-id="149d7-3038">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3038">No</span></span> | 
| <span data-ttu-id="149d7-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="149d7-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="149d7-3040">Hola servicio vinculado de almacenamiento de Azure que contiene registros, las dependencias y archivo de trabajo de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="149d7-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="149d7-3041">Si no especifica un valor para esta propiedad, se usa almacenamiento de hello asociado con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149d7-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="149d7-3042">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="149d7-3043">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3043">JSON example</span></span>

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
<span data-ttu-id="149d7-3044">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="149d7-3044">Note hello following points:</span></span> 

- <span data-ttu-id="149d7-3045">Hola **tipo** propiedad se establece demasiado**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="149d7-3046">Hola **Ruta_raíz** se establece demasiado**adfspark\\pyFiles** donde adfspark es contenedor de blobs de Azure de Hola y pyFiles es la carpeta correctamente en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="149d7-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="149d7-3047">En este ejemplo, hello almacenamiento de blobs de Azure es hello uno que esté asociado con el clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="149d7-3048">Puede cargar Hola archivo tooa almacenamiento de Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="149d7-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="149d7-3049">Si lo hace, cree un toolink de servicio vinculado de almacenamiento de Azure que factoría de datos de toohello de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="149d7-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="149d7-3050">A continuación, especificar nombre de Hola de servicio de hello vinculado como un valor de hello **sparkJobLinkedService** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="149d7-3051">Vea [propiedades de la actividad de Spark](#spark-activity-properties) para obtener más información acerca de esta propiedad y otras propiedades compatibles con hello Spark actividad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="149d7-3052">Hola **entryFilePath** se establece toohello **test.py**, que es el archivo de python de hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="149d7-3053">Hola **getDebugInfo** propiedad se establece demasiado**siempre**, lo que significa que los archivos de registro de hello siempre están generado (éxito o error).</span><span class="sxs-lookup"><span data-stu-id="149d7-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="149d7-3054">Se recomienda que no establezca esta propiedad tooAlways en un entorno de producción a menos que esté solucionando un problema.</span><span class="sxs-lookup"><span data-stu-id="149d7-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="149d7-3055">Hola **genera** sección tiene un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="149d7-3056">Debe especificar un conjunto de datos de salida, incluso si el programa de spark hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="149d7-3057">Hola salida dataset unidades Hola programación para canalización hello (etcetera diariamente, cada hora,.).</span><span class="sxs-lookup"><span data-stu-id="149d7-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="149d7-3058">Para obtener más información acerca de la actividad de hello, consulte [Spark actividad](data-factory-spark.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="149d7-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="149d7-3059">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="149d7-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="149d7-3060">Puede especificar Hola propiedades en una definición de JSON de actividad de ejecución de lote de aprendizaje automático de Azure siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="149d7-3061">debe ser propiedad de tipo Hello para la actividad de hello: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="149d7-3062">Debe crear una máquina de Azure en primer lugar, el servicio vinculado de aprendizaje y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-3063">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooAzureMLBatchExecution de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="149d7-3064">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3064">Property</span></span> | <span data-ttu-id="149d7-3065">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3065">Description</span></span> | <span data-ttu-id="149d7-3066">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="149d7-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="149d7-3067">webServiceInput</span></span> | <span data-ttu-id="149d7-3068">Hola toobe de conjunto de datos se pasa como entrada para el servicio web de aprendizaje automático de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="149d7-3069">Este conjunto de datos también debe incluirse en las entradas de Hola para actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="149d7-3070">Use webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="149d7-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="149d7-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="149d7-3071">webServiceInputs</span></span> | <span data-ttu-id="149d7-3072">Especificar los conjuntos de datos toobe pasadas como entradas para hello servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="149d7-3073">Si el servicio web de hello toma varias entradas, utilice la propiedad de webServiceInputs de hello en lugar de utilizar la propiedad de webServiceInput Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="149d7-3074">Conjuntos de datos que se hace referencia mediante hello **webServiceInputs** también debe incluirse en hello actividad **entradas**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="149d7-3075">Use webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="149d7-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="149d7-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="149d7-3076">webServiceOutputs</span></span> | <span data-ttu-id="149d7-3077">Hola conjuntos de datos que se asignan como salidas para el servicio web de aprendizaje automático de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="149d7-3078">servicio web de Hello devuelve datos de salida de este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="149d7-3079">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3079">Yes</span></span> | 
<span data-ttu-id="149d7-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-3080">globalParameters</span></span> | <span data-ttu-id="149d7-3081">Especificar valores para parámetros de servicio web de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="149d7-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="149d7-3082">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="149d7-3083">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3083">JSON example</span></span>
<span data-ttu-id="149d7-3084">En este ejemplo, actividad hello tiene el conjunto de datos de hello **MLSqlInput** como entrada y **MLSqlOutput** como salida de hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="149d7-3085">Hola **MLSqlInput** se pasa como un servicio web de entrada toohello por mediante hello **webServiceInput** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="149d7-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="149d7-3086">Hola **MLSqlOutput** se pasa como un servicio de Web de salida toohello por mediante hello **webServiceOutputs** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="149d7-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="149d7-3087">En el ejemplo de Hola a JSON, Hola implementado Azure Machine Learning servicio Web utiliza un lector y un sistema de escritura módulo tooread/escribir datos de / tooan base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="149d7-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="149d7-3088">Este servicio Web expone Hola cuatro parámetros siguientes: nombre del servidor, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="149d7-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="149d7-3089">Solo entradas y salidas de hello AzureMLBatchExecution actividad pueden pasarse como parámetros toohello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="149d7-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="149d7-3090">Por ejemplo, en hello por encima del fragmento de JSON, MLSqlInput es una entrada toohello AzureMLBatchExecution actividad, que se pasa como un servicio Web de entrada toohello a través del parámetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="149d7-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="149d7-3091">Actividad de recursos de actualización de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="149d7-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="149d7-3092">Puede especificar Hola propiedades en una definición de JSON de actividad de recursos de actualización de aprendizaje automático de Azure siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="149d7-3093">debe ser propiedad de tipo Hello para la actividad de hello: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="149d7-3094">Debe crear una máquina de Azure en primer lugar, el servicio vinculado de aprendizaje y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-3095">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooAzureMLUpdateResource de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="149d7-3096">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3096">Property</span></span> | <span data-ttu-id="149d7-3097">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3097">Description</span></span> | <span data-ttu-id="149d7-3098">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="149d7-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="149d7-3099">trainedModelName</span></span> | <span data-ttu-id="149d7-3100">Nombre del programa Hola a volver a entrenar el modelo.</span><span class="sxs-lookup"><span data-stu-id="149d7-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="149d7-3101">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3101">Yes</span></span> |  
<span data-ttu-id="149d7-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="149d7-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="149d7-3103">Archivo conjunto de datos señalador toohello iLearner devuelto por la operación de reciclaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="149d7-3104">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="149d7-3105">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3105">JSON example</span></span>
<span data-ttu-id="149d7-3106">canalización de Hello tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="149d7-3107">Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma los datos de entrenamiento de hello como entrada y genera un archivo iLearner como salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="149d7-3108">actividad Hello invoca el servicio web de aprendizaje hello (se expone como un servicio web experimento de entrenamiento) con los datos de entrenamiento de entradas de Hola y recibe el archivo ilearner de hello de hello webservice.</span><span class="sxs-lookup"><span data-stu-id="149d7-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="149d7-3109">Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="149d7-3110">Actividad U-SQL de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="149d7-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="149d7-3111">Puede especificar Hola propiedades en una definición de JSON de la actividad de U-SQL siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="149d7-3112">debe ser propiedad de tipo Hello para la actividad de hello: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="149d7-3113">Debe crear un servicio de análisis de Azure Data Lake vinculado y especifique el nombre de hello del mismo como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-3114">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de actividad tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="149d7-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="149d7-3115">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3115">Property</span></span> | <span data-ttu-id="149d7-3116">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3116">Description</span></span> | <span data-ttu-id="149d7-3117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="149d7-3118">scriptPath</span></span> |<span data-ttu-id="149d7-3119">Toofolder de ruta de acceso que contiene el script de Hola U-SQL.</span><span class="sxs-lookup"><span data-stu-id="149d7-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="149d7-3120">Nombre del archivo hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="149d7-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="149d7-3121">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="149d7-3121">No (if you use script)</span></span> |
| <span data-ttu-id="149d7-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="149d7-3122">scriptLinkedService</span></span> |<span data-ttu-id="149d7-3123">Servicio vinculado que se vincula el almacenamiento de Hola que contiene la factoría de datos de hello script toohello</span><span class="sxs-lookup"><span data-stu-id="149d7-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="149d7-3124">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="149d7-3124">No (if you use script)</span></span> |
| <span data-ttu-id="149d7-3125">script</span><span class="sxs-lookup"><span data-stu-id="149d7-3125">script</span></span> |<span data-ttu-id="149d7-3126">Especifique el script en línea en lugar de scriptPath y scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="149d7-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="149d7-3127">Por ejemplo: "script": "Prueba CREAR BASE DE DATOS".</span><span class="sxs-lookup"><span data-stu-id="149d7-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="149d7-3128">No (si usa scriptPath y scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="149d7-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="149d7-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="149d7-3129">degreeOfParallelism</span></span> |<span data-ttu-id="149d7-3130">número máximo de Hola de nodos simultáneamente utiliza trabajo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="149d7-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="149d7-3131">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3131">No</span></span> |
| <span data-ttu-id="149d7-3132">prioridad</span><span class="sxs-lookup"><span data-stu-id="149d7-3132">priority</span></span> |<span data-ttu-id="149d7-3133">Determina qué trabajos de todos los que se ponen en cola deberían estar seleccionado toorun en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="149d7-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="149d7-3134">Hola Hola número inferior, prioridad Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="149d7-3135">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3135">No</span></span> |
| <span data-ttu-id="149d7-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="149d7-3136">parameters</span></span> |<span data-ttu-id="149d7-3137">Parámetros de script de Hola U-SQL</span><span class="sxs-lookup"><span data-stu-id="149d7-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="149d7-3138">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="149d7-3139">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3139">JSON example</span></span>

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

<span data-ttu-id="149d7-3140">Para más información, consulte [Actividad de U-SQL de Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="149d7-3141">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="149d7-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="149d7-3142">Puede especificar propiedades en una definición de JSON de actividad de procedimiento almacenado siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="149d7-3143">debe ser propiedad de tipo Hello para la actividad de hello: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="149d7-3144">Debe crear un uno de hello después servicios vinculados y especificar el nombre de Hola de servicio de hello vinculado como un valor de hello **linkedServiceName** propiedad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="149d7-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="149d7-3145">SQL Server</span></span> 
- <span data-ttu-id="149d7-3146">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-3146">Azure SQL Database</span></span>
- <span data-ttu-id="149d7-3147">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="149d7-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="149d7-3148">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooSqlServerStoredProcedure de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="149d7-3149">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3149">Property</span></span> | <span data-ttu-id="149d7-3150">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3150">Description</span></span> | <span data-ttu-id="149d7-3151">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149d7-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="149d7-3152">storedProcedureName</span></span> |<span data-ttu-id="149d7-3153">Especifique el nombre de hello del procedimiento de hello almacenado en la base de datos de SQL Azure de Hola o almacenamiento de datos de SQL de Azure que está representado por el servicio de hello vinculado que Hola usos de la tabla de salida.</span><span class="sxs-lookup"><span data-stu-id="149d7-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="149d7-3154">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3154">Yes</span></span> |
| <span data-ttu-id="149d7-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="149d7-3155">storedProcedureParameters</span></span> |<span data-ttu-id="149d7-3156">Especifique valores para los parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="149d7-3157">Si necesitas toopass null para un parámetro, use la sintaxis de hello: "param1": null (todas las minúsculas).</span><span class="sxs-lookup"><span data-stu-id="149d7-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="149d7-3158">Vea Hola después toolearn de ejemplo sobre el uso de esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="149d7-3159">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3159">No</span></span> |

<span data-ttu-id="149d7-3160">Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para hello almacenado toorun de actividad de procedimiento.</span><span class="sxs-lookup"><span data-stu-id="149d7-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="149d7-3161">conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="149d7-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="149d7-3162">Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial.</span><span class="sxs-lookup"><span data-stu-id="149d7-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="149d7-3163">Debe especificar un conjunto de datos para una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="149d7-3164">Conjunto de datos de salida especifica hello **programación** para hello almacenados actividad de procedimiento (cada hora, semanalmente, mensualmente, etcetera).</span><span class="sxs-lookup"><span data-stu-id="149d7-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="149d7-3165">Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="149d7-3166">Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="149d7-3167">Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="149d7-3168">Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a.</span><span class="sxs-lookup"><span data-stu-id="149d7-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="149d7-3169">En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio**, que se usa solo la programación de hello toospecify para ejecutar Hola actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="149d7-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="149d7-3170">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3170">JSON example</span></span>

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

<span data-ttu-id="149d7-3171">Para más información, consulte el artículo [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="149d7-3172">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="149d7-3172">.NET custom activity</span></span>
<span data-ttu-id="149d7-3173">Puede especificar Hola propiedades en una definición de JSON de actividad personalizada .NET siguientes.</span><span class="sxs-lookup"><span data-stu-id="149d7-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="149d7-3174">debe ser propiedad de tipo Hello para la actividad de hello: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="149d7-3175">Debe crear un servicio vinculado de HDInsight de Azure o un lote de Azure vinculada de servicio y especificar el nombre de Hola de servicio de hello vinculado como un valor de hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="149d7-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="149d7-3176">Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooDotNetActivity de actividad:</span><span class="sxs-lookup"><span data-stu-id="149d7-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="149d7-3177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="149d7-3177">Property</span></span> | <span data-ttu-id="149d7-3178">Descripción</span><span class="sxs-lookup"><span data-stu-id="149d7-3178">Description</span></span> | <span data-ttu-id="149d7-3179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="149d7-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="149d7-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="149d7-3180">AssemblyName</span></span> | <span data-ttu-id="149d7-3181">Nombre del ensamblado de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3181">Name of hello assembly.</span></span> <span data-ttu-id="149d7-3182">En el ejemplo de Hola, es: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="149d7-3183">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3183">Yes</span></span> |
| <span data-ttu-id="149d7-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="149d7-3184">EntryPoint</span></span> |<span data-ttu-id="149d7-3185">Nombre de clase de Hola que implementa la interfaz de IDotNetActivity Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="149d7-3186">En el ejemplo de Hola, es: **MyDotNetActivityNS.MyDotNetActivity** donde MyDotNetActivityNS es el espacio de nombres de Hola y MyDotNetActivity es clase hello.</span><span class="sxs-lookup"><span data-stu-id="149d7-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="149d7-3187">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3187">Yes</span></span> | 
| <span data-ttu-id="149d7-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="149d7-3188">PackageLinkedService</span></span> | <span data-ttu-id="149d7-3189">Nombre del servicio vinculado de almacenamiento de Azure que señala el almacenamiento de blobs de toohello que contiene el archivo zip de actividad personalizada de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="149d7-3190">En el ejemplo de Hola, es: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="149d7-3191">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3191">Yes</span></span> |
| <span data-ttu-id="149d7-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="149d7-3192">PackageFile</span></span> | <span data-ttu-id="149d7-3193">Nombre del archivo zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3193">Name of hello zip file.</span></span> <span data-ttu-id="149d7-3194">En el ejemplo de Hola, es: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="149d7-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="149d7-3195">Sí</span><span class="sxs-lookup"><span data-stu-id="149d7-3195">Yes</span></span> |
| <span data-ttu-id="149d7-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="149d7-3196">extendedProperties</span></span> | <span data-ttu-id="149d7-3197">Propiedades extendidas que se pueden definir y pasar de código de .NET toohello.</span><span class="sxs-lookup"><span data-stu-id="149d7-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="149d7-3198">En este ejemplo, Hola **SliceStart** variable está establecida el valor de tooa en función de la variable del sistema SliceStart Hola.</span><span class="sxs-lookup"><span data-stu-id="149d7-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="149d7-3199">No</span><span class="sxs-lookup"><span data-stu-id="149d7-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="149d7-3200">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="149d7-3200">JSON example</span></span>

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

<span data-ttu-id="149d7-3201">Para obtener información detallada, vea el artículo [Uso de actividades personalizadas en Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="149d7-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="149d7-3202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="149d7-3202">Next Steps</span></span>
<span data-ttu-id="149d7-3203">Vea Hola tutoriales:</span><span class="sxs-lookup"><span data-stu-id="149d7-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="149d7-3204">Tutorial: crear una canalización con la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="149d7-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="149d7-3205">Tutorial: crear una canalización con la actividad de hive</span><span class="sxs-lookup"><span data-stu-id="149d7-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)