## <a name="specifying-formats"></a>Especificación de formatos
Factoría de datos de Azure admite Hola siguientes tipos de formato:

* [Formato de texto](#specifying-textformat)
* [Formato JSON](#specifying-jsonformat)
* [Formato Avro](#specifying-avroformat)
* [Formato ORC](#specifying-orcformat)
* [Formato Parquet](#specifying-parquetformat)

### <a name="specifying-textformat"></a>Especificación de TextFormat
Si desea que los archivos de texto hello tooparse o escribir datos de hello en formato de texto, establezca hello `format` `type` propiedad demasiado**TextFormat**. También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección. Vea [ejemplo TextFormat](#textformat-example) sección sobre cómo tooconfigure.

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| columnDelimiter |carácter de Hello usa tooseparate columnas en un archivo. Puede considerar toouse un char no pueden imprimirse poco frecuente que probablemente no existe en los datos: por ejemplo, especifique "\u0001" que representa el inicio de encabezado (SOH). |Solo se permite un carácter. Hola **predeterminado** valor es **coma (',')**. <br/><br/>toouse un carácter Unicode, consulte demasiado[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Hola código correspondiente para ella. |No |
| rowDelimiter |carácter de Hello usa tooseparate filas en un archivo. |Solo se permite un carácter. Hola **predeterminado** valor es uno de los siguiente valores de lectura de Hola: **["\r\n", "\r", "\n"]** y **"\r\n"** durante la escritura. |No |
| escapeChar |caracteres especiales de Hello utilizan tooescape un delimitador de columna en el contenido de hello del archivo de entrada. <br/><br/>No se puede especificar escapeChar y quoteChar para una tabla. |Solo se permite un carácter. No hay ningún valor predeterminado. <br/><br/>Ejemplo: Si tienes por comas (', ') como delimitador de columna Hola pero desea toohave carácter de coma hello en texto hello (ejemplo: "Hello, world"), puede definir "$" como carácter de escape de Hola y utilizar la cadena "Hello$, world" en el origen de Hola. |No |
| quoteChar |carácter de Hello usa tooquote un valor de cadena. delimitadores de fila y columna de Hello dentro de los caracteres de comillas Hola se trataría como parte del valor de cadena de Hola. Esta propiedad es aplicable tooboth entrada y salida de los conjuntos de datos.<br/><br/>No se puede especificar escapeChar y quoteChar para una tabla. |Solo se permite un carácter. No hay ningún valor predeterminado. <br/><br/>Por ejemplo, si tienes coma (', ') como delimitador de columna Hola pero desea toohave coma en texto hello (ejemplo: < Hola, mundo >), puede definir "(comillas dobles) como Hola delimitar caracteres y usar cadena de Hola"Hola, mundo"en el origen de Hola. |No |
| nullValue |Uno o más caracteres utilizan toorepresent un valor null. |Uno o más caracteres. Hola **predeterminado** valores son **"\N" y "NULL"** en lectura y **"\N"** durante la escritura. |No |
| encodingName |Especifique el nombre de codificación de Hola. |Un nombre de codificación válido. Consulte la [propiedad Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Por ejemplo: windows-1250 o shift_jis. Hola **predeterminado** valor es **UTF-8**. |No |
| firstRowAsHeader |Especifica si tooconsider Hola la primera fila como un encabezado. Para un conjunto de datos de entrada, Data Factory lee la primera fila como encabezado. Para un conjunto de datos de salida, Data Factory escribe la primera fila como encabezado. <br/><br/>Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios. |True<br/>**False (valor predeterminado)** |No |
| skipLineCount |Indica el número de Hola de filas tooskip al leer los datos de archivos de entrada. Si se especifican skipLineCount y firstRowAsHeader, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada. <br/><br/>Consulte [Escenarios de uso `firstRowAsHeader` y `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para ver ejemplos de escenarios. |Entero |No |
| treatEmptyAsNull |Especifica si hay tootreat una cadena nula o vacía como nula valor al leer los datos de un archivo de entrada. |**True (predeterminado)**<br/>False |No |

#### <a name="textformat-example"></a>Ejemplo de TextFormat
Hello en el ejemplo siguiente muestra algunas de las propiedades de formato de Hola para TextFormat.

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

toouse una `escapeChar` en lugar de `quoteChar`, reemplace la línea hello con `quoteChar` con hello después de escapeChar:

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Escenarios de uso de firstRowAsHeader y skipLineCount
* Va a copiar de un archivo de texto de origen no es un archivo tooa y desearía tooadd una línea de encabezado que contiene los metadatos del esquema de hello (por ejemplo: esquema SQL). Especificar `firstRowAsHeader` como true en el conjunto de datos de salida de hello para este escenario.
* Va a copiar de un archivo de texto que contiene un receptor no es un archivo de encabezado línea tooa y desearía toodrop que línea. Especificar `firstRowAsHeader` como true en el conjunto de datos de entrada de Hola.
* Va a copiar desde un archivo de texto y desea tooskip unas cuantas líneas al principio de Hola que no contienen ninguna información de datos o de encabezado. Especifique `skipLineCount` tooindicate Hola número de líneas toobe omitidos. Si el resto de hello del archivo hello contiene una línea de encabezado, también puede especificar `firstRowAsHeader`. Si ambos `skipLineCount` y `firstRowAsHeader` se especifican, líneas de saludo se omiten en primer lugar y, a continuación, se lee información de encabezado de Hola Hola archivo de entrada

### <a name="specifying-jsonformat"></a>Especificación de JsonFormat
demasiado**importación y exportación de archivos JSON como-está en/desde la base de datos de Azure Cosmos**, consulte [documentos JSON de importación y exportación](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sección en Conector de base de datos de Azure Cosmos Hola con detalles.

Si desea tooparse Hola JSON archivos o escribir datos de hello en formato JSON, establezca hello `format` `type` propiedad demasiado**JsonFormat**. También puede especificar Hola siguiente **opcional** propiedades Hola `format` sección. Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| filePattern |Indicar el patrón de Hola de los datos almacenados en cada archivo JSON. Estos son los valores permitidos: **setOfObjects** y **arrayOfObjects**. Hola **predeterminado** valor es **setOfObjects**. Consulte la sección [patrones de archivo JSON](#json-file-patterns) para obtener más información acerca de estos patrones. |No |
| jsonNodeReference | Si desea tooiterate y extraer datos de objetos de hello dentro de una matriz de campo con hello mismo patrón, especifique la ruta de acceso de hello JSON de dicha matriz. Esta propiedad se admite solo cuando se copian datos desde los archivos JSON. | No |
| jsonPathDefinition | Especifique la expresión de ruta de acceso de hello JSON para cada asignación de columna con un nombre de columna personalizada (comienzan con minúscula). Esta propiedad se admite solo cuando se copian datos desde archivos JSON y puede extraer datos del objeto o matriz. <br/><br/> Para los campos en el objeto raíz, comenzar por $ de raíz; para los campos dentro de la matriz de hello elegida por `jsonNodeReference` propiedad, inicio de elemento de la matriz de Hola. Vea [JsonFormat ejemplo](#jsonformat-example) sección sobre cómo tooconfigure. | No |
| encodingName |Especifique el nombre de codificación de Hola. Para hello lista de nombres de codificación válidos, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propiedad. Por ejemplo: windows-1250 o shift_jis. Hola **predeterminado** valor es: **UTF-8**. |No |
| nestingSeparator |Carácter que es usado tooseparate niveles de anidamiento. valor predeterminado de Hello es '.' (punto). |No |

#### <a name="json-file-patterns"></a>Patrones de archivo JSON

La actividad de copia puede analizar los siguientes patrones de archivos JSON:

- **Tipo I: setOfObjects**

    Cada archivo contiene un único objeto o bien varios objetos concatenados/delimitados por líneas. Si se elige esta opción en un conjunto de datos de salida, la actividad de copia genera un único archivo JSON con cada objeto por línea (delimitado por líneas).

    * **ejemplo de JSON de objeto único**

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

    * **ejemplo de JSON delimitado por líneas**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **ejemplo de JSON concatenado**

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

- **Tipo II: arrayOfObjects**

    Cada archivo contiene una matriz de objetos.

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

#### <a name="jsonformat-example"></a>Ejemplo de JsonFormat

**Caso 1: Copia de datos desde archivos JSON**

Vea a continuación de los dos tipos de muestras cuando se copian datos desde archivos JSON y Hola toonote puntos genérico:

**Ejemplo 1: extracción de datos de objeto y matriz**

En este ejemplo, espera un objeto JSON de raíz asigna el registro de toosingle de resultados tabulares. Si tiene un archivo JSON con hello siguen contenido:  

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
y desea que toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, extrayendo datos de objeto y matriz:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello). Más concretamente:

- `structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular. Esta sección es **opcional** a menos que necesite toodo asignación de columna. Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.
- `jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de. toocopy datos de matriz, puede usar **.property de matriz [x]** tooextract valo Hola dada la propiedad de objeto de x-ésima de hello, o se puede usar  **matriz [*] .property** toofind valor de Hola de cualquier objeto que contiene dicha propiedad.

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

**Ejemplo 2: cross aplicar varios objetos con el mismo patrón de matriz de Hola**

En este ejemplo, espera un objeto JSON raíz tootransform en varios registros en los resultados tabulares. Si tiene un archivo JSON con hello siguen contenido:  

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
y desea toocopy en una tabla de SQL Azure en la siguiente Hola dar formato, acoplando datos Hola dentro de la matriz de Hola y cross join con información de raíz común de hello:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

conjunto de datos de entrada de Hello con **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello). Más concretamente:

- `structure`sección define Hola personalizado los nombres de columna y el tipo de datos correspondiente de hello al convertir datos tootabular. Esta sección es **opcional** a menos que necesite toodo asignación de columna. Consulte [Especificación de la definición de la estructura de los conjuntos de datos rectangulares](#specifying-structure-definition-for-rectangular-datasets) para más información.
- `jsonNodeReference`indica datos tooiterate y la extracción de objetos de hello con hello mismo patrón en **matriz** orderlines.
- `jsonPathDefinition`Especifica la ruta de acceso JSON de Hola para cada columna que indica donde tooextract Hola datos de. En este ejemplo, "ordernumber", "orderdate" y "city" están bajo el objeto raíz con la ruta de acceso JSON a partir de "$.", mientras que "order_pd" y "order_price" se definen con la ruta de acceso que se deriva de elemento de la matriz de hello sin "$"..

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

**Tenga en cuenta Hola siguientes puntos:**

* Si hello `structure` y `jsonPathDefinition` no estén definidos en conjunto de datos de Data Factory de hello, hello actividad de copia detecta Hola esquema desde el primer objeto de Hola y simplificar el objeto entero Hola.
* Si la entrada JSON de hello tiene una matriz, de forma predeterminada Hola actividad de copia convierte valor de la matriz completa de hello en una cadena. Puede elegir tooextract datos de mediante `jsonNodeReference` o `jsonPathDefinition`, u omita especificándolo no en `jsonPathDefinition`.
* Si hay duplicados Hola de nombres en el mismo nivel, Hola actividad de copia toma Hola último.
* Los nombres de propiedad distinguen entre mayúsculas y minúsculas. Dos propiedades con el mismo nombre, pero con distintas mayúsculas y minúsculas se consideran propiedades independientes.

**Caso 2: Escribir datos tooJSON en el archivo**

Si tiene la siguiente tabla en SQL Database:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

y para cada registro, espera que toowrite tooa JSON objeto en el siguiente formato:
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

con el conjunto de datos de salida de Hello **JsonFormat** tipo se define como sigue: (definición parcial con solo partes pertinentes de hello). Más específicamente, `structure` sección define los nombres de propiedad Hola personalizado en el archivo de destino, `nestingSeparator` (valor predeterminado es ".") será la capa de anidamiento de hello tooidentify usado desde nombre hello. Esta sección es **opcional** a menos que se desea el nombre de la propiedad de hello toochange comparar con el nombre de la columna de origen o anidar algunas de las propiedades de Hola.

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

### <a name="specifying-avroformat"></a>Especificación de AvroFormat
Si desea tooparse hello Avro archivos o escribir datos de hello en el formato Avro, establezca hello `format` `type` propiedad demasiado**AvroFormat**. No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola. Ejemplo:

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse el formato Avro en una tabla de Hive, puede hacer referencia demasiado[tutorial de Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Tenga en cuenta Hola siguientes puntos:  

* No se admiten [tipos de datos complejos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumeraciones, matrices, asignaciones, uniones y fijos).

### <a name="specifying-orcformat"></a>Especificación de OrcFormat
Si desea tooparse Hola ORC archivos o escribir datos de hello en formato ORC, Establece hello `format` `type` propiedad demasiado**OrcFormat**. No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola. Ejemplo:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Si no va a copiar archivos ORC **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace. Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits. Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605). Elija Hola adecuada.
>
>

Tenga en cuenta Hola siguientes puntos:

* No se admiten tipos de daros complejos (STRUCT, MAP, LIST, UNION).
* El archivo ORC tiene tres [opciones relacionadas con la compresión](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB y SNAPPY. Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos. Utiliza la compresión de hello códec está en datos de saludo metadatos tooread Hola. Sin embargo, al escribir un archivo de tooan ORC, factoría de datos elige ZLIB, que es el valor predeterminado de Hola para ORC. Actualmente no hay ninguna opción toooverride este comportamiento.

### <a name="specifying-parquetformat"></a>Especificación de ParquetFormat
Si desea tooparse Hola Parquet archivos o escribir datos de hello en formato Parquet, Establece hello `format` `type` propiedad demasiado**ParquetFormat**. No es necesario toospecify las propiedades en la sección de formato de hello dentro de la sección de typeProperties Hola. Ejemplo:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Si no va a copiar archivos Parquet **como-es** entre local y nube almacenes de datos, necesita tooinstall Hola 8 JRE (Java Runtime Environment) en el equipo de puerta de enlace. Una puerta de enlace de 64 bits requiere JRE de 64 bits y una de 32 bits, JRE de 32 bits. Puede encontrar las dos versiones [aquí](http://go.microsoft.com/fwlink/?LinkId=808605). Elija Hola adecuada.
>
>

Tenga en cuenta Hola siguientes puntos:

* No se admiten tipos de daros complejos (MAP, LIST).
* Archivo parquet tiene Hola siguientes opciones de compresión: ninguno, SNAPPY, GZIP y LZO. Data Factory admite la lectura de datos del archivo ORC en cualquiera de los formatos comprimidos. Usa códec de compresión de hello en datos de saludo metadatos tooread Hola. Sin embargo, al escribir un archivo de Parquet tooa, factoría de datos elige SNAPPY, que es el predeterminado de hello para el formato de Parquet. Actualmente no hay ninguna opción toooverride este comportamiento.
