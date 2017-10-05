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
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="bf023-103">Cómo generar vistas en miniatura mediante el Codificador multimedia estándar con .NET</span><span class="sxs-lookup"><span data-stu-id="bf023-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="bf023-104">Puede utilizar Media Encoder Standard para generar una o varias vistas en miniatura de la entrada de vídeo en formatos de archivo de imagen [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format).</span><span class="sxs-lookup"><span data-stu-id="bf023-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="bf023-105">Puede enviar tareas que producen solo las imágenes o puede combinar la generación de miniaturas con la codificación.</span><span class="sxs-lookup"><span data-stu-id="bf023-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="bf023-106">Este tema proporciona algunos ejemplos de valores preestablecidos de miniaturas en código XML y JSON para estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="bf023-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="bf023-107">Al final del tema, hay un [código de ejemplo](#code_sample) que muestra cómo utilizar el SDK de .NET de Media Services para realizar la tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="bf023-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="bf023-108">Para más detalles sobre los elementos que se usan en los valores preestablecidos de ejemplo, consulte [Esquema de Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="bf023-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="bf023-109">Asegúrese de revisar la sección [Consideraciones](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) .</span><span class="sxs-lookup"><span data-stu-id="bf023-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="bf023-110">Ejemplo: archivo PNG único</span><span class="sxs-lookup"><span data-stu-id="bf023-110">Example – single PNG file</span></span>

<span data-ttu-id="bf023-111">El siguiente valor preestablecido en código JSON y XML puede usarse para generar un único archivo PNG de salida fuera de los primeros segundos de la entrada de vídeo, donde el codificador realiza un intento de mejor esfuerzo para buscar un marco "interesante".</span><span class="sxs-lookup"><span data-stu-id="bf023-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="bf023-112">Tenga en cuenta que las dimensiones de la imagen de salida se han establecido en 100%, lo que significa que se corresponderán con las dimensiones de la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="bf023-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="bf023-113">Tenga en cuenta también que es necesaria la configuración de "Format" en "Outputs" para que coincida con el uso de "PngLayers" en la sección "Codecs".</span><span class="sxs-lookup"><span data-stu-id="bf023-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="bf023-114">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="bf023-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="bf023-115">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="bf023-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="bf023-116">Ejemplo: una serie de imágenes JPEG</span><span class="sxs-lookup"><span data-stu-id="bf023-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="bf023-117">El siguiente valor preestablecido en código JSON y XML puede usarse para generar un conjunto de 10 imágenes en marcas de tiempo de 5%, 15%,..., el 95% de la escala de tiempo de entrada y donde se especifica que el tamaño de la imagen sea un cuarto del tamaño de la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="bf023-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="bf023-118">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="bf023-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="bf023-119">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="bf023-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="bf023-120">Ejemplo: una imagen en una marca de tiempo específica</span><span class="sxs-lookup"><span data-stu-id="bf023-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="bf023-121">El siguiente valor preestablecido en código JSON y XML puede usarse para generar una única imagen JPEG en la marca de 30 segundos de la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="bf023-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="bf023-122">Este valor preestablecido espera que la entrada sea más de 30 segundos de duración (de lo contrario el trabajo producirá un error).</span><span class="sxs-lookup"><span data-stu-id="bf023-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="bf023-123">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="bf023-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="bf023-124">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="bf023-124">XML preset</span></span>
    
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

## <span data-ttu-id="bf023-125"><a id="code_sample"></a>Ejemplo: codificar vídeo y generar miniatura</span><span class="sxs-lookup"><span data-stu-id="bf023-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="bf023-126">En el ejemplo de código siguiente se usa el último SDK para .NET de Servicios multimedia para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="bf023-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="bf023-127">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="bf023-127">Create an encoding job.</span></span>
* <span data-ttu-id="bf023-128">Obtener una referencia al codificador Codificador multimedia estándar.</span><span class="sxs-lookup"><span data-stu-id="bf023-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="bf023-129">Cargue el valor preestablecido [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contiene los valores preestablecidos de codificación, así como la información necesaria para generar vistas en miniatura.</span><span class="sxs-lookup"><span data-stu-id="bf023-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="bf023-130">Puede guardar este  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) en un archivo y usar el siguiente código para cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="bf023-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="bf023-131">Agregar una única tarea de codificación al trabajo.</span><span class="sxs-lookup"><span data-stu-id="bf023-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="bf023-132">Especificar el recurso de entrada que se va a codificar.</span><span class="sxs-lookup"><span data-stu-id="bf023-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="bf023-133">Crear un recurso de salida que contendrá el recurso codificado.</span><span class="sxs-lookup"><span data-stu-id="bf023-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="bf023-134">Agregar un controlador de eventos para comprobar el progreso del trabajo.</span><span class="sxs-lookup"><span data-stu-id="bf023-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="bf023-135">Envíe el trabajo.</span><span class="sxs-lookup"><span data-stu-id="bf023-135">Submit the job.</span></span>

