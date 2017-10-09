---
title: "aaaStream Lake almacén resultado del análisis de datos | Documentos de Microsoft"
description: "Configuración de la autenticación y la autorización de un Almacén de Azure Data Lake en un trabajo de Análisis de transmisiones"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="4b92a-103">Salida de los Análisis de transmisiones del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="4b92a-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="4b92a-104">Los trabajos de Análisis de transmisiones admiten varios métodos de salida, y uno de ellos es el [Almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="4b92a-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="4b92a-105">El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="4b92a-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="4b92a-106">Almacén de Data Lake permite toostore datos de cualquier tamaño, el tipo y la ingesta de velocidad para análisis operativos y exploratorios.</span><span class="sxs-lookup"><span data-stu-id="4b92a-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="4b92a-107">Autorización de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="4b92a-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="4b92a-108">Cuando se selecciona el almacén de Data Lake como una salida en hello portal de Azure, se le pedirá tooauthorize uso del almacén de Data Lake existente o toorequest acceso toohello de almacén de Data Lake a través de hello Portal clásico.</span><span class="sxs-lookup"><span data-stu-id="4b92a-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="4b92a-109">Si ya tiene acceso tooData Lake almacén, haga clic en "Autorizar ahora" y de un breve período de tiempo una página mostrará que indica "Redirigir tooauthorization".</span><span class="sxs-lookup"><span data-stu-id="4b92a-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="4b92a-110">página de Hola se cerrará automáticamente y aparecerá con la página de Hola que permitiría tooconfigure Hola almacén de Data Lake salida.</span><span class="sxs-lookup"><span data-stu-id="4b92a-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="4b92a-111">Si no se ha registrado para el almacén de Data Lake, puede seguir solicitud Hola de tooinitiate de "Sign up now" de vínculo de Hola o siga hello [obtener instrucciones iniciadas](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b92a-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="4b92a-112">Configurar las propiedades de salida de almacén de Data Lake Hola</span><span class="sxs-lookup"><span data-stu-id="4b92a-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="4b92a-113">Una vez que tenga cuenta de almacén de Data Lake Hola autenticado, puede configurar propiedades de hello para la salida de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4b92a-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="4b92a-114">Hola tabla es la lista de Hola de nombres de propiedad y su tooconfigure de descripción de la salida de su almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4b92a-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="4b92a-115"><B>NOMBRE DE LA PROPIEDAD</B></span><span class="sxs-lookup"><span data-stu-id="4b92a-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="4b92a-116"><B>DESCRIPCIÓN</B></span><span class="sxs-lookup"><span data-stu-id="4b92a-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-117">Alias de salida</span><span class="sxs-lookup"><span data-stu-id="4b92a-117">Output Alias</span></span></td>
<td><span data-ttu-id="4b92a-118">Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4b92a-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-119">Cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="4b92a-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="4b92a-120">nombre de Hola de cuenta de almacenamiento de Hola donde va a enviar el resultado.</span><span class="sxs-lookup"><span data-stu-id="4b92a-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="4b92a-121">Aparecerá una lista de cuentas de almacén de Data Lake Hola usuario registrado tenga acceso a.</span><span class="sxs-lookup"><span data-stu-id="4b92a-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-122">Patrón de prefijo de la ruta [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="4b92a-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="4b92a-123">Hola toowrite de ruta de archivo especifican de los archivos dentro de hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4b92a-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="4b92a-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="4b92a-124">{date}, {time}</span></span><BR><span data-ttu-id="4b92a-125">Ejemplo 1: carpeta1/registros/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="4b92a-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="4b92a-126">Ejemplo 2: carpeta1/registros/{date}</span><span class="sxs-lookup"><span data-stu-id="4b92a-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-127">Formato de fecha [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="4b92a-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="4b92a-128">Si el token de fecha de Hola se usa en la ruta de acceso de prefijo de hello, puede seleccionar formato de fecha de hello en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="4b92a-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="4b92a-129">Ejemplo: AAAA/MM/DD</span><span class="sxs-lookup"><span data-stu-id="4b92a-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-130">Formato de hora [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="4b92a-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="4b92a-131">Si el token de tiempo de Hola se usa en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="4b92a-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="4b92a-132">Actualmente, el valor de hello solo admitido es HH.</span><span class="sxs-lookup"><span data-stu-id="4b92a-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-133">Formato de serialización de eventos</span><span class="sxs-lookup"><span data-stu-id="4b92a-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="4b92a-134">Formato de serialización para los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="4b92a-134">Serialization format for output data.</span></span> <span data-ttu-id="4b92a-135">Se admiten JSON, CSV y Avro.</span><span class="sxs-lookup"><span data-stu-id="4b92a-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-136">Codificación</span><span class="sxs-lookup"><span data-stu-id="4b92a-136">Encoding</span></span></td>
<td><span data-ttu-id="4b92a-137">Si el formato CSV o JSON, debe especificarse una codificación.</span><span class="sxs-lookup"><span data-stu-id="4b92a-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="4b92a-138">UTF-8 es Hola solo admite el formato de codificación en este momento.</span><span class="sxs-lookup"><span data-stu-id="4b92a-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-139">Delimitador</span><span class="sxs-lookup"><span data-stu-id="4b92a-139">Delimiter</span></span></td>
<td><span data-ttu-id="4b92a-140">Solo se aplica para la serialización de CSV.</span><span class="sxs-lookup"><span data-stu-id="4b92a-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="4b92a-141">Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos CSV.</span><span class="sxs-lookup"><span data-stu-id="4b92a-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="4b92a-142">Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical.</span><span class="sxs-lookup"><span data-stu-id="4b92a-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4b92a-143">Formato</span><span class="sxs-lookup"><span data-stu-id="4b92a-143">Format</span></span></td>
<td><span data-ttu-id="4b92a-144">Solo se aplica para la serialización de JSON.</span><span class="sxs-lookup"><span data-stu-id="4b92a-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="4b92a-145">Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea.</span><span class="sxs-lookup"><span data-stu-id="4b92a-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="4b92a-146">Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="4b92a-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="4b92a-147">Renovación de la autorización del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="4b92a-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="4b92a-148">Actualmente, hay una limitación donde el token de autenticación de hello necesita toobe actualizar manualmente cada 90 días para todos los trabajos con salida de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4b92a-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="4b92a-149">También necesitará toore-autenticar la cuenta de almacén de Data Lake si ha cambiado la contraseña ya que el trabajo se creó o autenticado por última vez.</span><span class="sxs-lookup"><span data-stu-id="4b92a-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="4b92a-150">Un síntoma de este problema es ninguna salida de trabajo y un error en los registros de operaciones de Hola que indica la necesidad de autorización nuevo.</span><span class="sxs-lookup"><span data-stu-id="4b92a-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="4b92a-151">tooresolve este problema, detenga el trabajo en ejecución y vaya tooyour almacén de Data Lake de salida.</span><span class="sxs-lookup"><span data-stu-id="4b92a-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="4b92a-152">Haga clic en el vínculo de "Autorización Renew" Hola y durante un breve tiempo una página mostrará que indica "Redirigir tooauthorization..".</span><span class="sxs-lookup"><span data-stu-id="4b92a-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="4b92a-153">página de Hola se cerrará automáticamente y si se realiza correctamente, se indicará "Autorización renovada correctamente".</span><span class="sxs-lookup"><span data-stu-id="4b92a-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="4b92a-154">A continuación, necesita tooclick "Guardar" final Hola de página de Hola y puede continuar, reinicie el trabajo de hello pérdida de datos de tooavoid de última hora de detención.</span><span class="sxs-lookup"><span data-stu-id="4b92a-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

