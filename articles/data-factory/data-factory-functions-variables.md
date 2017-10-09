---
title: aaaData generador de funciones y Variables del sistema | Documentos de Microsoft
description: Proporciona una lista de funciones y variables del sistema de Azure Data Factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="50307-103">Azure Data Factory: funciones y variables del sistema</span><span class="sxs-lookup"><span data-stu-id="50307-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="50307-104">Este artículo proporciona información sobre las funciones y las variables compatibles con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="50307-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="50307-105">Variables del sistema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="50307-105">Data Factory system variables</span></span>
| <span data-ttu-id="50307-106">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="50307-106">Variable Name</span></span> | <span data-ttu-id="50307-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="50307-107">Description</span></span> | <span data-ttu-id="50307-108">Ámbito del objeto</span><span class="sxs-lookup"><span data-stu-id="50307-108">Object Scope</span></span> | <span data-ttu-id="50307-109">Ámbito JSON y casos de uso</span><span class="sxs-lookup"><span data-stu-id="50307-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50307-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="50307-110">WindowStart</span></span> |<span data-ttu-id="50307-111">Inicio del intervalo de tiempo para la ventana de ejecución de la actividad actual</span><span class="sxs-lookup"><span data-stu-id="50307-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="50307-112">activity</span><span class="sxs-lookup"><span data-stu-id="50307-112">activity</span></span> |<ol><li><span data-ttu-id="50307-113">Especifique las consultas de selección de datos.</span><span class="sxs-lookup"><span data-stu-id="50307-113">Specify data selection queries.</span></span> <span data-ttu-id="50307-114">Consulte los artículos de conector que se hace referencia en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="50307-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="50307-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="50307-115">WindowEnd</span></span> |<span data-ttu-id="50307-116">Final del intervalo de tiempo para la ventana de ejecución de actividad actual</span><span class="sxs-lookup"><span data-stu-id="50307-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="50307-117">activity</span><span class="sxs-lookup"><span data-stu-id="50307-117">activity</span></span> |<span data-ttu-id="50307-118">igual que WindowStart.</span><span class="sxs-lookup"><span data-stu-id="50307-118">same as WindowStart.</span></span> |
| <span data-ttu-id="50307-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="50307-119">SliceStart</span></span> |<span data-ttu-id="50307-120">Inicio del intervalo de tiempo para el segmento de datos que se está generando</span><span class="sxs-lookup"><span data-stu-id="50307-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="50307-121">activity</span><span class="sxs-lookup"><span data-stu-id="50307-121">activity</span></span><br/><span data-ttu-id="50307-122">dataset</span><span class="sxs-lookup"><span data-stu-id="50307-122">dataset</span></span> |<ol><li><span data-ttu-id="50307-123">Especifique rutas de acceso dinámicas a carpetas y nombres de archivo mientras trabaja con [Azure Blob](data-factory-azure-blob-connector.md) y [conjuntos de archivos del sistema de archivos](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="50307-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="50307-124">Especifique las dependencias de entrada con funciones de factoría de datos en la colección de entradas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="50307-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="50307-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="50307-125">SliceEnd</span></span> |<span data-ttu-id="50307-126">Fin del intervalo de tiempo del segmento de datos actual.</span><span class="sxs-lookup"><span data-stu-id="50307-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="50307-127">activity</span><span class="sxs-lookup"><span data-stu-id="50307-127">activity</span></span><br/><span data-ttu-id="50307-128">dataset</span><span class="sxs-lookup"><span data-stu-id="50307-128">dataset</span></span> |<span data-ttu-id="50307-129">igual que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="50307-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="50307-130">En la actualidad factoría de datos requiere ese Hola programar Hola especificado en actividad coincide exactamente con programación de hello especificada en la disponibilidad del conjunto de datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="50307-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="50307-131">Por lo tanto, WindowStart, WindowEnd y SliceStart y SliceEnd siempre asignan toohello mismo tiempo período y un segmento de salida único.</span><span class="sxs-lookup"><span data-stu-id="50307-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="50307-132">Ejemplo de uso de una variable del sistema</span><span class="sxs-lookup"><span data-stu-id="50307-132">Example for using a system variable</span></span>
<span data-ttu-id="50307-133">Hola siguiente ejemplo, año, mes, día y hora de **SliceStart** se extraen en variables independientes que usan **folderPath** y **fileName** propiedades.</span><span class="sxs-lookup"><span data-stu-id="50307-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="50307-134">Funciones de Data Factory</span><span class="sxs-lookup"><span data-stu-id="50307-134">Data Factory functions</span></span>
<span data-ttu-id="50307-135">Puede utilizar funciones de factoría de datos junto con las variables del sistema para hello siguientes fines:</span><span class="sxs-lookup"><span data-stu-id="50307-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="50307-136">Especificar las consultas de selección de datos (consulte los artículos de conector al que hace referencia hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="50307-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="50307-137">Hola tooinvoke de sintaxis es una función de la factoría de datos:  **$$ <function>**  para las consultas de selección de datos y otras propiedades en la actividad hello y conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="50307-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="50307-138">Especifique las dependencias de entrada con funciones de factoría de datos en la colección de entradas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="50307-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="50307-139">$$ no es necesario para especificar expresiones de dependencia de entrada.</span><span class="sxs-lookup"><span data-stu-id="50307-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="50307-140">Hola según muestra, **sqlReaderQuery** propiedad en un archivo JSON se asigna el valor tooa devolviendo hello `Text.Format` función.</span><span class="sxs-lookup"><span data-stu-id="50307-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="50307-141">Este ejemplo también utiliza una variable del sistema denominada **WindowStart**, que representa la hora de inicio de Hola de ventana de la ejecución de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="50307-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="50307-142">Consulte el tema [Cadenas con formato de fecha y hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx), en el que se describen las diferentes opciones de formato que puede usar (por ejemplo: aa frente a aaaa).</span><span class="sxs-lookup"><span data-stu-id="50307-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="50307-143">Functions</span><span class="sxs-lookup"><span data-stu-id="50307-143">Functions</span></span>
<span data-ttu-id="50307-144">Hola las tablas siguientes enumeran todas las funciones de hello en Data Factory de Azure:</span><span class="sxs-lookup"><span data-stu-id="50307-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="50307-145">Categoría</span><span class="sxs-lookup"><span data-stu-id="50307-145">Category</span></span> | <span data-ttu-id="50307-146">Función</span><span class="sxs-lookup"><span data-stu-id="50307-146">Function</span></span> | <span data-ttu-id="50307-147">Parámetros</span><span class="sxs-lookup"><span data-stu-id="50307-147">Parameters</span></span> | <span data-ttu-id="50307-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="50307-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50307-149">Hora</span><span class="sxs-lookup"><span data-stu-id="50307-149">Time</span></span> |<span data-ttu-id="50307-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-150">AddHours(X,Y)</span></span> |<span data-ttu-id="50307-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="50307-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-152">Y: int</span></span> |<span data-ttu-id="50307-153">Agrega Y horas toohello X momento dado.</span><span class="sxs-lookup"><span data-stu-id="50307-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="50307-154">Ejemplo: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="50307-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="50307-155">Hora</span><span class="sxs-lookup"><span data-stu-id="50307-155">Time</span></span> |<span data-ttu-id="50307-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="50307-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="50307-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-158">Y: int</span></span> |<span data-ttu-id="50307-159">Agrega Y minutos tooX.</span><span class="sxs-lookup"><span data-stu-id="50307-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="50307-160">Ejemplo: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="50307-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="50307-161">Hora</span><span class="sxs-lookup"><span data-stu-id="50307-161">Time</span></span> |<span data-ttu-id="50307-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="50307-162">StartOfHour(X)</span></span> |<span data-ttu-id="50307-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-163">X: Datetime</span></span> |<span data-ttu-id="50307-164">Obtiene Hola hora de inicio de hora de hello representada por el componente de hora de Hola de X.</span><span class="sxs-lookup"><span data-stu-id="50307-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="50307-165">Ejemplo: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="50307-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="50307-166">Date</span><span class="sxs-lookup"><span data-stu-id="50307-166">Date</span></span> |<span data-ttu-id="50307-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-167">AddDays(X,Y)</span></span> |<span data-ttu-id="50307-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-168">X: DateTime</span></span><br/><br/><span data-ttu-id="50307-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-169">Y: int</span></span> |<span data-ttu-id="50307-170">Agrega Y días tooX.</span><span class="sxs-lookup"><span data-stu-id="50307-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="50307-171">Ejemplo: 9/15/2013 12:00:00 PM + 2 días = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="50307-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="50307-172">También puede restar días especificando Y como un número negativo.</span><span class="sxs-lookup"><span data-stu-id="50307-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="50307-173">Ejemplo: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="50307-174">Date</span><span class="sxs-lookup"><span data-stu-id="50307-174">Date</span></span> |<span data-ttu-id="50307-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="50307-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-176">X: DateTime</span></span><br/><br/><span data-ttu-id="50307-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-177">Y: int</span></span> |<span data-ttu-id="50307-178">Agrega Y meses tooX.</span><span class="sxs-lookup"><span data-stu-id="50307-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="50307-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="50307-180">También puede restar meses especificando Y como un número negativo.</span><span class="sxs-lookup"><span data-stu-id="50307-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="50307-181">Ejemplo: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="50307-182">Date</span><span class="sxs-lookup"><span data-stu-id="50307-182">Date</span></span> |<span data-ttu-id="50307-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="50307-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="50307-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-185">Y: int</span></span> |<span data-ttu-id="50307-186">Suma Y * 3 meses tooX.</span><span class="sxs-lookup"><span data-stu-id="50307-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="50307-187">Ejemplo: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="50307-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="50307-188">Date</span><span class="sxs-lookup"><span data-stu-id="50307-188">Date</span></span> |<span data-ttu-id="50307-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="50307-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-190">X: DateTime</span></span><br/><br/><span data-ttu-id="50307-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-191">Y: int</span></span> |<span data-ttu-id="50307-192">Suma Y * tooX de 7 días</span><span class="sxs-lookup"><span data-stu-id="50307-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="50307-193">Ejemplo: 9/15/2013 12:00:00 PM + 1 semana = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="50307-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="50307-194">También puede restar semanas especificando Y como un número negativo.</span><span class="sxs-lookup"><span data-stu-id="50307-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="50307-195">Ejemplo: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="50307-196">Date</span><span class="sxs-lookup"><span data-stu-id="50307-196">Date</span></span> |<span data-ttu-id="50307-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="50307-197">AddYears(X,Y)</span></span> |<span data-ttu-id="50307-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-198">X: DateTime</span></span><br/><br/><span data-ttu-id="50307-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="50307-199">Y: int</span></span> |<span data-ttu-id="50307-200">Agrega Y años tooX.</span><span class="sxs-lookup"><span data-stu-id="50307-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="50307-201">También puede restar años especificando Y como un número negativo.</span><span class="sxs-lookup"><span data-stu-id="50307-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="50307-202">Ejemplo: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="50307-203">Date</span><span class="sxs-lookup"><span data-stu-id="50307-203">Date</span></span> |<span data-ttu-id="50307-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="50307-204">Day(X)</span></span> |<span data-ttu-id="50307-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-205">X: DateTime</span></span> |<span data-ttu-id="50307-206">Obtiene el componente de día de Hola de X.</span><span class="sxs-lookup"><span data-stu-id="50307-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="50307-207">Ejemplo: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="50307-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="50307-208">Date</span><span class="sxs-lookup"><span data-stu-id="50307-208">Date</span></span> |<span data-ttu-id="50307-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="50307-209">DayOfWeek(X)</span></span> |<span data-ttu-id="50307-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-210">X: DateTime</span></span> |<span data-ttu-id="50307-211">Obtiene el día de hello del componente de la semana de X.</span><span class="sxs-lookup"><span data-stu-id="50307-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="50307-212">Ejemplo: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="50307-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="50307-213">Date</span><span class="sxs-lookup"><span data-stu-id="50307-213">Date</span></span> |<span data-ttu-id="50307-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="50307-214">DayOfYear(X)</span></span> |<span data-ttu-id="50307-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-215">X: DateTime</span></span> |<span data-ttu-id="50307-216">Obtiene el día de hello en el año de hello representado por el componente correspondiente al año Hola de X.</span><span class="sxs-lookup"><span data-stu-id="50307-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="50307-217">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="50307-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="50307-218">Date</span><span class="sxs-lookup"><span data-stu-id="50307-218">Date</span></span> |<span data-ttu-id="50307-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="50307-219">DaysInMonth(X)</span></span> |<span data-ttu-id="50307-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-220">X: DateTime</span></span> |<span data-ttu-id="50307-221">Obtiene los días de hello en mes Hola representado por el componente de mes de hello del parámetro X.</span><span class="sxs-lookup"><span data-stu-id="50307-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="50307-222">Ejemplo: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="50307-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="50307-223">Date</span><span class="sxs-lookup"><span data-stu-id="50307-223">Date</span></span> |<span data-ttu-id="50307-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="50307-224">EndOfDay(X)</span></span> |<span data-ttu-id="50307-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-225">X: DateTime</span></span> |<span data-ttu-id="50307-226">Obtiene la fecha y hora de Hola que representa el final de Hola de hello día (componente de día) de X.</span><span class="sxs-lookup"><span data-stu-id="50307-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="50307-227">Ejemplo: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="50307-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="50307-228">Date</span><span class="sxs-lookup"><span data-stu-id="50307-228">Date</span></span> |<span data-ttu-id="50307-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="50307-229">EndOfMonth(X)</span></span> |<span data-ttu-id="50307-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-230">X: DateTime</span></span> |<span data-ttu-id="50307-231">Obtiene Hola final del mes de hello representado por el componente de mes del parámetro X.</span><span class="sxs-lookup"><span data-stu-id="50307-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="50307-232">Ejemplo: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (fecha y hora que representa Hola final del mes de septiembre)</span><span class="sxs-lookup"><span data-stu-id="50307-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="50307-233">Date</span><span class="sxs-lookup"><span data-stu-id="50307-233">Date</span></span> |<span data-ttu-id="50307-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="50307-234">StartOfDay(X)</span></span> |<span data-ttu-id="50307-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-235">X: DateTime</span></span> |<span data-ttu-id="50307-236">Obtiene Hola inicio del día de hello representado por el componente de día de hello del parámetro X.</span><span class="sxs-lookup"><span data-stu-id="50307-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="50307-237">Ejemplo: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="50307-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="50307-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="50307-238">DateTime</span></span> |<span data-ttu-id="50307-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="50307-239">From(X)</span></span> |<span data-ttu-id="50307-240">X: String</span><span class="sxs-lookup"><span data-stu-id="50307-240">X: String</span></span> |<span data-ttu-id="50307-241">Analizar la cadena X tooa fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="50307-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="50307-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="50307-242">DateTime</span></span> |<span data-ttu-id="50307-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="50307-243">Ticks(X)</span></span> |<span data-ttu-id="50307-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="50307-244">X: DateTime</span></span> |<span data-ttu-id="50307-245">Obtiene propiedad del parámetro hello X de tics de Hola. Un TIC es igual a 100 nanosegundos.</span><span class="sxs-lookup"><span data-stu-id="50307-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="50307-246">valor de Hola de esta propiedad representa número de Hola de pasos que han transcurrido desde medianoche de 12:00:00 del 1 de enero de 0001.</span><span class="sxs-lookup"><span data-stu-id="50307-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="50307-247">Texto</span><span class="sxs-lookup"><span data-stu-id="50307-247">Text</span></span> |<span data-ttu-id="50307-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="50307-248">Format(X)</span></span> |<span data-ttu-id="50307-249">X: String variable</span><span class="sxs-lookup"><span data-stu-id="50307-249">X: String variable</span></span> |<span data-ttu-id="50307-250">Hola de formatos de texto (usar `\\'` tooescape de combinación `'` caracteres).</span><span class="sxs-lookup"><span data-stu-id="50307-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="50307-251">Cuando se usa una función dentro de otra función, no es necesario toouse  **$$**  prefijo de función interna de Hola.</span><span class="sxs-lookup"><span data-stu-id="50307-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="50307-252">Por ejemplo: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' y RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="50307-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="50307-253">En este ejemplo, observe que  **$$**  prefijo no se utiliza para hello **Time.AddHours** (función).</span><span class="sxs-lookup"><span data-stu-id="50307-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="50307-254">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="50307-254">Example</span></span>
<span data-ttu-id="50307-255">Hola parámetros de entrada y salida de ejemplo siguientes para la actividad de Hive Hola se determinan mediante hello `Text.Format` funciones y variables de sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="50307-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="50307-256">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="50307-256">Example 2</span></span>

<span data-ttu-id="50307-257">En el siguiente ejemplo de Hola Hola Hola que actividad de procedimiento almacenado se determina mediante el texto hello en el parámetro DateTime.</span><span class="sxs-lookup"><span data-stu-id="50307-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="50307-258">Función de formato y Hola SliceStart variable.</span><span class="sxs-lookup"><span data-stu-id="50307-258">Format function and hello SliceStart variable.</span></span> 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="50307-259">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="50307-259">Example 3</span></span>
<span data-ttu-id="50307-260">tooread datos del día anterior en lugar de días representado por hello SliceStart, utilice la función de AddDays de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="50307-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="50307-261">Consulte el tema [Cadenas con formato de fecha y hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx), en el que se describen las diferentes opciones de formato que puede usar (por ejemplo: aa frente a aaaa).</span><span class="sxs-lookup"><span data-stu-id="50307-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

