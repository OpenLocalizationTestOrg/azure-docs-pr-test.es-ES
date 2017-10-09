---
title: aaaIndexing archivos multimedia con Azure Media Indexer
description: "Azure Media Indexer le permite toomake contenido de los archivos multimedia que permite realizar búsquedos y toogenerate una transcripción de texto completo para palabras clave y subtítulos. Este tema se muestra cómo toouse Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Indización de archivos multimedia con el Indizador multimedia de Azure
Azure Media Indexer le permite toomake contenido de los archivos multimedia que permite realizar búsquedos y toogenerate una transcripción de texto completo para palabras clave y subtítulos. Puede procesar uno o varios archivos multimedia en un lote.  

> [!IMPORTANT]
> Al realizar la indización de contenido, asegúrese de toouse seguro de archivos multimedia que tienen muy claro (sin música de fondo, ruido, efectos o audio del micrófono). Algunos ejemplos de contenido adecuado son: reuniones, conferencias o presentaciones grabadas. Hello siguiente contenido podría no ser adecuado para la indización: películas, programas de TV, cualquier cosa con audio mixto y efectos de sonido, contenido mal graban con fondo ruido de fondo.
> 
> 

Un trabajo de indización puede generar Hola siguientes salidas:

* Archivos de subtítulos en hello siguientes formatos: **SAMI**, **TTML**, y **WebVTT**.
  
    Archivos de subtítulos incluyen una etiqueta denominada Recognizability, que puntúa un trabajo de indexación según reconocimiento voz hello en vídeo de origen de hello es.  Puede usar el valor de hello Recognizability tooscreen de archivos de salida para su uso. Una puntuación baja significaría malos resultados de indexación debido tooaudio calidad.
