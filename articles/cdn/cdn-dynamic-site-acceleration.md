---
title: "aaaDynamic aceleración de sitio a través de la red CDN de Azure"
description: "Profundización de la aceleración de sitios dinámicos"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Aceleración de sitios dinámicos a través de la red CDN de Azure

Con expansión de Hola de redes sociales, comercio electrónico y web de hello hyper personalizada, se genera un porcentaje creciente de hello contenido servido tooend a los usuarios en tiempo real. Los usuarios esperan experiencias web rápidas, confiables y personalizadas, independientemente de su explorador, ubicación, dispositivo o red. Sin embargo, innovaciones muy Hola que hacen estas experiencias tan apasionantes, también lenta página Descargas y calidad de hello de la experiencia del consumidor de hello correr el riesgo. 

Funcionalidad CDN estándar incluye Hola capacidad toocache archivos más cerca de tooend usuarios toospeed la entrega de archivos estáticos. Sin embargo, con aplicaciones web dinámicas, almacenamiento en caché contenido en ubicaciones de los bordes no es posible porque servidor hello genera contenido hello en el comportamiento de toouser de respuesta. Lo que acelera la entrega de Hola de este tipo de contenido es más complejo que el almacenamiento en caché perimetral tradicional y requiere una solución end-to-end que cada elemento a lo largo de la ruta de acceso de datos completo de Hola desde principio toodelivery se ajusta con precisión. Con Azure CDN dinámica sitio aceleración (DSA), mejorará en gran medida se mejora el rendimiento Hola de páginas web con contenido dinámico.

Azure CDN de Akamai y Verizon ofrece optimización DSA a través de hello **optimizado para** menú durante la creación del punto de conexión.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Configuración de la entrega de tooaccelerate de punto de conexión de red CDN de archivos dinámicos

Puede configurar la entrega de toooptimize de punto de conexión de red CDN de archivos dinámicos mediante el portal de Azure, seleccione hello **aceleración de sitio dinámico** opción situada debajo de hello **optimizado para** selección de propiedad durante creación de punto de conexión de Hola. También puede usar nuestras API de REST o cualquiera de toodo de SDK de cliente de Hola Hola lo mismo mediante programación. 

### <a name="probe-path"></a>Ruta de acceso de sondeo
Ruta de acceso de sondeo es un tooDynamic específicos de característica Aceleración de sitio y es necesaria para la creación de uno válido. DSA utiliza una pequeña *ruta de acceso de sondeo* archivo se coloca en hello origen toooptimize enrutamiento configuraciones de red para la red CDN Hola. Puede descargar y cargar nuestro sitio de tooyour del archivo de ejemplo o usar un recurso existente en el origen que es aproximadamente 10 KB para la ruta de acceso de sondeo de hello en su lugar, si existe el recurso de Hola.

> [!Note]
> DSA incurre en cargos adicionales. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/cdn/) para obtener más información.

Hola siguientes capturas de pantalla muestra proceso Hola a través del portal de Azure.
 
