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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="93b49-103">Cómo miniaturas toogenerate utilizando Media Encoder estándar con .NET</span><span class="sxs-lookup"><span data-stu-id="93b49-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="93b49-104">Puede usar toogenerate Media Encoder estándar uno o más de las vistas en miniatura de la entrada de vídeo en [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formatos de archivo de imagen.</span><span class="sxs-lookup"><span data-stu-id="93b49-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="93b49-105">Puede enviar tareas que producen solo las imágenes o puede combinar la generación de miniaturas con la codificación.</span><span class="sxs-lookup"><span data-stu-id="93b49-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="93b49-106">Este tema proporciona algunos ejemplos de valores preestablecidos de miniaturas en código XML y JSON para estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="93b49-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="93b49-107">Al final de Hola de tema de hello, hay un [código de ejemplo](#code_sample) que muestra cómo toouse Hola Media Services .NET SDK tooaccomplish Hola tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="93b49-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="93b49-108">Para obtener más detalles sobre elementos de Hola que se usan en los valores preestablecidos de ejemplo, debe revisar [Media Encoder estándar esquema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="93b49-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="93b49-109">Realizar seguro hello tooreview [consideraciones](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sección.</span><span class="sxs-lookup"><span data-stu-id="93b49-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="93b49-110">Ejemplo: archivo PNG único</span><span class="sxs-lookup"><span data-stu-id="93b49-110">Example – single PNG file</span></span>

<span data-ttu-id="93b49-111">Hola después de JSON y valor preestablecido XML puede ser tooproduce usa una única salida PNG archivo fuera de hello primero algunos segundos de vídeo de entrada de hello, donde codificador Hola hace un intento de mejor esfuerzo en búsqueda de un marco "interesante".</span><span class="sxs-lookup"><span data-stu-id="93b49-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="93b49-112">Tenga en cuenta que se han establecido Hola dimensiones de la imagen de salida too100%, lo que significa que estos coincidirá con dimensiones de Hola de vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="93b49-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="93b49-113">Tenga en cuenta también cómo se requiere la configuración de "Format" Hola "Salidas" uso de hello toomatch de "PngLayers" en la sección de "Códecs" Hola.</span><span class="sxs-lookup"><span data-stu-id="93b49-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="93b49-114">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="93b49-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="93b49-115">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="93b49-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="93b49-116">Ejemplo: una serie de imágenes JPEG</span><span class="sxs-lookup"><span data-stu-id="93b49-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="93b49-117">Hola después de JSON y valor preestablecido XML puede ser tooproduce usa un conjunto de 10 imágenes en las marcas de tiempo del 5%, 15%,..., el 95% de la escala de tiempo de entrada hello, donde el tamaño de imagen de Hola es toobe especificado un cuarto que de hello una entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="93b49-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="93b49-118">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="93b49-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="93b49-119">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="93b49-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="93b49-120">Ejemplo: una imagen en una marca de tiempo específica</span><span class="sxs-lookup"><span data-stu-id="93b49-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="93b49-121">Hola siguiente valor preestablecido de JSON y XML puede ser utilizado tooproduce marca de 30 segundos de una sola imagen JPEG en Hola de vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="93b49-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="93b49-122">Este valor preestablecido espera Hola entrada toobe más de 30 segundos de duración (trabajo de hello else se producirá un error).</span><span class="sxs-lookup"><span data-stu-id="93b49-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="93b49-123">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="93b49-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="93b49-124">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="93b49-124">XML preset</span></span>
    
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

## <span data-ttu-id="93b49-125"><a id="code_sample"></a>Ejemplo: codificar vídeo y generar miniatura</span><span class="sxs-lookup"><span data-stu-id="93b49-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="93b49-126">Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="93b49-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="93b49-127">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="93b49-127">Create an encoding job.</span></span>
* <span data-ttu-id="93b49-128">Obtiene un Codificador multimedia codificador estándar toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="93b49-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="93b49-129">Valor preestablecido Hola carga [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contienen Hola codificación preestablecido, así como información necesaria toogenerate miniaturas.</span><span class="sxs-lookup"><span data-stu-id="93b49-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="93b49-130">Puede guardar esta [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) un Hola de archivo y use el archivo de código tooload Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="93b49-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="93b49-131">Agregar un único trabajo de codificación tarea toohello.</span><span class="sxs-lookup"><span data-stu-id="93b49-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="93b49-132">Especificar la entrada de hello toobe activo codificado.</span><span class="sxs-lookup"><span data-stu-id="93b49-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="93b49-133">Crear un recurso de salida que contendrá asset Hola codificado.</span><span class="sxs-lookup"><span data-stu-id="93b49-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="93b49-134">Agregue un progreso del controlador de eventos toocheck Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="93b49-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="93b49-135">Enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="93b49-135">Submit hello job.</span></span>

<span data-ttu-id="93b49-136">Vea hello [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md) tema para obtener instrucciones acerca de cómo tooset del entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="93b49-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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

## <span data-ttu-id="93b49-137"><a id="json"></a>Valor preestablecido JSON de miniatura</span><span class="sxs-lookup"><span data-stu-id="93b49-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="93b49-138">Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="93b49-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="93b49-139"><a id="xml"></a>Valor preestablecido XML de miniatura</span><span class="sxs-lookup"><span data-stu-id="93b49-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="93b49-140">Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="93b49-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="93b49-141">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="93b49-141">Considerations</span></span>
<span data-ttu-id="93b49-142">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="93b49-142">hello following considerations apply:</span></span>

* <span data-ttu-id="93b49-143">uso de Hola de marcas de tiempo explícito para el inicio/paso/intervalo supone que ese origen de entrada de hello es larga de 1 minuto como mínimo.</span><span class="sxs-lookup"><span data-stu-id="93b49-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="93b49-144">Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:</span><span class="sxs-lookup"><span data-stu-id="93b49-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="93b49-145">Número de marco si son enteros no negativos, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="93b49-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="93b49-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="93b49-146">"Start": "120",</span></span>
  * <span data-ttu-id="93b49-147">Duración de toosource relativa si expresado como sufijo de %, p. ej.</span><span class="sxs-lookup"><span data-stu-id="93b49-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="93b49-148">"Start": "15%", O</span><span class="sxs-lookup"><span data-stu-id="93b49-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="93b49-149">Marca de tiempo si se</span><span class="sxs-lookup"><span data-stu-id="93b49-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="93b49-150">expresa como formato HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="93b49-150">format.</span></span> <span data-ttu-id="93b49-151">P. ej.</span><span class="sxs-lookup"><span data-stu-id="93b49-151">Eg.</span></span> <span data-ttu-id="93b49-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="93b49-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="93b49-153">Puede mezclar y hacer coincidir notaciones a su conveniencia.</span><span class="sxs-lookup"><span data-stu-id="93b49-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="93b49-154">Además, inicio también admite una Macro especial: {recomendados}, que intenta toodetermine Hola primer "interesante" marco de contenido de hello Nota: (paso y el intervalo se omiten al inicio se establece demasiado {mejor})</span><span class="sxs-lookup"><span data-stu-id="93b49-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="93b49-155">Valores predeterminados: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="93b49-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="93b49-156">Formato de salida debe toobe indicado de forma explícita para cada formato de imagen: Jpg o Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="93b49-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="93b49-157">Cuando está presente, MES coincidirá JpgVideo tooJpgFormat y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="93b49-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="93b49-158">OutputFormat presenta una nueva Macro específica de códecs de imagen: {Index}, que necesita toobe presente (una vez y solo una vez) para formatos de salida de imagen.</span><span class="sxs-lookup"><span data-stu-id="93b49-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93b49-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93b49-159">Next steps</span></span>

<span data-ttu-id="93b49-160">Puede comprobar hello [progreso del trabajo](media-services-check-job-progress.md) al Hola trabajo de codificación está pendiente.</span><span class="sxs-lookup"><span data-stu-id="93b49-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="93b49-161">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="93b49-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93b49-162">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="93b49-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="93b49-163">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="93b49-163">See Also</span></span>
[<span data-ttu-id="93b49-164">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="93b49-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

