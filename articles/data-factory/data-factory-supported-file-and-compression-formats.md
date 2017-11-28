---
title: "Formatos de compresión de archivos en Azure Data Factory | Microsoft Docs"
description: Aprenda sobre los formatos de archivo compatibles con Azure Data Factory.
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="bf75c-104">Formatos de compresión de archivos admitidos por Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bf75c-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="bf75c-105">*Este tema se aplica a los conectores siguientes: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [sistema de archivos](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md) y [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="bf75c-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="bf75c-106">Azure Data Factory admite los siguientes tipos de formato de archivo:</span><span class="sxs-lookup"><span data-stu-id="bf75c-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="bf75c-107">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="bf75c-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="bf75c-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="bf75c-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="bf75c-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="bf75c-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="bf75c-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="bf75c-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="bf75c-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="bf75c-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="bf75c-112">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="bf75c-112">Text format</span></span>
<span data-ttu-id="bf75c-113">Si quiere leer un archivo de texto o escribir en él, establezca la propiedad `type` de la sección `format` del conjunto de datos en **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="bf75c-114">También puede especificar las siguientes propiedades **opcionales** en la sección `format`.</span><span class="sxs-lookup"><span data-stu-id="bf75c-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="bf75c-115">Consulte la sección [Ejemplo de TextFormat](#textformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bf75c-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="bf75c-116">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bf75c-116">Property</span></span> | <span data-ttu-id="bf75c-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="bf75c-117">Description</span></span> | <span data-ttu-id="bf75c-118">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="bf75c-118">Allowed values</span></span> | <span data-ttu-id="bf75c-119">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bf75c-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf75c-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="bf75c-120">columnDelimiter</span></span> |<span data-ttu-id="bf75c-121">El carácter utilizado para separar las columnas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="bf75c-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="bf75c-122">Puede considerar el uso de un carácter imprimible poco frecuente que es probable que no exista en sus datos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="bf75c-123">Por ejemplo, especifique "\u0001", que representa el inicio de encabezado (SOH).</span><span class="sxs-lookup"><span data-stu-id="bf75c-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="bf75c-124">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="bf75c-124">Only one character is allowed.</span></span> <span data-ttu-id="bf75c-125">El valor **predeterminado** es **coma (",")**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="bf75c-126">Para usar un carácter Unicode, consulte la [lista de caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) para obtener el código correspondiente.</span><span class="sxs-lookup"><span data-stu-id="bf75c-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="bf75c-127">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-127">No</span></span> |
| <span data-ttu-id="bf75c-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="bf75c-128">rowDelimiter</span></span> |<span data-ttu-id="bf75c-129">El carácter usado para separar las filas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="bf75c-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="bf75c-130">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="bf75c-130">Only one character is allowed.</span></span> <span data-ttu-id="bf75c-131">El valor **predeterminado** es cualquiera de los siguientes en lectura: **["\r\n", "\r", "\n"]** y **"\r\n"** en escritura.</span><span class="sxs-lookup"><span data-stu-id="bf75c-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="bf75c-132">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-132">No</span></span> |
| <span data-ttu-id="bf75c-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="bf75c-133">escapeChar</span></span> |<span data-ttu-id="bf75c-134">El carácter especial que se usa para anular un delimitador de columna en el contenido del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="bf75c-135">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="bf75c-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="bf75c-136">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="bf75c-136">Only one character is allowed.</span></span> <span data-ttu-id="bf75c-137">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-137">No default value.</span></span> <br/><br/><span data-ttu-id="bf75c-138">Ejemplo: si tiene la coma (',') como el delimitador de columna, pero quiere tener el carácter de coma en el texto (ejemplo: "Hello, world"), puede definir '$' como carácter de escape y usar la cadena "Hello$, world" en el origen.</span><span class="sxs-lookup"><span data-stu-id="bf75c-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="bf75c-139">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-139">No</span></span> |
| <span data-ttu-id="bf75c-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="bf75c-140">quoteChar</span></span> |<span data-ttu-id="bf75c-141">El carácter usado para poner entre comillas un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="bf75c-141">The character used to quote a string value.</span></span> <span data-ttu-id="bf75c-142">Los delimitadores de columna y fila entre comillas se tratarán como parte del valor de la cadena.</span><span class="sxs-lookup"><span data-stu-id="bf75c-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="bf75c-143">Esta propiedad se aplica a conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="bf75c-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="bf75c-144">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="bf75c-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="bf75c-145">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="bf75c-145">Only one character is allowed.</span></span> <span data-ttu-id="bf75c-146">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-146">No default value.</span></span> <br/><br/><span data-ttu-id="bf75c-147">Por ejemplo, si tiene la coma (',') como delimitador de columna, pero quiere tener el carácter de coma en el texto (por ejemplo: <Hello, world>), puede definir " (comillas dobles) como comillas y usar la cadena "Hello, world" en el origen.</span><span class="sxs-lookup"><span data-stu-id="bf75c-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="bf75c-148">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-148">No</span></span> |
| <span data-ttu-id="bf75c-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="bf75c-149">nullValue</span></span> |<span data-ttu-id="bf75c-150">Uno o más caracteres que se usan para representar un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="bf75c-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="bf75c-151">Uno o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf75c-151">One or more characters.</span></span> <span data-ttu-id="bf75c-152">Los valores **predeterminados** son **"\N" y "NULL"** en lectura y **"\N"** en escritura.</span><span class="sxs-lookup"><span data-stu-id="bf75c-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="bf75c-153">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-153">No</span></span> |
| <span data-ttu-id="bf75c-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="bf75c-154">encodingName</span></span> |<span data-ttu-id="bf75c-155">Especifique el nombre de codificación.</span><span class="sxs-lookup"><span data-stu-id="bf75c-155">Specify the encoding name.</span></span> |<span data-ttu-id="bf75c-156">Un nombre de codificación válido.</span><span class="sxs-lookup"><span data-stu-id="bf75c-156">A valid encoding name.</span></span> <span data-ttu-id="bf75c-157">Consulte la [propiedad Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf75c-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="bf75c-158">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="bf75c-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="bf75c-159">El valor **predeterminado** es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="bf75c-160">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-160">No</span></span> |
| <span data-ttu-id="bf75c-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="bf75c-161">firstRowAsHeader</span></span> |<span data-ttu-id="bf75c-162">Especifica si se tendrá en cuenta la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="bf75c-163">Para un conjunto de datos de entrada, Data Factory lee la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="bf75c-164">Para un conjunto de datos de salida, Data Factory escribe la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="bf75c-165">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="bf75c-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="bf75c-166">True</span><span class="sxs-lookup"><span data-stu-id="bf75c-166">True</span></span><br/><span data-ttu-id="bf75c-167"><b>False (valor predeterminado)</b></span><span class="sxs-lookup"><span data-stu-id="bf75c-167"><b>False (default)</b></span></span> |<span data-ttu-id="bf75c-168">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-168">No</span></span> |
| <span data-ttu-id="bf75c-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="bf75c-169">skipLineCount</span></span> |<span data-ttu-id="bf75c-170">Indica el número de filas que se omitirán al leer datos de archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="bf75c-171">Si se especifican skipLineCount y firstRowAsHeader, las líneas se omiten primero y luego la información del encabezado se lee del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="bf75c-172">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="bf75c-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="bf75c-173">Entero</span><span class="sxs-lookup"><span data-stu-id="bf75c-173">Integer</span></span> |<span data-ttu-id="bf75c-174">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-174">No</span></span> |
| <span data-ttu-id="bf75c-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="bf75c-175">treatEmptyAsNull</span></span> |<span data-ttu-id="bf75c-176">Especifica si las cadenas null o vacías se tratarán como valores null al leer datos de un archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="bf75c-177">**True (predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="bf75c-177">**True (default)**</span></span><br/><span data-ttu-id="bf75c-178">False</span><span class="sxs-lookup"><span data-stu-id="bf75c-178">False</span></span> |<span data-ttu-id="bf75c-179">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="bf75c-180">Ejemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="bf75c-180">TextFormat example</span></span>
<span data-ttu-id="bf75c-181">En la siguiente definición JSON de un conjunto de datos, se especifican algunas propiedades opcionales.</span><span class="sxs-lookup"><span data-stu-id="bf75c-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="bf75c-182">Para usar un `escapeChar` en lugar de `quoteChar`, reemplace la línea con `quoteChar` por el siguiente escapeChar:</span><span class="sxs-lookup"><span data-stu-id="bf75c-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="bf75c-183">Escenarios de uso de firstRowAsHeader y skipLineCount</span><span class="sxs-lookup"><span data-stu-id="bf75c-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="bf75c-184">Va a copiar de un origen que no es archivo a un archivo de texto y quiere agregar una línea de encabezado que contenga los metadatos de esquema (por ejemplo, esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="bf75c-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="bf75c-185">Especifique `firstRowAsHeader` como true en el conjunto de datos de salida de este escenario.</span><span class="sxs-lookup"><span data-stu-id="bf75c-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="bf75c-186">Va a copiar de un archivo de texto que contiene una línea de encabezado a un receptor que no es archivo y quiere eliminar esa línea.</span><span class="sxs-lookup"><span data-stu-id="bf75c-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="bf75c-187">Especifique `firstRowAsHeader` como true en el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="bf75c-188">Va a copiar de un archivo de texto y quiere omitir unas cuantas líneas al comienzo que no contienen datos ni información de encabezado.</span><span class="sxs-lookup"><span data-stu-id="bf75c-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="bf75c-189">Especifique `skipLineCount` para indicar el número de líneas que se omitirá.</span><span class="sxs-lookup"><span data-stu-id="bf75c-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="bf75c-190">Si el resto del archivo contiene una línea de encabezado, también puede especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="bf75c-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="bf75c-191">Si se especifican `skipLineCount` y `firstRowAsHeader`, las líneas se omiten primero y luego la información del encabezado se lee del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="bf75c-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="bf75c-192">JSON format</span></span>
<span data-ttu-id="bf75c-193">Para **importar un archivo JSON como está en Azure Cosmos DB o exportarlo**, vea la sección [Importación o exportación de documentos JSON](data-factory-azure-documentdb-connector.md#importexport-json-documents) en el artículo [Movimiento de datos hacia y desde DocumentDB mediante Azure Data Factory](data-factory-azure-documentdb-connector.md).</span><span class="sxs-lookup"><span data-stu-id="bf75c-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="bf75c-194">Si quiere analizar los archivos JSON o escribir los datos en formato JSON, establezca la propiedad `type` `format` en **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="bf75c-195">También puede especificar las siguientes propiedades **opcionales** en la sección `format`.</span><span class="sxs-lookup"><span data-stu-id="bf75c-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="bf75c-196">Consulte la sección [Ejemplo de JsonFormat](#jsonformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bf75c-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="bf75c-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bf75c-197">Property</span></span> | <span data-ttu-id="bf75c-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="bf75c-198">Description</span></span> | <span data-ttu-id="bf75c-199">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bf75c-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf75c-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="bf75c-200">filePattern</span></span> |<span data-ttu-id="bf75c-201">Indica el patrón de los datos almacenados en cada archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="bf75c-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="bf75c-202">Estos son los valores permitidos: **setOfObjects** y **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="bf75c-203">El valor **predeterminado** es **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="bf75c-204">Consulte la sección [patrones de archivo JSON](#json-file-patterns) para obtener más información acerca de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="bf75c-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="bf75c-205">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-205">No</span></span> |
| <span data-ttu-id="bf75c-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="bf75c-206">jsonNodeReference</span></span> | <span data-ttu-id="bf75c-207">Si desea iterar y extraer datos de los objetos dentro de un campo de matriz con el mismo patrón, especifique la ruta de acceso JSON de esa matriz.</span><span class="sxs-lookup"><span data-stu-id="bf75c-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="bf75c-208">Esta propiedad se admite solo cuando se copian datos desde los archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf75c-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="bf75c-209">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-209">No</span></span> |
| <span data-ttu-id="bf75c-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="bf75c-210">jsonPathDefinition</span></span> | <span data-ttu-id="bf75c-211">Especifique la expresión de ruta de acceso JSON para cada asignación de columna con un nombre de columna personalizado (que empiece con minúscula).</span><span class="sxs-lookup"><span data-stu-id="bf75c-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="bf75c-212">Esta propiedad se admite solo cuando se copian datos desde archivos JSON y puede extraer datos del objeto o matriz.</span><span class="sxs-lookup"><span data-stu-id="bf75c-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="bf75c-213">Para los campos en el objeto raíz, comience por root $; para los campos dentro de la matriz elegida mediante la propiedad `jsonNodeReference`, empiece desde el elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf75c-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="bf75c-214">Consulte la sección [Ejemplo de JsonFormat](#jsonformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bf75c-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="bf75c-215">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-215">No</span></span> |
| <span data-ttu-id="bf75c-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="bf75c-216">encodingName</span></span> |<span data-ttu-id="bf75c-217">Especifique el nombre de codificación.</span><span class="sxs-lookup"><span data-stu-id="bf75c-217">Specify the encoding name.</span></span> <span data-ttu-id="bf75c-218">Para obtener la lista de nombres de codificación válidos, vea el artículo sobre la propiedad [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bf75c-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="bf75c-219">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="bf75c-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="bf75c-220">El valor **predeterminado** es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="bf75c-221">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-221">No</span></span> |
| <span data-ttu-id="bf75c-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="bf75c-222">nestingSeparator</span></span> |<span data-ttu-id="bf75c-223">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="bf75c-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="bf75c-224">El valor predeterminado es '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="bf75c-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="bf75c-225">No</span><span class="sxs-lookup"><span data-stu-id="bf75c-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="bf75c-226">Patrones de archivo JSON</span><span class="sxs-lookup"><span data-stu-id="bf75c-226">JSON file patterns</span></span>

<span data-ttu-id="bf75c-227">La actividad de copia puede analizar los siguientes patrones de archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="bf75c-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="bf75c-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="bf75c-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="bf75c-229">Cada archivo contiene un único objeto o bien varios objetos concatenados/delimitados por líneas.</span><span class="sxs-lookup"><span data-stu-id="bf75c-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="bf75c-230">Si se elige esta opción en un conjunto de datos de salida, la actividad de copia genera un único archivo JSON con cada objeto por línea (delimitado por líneas).</span><span class="sxs-lookup"><span data-stu-id="bf75c-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="bf75c-231">**ejemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="bf75c-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="bf75c-232">**ejemplo de JSON delimitado por líneas**</span><span class="sxs-lookup"><span data-stu-id="bf75c-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="bf75c-233">**ejemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="bf75c-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="bf75c-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="bf75c-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="bf75c-235">Cada archivo contiene una matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="bf75c-236">Ejemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="bf75c-236">JsonFormat example</span></span>

<span data-ttu-id="bf75c-237">**Caso 1: Copia de datos desde archivos JSON**</span><span class="sxs-lookup"><span data-stu-id="bf75c-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="bf75c-238">Consulte los dos ejemplos siguientes al copiar datos desde archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf75c-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="bf75c-239">Puntos genéricos que deben tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="bf75c-239">The generic points to note:</span></span>

<span data-ttu-id="bf75c-240">**Ejemplo 1: extracción de datos de objeto y matriz**</span><span class="sxs-lookup"><span data-stu-id="bf75c-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="bf75c-241">En esta ejemplo, se espera un objeto JSON de raíz que se asigna al registro individual en resultado tabulares.</span><span class="sxs-lookup"><span data-stu-id="bf75c-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="bf75c-242">Si tiene un archivo JSON con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="bf75c-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="bf75c-243">y quiere copiarlo en una tabla de SQL de Azure con el formato siguiente extrayendo datos tanto de los objetos como de la matriz:</span><span class="sxs-lookup"><span data-stu-id="bf75c-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="bf75c-244">id</span><span class="sxs-lookup"><span data-stu-id="bf75c-244">id</span></span> | <span data-ttu-id="bf75c-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="bf75c-245">deviceType</span></span> | <span data-ttu-id="bf75c-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="bf75c-246">targetResourceType</span></span> | <span data-ttu-id="bf75c-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="bf75c-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="bf75c-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="bf75c-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bf75c-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="bf75c-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="bf75c-250">PC</span><span class="sxs-lookup"><span data-stu-id="bf75c-250">PC</span></span> | <span data-ttu-id="bf75c-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="bf75c-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="bf75c-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="bf75c-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="bf75c-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="bf75c-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="bf75c-254">El conjunto de datos de entrada con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="bf75c-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bf75c-255">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="bf75c-255">More specifically:</span></span>

- <span data-ttu-id="bf75c-256">La sección `structure` permite definir los nombres personalizados de columna y el tipo de datos correspondiente mientras los convierte a datos tabulares.</span><span class="sxs-lookup"><span data-stu-id="bf75c-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="bf75c-257">Esta sección es **opcional** a menos que necesite realizar una asignación de columnas.</span><span class="sxs-lookup"><span data-stu-id="bf75c-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="bf75c-258">Consulte la sección [Asignación de columnas de conjunto de datos de origen a columnas del conjunto de datos de destino](data-factory-map-columns.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="bf75c-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="bf75c-259">`jsonPathDefinition` especifica la ruta de acceso JSON para cada columna que indica de dónde se deben extraer los datos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="bf75c-260">Para copiar datos de matriz, puede usar **array[x].property** para extraer el valor de la propiedad especificada desde el objeto xº, o puede usar **array[*] .property** para encontrar el valor de cualquier objeto que contenga dicha propiedad.</span><span class="sxs-lookup"><span data-stu-id="bf75c-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="bf75c-261">**Ejemplo 2: aplicación cruzada en varios objetos del mismo patrón de matriz**</span><span class="sxs-lookup"><span data-stu-id="bf75c-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="bf75c-262">En este ejemplo, se espera transformar un objeto JSON de raíz en varios registros en resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="bf75c-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="bf75c-263">Si tiene un archivo JSON con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="bf75c-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="bf75c-264">y desea copiarlo en una tabla de Azure SQL del formato siguiente, puede hacerlo mediante el acoplamiento de los datos dentro de la matriz y la combinación cruzada con la información de la raíz habitual:</span><span class="sxs-lookup"><span data-stu-id="bf75c-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="bf75c-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="bf75c-265">ordernumber</span></span> | <span data-ttu-id="bf75c-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="bf75c-266">orderdate</span></span> | <span data-ttu-id="bf75c-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="bf75c-267">order_pd</span></span> | <span data-ttu-id="bf75c-268">order_price</span><span class="sxs-lookup"><span data-stu-id="bf75c-268">order_price</span></span> | <span data-ttu-id="bf75c-269">city</span><span class="sxs-lookup"><span data-stu-id="bf75c-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bf75c-270">01</span><span class="sxs-lookup"><span data-stu-id="bf75c-270">01</span></span> | <span data-ttu-id="bf75c-271">20170122</span><span class="sxs-lookup"><span data-stu-id="bf75c-271">20170122</span></span> | <span data-ttu-id="bf75c-272">P1</span><span class="sxs-lookup"><span data-stu-id="bf75c-272">P1</span></span> | <span data-ttu-id="bf75c-273">23</span><span class="sxs-lookup"><span data-stu-id="bf75c-273">23</span></span> | <span data-ttu-id="bf75c-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bf75c-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="bf75c-275">01</span><span class="sxs-lookup"><span data-stu-id="bf75c-275">01</span></span> | <span data-ttu-id="bf75c-276">20170122</span><span class="sxs-lookup"><span data-stu-id="bf75c-276">20170122</span></span> | <span data-ttu-id="bf75c-277">P2</span><span class="sxs-lookup"><span data-stu-id="bf75c-277">P2</span></span> | <span data-ttu-id="bf75c-278">13</span><span class="sxs-lookup"><span data-stu-id="bf75c-278">13</span></span> | <span data-ttu-id="bf75c-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bf75c-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="bf75c-280">01</span><span class="sxs-lookup"><span data-stu-id="bf75c-280">01</span></span> | <span data-ttu-id="bf75c-281">20170122</span><span class="sxs-lookup"><span data-stu-id="bf75c-281">20170122</span></span> | <span data-ttu-id="bf75c-282">P3</span><span class="sxs-lookup"><span data-stu-id="bf75c-282">P3</span></span> | <span data-ttu-id="bf75c-283">231</span><span class="sxs-lookup"><span data-stu-id="bf75c-283">231</span></span> | <span data-ttu-id="bf75c-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bf75c-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="bf75c-285">El conjunto de datos de entrada con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="bf75c-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bf75c-286">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="bf75c-286">More specifically:</span></span>

- <span data-ttu-id="bf75c-287">La sección `structure` permite definir los nombres personalizados de columna y el tipo de datos correspondiente mientras los convierte a datos tabulares.</span><span class="sxs-lookup"><span data-stu-id="bf75c-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="bf75c-288">Esta sección es **opcional** a menos que necesite realizar una asignación de columnas.</span><span class="sxs-lookup"><span data-stu-id="bf75c-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="bf75c-289">Consulte la sección [Asignación de columnas de conjunto de datos de origen a columnas del conjunto de datos de destino](data-factory-map-columns.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="bf75c-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="bf75c-290">`jsonNodeReference` indica la iteración y extracción de datos de los objetos con el mismo patrón de las líneas de pedido de **matriz**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="bf75c-291">`jsonPathDefinition` especifica la ruta de acceso JSON para cada columna que indica de dónde se deben extraer los datos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="bf75c-292">En este ejemplo, "ordernumber", "orderdate" y "city" están bajo el objeto raíz con la ruta de acceso JSON que empieza por "$.", mientras que "order_pd" y "order_price" se definen con la ruta de acceso que se deriva del elemento de matriz sin "$.".</span><span class="sxs-lookup"><span data-stu-id="bf75c-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="bf75c-293">**Tenga en cuenta los siguientes puntos:**</span><span class="sxs-lookup"><span data-stu-id="bf75c-293">**Note the following points:**</span></span>

* <span data-ttu-id="bf75c-294">Si no se definen la `structure` y `jsonPathDefinition` en el conjunto de datos de Data Factory, la actividad de copia detecta el esquema del primer objeto y acopla el objeto en su conjunto.</span><span class="sxs-lookup"><span data-stu-id="bf75c-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="bf75c-295">Si la entrada JSON tiene una matriz, la actividad de copia convierte de forma predeterminada el valor de toda la matriz en una cadena.</span><span class="sxs-lookup"><span data-stu-id="bf75c-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="bf75c-296">Puede elegir extraer los datos de esta mediante `jsonNodeReference` o `jsonPathDefinition`, u omitir la extracción no especificándolo en `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="bf75c-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="bf75c-297">Si hay algún nombre duplicado en el mismo nivel, la actividad de copia elige el último.</span><span class="sxs-lookup"><span data-stu-id="bf75c-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="bf75c-298">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bf75c-298">Property names are case-sensitive.</span></span> <span data-ttu-id="bf75c-299">Dos propiedades con el mismo nombre, pero con distintas mayúsculas y minúsculas se consideran propiedades independientes.</span><span class="sxs-lookup"><span data-stu-id="bf75c-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="bf75c-300">**Caso 2: Escritura de datos en el archivo JSON**</span><span class="sxs-lookup"><span data-stu-id="bf75c-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="bf75c-301">Si tiene la siguiente tabla en SQL Database:</span><span class="sxs-lookup"><span data-stu-id="bf75c-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="bf75c-302">id</span><span class="sxs-lookup"><span data-stu-id="bf75c-302">id</span></span> | <span data-ttu-id="bf75c-303">order_date</span><span class="sxs-lookup"><span data-stu-id="bf75c-303">order_date</span></span> | <span data-ttu-id="bf75c-304">order_price</span><span class="sxs-lookup"><span data-stu-id="bf75c-304">order_price</span></span> | <span data-ttu-id="bf75c-305">order_by</span><span class="sxs-lookup"><span data-stu-id="bf75c-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf75c-306">1</span><span class="sxs-lookup"><span data-stu-id="bf75c-306">1</span></span> | <span data-ttu-id="bf75c-307">20170119</span><span class="sxs-lookup"><span data-stu-id="bf75c-307">20170119</span></span> | <span data-ttu-id="bf75c-308">2000</span><span class="sxs-lookup"><span data-stu-id="bf75c-308">2000</span></span> | <span data-ttu-id="bf75c-309">David</span><span class="sxs-lookup"><span data-stu-id="bf75c-309">David</span></span> |
| <span data-ttu-id="bf75c-310">2</span><span class="sxs-lookup"><span data-stu-id="bf75c-310">2</span></span> | <span data-ttu-id="bf75c-311">20170120</span><span class="sxs-lookup"><span data-stu-id="bf75c-311">20170120</span></span> | <span data-ttu-id="bf75c-312">3500</span><span class="sxs-lookup"><span data-stu-id="bf75c-312">3500</span></span> | <span data-ttu-id="bf75c-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="bf75c-313">Patrick</span></span> |
| <span data-ttu-id="bf75c-314">3</span><span class="sxs-lookup"><span data-stu-id="bf75c-314">3</span></span> | <span data-ttu-id="bf75c-315">20170121</span><span class="sxs-lookup"><span data-stu-id="bf75c-315">20170121</span></span> | <span data-ttu-id="bf75c-316">4000</span><span class="sxs-lookup"><span data-stu-id="bf75c-316">4000</span></span> | <span data-ttu-id="bf75c-317">Jason</span><span class="sxs-lookup"><span data-stu-id="bf75c-317">Jason</span></span> |

<span data-ttu-id="bf75c-318">y para cada registro, espera escribir en un objeto JSON con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="bf75c-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="bf75c-319">El conjunto de datos de salida con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="bf75c-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bf75c-320">Más concretamente, la sección `structure` permite definir los nombres de propiedad personalizados en el archivo de destino y `nestingSeparator` (el valor predeterminado es ".") se usa para identificar el nivel de anidamiento del nombre.</span><span class="sxs-lookup"><span data-stu-id="bf75c-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="bf75c-321">Esta sección es **opcional** a menos que desee cambiar el nombre de la propiedad comparándolo con el nombre de la columna de origen, o anidar algunas de las propiedades.</span><span class="sxs-lookup"><span data-stu-id="bf75c-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="bf75c-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="bf75c-322">AVRO format</span></span>
<span data-ttu-id="bf75c-323">Si desea analizar los archivos Avro o escribir los datos en formato Avro, establezca la propiedad `format` `type` en **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="bf75c-324">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bf75c-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bf75c-325">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bf75c-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="bf75c-326">Para usar el formato Avro en una tabla de Hive, puede consultar [Tutorial de Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="bf75c-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="bf75c-327">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="bf75c-327">Note the following points:</span></span>  

* <span data-ttu-id="bf75c-328">No se admiten [tipos de datos complejos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumeraciones, matrices, asignaciones, uniones y fijos).</span><span class="sxs-lookup"><span data-stu-id="bf75c-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="bf75c-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="bf75c-329">ORC format</span></span>
<span data-ttu-id="bf75c-330">Si desea analizar los archivos ORC o escribir los datos en formato ORC, establezca la propiedad `format` `type` en **ORCFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="bf75c-331">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bf75c-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bf75c-332">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bf75c-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="bf75c-333">Si no va a copiar archivos ORC **como están** entre almacenes de datos locales y en la nube, debe instalar JRE 8 (Java Runtime Environment) en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="bf75c-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="bf75c-334">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="bf75c-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="bf75c-335">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="bf75c-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="bf75c-336">Elija la más adecuada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="bf75c-337">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="bf75c-337">Note the following points:</span></span>

* <span data-ttu-id="bf75c-338">No se admiten tipos de daros complejos (STRUCT, MAP, LIST, UNION).</span><span class="sxs-lookup"><span data-stu-id="bf75c-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="bf75c-339">El archivo ORC tiene tres [opciones relacionadas con la compresión](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB y SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="bf75c-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="bf75c-340">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="bf75c-341">Se utiliza el códec de compresión en los metadatos para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="bf75c-342">Sin embargo, al escribir en un archivo ORC, Data Factory elige ZLIB que es el valor predeterminado para ORC.</span><span class="sxs-lookup"><span data-stu-id="bf75c-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="bf75c-343">Por el momento, no hay ninguna opción para invalidar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="bf75c-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="bf75c-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="bf75c-344">Parquet format</span></span>
<span data-ttu-id="bf75c-345">Si desea analizar los archivos Parquet o escribir los datos en formato Parquet, establezca la propiedad `format` `type` en **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="bf75c-346">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bf75c-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bf75c-347">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bf75c-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="bf75c-348">Si no va a copiar archivos Parquet **como están** entre almacenes de datos locales y en la nube, debe instalar JRE 8 (Java Runtime Environment) en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="bf75c-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="bf75c-349">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="bf75c-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="bf75c-350">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="bf75c-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="bf75c-351">Elija la más adecuada.</span><span class="sxs-lookup"><span data-stu-id="bf75c-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="bf75c-352">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="bf75c-352">Note the following points:</span></span>

* <span data-ttu-id="bf75c-353">No se admiten tipos de daros complejos (MAP, LIST).</span><span class="sxs-lookup"><span data-stu-id="bf75c-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="bf75c-354">El archivo Parquet tiene las siguientes opciones relacionadas con la compresión: NONE, SNAPPY, GZIP y LZO.</span><span class="sxs-lookup"><span data-stu-id="bf75c-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="bf75c-355">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="bf75c-356">Utiliza el códec de compresión en los metadatos para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="bf75c-357">Sin embargo, al escribir en un archivo Parquet, Data Factory elige SNAPPY que es el valor predeterminado para Parquet.</span><span class="sxs-lookup"><span data-stu-id="bf75c-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="bf75c-358">Por el momento, no hay ninguna opción para invalidar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="bf75c-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="bf75c-359">Compatibilidad de compresión</span><span class="sxs-lookup"><span data-stu-id="bf75c-359">Compression support</span></span>
<span data-ttu-id="bf75c-360">El procesamiento de grandes conjuntos de datos puede provocar cuellos de botella de E/S y red.</span><span class="sxs-lookup"><span data-stu-id="bf75c-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="bf75c-361">Por lo tanto, los datos comprimidos en almacenes pueden no solo acelerar la transferencia de datos a través de la red y ahorrar espacio en disco, sino también introducir importantes mejoras de rendimiento en el procesamiento de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="bf75c-362">En este momento, se admite la compresión para almacenes de datos basados en archivos como Blob de Azure o el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="bf75c-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="bf75c-363">Para especificar la compresión para un conjunto de datos, use la propiedad **compression** del conjunto de datos JSON como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bf75c-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="bf75c-364">Supongamos que el conjunto de datos de ejemplo se usa como salida de una actividad de copia; la actividad de copia comprime los datos de salida con el códec GZIP con una proporción óptima y, luego, escribe los datos comprimidos en un archivo denominado pagecounts.csv.gz en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bf75c-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="bf75c-365">La configuración de la compresión no se admite para los datos con los formatos **AvroFormat**, **OrcFormat** o **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="bf75c-366">Al leer archivos en estos formatos, Data Factory detecta y usa el códec de compresión en los metadatos.</span><span class="sxs-lookup"><span data-stu-id="bf75c-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="bf75c-367">Sin embargo, al escribir en archivos en estos formatos, Data Factory elige el códec de compresión predeterminado para ese formato.</span><span class="sxs-lookup"><span data-stu-id="bf75c-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="bf75c-368">Por ejemplo, ZLIB en el caso de OrcFormat y SNAPPY en el caso de ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="bf75c-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="bf75c-369">La sección **compression** tiene dos propiedades:</span><span class="sxs-lookup"><span data-stu-id="bf75c-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="bf75c-370">**Type**: el códec de compresión, que puede ser **GZIP**, **Deflate** o **BZIP2** o **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="bf75c-371">**Level**: la relación de compresión, que puede ser **Optimal** o **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="bf75c-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="bf75c-372">**Fastest:** la operación de compresión debe completarse tan pronto como sea posible, incluso si el archivo resultante no se comprime de forma óptima.</span><span class="sxs-lookup"><span data-stu-id="bf75c-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="bf75c-373">**Optimal:**la operación de compresión se debe comprimir óptimamente, incluso si tarda más tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="bf75c-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="bf75c-374">Para más información, consulte el tema [Nivel de compresión](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bf75c-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="bf75c-375">Cuando se especifica la propiedad `compression` en un JSON del conjunto de datos de entrada, la canalización puede leer los datos comprimidos del origen, mientras que cuando se especifica la propiedad en un conjunto del conjunto de datos de salida, la actividad de copia puede escribir datos comprimidos en el destino.</span><span class="sxs-lookup"><span data-stu-id="bf75c-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="bf75c-376">Estos son algunos escenarios de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bf75c-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="bf75c-377">Leer datos comprimidos con GZIP de un blob de Azure, descomprimirlos y escribir los datos de resultado en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf75c-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="bf75c-378">Defina el conjunto de datos del blob de Azure de entrada con la propiedad de JSON `compression` `type` como GZIP.</span><span class="sxs-lookup"><span data-stu-id="bf75c-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="bf75c-379">Leer datos de un archivo de texto sin formato del sistema de archivos local, comprimirlos con formato GZip y escribir los datos comprimidos en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf75c-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="bf75c-380">Defina el conjunto de datos del blob de Azure de salida con la propiedad de JSON `compression` `type` como GZip.</span><span class="sxs-lookup"><span data-stu-id="bf75c-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="bf75c-381">Leer el archivo .zip del servidor FTP, descomprimirlo para obtener los archivos que contiene y colocar dichos archivos en Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bf75c-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="bf75c-382">Defina el conjunto de datos del FTP de entrada con la propiedad de JSON `compression` `type` como ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="bf75c-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="bf75c-383">Leer datos comprimidos con GZIP de un blob de Azure, descomprimirlos, comprimirlos con BZIP2 y escribir los datos de resultado en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf75c-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="bf75c-384">Defina el conjunto de datos de blob de Azure de entrada con `compression` `type` establecidos en GZIP y el conjunto de datos de salida con `compression` `type` establecido en BZIP2 en este caso.</span><span class="sxs-lookup"><span data-stu-id="bf75c-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="bf75c-385">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf75c-385">Next steps</span></span>
<span data-ttu-id="bf75c-386">Consulte los siguientes artículos relativos a los almacenes de datos basados en archivos compatibles con Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="bf75c-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="bf75c-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bf75c-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="bf75c-388">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bf75c-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="bf75c-389">FTP</span><span class="sxs-lookup"><span data-stu-id="bf75c-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="bf75c-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="bf75c-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="bf75c-391">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="bf75c-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="bf75c-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="bf75c-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
