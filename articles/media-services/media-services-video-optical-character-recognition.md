---
title: "texto de aaaDigitize con Azure Media análisis OCR | Documentos de Microsoft"
description: "Azure Media análisis OCR (reconocimiento óptico de caracteres) le permite tooconvert el contenido de texto en archivos de vídeo en modificable, puede buscar texto digital.  Esto permite la extracción de hello tooautomate de metadatos significativo de señal de vídeo de Hola de los medios."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Usar el contenido de texto de tooconvert de análisis de multimedia de Azure en archivos de vídeo en textos digitales
## <a name="overview"></a>Información general
Si necesita tooextract texto contenido desde los archivos de vídeo y generar un texto digital editable, búsquedo, debe usar Azure Media análisis OCR (reconocimiento óptico de caracteres). Este procesador multimedia de Azure detecta contenido de texto en los archivos de vídeo y genera archivos de texto para su uso. OCR permite tooautomate Hola extracción de metadatos significativo de señal de vídeo de Hola de los medios.

Cuando se usa junto con un motor de búsqueda, puede fácilmente indexar los medios por texto y mejorar la detectabilidad de hello del contenido. Esto es muy útil en vídeos con gran cantidad de texto, como una grabación de vídeo o una captura de pantalla de una presentación de diapositivas. Hola procesador multimedia de Azure OCR está optimizado para texto digital.

Hola **Azure Media OCR** procesador multimedia está actualmente en vista previa.

Este tema proporciona detalles acerca de **Azure Media OCR** y muestra cómo toouse con el SDK de servicios multimedia para. NET. Para obtener información adicional y ejemplos, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>Archivos de entrada para OCR
Archivos de vídeo. Actualmente, se admite Hola siguientes formatos: MP4, MOV y WMV.

## <a name="task-configuration"></a>Configuración de tareas
Configuración de tareas (valor predeterminado) Cuando se crea una tarea con **Azure Media OCR**, debe especificar una configuración preestablecida mediante JSON o XML. 

>[!NOTE]
>motor de OCR Hola solo toma un área de imagen a mínimo 40 toomaximum 32000 píxeles como una entrada válida en ambos alto y ancho.
>

### <a name="attribute-descriptions"></a>Descripciones de atributos
| Nombre del atributo | Descripción |
| --- | --- |
|AdvancedOutput| Si establece AdvancedOutput tootrue, salida JSON de hello contendrá datos posicionales cada palabra única (en suma toophrases y regiones). Si no desea toosee estos detalles, establezca Hola marca toofalse. valor predeterminado de Hello es false. Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| language |(opcional) describe lenguaje Hola de texto para que toolook. Uno de los siguientes hello: detección automática (valor predeterminado), árabe, chino, chino tradicional, checo danés, neerlandés, inglés, finés, francés, alemán, griego, húngaro, italiano, japonés, coreano, noruego, polaco, portugués, rumano, ruso, SerbianCyrillic, SerbianLatin, eslovaco, español, sueco, turco. |
| TextOrientation |(opcional) describe la orientación de hello del texto para que toolook.  "Izquierda" significa que Hola parte superior de todas las letras se señala hacia la izquierda de Hola.  El texto predeterminado (similar al que se encuentra en un libro) se puede denominar orientado "hacia arriba".  Uno de los siguientes hello: detección automática (valor predeterminado), hasta izquierda, derecha, abajo. |
| TimeInterval |(opcional) describe la frecuencia de muestreo de Hola.  El valor predeterminado es cada 1/2 segundo.<br/>Formato JSON: HH:mm:ss.SSS (predeterminado 00:00:00.500)<br/>Formato XML – primitiva de duración W3C XSD (valor predeterminado PT0.5) |
| DetectRegions |(opcional) Una matriz de objetos de DetectRegion especificando las regiones dentro de fotograma de vídeo de hello en texto para que toodetect.<br/>Un objeto DetectRegion consta de hello después de cuatro valores enteros:<br/>Izquierda: píxeles desde el margen izquierdo de Hola<br/>Parte superior: píxeles del margen superior de Hola<br/>Ancho: el ancho del área de hello en píxeles<br/>Alto: el alto del área de hello en píxeles |

#### <a name="json-preset-example"></a>Ejemplo de JSON preestablecido

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Ejemplo de XML preestablecido
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>Archivos de salida OCR
salida de Hello de procesador de multimedia de hello OCR es un archivo JSON.

### <a name="elements-of-hello-output-json-file"></a>Elementos Hola JSON del archivo de salida
salida de vídeo OCR Hello proporciona segmentada en tiempo de datos en caracteres de Hola que se encuentren en el vídeo.  Puede usar atributos como el idioma o la orientación en toohone en exactamente las palabras hello que está interesado en analizar. 

salida de Hello contiene Hola siguientes atributos:

| Elemento | Description |
| --- | --- |
| Escala de tiempo |"tics" de vídeo de Hola por segundo |
| Offset |Diferencia de tiempo para las marcas de tiempo En la versión 1.0 de las API de vídeo, será siempre 0. |
| Framerate |Fotogramas por segundo de hello vídeo |
| width |ancho del vídeo en píxeles Hola |
| height |alto de vídeo en píxeles Hola |
| Fragments |matriz de fragmentos basado en tiempo de vídeo en qué Hola está fragmentado metadatos |
| start |Hora de inicio de un fragmento en "tics" |
| duration |Duración de un fragmento en "tics" |
| interval |intervalo de cada evento de hello dado fragmento |
| events |La matriz que contiene las regiones |
| region |Objeto que representa las palabras o frases detectadas |
| Idioma |idioma del texto hello detectado dentro de una región |
| orientation |orientación del texto hello detectado dentro de una región |
| lines |Matriz de líneas de texto detectadas en una región |
| text |texto real de Hola |

### <a name="json-output-example"></a>Ejemplo de salida JSON
Hello siguiente ejemplo de salida contiene información de vídeo general hello y varios fragmentos de vídeo. En cada fragmento de vídeo, contiene todas las regiones que se ha detectado por MP de OCR con lenguaje de Hola y su orientación del texto. región de Hello también contiene cada línea de word en esta región con el texto de la línea hello, posición de la línea hello y cada información de word (contenido de word, posición y confianza) en esta línea. Hola siguiente es un ejemplo y colocan algunos comentarios entre líneas.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Código de ejemplo de .NET

siguiente de Hello programa muestra cómo:

1. Crear un activo y cargar un archivo multimedia en activo de Hola.
2. Cree un trabajo con un archivo de configuración o valores preestablecidos de OCR.
3. Descargar archivos de hello salida JSON. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Ejemplo

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
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

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

