## <a name="specifying-formats"></a><span data-ttu-id="95d11-101">Especificación de formatos</span><span class="sxs-lookup"><span data-stu-id="95d11-101">Specifying formats</span></span>
<span data-ttu-id="95d11-102">Azure Data Factory admite los siguientes tipos de formato:</span><span class="sxs-lookup"><span data-stu-id="95d11-102">Azure Data Factory supports the following format types:</span></span>

* [<span data-ttu-id="95d11-103">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="95d11-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="95d11-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="95d11-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="95d11-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="95d11-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="95d11-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="95d11-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="95d11-107">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="95d11-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="95d11-108">Especificación de TextFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-108">Specifying TextFormat</span></span>
<span data-ttu-id="95d11-109">Si desea analizar los archivos de texto o escribir los datos en formato de texto, establezca la propiedad `format` `type` en **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="95d11-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="95d11-110">También puede especificar las siguientes propiedades **opcionales** en la sección `format`.</span><span class="sxs-lookup"><span data-stu-id="95d11-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="95d11-111">Consulte la sección [Ejemplo de TextFormat](#textformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="95d11-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="95d11-112">Propiedad</span><span class="sxs-lookup"><span data-stu-id="95d11-112">Property</span></span> | <span data-ttu-id="95d11-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="95d11-113">Description</span></span> | <span data-ttu-id="95d11-114">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="95d11-114">Allowed values</span></span> | <span data-ttu-id="95d11-115">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="95d11-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="95d11-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="95d11-116">columnDelimiter</span></span> |<span data-ttu-id="95d11-117">El carácter utilizado para separar las columnas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="95d11-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="95d11-118">Puede usar un carácter no imprimible excepcional que probablemente no existe en los datos: por ejemplo, especifique "\u0001", que representa el inicio de encabezado (SOH).</span><span class="sxs-lookup"><span data-stu-id="95d11-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="95d11-119">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="95d11-119">Only one character is allowed.</span></span> <span data-ttu-id="95d11-120">El valor **predeterminado** es **coma (",")**.</span><span class="sxs-lookup"><span data-stu-id="95d11-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="95d11-121">Para usar un carácter Unicode, consulte [Caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) para obtener el código correspondiente.</span><span class="sxs-lookup"><span data-stu-id="95d11-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="95d11-122">No</span><span class="sxs-lookup"><span data-stu-id="95d11-122">No</span></span> |
| <span data-ttu-id="95d11-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="95d11-123">rowDelimiter</span></span> |<span data-ttu-id="95d11-124">El carácter usado para separar las filas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="95d11-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="95d11-125">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="95d11-125">Only one character is allowed.</span></span> <span data-ttu-id="95d11-126">El valor **predeterminado** es cualquiera de los siguientes en lectura: **["\r\n", "\r", "\n"]** y **"\r\n"** en escritura.</span><span class="sxs-lookup"><span data-stu-id="95d11-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="95d11-127">No</span><span class="sxs-lookup"><span data-stu-id="95d11-127">No</span></span> |
| <span data-ttu-id="95d11-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="95d11-128">escapeChar</span></span> |<span data-ttu-id="95d11-129">El carácter especial que se usa para anular un delimitador de columna en el contenido del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="95d11-130">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="95d11-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="95d11-131">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="95d11-131">Only one character is allowed.</span></span> <span data-ttu-id="95d11-132">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="95d11-132">No default value.</span></span> <br/><br/><span data-ttu-id="95d11-133">Ejemplo: si tiene la coma (',') como el delimitador de columna, pero quiere tener el carácter de coma en el texto (ejemplo: "Hello, world"), puede definir '$' como carácter de escape y usar la cadena "Hello$, world" en el origen.</span><span class="sxs-lookup"><span data-stu-id="95d11-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="95d11-134">No</span><span class="sxs-lookup"><span data-stu-id="95d11-134">No</span></span> |
| <span data-ttu-id="95d11-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="95d11-135">quoteChar</span></span> |<span data-ttu-id="95d11-136">El carácter usado para poner entre comillas un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="95d11-136">The character used to quote a string value.</span></span> <span data-ttu-id="95d11-137">Los delimitadores de columna y fila entre comillas se tratarán como parte del valor de la cadena.</span><span class="sxs-lookup"><span data-stu-id="95d11-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="95d11-138">Esta propiedad se aplica a conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="95d11-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="95d11-139">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="95d11-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="95d11-140">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="95d11-140">Only one character is allowed.</span></span> <span data-ttu-id="95d11-141">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="95d11-141">No default value.</span></span> <br/><br/><span data-ttu-id="95d11-142">Por ejemplo, si tiene la coma (',') como delimitador de columna, pero quiere tener el carácter de coma en el texto (por ejemplo: <Hello, world>), puede definir " (comillas dobles) como comillas y usar la cadena "Hello, world" en el origen.</span><span class="sxs-lookup"><span data-stu-id="95d11-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="95d11-143">No</span><span class="sxs-lookup"><span data-stu-id="95d11-143">No</span></span> |
| <span data-ttu-id="95d11-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="95d11-144">nullValue</span></span> |<span data-ttu-id="95d11-145">Uno o más caracteres que se usan para representar un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="95d11-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="95d11-146">Uno o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="95d11-146">One or more characters.</span></span> <span data-ttu-id="95d11-147">Los valores **predeterminados** son **"\N" y "NULL"** en lectura y **"\N"** en escritura.</span><span class="sxs-lookup"><span data-stu-id="95d11-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="95d11-148">No</span><span class="sxs-lookup"><span data-stu-id="95d11-148">No</span></span> |
| <span data-ttu-id="95d11-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="95d11-149">encodingName</span></span> |<span data-ttu-id="95d11-150">Especifique el nombre de codificación.</span><span class="sxs-lookup"><span data-stu-id="95d11-150">Specify the encoding name.</span></span> |<span data-ttu-id="95d11-151">Un nombre de codificación válido.</span><span class="sxs-lookup"><span data-stu-id="95d11-151">A valid encoding name.</span></span> <span data-ttu-id="95d11-152">Consulte la [propiedad Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="95d11-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="95d11-153">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="95d11-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="95d11-154">El valor **predeterminado** es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="95d11-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="95d11-155">No</span><span class="sxs-lookup"><span data-stu-id="95d11-155">No</span></span> |
| <span data-ttu-id="95d11-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="95d11-156">firstRowAsHeader</span></span> |<span data-ttu-id="95d11-157">Especifica si se tendrá en cuenta la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="95d11-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="95d11-158">Para un conjunto de datos de entrada, Data Factory lee la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="95d11-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="95d11-159">Para un conjunto de datos de salida, Data Factory escribe la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="95d11-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="95d11-160">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="95d11-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="95d11-161">True</span><span class="sxs-lookup"><span data-stu-id="95d11-161">True</span></span><br/><span data-ttu-id="95d11-162">**False (valor predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="95d11-162">**False (default)**</span></span> |<span data-ttu-id="95d11-163">No</span><span class="sxs-lookup"><span data-stu-id="95d11-163">No</span></span> |
| <span data-ttu-id="95d11-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="95d11-164">skipLineCount</span></span> |<span data-ttu-id="95d11-165">Indica el número de filas que se omitirán al leer datos de archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="95d11-166">Si se especifican skipLineCount y firstRowAsHeader, las líneas se omiten primero y luego la información del encabezado se lee del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="95d11-167">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="95d11-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="95d11-168">Entero</span><span class="sxs-lookup"><span data-stu-id="95d11-168">Integer</span></span> |<span data-ttu-id="95d11-169">No</span><span class="sxs-lookup"><span data-stu-id="95d11-169">No</span></span> |
| <span data-ttu-id="95d11-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="95d11-170">treatEmptyAsNull</span></span> |<span data-ttu-id="95d11-171">Especifica si las cadenas null o vacías se tratarán como valores null al leer datos de un archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="95d11-172">**True (predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="95d11-172">**True (default)**</span></span><br/><span data-ttu-id="95d11-173">False</span><span class="sxs-lookup"><span data-stu-id="95d11-173">False</span></span> |<span data-ttu-id="95d11-174">No</span><span class="sxs-lookup"><span data-stu-id="95d11-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="95d11-175">Ejemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-175">TextFormat example</span></span>
<span data-ttu-id="95d11-176">En el ejemplo siguiente se muestran algunas de las propiedades de formato de TextFormat.</span><span class="sxs-lookup"><span data-stu-id="95d11-176">The following sample shows some of the format properties for TextFormat.</span></span>

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

<span data-ttu-id="95d11-177">Para usar un `escapeChar` en lugar de `quoteChar`, reemplace la línea con `quoteChar` por el siguiente escapeChar:</span><span class="sxs-lookup"><span data-stu-id="95d11-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="95d11-178">Escenarios de uso de firstRowAsHeader y skipLineCount</span><span class="sxs-lookup"><span data-stu-id="95d11-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="95d11-179">Va a copiar de un origen que no es archivo a un archivo de texto y quiere agregar una línea de encabezado que contenga los metadatos de esquema (por ejemplo, esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="95d11-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="95d11-180">Especifique `firstRowAsHeader` como true en el conjunto de datos de salida de este escenario.</span><span class="sxs-lookup"><span data-stu-id="95d11-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="95d11-181">Va a copiar de un archivo de texto que contiene una línea de encabezado a un receptor que no es archivo y quiere eliminar esa línea.</span><span class="sxs-lookup"><span data-stu-id="95d11-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="95d11-182">Especifique `firstRowAsHeader` como true en el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="95d11-183">Va a copiar de un archivo de texto y quiere omitir unas cuantas líneas al comienzo que no contienen datos ni información de encabezado.</span><span class="sxs-lookup"><span data-stu-id="95d11-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="95d11-184">Especifique `skipLineCount` para indicar el número de líneas que se omitirá.</span><span class="sxs-lookup"><span data-stu-id="95d11-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="95d11-185">Si el resto del archivo contiene una línea de encabezado, también puede especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="95d11-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="95d11-186">Si se especifican `skipLineCount` y `firstRowAsHeader`, las líneas se omiten primero y luego la información del encabezado se lee del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="95d11-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="95d11-187">Especificación de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-187">Specifying JsonFormat</span></span>
<span data-ttu-id="95d11-188">Para **importar y exportar archivos JSON tal como están hacia o desde Azure Cosmos DB**, consulte la sección sobre la [importación y exportación de documentos JSON](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) en el conector de Azure Cosmos DB para más información.</span><span class="sxs-lookup"><span data-stu-id="95d11-188">To **import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in the Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="95d11-189">Si desea analizar los archivos JSON o escribir los datos en formato JSON, establezca la propiedad `format` `type` en **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="95d11-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="95d11-190">También puede especificar las siguientes propiedades **opcionales** en la sección `format`.</span><span class="sxs-lookup"><span data-stu-id="95d11-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="95d11-191">Consulte la sección [Ejemplo de JsonFormat](#jsonformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="95d11-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="95d11-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="95d11-192">Property</span></span> | <span data-ttu-id="95d11-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="95d11-193">Description</span></span> | <span data-ttu-id="95d11-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="95d11-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95d11-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="95d11-195">filePattern</span></span> |<span data-ttu-id="95d11-196">Indica el patrón de los datos almacenados en cada archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="95d11-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="95d11-197">Estos son los valores permitidos: **setOfObjects** y **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="95d11-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="95d11-198">El valor **predeterminado** es **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="95d11-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="95d11-199">Consulte la sección [patrones de archivo JSON](#json-file-patterns) para obtener más información acerca de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="95d11-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="95d11-200">No</span><span class="sxs-lookup"><span data-stu-id="95d11-200">No</span></span> |
| <span data-ttu-id="95d11-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="95d11-201">jsonNodeReference</span></span> | <span data-ttu-id="95d11-202">Si desea iterar y extraer datos de los objetos dentro de un campo de matriz con el mismo patrón, especifique la ruta de acceso JSON de esa matriz.</span><span class="sxs-lookup"><span data-stu-id="95d11-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="95d11-203">Esta propiedad se admite solo cuando se copian datos desde los archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="95d11-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="95d11-204">No</span><span class="sxs-lookup"><span data-stu-id="95d11-204">No</span></span> |
| <span data-ttu-id="95d11-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="95d11-205">jsonPathDefinition</span></span> | <span data-ttu-id="95d11-206">Especifique la expresión de ruta de acceso JSON para cada asignación de columna con un nombre de columna personalizado (que empiece con minúscula).</span><span class="sxs-lookup"><span data-stu-id="95d11-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="95d11-207">Esta propiedad se admite solo cuando se copian datos desde archivos JSON y puede extraer datos del objeto o matriz.</span><span class="sxs-lookup"><span data-stu-id="95d11-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="95d11-208">Para los campos en el objeto raíz, comience por root $; para los campos dentro de la matriz elegida mediante la propiedad `jsonNodeReference`, empiece desde el elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="95d11-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="95d11-209">Consulte la sección [Ejemplo de JsonFormat](#jsonformat-example) sobre cómo realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="95d11-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="95d11-210">No</span><span class="sxs-lookup"><span data-stu-id="95d11-210">No</span></span> |
| <span data-ttu-id="95d11-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="95d11-211">encodingName</span></span> |<span data-ttu-id="95d11-212">Especifique el nombre de codificación.</span><span class="sxs-lookup"><span data-stu-id="95d11-212">Specify the encoding name.</span></span> <span data-ttu-id="95d11-213">Para obtener la lista de nombres de codificación válidos, vea el artículo sobre la propiedad [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="95d11-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="95d11-214">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="95d11-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="95d11-215">El valor **predeterminado** es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="95d11-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="95d11-216">No</span><span class="sxs-lookup"><span data-stu-id="95d11-216">No</span></span> |
| <span data-ttu-id="95d11-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="95d11-217">nestingSeparator</span></span> |<span data-ttu-id="95d11-218">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="95d11-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="95d11-219">El valor predeterminado es '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="95d11-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="95d11-220">No</span><span class="sxs-lookup"><span data-stu-id="95d11-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="95d11-221">Patrones de archivo JSON</span><span class="sxs-lookup"><span data-stu-id="95d11-221">JSON file patterns</span></span>

<span data-ttu-id="95d11-222">La actividad de copia puede analizar los siguientes patrones de archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="95d11-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="95d11-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="95d11-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="95d11-224">Cada archivo contiene un único objeto o bien varios objetos concatenados/delimitados por líneas.</span><span class="sxs-lookup"><span data-stu-id="95d11-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="95d11-225">Si se elige esta opción en un conjunto de datos de salida, la actividad de copia genera un único archivo JSON con cada objeto por línea (delimitado por líneas).</span><span class="sxs-lookup"><span data-stu-id="95d11-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="95d11-226">**ejemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="95d11-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="95d11-227">**ejemplo de JSON delimitado por líneas**</span><span class="sxs-lookup"><span data-stu-id="95d11-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="95d11-228">**ejemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="95d11-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="95d11-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="95d11-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="95d11-230">Cada archivo contiene una matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="95d11-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="95d11-231">Ejemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-231">JsonFormat example</span></span>

<span data-ttu-id="95d11-232">**Caso 1: Copia de datos desde archivos JSON**</span><span class="sxs-lookup"><span data-stu-id="95d11-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="95d11-233">Vea a continuación dos tipos de ejemplos en los que se copian datos desde archivos JSON, y los puntos de genéricos a tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="95d11-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="95d11-234">**Ejemplo 1: extracción de datos de objeto y matriz**</span><span class="sxs-lookup"><span data-stu-id="95d11-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="95d11-235">En esta ejemplo, se espera un objeto JSON de raíz que se asigna al registro individual en resultado tabulares.</span><span class="sxs-lookup"><span data-stu-id="95d11-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="95d11-236">Si tiene un archivo JSON con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="95d11-236">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="95d11-237">y quiere copiarlo en una tabla de SQL de Azure con el formato siguiente extrayendo datos tanto de los objetos como de la matriz:</span><span class="sxs-lookup"><span data-stu-id="95d11-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="95d11-238">id</span><span class="sxs-lookup"><span data-stu-id="95d11-238">id</span></span> | <span data-ttu-id="95d11-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="95d11-239">deviceType</span></span> | <span data-ttu-id="95d11-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="95d11-240">targetResourceType</span></span> | <span data-ttu-id="95d11-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="95d11-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="95d11-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="95d11-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="95d11-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="95d11-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="95d11-244">PC</span><span class="sxs-lookup"><span data-stu-id="95d11-244">PC</span></span> | <span data-ttu-id="95d11-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="95d11-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="95d11-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="95d11-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="95d11-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="95d11-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="95d11-248">El conjunto de datos de entrada con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="95d11-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="95d11-249">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="95d11-249">More specifically:</span></span>

- <span data-ttu-id="95d11-250">La sección `structure` permite definir los nombres personalizados de columna y el tipo de datos correspondiente mientras los convierte a datos tabulares.</span><span class="sxs-lookup"><span data-stu-id="95d11-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="95d11-251">Esta sección es **opcional** a menos que necesite realizar una asignación de columnas.</span><span class="sxs-lookup"><span data-stu-id="95d11-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="95d11-252">Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.</span><span class="sxs-lookup"><span data-stu-id="95d11-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="95d11-253">`jsonPathDefinition` especifica la ruta de acceso JSON para cada columna que indica de dónde se deben extraer los datos.</span><span class="sxs-lookup"><span data-stu-id="95d11-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="95d11-254">Para copiar datos de matriz, puede usar **array[x].property** para extraer el valor de la propiedad especificada desde el objeto xº, o puede usar **array[*] .property** para encontrar el valor de cualquier objeto que contenga dicha propiedad.</span><span class="sxs-lookup"><span data-stu-id="95d11-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="95d11-255">**Ejemplo 2: aplicación cruzada en varios objetos del mismo patrón de matriz**</span><span class="sxs-lookup"><span data-stu-id="95d11-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="95d11-256">En este ejemplo, se espera transformar un objeto JSON de raíz en varios registros en resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="95d11-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="95d11-257">Si tiene un archivo JSON con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="95d11-257">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="95d11-258">y desea copiarlo en una tabla de Azure SQL del formato siguiente, puede hacerlo mediante el acoplamiento de los datos dentro de la matriz y la combinación cruzada con la información de la raíz habitual:</span><span class="sxs-lookup"><span data-stu-id="95d11-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="95d11-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="95d11-259">ordernumber</span></span> | <span data-ttu-id="95d11-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="95d11-260">orderdate</span></span> | <span data-ttu-id="95d11-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="95d11-261">order_pd</span></span> | <span data-ttu-id="95d11-262">order_price</span><span class="sxs-lookup"><span data-stu-id="95d11-262">order_price</span></span> | <span data-ttu-id="95d11-263">city</span><span class="sxs-lookup"><span data-stu-id="95d11-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="95d11-264">01</span><span class="sxs-lookup"><span data-stu-id="95d11-264">01</span></span> | <span data-ttu-id="95d11-265">20170122</span><span class="sxs-lookup"><span data-stu-id="95d11-265">20170122</span></span> | <span data-ttu-id="95d11-266">P1</span><span class="sxs-lookup"><span data-stu-id="95d11-266">P1</span></span> | <span data-ttu-id="95d11-267">23</span><span class="sxs-lookup"><span data-stu-id="95d11-267">23</span></span> | <span data-ttu-id="95d11-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="95d11-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="95d11-269">01</span><span class="sxs-lookup"><span data-stu-id="95d11-269">01</span></span> | <span data-ttu-id="95d11-270">20170122</span><span class="sxs-lookup"><span data-stu-id="95d11-270">20170122</span></span> | <span data-ttu-id="95d11-271">P2</span><span class="sxs-lookup"><span data-stu-id="95d11-271">P2</span></span> | <span data-ttu-id="95d11-272">13</span><span class="sxs-lookup"><span data-stu-id="95d11-272">13</span></span> | <span data-ttu-id="95d11-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="95d11-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="95d11-274">01</span><span class="sxs-lookup"><span data-stu-id="95d11-274">01</span></span> | <span data-ttu-id="95d11-275">20170122</span><span class="sxs-lookup"><span data-stu-id="95d11-275">20170122</span></span> | <span data-ttu-id="95d11-276">P3</span><span class="sxs-lookup"><span data-stu-id="95d11-276">P3</span></span> | <span data-ttu-id="95d11-277">231</span><span class="sxs-lookup"><span data-stu-id="95d11-277">231</span></span> | <span data-ttu-id="95d11-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="95d11-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="95d11-279">El conjunto de datos de entrada con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="95d11-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="95d11-280">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="95d11-280">More specifically:</span></span>

- <span data-ttu-id="95d11-281">La sección `structure` permite definir los nombres personalizados de columna y el tipo de datos correspondiente mientras los convierte a datos tabulares.</span><span class="sxs-lookup"><span data-stu-id="95d11-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="95d11-282">Esta sección es **opcional** a menos que necesite realizar una asignación de columnas.</span><span class="sxs-lookup"><span data-stu-id="95d11-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="95d11-283">Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.</span><span class="sxs-lookup"><span data-stu-id="95d11-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="95d11-284">`jsonNodeReference` indica la iteración y extracción de datos de los objetos con el mismo patrón de las líneas de pedido de **matriz**.</span><span class="sxs-lookup"><span data-stu-id="95d11-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="95d11-285">`jsonPathDefinition` especifica la ruta de acceso JSON para cada columna que indica de dónde se deben extraer los datos.</span><span class="sxs-lookup"><span data-stu-id="95d11-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="95d11-286">En este ejemplo, "ordernumber", "orderdate" y "city" están bajo el objeto raíz con la ruta de acceso JSON que empieza por "$.", mientras que "order_pd" y "order_price" se definen con la ruta de acceso que se deriva del elemento de matriz sin "$.".</span><span class="sxs-lookup"><span data-stu-id="95d11-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="95d11-287">**Tenga en cuenta los siguientes puntos:**</span><span class="sxs-lookup"><span data-stu-id="95d11-287">**Note the following points:**</span></span>

* <span data-ttu-id="95d11-288">Si no se definen la `structure` y `jsonPathDefinition` en el conjunto de datos de Data Factory, la actividad de copia detecta el esquema del primer objeto y acopla el objeto en su conjunto.</span><span class="sxs-lookup"><span data-stu-id="95d11-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="95d11-289">Si la entrada JSON tiene una matriz, la actividad de copia convierte de forma predeterminada el valor de toda la matriz en una cadena.</span><span class="sxs-lookup"><span data-stu-id="95d11-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="95d11-290">Puede elegir extraer los datos de esta mediante `jsonNodeReference` o `jsonPathDefinition`, u omitir la extracción no especificándolo en `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="95d11-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="95d11-291">Si hay algún nombre duplicado en el mismo nivel, la actividad de copia elige el último.</span><span class="sxs-lookup"><span data-stu-id="95d11-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="95d11-292">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="95d11-292">Property names are case-sensitive.</span></span> <span data-ttu-id="95d11-293">Dos propiedades con el mismo nombre, pero con distintas mayúsculas y minúsculas se consideran propiedades independientes.</span><span class="sxs-lookup"><span data-stu-id="95d11-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="95d11-294">**Caso 2: Escritura de datos en el archivo JSON**</span><span class="sxs-lookup"><span data-stu-id="95d11-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="95d11-295">Si tiene la siguiente tabla en SQL Database:</span><span class="sxs-lookup"><span data-stu-id="95d11-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="95d11-296">id</span><span class="sxs-lookup"><span data-stu-id="95d11-296">id</span></span> | <span data-ttu-id="95d11-297">order_date</span><span class="sxs-lookup"><span data-stu-id="95d11-297">order_date</span></span> | <span data-ttu-id="95d11-298">order_price</span><span class="sxs-lookup"><span data-stu-id="95d11-298">order_price</span></span> | <span data-ttu-id="95d11-299">order_by</span><span class="sxs-lookup"><span data-stu-id="95d11-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="95d11-300">1</span><span class="sxs-lookup"><span data-stu-id="95d11-300">1</span></span> | <span data-ttu-id="95d11-301">20170119</span><span class="sxs-lookup"><span data-stu-id="95d11-301">20170119</span></span> | <span data-ttu-id="95d11-302">2000</span><span class="sxs-lookup"><span data-stu-id="95d11-302">2000</span></span> | <span data-ttu-id="95d11-303">David</span><span class="sxs-lookup"><span data-stu-id="95d11-303">David</span></span> |
| <span data-ttu-id="95d11-304">2</span><span class="sxs-lookup"><span data-stu-id="95d11-304">2</span></span> | <span data-ttu-id="95d11-305">20170120</span><span class="sxs-lookup"><span data-stu-id="95d11-305">20170120</span></span> | <span data-ttu-id="95d11-306">3500</span><span class="sxs-lookup"><span data-stu-id="95d11-306">3500</span></span> | <span data-ttu-id="95d11-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="95d11-307">Patrick</span></span> |
| <span data-ttu-id="95d11-308">3</span><span class="sxs-lookup"><span data-stu-id="95d11-308">3</span></span> | <span data-ttu-id="95d11-309">20170121</span><span class="sxs-lookup"><span data-stu-id="95d11-309">20170121</span></span> | <span data-ttu-id="95d11-310">4000</span><span class="sxs-lookup"><span data-stu-id="95d11-310">4000</span></span> | <span data-ttu-id="95d11-311">Jason</span><span class="sxs-lookup"><span data-stu-id="95d11-311">Jason</span></span> |

<span data-ttu-id="95d11-312">y para cada registro espera escribir en un objeto JSON con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d11-312">and for each record, you expect to write to a JSON object in below format:</span></span>
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

<span data-ttu-id="95d11-313">El conjunto de datos de salida con el tipo **JsonFormat** se define de la siguiente manera: (definición parcial en la que solo se ilustran las secciones relevantes).</span><span class="sxs-lookup"><span data-stu-id="95d11-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="95d11-314">Más concretamente, la sección `structure` permite definir los nombres personalizados de las propiedades en el archivo de destino, `nestingSeparator` (el valor predeterminado es ".") se usará para identificar el nivel de anidamiento del nombre.</span><span class="sxs-lookup"><span data-stu-id="95d11-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="95d11-315">Esta sección es **opcional** a menos que desee cambiar el nombre de la propiedad comparándolo con el nombre de la columna de origen, o anidar algunas de las propiedades.</span><span class="sxs-lookup"><span data-stu-id="95d11-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="95d11-316">Especificación de AvroFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-316">Specifying AvroFormat</span></span>
<span data-ttu-id="95d11-317">Si desea analizar los archivos Avro o escribir los datos en formato Avro, establezca la propiedad `format` `type` en **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="95d11-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="95d11-318">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="95d11-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="95d11-319">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="95d11-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="95d11-320">Para usar el formato Avro en una tabla de Hive, puede consultar [Tutorial de Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="95d11-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="95d11-321">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="95d11-321">Note the following points:</span></span>  

* <span data-ttu-id="95d11-322">No se admiten [tipos de datos complejos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumeraciones, matrices, asignaciones, uniones y fijos).</span><span class="sxs-lookup"><span data-stu-id="95d11-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="95d11-323">Especificación de OrcFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-323">Specifying OrcFormat</span></span>
<span data-ttu-id="95d11-324">Si desea analizar los archivos ORC o escribir los datos en formato ORC, establezca la propiedad `format` `type` en **ORCFormat**.</span><span class="sxs-lookup"><span data-stu-id="95d11-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="95d11-325">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="95d11-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="95d11-326">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="95d11-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="95d11-327">Si no va a copiar archivos ORC **como están** entre almacenes de datos locales y en la nube, debe instalar JRE 8 (Java Runtime Environment) en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="95d11-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="95d11-328">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="95d11-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="95d11-329">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="95d11-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="95d11-330">Elija la más adecuada.</span><span class="sxs-lookup"><span data-stu-id="95d11-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="95d11-331">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="95d11-331">Note the following points:</span></span>

* <span data-ttu-id="95d11-332">No se admiten tipos de daros complejos (STRUCT, MAP, LIST, UNION).</span><span class="sxs-lookup"><span data-stu-id="95d11-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="95d11-333">El archivo ORC tiene tres [opciones relacionadas con la compresión](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB y SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="95d11-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="95d11-334">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="95d11-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="95d11-335">Se utiliza el códec de compresión en los metadatos para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="95d11-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="95d11-336">Sin embargo, al escribir en un archivo ORC, Data Factory elige ZLIB que es el valor predeterminado para ORC.</span><span class="sxs-lookup"><span data-stu-id="95d11-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="95d11-337">Por el momento, no hay ninguna opción para invalidar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="95d11-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="95d11-338">Especificación de ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="95d11-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="95d11-339">Si desea analizar los archivos Parquet o escribir los datos en formato Parquet, establezca la propiedad `format` `type` en **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="95d11-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="95d11-340">No es preciso especificar propiedades en la sección Format de la sección typeProperties.</span><span class="sxs-lookup"><span data-stu-id="95d11-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="95d11-341">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="95d11-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="95d11-342">Si no va a copiar archivos Parquet **como están** entre almacenes de datos locales y en la nube, debe instalar JRE 8 (Java Runtime Environment) en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="95d11-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="95d11-343">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="95d11-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="95d11-344">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="95d11-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="95d11-345">Elija la más adecuada.</span><span class="sxs-lookup"><span data-stu-id="95d11-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="95d11-346">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="95d11-346">Note the following points:</span></span>

* <span data-ttu-id="95d11-347">No se admiten tipos de daros complejos (MAP, LIST).</span><span class="sxs-lookup"><span data-stu-id="95d11-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="95d11-348">El archivo Parquet tiene las siguientes opciones relacionadas con la compresión: NONE, SNAPPY, GZIP y LZO.</span><span class="sxs-lookup"><span data-stu-id="95d11-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="95d11-349">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="95d11-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="95d11-350">Utiliza el códec de compresión en los metadatos para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="95d11-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="95d11-351">Sin embargo, al escribir en un archivo Parquet, Data Factory elige SNAPPY que es el valor predeterminado para Parquet.</span><span class="sxs-lookup"><span data-stu-id="95d11-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="95d11-352">Por el momento, no hay ninguna opción para invalidar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="95d11-352">Currently, there is no option to override this behavior.</span></span>
