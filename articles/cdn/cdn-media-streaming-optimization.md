---
title: "aaaMedia optimización a través de la red de entrega de contenido de Azure Hola de transmisión por secuencias"
description: Optimizar el streaming de archivos multimedia para una entrega sin problemas
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Optimización a través de la red de entrega de contenido de Azure Hola la transmisión por secuencias 
 
Uso de vídeo de alta definición está aumentando en hello Internet, lo que crea problemas de entrega eficaz de archivos grandes. Los clientes esperan una reproducción suave de vídeo a petición o live recursos de vídeo en una variedad de clientes y redes todo Hola a todos. Un mecanismo de entrega rápida y eficiente para archivos de la transmisión por secuencias es crítico tooensure una experiencia de consumidor suaves y divertida.  

Multimedia de transmisión por secuencias en directo es especialmente difícil toodeliver debido a tamaños grandes de Hola y el número de usuarios simultáneos. Grandes retrasos provocar tooleave de los usuarios. Porque secuencias en directo no pueden almacenarse en memoria caché antes de tiempo y las latencias largas no tooviewers aceptable, se deben entregar fragmentos de vídeo de una manera oportuna. 

los patrones de solicitud de Hola de transmisión por secuencias también proporcionan algunos desafíos nuevos. Cuando se publica una secuencia en directo popular o una nueva serie de vídeo bajo demanda, miles toomillions de visores podría solicitar el flujo de hello en hello mismo tiempo. En este caso, solicitud inteligente consolidación es vital toonot sobrecargando servidores de origen de hello cuando no se almacena en caché activos Hola todavía.
 
Hola red de entrega de contenido de Azure de Akamai ahora proporciona una característica que proporciona a recursos de transmisión por secuencias multimedia eficazmente toousers entre mundo Hola a escala. característica de Hello reduce las latencias porque se reduce la carga de hello en los servidores de origen Hola. Esta característica está disponible con el nivel de precios de hello Akamai estándar. 

Hola red de entrega de contenido de Azure desde Verizon entrega multimedia de transmisión por secuencias directamente en el tipo de optimización de entrega de hello web general.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Configurar un punto de conexión toooptimize streaming multimedia en red de entrega de contenido de Azure de Akamai Hola
 
Puede configurar la entrega de toooptimize de punto de conexión de entrega de contenido (CDN) de red para archivos grandes a través del portal de Azure de Hola. También puede usar nuestras API de REST o cualquiera de Hola cliente SDK toodo esto. Hello pasos siguientes muestran proceso Hola a través de hello portal de Azure:

1. un nuevo extremo en hello tooadd **perfil de CDN** página, seleccione **punto de conexión**.
  
    ![Nuevo punto de conexión](./media/cdn-media-streaming-optimization/01_Adding.png)

