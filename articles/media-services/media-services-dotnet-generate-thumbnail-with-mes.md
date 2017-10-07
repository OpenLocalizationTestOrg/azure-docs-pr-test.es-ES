---
title: "aaaHow toogenerate miniaturas utilizando Media Encoder estándar con .NET"
description: "Este tema se muestra cómo toouse .NET tooencode un activo y generen miniaturas en hello simultánea mediante el estándar de codificador multimedia."
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
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Cómo miniaturas toogenerate utilizando Media Encoder estándar con .NET

Puede usar toogenerate Media Encoder estándar uno o más de las vistas en miniatura de la entrada de vídeo en [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formatos de archivo de imagen. Puede enviar tareas que producen solo las imágenes o puede combinar la generación de miniaturas con la codificación. Este tema proporciona algunos ejemplos de valores preestablecidos de miniaturas en código XML y JSON para estos escenarios. Al final de Hola de tema de hello, hay un [código de ejemplo](#code_sample) que muestra cómo toouse Hola Media Services .NET SDK tooaccomplish Hola tarea de codificación.

Para obtener más detalles sobre elementos de Hola que se usan en los valores preestablecidos de ejemplo, debe revisar [Media Encoder estándar esquema](media-services-mes-schema.md).

Realizar seguro hello tooreview [consideraciones](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sección.

## <a name="example--single-png-file"></a>Ejemplo: archivo PNG único

Hola después de JSON y valor preestablecido XML puede ser tooproduce usa una única salida PNG archivo fuera de hello primero algunos segundos de vídeo de entrada de hello, donde codificador Hola hace un intento de mejor esfuerzo en búsqueda de un marco "interesante". Tenga en cuenta que se han establecido Hola dimensiones de la imagen de salida too100%, lo que significa que estos coincidirá con dimensiones de Hola de vídeo de entrada de Hola. Tenga en cuenta también cómo se requiere la configuración de "Format" Hola "Salidas" uso de hello toomatch de "PngLayers" en la sección de "Códecs" Hola. 

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

Hola después de JSON y valor preestablecido XML puede ser tooproduce usa un conjunto de 10 imágenes en las marcas de tiempo del 5%, 15%,..., el 95% de la escala de tiempo de entrada hello, donde el tamaño de imagen de Hola es toobe especificado un cuarto que de hello una entrada de vídeo.

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

Hola siguiente valor preestablecido de JSON y XML puede ser utilizado tooproduce marca de 30 segundos de una sola imagen JPEG en Hola de vídeo de entrada de Hola. Este valor preestablecido espera Hola entrada toobe más de 30 segundos de duración (trabajo de hello else se producirá un error).

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

Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:

* Crear un trabajo de codificación.
* Obtiene un Codificador multimedia codificador estándar toohello de referencia.
* Valor preestablecido Hola carga [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contienen Hola codificación preestablecido, así como información necesaria toogenerate miniaturas. Puede guardar esta [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) un Hola de archivo y use el archivo de código tooload Hola siguiente.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Agregar un único trabajo de codificación tarea toohello. 
* Especificar la entrada de hello toobe activo codificado.
* Crear un recurso de salida que contendrá asset Hola codificado.
* Agregue un progreso del controlador de eventos toocheck Hola trabajo.
* Enviar el trabajo de Hola.

Vea hello [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md) tema para obtener instrucciones acerca de cómo tooset del entorno de desarrollo.

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
            // Read values from hello App.config file.
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

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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
Hola siguientes consideraciones se aplica:

* uso de Hola de marcas de tiempo explícito para el inicio/paso/intervalo supone que ese origen de entrada de hello es larga de 1 minuto como mínimo.
* Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:
  
  * Número de marco si son enteros no negativos, por ejemplo, "Start": "120",
  * Duración de toosource relativa si expresado como sufijo de %, p. ej. "Start": "15%", O
  * Marca de tiempo si se expresa como formato HH:MM:SS… P. ej. "Start" : "00:01:00"
    
    Puede mezclar y hacer coincidir notaciones a su conveniencia.
    
    Además, inicio también admite una Macro especial: {recomendados}, que intenta toodetermine Hola primer "interesante" marco de contenido de hello Nota: (paso y el intervalo se omiten al inicio se establece demasiado {mejor})
  * Valores predeterminados: Start:{Best}
* Formato de salida debe toobe indicado de forma explícita para cada formato de imagen: Jpg o Png/BmpFormat. Cuando está presente, MES coincidirá JpgVideo tooJpgFormat y así sucesivamente. OutputFormat presenta una nueva Macro específica de códecs de imagen: {Index}, que necesita toobe presente (una vez y solo una vez) para formatos de salida de imagen.

## <a name="next-steps"></a>Pasos siguientes

Puede comprobar hello [progreso del trabajo](media-services-check-job-progress.md) al Hola trabajo de codificación está pendiente.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Información general sobre la codificación de Servicios multimedia](media-services-encode-asset.md)

