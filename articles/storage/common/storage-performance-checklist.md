---
title: checklist de rendimiento y escalabilidad de almacenamiento de aaaAzure | Documentos de Microsoft
description: "Lista de comprobación de prácticas probadas para su uso con Azure Storage para desarrollar aplicaciones de alto rendimiento."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage
## <a name="overview"></a>Información general
Desde la versión de Hola de servicios de almacenamiento de Microsoft Azure hello, Microsoft ha desarrollado una serie de prácticas demostradas para usar estos servicios de una manera eficiente y este artículo sirve de hello tooconsolidate más importantes de ellas en una lista de estilo de la lista de comprobación. intención de Hola de este artículo es que los desarrolladores de aplicaciones de toohelp comprobar usaran prácticas demostradas con almacenamiento de Azure y toohelp ellos identifican otras prácticas demostradas que deben considerar la adopción. En este artículo no intenta toocover cada posible optimización de rendimiento y escalabilidad: las que son pequeños en su impacto o no se aplica ampliamente excluye. extensión de toohello que Hola el comportamiento de la aplicación se puede predecir durante el diseño, resulta útil tookeep en cuenta desde el principio tooavoid diseños que se ejecutarán en los problemas de rendimiento.  

Cada desarrollador de aplicaciones con almacenamiento de Azure debe tomar Hola tiempo tooread este artículo y compruebe que su aplicación sigue cada uno de hello demostrado los procedimientos que se enumeran a continuación.  

## <a name="checklist"></a>Lista de comprobación
En este artículo organiza prácticas Hola demostrado en hello los grupos siguientes. Prácticas probadas aplicables a:  

* Todos los servicios de Azure Storage (Blob, Table, Queue y Files)
* Blobs
* Tablas
* Colas  

