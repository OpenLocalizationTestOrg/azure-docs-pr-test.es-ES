---
title: entrega de contenido de Azure para su escenario de aaaOptimize
description: "¿Cómo toooptimize entrega del contenido para escenarios concretos"
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
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Optimizar la entrega de contenido de Azure para su escenario

Cuando entregue contenido tooa audiencia global grandes, es entrega de hello optimizado tooensure críticos de su contenido. Hola red de entrega de contenido de Azure puede optimizar la experiencia de entrega de hello en función de tipo de Hola de contenido que tiene. El contenido puede ser un sitio web, una transmisión en directo, un vídeo o un archivo grande para su descarga. Cuando se crea un punto de conexión de entrega de contenido (CDN) de red, especificar un escenario en hello **optimizado para** opción. Su elección determina qué optimización está aplicada toohello contenido vaya a entregar desde el punto de conexión de red CDN Hola.

Opciones de optimización son toouse diseñada comportamientos de prácticas recomendadas tooimprove entrega de contenido rendimiento y la descarga de origen mejor. Las opciones de escenario afectar al rendimiento mediante la modificación de las configuraciones de almacenamiento parcial en caché, objeto de fragmentación y directiva de reintentos de error de origen de Hola. 

En este artículo se proporciona una introducción a las diversas características de optimización y cuándo se deben usar. Para obtener más información sobre las características y limitaciones, vea los artículos correspondientes de Hola en cada tipo de optimización individuales.

> [!NOTE]
> Su **optimizado para** opciones pueden variar en función de proveedor de Hola que seleccione. Proveedores CDN aplican la mejora de maneras diferentes, según el escenario de Hola. 

## <a name="provider-options"></a>Opciones de proveedor

Red de entrega de contenido de Azure de Akamai Hello es compatible con:

* Entrega web general 

* Streaming multimedia general

* Streaming multimedia de vídeo a petición

* Descarga de archivos de gran tamaño

* Aceleración de sitios dinámicos 

Hola red de entrega de contenido de Azure desde Verizon admite la entrega de web general solo. Se puede usar para vídeo bajo demanda y descarga de archivos grandes. Tooselect no tiene un tipo de optimización.

Recomendamos encarecidamente que pruebe las variaciones de rendimiento entre proveedor óptimo Hola de diferentes proveedores tooselect para su entrega.

## <a name="select-and-configure-optimization-types"></a>Seleccionar y configurar los tipos de optimización

toocreate un nuevo punto de conexión, seleccione un tipo de optimización que mejor coincida con el escenario de Hola y el tipo de contenido que se desea Hola toodeliver de punto de conexión. **Entrega de web general** es la selección predeterminada de Hola. Puede actualizar la opción de optimización de Hola para cualquier extremo de Akamai existente en cualquier momento. Este cambio no interrumpa la entrega de CDN Hola. 

1. Seleccione un punto de conexión del perfil estándar de Akamai.

    ![Selección de punto de conexión ](./media/cdn-optimization-overview/01_Akamai.png)

