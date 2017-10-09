---
title: "formatos de compresión y aaaFile de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los formatos de archivo de hello compatibles con Data Factory de Azure."
keywords: datos de blob, copia de blobs de azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="0de8e-104">Formatos de compresión de archivos admitidos por Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0de8e-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="0de8e-105">*Este tema aplica después de conectores de toohello: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [almacén de Azure Data Lake](data-factory-azure-datalake-connector.md), [sistema de archivos](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), y [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="0de8e-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="0de8e-106">Factoría de datos de Azure admite Hola siguientes tipos de formato de archivo:</span><span class="sxs-lookup"><span data-stu-id="0de8e-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="0de8e-107">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="0de8e-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="0de8e-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="0de8e-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="0de8e-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="0de8e-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="0de8e-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="0de8e-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="0de8e-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="0de8e-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="0de8e-112">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="0de8e-112">Text format</span></span>
<span data-ttu-id="0de8e-113">Si desea obtener tooread desde un archivo de texto o escribir en el archivo de texto tooa, establezca hello `type` propiedad Hola `format` sección del conjunto de datos de hello demasiado**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="0de8e-114">También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección.</span><span class="sxs-lookup"><span data-stu-id="0de8e-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="0de8e-115">Vea [ejemplo TextFormat](#textformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="0de8e-116">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0de8e-116">Property</span></span> | <span data-ttu-id="0de8e-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="0de8e-117">Description</span></span> | <span data-ttu-id="0de8e-118">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0de8e-118">Allowed values</span></span> | <span data-ttu-id="0de8e-119">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0de8e-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0de8e-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="0de8e-120">columnDelimiter</span></span> |<span data-ttu-id="0de8e-121">carácter de Hello usa tooseparate columnas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0de8e-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="0de8e-122">Puede considerar toouse char no pueden imprimirse poco frecuente que puede no es probable que existe en los datos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="0de8e-123">Por ejemplo, especifique "\u0001", que representa el inicio de encabezado (SOH).</span><span class="sxs-lookup"><span data-stu-id="0de8e-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="0de8e-124">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="0de8e-124">Only one character is allowed.</span></span> <span data-ttu-id="0de8e-125">Hola **predeterminado** valor es **coma (',')**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="0de8e-126">toouse un carácter Unicode, consulte demasiado[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Hola código correspondiente para ella.</span><span class="sxs-lookup"><span data-stu-id="0de8e-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="0de8e-127">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-127">No</span></span> |
| <span data-ttu-id="0de8e-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="0de8e-128">rowDelimiter</span></span> |<span data-ttu-id="0de8e-129">carácter de Hello usa tooseparate filas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0de8e-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="0de8e-130">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="0de8e-130">Only one character is allowed.</span></span> <span data-ttu-id="0de8e-131">Hola **predeterminado** valor es uno de los siguiente valores de lectura de Hola: **["\r\n", "\r", "\n"]** y **"\r\n"** durante la escritura.</span><span class="sxs-lookup"><span data-stu-id="0de8e-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="0de8e-132">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-132">No</span></span> |
| <span data-ttu-id="0de8e-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="0de8e-133">escapeChar</span></span> |<span data-ttu-id="0de8e-134">caracteres especiales de Hello utilizan tooescape un delimitador de columna en el contenido de hello del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="0de8e-135">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="0de8e-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="0de8e-136">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="0de8e-136">Only one character is allowed.</span></span> <span data-ttu-id="0de8e-137">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-137">No default value.</span></span> <br/><br/><span data-ttu-id="0de8e-138">Ejemplo: Si tienes por comas (', ') como delimitador de columna Hola pero desea toohave carácter de coma hello en texto hello (ejemplo: "Hello, world"), puede definir "$" como carácter de escape de Hola y utilizar la cadena "Hello$, world" en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="0de8e-139">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-139">No</span></span> |
| <span data-ttu-id="0de8e-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="0de8e-140">quoteChar</span></span> |<span data-ttu-id="0de8e-141">carácter de Hello usa tooquote un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="0de8e-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="0de8e-142">delimitadores de fila y columna de Hello dentro de los caracteres de comillas Hola se trataría como parte del valor de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="0de8e-143">Esta propiedad es aplicable tooboth entrada y salida de los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="0de8e-144">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="0de8e-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="0de8e-145">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="0de8e-145">Only one character is allowed.</span></span> <span data-ttu-id="0de8e-146">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-146">No default value.</span></span> <br/><br/><span data-ttu-id="0de8e-147">Por ejemplo, si tienes coma (', ') como delimitador de columna Hola pero desea toohave coma en texto hello (ejemplo: < Hola, mundo >), puede definir "(comillas dobles) como Hola delimitar caracteres y usar cadena de Hola"Hola, mundo"en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="0de8e-148">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-148">No</span></span> |
| <span data-ttu-id="0de8e-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="0de8e-149">nullValue</span></span> |<span data-ttu-id="0de8e-150">Uno o más caracteres utilizan toorepresent un valor null.</span><span class="sxs-lookup"><span data-stu-id="0de8e-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="0de8e-151">Uno o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="0de8e-151">One or more characters.</span></span> <span data-ttu-id="0de8e-152">Hola **predeterminado** valores son **"\N" y "NULL"** en lectura y **"\N"** durante la escritura.</span><span class="sxs-lookup"><span data-stu-id="0de8e-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="0de8e-153">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-153">No</span></span> |
| <span data-ttu-id="0de8e-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="0de8e-154">encodingName</span></span> |<span data-ttu-id="0de8e-155">Especifique el nombre de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-155">Specify hello encoding name.</span></span> |<span data-ttu-id="0de8e-156">Un nombre de codificación válido.</span><span class="sxs-lookup"><span data-stu-id="0de8e-156">A valid encoding name.</span></span> <span data-ttu-id="0de8e-157">Consulte la [propiedad Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="0de8e-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="0de8e-158">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="0de8e-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="0de8e-159">Hola **predeterminado** valor es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="0de8e-160">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-160">No</span></span> |
| <span data-ttu-id="0de8e-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="0de8e-161">firstRowAsHeader</span></span> |<span data-ttu-id="0de8e-162">Especifica si tooconsider Hola la primera fila como un encabezado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="0de8e-163">Para un conjunto de datos de entrada, Data Factory lee la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="0de8e-164">Para un conjunto de datos de salida, Data Factory escribe la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="0de8e-165">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="0de8e-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="0de8e-166">True</span><span class="sxs-lookup"><span data-stu-id="0de8e-166">True</span></span><br/><span data-ttu-id="0de8e-167"><b>False (valor predeterminado)</b></span><span class="sxs-lookup"><span data-stu-id="0de8e-167"><b>False (default)</b></span></span> |<span data-ttu-id="0de8e-168">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-168">No</span></span> |
| <span data-ttu-id="0de8e-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="0de8e-169">skipLineCount</span></span> |<span data-ttu-id="0de8e-170">Indica el número de Hola de filas tooskip al leer los datos de archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="0de8e-171">Si se especifican skipLineCount y firstRowAsHeader, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="0de8e-172">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="0de8e-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="0de8e-173">Entero</span><span class="sxs-lookup"><span data-stu-id="0de8e-173">Integer</span></span> |<span data-ttu-id="0de8e-174">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-174">No</span></span> |
| <span data-ttu-id="0de8e-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="0de8e-175">treatEmptyAsNull</span></span> |<span data-ttu-id="0de8e-176">Especifica si hay tootreat una cadena nula o vacía como nula valor al leer los datos de un archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="0de8e-177">**True (predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="0de8e-177">**True (default)**</span></span><br/><span data-ttu-id="0de8e-178">False</span><span class="sxs-lookup"><span data-stu-id="0de8e-178">False</span></span> |<span data-ttu-id="0de8e-179">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="0de8e-180">Ejemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="0de8e-180">TextFormat example</span></span>
<span data-ttu-id="0de8e-181">Hola después de la definición de JSON para un conjunto de datos, se especifican algunas de las propiedades opcionales Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="0de8e-182">toouse una `escapeChar` en lugar de `quoteChar`, reemplace la línea hello con `quoteChar` con hello después de escapeChar:</span><span class="sxs-lookup"><span data-stu-id="0de8e-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="0de8e-183">Escenarios de uso de firstRowAsHeader y skipLineCount</span><span class="sxs-lookup"><span data-stu-id="0de8e-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="0de8e-184">Va a copiar de un archivo de texto de origen no es un archivo tooa y desearía tooadd una línea de encabezado que contiene los metadatos del esquema de hello (por ejemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="0de8e-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="0de8e-185">Especificar `firstRowAsHeader` como true en el conjunto de datos de salida de hello para este escenario.</span><span class="sxs-lookup"><span data-stu-id="0de8e-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="0de8e-186">Va a copiar de un archivo de texto que contiene un receptor no es un archivo de encabezado línea tooa y desearía toodrop que línea.</span><span class="sxs-lookup"><span data-stu-id="0de8e-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="0de8e-187">Especificar `firstRowAsHeader` como true en el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="0de8e-188">Va a copiar desde un archivo de texto y desea tooskip unas cuantas líneas al principio de Hola que no contienen ninguna información de datos o de encabezado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="0de8e-189">Especifique `skipLineCount` tooindicate Hola número de líneas toobe omitidos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="0de8e-190">Si el resto de hello del archivo hello contiene una línea de encabezado, también puede especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="0de8e-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="0de8e-191">Si ambos `skipLineCount` y `firstRowAsHeader` se especifican, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada</span><span class="sxs-lookup"><span data-stu-id="0de8e-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="0de8e-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="0de8e-192">JSON format</span></span>
<span data-ttu-id="0de8e-193">demasiado**importación y exportación de un archivo JSON como-está en/desde la base de datos de Azure Cosmos**, vea hello [documentos JSON de importación y exportación de](data-factory-azure-documentdb-connector.md#importexport-json-documents) sección [mover datos hacia y desde la base de datos de Azure Cosmos](data-factory-azure-documentdb-connector.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="0de8e-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="0de8e-194">Si desea tooparse Hola JSON archivos o escribir datos de hello en formato JSON, establezca hello `type` propiedad Hola `format` sección demasiado**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="0de8e-195">También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección.</span><span class="sxs-lookup"><span data-stu-id="0de8e-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="0de8e-196">Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="0de8e-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0de8e-197">Property</span></span> | <span data-ttu-id="0de8e-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="0de8e-198">Description</span></span> | <span data-ttu-id="0de8e-199">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0de8e-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0de8e-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="0de8e-200">filePattern</span></span> |<span data-ttu-id="0de8e-201">Indicar el patrón de Hola de los datos almacenados en cada archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="0de8e-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="0de8e-202">Estos son los valores permitidos: **setOfObjects** y **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="0de8e-203">Hola **predeterminado** valor es **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="0de8e-204">Consulte la sección [patrones de archivo JSON](#json-file-patterns) para obtener más información acerca de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="0de8e-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="0de8e-205">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-205">No</span></span> |
| <span data-ttu-id="0de8e-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="0de8e-206">jsonNodeReference</span></span> | <span data-ttu-id="0de8e-207">Si desea tooiterate y extraer datos de objetos de hello dentro de una matriz de campo con hello mismo patrón, especifique la ruta de acceso de hello JSON de dicha matriz.</span><span class="sxs-lookup"><span data-stu-id="0de8e-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="0de8e-208">Esta propiedad se admite solo cuando se copian datos desde los archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="0de8e-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="0de8e-209">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-209">No</span></span> |
| <span data-ttu-id="0de8e-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="0de8e-210">jsonPathDefinition</span></span> | <span data-ttu-id="0de8e-211">Especifique la expresión de ruta de acceso de hello JSON para cada asignación de columna con un nombre de columna personalizada (comienzan con minúscula).</span><span class="sxs-lookup"><span data-stu-id="0de8e-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="0de8e-212">Esta propiedad se admite solo cuando se copian datos desde archivos JSON y puede extraer datos del objeto o matriz.</span><span class="sxs-lookup"><span data-stu-id="0de8e-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="0de8e-213">Para los campos en el objeto raíz, comenzar por $ de raíz; para los campos dentro de la matriz de hello elegida por `jsonNodeReference` propiedad, inicio de elemento de la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="0de8e-214">Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="0de8e-215">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-215">No</span></span> |
| <span data-ttu-id="0de8e-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="0de8e-216">encodingName</span></span> |<span data-ttu-id="0de8e-217">Especifique el nombre de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-217">Specify hello encoding name.</span></span> <span data-ttu-id="0de8e-218">Para hello lista de nombres de codificación válidos, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propiedad.</span><span class="sxs-lookup"><span data-stu-id="0de8e-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="0de8e-219">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="0de8e-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="0de8e-220">Hola **predeterminado** valor es: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="0de8e-221">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-221">No</span></span> |
| <span data-ttu-id="0de8e-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="0de8e-222">nestingSeparator</span></span> |<span data-ttu-id="0de8e-223">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="0de8e-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="0de8e-224">valor predeterminado de Hello es '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="0de8e-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="0de8e-225">No</span><span class="sxs-lookup"><span data-stu-id="0de8e-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="0de8e-226">Patrones de archivo JSON</span><span class="sxs-lookup"><span data-stu-id="0de8e-226">JSON file patterns</span></span>

<span data-ttu-id="0de8e-227">Actividad de copia puede analizar Hola siguientes patrones de archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="0de8e-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="0de8e-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="0de8e-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="0de8e-229">Cada archivo contiene un único objeto o bien varios objetos concatenados/delimitados por líneas.</span><span class="sxs-lookup"><span data-stu-id="0de8e-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="0de8e-230">Si se elige esta opción en un conjunto de datos de salida, la actividad de copia genera un único archivo JSON con cada objeto por línea (delimitado por líneas).</span><span class="sxs-lookup"><span data-stu-id="0de8e-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="0de8e-231">**ejemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="0de8e-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="0de8e-232">**ejemplo de JSON delimitado por líneas**</span><span class="sxs-lookup"><span data-stu-id="0de8e-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="0de8e-233">**ejemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="0de8e-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="0de8e-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="0de8e-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="0de8e-235">Cada archivo contiene una matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="0de8e-236">Ejemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="0de8e-236">JsonFormat example</span></span>

<span data-ttu-id="0de8e-237">**Caso 1: Copia de datos desde archivos JSON**</span><span class="sxs-lookup"><span data-stu-id="0de8e-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="0de8e-238">Vea Hola siguiendo dos muestras cuando se copian datos desde archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="0de8e-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="0de8e-239">Hola toonote puntos genérico:</span><span class="sxs-lookup"><span data-stu-id="0de8e-239">hello generic points toonote:</span></span>

<span data-ttu-id="0de8e-240">**Ejemplo 1: extracción de datos de objeto y matriz**</span><span class="sxs-lookup"><span data-stu-id="0de8e-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="0de8e-241">En este ejemplo, espera un objeto JSON de raíz asigna el registro de toosingle de resultados tabulares.</span><span class="sxs-lookup"><span data-stu-id="0de8e-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="0de8e-242">Si tiene un archivo JSON con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="0de8e-242">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="0de8e-243">y desea que toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, extrayendo datos de objeto y matriz:</span><span class="sxs-lookup"><span data-stu-id="0de8e-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="0de8e-244">id</span><span class="sxs-lookup"><span data-stu-id="0de8e-244">id</span></span> | <span data-ttu-id="0de8e-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="0de8e-245">deviceType</span></span> | <span data-ttu-id="0de8e-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="0de8e-246">targetResourceType</span></span> | <span data-ttu-id="0de8e-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="0de8e-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="0de8e-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="0de8e-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0de8e-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="0de8e-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="0de8e-250">PC</span><span class="sxs-lookup"><span data-stu-id="0de8e-250">PC</span></span> | <span data-ttu-id="0de8e-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="0de8e-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="0de8e-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="0de8e-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="0de8e-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="0de8e-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="0de8e-254">conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="0de8e-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="0de8e-255">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="0de8e-255">More specifically:</span></span>

- <span data-ttu-id="0de8e-256">`structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular.</span><span class="sxs-lookup"><span data-stu-id="0de8e-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="0de8e-257">Esta sección es **opcional** a menos que necesite toodo asignación de columna.</span><span class="sxs-lookup"><span data-stu-id="0de8e-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="0de8e-258">Vea [asignar columnas de conjunto de datos de origen dataset columnas toodestination](data-factory-map-columns.md) sección para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="0de8e-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="0de8e-259">`jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de.</span><span class="sxs-lookup"><span data-stu-id="0de8e-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="0de8e-260">toocopy datos de matriz, puede usar **.property de matriz [x]** tooextract valo Hola dada la propiedad de objeto de x-ésima de hello, o se puede usar  **matriz [*] .property** toofind valor de Hola de cualquier objeto que contiene dicha propiedad.</span><span class="sxs-lookup"><span data-stu-id="0de8e-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="0de8e-261">**Ejemplo 2: cross aplicar varios objetos con el mismo patrón de matriz de Hola**</span><span class="sxs-lookup"><span data-stu-id="0de8e-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="0de8e-262">En este ejemplo, espera un objeto JSON raíz tootransform en varios registros en los resultados tabulares.</span><span class="sxs-lookup"><span data-stu-id="0de8e-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="0de8e-263">Si tiene un archivo JSON con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="0de8e-263">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="0de8e-264">y desea toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, acoplando datos Hola dentro de la matriz de Hola y cross join con información de raíz común de hello:</span><span class="sxs-lookup"><span data-stu-id="0de8e-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="0de8e-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="0de8e-265">ordernumber</span></span> | <span data-ttu-id="0de8e-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="0de8e-266">orderdate</span></span> | <span data-ttu-id="0de8e-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="0de8e-267">order_pd</span></span> | <span data-ttu-id="0de8e-268">order_price</span><span class="sxs-lookup"><span data-stu-id="0de8e-268">order_price</span></span> | <span data-ttu-id="0de8e-269">city</span><span class="sxs-lookup"><span data-stu-id="0de8e-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0de8e-270">01</span><span class="sxs-lookup"><span data-stu-id="0de8e-270">01</span></span> | <span data-ttu-id="0de8e-271">20170122</span><span class="sxs-lookup"><span data-stu-id="0de8e-271">20170122</span></span> | <span data-ttu-id="0de8e-272">P1</span><span class="sxs-lookup"><span data-stu-id="0de8e-272">P1</span></span> | <span data-ttu-id="0de8e-273">23</span><span class="sxs-lookup"><span data-stu-id="0de8e-273">23</span></span> | <span data-ttu-id="0de8e-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="0de8e-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="0de8e-275">01</span><span class="sxs-lookup"><span data-stu-id="0de8e-275">01</span></span> | <span data-ttu-id="0de8e-276">20170122</span><span class="sxs-lookup"><span data-stu-id="0de8e-276">20170122</span></span> | <span data-ttu-id="0de8e-277">P2</span><span class="sxs-lookup"><span data-stu-id="0de8e-277">P2</span></span> | <span data-ttu-id="0de8e-278">13</span><span class="sxs-lookup"><span data-stu-id="0de8e-278">13</span></span> | <span data-ttu-id="0de8e-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="0de8e-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="0de8e-280">01</span><span class="sxs-lookup"><span data-stu-id="0de8e-280">01</span></span> | <span data-ttu-id="0de8e-281">20170122</span><span class="sxs-lookup"><span data-stu-id="0de8e-281">20170122</span></span> | <span data-ttu-id="0de8e-282">P3</span><span class="sxs-lookup"><span data-stu-id="0de8e-282">P3</span></span> | <span data-ttu-id="0de8e-283">231</span><span class="sxs-lookup"><span data-stu-id="0de8e-283">231</span></span> | <span data-ttu-id="0de8e-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="0de8e-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="0de8e-285">conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="0de8e-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="0de8e-286">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="0de8e-286">More specifically:</span></span>

- <span data-ttu-id="0de8e-287">`structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular.</span><span class="sxs-lookup"><span data-stu-id="0de8e-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="0de8e-288">Esta sección es **opcional** a menos que necesite toodo asignación de columna.</span><span class="sxs-lookup"><span data-stu-id="0de8e-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="0de8e-289">Vea [asignar columnas de conjunto de datos de origen dataset columnas toodestination](data-factory-map-columns.md) sección para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="0de8e-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="0de8e-290">`jsonNodeReference`indica datos tooiterate y la extracción de objetos de hello con hello mismo patrón en **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="0de8e-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="0de8e-291">`jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de.</span><span class="sxs-lookup"><span data-stu-id="0de8e-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="0de8e-292">En este ejemplo, "ordernumber", "orderdate" y "city" están bajo el objeto raíz con la ruta de acceso JSON a partir de "$.", mientras que "order_pd" y "order_price" se definen con la ruta de acceso que se deriva de elemento de la matriz de hello sin "$"..</span><span class="sxs-lookup"><span data-stu-id="0de8e-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="0de8e-293">**Tenga en cuenta Hola siguientes puntos:**</span><span class="sxs-lookup"><span data-stu-id="0de8e-293">**Note hello following points:**</span></span>

* <span data-ttu-id="0de8e-294">Si hello `structure` y `jsonPathDefinition` no estén definidos en conjunto de datos de Data Factory de hello, hello actividad de copia detecta Hola esquema desde el primer objeto de Hola y simplificar el objeto entero Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="0de8e-295">Si la entrada JSON de hello tiene una matriz, de forma predeterminada Hola actividad de copia convierte valor de la matriz completa de hello en una cadena.</span><span class="sxs-lookup"><span data-stu-id="0de8e-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="0de8e-296">Puede elegir tooextract datos de mediante `jsonNodeReference` o `jsonPathDefinition`, u omita especificándolo no en `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="0de8e-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="0de8e-297">Si hay duplicados Hola de nombres en el mismo nivel, Hola actividad de copia toma Hola último.</span><span class="sxs-lookup"><span data-stu-id="0de8e-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="0de8e-298">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0de8e-298">Property names are case-sensitive.</span></span> <span data-ttu-id="0de8e-299">Dos propiedades con el mismo nombre, pero con distintas mayúsculas y minúsculas se consideran propiedades independientes.</span><span class="sxs-lookup"><span data-stu-id="0de8e-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="0de8e-300">**Caso 2: Escribir datos tooJSON en el archivo**</span><span class="sxs-lookup"><span data-stu-id="0de8e-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="0de8e-301">Si tienes hello en la base de datos SQL en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="0de8e-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="0de8e-302">id</span><span class="sxs-lookup"><span data-stu-id="0de8e-302">id</span></span> | <span data-ttu-id="0de8e-303">order_date</span><span class="sxs-lookup"><span data-stu-id="0de8e-303">order_date</span></span> | <span data-ttu-id="0de8e-304">order_price</span><span class="sxs-lookup"><span data-stu-id="0de8e-304">order_price</span></span> | <span data-ttu-id="0de8e-305">order_by</span><span class="sxs-lookup"><span data-stu-id="0de8e-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0de8e-306">1</span><span class="sxs-lookup"><span data-stu-id="0de8e-306">1</span></span> | <span data-ttu-id="0de8e-307">20170119</span><span class="sxs-lookup"><span data-stu-id="0de8e-307">20170119</span></span> | <span data-ttu-id="0de8e-308">2000</span><span class="sxs-lookup"><span data-stu-id="0de8e-308">2000</span></span> | <span data-ttu-id="0de8e-309">David</span><span class="sxs-lookup"><span data-stu-id="0de8e-309">David</span></span> |
| <span data-ttu-id="0de8e-310">2</span><span class="sxs-lookup"><span data-stu-id="0de8e-310">2</span></span> | <span data-ttu-id="0de8e-311">20170120</span><span class="sxs-lookup"><span data-stu-id="0de8e-311">20170120</span></span> | <span data-ttu-id="0de8e-312">3500</span><span class="sxs-lookup"><span data-stu-id="0de8e-312">3500</span></span> | <span data-ttu-id="0de8e-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="0de8e-313">Patrick</span></span> |
| <span data-ttu-id="0de8e-314">3</span><span class="sxs-lookup"><span data-stu-id="0de8e-314">3</span></span> | <span data-ttu-id="0de8e-315">20170121</span><span class="sxs-lookup"><span data-stu-id="0de8e-315">20170121</span></span> | <span data-ttu-id="0de8e-316">4000</span><span class="sxs-lookup"><span data-stu-id="0de8e-316">4000</span></span> | <span data-ttu-id="0de8e-317">Jason</span><span class="sxs-lookup"><span data-stu-id="0de8e-317">Jason</span></span> |

<span data-ttu-id="0de8e-318">y para cada registro, se espera que toowrite tooa JSON objeto Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="0de8e-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="0de8e-319">con el conjunto de datos de salida de Hello **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="0de8e-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="0de8e-320">Más específicamente, `structure` sección define los nombres de propiedad Hola personalizado en el archivo de destino, `nestingSeparator` (valor predeterminado es ".") son utilizados tooidentify Hola anidamiento capa del nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="0de8e-321">Esta sección es **opcional** a menos que se desea el nombre de la propiedad de hello toochange comparar con el nombre de la columna de origen o anidar algunas de las propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="0de8e-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="0de8e-322">AVRO format</span></span>
<span data-ttu-id="0de8e-323">Si desea tooparse hello Avro archivos o escribir datos de hello en el formato Avro, establezca hello `format` `type` propiedad demasiado**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="0de8e-324">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="0de8e-325">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0de8e-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="0de8e-326">toouse el formato Avro en una tabla de Hive, puede hacer referencia demasiado[tutorial de Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="0de8e-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="0de8e-327">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="0de8e-327">Note hello following points:</span></span>  

* <span data-ttu-id="0de8e-328">No se admiten [tipos de datos complejos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumeraciones, matrices, asignaciones, uniones y fijos).</span><span class="sxs-lookup"><span data-stu-id="0de8e-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="0de8e-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="0de8e-329">ORC format</span></span>
<span data-ttu-id="0de8e-330">Si desea tooparse Hola ORC archivos o escribir datos de hello en formato ORC, Establece hello `format` `type` propiedad demasiado**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="0de8e-331">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="0de8e-332">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0de8e-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="0de8e-333">Si no va a copiar archivos ORC **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0de8e-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="0de8e-334">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="0de8e-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="0de8e-335">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="0de8e-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="0de8e-336">Elija Hola adecuada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="0de8e-337">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="0de8e-337">Note hello following points:</span></span>

* <span data-ttu-id="0de8e-338">No se admiten tipos de daros complejos (STRUCT, MAP, LIST, UNION).</span><span class="sxs-lookup"><span data-stu-id="0de8e-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="0de8e-339">El archivo ORC tiene tres [opciones relacionadas con la compresión](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB y SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="0de8e-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="0de8e-340">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="0de8e-341">Utiliza la compresión de hello códec está en datos de saludo metadatos tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="0de8e-342">Sin embargo, al escribir un archivo de tooan ORC, factoría de datos elige ZLIB, que es el valor predeterminado de Hola para ORC.</span><span class="sxs-lookup"><span data-stu-id="0de8e-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="0de8e-343">Actualmente no hay ninguna opción toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="0de8e-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="0de8e-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="0de8e-344">Parquet format</span></span>
<span data-ttu-id="0de8e-345">Si desea tooparse Hola Parquet archivos o escribir datos de hello en formato Parquet, Establece hello `format` `type` propiedad demasiado**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="0de8e-346">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="0de8e-347">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0de8e-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="0de8e-348">Si no va a copiar archivos Parquet **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0de8e-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="0de8e-349">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="0de8e-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="0de8e-350">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="0de8e-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="0de8e-351">Elija Hola adecuada.</span><span class="sxs-lookup"><span data-stu-id="0de8e-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="0de8e-352">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="0de8e-352">Note hello following points:</span></span>

* <span data-ttu-id="0de8e-353">No se admiten tipos de daros complejos (MAP, LIST).</span><span class="sxs-lookup"><span data-stu-id="0de8e-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="0de8e-354">Archivo parquet tiene Hola siguientes opciones de compresión: ninguno, SNAPPY, GZIP y LZO.</span><span class="sxs-lookup"><span data-stu-id="0de8e-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="0de8e-355">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="0de8e-356">Usa códec de compresión de hello en datos de saludo metadatos tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="0de8e-357">Sin embargo, al escribir un archivo de Parquet tooa, factoría de datos elige SNAPPY, que es el predeterminado de hello para el formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="0de8e-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="0de8e-358">Actualmente no hay ninguna opción toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="0de8e-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="0de8e-359">Compatibilidad de compresión</span><span class="sxs-lookup"><span data-stu-id="0de8e-359">Compression support</span></span>
<span data-ttu-id="0de8e-360">El procesamiento de grandes conjuntos de datos puede provocar cuellos de botella de E/S y red.</span><span class="sxs-lookup"><span data-stu-id="0de8e-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="0de8e-361">Por lo tanto, los datos comprimidos en almacenes pueden no solo acelerar la transferencia de datos a través de red de Hola y ahorrar espacio en disco, pero abrir importantes mejoras de rendimiento en el procesamiento de grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="0de8e-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="0de8e-362">En este momento, se admite la compresión para almacenes de datos basados en archivos como Blob de Azure o el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="0de8e-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="0de8e-363">compresión de toospecify para un conjunto de datos, use hello **compresión** propiedad Hola dataset JSON como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="0de8e-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="0de8e-364">Supongamos que el conjunto de datos de ejemplo de Hola se usa como salida de hello de una actividad de copia, Hola copia actividad comprime Hola códec GZIP usando proporción óptima los datos de salida y, a continuación, escribir datos de hello comprimido en un archivo denominado pagecounts.csv.gz en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="0de8e-365">No se admiten valores de compresión de datos en hello **AvroFormat**, **OrcFormat**, o **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="0de8e-366">Al leer archivos en estos formatos, factoría de datos detecta y usa el códec de compresión de hello en los metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de8e-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="0de8e-367">Al escribir toofiles en estos formatos, factoría de datos elige códec de compresión predeterminado de Hola para ese formato.</span><span class="sxs-lookup"><span data-stu-id="0de8e-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="0de8e-368">Por ejemplo, ZLIB en el caso de OrcFormat y SNAPPY en el caso de ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="0de8e-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="0de8e-369">Hola **compresión** sección tiene dos propiedades:</span><span class="sxs-lookup"><span data-stu-id="0de8e-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="0de8e-370">**Tipo:** códec de compresión de hello, que puede ser **GZIP**, **Deflate**, **BZIP2**, o **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="0de8e-371">**Nivel:** razón de compresión de hello, que puede ser **óptimo** o **más rápido**.</span><span class="sxs-lookup"><span data-stu-id="0de8e-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="0de8e-372">**Más rápido:** operación de compresión de hello debe completarse tan rápidamente como sea posible, incluso si el archivo resultante de hello no se comprime un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="0de8e-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="0de8e-373">**Óptimo**: operación de compresión de hello debe óptimamente comprimirse, incluso si la operación de hello toma un toocomplete de tiempo más largo.</span><span class="sxs-lookup"><span data-stu-id="0de8e-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="0de8e-374">Para más información, consulte el tema [Nivel de compresión](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0de8e-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="0de8e-375">Cuando se especifica `compression` propiedad en un conjunto de datos de entrada JSON, canalización Hola puede leer los datos comprimidos de origen de hello; y cuando se especifica la propiedad de hello en un conjunto de datos de salida JSON, actividad de copia de hello puede escribir el destino de los datos comprimidos toohello.</span><span class="sxs-lookup"><span data-stu-id="0de8e-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="0de8e-376">Estos son algunos escenarios de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0de8e-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="0de8e-377">Leer datos GZIP comprimido de un blob de Azure, descomprimir el archivo y escribir la base de datos SQL de Azure tooan de datos de resultado.</span><span class="sxs-lookup"><span data-stu-id="0de8e-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="0de8e-378">Definir Hola la conjunto de datos de Blob de Azure entrada con hello `compression` `type` propiedad JSON como GZIP.</span><span class="sxs-lookup"><span data-stu-id="0de8e-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="0de8e-379">Leer datos desde un archivo de texto sin formato de sistema de archivos local, comprima con formato GZip y escritura Hola comprimir datos tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="0de8e-380">Definir un conjunto de datos de salida Blob de Azure con hello `compression` `type` propiedad JSON como GZip.</span><span class="sxs-lookup"><span data-stu-id="0de8e-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="0de8e-381">Archivo .zip de lectura desde el servidor FTP, descomprimir archivos de hello tooget dentro de y se dirigirán a esos archivos en el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de8e-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="0de8e-382">Definir un conjunto de datos de entrada FTP con hello `compression` `type` propiedad JSON como ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="0de8e-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="0de8e-383">Leer datos de compresión GZIP de un blob de Azure, descomprimir el archivo, comprimir mediante BZIP2 y escribir datos de resultado tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0de8e-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="0de8e-384">Definir Hola la conjunto de datos de Blob de Azure entrada con `compression` `type` establecer tooGZIP y con el conjunto de datos de salida de hello `compression` `type` establecido tooBZIP2 en este caso.</span><span class="sxs-lookup"><span data-stu-id="0de8e-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="0de8e-385">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0de8e-385">Next steps</span></span>
<span data-ttu-id="0de8e-386">Vea Hola siguientes artículos basados en archivos para almacenes de datos compatibles con Data Factory de Azure:</span><span class="sxs-lookup"><span data-stu-id="0de8e-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="0de8e-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="0de8e-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="0de8e-388">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0de8e-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="0de8e-389">FTP</span><span class="sxs-lookup"><span data-stu-id="0de8e-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="0de8e-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="0de8e-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="0de8e-391">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="0de8e-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="0de8e-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="0de8e-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
