---
title: "optimización de descarga de archivos de aaaLarge a través de la red de entrega de contenido de Azure Hola"
description: "Optimización de descargas de archivos grandes explicada en profundidad"
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
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Optimización de descarga de archivos grandes a través de la red de entrega de contenido de Azure Hola

Tamaño de los archivos de contenido que se envían a través de Internet de hello continuar toogrow debido tooenhanced funcionalidad, gráficos mejorados y contenido de medios enriquecidos. Este crecimiento se debe a muchos factores: el acceso de la banda ancha, dispositivos de almacenamiento de bajo costo, aumento generalizado de vídeo de alta definición y dispositivos conectados a Internet (IoT). Un mecanismo de entrega rápida y eficiente para archivos de gran tamaño es crítico tooensure una experiencia de consumidor suaves y divertida.

La entrega de archivos grandes tiene varios desafíos. En primer lugar, toodownload de tiempo medio de hello un archivo grande puede ser importante porque las aplicaciones no podrían descargar todos los datos de forma secuencial. En algunos casos, las aplicaciones podrían descargar la última parte de un archivo antes de la primera parte de Hola de Hola. Cuando se solicita solo una pequeña cantidad de un archivo o un usuario pone en pausa una descarga, puede producir un error en la descarga de Hola. descarga de Hello también se retrasa hasta después de hello red de entrega de contenido (CDN) recupera todo el archivo hello desde el servidor de origen de Hola. 

En segundo lugar, latencia Hola entre el equipo del usuario y el archivo hello determina la velocidad de hello en el que puede ver el contenido. Además, los problemas de capacidad y congestión de la red también afectan al rendimiento. Mayores distancias entre los servidores y los usuarios crean oportunidades adicionales para toooccur de pérdida de paquetes, lo que reduce la calidad. reducción de Hola de calidad que se deba a que un rendimiento limitado y pérdida de paquetes mayor puede aumentar el tiempo de espera de Hola para un toofinish de descarga de archivos. 

En tercer lugar, muchos archivos grandes no se envían en su totalidad. Los usuarios pueden cancelar una descarga a mitad de camino a través de o ver solo Hola primeros minutos de un vídeo MP4 largo. Por lo tanto, las empresas de entrega de software y los medios desean toodeliver solo parte de Hola de un archivo que se solicita. Distribución eficaz de hello solicitado partes reduce el tráfico de salida de hello desde el servidor de origen de Hola. Distribución eficaz también reduce la memoria de Hola y presión de E/S en el servidor de origen de Hola. 

Hola red de entrega de contenido de Azure de Akamai ahora proporciona una característica que proporciona archivos de gran tamaño eficazmente toousers entre mundo Hola a escala. característica de Hello reduce las latencias porque se reduce la carga de hello en los servidores de origen Hola. Esta característica está disponible con el nivel de precios de hello Akamai estándar.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Configurar una entrega de toooptimize de punto de conexión de red CDN de archivos grandes

Puede configurar la entrega de toooptimize de punto de conexión CDN para archivos grandes a través de hello portal de Azure. También puede usar nuestras API de REST o cualquiera de Hola cliente SDK toodo esto. Hello pasos siguientes muestran proceso Hola a través de hello portal de Azure.