2. En **CONFIGURACIÓN**, seleccione **Optimización**. A continuación, seleccione un tipo de hello **optimizado para** lista desplegable.

    ![Selección de la optimización y el tipo.](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Optimización de escenarios específicos

Puede optimizar el extremo de red CDN Hola para uno de los escenarios siguientes de Hola. 

### <a name="general-web-delivery"></a>Entrega web general

Entrega de web general es la opción de optimización más comunes de Hola. Está diseñada para la optimización de contenido web general, como páginas web y aplicaciones web. Esta optimización puede usarse también para la descarga de archivos y vídeos.

Un sitio web típico incluye contenido estático y dinámico. Contenido estático incluye imágenes, las bibliotecas de JavaScript y hojas de estilos que se pueden almacenan en caché y entregan toodifferent a los usuarios. Contenido dinámico está personalizado para un usuario individual, como elementos de noticias que adaptan tooa perfil de usuario. Contenido dinámico no está almacenado en memoria caché porque es usuario de tooeach único, como el contenido del carro de la compra. La entrega web general puede optimizar todo el sitio web. 

> [!NOTE]
> Si usas Hola red de entrega de contenido de Azure de Akamai, conviene toouse esta optimización si el tamaño medio de los archivos es menor que 10 MB. Si el tamaño medio de los archivos es superior a 10 MB, seleccione **descarga de archivos grandes** de hello **optimizado para** lista desplegable.

### <a name="general-media-streaming"></a>Streaming multimedia general

Si necesita el punto de conexión de toouse Hola de transmisión por secuencias de vídeo bajo demanda y transmisión por secuencias en directo, se recomienda la optimización de transmisión por secuencias de multimedia general.

Transmisión por secuencias multimedia es tiempo confidencial, ya que los paquetes que llegan en tiempo de ejecución en el cliente de Hola pueden provocar una experiencia de visualización degradado, como el almacenamiento en búfer frecuentes en contenido de vídeo. Optimización de la transmisión por secuencias reduce la latencia de Hola de entrega de contenido multimedia y ofrece una experiencia de transmisión por secuencias suave para los usuarios. 

Es un escenario común para los clientes de Azure Media Services. Cuando usa Azure Media Services, obtiene un punto de conexión de streaming que puede usarse para streaming en vivo y bajo demanda. Con este escenario, los clientes no necesitan tooswitch tooanother extremo cuando cambian de transmisión por secuencias en directo tooon a petición. La optimización de streaming multimedia general admite este tipo de escenario.

Red de entrega de contenido de Azure de Verizon Hello usa hello web general entrega optimización tipo toodeliver transmisión por secuencias contenido multimedia.

vea toolearn más información acerca de la optimización, la transmisión por secuencias [optimización la transmisión por secuencias](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Streaming multimedia de vídeo a petición

La optimización del streaming multimedia de vídeo a petición mejora el contenido que se transmite a petición. Si usa un punto de conexión para la transmisión por secuencias de vídeo bajo demanda, conviene toouse esta opción.

Red de entrega de contenido de Azure de Verizon Hello usa hello web general entrega optimización tipo toodeliver transmisión por secuencias contenido multimedia.

vea toolearn más información acerca de la optimización, la transmisión por secuencias [optimización la transmisión por secuencias](cdn-media-streaming-optimization.md).

> [!NOTE]
> Si el punto de conexión de hello sirve principalmente contenido de vídeo bajo demanda, use este tipo de optimización. Hola la diferencia principal entre esta optimización y la optimización de transmisión por secuencias de multimedia general de hello consiste en tiempo de espera de reintento de conexión de Hola. tiempo de espera de Hello es mucho más corta toowork con escenarios de transmisión por secuencias en directo.

### <a name="large-file-download"></a>Descarga de archivos de gran tamaño

Si usas Hola red de entrega de contenido de Azure de Akamai, debe usar archivos de toodeliver de descarga de archivos grandes mayores de 1,8 GB. Hola red de entrega de contenido de Azure de Verizon no tiene una limitación en el archivo de tamaño en su optimización de entrega de web general de la descarga.

Si usas Hola red de entrega de contenido de Azure de Akamai, descargas de archivos grandes se optimizan para el contenido de más de 10 MB. Si el tamaño medio de los archivos es menor que 10 MB, conviene entrega de toouse web general. Si los tamaños de archivos promedio son constantemente superiores a 10 MB, podría ser más eficaz toocreate un extremo independiente para archivos de gran tamaño. Por ejemplo, las actualizaciones de firmware o software normalmente son archivos grandes.

Red de entrega de contenido de Azure de Verizon Hello usa hello web general entrega optimización tipo toodeliver transmisión por secuencias contenido multimedia.

toolearn más información acerca de la optimización de archivos de gran tamaño, vea [optimización de archivos grandes](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Aceleración de sitios dinámicos

 La aceleración de sitios dinámicos está disponible en los perfiles de Content Delivery Network de Akamai y Verizon. Esta optimización implica un toouse cuota adicional. Para obtener más información, vea Hola página de precios.

Aceleración de sitio dinámico incluye diversas técnicas que se benefician de latencia de Hola y el rendimiento de contenido dinámico. Las técnicas incluyen la optimización de rutas y redes, la optimización de TCP y mucho más. 

Puede usar esta aplicación web que incluye muchas de las respuestas que no estén almacenable en caché de tooaccelerate de optimización. Algunos ejemplos son los resultados de búsquedas, transacciones de finalización de la compra o datos en tiempo real. Puede continuar capacidades de almacenamiento en caché de CDN de principales y toouse para datos estáticos. 