* Archivo de palabras clave (XML).
* Archivo blob de indización de audio (AIB) para usar con SQL Server.
  
    Para obtener más información, consulte [Uso de archivos AIB con Azure Media Indexer y SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Este tema muestra cómo la indización de toocreate trabajos demasiado**indexar un recurso** y **indexar varios archivos**.

Actualizaciones más recientes de Azure Media Indexer de hello, consulte [blogs de servicios multimedia](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Uso de archivos de manifiesto y de manifiesto para tareas de indización
Puede especificar más detalles de las tareas de indización mediante la configuración de tarea. Por ejemplo, puede especificar qué toouse de metadatos para el archivo de medios. Estos metadatos son utilizan Hola lenguaje motor tooexpand su vocabulario y mejora considerablemente la precisión del reconocimiento de voz de Hola.  También es toospecify capaz de los archivos de salida que desee.

También puede procesar varios archivos multimedia a la vez mediante un archivo de manifiesto.

Para obtener más información, consulte [Valores preestablecidos de tarea para Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Indización de un recurso
Hello método siguiente carga un archivo multimedia como un recurso y crea un recurso de trabajo tooindex Hola.

Tenga en cuenta que si no se especifica ningún archivo de configuración, archivo de medios de hello se indizarán con todos los valores predeterminados.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Archivos de salida
De forma predeterminada, un trabajo de indexación genera Hola siguientes archivos de salida. Hola archivos se almacenarán en el primer recurso de salida Hola.

Cuando hay más de un archivo multimedia de entrada, indizador generará un archivo de manifiesto de las salidas de trabajo de hello, llamado 'JobResult.txt'. Para cada archivo multimedia de entrada, hello resultantes de AIB, SAMI, TTML, WebVTT y archivos de la palabra clave, se secuencialmente numerados y denominados mediante Hola "Alias".

| Nombre de archivo | Description |
| --- | --- |
| **InputFileName.aib** |Archivo Blob de indización de audio. <br/><br/> El archivo Blob de indexación de audio (AIB) es un archivo que se puede buscar en Microsoft SQL Server mediante la búsqueda de texto completo.  archivo AIB Hello es más eficaz que archivos de subtítulos sencillos de hello, ya que contiene alternativas para cada palabra, lo que permite una experiencia de búsqueda mucho más completa. <br/> <br/>Requiere la instalación de Hola de complemento de SQL de indizador de hello en un equipo está ejecutando Microsoft SQL server 2008 o posterior. Buscar hello AIB mediante Microsoft SQL búsqueda de texto completo de servidor proporciona resultados más precisos de búsqueda Hola cerrarse archivos de subtítulos generados por WAMI. Esto es porque hello AIB contiene alternativas con palabras que suenan parecidas, mientras que Hola cierra archivos de subtítulos contienen la palabra de hello mayor confianza para cada segmento de audio de Hola. Si busca oral es lo que más importancia, se recomienda toouse hello Aib junto con Microsoft SQL Server.<br/><br/> toodownload Hola complemento, haga clic en <a href="http://aka.ms/indexersql">Azure Media Indexer SQL complemento</a>. <br/><br/>También es posible tooutilize otros motores de búsqueda como Apache Lucene/Solr Hola de índice de toosimply vídeo basadas en hello cerrado título y la palabra clave archivos XML, pero esto dará como resultado menos precisos en resultados de búsqueda. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Archivos de subtítulos en los formatos SAMI, TTML y WebVTT.<br/><br/>Pueden ser utilizados toomake audio y vídeo archivos toopeople accesible con discapacidades auditivas.<br/><br/>Archivos de subtítulos cerrados incluyen una etiqueta denominada <b>Recognizability</b> que puntúa un trabajo de indexación en función de reconocimiento voz hello en vídeo de origen de hello es.  Se puede utilizar el valor de Hola de <b>Recognizability</b> tooscreen archivos para facilidad de uso de salida. Una puntuación baja significaría malos resultados de indexación debido tooaudio calidad. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Archivos de información y palabras clave. <br/><br/>Archivo de palabras clave es un archivo XML que contiene palabras clave extraídas de contenidos de hello orales, con frecuencia y la información de desplazamiento. <br/><br/>El archivo de información es un archivo de texto sin formato que contiene información detallada acerca de cada término reconocido. primera línea de Hello es especial y contiene hello Recognizability puntuación. Cada línea siguiente es una lista separados por tabulaciones de hello datos siguientes: inicio de tiempo, hora de finalización, palabra o frase, confianza. tiempos de Hola se proporcionan en segundos y confianza Hola se proporciona como un número entre 0-1. <br/><br/>Línea de ejemplo: "1,20    1,45    palabra    0,67" <br/><br/>Estos archivos pueden utilizarse para una serie de propósitos, como análisis de voz de tooperform, o los motores de toosearch expuesto como Bing, Google o Microsoft SharePoint toomake Hola archivos multimedia más reconocibles, o incluso usado toodeliver anuncios más relevantes. |
| **JobResult.txt** |Manifiesto de salida, está presente sólo cuando la indización de varios archivos, que contiene Hola siguiente información:<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Error</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Si no todos los archivos multimedia de entrada se indexan correctamente, se producirá un error de trabajo de indexación de hello con código de error 4000. Para obtener más información, consulte [Códigos de error](#error_codes).

## <a name="index-multiple-files"></a>Indización de varios archivos
Hola siguiendo el método carga varios archivos multimedia como un recurso y crea un trabajo tooindex todos estos archivos en un lote.

Un archivo de manifiesto con la extensión .lst de hello es creado y se carga en el recurso de Hola. archivo de manifiesto de Hello contiene la lista de Hola de todos los archivos de recursos de Hola. Para obtener más información, consulte [Valores preestablecidos de tarea para Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Trabajo parcialmente correcto
Si no todos los archivos multimedia de entrada se indexan correctamente, se producirá un error de trabajo de indexación de hello con código de error 4000. Para obtener más información, consulte [Códigos de error](#error_codes).

Hola mismas salidas (como trabajos correctos) se generan. Se puede hacer referencia toohello salida archivo de manifiesto toofind qué archivos de entrada no se pudieron, según toohello valores de columna de Error. Para archivos de entrada que no se pudo Hola resultantes de AIB, SAMI, TTML, WebVTT y no se generarán archivos de palabra clave.

### <a id="preset"></a> Valores predefinidos de tarea para Azure Media Indexer
Hola de procesamiento de Azure Media Indexer puede personalizarse proporcionando una tarea opcional preestablecida junto con la tarea hello.  Hola a continuación describe formato Hola de este archivo xml de configuración.

| Nombre | Necesario | Description |
| --- | --- | --- |
| **input** |false |Archivos de recurso que desea tooindex.</p><p>Azure Media Indexer es compatible con hello siguientes formatos de archivo multimedia: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>Puede especificar el nombre de archivo (s) de Hola Hola **nombre** o **lista** atributo de hello **entrada** elemento (tal y como se muestra a continuación). Si no especifica qué tooindex del archivo de activos, se seleccionará el archivo principal de Hola. Si se establece ningún archivo de recurso principal, se indiza archivo primera hello en el recurso de entrada de Hola.</p><p>tooexplicitly especificar nombre de archivo de activos de hello, realice:<br/>`<input name="TestFile.wmv">`<br/><br/>También puede indizar varios archivos de recursos a la vez (seguridad de los archivos de too10). toodo esto:<br/><br/><ol class="ordered"><li><p>Cree un archivo de texto (archivo de manifiesto) y asígnele una extensión .lst. </p></li><li><p>Agregue una lista de todos los nombres de archivo de activos de hello en el archivo de manifiesto de recurso de entrada toothis. </p></li><li><p>Agregar (cargar) thanifest archivo toohello activo.  </p></li><li><p>Especifique el nombre de Hola Hola del archivo de manifiesto en el atributo de la lista de la entrada de Hola.<br/>`<input list="input.lst">`</li></ol><br/><br/>Nota: Si agrega más de 10 archivos de archivo de manifiesto toohello, Hola trabajo de indización se producirá un error con código de error de hello 2006. |
| **metadata** |false |Metadatos de hello especifican archivos de recurso que se utiliza para la adaptación de vocabulario.  Tooprepare útil indizador toorecognize vocabulario no estándar o más palabras como nombres propios.<br/>`<metadata key="..." value="..."/>` <br/><br/>Puede proporcionar **valores** para **claves** predefinidas. Actualmente se admite Hola siguiendo las claves:<br/><br/>"título" y "Descripción" - utilizada para el idioma de vocabulario adaptación tootweak Hola de modelo para su trabajo y mejorar la precisión del reconocimiento de voz.  valores de Hello propagarlo Internet búsquedas toofind texto correspondiente como documentos, con diccionario interno de hello contenido tooaugment Hola durante hello de la tarea de indización.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **features** <br/><br/> Agregado en la versión 1.2. Actualmente, la característica de hello solo admitido es el reconocimiento de voz ("ASR"). |false |característica de reconocimiento de voz de Hello tiene Hola después de claves de configuración:<table><tr><th><p>Clave</p></th>        <th><p>Descripción</p></th><th><p>Valor de ejemplo</p></th></tr><tr><td><p>language</p></td><td><p>Hola toobe de lenguaje natural que se reconocen en el archivo multimedia de hello.</p></td><td><p>Inglés, español</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>una lista separada por punto y coma de hello deseado formatos de salida de título (si existe)</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Una marca booleana que especifica si un archivo AIB se requiere (para su uso con clientes de SQL Server y Hola IFilter del indexador).  Para obtener más información, consulte <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Uso de archivos AIB con Azure Media Indexer y SQL Server</a>.</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Una marca booleana que especifica si se requiere un archivo XML de palabras clave o no.</p></td><td><p>True; False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Una marca booleana que especifica si se permite o no títulos tooforce completa (independientemente del nivel de confianza).  </p><p>Valor predeterminado es false, en cuyo caso palabras y frases que tienen un nivel de confianza del 50% menos se omite de salidas de título final de Hola y sustituye por puntos suspensivos ("...").  puntos suspensivos de Hello son útiles para el control de calidad de título y auditoría.</p></td><td><p>True; False. </p></td></tr></table> |

### <a id="error_codes"></a>Códigos de error
En caso de hello de un error, debería notificar Azure Media Indexer hacia atrás un Hola siguientes códigos de error:

| Código | Nombre | Razones posibles |
| --- | --- | --- |
| 2000 |Configuración no válida |Configuración no válida |
| 2001 |Recursos de entrada no válidos |Faltan recursos de entrada o están vacíos. |
| 2002 |Manifiesto no válido |El manifiesto está vacío o contiene elementos no válidos. |
| 2003 |Archivo de error toodownload multimedia |Dirección URL no válida en el archivo de manifiesto. |
| 2004 |Protocolo no admitido |No se admite el protocolo de dirección URL de los medios. |
| 2005 |Tipo de archivo no admitido |No se admite el tipo de archivo multimedia de entrada. |
| 2006 |Hay demasiados archivos de entrada |Hay más de 10 archivos en el manifiesto de entrada de Hola. |
| 3000 |Archivo de error toodecode multimedia |Códec multimedia no compatible  <br/>o<br/> El archivo multimedia está dañado. <br/>o<br/> No hay ninguna secuencia de audio en el archivo multimedia de entrada. |
| 4000 |Indización de lote parcialmente correcta |Error en alguna de multimedia de entrada de hello son archivos toobe indizado. Para obtener más información, consulte <a href="#output_files">Archivos de salida</a>. |
| otros |Errores internos |Póngase en contacto con el equipo de soporte técnico. indexer@microsoft.com |

## <a id="supported_languages"></a>Idiomas admitidos
Actualmente, se admiten los idiomas inglés y español de Hola. Para obtener más información, consulte [Hola entrada de blog de versión v1.2](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Información general de análisis de Servicios multimedia de Azure](media-services-analytics-overview.md)

[Uso de archivos AIB con el Indizador multimedia de Azure y SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indización de archivos multimedia con Azure Media Indexer 2 Preview](media-services-process-content-with-indexer2.md)

