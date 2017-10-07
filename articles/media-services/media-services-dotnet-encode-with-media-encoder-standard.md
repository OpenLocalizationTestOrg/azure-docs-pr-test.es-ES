---
title: "un activo con Media Encoder estándar mediante .NET aaaEncode | Documentos de Microsoft"
description: "Este tema se muestra cómo toouse .NET tooencode un activo mediante el estándar de codificador multimedia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Codificación de un recurso mediante Estándar de codificador multimedia
Trabajos de codificación son una de las operaciones de procesamiento más habituales de hello en los servicios multimedia. Crear archivos multimedia de codificación trabajos tooconvert desde una tooanother de codificación. Al codificar, puede usar Hola Codificador multimedia integrado de servicios multimedia. También puede utilizar un codificador proporcionado por un socio de servicios multimedia; codificadores de terceros están disponibles a través de hello Azure Marketplace. 

Este tema se muestra cómo toouse .NET tooencode sus activos con medios codificador estándar (MES). Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Se recomienda tooalways codificar los archivos de origen en un conjunto de MP4 de velocidad de bits adaptativa y, a continuación, convertir mediante Hola Hola conjunto toohello deseado formato [empaquetado dinámico](media-services-dynamic-packaging-overview.md). 

Si el recurso de salida tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos. Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Genera MES con un nombre que contiene un archivo de salida Hola 32 primeros caracteres de Hola nombre de archivo de entrada. nombre de Hola se basa en lo que se especifique en el archivo de valores preestablecidos de Hola. Por ejemplo, "FileName": "{nombreBase}_{índice}{extensión}". {Basename} se reemplaza por hello 32 primeros caracteres del nombre de archivo de entrada de Hola.
> 
> 

### <a name="mes-formats"></a>Formatos de MES
[Códecs y formatos](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Valores preestablecidos de MES
Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadatos de entrada y salida
Al codificar un activo de entrada (o activos) el uso de MES, obtendrá un recurso de salida en hello finalización correcta de los que codificar la tarea. Hola activo de salida contiene vídeo, audio, miniaturas, manifiesto, etc., basado en el valor predeterminado de codificación de hello que usa.

recurso de salida de Hello también contiene un archivo con metadatos sobre el recurso de entrada de Hola. nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: < asset_id > _metadata.xml (por ejemplo, 41114ad3-eb5e - 4c 57-8d 92-5354e2b7d4a4_metadata.xml), donde < id_recurso > es valor de AssetId Hola de recurso de entrada de Hola. Hello esquema de esta entrado metadatos XML se describe [aquí](media-services-input-metadata-schema.md).

recurso de salida de Hello también contiene un archivo con metadatos sobre el recurso de salida de hello. nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: < nombre_archivo_origen > _manifest.xml (por ejemplo, BigBuckBunny_manifest.xml). esquema de Hola de estos metadatos de salida XML se describe [aquí](media-services-output-metadata-schema.md).

Si desea tooexamine cualquiera de los archivos de metadatos de hello dos, puede crear un localizador SAS y descargar el equipo local de hello archivo tooyour. Puede encontrar un ejemplo sobre cómo toocreate un localizador SAS y descargar un archivo mediante hello de servicios multimedia extensiones del SDK de. NET.

## <a name="download-sample"></a>Descarga de un ejemplo
Puede obtener y ejecutar un ejemplo que muestra cómo tooencode con el MES de [aquí](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Código de ejemplo de .NET

Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:

* Crear un trabajo de codificación.
* Obtiene un Codificador multimedia codificador estándar toohello de referencia.
* Especificar hello toouse [transmisión por secuencias adaptativa](media-services-autogen-bitrate-ladder-with-mes.md) preestablecido. 
* Agregar un único trabajo de codificación tarea toohello. 
* Especificar la entrada de hello toobe activo codificado.
* Crear un recurso de salida que contendrá asset Hola codificado.
* Agregue un progreso del controlador de eventos toocheck Hola trabajo.
* Enviar el trabajo de Hola.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Ejemplo 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    // Get an uploaded asset.
                    var asset = _context.Assets.FirstOrDefault();

                    // Encode and generate hello output using hello "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass tooit hello name of hello 
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset toocontain hello results of hello job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means hello output asset is not encrypted. 
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
                    job.Submit();
                    job.GetExecutionProgressTask(CancellationToken.None).Wait();

                    return job.OutputMediaAssets[0];
                }

                private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);
                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                            break;
                        default:
                            break;
                    }
                }

                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes
[Cómo miniatura toogenerate con Media Encoder estándar .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codificación Introducción a servicios multimedia](media-services-encode-asset.md)

