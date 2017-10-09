## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Especificación de la definición de la estructura de los conjuntos de datos rectangulares
Hola sección sobre la estructura en conjuntos de datos de hello JSON es un **opcional** contiene una colección de columnas de tabla de Hola y la sección para las tablas rectangulares (con filas y columnas). Sección de la estructura de hello usará para cualquier con información de tipo para las conversiones de tipos o realizar asignaciones de columnas. Hola siguientes secciones describe estas características en detalle. 

Cada columna contiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name |Nombre de columna de Hola. |Sí |
| type |Tipo de datos de columna de Hola. Consulte la sección de conversiones de tipos siguiente para más detalles sobre cuándo debe especificar la información de tipo. |No |
| culture |.NET según toobe de referencia cultural que se utilizan al tipo especificado y es el tipo de .NET Datetime o Datetimeoffset. El valor predeterminado es «en-us». |No |
| formato |Dar formato a toobe de cadena que se utiliza al tipo especificado y es el tipo de .NET Datetime o Datetimeoffset. |No |

Hello en el ejemplo siguiente se muestra hello sección sobre la estructura JSON para una tabla que tiene tres columnas userid, nombre y lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Hola siguientes instrucciones para cuando use información de la "estructura" tooinclude y qué tooinclude Hola **estructura** sección.

* **Para los orígenes de datos estructurados** que almacenar la información de esquema y el tipo de datos junto con los datos de hello propio (orígenes como tabla de Azure de SQL Server, Oracle, etc.), debe especificar la sección de "estructura" hello únicamente si desea que realice de asignación de columnas específicas de columnas de origen toospecific columnas receptor y sus nombres son Hola no igual (consulte los detalles en la siguiente sección de asignación de columna). 
  
    Como se mencionó anteriormente, información de tipo hello es opcional en la sección "estructura". Para los orígenes estructurados, ya está disponible la información de tipo como parte de la definición de conjunto de datos en el almacén de datos de hello, por lo que no debería incluir información de tipo cuando se incluye la sección sobre la "estructura" Hola.
* **Para el esquema en orígenes de datos de lectura (específicamente Azure blob)** puede elegir toostore datos sin tener que almacenar cualquier información de tipo o esquema con datos de Hola. Para estos tipos de orígenes de datos debe incluir "estructura" Hola 2 casos siguientes:
  * Desea toodo asignación de columna.
  * Cuando el conjunto de datos de hello es un origen en una actividad de copia, puede proporcionar información de tipos en "estructura" y factoría de datos utilizará esta información de tipo para tipos de conversión toonative de receptor de Hola. Vea [mover tooand de datos de Blob de Azure](../articles/data-factory/data-factory-azure-blob-connector.md) artículo para obtener más información.

### <a name="supported-net-based-types"></a>Tipos basados en .NET admitidos
Datos generador admite Hola después .NET conforme con CLS según los valores de tipo para proporcionar información de tipo en "estructura" de esquema en orígenes de datos de lectura como blobs de Azure.

* Int16
* Int32 
* Int64
* Single
* Doble
* DECIMAL
* Byte[]
* Booleano
* String 
* Guid
* Datetime
* Datetimeoffset
* TimeSpan 

Para Datetime y Datetimeoffset opcionalmente, también puede especificar "culture" & análisis de toofacilitate una cadena "format" de la cadena de fecha y hora personalizada. Consulte el ejemplo de conversión de tipos siguiente.