![Agregar un nuevo punto de conexión de red CDN](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Figura 1: Agregar un nuevo extremo CDN de perfil de CDN Hola*
 
![Creación de un nuevo punto de conexión de red CDN con DSA](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Figura 2: Creación de un punto de conexión de la red CDN con la opción de optimización de aceleración de sitios dinámicos seleccionada*

Una vez que se crea el extremo de red CDN Hola, aplica las optimizaciones de DSA Hola para todos los archivos que cumplan ciertos criterios. Hola pasos de la sección describe en detalle la optimización de DSA.

## <a name="dsa-optimization-using-azure-cdn"></a>Optimización de DSA con la red CDN de Azure

Aceleración de sitio dinámico en la red CDN de Azure acelera la entrega de recursos dinámicos mediante Hola siguiendo técnicas de:

-   Optimización de rutas
-   Optimizaciones de TCP
-   Captura previa de objetos (solo Akamai)
-   Compresión de imágenes de dispositivos móviles (solo Akamai)

### <a name="route-optimization"></a>Optimización de rutas

Optimización de rutas es importante porque Hola Internet es un lugar dinámico, donde el tráfico y temporalmente las interrupciones están cambiando constantemente topología de red de Hola. Hola protocolo de puerta de enlace de borde (BGP) es el protocolo de enrutamiento de hello del programa Hola a Internet, pero puede haber rutas más rápidas a través de intermediarios servidores de punto de presencia (PoP). 

Optimización de rutas elige origen de toohello de ruta de acceso más óptimo de Hola para que un sitio está continuamente contenido accesible y dinámico se entrega tooend a los usuarios a través de hello más rápido y más confiable ruta posible. 

red de Akamai Hello usa datos en tiempo real de técnicas toocollect y comparar varias rutas de acceso a través de varios nodos en hello Akamai servidor, así como ruta BGP de hello predeterminada por Hola abra Internet toodetermine hello más rápido ruta entre el origen de Hola y Hola Borde de la red CDN. Estas técnicas evitan los puntos de congestión en Internet y las rutas largas. 

De forma similar, usos de red Verizon Hola una combinación de Anycast DNS, gran capacidad admitir POP y comprobaciones de mantenimiento, toodetermine Hola mejor las puertas de enlace toobest ruta de datos de Hola origen toohello de cliente.
 
Como resultado, se entrega el contenido totalmente dinámico y transaccional más rápida y más confiable tooend usuarios, aunque sea almacenable. 

### <a name="tcp-optimizations"></a>Optimizaciones de TCP

Protocolo de Control de transmisión (TCP) es estándar de hello del conjunto de protocolos de Internet de hello usa toodeliver información entre aplicaciones en una red IP.  De forma predeterminada, hay varias atrás y hacia delante solicitudes necesario tooset una conexión TCP, así como congestions de red tooavoid límites, lo que traducir en ineficacias a escala. La red CDN de Azure de Akamai soluciona este problema mediante la optimización en tres áreas: 

 - eliminación del inicio lento
 - aprovechamiento de las conexiones persistentes
 - ajuste de los parámetros de paquete TCP (solo Akamai)

#### <a name="eliminating-slow-start"></a>Eliminación del inicio lento

*Ralentizar el inicio* forma parte del protocolo TCP de Hola que evita la congestión de la red limitando Hola cantidad de datos enviados a través de la red de Hola. Comienza con tamaños de ventana pequeña de congestión entre el remitente y receptor hasta que se alcanza el máximo de Hola o se detecta la pérdida de paquetes.

La red CDN de Azure de Akamai y Verizon elimina el inicio lento en tres pasos:

1.  Red de Akamai y de Verizon utilizar mantenimiento y supervisión de ancho de banda de toomeasure Hola de las conexiones entre los servidores de PoP de borde de ancho de banda.
2. las métricas de Hola se comparten entre los servidores de borde PoP para que cada servidor sea consciente de las condiciones de red de Hola y estado del servidor de Hola otros POP alrededor de ellos.  
3. servidores de borde CDN Hola ahora son toomake capaz de suposiciones sobre algunos parámetros de transmisión, como el tamaño de ventana óptimo Hola debe ser al comunicarse con otros servidores de borde de la red CDN en su proximidad. Este paso significa que el tamaño de ventana de congestión inicial Hola puede aumentarse si Hola el estado de conexión de hello entre servidores de borde CDN Hola es capaz de transferencias de datos de paquete mayor.  

#### <a name="leveraging-persistent-connections"></a>Aprovechamiento de las conexiones persistentes

Con una CDN, menos equipos únicos conectan directamente en comparación con los usuarios se conectan directamente tooyour origen tooyour del servidor de origen. Azure CDN de Akamai y Verizon también incluye el grupo tooestablish juntas de las solicitudes de usuario menos conexiones con el origen de Hola.

Como se mencionó anteriormente, las conexiones TCP toman varias solicitudes y hacia atrás en un tooestablish una nueva conexión de protocolo de enlace. Las conexiones persistentes, también conocido como "HTTP Keep-Alive," reutilizan las conexiones TCP existentes para varias veces ida y vuelta de HTTP solicitudes toosave y aceleran la entrega. 

red Verizon de Hello también envía paquetes keep-alive periódicos sobre Hola TCP conexión tooprevent una conexión abierta se cierren.

#### <a name="tuning-tcp-packet-parameters"></a>Ajuste de los parámetros de paquete TCP

Azure CDN de Akamai también optimiza los parámetros de Hola que rigen las conexiones de servidor a servidor y reduce Hola de largo alcance de ida y vuelta viajes requeridos tooretrieve contenido incrustada en el sitio de hello mediante Hola siguientes técnicas:

1.  Aumentar la ventana de congestión inicial de hello de modo que más paquetes se pueden enviar sin esperar una confirmación.
2.  Reducir el tiempo de espera de retransmisión inicial de Hola para que se detecta una pérdida y retransmisión se produce con más rapidez.
3.  Decreciente mínimo de Hola y máximo retransmiten el tiempo de espera de tiempo de espera tooreduce Hola antes de asumir que los paquetes se pierdan durante la transmisión.

### <a name="object-prefetch-akamai-only"></a>Captura previa de objetos (solo Akamai)

La mayoría de los sitios web tienen una página HTML que hace referencia a otros recursos como imágenes y scripts. Normalmente, cuando un cliente solicita una página Web, Explorador de hello primero descarga analiza Hola HTML objeto y, a continuación, hace que las solicitudes adicionales toolinked activos que son necesario toofully cargar la página de Hola. 

*Precarga de* es una técnica tooretrieve imágenes y scripts incrustan en hello página HTML mientras hello HTML ofrece toohello explorador, y antes de hello explorador incluso realiza estas solicitudes de objeto. 

Con hello **precargar** opción activada en tiempo de hello cuando Hola CDN ofrece explorador del cliente de hello HTML página base toohello, Hola CDN analiza el archivo hello HTML y realizar las solicitudes adicionales para todos los recursos vinculados y almacenarla en la memoria caché. Cuando hello cliente realiza solicitudes de Hola de activos de hello vinculado, servidor de borde CDN Hola ya ha Hola objetos solicitados y sirva inmediatamente sin un origen de toohello de ida y vuelta. Esta optimización beneficiará tanto al contenido que se puede almacenar en caché como al que no se puede almacenar en caché.

### <a name="adaptive-image-compression-akamai-only"></a>Compresión de imagen adaptable (solo Akamai)

Algunos dispositivos, especialmente los dispositivos móviles, experimentan de velocidades de red más lentas de tootime de tiempo. En estos casos, resulta más conveniente para imágenes más pequeñas tooreceive de hello usuario en su página Web más rápidamente, en lugar de esperar mucho tiempo para las imágenes de resolución completa.

Esta característica automáticamente supervisa la calidad de la red y utiliza los métodos estándar de compresión JPEG velocidades de red una vez tooimprove ralentiza el tiempo de entrega.

Compresión adaptable de imágenes | Extensiones de archivo  
--- | ---  
Compresión JPEG | .jpg, .jpeg, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Almacenamiento en caché

Con DSA, almacenamiento en caché está desactivada de forma predeterminada en hello CDN, incluso cuando el origen de Hola incluye encabezados/expira de control de caché en la respuesta de Hola. Este valor predeterminado se ha desactivado porque DSA normalmente se utiliza para activos dinámicos que no se deben guardar ya que son únicos tooeach cliente y activar el almacenamiento en caché de forma predeterminada puede anular este comportamiento.

Si tiene un sitio Web con una combinación de recursos estáticos y dinámicos, es mejor tootake un híbrido enfoque tooget Hola obtener el mejor rendimiento. 

Si usas ADN con Verizon Premium, puede activar el almacenamiento en caché para casos específicos con hello motor de reglas.  

Una alternativa es toouse dos extremos de red CDN. Uno con activos DSA toodeliver dinámicos y otro punto de conexión con una optimización estática tipo, como general entrega web, toodelivery almacenable en caché activos. En orden tooaccomplish este alternativo, modificará el toolink de las direcciones URL de la página Web directamente toohello asset en Hola piensa toouse de punto de conexión de red CDN. 

Por ejemplo: `mydynamic.azureedge.net/index.html` es una página dinámica y se carga desde el punto de conexión de hello DSA.  Hello página html hace referencia a varios recursos estáticos, como las bibliotecas de JavaScript o imágenes que se cargan desde Hola extremo CDN estático, como `mystatic.azureedge.net/banner.jpg` y `mystatic.azureedge.net/scripts.js`. 

Puede encontrar un ejemplo [aquí](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) en cómo toouse controladores en ASP.NET web tooserve del contenido de la aplicación a través de una URL específica de la red CDN.