| ¡Listo! | Ámbito | Categoría | Pregunta |
| --- | --- | --- | --- |
| &nbsp; | Todos los servicios |Objetivos de escalabilidad |[¿Está alcanzando su aplicación diseñada tooavoid objetivos de escalabilidad de hello?](#subheading1) |
| &nbsp; | Todos los servicios |Objetivos de escalabilidad |[¿Es la nomenclatura tooenable convención diseñada mejor equilibrio de carga?](#subheading47) |
| &nbsp; | Todos los servicios |Redes |[¿Los dispositivos de cliente tienen suficientemente alto ancho de banda y el rendimiento de hello tooachieve de baja latencia necesarios?](#subheading2) |
| &nbsp; | Todos los servicios |Redes |[¿Tienen los dispositivos del lado cliente un enlace con una calidad suficientemente alta?](#subheading3) |
| &nbsp; | Todos los servicios |Redes |[¿Aplicación de cliente de hello cerca "" cuenta de almacenamiento de hello?](#subheading4) |
| &nbsp; | Todos los servicios |Distribución de contenido |[¿Usa una red CDN para distribución de contenido?](#subheading5) |
| &nbsp; | Todos los servicios |Acceso directo del cliente |[¿Está usando SAS y CORS toostorage de acceso directo de tooallow en lugar de proxy?](#subheading6) |
| &nbsp; | Todos los servicios |Almacenamiento en caché |[¿Su aplicación almacena datos en caché que se usan repetidamente y rara vez cambian?](#subheading7) |
| &nbsp; | Todos los servicios |Almacenamiento en caché |[¿Su aplicación procesa por lotes las actualizaciones (almacenándolas en caché en el cliente y, a continuación, cargándolas en conjuntos más grandes)?](#subheading8) |
| &nbsp; | Todos los servicios |Configuración .NET |[¿Ha configurado su toouse un número suficiente de conexiones simultáneas de cliente?](#subheading9) |
| &nbsp; | Todos los servicios |Configuración .NET |[¿Si configuró .NET toouse un número suficiente de subprocesos?](#subheading10) |
| &nbsp; | Todos los servicios |Configuración .NET |[¿Usa .NET 4.5 o posterior, que ha mejorado la recolección de elementos no usados?](#subheading11) |
| &nbsp; | Todos los servicios |Paralelismo |[¿Se ha asegurado de que está limitado el paralelismo correctamente para que no se puede sobrecargar que las capacidades de cliente o de los objetivos de escalabilidad de Hola?](#subheading12) |
| &nbsp; | Todos los servicios |Herramientas |[¿Se está utilizando la versión más reciente de Hola de Microsoft proporcionan herramientas y bibliotecas de cliente?](#subheading13) |
| &nbsp; | Todos los servicios |Reintentos |[¿Usa una directiva de reintentos de retroceso exponencial para errores de limitación y tiempos de espera?](#subheading14) |
| &nbsp; | Todos los servicios |Reintentos |[¿Evita su aplicación reintentos para errores que no se pueden reintentar?](#subheading15) |
| &nbsp; | Blobs |Objetivos de escalabilidad |[¿Tiene un gran número de clientes que acceden simultáneamente a un único objeto?](#subheading46) |
| &nbsp; | Blobs |Objetivos de escalabilidad |[¿Se desvía la aplicación de destino de escalabilidad de hello operaciones o ancho de banda para un único blob?](#subheading16) |
| &nbsp; | Blobs |Copia de blobs |[¿Copia blobs de una manera eficiente?](#subheading17) |
| &nbsp; | Blobs |Copia de blobs |[¿Usa AzCopy para copias de blobs en masa?](#subheading18) |
| &nbsp; | Blobs |Copia de blobs |[¿Está usando la importación y exportación de Azure tootransfer muy grandes volúmenes de datos?](#subheading19) |
| &nbsp; | Blobs |Usar metadatos |[¿Almacena metadatos usados frecuentemente acerca de blobs en los metadatos de estos?](#subheading20) |
| &nbsp; | Blobs |Carga rápida |[¿Al tratar de un blob de tooupload rápidamente, se carga de bloques en paralelo?](#subheading21) |
| &nbsp; | Blobs |Carga rápida |[¿Al tratar de tooupload muchos blobs rápidamente, se cargar blobs en paralelo?](#subheading22) |
| &nbsp; | Blobs |Tipo de blob correcto |[¿Usa blobs en páginas o blobs en bloques cuando es apropiado?](#subheading23) |
| &nbsp; | Tablas |Objetivos de escalabilidad |[¿Son también con hello objetivos de escalabilidad para entidades por segundo?](#subheading24) |
| &nbsp; | Tablas |Configuración |[¿Usa JSON para sus solicitudes de tabla?](#subheading25) |
| &nbsp; | Tablas |Configuración |[¿Se ha desactivado Nagle rendimiento de hello tooimprove de las solicitudes de pequeñas?](#subheading26) |
| &nbsp; | Tablas |Tablas y particiones |[¿Ha particionado sus datos correctamente?](#subheading27) |
| &nbsp; | Tablas |Particiones calientes |[¿Evita los patrones Solo anexar y Solo anteponer?](#subheading28) |
| &nbsp; | Tablas |Particiones calientes |[¿Se despliegan sus inserciones y actualizaciones por muchas particiones?](#subheading29) |
| &nbsp; | Tablas |Ámbito de las consultas |[¿Se ha diseñado su tooallow de esquema para el punto de consultas toobe utilizado en la mayoría de los casos y tabla consultas toobe utilizar demasiado a menudo?](#subheading30) |
| &nbsp; | Tablas |Densidad de las consultas |[¿Normalmente sus consultas solamente examinan y devuelven filas que usará su aplicación?](#subheading31) |
| &nbsp; | Tablas |Limitación de datos devueltos |[¿Está usando filtrado tooavoid devolver las entidades que no son necesarios?](#subheading32) |
| &nbsp; | Tablas |Limitación de datos devueltos |[¿Está usando tooavoid proyección devuelven propiedades que no son necesarios?](#subheading33) |
| &nbsp; | Tablas |Desnormalización |[¿Ha desnormalizado los datos de forma que evitar consultas ineficaces o varias solicitudes de lectura al intentar tooget datos?](#subheading34) |
| &nbsp; | Tablas |Inserción, actualización y eliminación |[¿Son por lotes las solicitudes que necesitan toobe transaccional o pueden realizarse en hello mismo tiempo de ida y vuelta de tooreduce?](#subheading35) |
| &nbsp; | Tablas |Inserción, actualización y eliminación |[¿Se evita recuperar un toodetermine simplemente entidad si toocall insertar o actualizar?](#subheading36) |
| &nbsp; | Tablas |Inserción, actualización y eliminación |[¿Ha pensado en almacenar series de datos que se recuperarán frecuentemente de forma conjunta en una sola entidad como propiedades en lugar de varias entidades?](#subheading37) |
| &nbsp; | Tablas |Inserción, actualización y eliminación |[Para entidades que siempre se recuperarán conjuntamente y que se pueden escribir en lotes (por ejemplo, datos de serie de temporales), ¿ha pensado en usar blobs en lugar de tablas?](#subheading38) |
| &nbsp; | Colas |Objetivos de escalabilidad |[¿Son también con hello objetivos de escalabilidad para mensajes por segundo?](#subheading39) |
| &nbsp; | Colas |Configuración |[¿Se ha desactivado Nagle rendimiento de hello tooimprove de las solicitudes de pequeñas?](#subheading40) |
| &nbsp; | Colas |Tamaño de los mensajes |[¿Son los mensajes de rendimiento de hello tooimprove compact de cola de Hola?](#subheading41) |
| &nbsp; | Colas |Recuperación en masa |[¿Recupera varios mensajes en una sola operación "Get"?](#subheading42) |
| &nbsp; | Colas |Frecuencia de sondeo |[¿Se sondean con frecuencia suficiente Hola de tooreduce percibida latencia de la aplicación?](#subheading43) |
| &nbsp; | Colas |Actualizar mensaje |[¿Está usando UpdateMessage toostore progreso de procesamiento de mensajes, evitar tener todo mensaje de bienvenida de tooreprocess si se produce un error?](#subheading44) |
| &nbsp; | Colas |Arquitectura |[¿Está usando colas toomake toda la aplicación más escalable manteniendo las cargas de trabajo de larga ejecución fuera de la ruta crítica de Hola y escala, a continuación, por separado?](#subheading45) |

## <a name="allservices"></a>Todos los servicios
Esta sección enumeran las prácticas demostradas que usan toohello aplicables de cualquiera de los servicios de almacenamiento de Azure de hello (blobs, tablas, colas o archivos).  

### <a name="subheading1"></a>Objetivos de escalabilidad
Cada uno de los servicios de almacenamiento de Azure de hello tiene objetivos de escalabilidad de capacidad (GB), la velocidad de transacción y el ancho de banda. Si la aplicación se aproxima o supera alguno de los objetivos de escalabilidad de hello, puede encontrar las latencias de transacción mayor o limitación. Cuando un servicio de almacenamiento limita la aplicación, servicio de hello comienza tooreturn "503 servidor ocupado" o "tiempo de espera de operación 500" códigos de error para algunas transacciones de almacenamiento. Esta sección describen ambos toodealing de enfoque general Hola con objetivos de escalabilidad y objetivos de escalabilidad de ancho de banda en particular. En secciones posteriores que se encargan de servicios de almacenamiento individuales se tratan los objetivos de escalabilidad en el contexto de Hola de ese servicio en concreto:  

* [Ancho de banda de blob y solicitudes por segundo](#subheading16)
* [Entidades de tabla por segundo](#subheading24)
* [Mensajes de cola por segundo](#subheading39)  

#### <a name="sub1bandwidth"></a>Objetivo de escalabilidad de ancho de banda para todos los servicios
En tiempo de Hola de escritura, destinos de ancho de banda de hello en la cuenta de hello US para un almacenamiento con redundancia geográfica (GRS) son 10 gigabits por segundo (Gbps) para la entrada (datos envían toohello cuenta de almacenamiento) y 20 GB/s para la salida (los datos enviados desde la cuenta de almacenamiento de hello). Para una cuenta de almacenamiento con redundancia local (LRS), los límites de hello son superiores: 20 GB/s de entrada y de 30 GB/s para la salida.  Los límites de ancho de banda internacionales pueden ser menores y puede encontrarlos en nuestra [página de objetivos de escalabilidad](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Para obtener más información sobre las opciones de redundancia de almacenamiento de hello, vea los vínculos de hello en [recursos útiles](#sub1useful) a continuación.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>¿Qué toodo cuando planee un objetivo de escalabilidad
Si la aplicación se está aproximando a los objetivos de escalabilidad de Hola para una única cuenta de almacenamiento, considere la posibilidad de adoptar uno de los siguientes enfoques de hello:  

* Mayor carga de trabajo de Hola que hace que su aplicación tooapproach o superar el objetivo de escalabilidad de Hola. ¿Puede diseñarlo diferente toouse menos ancho de banda o capacidad o menos transacciones?
* Si una aplicación debe superar uno de los objetivos de escalabilidad de hello, debe crear varias cuentas de almacenamiento y partición de datos de su aplicación en esos varias cuentas de almacenamiento. Si utiliza este patrón, a continuación, ser toodesign seguro de la aplicación para que pueda agregar más cuentas de almacenamiento en hello futura para el equilibrio de carga. En el momento de escribir este artículo, cada suscripción de Azure puede tener hasta too100 cuentas de almacenamiento.  Las cuentas de almacenamiento tampoco tienen ningún costo que no sea el de su uso en términos de datos almacenados, transacciones realizadas o datos transferidos.
* Si la aplicación llega a destinos de ancho de banda de hello, considere la posibilidad de comprimir los datos en hello cliente tooreduce Hola ancho de banda necesario toosend Hola datos toohello servicio de almacenamiento.  Tenga en cuenta que aunque esto puede ahorrar ancho de banda y mejorar el rendimiento de la red, también puede tener algunos impactos negativos.  Se debe evaluar el impacto de rendimiento de Hola de esto debido a los requisitos de procesamiento adicionales de toohello para comprimir y descomprimir los datos de cliente de Hola. Además, almacenar los datos comprimidos puede ser más difíciles problemas tootroubleshoot ya que podría ser más difíciles datos tooview almacenado mediante herramientas estándar.
* Si la aplicación alcanza los objetivos de escalabilidad de hello, a continuación, asegúrese de que está usando un retroceso exponencial para reintentos (vea [reintentos](#subheading14)).  Simplemente mantener no volver a intentar rápidamente, realizar Hola limitación empeoran su mejor toomake seguro nunca enfocar objetivos de escalabilidad de hello (mediante uno de hello métodos anteriores), pero esto garantizará que la aplicación.  

#### <a name="useful-resources"></a>Recursos útiles
Hola siguientes vínculos proporciona detalles adicionales sobre objetivos de escalabilidad:

* Consulte [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md) para obtener información sobre los objetivos de escalabilidad.
* Vea [replicación de almacenamiento de Azure](storage-redundancy.md) y entrada de blog de hello [opciones de redundancia de almacenamiento de Azure y almacenamiento con redundancia geográfica acceso de lectura](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) para obtener información acerca de las opciones de redundancia de almacenamiento.
* Para obtener información actual sobre los precios de los servicios de Azure, consulte [Precios de Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Convención de nomenclatura de particiones
Almacenamiento de Azure usa un basada en intervalo partición esquema tooscale y carga saldo Hola sistema. clave de partición de Hello es toopartition usa datos en intervalos y estos intervalos son con equilibrio de carga en todo sistema Hola. Esto significa que las convenciones de nomenclatura como léxico de ordenación (por ejemplo, msftpayroll, msftperformance, msftemployees, etcetera) o con marcas de tiempo (log20160101, log20160102, log20160102, etcetera) prestan particiones toohello potencialmente que se va a colocar en hello servidor de particiones mismo, hasta que una operación de equilibrio de carga divide Consúltelas en intervalos más pequeños. Por ejemplo, todos los blobs dentro de un contenedor se pueden atender un único servidor hasta que hello carga en estos blobs requiere aún más el equilibrio de intervalos de partición de Hola. De forma similar, un grupo de cuentas con carga ligera con sus nombres organizados en orden léxico puede procesarse mediante un servidor único hasta Hola cargar en una o todas estas cuentas necesiten toobe dividido entre varios servidores de particiones. Cada operación de equilibrio de carga puede afecta a la latencia de Hola de llamadas de almacenamiento durante la operación de Hola. toohandle de capacidad del sistema de Hello que una ráfaga repentina de partición de tooa de tráfico está limitada por la escalabilidad de Hola de un solo servidor de particiones hasta que la operación de equilibrio de carga de hello en aparece y vuelve a equilibrar intervalo de claves de partición de Hola.  

Puede seguir algunas frecuencia de Hola tooreduce de prácticas recomendada de tales operaciones.  

* Examine la convención de nomenclatura de hello que utilizas para cuentas, contenedores, blobs, tablas y colas, estrechamente. Considere la posibilidad de prefijar nombres de cuenta con un hash de 3 dígitos con la función hash que mejor se adapte a sus necesidades.  
* Si organiza los datos mediante las marcas de tiempo o identificadores numéricos, tener tooensure no usa un patrones de tráfico solo de adición (o solo anteposición). Estos patrones no son adecuados para un intervalo de-según el sistema de creación de particiones, y podrían responsable tooall Hola tráfico continuo tooa única partición y restricción sistema Hola desde eficazmente equilibrio de carga. Por ejemplo, si tienes diariamente las operaciones que utilizan un objeto blob con una marca de tiempo como AAAAMMDD, a continuación, todo Hola el tráfico para que sea el funcionamiento diario dirigen tooa único objeto que es atendido por un servidor de una sola partición. Examine si limita Hola por blob y por partición límites de sus necesidades y considere la posibilidad de dividir esta operación en varios blobs si es necesario. De forma similar, si almacena datos de series temporales de las tablas, todo el tráfico de hello podría ser dirigido toohello última parte del espacio de nombres de clave de Hola. Si debe utilizar las marcas de tiempo o identificadores numéricos, un prefijo de Id. de hello con un hash de 3 dígitos, o en caso de hello de parte de las marcas de tiempo prefijo Hola segundos de tiempo de hello como ssyyyymmdd. Si se realizan operaciones de enumeración y consulta de manera habitual, elija una función hash que limite su número de consultas. En otros casos, un prefijo aleatorio puede ser suficiente.  
* Para obtener información adicional sobre Hola utilizado en el almacenamiento de Azure de esquema de partición, lea el documento SOSP del hello [aquí](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Redes
Si bien Hola API llama materia, las restricciones red física a menudo de Hola de aplicación hello tienen un impacto significativo en rendimiento. Hola continuación indican algunas de las limitaciones que los usuarios pueden encontrar.  

#### <a name="client-network-capability"></a>Capacidad de red del cliente
##### <a name="subheading2"></a>Capacidad de proceso
Por ancho de banda, problema de hello suele ser capacidades de hello del cliente de Hola. Por ejemplo, mientras que una cuenta de almacenamiento solo puede controlar 10 Gbps o más de entrada (vea [objetivos de escalabilidad de ancho de banda](#sub1bandwidth)), velocidad de red de hello en una instancia de rol de trabajador de Azure "Pequeño" sólo es capaz de aproximadamente 100 Mbps. Las instancias de Azure mayores tienen NIC con mayor capacidad, por lo que debe plantearse la posibilidad de usar una instancia mayor o más máquinas virtuales si necesita aumentar los límites de red de una sola máquina. Si obtiene acceso a un servicio de almacenamiento desde una aplicación local de, hello misma regla se aplica: comprender las capacidades de red de hello de dispositivo de cliente de Hola y toohello de conectividad de red de hello ubicación de almacenamiento de Azure y mejoran ellos según sea necesario o diseñar la toowork de aplicación dentro de sus capacidades.  

##### <a name="subheading3"></a>Calidad del enlace
Como con cualquier uso de red, sea consciente de que las condiciones de la red dan lugar a errores y la pérdida de paquetes reducirá el rendimiento efectivo.  El uso de WireShark o NetMon puede ayudar a diagnosticar este problema.  

##### <a name="useful-resources"></a>Recursos útiles
Para obtener información sobre los tamaños de máquina virtual y el ancho de banda asignado, consulte los artículos sobre [Tamaños de las máquinas virtuales Windows](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Tamaños de las máquinas virtuales Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Ubicación
En cualquier entorno distribuido, colocar cliente hello cerca toohello server ofrece mejor rendimiento de Hola. Para acceder al almacenamiento de Azure con latencia más baja de hello, mejor ubicación hello para el cliente está dentro Hola misma región de Azure. Por ejemplo, si tiene un sitio web Azure que usa Azure Storage, debe colocar ambos dentro de una sola región (por ejemplo Oeste de EE. UU. o Sudeste de Asia). Esto reduce la latencia de Hola y Hola de costo: en tiempo de Hola de escritura, uso de ancho de banda en una única región es gratuito.  

Si el cliente de aplicaciones no están hospedadas dentro de Azure (por ejemplo, aplicaciones para dispositivos móviles o en servicios de enterprise locales), a continuación, vuelva a colocar la cuenta de almacenamiento de hello en una región cerca de los dispositivos de toohello que tiene acceso a él, reducirá generalmente latencia. Si los clientes están muy distribuidos (por ejemplo algunos en Norteamérica y otros en Europa), debe plantearse el uso de varias cuentas de almacenamiento: una ubicada en una región de Norteamérica y otra en una región de Europa. Esto le ayudará a latencia tooreduce para los usuarios de ambas regiones. Este enfoque es tooimplement suele ser más fácil si Hola Hola aplicaciones y almacenes de datos está tooindividual específicos a los usuarios, no requiere la replicación de datos entre las cuentas de almacenamiento.  Amplia distribución de contenido, se recomienda una CDN: vea Hola próxima sección para obtener más detalles.  

### <a name="subheading5"></a>Distribución de contenido
En ocasiones, un Hola de tooserve de necesidades de aplicación mismo toomany contenido a los usuarios (por ejemplo, un producto de demostración de vídeo que se usa en la página principal de Hola de un sitio Web), ubicado en la vista Hola mismo o en varias regiones. En este escenario, debe usar una red de entrega de contenido (CDN) como la red CDN de Azure y red CDN Hola utilizaría el almacenamiento de Azure como origen de Hola de los datos de Hola. A diferencia de una cuenta de almacenamiento de Azure que se encuentran en una única región y que no puede entregar contenido con una latencia baja tooother regiones, CDN de Azure usa servidores en varios centros de datos alrededor de Hola a todos. Además, una red CDN normalmente puede admitir límites de salida mucho más altos que una sola cuenta de almacenamiento.  

Para obtener más información acerca de la red CDN de Azure, consulte [Red CDN de Azure](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Uso de SAS y CORS
Cuando se necesita código tooauthorize como JavaScript en el Explorador de web de un usuario o un datos de tooaccess de aplicación de teléfono móvil en almacenamiento de Azure, un enfoque es toouse una aplicación en el rol web como un proxy: dispositivo del usuario de Hola se autentica con el rol de web de hello, que a su vez se autentica con el servicio de almacenamiento de Hola. De esta forma, puede evitar la exposición de sus claves de cuenta de almacenamiento en dispositivos no seguros. Sin embargo, esto aumenta una gran sobrecarga en el rol web de hello porque todos los datos de hello transfieren entre el dispositivo del usuario de Hola y Hola servicio de almacenamiento debe atravesar rol web de Hola. Se puede evitar usando un rol web como un proxy para el servicio de almacenamiento de Hola mediante firmas de acceso compartido (SAS), a veces, junto con los encabezados de uso compartido de recursos entre orígenes (CORS). Usar SAS, puede permitir que toomake de dispositivo del usuario solicita directamente tooa almacenamiento de servicio por medio de un token de acceso limitado. Por ejemplo, si un usuario desea tooupload una aplicación de tooyour fotografías, su rol web puede generar y enviar un token SAS que concede blob en cuestión permiso toowrite tooa o un contenedor para hello siguientes 30 minutos (después del cual hello token SAS expira) de dispositivo del usuario toohello.

Normalmente, un explorador no permitirá JavaScript en una página hospedada en un sitio Web en un dominio tooperform las operaciones concretas, como un dominio de tooanother "PUT". Por ejemplo, si hospeda un rol web en "contosomarketing.cloudapp.net" y desea toouse cliente lado JavaScript tooupload una cuenta de almacenamiento de blobs tooyour en "contosoproducts.blob.core.windows.net", Hola del explorador "Directiva de mismo origen" prohíba esto operación. CORS es una característica del explorador que permite Hola destino (en esta cuenta de almacenamiento Hola mayúsculas) toocommunicate toohello Examinador de dominio que confía en las solicitudes que se originan en los dominios de origen de hello (de este rol web de hello mayúsculas).  

Estas dos tecnologías pueden ayudarle a evitar una carga innecesaria (y cuellos de botella) en la aplicación web.  

#### <a name="useful-resources"></a>Recursos útiles
Para obtener más información sobre SAS, consulte [firmas de acceso compartido, parte 1: Hola descripción modelo SAS](../storage-dotnet-shared-access-signature-part-1.md).  

Para obtener más información acerca de CORS, consulte [compatibilidad de uso compartido de recursos entre orígenes (CORS) para servicios de almacenamiento de Azure hello](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Almacenamiento en caché
#### <a name="subheading7"></a>Obtención de datos
En general, obtener datos de un servicio una vez es mejor que obtenerlos dos veces. Considere el ejemplo de Hola de una aplicación web MVC ejecutar en un rol web que ya se ha recuperado un blob de 50MB de hello tooserve de servicio de almacenamiento como usuario tooa contenido. aplicación Hello podría, a continuación, recupera ese mismo blob cada vez que un usuario lo solicita o puede almacenar en caché se localmente toodisk y volver a hello en caché versión para las solicitudes de usuario siguientes. Además, cada vez que un usuario solicita datos de hello, Hola aplicación podría emitir comandos GET con un encabezado condicional para tiempo de modificación, lo que podría evitar que aparezcan los blob completo Hola si no se haya modificado. Puede aplicar este mismo tooworking de patrón con entidades de tabla.  

En algunos casos, puede decidir que la aplicación puede asumir que ese blob Hola sigue siendo válido durante un breve período después de recuperar y durante este período Hola aplicación no es necesario que toocheck si se ha modificado el blob de Hola.

Configuración, búsqueda y otros datos que se usan siempre mediante la aplicación hello son buenos candidatos para el almacenamiento en caché.  

Para obtener un ejemplo de cómo tooget Hola de toodiscover de propiedades de un blob en fecha de última modificación con. NET, vea [conjunto y recuperar propiedades y metadatos](../blobs/storage-properties-metadata.md). Para obtener más información sobre las descargas condicionales, consulte [Actualización condicional de una copia local de un blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Carga de datos en lotes
En algunos escenarios de aplicación, puede agregar datos localmente y, a continuación, cargarlos periódicamente en un lote en lugar de cargar cada parte de datos inmediatamente. Por ejemplo, una aplicación web podría mantener un archivo de registro de actividades: Hola aplicación podría cualquiera cargar detalles de cada actividad, tal y como se produce como una entidad de tabla (que requiere muchas operaciones de almacenamiento), o puede guardar la actividad detalles tooa archivo de registro local y, a continuación, cargar periódicamente todos los detalles de actividad como un blob de tooa de archivo delimitado. Si cada entrada de registro es de 1KB de tamaño, puede cargar miles en una sola transacción "Put Blob" (se puede cargar un blob de seguridad too64MB de tamaño en una única transacción). Por supuesto, si máquina local Hola bloquea la carga toohello anterior, potencialmente perderá algunos datos de registro: desarrollador de la aplicación hello debe diseñar con posibilidad de hello de dispositivo de cliente o cargar errores.  Si los datos de actividad de hello necesitan toobe descargado para intervalos de tiempo (no una sola actividad), se recomiendan blobs sobre las tablas.

### <a name="net-configuration"></a>Configuración .NET
Si utiliza hello .NET Framework, esta sección enumeran varias opciones de configuración rápida que puede usar toomake importantes mejoras de rendimiento.  Si se utilizan otros idiomas, compruebe toosee si conceptos similares que se aplican en el lenguaje elegido.  

#### <a name="subheading9"></a>Aumento del límite de conexiones predeterminado
En. NET, Hola sigue código aumenta el límite de conexiones predeterminado de hello (que normalmente es 2 en un entorno de cliente o 10 en un entorno de servidor) too100. Por lo general, debe establecer el número de hello valor tooapproximately Hola de subprocesos usados por la aplicación.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Debe establecer el límite de conexiones de hello antes de abrir todas las conexiones.  

Para otros lenguajes de programación, vea toodetermine de documentación de ese lenguaje cómo limitar la conexión de hello tooset.  

Para obtener más información, consulte el blog de hello [servicios Web: conexiones simultáneas](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Aumento de los subprocesos mínimos ThreadPool si se usa código sincrónico con tareas asincrónicas
Este código aumentará Hola min subprocesos ThreadPool:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Para obtener más información, consulte [Método ThreadPool.SetMinThreads](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Aprovechamiento de la recolección de elementos no usados de .NET 4.5
Usar .NET 4.5 o posterior para hello cliente aplicación tootake aprovechar las mejoras de rendimiento en la recolección de elementos no utilizados de servidor.

Para obtener más información, vea el artículo de hello [una información general de mejoras en el rendimiento en .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Paralelismo no vinculado
Mientras paralelismo puede ser bueno para el rendimiento, tenga cuidado cuando use unbounded paralelismo (sin límite en el número de Hola de subprocesos o las solicitudes paralelas) tooupload o descarga datos mediante varios de los trabajadores tooaccess varias particiones (contenedores, las colas, o las particiones de tabla) en Hola misma cuenta de almacenamiento o tooaccess varios elementos en hello misma partición. Si el paralelismo hello es ilimitado, la aplicación puede superar las capacidades del dispositivo de cliente de Hola u Hola objetivos de escalabilidad de la cuenta de almacenamiento resultante en las latencias más y la limitación.  

### <a name="subheading13"></a>Herramientas y bibliotecas de cliente de Storage
Utilice siempre herramientas y bibliotecas de cliente de Microsoft proporciona más recientes de Hola. En tiempo de Hola de escritura, existen las bibliotecas de cliente disponibles para. NET, Windows Phone, Windows Runtime, Java y C++, así como bibliotecas de vista previa para otros idiomas. Además, Microsoft ha lanzado cmdlets de PowerShell y comandos de la CLI de Azure para trabajar con Azure Storage. Microsoft activamente desarrolla estas herramientas con el rendimiento en mente, mantiene una toodate con versiones más recientes de servicio de Hola y garantiza que controlan muchos de hello demostrado prácticas recomendadas de rendimiento internamente.  

### <a name="retries"></a>Reintentos
#### <a name="subheading14"></a>Limitación y servidor ocupado
En algunos casos, Hola servicio de almacenamiento puede limitar la aplicación o puede simplemente sea solicitud de hello tooserve no se puede pagar condición transitoria toosome y devolver un mensaje de "503 servidor ocupado" o "tiempo de espera de 500".  Esto puede ocurrir si la aplicación se está aproximando a cualquiera de los objetivos de escalabilidad de Hola o si el sistema de hello es reequilibrio su tooallow datos particionados para un mayor rendimiento.  aplicación de cliente de Hello normalmente debería intentar realizar la operación de Hola que hace que este tipo de error: intentar Hola mismo solicitar más adelante se realice correctamente. Sin embargo, si el servicio de almacenamiento de hello está limitando la aplicación porque supera los objetivos de escalabilidad, o incluso si el servicio de hello tooserve no se puede Hola solicitud por algún otro motivo, reintentos normalmente empeorar Hola problema. Por este motivo, debe usar un valor exponencial de interrupción (Hola bibliotecas predeterminado toothis comportamiento del cliente). Por ejemplo, su aplicación puede llevar a cabo los reintentos después de 2 segundos, luego 4 segundos, después 10 segundos, luego 30 segundos y, después, renunciar. Este comportamiento se produce en la aplicación, lo que reduce la carga de servicio de hello significativamente en lugar de que agrava los problemas.  

Tenga en cuenta que los errores de conectividad se pueden recuperar inmediatamente, porque no son resultado de hello de limitación y están esperado toobe transitorio.  

#### <a name="subheading15"></a>Errores que no se pueden reintentar
bibliotecas de cliente de Hello son conscientes de los errores son reintentable y cuáles no. Sin embargo, si está escribiendo su propio código en el almacenamiento de hello API de REST, recuerde que hay algunos errores que no debería intentar: por ejemplo, un error 400 (solicitud incorrecta) respuesta indica que aplicación de cliente hello envía una solicitud que no se pudieron procesar porque se no estaba en un formulario que se espera. Volver a enviar esta solicitud dará como resultado Hola misma respuesta cada vez, por lo que no hay ningún punto de volver a intentarlo. Si está escribiendo su propio código en el almacenamiento de hello API de REST, tener en cuenta qué tipo de error Hola códigos hello y Media tooretry de manera adecuada (o no) para cada uno de ellos.  

#### <a name="useful-resources"></a>Recursos útiles
Para obtener más información acerca de los códigos de error de almacenamiento, consulte [estado y códigos de Error](http://msdn.microsoft.com/library/azure/dd179382.aspx) en el sitio web de Microsoft Azure de Hola.  

## <a name="blobs"></a>Blobs
En toohello adición prácticas para comprobadas [todos los servicios](#allservices) se ha descrito anteriormente, siguiente de hello prácticas comprobadas aplica específicamente toohello de servicio.  

### <a name="blob-specific-scalability-targets"></a>Objetivos de escalabilidad específicos de blob
#### <a name="subheading46"></a>Acceso simultáneo a un único objeto por parte de varios clientes
Si tiene un gran número de clientes que tienen acceso simultáneamente a un único objeto deberá tooconsider por objetivos de escalabilidad de cuenta de almacenamiento y el objeto. número exacto de Hola de clientes que puede tener acceso a un objeto único se varían en función de factores como el número de clientes que solicitan objetos de hello simultáneamente, tamaño de hello del objeto de Hola Hola, etcetera de las condiciones de red.

Si el objeto de hello puede distribuirse a través de una CDN como imágenes o vídeos provienen de un sitio Web, a continuación, debe usar una CDN. Consulte [aquí](#subheading5).

En otros escenarios como simulaciones científicos donde están confidenciales datos hello tiene dos opciones. Hola en primer lugar es toostagger se tiene acceso a acceso la carga de trabajo, que Hola objeto durante un período de vs de tiempo que se obtiene acceso al mismo tiempo. Como alternativa, puede copiar temporalmente Hola objeto toomultiple las cuentas de almacenamiento y así aumente Hola IOPS total por objeto y a través de las cuentas de almacenamiento. En algunas pruebas descubrimos que aproximadamente 25 máquinas virtuales al mismo tiempo pueden descargar un blob de 100GB en paralelo (cada máquina virtual paralelizar descarga Hola con 32 subprocesos). Si tuviera 100 clientes necesidad de objeto de hello tooaccess, primero cópielo tooa una segunda cuenta de almacenamiento y, a continuación, ha Hola primeros 50 máquinas virtuales acceso Hola primer blob y Hola en segundo lugar 50 blob segunda de las máquinas virtuales acceso Hola. Los resultados varían según el comportamiento de las aplicaciones, por lo que debe realizar las pruebas durante el diseño. 

#### <a name="subheading16"></a>Ancho de banda y operaciones por blob
Puede leer o escribir tooa solo blob en una tooa máximo de 60 MB/segundo (Esto es aproximadamente 480 Mbps que excede las capacidades de Hola de muchas redes de lado cliente (incluidos Hola NIC física en el dispositivo de cliente hello). Además, se admite un único blob too500 solicitudes por segundo. Si tiene varios clientes que necesitan tooread hello mismo blob y puede superar estos límites, debe considerar el uso de una CDN para distribuir el blob de Hola.  

Para obtener más información sobre el rendimiento objetivo para blobs, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Copia y movimiento de blobs
#### <a name="subheading17"></a>Copia de blobs
almacenamiento Hola API de REST versión 2012-02-12 introdujo blobs de hello capacidad útil toocopy entre cuentas: una aplicación cliente puede indicar a toocopy de servicio de almacenamiento de hello un blob desde otro origen (posiblemente en una cuenta de almacenamiento diferente) y, a continuación, dejar que Hola servicio realizar copia de Hola de forma asincrónica. Esto puede reducir significativamente el ancho de banda de hello necesario para la aplicación hello cuando va a migrar datos desde otras cuentas de almacenamiento porque no necesita toodownload y cargar datos de Hola.  

Una consideración, sin embargo, es que, al copiar datos entre las cuentas de almacenamiento, no hay ninguna garantía de vez en cuando se completará copia Hola. Si la aplicación necesita toocomplete un blob copiar rápidamente bajo su control, puede ser mejor blob de hello toocopy, descargar tooa máquina virtual y, a continuación, se carga toohello destino.  Para poder predecir completa en esa situación, asegúrese de que se realiza la copia de Hola por una máquina virtual que se ejecuta en hello misma región de Azure, o bien las condiciones de red pueden (y probablemente hará) afectan a su rendimiento de la copia.  Además, se puede supervisar el progreso de Hola de una copia asincrónica mediante programación.  

Tenga en cuenta que copia dentro de la misma cuenta de almacenamiento propio generalmente se completan rápidamente de Hola.  

Para obtener más información, consulte [Copia de blobs](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Uso de AzCopy
equipo de almacenamiento de Azure de Hello ha lanzado una herramienta de línea de comandos "AzCopy" que es están hecho toohelp con bulk transferir muchos blobs para, de y a través de las cuentas de almacenamiento.  Esta herramienta está optimizada para este escenario y puede lograr altas tasas de transferencia.  Su uso es muy recomendable para escenarios de carga, descarga y copia en masa. toolearn más sobre él y descargarlo, vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Servicio de importación y exportación de Azure
Para volúmenes muy grandes de datos (más de 1TB), Hola almacenamiento de Azure ofrece Hola servicio de importación y exportación, que permite la carga y descarga de almacenamiento de blobs mediante el envío de unidades de disco duro.  Puede colocar datos en una unidad de disco duro y enviarlo tooMicrosoft para la carga o enviar una unidad de disco duro en blanco tooMicrosoft toodownload de datos.  Para obtener más información, consulte [usar Hola servicio de importación y exportación de Microsoft Azure tooTransfer datos tooBlob almacenamiento](../storage-import-export-service.md).  Esto puede ser mucho más eficaz que carga/descarga de este volumen de datos a través de red de Hola.  

### <a name="subheading20"></a>Uso de metadatos
servicio de blob de Hello es compatible con las solicitudes head, que pueden incluir metadatos acerca de blob de Hola. Por ejemplo, si la aplicación necesita Hola EXIF de datos fuera de una foto, podría recuperar fotográfica hello y extráigalo. ancho de banda toosave y mejorar el rendimiento, la aplicación puede almacenar datos EXIF de hello en metadatos del blob de hello cuando aplicación hello carga foto hello: a continuación, puede recuperar datos EXIF de hello en los metadatos mediante sólo una solicitud HEAD, ahorra ancho de banda significativo y en tiempo de procesamiento de hello necesarios tooextract Hola datos EXIF se lee cada blob de Hola de tiempo. Esto resultaría útil en escenarios donde solo necesita metadatos hello y no Hola todo el contenido de un blob.  Tenga en cuenta que solo 8 KB de metadatos se pueden almacenar por blob (servicio de hello no aceptará una solicitud toostore mayor que), por lo que si los datos de hello no caben en ese tamaño, no puede ser capaz de toouse este enfoque.  

Para obtener un ejemplo de cómo tooget los metadatos de un blob con. NET, vea [conjunto y recuperar propiedades y metadatos](../blobs/storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Carga rápida
tooupload de objetos BLOB rápido, tooanswer de hello primera pregunta es: ¿está cargando un blob o muchas?  Usar hello debajo de orientación toodetermine Hola método correcto toouse según el escenario.  

#### <a name="subheading21"></a>Carga de un blob grande rápidamente
tooupload una sola grande objetos binarios rápidamente, la aplicación cliente debe cargar sus bloques o páginas en paralelo (que se va a prestar atención a los objetivos de escalabilidad de Hola para blobs individuales y cuenta de almacenamiento de Hola como un todo).  Tenga en cuenta que Hola oficial proporcionado por Microsoft RTM almacenamiento bibliotecas de cliente (. NET, Java) tienen Hola capacidad toodo esto.  Para cada una de las bibliotecas de hello, utilice Hola por debajo del nivel de objeto especificado o la propiedad tooset Hola de simultaneidad:  

* . NET: ParallelOperationThreadCount de conjunto en un toobe de objeto BlobRequestOptions usa.
* Java/Android: use BlobRequestOptions.setConcurrentRequestCount()
* Node.js: Use parallelOperationThreadCount en cualquier opciones de solicitud de Hola o en servicio de blob de Hola.
* C++: Método usar hello blob_request_options:: set_parallelism_factor.

#### <a name="subheading22"></a>Carga de muchos blobs rápidamente
tooupload muchos blobs rápidamente, cargar blobs en paralelo. Esto es más rápido que cargar blobs únicos a la vez con cargas de bloque paralelo, ya que reparte la carga de hello en varias particiones del servicio de almacenamiento de Hola. Un solo blob únicamente admite un rendimiento de 60 MB/segundo (aproximadamente 480 Mbps). En tiempo de Hola de escritura, una cuenta basada en Estados Unidos LRS admite hasta too20 GB/s de entrada que es mucho mayor que el rendimiento de hello admitido por un blob individual.  [AzCopy](#subheading18) realiza cargas en paralelo de forma predeterminada y se recomienda para este escenario.  

### <a name="subheading23"></a>Elegir tipo correcto de Hola de blob
Azure Storage admite dos tipos de blobs: *de página* y *de bloque*. Para un escenario de uso determinado, la elección del tipo de blob afectará Hola rendimiento y escalabilidad de la solución. Los blobs en bloques son adecuados cuando se desea eficazmente grandes cantidades de datos de tooupload: por ejemplo, una aplicación cliente que necesite fotografías tooupload o almacenamiento de vídeo tooblob. Blobs en páginas son adecuados si aplicación hello necesita tooperform operaciones de escritura aleatorias en datos de hello: por ejemplo, discos duros virtuales de Azure se almacenan como blobs en páginas.  

Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tablas
En toohello adición prácticas para comprobadas [todos los servicios](#allservices) se ha descrito anteriormente, siguiente de hello prácticas comprobadas aplica específicamente el servicio de tabla toohello.  

### <a name="subheading24"></a>Objetivos de escalabilidad específicos de tabla
Limitaciones de ancho de banda de toohello de adición de una cuenta de almacenamiento en su totalidad, tablas tienen Hola siguiendo el límite de escalabilidad específico.  Tenga en cuenta que sistema Hola equilibrará la carga como los aumentos del tráfico, pero si su tráfico tiene ráfagas súbitas, es posible que no sea capaz de tooget este volumen de rendimiento inmediatamente.  Si el modelo tiene ráfagas, debe esperar que la limitación de toosee o tiempos de espera durante Hola ráfaga como servicio de almacenamiento de hello automáticamente equilibra la carga de la tabla.  Refuerza lenta generalmente tiene mejores resultados, ya que esto ofrece equilibrio de hello sistema tiempo tooload adecuadamente.  

#### <a name="entities-per-second-account"></a>Entidades por segundo (cuenta)
límite de escalabilidad de Hello para tener acceso a tablas es hasta too20, 000 entidades (de 1KB cada uno) por segundo para una cuenta.  En general, cada entidad que se inserta, actualiza, elimina o examina, cuenta para este objetivo.  Por tanto, una inserción por lotes que contiene 100 entidades contaría como 100 entidades.  Una consulta que examina 1.000 y devuelve 5, contaría como 1.000 entidades.  

#### <a name="entities-per-second-partition"></a>Entidades por segundo (partición)
Dentro de una sola partición, Hola objetivo de escalabilidad para tener acceso a tablas es 2.000 entidades (de 1KB cada uno) por segundo, utilizando Hola contando mismo tal y como se describe en la sección anterior de Hola.  

### <a name="configuration"></a>Configuración
Esta sección enumeran varias opciones de configuración rápida que puede usar toomake importantes mejoras de rendimiento de servicio de la tabla de hello:  

#### <a name="subheading25"></a>Uso de JSON
A partir de la versión de servicio de almacenamiento 2013-08-15, servicio de la tabla de hello admite el uso de JSON en lugar de formato de hello AtomPub basado en XML para transferir datos de la tabla. Esto puede reducir el tamaño de carga tanto como un 75% y puede mejorar significativamente el rendimiento de saludo de la aplicación.

Para obtener más información, vea Hola entrada [tablas de Microsoft Azure: Introducción a JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) y [formato de carga para las operaciones del servicio tabla](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Desactivación de Nagle
Algoritmo de Nagle ampliamente se implementa a través de redes TCP/IP como un rendimiento medio de la red de tooimprove. Sin embargo, no es óptimo en todas las situaciones (como por ejemplo en entornos altamente interactivos). Almacenamiento de Azure, algoritmo de Nagle tiene un impacto negativo en el rendimiento de hello de servicios de tabla y cola de solicitudes toohello y debe deshabilitarse si es posible.  

Para obtener más información, consulte nuestro blog [algoritmo de Nagle no es descriptivo hacia las solicitudes de pequeñas](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), que explica por qué algoritmo de Nagle mal interactúa con las solicitudes de tabla y cola y muestra cómo toodisable en el cliente aplicación.  

### <a name="schema"></a>Esquema
Cómo se representan y consultar los datos es el factor único más importante Hola que afecta al rendimiento de Hola de servicio de la tabla de Hola. Aunque cada aplicación es diferente, en esta sección se describen algunas prácticas probadas generales relacionadas con:  

* Diseño de tablas
* Consultas eficientes
* Actualizaciones de datos eficientes  

#### <a name="subheading27"></a>Tablas y particiones
Las tablas se dividen en dos particiones. Cada entidad almacenada en una partición de recursos compartidos de Hola la misma clave de partición y tiene un tooidentify de clave de fila único dentro de esa partición. Las particiones proporcionan ventajas pero también presentan limitaciones de escalabilidad.  

* Ventajas: Puede actualizar las entidades de hello igual de partición en una transacción de lote único, atómica, que contiene las operaciones de almacenamiento separadas too100 (límite de tamaño total de 4MB). Suponiendo que Hola el mismo número de entidades toobe recuperar, también puede consultar datos en una única partición forma más eficaz que los datos que afecten a las particiones (aunque siga leyendo para obtener más recomendaciones sobre cómo realizar consultas de datos de la tabla).
* El límite de escalabilidad: tooentities de acceso almacenada en una sola partición no puede ser con equilibrio de carga porque las particiones admiten transacciones atómicas. Por esta razón, destino de escalabilidad de Hola de una partición de tabla individual es inferior de servicio de la tabla de Hola como un todo.  

Debido a estas características de las tablas y particiones, debería adoptar Hola siguiendo los principios de diseño:  

* Datos que la aplicación cliente actualizada con frecuencia o consulta en hello misma unidad lógica de trabajo debe estar ubicado en Hola misma partición.  Puede tratarse de la aplicación está agregando escrituras o porque desea tootake aprovechar las operaciones atómicas por lotes.  Asimismo, los datos de una sola partición pueden ser consultados de forma más eficiente en una sola consulta que los datos que se encuentran repartidos por particiones.
* Separan los datos que la aplicación cliente no insert, update o de consulta en hello misma unidad lógica de trabajo (única consulta o actualización por lotes) debe estar ubicado en particiones.  Una nota importante es que no hay ningún toohello limitar el número de claves de partición en una sola tabla, por lo que tener millones de las claves de partición no es un problema y no afectará al rendimiento.  Por ejemplo, si la aplicación es un sitio Web popular con inicio de sesión de usuario, utilizando Hola Id. de usuario como clave de partición de Hola podría ser una buena opción.  

#### <a name="hot-partitions"></a>Particiones calientes
Una partición activa es aquella que está recibiendo un porcentaje desproporcionado de cuenta de hello tráfico tooan y no se puede tener la carga equilibrada porque es una sola partición.  En general, las particiones calientes se crean de una de dos formas:  

##### <a name="subheading28"></a>Patrones Solo anexar y Solo anteponer
patrón de "Sólo anexar" Hello es uno donde todos (o casi todos) de hello tráfico tooa dado PK aumentan y disminuye toohello correspondiente tiempo actual.  Un ejemplo es si la aplicación usa Hola fecha actual como una clave de partición de datos de registro.  Esto da como resultado todas de inserciones de hello va toohello última partición en la tabla y sistema de hello no puede equilibrar la carga como ninguna de las escrituras de hello continuo toohello final de la tabla.  Si el volumen Hola de partición de toothat de tráfico supera el objetivo de escalabilidad de nivel de partición de hello, se producirá en la limitación.  Es mejor tooensure que el tráfico se envía toomultiple particiones, Hola de equilibrio de carga de tooenable solicita a través de la tabla.  

##### <a name="subheading29"></a>Datos con mucho tráfico
Si los resultados de esquema de partición en una sola partición que solo tiene datos que se utilizan mucho más que otras particiones, también puede ver la limitación como destino de escalabilidad de Hola de una sola partición de enfoques de esa partición.  Es mejor toomake seguro de que los resultados del esquema de partición en ningún única partición con objetivos de escalabilidad de Hola.  

#### <a name="querying"></a>Consultas
Esta sección describen las prácticas demostradas para consultar el servicio de la tabla de Hola.  

##### <a name="subheading30"></a>Ámbito de la consulta
Hay varias maneras toospecify Hola comprendida tooquery de entidades.  Hola aquí te mostramos una explicación de los usos de Hola de cada uno.  

En general, evitar análisis (consultas mayores que una sola entidad), pero si debe recorrer, intente tooorganize los datos para que los análisis recuperan datos de Hola que necesita sin examen o devolver una cantidad significativa de entidades que no sea necesario.  

###### <a name="point-queries"></a>Consultas puntuales
Una consulta puntual recupera exactamente una entidad. Hace esto mediante la especificación de clave de partición de Hola y clave de fila de hello entidad tooretrieve. Estas consultas son muy diferentes y debe usarlas siempre que sea posible.  

###### <a name="partition-queries"></a>Consultas de partición
Una consulta de partición es una consulta que recupera un conjunto de datos que comparte una clave de partición común. Por lo general, consulta Hola especifica un intervalo de valores de clave de fila o un intervalo de valores para algunas propiedades de entidad en la clave de partición de tooa de adición. Son menos eficientes que las consultas puntuales y se deben usar con moderación.  

###### <a name="table-queries"></a>Consultas de tabla
Una consulta de tabla es una consulta que recupera un conjunto de entidades que no comparte una clave de partición común. Estas consultas no son diferentes y debe evitarlas siempre que sea posible.  

##### <a name="subheading31"></a>Densidad de consulta
Otro factor clave para la eficacia de las consultas es número Hola de entidades devueltas como toohello comparados número de entidades devueltas establezca toofind digitalizados Hola. Si la aplicación realiza una consulta de tabla con un filtro para un valor de propiedad que solo el 1% de los recursos compartidos de datos de hello, Hola consulta examina 100 entidades para cada una entidad que devuelve. Hello objetivos de escalabilidad de tabla se describe anteriormente todos relacionan toohello número de entidades que se analizan y no Hola número de entidades devueltas: una densidad baja consulta puede hacer fácilmente que Hola tabla servicio toothrottle la aplicación porque debe recorrer tantas entidad de entidades tooretrieve Hola que está buscando.  Consulte la sección de Hola a continuación en [desnormalización](#subheading34) para obtener más información acerca de cómo tooavoid esto.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Limitar Hola cantidad de datos devueltos
###### <a name="subheading32"></a>Filtros
Si sabe que una consulta devolverá las entidades que no es necesario en la aplicación de cliente de hello, considere la posibilidad de con un tamaño de hello tooreduce de filtro de hello devolvió un conjunto. Aunque las entidades de hello no devuelven toohello cliente seguirá teniéndose en cuenta hacia los límites de escalabilidad de hello, mejorará debido a tamaño de carga de red reducido de Hola y Hola reducción del número de entidades que la aplicación cliente debe procesar el rendimiento de la aplicación .  Vea por encima de la nota en [consulta densidad](#subheading31), sin embargo, los objetivos de escalabilidad de Hola relacionan toohello número de entidades que se analizan, por lo que una consulta que filtra las muchas entidades puede seguir produciéndose de limitación, incluso si se devuelven las entidades algunos.  

###### <a name="subheading33"></a>Proyección
Si la aplicación cliente necesita solo un conjunto limitado de propiedades de entidades de hello en la tabla, puede usar el tamaño de proyección toolimit Hola de hello devolvió un conjunto de datos. Como ocurre con filtrado, esto ayuda a tooreduce de carga de red y procesamiento del cliente.  

##### <a name="subheading34"></a>Desnormalización
A diferencia del trabajo con bases de datos relacionales, hello prácticas demostradas para consultar eficazmente los datos de la tabla provocar toodenormalizing los datos. Es decir, duplicar Hola mismos datos en varias entidades (uno por cada clave puede usar datos de hello toofind) número de hello toominimize de entidades que una consulta debe recorrer toofind Hola datos Hola cliente necesidades, en lugar de tener tooscan gran número de entidades toofind datos de Hola la aplicación necesita.  Por ejemplo, en un sitio Web de comercio electrónico, puede que desee toofind un orden tanto por ID de cliente de hello (ofrecerme pedidos del cliente) y por fecha de hello (ofrecerme pedidos en una fecha).  En el almacenamiento de tabla, es mejor entidad de hello toostore (o un tooit de referencia) dos veces: una vez con el nombre de la tabla y PK, Ana buscar toofacilitate con el identificador de cliente, una vez toofacilitate buscar por fecha de Hola.  

#### <a name="insertupdatedelete"></a>Inserción, actualización y eliminación
Esta sección describen las prácticas demostradas para modificar las entidades almacenadas en el servicio de la tabla de Hola.  

##### <a name="subheading35"></a>Lotes
Transacciones por lotes se conocen como las transacciones de grupo de entidad (ETG) en el almacenamiento de Azure; todas las operaciones de hello dentro de un ETG deben estar en una sola partición en una sola tabla. Siempre que sea posible, utilice ETGs tooperform inserciones, actualizaciones y eliminaciones en lotes. Esto reduce el número de Hola de ida y vuelta desde el servidor de toohello de aplicación de cliente, reduce el número de Hola de transacciones facturables (un ETG cuenta como una sola transacción con fines de facturación y puede contener las operaciones de almacenamiento de too100) y se permite atómica actualizaciones (todas las operaciones que se realizan correctamente o produzcan un error dentro de un ETG todas). Los entornos con altas latencias, como por ejemplo dispositivos móviles, sacarán un enorme provecho al uso de ETG.  

##### <a name="subheading36"></a>Upsert
Use operaciones **Upsert** de tabla siempre que sea posible. Hay dos tipos de operaciones **Upsert**; ambos pueden ser más eficientes que las operaciones **Insert** y **Update** tradicionales:  

* **InsertOrMerge**: Utilice esta opción cuando desee tooupload un subconjunto de propiedades de la entidad de hello, pero no está seguro de si ya existe entidad Hola. Si existe la entidad de hello, esta llamada actualiza las propiedades de hello incluidos en hello **Upsert** operación y deja todas las propiedades existentes tal como están, si hello entidad no existe, inserta Hola nueva entidad. Esto es similar proyección toousing en una consulta, ya que solo tiene propiedades de hello tooupload que va a cambiar.
* **InsertOrReplace**: Utilice esta opción cuando desee tooupload una entidad completamente nueva, pero no está seguro de si ya existe. Debe utilizarse únicamente cuando sepa que Hola recién cargado entidad es completamente correcta porque ésta sobrescribe completamente entidad antiguo Hola. Por ejemplo, las que desea tooupdate Hola entidad que almacena la ubicación actual de un usuario, independientemente de si o no aplicación hello previamente almacena los datos de ubicación para el usuario de hello; Hola nueva entidad de ubicación está completa y es necesario que toda la información de cualquier entidad anterior.

##### <a name="subheading37"></a>Almacenamiento de series de datos en una sola entidad
A veces, una aplicación almacena una serie de datos que con frecuencia necesita tooretrieve a la vez: por ejemplo, una aplicación podría realizar un seguimiento de uso de CPU con el tiempo en orden tooplot un gráfico de datos de hello gradual de hello últimas 24 horas. Un enfoque es la entidad de una tabla toohave por hora, con cada entidad que representa una hora concreta y almacenar el uso de CPU de Hola durante esa hora. tooplot estos datos, la aplicación hello deben entidades de hello tooretrieve que contiene datos de Hola de hello 24 horas más reciente.  

Como alternativa, la aplicación puede almacenar el uso de CPU de Hola durante cada hora como una propiedad independiente de una sola entidad: tooupdate cada hora, la aplicación puede utilizar una sola **InsertOrMerge Upsert** llame al valor de hello tooupdate para hello hora más reciente. datos de hello tooplot, aplicación hello solo necesita tooretrieve una sola entidad en lugar de 24, realizar para una consulta muy eficaz (consulte más arriba discusión en [ámbito de consulta](#subheading30)).

##### <a name="subheading38"></a>Almacenamiento de datos estructurados en blobs
Algunas veces, da la sensación de que los datos estructurados deben ir en tablas, pero los intervalos de entidades siempre se recuperan conjuntamente y se pueden insertar por lotes.  Un buen ejemplo de esto es un archivo de registro.  En este caso, puede procesar por lotes varios minutos de registros, insertarlos y, después, siempre estará recuperando varios minutos de registros simultáneamente.  En este caso, para el rendimiento, es mejor blobs toouse en lugar de tablas, ya que se puede reducir significativamente el número de Hola de escritos/devuelven los objetos, así como Hola normalmente el número de solicitudes que necesitan realizar.  

## <a name="queues"></a>Colas
En toohello adición prácticas para comprobadas [todos los servicios](#allservices) se ha descrito anteriormente, siguiente de hello prácticas comprobadas aplica específicamente el servicio de cola toohello.  

### <a name="subheading39"></a>Límites de escalabilidad
Una sola cola puede procesar aproximadamente 2.000 mensajes (1 KB cada uno) por segundo (AddMessage GetMessage y DeleteMessage se cuentan como mensajes aquí). Si esto no es suficiente para la aplicación, debe usar varias colas y mensajes de Hola repartidos.  

Vea los objetivos de escalabilidad actuales en [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md).  

### <a name="subheading40"></a>Desactivación de Nagle
Vea la sección de hello en configuración de la tabla que describe el algoritmo de Nagle hello, algoritmo de Nagle hello es generalmente incorrecto para el rendimiento de Hola de poniendo en cola solicitudes y debe deshabilitarse.  

### <a name="subheading41"></a>Tamaño de los mensajes
El rendimiento y la escalabilidad de la cola se reducen a medida que aumenta el tamaño de los mensajes. Debería colocar necesario de receptor Hola solo hello de la información en un mensaje.  

### <a name="subheading42"></a>Recuperación por lotes
Puede recuperar los mensajes de too32 de una cola en una sola operación. Esto puede reducir el número de Hola de ida y vuelta desde la aplicación de cliente de hello, que es especialmente útil para entornos, como dispositivos móviles, con una latencia elevada.  

### <a name="subheading43"></a>Intervalo de sondeo de la cola
Mayoría de las aplicaciones se sondea para mensajes de una cola, que puede ser uno de los orígenes más grandes de Hola de transacciones para esa aplicación. Seleccione el intervalo de sondeo con cuidado: con demasiada frecuencia de sondeo podría provocar que la aplicación tooapproach objetivos de escalabilidad de Hola de cola de Hola. Sin embargo, en las 200.000 transacciones para 0,01 USD (en el momento de Hola de escritura), un único procesador sondeo una vez cada segundo durante un mes costaría inferior a 15 centavos costos por lo que no es normalmente un factor que afecte a su elección de intervalo de sondeo.  

Para obtener información de costo actualizada, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Puede usar **UpdateMessage** tooincrease Hola invisibilidad tiempo de espera o tooupdate información de estado de un mensaje. Aunque esto es eficaz, recuerde que cada **UpdateMessage** operación cuenta hacia el objetivo de escalabilidad de Hola. Sin embargo, esto puede ser una solución mucho más eficaz que cuando se tiene un flujo de trabajo que pasa a continuación, un trabajo de una cola toohello tal y como se complete cada paso de trabajo de Hola. Con hello **UpdateMessage** operación permite que el mensaje toohello del estado de trabajo de aplicación toosave Hola y, a continuación, seguir trabajando, en lugar de volver a poner en cola el mensaje de saludo para el siguiente paso de trabajo de hello cada vez que se completa un paso de Hola.  

Para obtener más información, vea el artículo de hello [Cómo: cambiar Hola contenido de un mensaje en cola](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Arquitectura de la aplicación
Debe usar colas toomake su arquitectura escalable de la aplicación. continuación de Hola enumeran algunas formas de usar colas toomake la aplicación más escalable:  

* Puede usar los trabajos pendientes toocreate colas de trabajo para su procesamiento y suavizan las cargas de trabajo en la aplicación. Por ejemplo, podría poner en cola las solicitudes de los usuarios tooperform intensivo trabajo del procesador, como cambiar el tamaño de imágenes cargadas.
* Puede utilizar elementos de toodecouple de colas de la aplicación para que se puede escalar de forma independiente. Por ejemplo, un front-end web podría poner resultados de encuesta de usuarios en una cola para analizarlos y almacenarlos posteriormente. Puede agregar que más tooprocess de instancias de rol de trabajo Hola datos de la cola según sea necesario.  

## <a name="conclusion"></a>Conclusión
En este artículo analizado algunos de hello más comunes, prácticas para optimizar el rendimiento al usar el almacenamiento de Azure comprobadas. Se fomentar cada tooassess de desarrollador de aplicaciones que su aplicación en cada uno de Hola por encima de las prácticas y considere la posibilidad de actuar en hello recomendaciones tooget un gran rendimiento para las aplicaciones que utilizan el almacenamiento de Azure.
