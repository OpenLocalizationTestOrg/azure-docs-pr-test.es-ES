---
title: aaaImport su tooAnalytics de datos en Azure Application Insights | Documentos de Microsoft
description: "Importar datos estáticos toojoin con la telemetría de aplicación, o importar un tooquery de flujo de datos independiente con el análisis."
services: application-insights
keywords: "esquema abierto, importación de datos"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Importación de datos a Analytics

Importar los datos tabulares en [análisis](app-insights-analytics.md), ya sea toojoin con [Application Insights](app-insights-overview.md) telemetría de la aplicación, o para que se puede analizar como una secuencia independiente. El análisis es una secuencias de consulta eficaz lenguaje tooanalyzing adecuada con marca de tiempo de gran volumen de telemetría.

Puede importar datos en Analytics mediante un esquema propio. No tiene esquemas toouse Hola de Application Insights estándar como solicitud o un seguimiento.

Puede importar archivos JSON o DSV (valores separados por delimitadores, como pueden ser comas, puntos y coma o tabulaciones).

Existen tres situaciones donde es útil importar tooAnalytics:

* **Combinar con la telemetría de la aplicación.** Por ejemplo, puede importar una tabla que asigna las direcciones URL de los títulos de página legible toomore de sitio Web. En el análisis, puede crear un informe de gráfico de panel que muestra los diez páginas más populares de hello en el sitio Web. Ahora puede mostrar títulos de página en lugar de direcciones URL de Hola Hola.
* **Correlacionar la telemetría de la aplicación** con otros orígenes, como tráfico de red, datos de servidor o archivos de registro de red CDN.
* **Aplicar el flujo de datos independiente de análisis tooa.** Application Insights de Analytics es una herramienta eficaz, que funciona bien con flujos dispersos con marca de tiempo; en muchos casos, de manera mucho mejor que SQL. Si tiene un flujo de este tipo de algún otro origen, puede analizarlo con Analytics.

Origen de datos de envío datos tooyour es fácil. 

1. (Una vez) Definir el esquema de Hola de los datos en un origen de datos' '.
2. (Periódicamente) Cargar el almacenamiento de datos tooAzure y toonotify de la API de REST de hello nos llame que está esperando la ingesta de nuevos datos. Dentro de unos minutos, están disponibles para consultas de análisis de datos Hola.

frecuencia de carga de Hola Hola se define una por parte del usuario y rapidez quiere que su toobe de datos disponible para las consultas. Es más eficiente de los datos de tooupload en fragmentos mayores, pero no mayor que 1GB.

