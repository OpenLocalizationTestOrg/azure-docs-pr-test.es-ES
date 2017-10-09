## <a name="specifying-formats"></a><span data-ttu-id="ab2df-101">Especificación de formatos</span><span class="sxs-lookup"><span data-stu-id="ab2df-101">Specifying formats</span></span>
<span data-ttu-id="ab2df-102">Factoría de datos de Azure admite Hola siguientes tipos de formato:</span><span class="sxs-lookup"><span data-stu-id="ab2df-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="ab2df-103">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="ab2df-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="ab2df-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="ab2df-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="ab2df-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="ab2df-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="ab2df-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="ab2df-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="ab2df-107">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="ab2df-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="ab2df-108">Especificación de TextFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-108">Specifying TextFormat</span></span>
<span data-ttu-id="ab2df-109">Si desea que los archivos de texto hello tooparse o escribir datos de hello en formato de texto, establezca hello `format` `type` propiedad demasiado**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="ab2df-110">También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección.</span><span class="sxs-lookup"><span data-stu-id="ab2df-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="ab2df-111">Vea [ejemplo TextFormat](#textformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ab2df-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="ab2df-112">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ab2df-112">Property</span></span> | <span data-ttu-id="ab2df-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab2df-113">Description</span></span> | <span data-ttu-id="ab2df-114">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ab2df-114">Allowed values</span></span> | <span data-ttu-id="ab2df-115">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ab2df-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab2df-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="ab2df-116">columnDelimiter</span></span> |<span data-ttu-id="ab2df-117">carácter de Hello usa tooseparate columnas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="ab2df-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="ab2df-118">Puede considerar toouse un char no pueden imprimirse poco frecuente que probablemente no existe en los datos: por ejemplo, especifique "\u0001" que representa el inicio de encabezado (SOH).</span><span class="sxs-lookup"><span data-stu-id="ab2df-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="ab2df-119">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="ab2df-119">Only one character is allowed.</span></span> <span data-ttu-id="ab2df-120">Hola **predeterminado** valor es **coma (',')**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="ab2df-121">toouse un carácter Unicode, consulte demasiado[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Hola código correspondiente para ella.</span><span class="sxs-lookup"><span data-stu-id="ab2df-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="ab2df-122">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-122">No</span></span> |
| <span data-ttu-id="ab2df-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="ab2df-123">rowDelimiter</span></span> |<span data-ttu-id="ab2df-124">carácter de Hello usa tooseparate filas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="ab2df-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="ab2df-125">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="ab2df-125">Only one character is allowed.</span></span> <span data-ttu-id="ab2df-126">Hola **predeterminado** valor es uno de los siguiente valores de lectura de Hola: **["\r\n", "\r", "\n"]** y **"\r\n"** durante la escritura.</span><span class="sxs-lookup"><span data-stu-id="ab2df-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="ab2df-127">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-127">No</span></span> |
| <span data-ttu-id="ab2df-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="ab2df-128">escapeChar</span></span> |<span data-ttu-id="ab2df-129">caracteres especiales de Hello utilizan tooescape un delimitador de columna en el contenido de hello del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="ab2df-130">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="ab2df-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="ab2df-131">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="ab2df-131">Only one character is allowed.</span></span> <span data-ttu-id="ab2df-132">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-132">No default value.</span></span> <br/><br/><span data-ttu-id="ab2df-133">Ejemplo: Si tienes por comas (', ') como delimitador de columna Hola pero desea toohave carácter de coma hello en texto hello (ejemplo: "Hello, world"), puede definir "$" como carácter de escape de Hola y utilizar la cadena "Hello$, world" en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="ab2df-134">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-134">No</span></span> |
| <span data-ttu-id="ab2df-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="ab2df-135">quoteChar</span></span> |<span data-ttu-id="ab2df-136">carácter de Hello usa tooquote un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="ab2df-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="ab2df-137">delimitadores de fila y columna de Hello dentro de los caracteres de comillas Hola se trataría como parte del valor de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="ab2df-138">Esta propiedad es aplicable tooboth entrada y salida de los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="ab2df-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="ab2df-139">No se puede especificar escapeChar y quoteChar para una tabla.</span><span class="sxs-lookup"><span data-stu-id="ab2df-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="ab2df-140">Solo se permite un carácter.</span><span class="sxs-lookup"><span data-stu-id="ab2df-140">Only one character is allowed.</span></span> <span data-ttu-id="ab2df-141">No hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-141">No default value.</span></span> <br/><br/><span data-ttu-id="ab2df-142">Por ejemplo, si tienes coma (', ') como delimitador de columna Hola pero desea toohave coma en texto hello (ejemplo: < Hola, mundo >), puede definir "(comillas dobles) como Hola delimitar caracteres y usar cadena de Hola"Hola, mundo"en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="ab2df-143">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-143">No</span></span> |
| <span data-ttu-id="ab2df-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="ab2df-144">nullValue</span></span> |<span data-ttu-id="ab2df-145">Uno o más caracteres utilizan toorepresent un valor null.</span><span class="sxs-lookup"><span data-stu-id="ab2df-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="ab2df-146">Uno o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="ab2df-146">One or more characters.</span></span> <span data-ttu-id="ab2df-147">Hola **predeterminado** valores son **"\N" y "NULL"** en lectura y **"\N"** durante la escritura.</span><span class="sxs-lookup"><span data-stu-id="ab2df-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="ab2df-148">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-148">No</span></span> |
| <span data-ttu-id="ab2df-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="ab2df-149">encodingName</span></span> |<span data-ttu-id="ab2df-150">Especifique el nombre de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-150">Specify hello encoding name.</span></span> |<span data-ttu-id="ab2df-151">Un nombre de codificación válido.</span><span class="sxs-lookup"><span data-stu-id="ab2df-151">A valid encoding name.</span></span> <span data-ttu-id="ab2df-152">Consulte la [propiedad Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab2df-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="ab2df-153">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="ab2df-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="ab2df-154">Hola **predeterminado** valor es **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="ab2df-155">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-155">No</span></span> |
| <span data-ttu-id="ab2df-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="ab2df-156">firstRowAsHeader</span></span> |<span data-ttu-id="ab2df-157">Especifica si tooconsider Hola la primera fila como un encabezado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="ab2df-158">Para un conjunto de datos de entrada, Data Factory lee la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="ab2df-159">Para un conjunto de datos de salida, Data Factory escribe la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="ab2df-160">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="ab2df-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="ab2df-161">True</span><span class="sxs-lookup"><span data-stu-id="ab2df-161">True</span></span><br/><span data-ttu-id="ab2df-162">**False (valor predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="ab2df-162">**False (default)**</span></span> |<span data-ttu-id="ab2df-163">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-163">No</span></span> |
| <span data-ttu-id="ab2df-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="ab2df-164">skipLineCount</span></span> |<span data-ttu-id="ab2df-165">Indica el número de Hola de filas tooskip al leer los datos de archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="ab2df-166">Si se especifican skipLineCount y firstRowAsHeader, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="ab2df-167">Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios.</span><span class="sxs-lookup"><span data-stu-id="ab2df-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="ab2df-168">Entero</span><span class="sxs-lookup"><span data-stu-id="ab2df-168">Integer</span></span> |<span data-ttu-id="ab2df-169">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-169">No</span></span> |
| <span data-ttu-id="ab2df-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="ab2df-170">treatEmptyAsNull</span></span> |<span data-ttu-id="ab2df-171">Especifica si hay tootreat una cadena nula o vacía como nula valor al leer los datos de un archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="ab2df-172">**True (predeterminado)**</span><span class="sxs-lookup"><span data-stu-id="ab2df-172">**True (default)**</span></span><br/><span data-ttu-id="ab2df-173">False</span><span class="sxs-lookup"><span data-stu-id="ab2df-173">False</span></span> |<span data-ttu-id="ab2df-174">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="ab2df-175">Ejemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-175">TextFormat example</span></span>
<span data-ttu-id="ab2df-176">Hello en el ejemplo siguiente muestra algunas de las propiedades de formato de Hola para TextFormat.</span><span class="sxs-lookup"><span data-stu-id="ab2df-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="ab2df-177">toouse una `escapeChar` en lugar de `quoteChar`, reemplace la línea hello con `quoteChar` con hello después de escapeChar:</span><span class="sxs-lookup"><span data-stu-id="ab2df-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="ab2df-178">Escenarios de uso de firstRowAsHeader y skipLineCount</span><span class="sxs-lookup"><span data-stu-id="ab2df-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="ab2df-179">Va a copiar de un archivo de texto de origen no es un archivo tooa y desearía tooadd una línea de encabezado que contiene los metadatos del esquema de hello (por ejemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="ab2df-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="ab2df-180">Especificar `firstRowAsHeader` como true en el conjunto de datos de salida de hello para este escenario.</span><span class="sxs-lookup"><span data-stu-id="ab2df-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="ab2df-181">Va a copiar de un archivo de texto que contiene un receptor no es un archivo de encabezado línea tooa y desearía toodrop que línea.</span><span class="sxs-lookup"><span data-stu-id="ab2df-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="ab2df-182">Especificar `firstRowAsHeader` como true en el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="ab2df-183">Va a copiar desde un archivo de texto y desea tooskip unas cuantas líneas al principio de Hola que no contienen ninguna información de datos o de encabezado.</span><span class="sxs-lookup"><span data-stu-id="ab2df-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="ab2df-184">Especifique `skipLineCount` tooindicate Hola número de líneas toobe omitidos.</span><span class="sxs-lookup"><span data-stu-id="ab2df-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="ab2df-185">Si el resto de hello del archivo hello contiene una línea de encabezado, también puede especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="ab2df-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="ab2df-186">Si ambos `skipLineCount` y `firstRowAsHeader` se especifican, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada</span><span class="sxs-lookup"><span data-stu-id="ab2df-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="ab2df-187">Especificación de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-187">Specifying JsonFormat</span></span>
<span data-ttu-id="ab2df-188">demasiado**importación y exportación de archivos JSON como-está en/desde la base de datos de Azure Cosmos**, consulte [documentos JSON de importación y exportación](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sección en Conector de base de datos de Azure Cosmos Hola con detalles.</span><span class="sxs-lookup"><span data-stu-id="ab2df-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="ab2df-189">Si desea tooparse Hola JSON archivos o escribir datos de hello en formato JSON, establezca hello `format` `type` propiedad demasiado**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="ab2df-190">También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección.</span><span class="sxs-lookup"><span data-stu-id="ab2df-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="ab2df-191">Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ab2df-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="ab2df-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ab2df-192">Property</span></span> | <span data-ttu-id="ab2df-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab2df-193">Description</span></span> | <span data-ttu-id="ab2df-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ab2df-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab2df-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="ab2df-195">filePattern</span></span> |<span data-ttu-id="ab2df-196">Indicar el patrón de Hola de los datos almacenados en cada archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="ab2df-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="ab2df-197">Estos son los valores permitidos: **setOfObjects** y **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="ab2df-198">Hola **predeterminado** valor es **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="ab2df-199">Consulte la sección [patrones de archivo JSON](#json-file-patterns) para obtener más información acerca de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="ab2df-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="ab2df-200">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-200">No</span></span> |
| <span data-ttu-id="ab2df-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="ab2df-201">jsonNodeReference</span></span> | <span data-ttu-id="ab2df-202">Si desea tooiterate y extraer datos de objetos de hello dentro de una matriz de campo con hello mismo patrón, especifique la ruta de acceso de hello JSON de dicha matriz.</span><span class="sxs-lookup"><span data-stu-id="ab2df-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="ab2df-203">Esta propiedad se admite solo cuando se copian datos desde los archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="ab2df-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="ab2df-204">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-204">No</span></span> |
| <span data-ttu-id="ab2df-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="ab2df-205">jsonPathDefinition</span></span> | <span data-ttu-id="ab2df-206">Especifique la expresión de ruta de acceso de hello JSON para cada asignación de columna con un nombre de columna personalizada (comienzan con minúscula).</span><span class="sxs-lookup"><span data-stu-id="ab2df-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="ab2df-207">Esta propiedad se admite solo cuando se copian datos desde archivos JSON y puede extraer datos del objeto o matriz.</span><span class="sxs-lookup"><span data-stu-id="ab2df-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="ab2df-208">Para los campos en el objeto raíz, comenzar por $ de raíz; para los campos dentro de la matriz de hello elegida por `jsonNodeReference` propiedad, inicio de elemento de la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="ab2df-209">Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ab2df-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="ab2df-210">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-210">No</span></span> |
| <span data-ttu-id="ab2df-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="ab2df-211">encodingName</span></span> |<span data-ttu-id="ab2df-212">Especifique el nombre de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-212">Specify hello encoding name.</span></span> <span data-ttu-id="ab2df-213">Para hello lista de nombres de codificación válidos, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propiedad.</span><span class="sxs-lookup"><span data-stu-id="ab2df-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="ab2df-214">Por ejemplo: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="ab2df-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="ab2df-215">Hola **predeterminado** valor es: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="ab2df-216">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-216">No</span></span> |
| <span data-ttu-id="ab2df-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ab2df-217">nestingSeparator</span></span> |<span data-ttu-id="ab2df-218">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="ab2df-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="ab2df-219">valor predeterminado de Hello es '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="ab2df-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="ab2df-220">No</span><span class="sxs-lookup"><span data-stu-id="ab2df-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="ab2df-221">Patrones de archivo JSON</span><span class="sxs-lookup"><span data-stu-id="ab2df-221">JSON file patterns</span></span>

<span data-ttu-id="ab2df-222">La actividad de copia puede analizar los siguientes patrones de archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="ab2df-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="ab2df-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="ab2df-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="ab2df-224">Cada archivo contiene un único objeto o bien varios objetos concatenados/delimitados por líneas.</span><span class="sxs-lookup"><span data-stu-id="ab2df-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="ab2df-225">Si se elige esta opción en un conjunto de datos de salida, la actividad de copia genera un único archivo JSON con cada objeto por línea (delimitado por líneas).</span><span class="sxs-lookup"><span data-stu-id="ab2df-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="ab2df-226">**ejemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="ab2df-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="ab2df-227">**ejemplo de JSON delimitado por líneas**</span><span class="sxs-lookup"><span data-stu-id="ab2df-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="ab2df-228">**ejemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="ab2df-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="ab2df-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="ab2df-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="ab2df-230">Cada archivo contiene una matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="ab2df-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="ab2df-231">Ejemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-231">JsonFormat example</span></span>

<span data-ttu-id="ab2df-232">**Caso 1: Copia de datos desde archivos JSON**</span><span class="sxs-lookup"><span data-stu-id="ab2df-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="ab2df-233">Vea a continuación de los dos tipos de muestras cuando se copian datos desde archivos JSON y Hola toonote puntos genérico:</span><span class="sxs-lookup"><span data-stu-id="ab2df-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="ab2df-234">**Ejemplo 1: extracción de datos de objeto y matriz**</span><span class="sxs-lookup"><span data-stu-id="ab2df-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="ab2df-235">En este ejemplo, espera un objeto JSON de raíz asigna el registro de toosingle de resultados tabulares.</span><span class="sxs-lookup"><span data-stu-id="ab2df-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="ab2df-236">Si tiene un archivo JSON con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="ab2df-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="ab2df-237">y desea que toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, extrayendo datos de objeto y matriz:</span><span class="sxs-lookup"><span data-stu-id="ab2df-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="ab2df-238">id</span><span class="sxs-lookup"><span data-stu-id="ab2df-238">id</span></span> | <span data-ttu-id="ab2df-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="ab2df-239">deviceType</span></span> | <span data-ttu-id="ab2df-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="ab2df-240">targetResourceType</span></span> | <span data-ttu-id="ab2df-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="ab2df-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="ab2df-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="ab2df-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ab2df-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="ab2df-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="ab2df-244">PC</span><span class="sxs-lookup"><span data-stu-id="ab2df-244">PC</span></span> | <span data-ttu-id="ab2df-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="ab2df-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="ab2df-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="ab2df-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="ab2df-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="ab2df-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="ab2df-248">conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="ab2df-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="ab2df-249">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="ab2df-249">More specifically:</span></span>

- <span data-ttu-id="ab2df-250">`structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular.</span><span class="sxs-lookup"><span data-stu-id="ab2df-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="ab2df-251">Esta sección es **opcional** a menos que necesite toodo asignación de columna.</span><span class="sxs-lookup"><span data-stu-id="ab2df-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="ab2df-252">Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.</span><span class="sxs-lookup"><span data-stu-id="ab2df-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="ab2df-253">`jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de.</span><span class="sxs-lookup"><span data-stu-id="ab2df-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="ab2df-254">toocopy datos de matriz, puede usar **.property de matriz [x]** tooextract valo Hola dada la propiedad de objeto de x-ésima de hello, o se puede usar  **matriz [*] .property** toofind valor de Hola de cualquier objeto que contiene dicha propiedad.</span><span class="sxs-lookup"><span data-stu-id="ab2df-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="ab2df-255">**Ejemplo 2: cross aplicar varios objetos con el mismo patrón de matriz de Hola**</span><span class="sxs-lookup"><span data-stu-id="ab2df-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="ab2df-256">En este ejemplo, espera un objeto JSON raíz tootransform en varios registros en los resultados tabulares.</span><span class="sxs-lookup"><span data-stu-id="ab2df-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="ab2df-257">Si tiene un archivo JSON con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="ab2df-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="ab2df-258">y desea toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, acoplando datos Hola dentro de la matriz de Hola y cross join con información de raíz común de hello:</span><span class="sxs-lookup"><span data-stu-id="ab2df-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="ab2df-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="ab2df-259">ordernumber</span></span> | <span data-ttu-id="ab2df-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="ab2df-260">orderdate</span></span> | <span data-ttu-id="ab2df-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="ab2df-261">order_pd</span></span> | <span data-ttu-id="ab2df-262">order_price</span><span class="sxs-lookup"><span data-stu-id="ab2df-262">order_price</span></span> | <span data-ttu-id="ab2df-263">city</span><span class="sxs-lookup"><span data-stu-id="ab2df-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ab2df-264">01</span><span class="sxs-lookup"><span data-stu-id="ab2df-264">01</span></span> | <span data-ttu-id="ab2df-265">20170122</span><span class="sxs-lookup"><span data-stu-id="ab2df-265">20170122</span></span> | <span data-ttu-id="ab2df-266">P1</span><span class="sxs-lookup"><span data-stu-id="ab2df-266">P1</span></span> | <span data-ttu-id="ab2df-267">23</span><span class="sxs-lookup"><span data-stu-id="ab2df-267">23</span></span> | <span data-ttu-id="ab2df-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ab2df-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="ab2df-269">01</span><span class="sxs-lookup"><span data-stu-id="ab2df-269">01</span></span> | <span data-ttu-id="ab2df-270">20170122</span><span class="sxs-lookup"><span data-stu-id="ab2df-270">20170122</span></span> | <span data-ttu-id="ab2df-271">P2</span><span class="sxs-lookup"><span data-stu-id="ab2df-271">P2</span></span> | <span data-ttu-id="ab2df-272">13</span><span class="sxs-lookup"><span data-stu-id="ab2df-272">13</span></span> | <span data-ttu-id="ab2df-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ab2df-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="ab2df-274">01</span><span class="sxs-lookup"><span data-stu-id="ab2df-274">01</span></span> | <span data-ttu-id="ab2df-275">20170122</span><span class="sxs-lookup"><span data-stu-id="ab2df-275">20170122</span></span> | <span data-ttu-id="ab2df-276">P3</span><span class="sxs-lookup"><span data-stu-id="ab2df-276">P3</span></span> | <span data-ttu-id="ab2df-277">231</span><span class="sxs-lookup"><span data-stu-id="ab2df-277">231</span></span> | <span data-ttu-id="ab2df-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ab2df-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="ab2df-279">conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="ab2df-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="ab2df-280">Más concretamente:</span><span class="sxs-lookup"><span data-stu-id="ab2df-280">More specifically:</span></span>

- <span data-ttu-id="ab2df-281">`structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular.</span><span class="sxs-lookup"><span data-stu-id="ab2df-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="ab2df-282">Esta sección es **opcional** a menos que necesite toodo asignación de columna.</span><span class="sxs-lookup"><span data-stu-id="ab2df-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="ab2df-283">Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.</span><span class="sxs-lookup"><span data-stu-id="ab2df-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="ab2df-284">`jsonNodeReference`indica datos tooiterate y la extracción de objetos de hello con hello mismo patrón en **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="ab2df-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="ab2df-285">`jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de.</span><span class="sxs-lookup"><span data-stu-id="ab2df-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="ab2df-286">En este ejemplo, "ordernumber", "orderdate" y "city" están bajo el objeto raíz con la ruta de acceso JSON a partir de "$.", mientras que "order_pd" y "order_price" se definen con la ruta de acceso que se deriva de elemento de la matriz de hello sin "$"..</span><span class="sxs-lookup"><span data-stu-id="ab2df-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="ab2df-287">**Tenga en cuenta Hola siguientes puntos:**</span><span class="sxs-lookup"><span data-stu-id="ab2df-287">**Note hello following points:**</span></span>

* <span data-ttu-id="ab2df-288">Si hello `structure` y `jsonPathDefinition` no estén definidos en conjunto de datos de Data Factory de hello, hello actividad de copia detecta Hola esquema desde el primer objeto de Hola y simplificar el objeto entero Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="ab2df-289">Si la entrada JSON de hello tiene una matriz, de forma predeterminada Hola actividad de copia convierte valor de la matriz completa de hello en una cadena.</span><span class="sxs-lookup"><span data-stu-id="ab2df-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="ab2df-290">Puede elegir tooextract datos de mediante `jsonNodeReference` o `jsonPathDefinition`, u omita especificándolo no en `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="ab2df-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="ab2df-291">Si hay duplicados Hola de nombres en el mismo nivel, Hola actividad de copia toma Hola último.</span><span class="sxs-lookup"><span data-stu-id="ab2df-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="ab2df-292">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ab2df-292">Property names are case-sensitive.</span></span> <span data-ttu-id="ab2df-293">Dos propiedades con el mismo nombre, pero con distintas mayúsculas y minúsculas se consideran propiedades independientes.</span><span class="sxs-lookup"><span data-stu-id="ab2df-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="ab2df-294">**Caso 2: Escribir datos tooJSON en el archivo**</span><span class="sxs-lookup"><span data-stu-id="ab2df-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="ab2df-295">Si tiene la siguiente tabla en SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ab2df-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="ab2df-296">id</span><span class="sxs-lookup"><span data-stu-id="ab2df-296">id</span></span> | <span data-ttu-id="ab2df-297">order_date</span><span class="sxs-lookup"><span data-stu-id="ab2df-297">order_date</span></span> | <span data-ttu-id="ab2df-298">order_price</span><span class="sxs-lookup"><span data-stu-id="ab2df-298">order_price</span></span> | <span data-ttu-id="ab2df-299">order_by</span><span class="sxs-lookup"><span data-stu-id="ab2df-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab2df-300">1</span><span class="sxs-lookup"><span data-stu-id="ab2df-300">1</span></span> | <span data-ttu-id="ab2df-301">20170119</span><span class="sxs-lookup"><span data-stu-id="ab2df-301">20170119</span></span> | <span data-ttu-id="ab2df-302">2000</span><span class="sxs-lookup"><span data-stu-id="ab2df-302">2000</span></span> | <span data-ttu-id="ab2df-303">David</span><span class="sxs-lookup"><span data-stu-id="ab2df-303">David</span></span> |
| <span data-ttu-id="ab2df-304">2</span><span class="sxs-lookup"><span data-stu-id="ab2df-304">2</span></span> | <span data-ttu-id="ab2df-305">20170120</span><span class="sxs-lookup"><span data-stu-id="ab2df-305">20170120</span></span> | <span data-ttu-id="ab2df-306">3500</span><span class="sxs-lookup"><span data-stu-id="ab2df-306">3500</span></span> | <span data-ttu-id="ab2df-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="ab2df-307">Patrick</span></span> |
| <span data-ttu-id="ab2df-308">3</span><span class="sxs-lookup"><span data-stu-id="ab2df-308">3</span></span> | <span data-ttu-id="ab2df-309">20170121</span><span class="sxs-lookup"><span data-stu-id="ab2df-309">20170121</span></span> | <span data-ttu-id="ab2df-310">4000</span><span class="sxs-lookup"><span data-stu-id="ab2df-310">4000</span></span> | <span data-ttu-id="ab2df-311">Jason</span><span class="sxs-lookup"><span data-stu-id="ab2df-311">Jason</span></span> |

<span data-ttu-id="ab2df-312">y para cada registro, espera que toowrite tooa JSON objeto en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="ab2df-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="ab2df-313">con el conjunto de datos de salida de Hello **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello).</span><span class="sxs-lookup"><span data-stu-id="ab2df-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="ab2df-314">Más específicamente, `structure` sección define los nombres de propiedad Hola personalizado en el archivo de destino, `nestingSeparator` (valor predeterminado es ".") será la capa de anidamiento de hello tooidentify usado desde nombre hello.</span><span class="sxs-lookup"><span data-stu-id="ab2df-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="ab2df-315">Esta sección es **opcional** a menos que se desea el nombre de la propiedad de hello toochange comparar con el nombre de la columna de origen o anidar algunas de las propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="ab2df-316">Especificación de AvroFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-316">Specifying AvroFormat</span></span>
<span data-ttu-id="ab2df-317">Si desea tooparse hello Avro archivos o escribir datos de hello en el formato Avro, establezca hello `format` `type` propiedad demasiado**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="ab2df-318">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="ab2df-319">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab2df-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="ab2df-320">toouse el formato Avro en una tabla de Hive, puede hacer referencia demasiado[tutorial de Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="ab2df-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="ab2df-321">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="ab2df-321">Note hello following points:</span></span>  

* <span data-ttu-id="ab2df-322">No se admiten [tipos de datos complejos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumeraciones, matrices, asignaciones, uniones y fijos).</span><span class="sxs-lookup"><span data-stu-id="ab2df-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="ab2df-323">Especificación de OrcFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-323">Specifying OrcFormat</span></span>
<span data-ttu-id="ab2df-324">Si desea tooparse Hola ORC archivos o escribir datos de hello en formato ORC, Establece hello `format` `type` propiedad demasiado**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="ab2df-325">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="ab2df-326">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab2df-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="ab2df-327">Si no va a copiar archivos ORC **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ab2df-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="ab2df-328">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="ab2df-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="ab2df-329">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="ab2df-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="ab2df-330">Elija Hola adecuada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="ab2df-331">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="ab2df-331">Note hello following points:</span></span>

* <span data-ttu-id="ab2df-332">No se admiten tipos de daros complejos (STRUCT, MAP, LIST, UNION).</span><span class="sxs-lookup"><span data-stu-id="ab2df-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="ab2df-333">El archivo ORC tiene tres [opciones relacionadas con la compresión](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB y SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="ab2df-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="ab2df-334">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="ab2df-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="ab2df-335">Utiliza la compresión de hello códec está en datos de saludo metadatos tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="ab2df-336">Sin embargo, al escribir un archivo de tooan ORC, factoría de datos elige ZLIB, que es el valor predeterminado de Hola para ORC.</span><span class="sxs-lookup"><span data-stu-id="ab2df-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="ab2df-337">Actualmente no hay ninguna opción toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="ab2df-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="ab2df-338">Especificación de ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="ab2df-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="ab2df-339">Si desea tooparse Hola Parquet archivos o escribir datos de hello en formato Parquet, Establece hello `format` `type` propiedad demasiado**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ab2df-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="ab2df-340">No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="ab2df-341">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab2df-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="ab2df-342">Si no va a copiar archivos Parquet **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ab2df-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="ab2df-343">Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="ab2df-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="ab2df-344">Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="ab2df-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="ab2df-345">Elija Hola adecuada.</span><span class="sxs-lookup"><span data-stu-id="ab2df-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="ab2df-346">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="ab2df-346">Note hello following points:</span></span>

* <span data-ttu-id="ab2df-347">No se admiten tipos de daros complejos (MAP, LIST).</span><span class="sxs-lookup"><span data-stu-id="ab2df-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="ab2df-348">Archivo parquet tiene Hola siguientes opciones de compresión: ninguno, SNAPPY, GZIP y LZO.</span><span class="sxs-lookup"><span data-stu-id="ab2df-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="ab2df-349">Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="ab2df-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="ab2df-350">Usa códec de compresión de hello en datos de saludo metadatos tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2df-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="ab2df-351">Sin embargo, al escribir un archivo de Parquet tooa, factoría de datos elige SNAPPY, que es el predeterminado de hello para el formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="ab2df-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="ab2df-352">Actualmente no hay ninguna opción toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="ab2df-352">Currently, there is no option toooverride this behavior.</span></span>
