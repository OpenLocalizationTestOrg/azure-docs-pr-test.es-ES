---
title: "aaaPerform avanzado de codificación mediante la personalización de valores preestablecidos MES | Documentos de Microsoft"
description: "Este tema muestra cómo tooperform avanzado de codificación mediante la personalización de Media Encoder estándar de valores preestablecidos de tarea."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Codificación avanzada mediante la personalización de valores preestablecidos de MES 

## <a name="overview"></a>Información general

Este tema muestra cómo se configura toocustomize Media Encoder estándar. Hola [codificación con Media Encoder estándar con valores preestablecidos personalizados](media-services-custom-mes-presets-with-dotnet.md) tema muestra cómo toouse .NET toocreate una codificación de tareas y un trabajo que se ejecuta esta tarea. Después de personalizar un ajuste preestablecido, tarea de codificación de toohello de alimentación Hola valores preestablecidos personalizados. 

>[!NOTE]
>Si utiliza un ajuste preestablecido XML, asegúrese de seguro orden de Hola de toopreserve de elementos, como se muestra en los siguientes ejemplos XML (por ejemplo, KeyFrameInterval debe preceder SceneChangeDetection).
>

En este tema, se muestran los valores preestablecidos personalizados Hola que llevan a cabo Hola después de tareas de codificación.

## <a name="support-for-relative-sizes"></a>Compatibilidad con tamaños relativos

Si desea generar vistas en miniatura, no es necesario tooalways especificar ancho de salida y el alto en píxeles. Puede especificar las credenciales en porcentajes, en el intervalo de hello [% 1, …, 100%].

### <a name="json-preset"></a>Valor preestablecido JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Valor preestablecido XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Generación de miniaturas

Esta sección se muestra cómo toocustomize un ajuste preestablecido que genera las miniaturas. Hello valor preestablecido definida a continuación contiene información sobre cómo desea que tooencode el archivo, así como información necesaria toogenerate miniaturas. Puede realizar cualquiera de valores preestablecidos MES de hello documentados [esto](media-services-mes-presets-overview.md) sección y agregue código que genera las miniaturas.  

> [!NOTE]
> Hola **SceneChangeDetection** configuración Hola después preestablecido solo puede establecerse tootrue si va a codificar vídeo de velocidad de bits única tooa. Si va a codificar tooa velocidades de bits vídeo y establecer **SceneChangeDetection** tootrue, el codificador de hello devuelve un error.  
>
>

Para obtener información sobre el esquema, consulte [este](media-services-mes-schema.md) tema.

