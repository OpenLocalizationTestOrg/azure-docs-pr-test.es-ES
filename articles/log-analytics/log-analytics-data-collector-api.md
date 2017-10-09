---
title: "API del recopilador de datos de análisis HTTP aaaLog | Documentos de Microsoft"
description: "Puede usar el repositorio de análisis de registros de hello API de recopilador de datos de análisis de registros HTTP tooadd POST JSON datos toohello desde cualquier cliente que puede llamar a la API de REST de Hola. Este artículo describe cómo toouse Hola API y tiene algunos ejemplos de cómo toopublish datos mediante el uso de diferentes lenguajes de programación."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="0b4ab-104">Enviar datos tooLog análisis con hello API de recopilador de datos HTTP</span><span class="sxs-lookup"><span data-stu-id="0b4ab-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="0b4ab-105">Este artículo muestra cómo toouse Hola API de recopilador de datos HTTP toosend datos tooLog análisis desde un cliente de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="0b4ab-106">Se describe cómo incluir en una solicitud de datos tooformat recopilados por el script o la aplicación y tiene esa solicitud autorizada por análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="0b4ab-107">Se proporcionan ejemplos de PowerShell, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="0b4ab-108">Conceptos</span><span class="sxs-lookup"><span data-stu-id="0b4ab-108">Concepts</span></span>
<span data-ttu-id="0b4ab-109">Puede usar Hola API de recopilador de datos HTTP toosend datos tooLog análisis desde cualquier cliente que puede llamar a una API de REST.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="0b4ab-110">Podría tratarse de un runbook en automatización de Azure que recopila la administración de datos de Azure u otra nube o se podrían formar parte de un sistema de administración alternativo que usa el análisis de registros tooconsolidate y analizar datos.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="0b4ab-111">Todos los datos en el repositorio de análisis de registros de Hola se almacena como un registro con un tipo de registro concreto.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="0b4ab-112">Dar formato a su toohello de toosend de datos API de recopilador de datos HTTP como varios registros en JSON.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="0b4ab-113">Al enviar datos de hello, se crea un registro individual en el repositorio de Hola para cada registro de carga de la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Información general del recopilador de datos HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="0b4ab-115">Creación de una solicitud</span><span class="sxs-lookup"><span data-stu-id="0b4ab-115">Create a request</span></span>
<span data-ttu-id="0b4ab-116">API de recopilador de datos de toouse Hola HTTP, cree una solicitud POST que incluye Hola datos toosend en JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="0b4ab-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="0b4ab-117">Hola siguientes tres tablas lista Hola atributos que son necesarios para cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="0b4ab-118">Se describe cada atributo con más detalle más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="0b4ab-119">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="0b4ab-119">Request URI</span></span>
| <span data-ttu-id="0b4ab-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b4ab-120">Attribute</span></span> | <span data-ttu-id="0b4ab-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0b4ab-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="0b4ab-122">Método</span><span class="sxs-lookup"><span data-stu-id="0b4ab-122">Method</span></span> |<span data-ttu-id="0b4ab-123">POST</span><span class="sxs-lookup"><span data-stu-id="0b4ab-123">POST</span></span> |
| <span data-ttu-id="0b4ab-124">URI</span><span class="sxs-lookup"><span data-stu-id="0b4ab-124">URI</span></span> |<span data-ttu-id="0b4ab-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="0b4ab-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="0b4ab-126">Tipo de contenido</span><span class="sxs-lookup"><span data-stu-id="0b4ab-126">Content type</span></span> |<span data-ttu-id="0b4ab-127">application/json</span><span class="sxs-lookup"><span data-stu-id="0b4ab-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="0b4ab-128">Parámetros de URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="0b4ab-128">Request URI parameters</span></span>
| <span data-ttu-id="0b4ab-129">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0b4ab-129">Parameter</span></span> | <span data-ttu-id="0b4ab-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b4ab-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0b4ab-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="0b4ab-131">CustomerID</span></span> |<span data-ttu-id="0b4ab-132">Identificador único de Hello para el área de trabajo de hello Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="0b4ab-133">Recurso</span><span class="sxs-lookup"><span data-stu-id="0b4ab-133">Resource</span></span> |<span data-ttu-id="0b4ab-134">nombre del recurso Hola API: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="0b4ab-135">Versión de API</span><span class="sxs-lookup"><span data-stu-id="0b4ab-135">API Version</span></span> |<span data-ttu-id="0b4ab-136">versión de Hola de hello API toouse a esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="0b4ab-137">Actualmente, es 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0b4ab-138">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="0b4ab-138">Request headers</span></span>
| <span data-ttu-id="0b4ab-139">Encabezado</span><span class="sxs-lookup"><span data-stu-id="0b4ab-139">Header</span></span> | <span data-ttu-id="0b4ab-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b4ab-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0b4ab-141">Autorización</span><span class="sxs-lookup"><span data-stu-id="0b4ab-141">Authorization</span></span> |<span data-ttu-id="0b4ab-142">firma de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-142">hello authorization signature.</span></span> <span data-ttu-id="0b4ab-143">Más adelante en el artículo de hello, puede leer acerca de cómo toocreate un HMAC-SHA256 encabezado.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="0b4ab-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="0b4ab-144">Log-Type</span></span> |<span data-ttu-id="0b4ab-145">Especifique el tipo de registro de hello de datos de Hola que se está enviando.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="0b4ab-146">Actualmente, el tipo de registro de hello es compatible con solo caracteres alfabéticos.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="0b4ab-147">No admite valores numéricos ni caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="0b4ab-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="0b4ab-148">x-ms-date</span></span> |<span data-ttu-id="0b4ab-149">fecha de Hola se procesó la solicitud hello, en formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="0b4ab-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="0b4ab-150">time-generated-field</span></span> |<span data-ttu-id="0b4ab-151">nombre de Hola de un campo de datos de Hola que contiene la marca de tiempo de Hola Hola del elemento de datos.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="0b4ab-152">Si especifica un campo, su contenido se usa para **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="0b4ab-153">Si no se especifica este campo, Hola predeterminado para **TimeGenerated** es hora de Hola que hello es ingestión mensaje.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="0b4ab-154">contenido de Hello del campo de mensaje de Hola debe seguir el formato de hello ISO 8601 aaaa-MM-ddTHH.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="0b4ab-155">Autorización</span><span class="sxs-lookup"><span data-stu-id="0b4ab-155">Authorization</span></span>
<span data-ttu-id="0b4ab-156">Las API de recopilador de datos de análisis de registro HTTP de solicitud toohello debe incluir un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="0b4ab-157">tooauthenticate una solicitud, debe firmar solicitud de hello con hello principal o clave secundaria de Hola de área de trabajo de Hola que está realizando la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="0b4ab-158">A continuación, pasar esa firma como parte de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="0b4ab-159">Este es el formato hello para el encabezado de autorización de Hola:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="0b4ab-160">*WorkspaceID* es Hola identificador único para el área de trabajo de hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="0b4ab-161">*Firma* es un [código de autenticación de mensajes basado en Hash (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que está construido a partir de la solicitud de hello y, a continuación, se calcula mediante hello [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b4ab-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="0b4ab-162">Luego se codifica con la codificación Base64.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="0b4ab-163">Utilice este Hola de tooencode formato **SharedKey** cadena de firma:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="0b4ab-164">Este es un ejemplo de una cadena de firma:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="0b4ab-165">Cuando haya cadena de firma de hello, codificar mediante Hola algoritmo HMAC-SHA256 en hello cadena codificada mediante UTF-8 y, a continuación, codificar el resultado de hello como Base64.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="0b4ab-166">Use este formato:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="0b4ab-167">ejemplos de Hello en las secciones siguientes se Hola tienen toohelp de código de ejemplo se crea un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="0b4ab-168">Request body</span><span class="sxs-lookup"><span data-stu-id="0b4ab-168">Request body</span></span>
<span data-ttu-id="0b4ab-169">cuerpo de Hola de mensaje de bienvenida debe estar en JSON.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="0b4ab-170">Debe incluir uno o más registros con pares de nombre y valor de propiedad de hello en este formato:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="0b4ab-171">Puede procesar por lotes varios registros en una única solicitud mediante Hola siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="0b4ab-172">Todos los registros de hello deben estar Hola mismo tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="0b4ab-173">Propiedades y tipo de registro</span><span class="sxs-lookup"><span data-stu-id="0b4ab-173">Record type and properties</span></span>
<span data-ttu-id="0b4ab-174">Definir un tipo de registro personalizado al enviar datos a través de la API de recopilador de datos de análisis de registros HTTP Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="0b4ab-175">Actualmente, no se puede escribir datos tooexisting tipos de registro creados por otros tipos de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="0b4ab-176">Análisis de registros leen los datos entrantes de hello y, a continuación, crea propiedades que coinciden con los tipos de datos de Hola de valores de hello que especifique.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="0b4ab-177">Cada toohello de solicitud API de análisis de registros debe incluir un **tipo de registro** encabezado con el nombre de hello para el tipo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="0b4ab-178">sufijo de Hello **_CL** es nombre automáticamente anexados toohello escriba toodistinguish desde el registro de otro tipos como un registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="0b4ab-179">Por ejemplo, si escribe el nombre de hello **MyNewRecordType**, análisis de registros, se crea un registro con el tipo de hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="0b4ab-180">Esto ayuda a garantizar que no haya conflictos entre los nombres de tipo creados por el usuario y los incluidos en las soluciones de Microsoft actuales o futuras.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="0b4ab-181">de tipo de datos de la propiedad tooidentify, análisis de registros agrega un nombre de propiedad toohello de sufijo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="0b4ab-182">Si una propiedad contiene un valor null, no se incluye la propiedad hello en ese registro.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="0b4ab-183">Esta tabla enumera el tipo de datos de propiedad de Hola y el sufijo correspondiente:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="0b4ab-184">Tipo de datos de la propiedad</span><span class="sxs-lookup"><span data-stu-id="0b4ab-184">Property data type</span></span> | <span data-ttu-id="0b4ab-185">Sufijo</span><span class="sxs-lookup"><span data-stu-id="0b4ab-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="0b4ab-186">Cadena</span><span class="sxs-lookup"><span data-stu-id="0b4ab-186">String</span></span> |<span data-ttu-id="0b4ab-187">_s</span><span class="sxs-lookup"><span data-stu-id="0b4ab-187">_s</span></span> |
| <span data-ttu-id="0b4ab-188">Booleano</span><span class="sxs-lookup"><span data-stu-id="0b4ab-188">Boolean</span></span> |<span data-ttu-id="0b4ab-189">_b</span><span class="sxs-lookup"><span data-stu-id="0b4ab-189">_b</span></span> |
| <span data-ttu-id="0b4ab-190">Double</span><span class="sxs-lookup"><span data-stu-id="0b4ab-190">Double</span></span> |<span data-ttu-id="0b4ab-191">_d</span><span class="sxs-lookup"><span data-stu-id="0b4ab-191">_d</span></span> |
| <span data-ttu-id="0b4ab-192">Fecha/hora</span><span class="sxs-lookup"><span data-stu-id="0b4ab-192">Date/time</span></span> |<span data-ttu-id="0b4ab-193">_t</span><span class="sxs-lookup"><span data-stu-id="0b4ab-193">_t</span></span> |
| <span data-ttu-id="0b4ab-194">GUID</span><span class="sxs-lookup"><span data-stu-id="0b4ab-194">GUID</span></span> |<span data-ttu-id="0b4ab-195">_g</span><span class="sxs-lookup"><span data-stu-id="0b4ab-195">_g</span></span> |

<span data-ttu-id="0b4ab-196">tipo de datos de Hola que utiliza el análisis de registros para cada propiedad depende de si tipo de registro de hello para el nuevo registro de hello ya existe.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="0b4ab-197">Si no existe el tipo de registro de hello, análisis de registros crea uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="0b4ab-198">Análisis de registros usa Hola JSON inferencia toodetermine Hola tipo de datos para cada propiedad para el nuevo registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="0b4ab-199">Si existe el tipo de registro de hello, análisis de registros intenta toocreate un nuevo registro en función de las propiedades existentes.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="0b4ab-200">Si hello tipo de datos para una propiedad en el nuevo registro de hello no coincide con y no se puede convertir toohello existente de tipo o si hello registro incluye una propiedad que no existe, análisis de registros crea una nueva propiedad que tiene el sufijo relevante Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="0b4ab-201">Por ejemplo, esta entrada de envío crearía un registro con tres propiedades **number_d**, **boolean_b** y **string_s**:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Registro de ejemplo 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="0b4ab-203">Si, a continuación, envía la entrada siguiente con todos los valores con formato como cadenas, no debería cambiar propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="0b4ab-204">Estos valores pueden ser tooexisting convertir tipos de datos:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-204">These values can be converted tooexisting data types:</span></span>

![Registro de ejemplo 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="0b4ab-206">Pero, si, a continuación, ha realizado este envío siguiente, análisis de registros crearía Hola nuevas propiedades **boolean_d** y **string_d**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="0b4ab-207">Estos valores no se pueden convertir:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-207">These values can't be converted:</span></span>

![Registro de ejemplo 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="0b4ab-209">Si, a continuación, envían Hola siguiente entrada, antes de que se creó el tipo de registro de hello, análisis de registros crearía un registro con tres propiedades **número**, **boolean_s**, y **string_s**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="0b4ab-210">En esta entrada, cada uno de los valores iniciales de hello formato es como una cadena:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Registro de ejemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="0b4ab-212">Límites de datos</span><span class="sxs-lookup"><span data-stu-id="0b4ab-212">Data limits</span></span>
<span data-ttu-id="0b4ab-213">Hay algunas restricciones sobre los datos de hello registrados toohello API de recopilación de datos de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="0b4ab-214">Máximo de 30 MB por post tooLog API de recopilador de datos de análisis.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="0b4ab-215">Se trata de un límite de tamaño para una sola publicación.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-215">This is a size limit for a single post.</span></span> <span data-ttu-id="0b4ab-216">Si datos Hola desde un solo elemento para exponer que supera los 30 MB, debe dividir Hola datos seguridad toosmaller tamaño fragmentos y envían al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="0b4ab-217">Límite de 32 kB para los valores de campo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="0b4ab-218">Si el valor del campo de hello es mayor que 32 KB, se truncará datos Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="0b4ab-219">El número máximo recomendado de campos para un tipo determinado es 50.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="0b4ab-220">Se trata de un límite práctico desde una perspectiva de la experiencia de búsqueda y la facilidad de uso.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="0b4ab-221">Códigos de retorno</span><span class="sxs-lookup"><span data-stu-id="0b4ab-221">Return codes</span></span>
<span data-ttu-id="0b4ab-222">Hola código de estado HTTP 200 significa que se ha recibido esa solicitud de hello para el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="0b4ab-223">Esto indica que esa operación Hola que se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="0b4ab-224">Esta tabla muestra hello conjunto completo de códigos de estado que podría devolver el servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="0b4ab-225">Código</span><span class="sxs-lookup"><span data-stu-id="0b4ab-225">Code</span></span> | <span data-ttu-id="0b4ab-226">Estado</span><span class="sxs-lookup"><span data-stu-id="0b4ab-226">Status</span></span> | <span data-ttu-id="0b4ab-227">Código de error</span><span class="sxs-lookup"><span data-stu-id="0b4ab-227">Error code</span></span> | <span data-ttu-id="0b4ab-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b4ab-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0b4ab-229">200</span><span class="sxs-lookup"><span data-stu-id="0b4ab-229">200</span></span> |<span data-ttu-id="0b4ab-230">OK</span><span class="sxs-lookup"><span data-stu-id="0b4ab-230">OK</span></span> | |<span data-ttu-id="0b4ab-231">correctamente se aceptó la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="0b4ab-232">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-232">400</span></span> |<span data-ttu-id="0b4ab-233">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-233">Bad request</span></span> |<span data-ttu-id="0b4ab-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="0b4ab-234">InactiveCustomer</span></span> |<span data-ttu-id="0b4ab-235">se ha cerrado el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="0b4ab-236">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-236">400</span></span> |<span data-ttu-id="0b4ab-237">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-237">Bad request</span></span> |<span data-ttu-id="0b4ab-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="0b4ab-238">InvalidApiVersion</span></span> |<span data-ttu-id="0b4ab-239">versión de Hola API que especificó no se reconoció por servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="0b4ab-240">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-240">400</span></span> |<span data-ttu-id="0b4ab-241">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-241">Bad request</span></span> |<span data-ttu-id="0b4ab-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="0b4ab-242">InvalidCustomerId</span></span> |<span data-ttu-id="0b4ab-243">Id. de área de trabajo de Hello especificado no es válido.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="0b4ab-244">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-244">400</span></span> |<span data-ttu-id="0b4ab-245">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-245">Bad request</span></span> |<span data-ttu-id="0b4ab-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="0b4ab-246">InvalidDataFormat</span></span> |<span data-ttu-id="0b4ab-247">No envió un formato JSON no válido.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="0b4ab-248">cuerpo de respuesta de Hello podría contener más información acerca de cómo tooresolve Hola error.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="0b4ab-249">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-249">400</span></span> |<span data-ttu-id="0b4ab-250">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-250">Bad request</span></span> |<span data-ttu-id="0b4ab-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="0b4ab-251">InvalidLogType</span></span> |<span data-ttu-id="0b4ab-252">tipo de registro de Hello había especificado contiene caracteres especiales o valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="0b4ab-253">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-253">400</span></span> |<span data-ttu-id="0b4ab-254">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-254">Bad request</span></span> |<span data-ttu-id="0b4ab-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="0b4ab-255">MissingApiVersion</span></span> |<span data-ttu-id="0b4ab-256">no se especificó la versión de la API de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="0b4ab-257">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-257">400</span></span> |<span data-ttu-id="0b4ab-258">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-258">Bad request</span></span> |<span data-ttu-id="0b4ab-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="0b4ab-259">MissingContentType</span></span> |<span data-ttu-id="0b4ab-260">no se especificó el tipo de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="0b4ab-261">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-261">400</span></span> |<span data-ttu-id="0b4ab-262">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-262">Bad request</span></span> |<span data-ttu-id="0b4ab-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="0b4ab-263">MissingLogType</span></span> |<span data-ttu-id="0b4ab-264">Hola necesarios no se especificó el tipo de valor de registro.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="0b4ab-265">400</span><span class="sxs-lookup"><span data-stu-id="0b4ab-265">400</span></span> |<span data-ttu-id="0b4ab-266">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-266">Bad request</span></span> |<span data-ttu-id="0b4ab-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="0b4ab-267">UnsupportedContentType</span></span> |<span data-ttu-id="0b4ab-268">tipo de contenido de Hello no se estableció demasiado**application/json**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="0b4ab-269">403</span><span class="sxs-lookup"><span data-stu-id="0b4ab-269">403</span></span> |<span data-ttu-id="0b4ab-270">Prohibido</span><span class="sxs-lookup"><span data-stu-id="0b4ab-270">Forbidden</span></span> |<span data-ttu-id="0b4ab-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="0b4ab-271">InvalidAuthorization</span></span> |<span data-ttu-id="0b4ab-272">servicio de Hola Hola de tooauthenticate solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="0b4ab-273">Compruebe que esa clave de conexión y el Id. de área de trabajo de hello son válidos.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="0b4ab-274">404</span><span class="sxs-lookup"><span data-stu-id="0b4ab-274">404</span></span> |<span data-ttu-id="0b4ab-275">No encontrado</span><span class="sxs-lookup"><span data-stu-id="0b4ab-275">Not Found</span></span> | | <span data-ttu-id="0b4ab-276">Dirección URL de hello proporcionada no es correcto, u Hola solicitud es demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="0b4ab-277">429</span><span class="sxs-lookup"><span data-stu-id="0b4ab-277">429</span></span> |<span data-ttu-id="0b4ab-278">Demasiadas solicitudes</span><span class="sxs-lookup"><span data-stu-id="0b4ab-278">Too Many Requests</span></span> | | <span data-ttu-id="0b4ab-279">servicio de Hello está experimentando un gran volumen de datos de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="0b4ab-280">Vuelva a intentar la solicitud de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="0b4ab-281">500</span><span class="sxs-lookup"><span data-stu-id="0b4ab-281">500</span></span> |<span data-ttu-id="0b4ab-282">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="0b4ab-282">Internal Server Error</span></span> |<span data-ttu-id="0b4ab-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="0b4ab-283">UnspecifiedError</span></span> |<span data-ttu-id="0b4ab-284">servicio de Hello encontró un error interno.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-284">hello service encountered an internal error.</span></span> <span data-ttu-id="0b4ab-285">Vuelva a intentar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-285">Please retry hello request.</span></span> |
| <span data-ttu-id="0b4ab-286">503</span><span class="sxs-lookup"><span data-stu-id="0b4ab-286">503</span></span> |<span data-ttu-id="0b4ab-287">Servicio no disponible</span><span class="sxs-lookup"><span data-stu-id="0b4ab-287">Service Unavailable</span></span> |<span data-ttu-id="0b4ab-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="0b4ab-288">ServiceUnavailable</span></span> |<span data-ttu-id="0b4ab-289">servicio de Hello es actualmente las solicitudes de tooreceive disponible.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="0b4ab-290">Vuelva a intentar realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="0b4ab-291">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="0b4ab-291">Query data</span></span>
<span data-ttu-id="0b4ab-292">datos de tooquery enviados por hello API de recopilador de datos de HTTP de análisis de registros, búsqueda de registros con **tipo** que es igual toohello **LogType** valor que ha especificado, se anexa con **_CL**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="0b4ab-293">Por ejemplo, si utilizó **MyCustomLog**, se devolverán todos los registros cuyo **Type= MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="0b4ab-294">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="0b4ab-295">Solicitudes de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0b4ab-295">Sample requests</span></span>
<span data-ttu-id="0b4ab-296">En las secciones siguientes de hello, encontrará ejemplos de cómo toosubmit datos toohello API de recopilador de datos de análisis de registros HTTP mediante el uso de diferentes lenguajes de programación.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="0b4ab-297">Para cada ejemplo, realice estos pasos tooset variables de hello para el encabezado de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="0b4ab-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="0b4ab-298">En el portal de Operations Management Suite hello, seleccione hello **configuración** icono y, a continuación, seleccione hello **orígenes conectados** ficha.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="0b4ab-299">toohello derecha de **Id. de área de trabajo**, seleccione el icono de copiar de Hola y, a continuación, pegue el identificador hello como valor de Hola de hello **Id. de cliente** variable.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="0b4ab-300">toohello derecha de **Primary Key**, seleccione el icono de copiar de Hola y, a continuación, pegue el identificador hello como valor de Hola de hello **Shared Key** variable.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="0b4ab-301">Como alternativa, puede cambiar las variables de hello para el tipo de registro de hello y datos JSON.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="0b4ab-302">Ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b4ab-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="0b4ab-303">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="0b4ab-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="0b4ab-304">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="0b4ab-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="0b4ab-305">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b4ab-305">Next steps</span></span>
- <span data-ttu-id="0b4ab-306">Hola de uso [API de búsqueda de registros](log-analytics-log-search-api.md) tooretrieve datos del repositorio de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b4ab-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