<span data-ttu-id="bf023-136">Consulte el tema [Desarrollo en Media Services con .NET](media-services-dotnet-how-to-use.md) para obtener instrucciones acerca de cómo configurar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="bf023-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

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

## <span data-ttu-id="bf023-137"><a id="json"></a>Valor preestablecido JSON de miniatura</span><span class="sxs-lookup"><span data-stu-id="bf023-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="bf023-138">Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="bf023-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="bf023-139"><a id="xml"></a>Valor preestablecido XML de miniatura</span><span class="sxs-lookup"><span data-stu-id="bf023-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="bf023-140">Para obtener información sobre el esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="bf023-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="bf023-141">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="bf023-141">Considerations</span></span>
<span data-ttu-id="bf023-142">Se aplican las siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="bf023-142">The following considerations apply:</span></span>

* <span data-ttu-id="bf023-143">El uso de marcas de tiempo explícitas para inicio/paso/intervalo asume que el origen de la entrada tiene al menos 1 minuto de duración.</span><span class="sxs-lookup"><span data-stu-id="bf023-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="bf023-144">Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:</span><span class="sxs-lookup"><span data-stu-id="bf023-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="bf023-145">Número de marco si son enteros no negativos, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="bf023-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="bf023-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="bf023-146">"Start": "120",</span></span>
  * <span data-ttu-id="bf023-147">Relativos a la duración de origen si se expresan como sufijo de %, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="bf023-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="bf023-148">"Start": "15%", O</span><span class="sxs-lookup"><span data-stu-id="bf023-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="bf023-149">Marca de tiempo si se</span><span class="sxs-lookup"><span data-stu-id="bf023-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="bf023-150">expresa como formato HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="bf023-150">format.</span></span> <span data-ttu-id="bf023-151">P. ej.</span><span class="sxs-lookup"><span data-stu-id="bf023-151">Eg.</span></span> <span data-ttu-id="bf023-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="bf023-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="bf023-153">Puede mezclar y hacer coincidir notaciones a su conveniencia.</span><span class="sxs-lookup"><span data-stu-id="bf023-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="bf023-154">Además, Start también admite una macro especial:{Best}, que intenta determinar el primer marco "interesante" del contenido. NOTA: (Step y Range se omiten cuando Start se establece en {Best}).</span><span class="sxs-lookup"><span data-stu-id="bf023-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="bf023-155">Valores predeterminados: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="bf023-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="bf023-156">Es necesario proporcionar explícitamente el formato de salida para cada formato de imagen: Jpg, Png o BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="bf023-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="bf023-157">Cuando está presente, MES hará coincidir JpgVideo con JpgFormat y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="bf023-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="bf023-158">OutputFormat presenta una nueva macro específica de códec de imagen: {Index}, que debe estar presente (una vez y sólo una vez) para formatos de salida de imagen.</span><span class="sxs-lookup"><span data-stu-id="bf023-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf023-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf023-159">Next steps</span></span>

<span data-ttu-id="bf023-160">Puede comprobar el [progreso del trabajo](media-services-check-job-progress.md) mientras el trabajo de codificación está pendiente.</span><span class="sxs-lookup"><span data-stu-id="bf023-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bf023-161">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="bf023-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf023-162">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="bf023-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="bf023-163">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="bf023-163">See Also</span></span>
[<span data-ttu-id="bf023-164">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="bf023-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

