---
title: Salida de Stream Analytics Data Lake Store | Microsoft Docs
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
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="0b5b8-103">Salida de los Análisis de transmisiones del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b5b8-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="0b5b8-104">Los trabajos de Análisis de transmisiones admiten varios métodos de salida, y uno de ellos es el [Almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="0b5b8-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="0b5b8-105">El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="0b5b8-106">El Almacén de Data Lake permite almacenar datos de cualquier tamaño, tipo y velocidad de ingesta para realizar análisis exploratorios y operativos.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="0b5b8-107">Autorización de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b5b8-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="0b5b8-108">Cuando se selecciona Data Lake Store como una salida en Azure Portal, se le pedirá que autorice el uso de la instancia de Data Lake Store existente o pida acceso a Data Lake Store mediante el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="0b5b8-109">Si ya dispone de acceso a Data Lake Store, haga clic en "Autorizar ahora" y, durante unos segundos, se mostrará una página con el mensaje "Redirigiendo a la autorización...".</span><span class="sxs-lookup"><span data-stu-id="0b5b8-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="0b5b8-110">Esta página se cerrará automáticamente y se le mostrará la página donde podrá configurar la salida del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="0b5b8-111">Si no se registró en Data Lake Store, puede hacer clic en el vínculo "Suscribirme ahora" para iniciar la solicitud, o bien siga las [instrucciones de introducción](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b5b8-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="0b5b8-112">Configuración de las propiedades de salida del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b5b8-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="0b5b8-113">Una vez que se haya autenticado la cuenta del Almacén de Data Lake, podrá configurar las propiedades para su salida del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="0b5b8-114">En la siguiente tabla podrá encontrar una lista de nombres de propiedades y su descripción para configurar la salida del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="0b5b8-115"><B>NOMBRE DE LA PROPIEDAD</B></span><span class="sxs-lookup"><span data-stu-id="0b5b8-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="0b5b8-116"><B>DESCRIPCIÓN</B></span><span class="sxs-lookup"><span data-stu-id="0b5b8-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-117">Alias de salida</span><span class="sxs-lookup"><span data-stu-id="0b5b8-117">Output Alias</span></span></td>
<td><span data-ttu-id="0b5b8-118">Se trata de un nombre descriptivo utilizado en las consultas para dirigir la salida de la consulta a este Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-119">Cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b5b8-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="0b5b8-120">El nombre de la cuenta de almacenamiento a donde está enviando la salida</span><span class="sxs-lookup"><span data-stu-id="0b5b8-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="0b5b8-121">Aparecerá una lista de cuentas de almacén de Data Lake Store a que el usuario que ha iniciado sesión tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-122">Patrón de prefijo de la ruta [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0b5b8-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0b5b8-123">La ruta de acceso utilizada para escribir sus archivos en la cuenta del Almacén de Data Lake especificada.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="0b5b8-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="0b5b8-124">{date}, {time}</span></span><BR><span data-ttu-id="0b5b8-125">Ejemplo 1: carpeta1/registros/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="0b5b8-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="0b5b8-126">Ejemplo 2: carpeta1/registros/{date}</span><span class="sxs-lookup"><span data-stu-id="0b5b8-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-127">Formato de fecha [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0b5b8-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0b5b8-128">Si el token de fecha se usa en la ruta de acceso de prefijo, puede seleccionar el formato de fecha en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="0b5b8-129">Ejemplo: AAAA/MM/DD</span><span class="sxs-lookup"><span data-stu-id="0b5b8-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-130">Formato de hora [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0b5b8-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0b5b8-131">Si el token de hora se usa en la ruta de acceso de prefijo, puede seleccionar el formato de hora en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="0b5b8-132">Actualmente, el único valor admitido es HH.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-133">Formato de serialización de eventos</span><span class="sxs-lookup"><span data-stu-id="0b5b8-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="0b5b8-134">Formato de serialización para los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-134">Serialization format for output data.</span></span> <span data-ttu-id="0b5b8-135">Se admiten JSON, CSV y Avro.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-136">Codificación</span><span class="sxs-lookup"><span data-stu-id="0b5b8-136">Encoding</span></span></td>
<td><span data-ttu-id="0b5b8-137">Si el formato CSV o JSON, debe especificarse una codificación.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="0b5b8-138">Por el momento, UTF-8 es el único formato de codificación compatible.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-139">Delimitador</span><span class="sxs-lookup"><span data-stu-id="0b5b8-139">Delimiter</span></span></td>
<td><span data-ttu-id="0b5b8-140">Solo se aplica para la serialización de CSV.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="0b5b8-141">Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos CSV.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="0b5b8-142">Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0b5b8-143">Formato</span><span class="sxs-lookup"><span data-stu-id="0b5b8-143">Format</span></span></td>
<td><span data-ttu-id="0b5b8-144">Solo se aplica para la serialización de JSON.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="0b5b8-145">Separado por líneas especifica que la salida se formateará de tal forma que cada objeto JSON esté separado por una línea nueva.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="0b5b8-146">Matriz especifica que la salida se formateará como una matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="0b5b8-147">Renovación de la autorización del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b5b8-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="0b5b8-148">Actualmente, existe una limitación según la que el token de autenticación debe actualizarse manualmente cada 90 días para todos los trabajos con salida del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="0b5b8-149">También tendrá que volver a autenticar la cuenta del Almacén de Data Lake si ha cambiado la contraseña desde que se creó o autenticó por última vez su trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="0b5b8-150">Un síntoma de este problema es la ausencia de salidas de trabajos y un error en los registros de operaciones en el que se indica que se debe volver a conceder la autorización.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="0b5b8-151">Para resolver este problema, detenga su trabajo en ejecución y vaya a la salida del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="0b5b8-152">Haga clic en el vínculo “Renovar autorización” y, durante unos segundos, se mostrará una página con el mensaje “Redirigiendo a la autorización...”.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="0b5b8-153">La página se cerrará automáticamente y, si la operación se realiza correctamente, indicará “La autorización se ha renovado correctamente”.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="0b5b8-154">Después, debe hacer clic en “Guardar” en la parte inferior de la página y podrá continuar reiniciando el trabajo desde la hora de la última detención para evitar la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="0b5b8-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

