---
title: "Cómo generar vistas en miniatura mediante el Codificador multimedia estándar con .NET"
description: "En este tema, se muestra cómo se usa .NET para codificar un recurso y generar miniaturas al mismo tiempo con Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a>Cómo generar vistas en miniatura mediante el Codificador multimedia estándar con .NET

Puede utilizar Media Encoder Standard para generar una o varias vistas en miniatura de la entrada de vídeo en formatos de archivo de imagen [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format). Puede enviar tareas que producen solo las imágenes o puede combinar la generación de miniaturas con la codificación. Este tema proporciona algunos ejemplos de valores preestablecidos de miniaturas en código XML y JSON para estos escenarios. Al final del tema, hay un [código de ejemplo](#code_sample) que muestra cómo utilizar el SDK de .NET de Media Services para realizar la tarea de codificación.

Para más detalles sobre los elementos que se usan en los valores preestablecidos de ejemplo, consulte [Esquema de Media Encoder Standard](media-services-mes-schema.md).

Asegúrese de revisar la sección [Consideraciones](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) .

## <a name="example--single-png-file"></a>Ejemplo: archivo PNG único

El siguiente valor preestablecido en código JSON y XML puede usarse para generar un único archivo PNG de salida fuera de los primeros segundos de la entrada de vídeo, donde el codificador realiza un intento de mejor esfuerzo para buscar un marco "interesante". Tenga en cuenta que las dimensiones de la imagen de salida se han establecido en 100%, lo que significa que se corresponderán con las dimensiones de la entrada de vídeo. Tenga en cuenta también que es necesaria la configuración de "Format" en "Outputs" para que coincida con el uso de "PngLayers" en la sección "Codecs". 

### <a name="json-preset"></a>Valor preestablecido JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>Valor preestablecido XML

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a>Ejemplo: una serie de imágenes JPEG

El siguiente valor preestablecido en código JSON y XML puede usarse para generar un conjunto de 10 imágenes en marcas de tiempo de 5%, 15%,..., el 95% de la escala de tiempo de entrada y donde se especifica que el tamaño de la imagen sea un cuarto del tamaño de la entrada de vídeo.

### <a name="json-preset"></a>Valor preestablecido JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Valor preestablecido XML
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a>Ejemplo: una imagen en una marca de tiempo específica

El siguiente valor preestablecido en código JSON y XML puede usarse para generar una única imagen JPEG en la marca de 30 segundos de la entrada de vídeo. Este valor preestablecido espera que la entrada sea más de 30 segundos de duración (de lo contrario el trabajo producirá un error).

### <a name="json-preset"></a>Valor preestablecido JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>Valor preestablecido XML
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a id="code_sample"></a>Ejemplo: codificar vídeo y generar miniatura

En el ejemplo de código siguiente se usa el último SDK para .NET de Servicios multimedia para realizar las siguientes tareas:

* Crear un trabajo de codificación.
* Obtener una referencia al codificador Codificador multimedia estándar.
* Cargue el valor preestablecido [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contiene los valores preestablecidos de codificación, así como la información necesaria para generar vistas en miniatura. Puede guardar este  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) en un archivo y usar el siguiente código para cargar el archivo.
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* Agregar una única tarea de codificación al trabajo. 
* Especificar el recurso de entrada que se va a codificar.
* Crear un recurso de salida que contendrá el recurso codificado.
* Agregar un controlador de eventos para comprobar el progreso del trabajo.
* Envíe el trabajo.

Consulte el tema [Desarrollo en Media Services con .NET](media-services-dotnet-how-to-use.md) para obtener instrucciones acerca de cómo configurar el entorno de desarrollo.

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <a id="json"></a>Valor preestablecido JSON de miniatura
Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="xml"></a>Valor preestablecido XML de miniatura
Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a>Consideraciones
Se aplican las siguientes consideraciones:

* El uso de marcas de tiempo explícitas para inicio/paso/intervalo asume que el origen de la entrada tiene al menos 1 minuto de duración.
* Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:
  
  * Número de marco si son enteros no negativos, por ejemplo, "Start": "120",
  * Relativos a la duración de origen si se expresan como sufijo de %, por ejemplo, "Start": "15%", O
  * Marca de tiempo si se expresa como formato HH:MM:SS… P. ej. "Start" : "00:01:00"
    
    Puede mezclar y hacer coincidir notaciones a su conveniencia.
    
    Además, Start también admite una macro especial:{Best}, que intenta determinar el primer marco "interesante" del contenido. NOTA: (Step y Range se omiten cuando Start se establece en {Best}).
  * Valores predeterminados: Start:{Best}
* Es necesario proporcionar explícitamente el formato de salida para cada formato de imagen: Jpg, Png o BmpFormat. Cuando está presente, MES hará coincidir JpgVideo con JpgFormat y así sucesivamente. OutputFormat presenta una nueva macro específica de códec de imagen: {Index}, que debe estar presente (una vez y sólo una vez) para formatos de salida de imagen.

## <a name="next-steps"></a>Pasos siguientes

Puede comprobar el [progreso del trabajo](media-services-check-job-progress.md) mientras el trabajo de codificación está pendiente.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Información general sobre la codificación de Servicios multimedia](media-services-encode-asset.md)

