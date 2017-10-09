---
title: "esquema estándar de codificador aaaMedia | Documentos de Microsoft"
description: "tema de Hello ofrezca una visión general de esquema estándar de codificador multimedia de Hola."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Esquema de Media Encoder Standard
Este tema describen algunos de los elementos de Hola y tipos de esquema XML de hello en el que [presintonías Media Encoder estándar](media-services-mes-presets-overview.md) se basan. tema de Hello ofrece una explicación de los elementos y sus valores válidos. esquema de Hello completa se publicará en una fecha posterior.  

## <a name="Preset"></a> Preset (elemento raíz)
Define un valor preestablecido de codificación.  

### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Encoding** |[Encoding](media-services-mes-schema.md#Encoding) |Elemento raíz, indica que los orígenes de entrada de hello toobe codificado. |
| **Outputs** |[Outputs](media-services-mes-schema.md#Output) |Colección de archivos de salida deseados. |

### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Versión**<br/><br/> Obligatorio |**xs:decimal** |Hola había preestablecido de la versión. Hello las restricciones siguientes se aplican: valor xs:fractionDigits = "1" y xs:minInclusive value = "1" por ejemplo, **versión = "1.0"**. |

## <a name="Encoding"></a> Encoding
Contiene una secuencia de hello siguientes elementos.  

### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Configuración de la codificación H.264 de vídeo. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Configuración de la codificación AAC de audio. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Configuración de la imagen Bmp. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Configuración de la imagen Png. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Configuración de la imagen Jpg. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |Actualmente, solo se admite la codificación en un solo paso. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |Determina Hola fijada espaciado entre marcos IDR en unidades de segundos. También se conoce duración del GOP tooas Hola. Vea **SceneChangeDetection** (a continuación) para controlar si hello codificador puede desviarse de este valor. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default=”false” |**xs:boolean** |Si set tootrue, intentos de codificador escena toodetect cambiar en vídeo de hello e inserta un marco IDR. |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |Controles Hola equilibrio entre codificar calidad de velocidad y el vídeo. Puede ser uno de hello siguientes valores: **velocidad**, **equilibrada**, o **calidad**<br/><br/> Valor predeterminado: **Balanced** |
| **SyncMode**<br/><br/> minOccurs="0" | |La característica se expondrá en versiones futuras. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Colección de capas de vídeo de salida. |

### <a name="attributes"></a>Attributes
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Condition** |**xs:string** | Cuando la entrada de hello no tiene ningún vídeo, puede que desee tooforce Hola codificador tooinsert una pista de vídeo monocromática. toodo que usar condición = "InsertBlackIfNoVideoBottomLayerOnly" (tooinsert un vídeo en solo Hola menor velocidad de bits) o la condición = "InsertBlackIfNoVideo" (tooinsert un vídeo a todas las velocidades de bits de salida). Para obtener más información, consulte [este tema](media-services-advanced-encoding-with-mes.md#no_video) .|

## <a name="H264Layers"></a> H264Layers

De forma predeterminada, si envía un codificador toohello de entrada que contiene solo audio y no hay video, Hola activo de salida contiene archivos con datos de audio solo. Algunos reproductores no pueden tener toohandle tal flujos de salida. Puede usar de hello H264Video **InsertBlackIfNoVideo** atributo estableciendo tooforce Hola codificador tooadd una salida de toohello de pista de vídeo en ese escenario. Para obtener más información, consulte [este tema](media-services-advanced-encoding-with-mes.md#no_video) .
              
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Una colección de capas H264. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> Límites de vídeo se basan en valores de hello descritos en hello [H264 niveles](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) tabla.  
> 
> 

### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Perfil**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** |Puede ser de uno de los siguientes hello **xs: String** valores: **automática**, **previsto**, **Main**, **alta**. |
| **Level**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |velocidad de bits de Hello utilizada para esta capa de vídeo, especificada en kbps. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |Hola máxima velocidad de bits utilizada para esta capa de vídeo, especificada en kbps. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs:time** |Longitud del búfer de vídeo de Hola. |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Ancho del marco de las vídeo de salida de hello, en píxeles.<br/><br/> Tenga en cuenta que, actualmente, debe especificar ancho y alto. Hola ancho y alto necesitan que los números de par toobe. |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Alto de hello salida vídeo fotograma, en píxeles.<br/><br/> Tenga en cuenta que, actualmente, debe especificar ancho y alto. Hola ancho y alto necesitan que los números de par toobe.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |Número de fotogramas B entre fotogramas de referencia. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |Número de fotogramas de referencia en un GOP. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default=”Cabac” |**xs:string** |Puede ser uno de hello siguientes valores: **Cabac** y **Cavlc**. |
| **FrameRate**<br/><br/> minOccurs="0" |número racional |Determina la velocidad de fotogramas de Hola de salida de hello vídeo. Utilice el valor predeterminado es "0/1" toolet Hola codificador uso Hola mismo marco clasificar como Hola de entrada de vídeo. Los valores permitidos son toobe esperado velocidades de fotogramas de vídeo comunes, tal y como se muestra a continuación. No obstante, se admite cualquier número racional válido. Por ejemplo, 1/1 sería 1 fps y es válido.<br/><br/> - 12/1  (12 fps)<br/><br/> - 15/1 (15 fps)<br/><br/> - 24/1 (24 fps)<br/><br/> - 24000/1001 (23,976 fps)<br/><br/> - 25/1 (25 fps)<br/><br/>  - 30/1 (30 fps)<br/><br/> - 30000/1001 (29,97 fps) <br/> <br/>**Tenga en cuenta** si va a crear un ajuste preestablecido para la codificación de velocidad de bits múltiple personalizado, todas las capas de hello preestablecido **debe** uso Hola mismo valor de velocidad de fotogramas.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |Copia de Azure Media Encoder. |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |Determina en cuántos segmentos se divide un fotograma. Se recomienda usar el valor predeterminado. |

## <a name="AACAudio"></a> AACAudio
 Contiene una secuencia de hello siguientes elementos y grupos.  

 Para más información acerca de AAC, consulte [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Perfil**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Puede ser uno de hello siguientes valores: **AACLC**, **HEAACV1**, o **HEAACV2**. |

### <a name="attributes"></a>Attributes
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce Hola codificador tooproduce un activo que contenga una pista de audio silenciosa cuando entrada no tiene oye ningún sonido, especifique el valor de "InsertSilenceIfNoAudio" Hola.<br/><br/> De forma predeterminada, si envía un codificador de entrada toohello que solo no contiene vídeo, se oye ningún sonido, a continuación, Hola activo de salida contiene archivos que contienen datos de solo vídeo. Algunos reproductores no pueden tener toohandle tal flujos de salida. Puede usar este tooadd de codificador de hello configuración tooforce una salida de toohello silenciosa pista de audio en ese escenario. |

### <a name="groups"></a>Grupos
| Referencia | Descripción |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |Consulte la descripción de [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow Hola número apropiado de canales, la velocidad de muestreo y velocidad de bits que se pueden establecer para cada perfil. |

## <a name="AudioGroup"></a> AudioGroup
Para obtener más información acerca de qué valores son válidos para cada perfil, vea tabla "Detalles de códec de Audio" hello siguiente.  

### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |número de Hola de canales de audio codificados. Hello siguiente es opciones válidas: 1, 2, 5, 6, 8.<br/><br/> Valor predeterminado: 2. |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |velocidad de muestreo de audio de Hello, especificado en Hz. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |velocidad de bits de Hello utilizada al codificar audio hello, especificada en kbps. |

### <a name="audio-codec-details"></a>Detalles de códec de audio
Códec de audio|Detalles  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025: 8 &lt;= velocidad de bits &lt; 16<br/><br/> - 12000: 8 &lt;= velocidad de bits &lt; 16<br/><br/> - 16000: 8 &lt;= velocidad de bits &lt;32<br/><br/>- 22050: 24 &lt;= velocidad de bits &lt; 32<br/><br/> - 24000: 24 &lt;= velocidad de bits &lt; 32<br/><br/> - 32000: 32 &lt;= velocidad de bits &lt;= 192<br/><br/> - 44100: 56 &lt;= velocidad de bits &lt;= 288<br/><br/> - 48000: 56 &lt;= velocidad de bits &lt;= 288<br/><br/> - 88200: 128 &lt;= velocidad de bits &lt;= 288<br/><br/> - 96000: 128 &lt;= velocidad de bits &lt;= 288<br/><br/> 2.<br/><br/> - 11025: 16 &lt;= velocidad de bits &lt; 24<br/><br/> - 12000: 16 &lt;= velocidad de bits &lt; 24<br/><br/> - 16000: 16 &lt;= velocidad de bits &lt; 40<br/><br/> - 22050: 32 &lt;= velocidad de bits &lt; 40<br/><br/> - 24000: 32 &lt;= velocidad de bits &lt; 40<br/><br/> - 32000: 40 &lt;= velocidad de bits &lt;= 384<br/><br/> - 44100: 96 &lt;= velocidad de bits &lt;= 576<br/><br/> - 48000: 96 &lt;= velocidad de bits &lt;= 576<br/><br/> - 88200: 256 &lt;= velocidad de bits &lt;= 576<br/><br/> - 96000: 256 &lt;= velocidad de bits &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000: 160 &lt;= velocidad de bits &lt;= 896<br/><br/> - 44100: 240 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 48000: 240 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 88200: 640 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 96000: 640 &lt;= velocidad de bits &lt;= 1024<br/><br/> 8:<br/><br/> - 32000: 224 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 44100: 384 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 48000: 384 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 88200: 896 &lt;= velocidad de bits &lt;= 1024<br/><br/> - 96000: 896 &lt;= velocidad de bits &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050: velocidad de bits = 8<br/><br/> - 24000: 8 &lt;= velocidad de bits &lt;= 10<br/><br/> - 32000: 12 &lt;= velocidad de bits &lt;= 64<br/><br/> - 44100: 20 &lt;= velocidad de bits &lt;= 64<br/><br/> - 48000: 20 &lt;= velocidad de bits &lt;= 64<br/><br/> - 88200: velocidad de bits = 64<br/><br/> 2.<br/><br/> - 32000: 16 &lt;= velocidad de bits &lt;= 128<br/><br/> - 44100: 16 &lt;= velocidad de bits &lt;= 128<br/><br/> - 48000: 16 &lt;= velocidad de bits &lt;= 128<br/><br/> - 88200 : 96 &lt;= velocidad de bits &lt;= 128<br/><br/> - 96000 : 96 &lt;= velocidad de bits &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000: 64 &lt;= velocidad de bits &lt;= 320<br/><br/> - 44100: 64 &lt;= velocidad de bits &lt;= 320<br/><br/> - 48000: 64 &lt;= velocidad de bits &lt;= 320<br/><br/> - 88200: 256 &lt;= velocidad de bits &lt;= 320<br/><br/> - 96000: 256 &lt;= velocidad de bits &lt;= 320<br/><br/> 8:<br/><br/> - 32000: 96 &lt;= velocidad de bits &lt;= 448<br/><br/> - 44100 : 96 &lt;= velocidad de bits &lt;= 448<br/><br/> - 48000: 96 &lt;= velocidad de bits &lt;= 448<br/><br/> - 88200: 384 &lt;= velocidad de bits &lt;= 448<br/><br/> - 96000: 384 &lt;= velocidad de bits &lt;= 448  
**HEAACV2**|2.<br/><br/> - 22050: 8 &lt;= velocidad de bits &lt;= 10<br/><br/> - 24000: 8 &lt;= velocidad de bits &lt;= 10<br/><br/> - 32000: 12 &lt;= velocidad de bits &lt;= 64<br/><br/> - 44100: 20 &lt;= velocidad de bits &lt;= 64<br/><br/> - 48000: 20 &lt;= velocidad de bits &lt;= 64<br/><br/> - 88200: 64 &lt;= velocidad de bits &lt;= 64  
  

## <a name="Clip"></a> Clip
### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **StartTime** |**xs:duration** |Especifica la hora de inicio de Hola de una presentación. valor de Hola de StartTime debe toomatch Hola absoluta las marcas de tiempo de vídeo de entrada de Hola. Por ejemplo, si hello primer fotograma de vídeo de entrada de hello tiene una marca de tiempo de 12:00:10.000, StartTime debe tener al menos 12:00:10.000 o superior. |
| **Duration** |**xs:duration** |Especifica la duración de Hola de una presentación (por ejemplo, la apariencia de superposición de vídeo de hello). |

## <a name="Output"></a> Output
### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **FileName** |**xs:string** |nombre de Hola Hola del archivo de salida.<br/><br/> Puede utilizar macros descritas en hello siguiendo los nombres de archivo de salida de tabla toobuild Hola. Por ejemplo:<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Macros
| Macro | Descripción |
| --- | --- |
| **{Basename}** |Si está realizando la codificación VoD, Hola {Basename} es Hola 32 primeros caracteres de propiedad de AssetFile.Name de hello del archivo principal de hello en el recurso de entrada de Hola.<br/><br/> Si el recurso de entrada de hello es un archivo dinámico, a continuación, hello {Basename} se deriva de atributos de trackName hello en el manifiesto del servidor de Hola. Si va a enviar un trabajo de subclip mediante hello TopBitrate, como en: "< VideoStream\>TopBitrate < / VideoStream\>" y archivo de salida de hello contiene vídeo, a continuación, Hola {Basename} es Hola 32 primeros caracteres de hello trackName de hello capa de vídeo con velocidad de bits más alta de Hola.<br/><br/> Si en su lugar, envía un trabajo de subclip usando el máximo de velocidades de bits de entrada hello, como "< VideoStream\>* < / VideoStream\>" y archivo de salida de hello contiene vídeo, a continuación, {Basename} es hello primero 32 caracteres de hello trackName de nivel de vídeo correspondiente de Hola. |
| **{Codec}** |Se asigna demasiado "H264" de vídeo y "AAC" para que el audio. |
| **{Bitrate}** |Hola destino vídeo velocidad de bits si el archivo de salida de hello contiene audio y vídeo o velocidad de bits de audio de destino si el archivo de salida de hello sólo audio. valor de Hola que se utiliza es la velocidad de bits de hello en kbps. |
| **{Channel}** |Número de canales de audio si archivo hello contiene audio. |
| **{Width}** |Ancho del vídeo, en píxeles, en el archivo de salida de hello, si el archivo hello contiene vídeo Hola. |
| **{Height}** |Alto del vídeo, en píxeles, en el archivo de salida de hello, si el archivo hello contiene vídeo Hola. |
| **{Extension}** |Hereda de la propiedad "Tipo" archivo de salida de hello de Hola. nombre de archivo de salida de Hello tendrá una extensión que es uno de: "mp4", "ts", "jpg", "png" o "bmp". |
| **{Index}** |Obligatorio para una miniatura. Solo debe estar presente una vez. |

## <a name="Video"></a> Video (tipo complejo que hereda de Codec)
### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Iniciar** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |Para ver una explicación detallada, vea Hola pasos de la sección: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
Se recomienda marca de PreserveResolutionAfterRotation toouse hello en combinación con los valores de resolución expresados en términos de porcentaje (Width = "100%", Height = "100%").  

De forma predeterminada, Hola codificar la configuración de resolución (ancho, alto) Hola valores preestablecidos de medios codificador estándar (MES) se dirigen a vídeos con rotación de 0 grados. Por ejemplo, si el vídeo de entrada es 1280 x 720 con cero rotación de grado, a continuación, Hola preestablecidos Asegúrese de que salida de hello tiene Hola misma resolución. Vea la ilustración siguiente.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Sin embargo, esto significa que si el vídeo de entrada de Hola se ha capturado con rotación distinto de cero (p. ej. una tableta o smartphone mantiene verticalmente), a continuación, MES, de forma predeterminada aplicará Hola codificar la resolución de vídeo de entrada toohello de configuración (ancho, alto) y, a continuación, compensar la rotación de Hola. Por ejemplo, vea la figura Hola siguiente. valor preestablecido de Hello usa ancho = "100%", Height = "100%", que se interpreta el MES que requieran Hola salida toobe 1280 píxeles amplia y 720 píxeles de alto. Después de la rotación de vídeo de hello, lo, a continuación, reduce Hola imagen toofit en esa ventana, lo que conduce áreas toopillar cuadro en hello izquierdo y derecho.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Si Hola anterior no es el comportamiento de hello deseado, puede hacer que el uso de hello PreserveResolutionAfterRotation marca y establecerlo como demasiado "true" (el valor predeterminado es "false"). Por lo que si el valor preestablecido tiene un ancho = "100%", alto = "100%" y PreserveResolutionAfterRotation establecido demasiado "true", un resultado con cero rotación grado pero 720 píxeles de ancho y 1280 será un vídeo de entrada que es 1280 píxeles de ancho y 720 píxeles de alto con la rotación de 90 grados píxeles de alto. Vea Hola figura siguiente.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (grupo)
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>Elemento
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>Elemento
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>Elemento
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |Valores válidos: 1 (peor)-100 (mejor) |

### <a name="attributes"></a>Atributos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (tipo complejo que hereda de Video)
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Capas Png |

## <a name="JpgImage"></a> JpgImage (tipo complejo que hereda de Video)
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Capas Png |

## <a name="PngImage"></a> PngImage (tipo complejo que hereda de Video)
### <a name="elements"></a>Elementos
| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Capas Png |

## <a name="examples"></a>Ejemplos
Consulte ejemplos de valores preestablecidos de XML que se generan a partir de este esquema en [Task Presets for MES (Media Encoder Standard)](media-services-mes-presets-overview.md) (Valores preestablecidos de tareas para MES [Media Encoder Standard]).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