2. Hola **optimizado para** lista desplegable, seleccione **vídeo de transmisión por secuencias de multimedia de petición** para los activos de vídeo bajo demanda. Si realiza una combinación de streaming en vivo y bajo demanda, seleccione **Streaming multimedia general**.

    ![Streaming seleccionado](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Después de crear el punto de conexión de hello, se aplica la optimización de Hola para todos los archivos que cumplan ciertos criterios. Hola siguiente sección describe este proceso. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Optimizaciones de red de entrega de contenido de Azure de Akamai Hola la transmisión por secuencias
 
La optimización del streaming multimedia de Akamai es eficaz para el streaming multimedia en vivo o de vídeo bajo demanda que usa fragmentos multimedia individuales para la entrega. Este proceso es diferente a la transferencia de un solo recurso de gran tamaño a través de descarga progresiva o mediante solicitudes de intervalo de bytes. Para obtener información sobre ese estilo de entrega multimedia, vea [Optimización de archivos grandes](cdn-large-file-optimization.md).


Hello general vídeo bajo demanda o entrega multimedia entrega optimización tipos de medios utilizan el CDN con recursos multimedia de optimizaciones de back-end toodeliver con mayor rapidez. También usan configuraciones para recursos multimedia en función de procedimientos recomendados aprendidos con el tiempo.

### <a name="caching"></a>Almacenamiento en caché

Si Hola red de entrega de contenido de Azure de Akamai detecta que dicho activo hello es un manifiesto de transmisión por secuencias o fragmento, usa distintos tiempos de expiración de almacenamiento en caché de entrega de web general. (Vea la lista completa de hello en hello en la tabla siguiente). Como siempre, se respetan cache-control o encabezados Expires enviados desde el origen de Hola. Si Hola activo no es un recurso multimedia, almacena en caché mediante el uso de tiempos de expiración de hello para la entrega de web general.

tiempo de almacenamiento en caché negativo corto Hello es útil para la descarga de origen cuando muchos usuarios solicitan un fragmento que no existe todavía. Un ejemplo es una secuencia en directo que paquetes de saludo no están disponibles desde el origen de hello ese segundo. intervalo de almacenamiento en caché ya Hello también ayuda a descargar las solicitudes desde el origen de hello porque normalmente no se modifique el contenido de vídeo.
 

|    | General<br> web<br>entrega | General<br> medios<br> streaming | Vídeo bajo demanda <br>medios<br> streaming  
--- | --- | --- | ---
Almacenamiento en caché: positivo <br> HTTP 200, 203, 300, <br> 301, 302 y 410 | 7 días |365 días | 365 días   
Almacenamiento en caché: negativo <br> HTTP 204, 305, 404, <br> y 405 | None | 1 segundo | 1 segundo
 
### <a name="deal-with-origin-failure"></a>Tratamiento del error de origen  

La entrega multimedia general y la entrega multimedia de vídeo bajo demanda también tienen tiempo de espera de origen y un registro de reintentos basado en los procedimientos recomendados para patrones de solicitud típicos. Por ejemplo, como entrega multimedia general es para en vivo y entrega de medios de vídeo bajo demanda, usa un tiempo de espera de conexión más corta debido toohello naturaleza de sujetos a limitación temporal de streaming en vivo.

Cuando se agota el tiempo de espera de una conexión, CDN Hola vuelve a intentar un número de veces antes de enviar a un cliente de toohello de error de "504: tiempo de espera de puerta de enlace". 

Cuando un archivo coincide con la lista de condiciones de tipo y el tamaño de los archivos de hello, CDN Hola usa un comportamiento de hello para la transmisión por secuencias. De lo contrario, se usa la entrega web general.
   
### <a name="conditions-for-media-streaming-optimization"></a>Condiciones para la optimización de streaming multimedia 

Hello en la tabla siguiente enumera conjunto Hola de criterios toobe satisfecho para la optimización de transmisión por secuencias: 
 
Tipos de streaming admitidos | Extensiones de archivo  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, clave, ts y aac
Adobe HDS | f4m, f4x, drmmeta, arranque, f4f,<br>Estructura de dirección URL Seg-Frag <br> (expresión regular de coincidencia: ^(/.*)Seq(\d+)-Frag(\d+))
DASH | mpd, guión, divx, ismv, m4s, m4v, mp4,. mp4v, <br> sidx, webm, mp4a, m4a y isma
Streaming con velocidad de transmisión adaptable | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Optimizaciones de red de entrega de contenido de Azure desde Verizon Hola la transmisión por secuencias

Hola red de entrega de contenido de Azure desde Verizon ofrece a recursos de multimedia de transmisión por secuencias directamente mediante el tipo de optimización de entrega de hello web general. Algunas de las características de red CDN Hola assist directamente en la entrega de recursos multimedia de forma predeterminada.

### <a name="partial-cache-sharing"></a>Uso compartido de caché parcial

Uso compartido de caché parcial permite que las solicitudes de contenido toonew de hello CDN tooserve parcialmente en caché. Por ejemplo, si Hola primera solicitud toohello CDN da como resultado un error de caché, Hola se envía solicitud toohello origen. Aunque este contenido incompleta se carga en memoria caché CDN Hola, otro toohello solicitudes CDN puede empezar a recibir estos datos. 

### <a name="cache-fill-wait-time"></a>Tiempo de espera de relleno de caché

 característica de tiempo de espera de relleno de caché de Hello fuerza hello borde server toohold todas las solicitudes subsiguientes para Hola mismo recurso hasta que la respuesta HTTP encabezados proceden del servidor de origen Hola. Si los encabezados de respuesta HTTP desde el origen de hello llegan antes de que expire el temporizador de hello, todas las solicitudes que se han puesto en espera se sirven de hello aumentando la memoria caché. En hello mismo tiempo, hello caché se llena con datos de origen de Hola. De forma predeterminada, el tiempo de espera de relleno de caché de Hola se establece too3, 000 milisegundos. 