Realizar seguro hello tooreview [consideraciones](#considerations) sección.

### <a id="json"></a>Valor preestablecido JSON
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Valor preestablecido XML
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Consideraciones

Hola siguientes consideraciones se aplica:

* uso de Hola de marcas de tiempo explícito para el inicio/paso/intervalo supone que ese origen de entrada de hello es larga de 1 minuto como mínimo.
* Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:

  * Número de marco si son enteros no negativos, por ejemplo, Start: 120
  * Duración de toosource relativa si expresado como sufijo de %, por ejemplo "Start": "el 15%", o
  * Marca de tiempo si se por ejemplo, "Start" : "00:01:00"

    Puede mezclar y hacer coincidir notaciones a su conveniencia.

    Además, inicio también admite una Macro especial: {recomendados}, que intenta toodetermine Hola primer "interesante" marco de contenido de hello Nota: (paso y el intervalo se omiten al inicio se establece demasiado {mejor})
  * Valores predeterminados: Start:{Best}
* Formato de salida debe toobe indicado de forma explícita para cada formato de imagen: Jpg o Png/BmpFormat. Cuando está presente, MES coincide con la JpgVideo tooJpgFormat y así sucesivamente. OutputFormat presenta una nueva Macro específica de códecs de imagen: {Index}, que necesita toobe presente (una vez y solo una vez) para formatos de salida de imagen.

## <a id="trim_video"></a>Recorte de un vídeo
Este conferencias de la sección acerca de cómo modificar el codificador de hello presintonías tooclip o recortar el vídeo de entrada de Hola donde hello entrada es un archivo mezzanine denominadas o a petición. Hello codificador puede también tooclip usado o un activo, que es capturado o archivado desde una secuencia en directo de recorte: Hola detalles para este están disponibles en [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim sus vídeos, puede realizar cualquiera de valores preestablecidos MES de hello documentados [esto](media-services-mes-presets-overview.md) sección y modificar hello **orígenes** elemento (tal y como se muestra a continuación). valor de Hola de StartTime debe toomatch Hola absoluta las marcas de tiempo de vídeo de entrada de Hola. Por ejemplo, si hello primer fotograma de vídeo de entrada de hello tiene una marca de tiempo de 12:00:10.000, StartTime debe tener al menos 12:00:10.000 y versiones posteriores. En el ejemplo de Hola siguiente, se supone que el vídeo de entrada de hello tiene una marca de tiempo inicial de cero. **Orígenes** deberá colocarse al principio de Hola de hello presintonía.

### <a id="json"></a>Valor preestablecido JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Valor preestablecido XML
tootrim sus vídeos, puede realizar cualquiera de valores preestablecidos MES de hello documentados [aquí](media-services-mes-presets-overview.md) y modificar hello **orígenes** elemento (tal y como se muestra a continuación).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Creación de una superposición

Hola Media Encoder estándar permite toooverlay una imagen en un vídeo existente. Actualmente, se admite Hola siguientes formatos: png, jpg, gif y bmp. Hello valor preestablecido definida a continuación es un ejemplo básico de una superposición de vídeo.

Además toodefining un archivo de valores preestablecidos, también tiene los servicios multimedia toolet saber qué archivo de recurso de hello es Hola superposición imagen y cuál es el archivo vídeo de origen de hello en el que desea toooverlay imagen de Hola. archivo de vídeo de Hello tiene hello toobe **principal** archivo.

Si usas. NET, agregue Hola siguiendo dos funciones toohello .NET en el ejemplo se define en [esto](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tema. Hola **UploadMediaFilesFromFolder** función carga archivos desde una carpeta (por ejemplo, BigBuckBunny.mp4 y Image001.png) y conjuntos de Hola mp4 archivo toobe Hola archivo principal de hello recurso. Hola **EncodeWithOverlay** función usa el archivo preestablecido personalizado Hola que se pasó tooit (por ejemplo, hello preestablecido que se indica a continuación) toocreate Hola tarea de codificación.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Limitaciones actuales:
>
> no se admite el valor de opacidad de superposición de Hola.
>
> Su archivo de vídeo de origen y el archivo de imagen de superposición de hello tienen toobe en mismo activo de Hola y Hola conjunto de toobe de necesidades de archivo de vídeo como archivo principal de hello en este recurso.
>
>

### <a name="json-preset"></a>Valor preestablecido JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Valor preestablecido XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Inserción de una pista de audio silenciosa cuando la entrada no tiene audio
De forma predeterminada, si se envía un codificador de entrada toohello que solo no contiene vídeo, se oye ningún sonido, Hola activo de salida contiene archivos que contienen datos de solo vídeo. Algunos reproductores no pueden tener toohandle tal flujos de salida. Puede usar este tooadd de codificador de hello configuración tooforce una salida de toohello silenciosa pista de audio en ese escenario.

tooforce Hola codificador tooproduce un activo que contenga una pista de audio silenciosa cuando entrada no tiene oye ningún sonido, especifique el valor de "InsertSilenceIfNoAudio" Hola.

Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:

### <a name="json-preset"></a>Valor preestablecido JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Valor preestablecido XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Deshabilitar el entrelazado automático
Los clientes no necesitan toodo nada si únicamente como Hola entrelazado toobe contenido automáticamente anular entrelazada. Una vez automática Hola de entrelazado en hello (valor predeterminado) MES Hola automáticamente la detección de fotogramas entrelazados y solo anular interlaces fotogramas marcados como entrelazado.

Puede desactivar automáticamente Hola de entrelazado. Esta opción nos e recomienda.

### <a name="json-preset"></a>Valor preestablecido JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Valor preestablecido XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Valores preestablecidos de solo audio
Esta sección muestra dos valores preestablecidos de MES de solo audio: Audio AAC y Audio AAC de buena calidad.

### <a name="aac-audio"></a>Audio AAC
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>Audio AAC de buena calidad
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Concatenación de dos o más archivos de vídeo

Hello en el ejemplo siguiente se muestra cómo puede generar un valor preestablecido tooconcatenate dos o más archivos de vídeo. escenario más común de Hello es cuando se desea tooadd un encabezado o un vídeo principal toohello de finalizador. Hola pensado uso resulta propiedades (resolución de vídeo, velocidad de fotogramas, número de pista de audio, etcetera) del recurso compartido de archivos de vídeo de Hola que se está editando juntos. También debe tener cuidado no toomix vídeos de distintas velocidades de fotogramas o con un número diferente de pistas de audio.

>[!NOTE]
>Hello diseño actual de la característica de concatenación de hello espera ese Hola entrada clips de vídeo son coherentes en cuanto a la resolución, velocidad de fotogramas etcetera. 

### <a name="requirements-and-considerations"></a>Requisitos y consideraciones

* Los vídeos de entrada solo deberían tener una pista de audio.
* Vídeos de entrada deben tener todos Hola misma velocidad de fotogramas.
* Debe cargar los vídeos en activos independientes y establecer vídeos hello como archivo principal de Hola de cada recurso.
* Necesita tooknow Hola que dure sus vídeos.
* Hello preestablecidos ejemplos siguientes se supone que todos los vídeos de entrada de hello comience con una marca de tiempo de cero. Necesita toomodify Hola StartTime valores si los vídeos de hello tienen marca de tiempo inicial diferente, como sucede normalmente Hola con archivos de almacenamiento en vivo.
* Hello valor preestablecido JSON hace que las referencias explícitas toohello AssetID valores Hola de recursos de entrada.
* código de ejemplo de Hola se da por supuesto que Hola preestablecido JSON se ha guardado el archivo local de tooa, por ejemplo, "C:\supportFiles\preset.json". También se supone que se han creado dos recursos mediante la carga de archivos de vídeo de dos, y que sepan Hola valores AssetID resultantes.
* Hola fragmento de código y JSON valor preestablecido muestra un ejemplo de la concatenación de dos archivos de vídeo. Se puede ampliar toomore que dos vídeos:

  1. Tarea que realiza la llamada. InputAssets.Add() tooadd varias veces más vídeos, en orden.
  2. Realizar correspondiente edita el elemento toohello "orígenes" Hola JSON, agregando más entradas en hello mismo orden.

### <a name="net-code"></a>Código .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Valor preestablecido JSON

Actualizar el valor preestablecido con identificadores de activos de Hola que desea tooconcatenate y con el segmento de tiempo adecuado de Hola para cada vídeo personalizado.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Recorte de vídeos con Codificador multimedia estándar
Vea hello [recortar vídeos con Media Encoder estándar](media-services-crop-video.md) tema.

## <a id="no_video"></a>Inserción de una pista de vídeo cuando la entrada cuando no tiene vídeo

De forma predeterminada, si se envía un codificador toohello de entrada que contiene solo audio y no hay video, Hola activo de salida contiene archivos que contienen datos de solo audio. Algunos reproductores, incluido Azure Media Player (vea [esto](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) puede no ser capaz de toohandle dichos flujos. Puede usar este tooadd de codificador de configuración tooforce Hola una salida de la pista de vídeo monocromática toohello en ese escenario.

> [!NOTE]
> Al forzar Hola codificador tooinsert un tamaño de salida pista de vídeo aumenta Hola de hello activo de salida y, por tanto, Hola costos derivados de las tareas de codificación de Hola. Debe ejecutar las pruebas tooverify que este incremento resultante tiene solo un leve impacto en los cargos mensuales.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Inserción de vídeo al solo Hola velocidades de bits bajas

Supongamos que usa una codificación de velocidad de bits múltiples preestablecido como ["H264 varias velocidades de bits 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode todo el catálogo de transmisión por secuencias, que contiene una mezcla de archivos de vídeo y archivos de solo audio de entrada. En este escenario, cuando la entrada de hello no tiene ningún vídeo, puede que desee tooforce Hola codificador tooinsert un vídeo monocromática realizar el seguimiento en simplemente Hola velocidades de bits bajas, como opuesto tooinserting vídeo en cada velocidad de bits de salida. tooachieve, necesita hello toouse **InsertBlackIfNoVideoBottomLayerOnly** marca.

Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:

#### <a name="json-preset"></a>Valor preestablecido JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Valor preestablecido XML

Cuando se utiliza XML, utilice condición = "InsertBlackIfNoVideoBottomLayerOnly" como un atributo toohello **H264Video** elemento y condición = "InsertSilenceIfNoAudio" como un atributo demasiado**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Inserción de vídeo con todas las velocidades de bits de salida
Supongamos que usa una codificación de velocidad de bits múltiples preestablecido como ["H264 varias velocidades de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode todo el catálogo de transmisión por secuencias, que contiene una mezcla de archivos de vídeo y archivos de solo audio de entrada. En este escenario, cuando la entrada de hello no tiene ningún vídeo, puede que desee tooforce Hola codificador tooinsert realizar un seguimiento de un vídeo monocromático a todas las velocidades de bits de salida de hello. Esto garantiza que el resultado de los activos son todo homogéneos con toonumber respecto de las pistas de vídeo y pistas de audio. tooachieve, necesita toospecify Hola marca "InsertBlackIfNoVideo".

Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:

#### <a name="json-preset"></a>Valor preestablecido JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Valor preestablecido XML

Cuando se utiliza XML, utilice condición = "InsertBlackIfNoVideo" como un atributo toohello **H264Video** elemento y condición = "InsertSilenceIfNoAudio" como un atributo demasiado**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Girar un vídeo
Hola [Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md) admite la rotación de ángulos de 0/90/180 y 270. comportamiento predeterminado de Hello es "Auto", donde intenta toodetect Hola rotación metadatos en el archivo de vídeo entrante hello y compensar para él. Hola siguientes **orígenes** tooone de elemento de valores preestablecidos de hello definidos en [esto](media-services-mes-presets-overview.md) sección:

### <a name="json-preset"></a>Valor preestablecido JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Valor preestablecido XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Consulte también [esto](media-services-mes-schema.md#PreserveResolutionAfterRotation) tema para obtener más información sobre cómo codificador Hola interpreta la configuración de ancho y alto de Hola Hola predefinidos, cuando se activa la compensación de rotación.

Puede usar Hola valor "0" tooindicate toohello codificador tooignore rotación metadatos, si están presentes en vídeo de entrada de Hola.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Información general sobre la codificación de Servicios multimedia](media-services-encode-asset.md)