1. un nuevo extremo en hello tooadd **perfil de CDN** página, seleccione **punto de conexión**.

    ![Nuevo punto de conexión](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. Hola **optimizado para** lista desplegable, seleccione **descarga de archivos grandes**.

    ![Optimización de archivos grandes seleccionada](./media/cdn-large-file-optimization/02_Creating.png)


Después de crear el extremo de red CDN Hola, aplica las optimizaciones de archivos grandes de Hola para todos los archivos que cumplan ciertos criterios. Hola siguiente sección describe este proceso.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Optimizar para la entrega de archivos de gran tamaño con hello red de entrega de contenido de Azure de Akamai

característica de optimización de tipos de archivo grande Hola activa las optimizaciones y las configuraciones toodeliver grandes archivos de red más rápido y mayor capacidad de respuesta. La entrega general en Internet con Akamai almacena en caché archivos solo inferior a 1,8 GB y puede túnel (no caché) archivos de too150 GB. Optimización de archivos grandes se almacena en memoria caché los archivos de too150 GB.

La optimización de archivos grandes es efectiva cuando se cumplen determinadas condiciones. Entre las condiciones se incluyen cómo funciona el servidor de origen de Hola y tamaños de Hola y tipos de archivos de Hola que se solicitan. Antes de entrar en detalles acerca de estos temas, debe entender cómo funciona la optimización de Hola. 

### <a name="object-chunking"></a>Fragmentación de objetos 

Hola red de entrega de contenido de Azure de Akamai utiliza una técnica denominada fragmentación de objeto. Cuando se solicita un archivo grande, CDN Hola recupera partes más pequeñas del archivo Hola Hola origen. Después de servidor de borde/POP de CDN Hola recibe una solicitud de archivo completo o intervalo de bytes, comprueba si el tipo de archivo de hello es compatible con esta optimización. También comprueba si el tipo de archivo de hello cumple requisitos de tamaño de archivo de Hola. Si el tamaño del archivo de hello es mayor que 10 MB, servidor de borde CDN Hola solicita archivo hello de origen de hello en fragmentos de 2 MB. 

Después de fragmento de hello llega al borde de la red CDN Hola, tiene almacenados en memoria caché y sirve inmediatamente toohello usuario. CDN Hola y el siguiente fragmento de Hola de captura en paralelo. Este precarga garantiza que el contenido de hello permanece un fragmento por delante de usuario de hello, lo que reduce la latencia. Este proceso continúa hasta que todo Hola se descarga el archivo (si se solicita), todos los intervalos de bytes disponibles (si se solicita), o cliente hello finaliza la conexión de Hola. 

Para obtener más información sobre la solicitud de intervalo de bytes de hello, consulte [7233 RFC](https://tools.ietf.org/html/rfc7233).

Hola CDN almacena en caché los fragmentos que se reciban. todo el archivo hello no tiene toobe almacena en caché en memoria caché CDN Hola. Las solicitudes posteriores de intervalos de archivos o bytes de Hola se sirven desde la memoria caché CDN Hola. Si no todos los fragmentos de Hola se almacenan en caché en la red CDN Hola, precarga es toorequest usado fragmentos desde el origen de Hola. Esta optimización se basa en la capacidad de Hola de solicitudes de intervalo de bytes de toosupport de servidor de origen de Hola. _Si el servidor de origen de hello no es compatible con las solicitudes de intervalo de bytes, esta optimización no es efectiva._ 

### <a name="caching"></a>Almacenamiento en caché
La optimización de archivos grandes usa tiempos de expiración de almacenamiento en caché predeterminados distintos a los de la entrega web general. Esto marca la diferencia entre el almacenamiento en caché positivo y el negativo, en función de códigos de respuesta HTTP. Si el servidor de origen de hello especifica un tiempo de expiración a través de un control de caché o expira el encabezado de respuesta de hello, CDN Hola respeta ese valor. Si no especifica el origen de Hola y archivo hello coincide con las condiciones de tipo y el tamaño de Hola para este tipo de optimización, CDN Hola usa valores predeterminados de hello para la optimización de archivos de gran tamaño. En caso contrario, CDN Hola usa valores predeterminados para la entrega de web general.


|    | Web general | Optimización de archivos grandes 
--- | --- | --- 
Almacenamiento en caché: positivo <br> HTTP 200, 203, 300, <br> 301, 302 y 410 | 7 días |1 día  
Almacenamiento en caché: negativo <br> HTTP 204, 305, 404, <br> y 405 | None | 1 segundo 

### <a name="deal-with-origin-failure"></a>Tratamiento del error de origen

tiempo de espera de lectura del origen de Hello aumenta de dos segundos en minutos de tootwo de entrega de web general para el tipo de optimización de archivos grandes de Hola. Este aumento representa tooavoid tamaños de archivo mayor de hello una conexión prematura de tiempo de espera.

Cuando se agota el tiempo de espera de una conexión, CDN Hola vuelve a intentar un número de veces antes de enviar a un cliente de toohello de error de "504: tiempo de espera de puerta de enlace". 

### <a name="conditions-for-large-file-optimization"></a>Condiciones para la optimización de archivos grandes

Hello en la tabla siguiente enumera conjunto Hola de criterios toobe satisfecho para la optimización de archivos de gran tamaño:

Condición | Valores 
--- | --- 
Tipos de archivo admitidos | 3g2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> gz, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> mpeg, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Tamaño de archivo mínimo | 10 MB 
Tamaño de archivo máximo | 150 GB 
Características del servidor de origen | Debe admitir solicitudes de intervalo de bytes 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Optimizar para la entrega de archivos de gran tamaño con hello red de entrega de contenido de Azure de Verizon

Hola red de entrega de contenido de Azure desde Verizon entrega archivos grandes sin un límite de tamaño de archivo. Características adicionales se activan mediante entrega de toomake predeterminado de archivos de gran tamaño con mayor rapidez.

### <a name="complete-cache-fill"></a>Relleno de la memoria caché completa

Hola predeterminado caché completa relleno posibilita la toopull CDN Hola un archivo en la memoria caché de hello cuando se abandona o se pierde una solicitud inicial. 

El relleno de la memoria caché completa es más útil para los recursos grandes. Normalmente, los usuarios no descargan desde toofinish de inicio. Usan la descarga progresiva. comportamiento predeterminado de Hello fuerza hello borde server tooinitiate una captura de fondo del activo de Hola desde el servidor de origen de Hola. A continuación, activo de Hola se encuentra en caché local del servidor de hello borde. Una vez objetos hello en memoria caché de hello, servidor perimetral de hello cumple toohello de las solicitudes de intervalo de bytes CDN para el objeto almacenado en caché de Hola.

comportamiento predeterminado de Hello puede deshabilitarse a través del motor de reglas de Hola Hola nivel Verizon Premium.

### <a name="peer-cache-fill-hot-filing"></a>Creación de archivos activos de llenado de la caché del mismo nivel

característica del caché relleno caliente de rellenado de Hello predeterminada del mismo nivel utiliza un sofisticado algoritmo propietario. Usa almacenamiento en caché de los servidores basados en el ancho de banda de borde adicional y agregado solicitudes métricas toofulfill cliente para los objetos grandes tremendamente populares. Esta característica impide que una situación en la que gran número de solicitudes adicionales se envía el servidor de origen del usuario tooa. 

### <a name="conditions-for-large-file-optimization"></a>Condiciones para la optimización de archivos grandes

características de optimización de Hola para Verizon están activadas de forma predeterminada. No hay ningún límite en el tamaño de archivo máximo. 

## <a name="additional-considerations"></a>Consideraciones adicionales

Considere la posibilidad de hello después aspectos adicionales para este tipo de optimización.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Azure Content Delivery Network de Akamai

- Hola fragmentación proceso genera el servidor de origen de toohello las solicitudes adicionales. Sin embargo, hello general volumen de datos entregados desde origen hello es mucho menor. Fragmentación da como resultado una mejor las características de almacenamiento en caché en la red CDN Hola.

- Memoria y presión de E/S se reducen en origen Hola porque se entregan las partes más pequeñas de archivo hello.

- Para fragmentos almacenado en caché en la red CDN Hola, no hay ninguna solicitud adicional toohello origen hasta que expira el contenido de Hola o se expulsa de la memoria caché de Hola.

- Los usuarios pueden realizar intervalo solicita toohello CDN y se va a tratar como cualquier archivo normal. La optimización se aplica solo si es un tipo de archivo válido y el intervalo de bytes de hello es entre 10 MB y 150 GB. Si el tamaño medio de los archivos de hello solicitado es menor que 10 MB, conviene entrega de toouse web general en su lugar.

### <a name="azure-content-delivery-network-from-verizon"></a>Azure Content Delivery Network de Verizon

tipo de optimización de entrega de Hello web general puede entregar los archivos de gran tamaño.