> [!NOTE]
> *¿Tiene una gran cantidad de tooanalyze de orígenes de datos?* [*Considere el uso de* logstash *tooship los datos en información de la aplicación.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Antes de comenzar

Necesita:

1. Un recurso de Application Insights en Microsoft Azure.

 * Si desea que tooanalyze los datos por separado de los otro telemetría, [crear un nuevo recurso de Application Insights](app-insights-create-new-resource.md).
 * Si va a combinar o comparar los datos con la telemetría desde una aplicación que ya está configurada con Application Insights, puede usar recursos de Hola para esa aplicación.
 * Recursos de toothat de acceso de propietario o colaborador.
 
2. Azure Storage. Cargar tooAzure almacenamiento y análisis obtiene los datos a partir de ahí. 

 * Se recomienda crear una cuenta de almacenamiento dedicado para los blobs. Si los blobs se comparten con otros procesos, se tarda más tiempo para nuestro tooread procesos los blobs.


## <a name="define-your-schema"></a>Definición del esquema

Para poder importar datos, debe definir un *origen de datos,* que especifica el esquema de Hola de los datos.
Puede tener hasta too50 orígenes de datos en un único recurso de Application Insights

1. Inicie el Asistente para orígenes de datos de Hola. Use el botón "Agregar nuevo origen de datos". También puede hacer clic en el botón de configuración en la esquina superior derecha y elegir "Orígenes de datos" en el menú desplegable.

    ![Agregar nuevo origen de datos](./media/app-insights-analytics-import/add-new-data-source.png)

    Proporcione un nombre para el nuevo origen de datos.

2. Definir el formato de los archivos de Hola que va a cargar.

    Puede definir manualmente el formato de Hola o cargar un archivo de ejemplo.

    Si los datos de hello están en formato CSV, Hola primera fila de ejemplo Hola puede ser encabezados de columna. Puede cambiar los nombres de campo de hello en el paso siguiente de saludo.

    ejemplo de Hola debe incluir al menos 10 filas o registros de datos.

    Los nombres de campo o columna deben ser alfanuméricos (sin espacios ni signos de puntuación).

    ![Carga de un archivo de ejemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. Esquema de Hola de revisión que Hola asistente tiene una capacidad. Si deduce tipos Hola de un ejemplo, tendrá que los tipos de hello inferir tooadjust de columnas de Hola.

    ![Esquema de hello inferida de revisión](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Opcional). Cargue una definición de esquema. Consulte formato de Hola a continuación.

 * Seleccione una marca de tiempo. Todos los datos de Analytics deben tener un campo de marca de tiempo. Debe tener el tipo `datetime`, pero no es necesario toobe denominado 'timestamp'. Si los datos tienen una columna que contiene una fecha y hora en formato ISO, elija esta opción como columna de marca de tiempo de Hola. En caso contrario, elija "como datos llegó" y proceso de importación de Hola agregará un campo de marca de tiempo.

5. Crear origen de datos de Hola.

### <a name="schema-definition-file-format"></a>Formato del archivo de definición de esquema

En lugar de modificar el esquema de hello en la interfaz de usuario, puede cargar la definición de esquema de Hola desde un archivo. formato de definición de esquemas de Hello es como sigue: 

Formato delimitado 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Formato JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Cada columna se identifica por tipo, nombre y ubicación de Hola. 

* Ubicación: de archivo delimitado formatearlo es posición Hola del valor de hello asignado. Para el formato JSON, resulta jpath Hola de clave de hello asignado.
* Nombre: Hola muestra el nombre de columna de Hola.
* Tipo: tipo de datos de Hola de esa columna.
 
En caso de que se usan datos de muestra y está delimitada por el formato de archivo, definición de esquemas de hello debe asignar todas las columnas y agregar nuevas columnas al final de Hola. 

JSON permite una asignación parcial de los datos de hello, por lo tanto, hello definición de esquemas de formato JSON no tiene toomap todas las claves que se encuentra en datos de muestra. También pueden asignar las columnas que no forman parte de los datos de ejemplo de Hola. 

## <a name="import-data"></a>Importar datos

datos de tooimport, cargarlo tooAzure almacenamiento, crear una clave de acceso para él y, a continuación, realizar una llamada de API de REST.

![Agregar nuevo origen de datos](./media/app-insights-analytics-import/analytics-upload-process.png)

Puede realizar Hola siguiendo el proceso manualmente o configurar un sistema automatizado toodo él a intervalos regulares. Necesita toofollow estos pasos para cada bloque de datos que desee tooimport.

1. Cargar datos de hello demasiado[almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * Blobs pueden tener cualquier tamaño la too1GB sin comprimir. Los blobs grandes de cientos de MB son ideales desde la perspectiva del rendimiento.
 * Es posible comprimir con tiempo de carga tooimprove Gzip y latencia de hello datos toobe disponible para su consulta. Hola de uso `.gz` extensión de nombre de archivo.
 * Es mejor toouse una cuenta de almacenamiento independiente para este propósito, tooavoid llamadas de distintos servicios disminuyendo el rendimiento.
 * Al enviar datos de alta frecuencia, cada pocos segundos, se recomienda toouse más de una cuenta de almacenamiento, por motivos de rendimiento.

 
2. [Crear una clave de firma de acceso compartido para el blob de hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). clave de Hello debe disponer de un período de expiración de un día y proporcionar acceso de lectura.
3. Realizar una toonotify de llamada REST Application Insights que está esperando los datos.

 * Punto de conexión: `https://dc.services.visualstudio.com/v2/track`
 * Método HTTP: POST
 * Carga útil:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

marcadores de posición de Hello son:

* `Blob URI with Shared Access Key`: Puede obtener del procedimiento de Hola para crear una clave. Es blob toohello específico.
* `Schema ID`: Hola Id. del esquema generado para el esquema definido. datos de Hello en este blob deben cumplir toohello esquema.
* `DateTime`: hora de hello en qué Hola se envía la solicitud, UTC. Se aceptan estos formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").
* `Instrumentation key` del recurso de Application Insights.

datos de Hello están disponibles en el análisis después de unos minutos.

## <a name="error-responses"></a>Respuestas de errores

* **400 Solicitud incorrecta**: indica que esa carga de la solicitud de hello es válido. Comprobar:
 * Clave de instrumentación correcta.
 * Valor de hora válido. Debe ser tiempo Hola ahora en UTC.
 * JSON de evento Hola cumple toohello esquema.
* **403 Prohibido**: blob Hola que ha enviado no es accesible. Asegúrese de que esa clave de acceso compartido hello es válida y no ha expirado.
* **404 No encontrado**:
 * no existe el blob de Hola.
 * Hola sourceId es incorrecto.

Información más detallada está disponible en el mensaje de error de respuesta de saludo.


## <a name="sample-code"></a>Código de ejemplo

Este código usa hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) paquete NuGet.

### <a name="classes"></a>Clases

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Introducir datos

Use este código para cada blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Pasos siguientes

* [Paseo de hello lenguaje de consultas de análisis de registros](app-insights-analytics-tour.md)
* [Use *Logstash* toosend datos tooApplication visión](https://github.com/Microsoft/logstash-output-application-insights)
