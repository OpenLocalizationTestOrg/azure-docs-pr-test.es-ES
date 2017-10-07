---
title: aaaIntroduction tooAzure almacenamiento | Documentos de Microsoft
description: "Información general del almacenamiento de Azure, almacenamiento de datos en línea de Microsoft en la nube de Hola. Obtenga información acerca de cómo toouse Hola mejor solución de almacenamiento de nube disponibles en las aplicaciones."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Introducción tooMicrosoft almacenamiento de Azure

## <a name="overview"></a>Información general
Almacenamiento de Azure es la solución de almacenamiento de hello en la nube para aplicaciones modernas que se basan en las necesidades de escalabilidad toomeet Hola de sus clientes, la disponibilidad y la durabilidad. Al leer este artículo, los desarrolladores, los profesionales de TI y los responsables de negocios aprenderán lo siguiente:

* Qué es Azure Storage y cómo puede aprovecharlo en las aplicaciones en la nube, móviles, de servidor y de escritorio
* ¿Qué tipos de datos se pueden almacenar con los servicios de almacenamiento de Azure de hello: blob de datos (objeto), datos de la tabla de NoSQL, cola de mensajes y los recursos compartidos de archivos.
* Cómo se administra el acceso a datos de tooyour de almacenamiento de Azure
* Cómo se consigue que los datos de Azure Storage sean duraderos mediante la redundancia y la replicación
* Donde toogo siguiente toobuild su primera aplicación de almacenamiento de Azure

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Para obtener más información sobre las herramientas, las bibliotecas y otros recursos para trabajar con Azure Storage, consulte el apartado [Pasos siguientes](#next-steps) que encontrará a continuación.

## <a name="what-is-azure-storage"></a>¿Qué es Azure Storage?
La informática en la nube posibilita nuevos escenarios para aplicaciones que requieren un almacenamiento escalable, duradero y de alta disponibilidad para sus datos, que es justo el motivo por el que Microsoft ha desarrollado Azure Storage. En suma toomaking lo posible para escenarios nuevos de los desarrolladores toobuild aplicaciones a gran escala toosupport, almacenamiento de Azure también proporciona Hola almacenamiento base para máquinas virtuales de Azure, una potencia de tooits FE adicional.

Almacenamiento de Azure es escalable de forma masiva, por lo que puede almacenar y procesar cientos de terabytes de escenarios de grandes cantidades de datos de datos toosupport Hola requeridos por los análisis financieros, científicos y aplicaciones multimedia. O bien, puede almacenar pequeñas cantidades de datos necesarios para un sitio Web de pequeñas empresas de Hola. Siempre que se encuentran en sus necesidades, solo paga por los datos de hello que almacena. Actualmente, Azure Storage alberga decenas de billones de objetos de cliente únicos y administra, por término medio, millones de solicitudes por segundo.

Almacenamiento de Azure es flexible, para que pueda diseñar aplicaciones para una audiencia global grande y escale esas aplicaciones según le convenga - tanto en cuanto a la cantidad de Hola de los datos almacenados y Hola número de solicitudes realizadas en él. Solo pagará por lo que use y únicamente cuando lo use.

Azure Storage utiliza un sistema de creación automática de particiones que equilibra la carga de los datos automáticamente en función del tráfico. Esto significa que como peticiones de hello en el crecimiento de su aplicación, el almacenamiento de Azure asigna automáticamente toomeet de los recursos adecuados de hello ellos.

Almacenamiento de Azure es accesible desde cualquier lugar en hello world, desde cualquier tipo de aplicación, si se está ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un teléfono móvil o dispositivo de tableta gráfica. Puede usar el almacenamiento de Azure en los escenarios móviles donde la aplicación hello almacena un subconjunto de datos en el dispositivo de Hola y sincroniza con un conjunto completo de los datos almacenados en la nube de Hola.

Azure Storage admite clientes que utilizan una gran variedad de sistemas operativos (incluidos Windows y Linux) y diversos lenguajes de programación (incluidos .NET, Node.js, Python, Ruby, PHP y C++, así como lenguajes de programación móvil) para un desarrollo más práctico. Almacenamiento de Azure también expone recursos de datos a través de las API de REST simple, que están disponibles tooany cliente capaz de enviar y recibir datos a través de HTTP/HTTPS.

Azure Premium Storage ofrece compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo con un alto consumo de E/S que se ejecutan en Azure Virtual Machines. Con el almacenamiento de Azure Premium, puede adjuntar varios datos persistentes discos tooa virtual machine y configurarlos toomeet los requisitos de rendimiento. Un disco de SSD de Azure Premium Storage realiza copias de seguridad de cada disco de datos para ofrecer un rendimiento máximo de E/S. Consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](storage-premium-storage.md) para ver información detallada.

## <a name="introducing-hello-azure-storage-services"></a>Introducción a servicios de almacenamiento de Azure de Hola
El almacenamiento de Azure proporciona Hola siguientes cuatro servicios: almacenamiento de blobs, el almacenamiento de tabla, almacenamiento en la cola y el almacenamiento de archivos.

* Blob Storage almacena datos de objetos no estructurados. Un blob puede ser un tipo cualquiera de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es que se hace referencia tooas almacenamiento de objetos.
* Table Storage almacena conjuntos de datos estructurados. Almacenamiento de tabla es un almacén de datos del atributo de clave NoSQL, que permite el desarrollo rápido y las cantidades de toolarge de acceso rápido de datos.
* Queue Storage ofrece una solución de mensajería confiable para el procesamiento de flujos de trabajo y para la comunicación entre los componentes de los servicios en la nube.
* Almacenamiento de archivos ofrece almacenamiento compartido para aplicaciones heredadas mediante el protocolo SMB estándar de Hola. Máquinas virtuales de Azure y servicios en la nube pueden compartir datos de archivos a través de los componentes de la aplicación a través de recursos compartidos montados y aplicaciones locales pueden tener acceso a los datos de archivo en un recurso compartido a través de hello API de REST de servicio de archivos.

Una cuenta de almacenamiento de Azure es una cuenta segura que proporciona acceso a tooservices en el almacenamiento de Azure. La cuenta de almacenamiento proporciona Hola espacio de nombres único para los recursos de almacenamiento. imagen de Hello siguiente muestra las relaciones de hello entre los recursos de almacenamiento de Azure de hello en una cuenta de almacenamiento:

![Recursos de Azure Storage](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Almacenamiento de blobs
Para los usuarios con grandes cantidades de toostore de datos de objeto no estructurados en la nube de hello, almacenamiento de blobs ofrece una solución escalable y rentable. Puede usar el contenido de toostore de almacenamiento de blobs como:

* Documentos
* Datos de contenido social, como fotos, vídeos, música y blogs
* Copias de seguridad de archivos, equipos, bases de datos y dispositivos
* Imágenes y texto para las aplicaciones web
* Datos de configuración para las aplicaciones en la nube
* Datos de gran tamaño, como registros y otros conjuntos de datos grandes

Cada blob se organiza en un contenedor. Los contenedores también proporcionan un toogroups de directivas de seguridad de un modo útil tooassign de objetos. Una cuenta de almacenamiento puede contener cualquier número de contenedores y un contenedor puede contener cualquier número de blobs, seguridad de límite de capacidad de 500 TB toohello de cuenta de almacenamiento de Hola.

Blob Storage ofrece tres tipos de blobs: blobs en bloques, blobs en anexos y blobs en páginas (discos).

* Los blobs en bloques están optimizados para el streaming y para el almacenamiento de objetos en la nube, y constituyen una opción idónea para almacenar documentos, archivos multimedia y copias de seguridad, entre otros.
* Anexar blobs de blobs de tooblock similares, pero están optimizados para las operaciones de anexión. Se puede actualizar un blob en anexos agregando un nuevo extremo toohello de bloque. Anexar blobs son una buena elección para escenarios como la del registro, donde nuevos datos necesitan toobe escribe solo toohello final del blob de Hola.
* Blobs en páginas se optimización para representar los discos de IaaS y admitir aleatorio escribe y puede ser up too1 TB de tamaño. Un disco IaaS asociado a una red de máquinas virtuales de Azure es un VHD almacenado como blob en páginas.

Para grandes conjuntos de datos donde las restricciones de red que cargar o descargar el almacenamiento de datos tooBlob a través de la conexión de hello poco realista, puede enviar un tooimport tooMicrosoft de unidad de disco duro o exportar datos directamente desde el centro de datos de Hola. Vea [usar Hola servicio de importación y exportación de Microsoft Azure tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md).

## <a name="table-storage"></a>Almacenamiento de tablas

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

A menudo, las aplicaciones modernas demandan almacenes de datos con una flexibilidad y escalabilidad superiores a las que requerían las generaciones anteriores de software. Almacenamiento de tabla ofrece un almacenamiento altamente disponible y escalable de forma masiva, por lo que la aplicación puede escalar automáticamente toomeet demanda de los usuarios. Este tipo de almacenamiento se basa en un almacén de claves/atributos NoSQL de Microsoft con un diseño sin esquema que lo diferencia de las bases de datos relacionales tradicionales. Con un almacén de datos schemaless, resulta fácil tooadapt necesidades de los datos como Hola de evolucionar de la aplicación. Almacenamiento de tabla es fácil toouse, por lo que los desarrolladores pueden crear aplicaciones rápidamente. Acceso toodata es rápido y rentable para todos los tipos de aplicaciones.  además, su coste es muy inferior al del SQL tradicional para volúmenes de datos similares.

Este tipo de almacenamiento se basa en un almacén de clave-atributo, lo que significa que cada valor de una tabla se almacena con un nombre de propiedad tipado. nombre de la propiedad de Hello puede usarse para filtrar y especificar criterios de selección. Una colección de propiedades y sus valores, componen una entidad. Puesto que el almacenamiento de tabla es schemaless, dos entidades en Hola misma tabla puede contener diferentes colecciones de propiedades y esas propiedades pueden ser de tipos diferentes.

Puede usar la tabla almacenamiento toostore flexible conjuntos de datos, como los datos de usuario para aplicaciones web, libretas de direcciones, información del dispositivo y cualquier otro tipo de metadatos que necesite el servicio.  Puede almacenar cualquier número de entidades en una tabla y una cuenta de almacenamiento puede contener cualquier número de tablas, una toohello el límite de capacidad de la cuenta de almacenamiento de Hola.

Al igual que los Blobs y colas, los desarrolladores pueden administrar y tener acceso al almacenamiento de tabla utilizando los protocolos estándar de REST, sin embargo almacenamiento de tablas también admite un subconjunto del protocolo de OData de hello, simplificando avanzadas capacidades de consulta y la habilitación de JSON y AtomPub (basado en XML) da formato.

Para aplicaciones basadas en Internet de hoy en día, las bases de datos NoSQL como el almacenamiento de tabla ofrecen una popular tootraditional alternativo bases de datos relacionales.

## <a name="queue-storage"></a>Queue Storage
A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente. Almacenamiento de cola proporciona una solución de mensajería confiable para la comunicación asincrónica entre los componentes de aplicación, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil. Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.

Una cuenta de almacenamiento puede contener un número cualquiera de colas y, Una cola puede contener cualquier número de mensajes, seguridad toohello el límite de capacidad de la cuenta de almacenamiento de Hola. Los mensajes individuales pueden ser up too64 KB de tamaño.

## <a name="file-storage"></a>File Storage
Hola servicio de archivos de Azure permite tooset los recursos compartidos de archivos de red de alta disponibilidad que se puede acceder mediante Protocolo de bloque de mensajes del servidor (SMB) estándar de Hola. Que significa que varias máquinas virtuales pueden compartir Hola mismo archivos con acceso de lectura y escritura. También puede leer archivos de hello mediante la interfaz REST de Hola o bibliotecas de cliente de almacenamiento de Hola.

Único lo que distingue el almacenamiento de archivos de Azure de archivos en un recurso compartido de archivos corporativos es que puede tener acceso a archivos de Hola desde cualquier lugar de Hola a todos mediante una dirección URL que señala el archivo toohello e incluye un token de firma (SAS) de acceso compartido. Puede generar tokens SAS; le permiten a asset privada de tooa de acceso específico para un período de tiempo determinado.

Los recursos compartidos de archivos se pueden utilizar para muchos escenarios comunes:

* Muchas aplicaciones locales usan recursos compartidos de archivos. Esta característica hace más fácil toomigrate aquellas aplicaciones que comparten datos tooAzure. Si va a montar hello toohello del recurso compartido de archivo misma letra que Hola de unidad local aplicación usa, parte de saludo de la aplicación que tiene acceso a recurso compartido de archivos de Hola debe funcionar con unos cambios mínimos, si lo hay.

* Los archivos de configuración se pueden almacenar en un recurso compartido de archivos y se puede acceder a ellos desde varias máquinas virtuales. Herramientas y utilidades que se usan por varios desarrolladores en un grupo pueden almacenarse en un recurso compartido de archivos, asegurándose de que todo el mundo pueda encontrarlos, y que usan Hola misma versión.

* Registros de diagnóstico, métricas y volcados de memoria son sólo tres ejemplos de datos que se pueden escritos el recurso compartido de archivos de tooa y procesados o analizar más tarde.

En este tiempo, la autenticación basada en Active Directory y el acceso no se admiten listas de control (ACL), pero estarán en algún momento futuro Hola. credenciales de cuenta de almacenamiento de Hello son autenticación de tooprovide utilizado para el recurso compartido de archivos de toohello de acceso. Esto significa que cualquiera con el recurso compartido de hello montado tendrá el recurso compartido de toohello de acceso completo de lectura/escritura.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Acceso tooBlob, tabla, cola y archivo de recursos
De forma predeterminada, solo el propietario de cuenta del almacenamiento de hello puede tener acceso a los recursos de la cuenta de almacenamiento de Hola. Para la seguridad de Hola de los datos, se debe autenticar cada solicitud realizada en los recursos de la cuenta. Esta autenticación se basa en un modelo de clave compartida. Blobs también pueden ser toosupport configurado la autenticación anónima.

Al crear una cuenta de almacenamiento, se le asignan dos claves de acceso privado que se utilizan para la autenticación. Existencia de dos claves garantiza que la aplicación sigue estando disponible cuando se regeneran con regularidad claves hello como una práctica común de administración de claves de seguridad.

Si necesita recursos de almacenamiento de tooallow a los usuarios controlados acceso tooyour, a continuación, puede crear una firma de acceso compartido. Una firma de acceso compartido (SAS) es un símbolo (token) que puede ser la dirección URL de tooa anexado que permite delega acceso tooa de recursos de almacenamiento. Cualquier persona que posee el token de hello puede tener acceso a recursos de hello señala permisos de hello toowith especifica, para el período de Hola de tiempo que sea válido. A partir de la versión 2015-04-05, Azure Storage admite dos tipos de firmas de acceso compartido: SAS de servicio y SAS de cuenta.

delegados SAS del servicio de Hello tener acceso a recursos tooa en solo uno de los servicios de almacenamiento de hello: Hola servicio Blob, cola, tabla o archivo.

Una cuenta SA delega tooresources de acceso en uno o varios de los servicios de almacenamiento de Hola. Puede delegar operaciones de tooservice-nivel de acceso que no están disponibles con un servicio de SAS. También puede delegar el acceso tooread, escritura y las operaciones de eliminación en contenedores de blobs, tablas, colas y recursos compartidos de archivos que no se permiten con un servicio de SAS.

Por último, puede especificar que un contenedor y sus blobs, o un blob específico, estén disponibles para el acceso público. Cuando se indica que un contenedor o blob es público, todos los usuarios pueden leerlo de forma anónima: no se requiere autenticación.  Los contenedores y los blobs públicos son útiles para exponer recursos, como archivos multimedia y documentos hospedados en sitios web.  latencia de red toodecrease para una audiencia global, puede almacenar en caché datos de blob usados por sitios Web con hello CDN de Azure.

Para más información sobre firmas de acceso compartido, consulte [Uso de firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md) . Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md) y [autenticación para servicios de almacenamiento de Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) para obtener más información sobre la cuenta de almacenamiento de tooyour un acceso seguro.

## <a name="replication-for-durability-and-high-availability"></a>Replicación para obtener durabilidad y alta disponibilidad
datos de Hello en su cuenta de almacenamiento siempre es de Microsoft Azure replican tooensure durabilidad y alta disponibilidad. Copias de replicación de los datos, ya sea dentro de Hola mismo centro de datos o el segundo centro de datos tooa, según la opción de replicación que elija. La replicación protege los datos y conserva el tiempo de actividad de la aplicación en caso de hello de errores de hardware transitorios. Si se replican los datos del centro de datos segundo tooa, que también protege los datos frente a un error grave en la ubicación principal Hola.

La replicación garantiza que la cuenta de almacenamiento cumple hello [contrato de nivel de servicio (SLA) para el almacenamiento](https://azure.microsoft.com/support/legal/sla/storage/) incluso de cara de Hola de errores. Vea Hola SLA para obtener información sobre el almacenamiento de Azure garantiza la durabilidad y disponibilidad.

Cuando se crea una cuenta de almacenamiento, puede seleccionar una de las siguientes opciones de replicación de hello:

* **Almacenamiento con redundancia local (LRS).** El almacenamiento con redundancia local mantiene tres copias de sus datos. LRS se replica tres veces dentro de un único centro de datos de una sola región. LRS protege los datos de errores de hardware normal, pero no frente a errores de Hola de un solo centro de datos.

    LRS se ofrece con un descuento. Para la máxima durabilidad, es recomendable utilizar el almacenamiento con redundancia geográfica, que se describe a continuación.
* **Almacenamiento con redundancia de zona (ZRS).** El almacenamiento con redundancia de zona mantiene tres copias de los datos. ZRS se replica tres veces entre dos instalaciones de toothree, en una única región o entre dos regiones, lo que proporciona mayor durabilidad que el LRS. ZRS garantiza la durabilidad de sus datos dentro de una sola región.

    ZRS ofrece un mayor nivel de durabilidad que LRS; sin embargo, para disfrutar de la máxima durabilidad, es recomendable usar el almacenamiento con redundancia geográfica, que se describe a continuación.

  > [!NOTE]
  > Actualmente, el ZRS solo está disponible para los blobs en bloques y únicamente se admite en las versiones del 14/02/2014 y posteriores.
  >
  > Una vez que ha creado la cuenta de almacenamiento y selecciona ZRS, no puede convertir toouse tooany otro tipo de replicación, o viceversa.
  >
  >
* **Almacenamiento con redundancia geográfica (GRS)**. GRS mantiene seis copias de sus datos. Con GRS, los datos se replican tres veces dentro de la región principal de Hola y también se replican tres veces en una región secundaria a cientos de millas fuera de la región principal de hello, que proporciona el máximo nivel de durabilidad de Hola. En caso de hello de un error en la región principal de hello, almacenamiento de Azure impedirá la región secundaria toohello de conmutación por error. GRS garantiza la durabilidad de sus datos en dos regiones independientes.

    Para obtener información sobre los emparejamientos principales y secundarios por región, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).
* **Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS)**. Almacenamiento con redundancia geográfica con acceso de lectura replica los datos tooa ubicación secundaria y también proporciona acceso de lectura tooyour datos en la ubicación secundaria Hola. Almacenamiento con redundancia geográfica con acceso de lectura le permite tooaccess los datos de ubicación secundaria de hello, en caso de Hola que una ubicación deja de estar disponible u Hola principal. Almacenamiento con redundancia geográfica con acceso de lectura es la opción de valor predeterminado de hello para la cuenta de almacenamiento de forma predeterminada al crearlo.

  > [!IMPORTANT]
  > Puede cambiar cómo los datos se replican una vez creada la cuenta de almacenamiento, a menos que especifique ZRS cuando se creó la cuenta de hello. Sin embargo, tenga en cuenta que puede conllevar una coste si se cambia de LRS tooGRS o RA-GRS de transferencia de datos adicionales de un solo uso.
  >
  >

Consulte [Replicación de Azure Storage](storage-redundancy.md) para más información sobre las opciones de replicación de almacenamiento.

Para obtener información de precios para la replicación de cuentas de almacenamiento, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/). Consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services) para más información acerca de qué servicios están disponibles en cada región.

Para obtener detalles de arquitectura sobre la durabilidad con Azure Storage, consulte [Documento de SOSP: Azure Storage: un servicio de almacenamiento en la nube altamente disponible con gran coherencia](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transferencia de datos tooand de almacenamiento de Azure
Puede usar blob toocopy de hello AzCopy utilidad de línea de comandos, archivos y datos de la tabla dentro de la cuenta de almacenamiento o a través de las cuentas de almacenamiento. Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) para obtener más información.

AzCopy se basa en hello [biblioteca de movimiento de datos de Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), que está disponible actualmente en vista previa.

Hola servicio de importación y exportación de Azure proporciona una manera tooimport blob de datos en o exportar datos de blob de la cuenta de almacenamiento a través de un disco de la unidad de disco duro enviadas por toohello centro de datos de Azure. Para obtener más información acerca de hello servicio de importación/exportación, consulte [usar Hola servicio de importación y exportación de Microsoft Azure tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md).

## <a name="pricing"></a>Precios
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>API, bibliotecas y herramientas de Storage
Es posible acceder a los recursos de Azure Storage por medio de cualquier lenguaje que pueda realizar solicitudes HTTP/HTTPS. Además, ofrece bibliotecas de programación para varios lenguajes de amplio uso. Estas bibliotecas simplifican muchos aspectos relacionados con el uso de Azure,  Storage, ya que abordan detalles como la invocación sincrónica y asincrónica, el procesamiento por lotes de las operaciones, la administración de excepciones, los reintentos automáticos y el comportamiento operativo, entre otros. Bibliotecas están actualmente disponibles para hello siguientes lenguajes y plataformas, con otras personas en Hola canalización:

### <a name="azure-storage-data-services"></a>Servicios de datos de Azure Storage
* [API de REST de servicios de almacenamiento](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Biblioteca de cliente de almacenamiento para. NET, Windows Phone y Windows Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Biblioteca de cliente de almacenamiento para C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteca de cliente de Storage para Java/Android](https://azure.microsoft.com/develop/java/)
* [Biblioteca de cliente de Storage para Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteca de cliente de Storage para PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteca de cliente de Storage para Ruby](https://azure.microsoft.com/develop/ruby/)
* [Biblioteca de cliente de Storage para Python](https://azure.microsoft.com/develop/python/)
* [Cmdlets de Storage para PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Servicios de administración de Azure Storage
* [Referencia de API de REST de proveedor de recursos de almacenamiento](/rest/api/storagerp/)
* [Biblioteca de cliente del proveedor de recursos de Storage para .NET](/dotnet/api/microsoft.azure.management.storage)
* [Cmdlets de proveedor de recursos de Storage para PowerShell 1.0](/powershell/module/azure.storage)
* [API de REST de administración de servicios de almacenamiento (clásico)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Servicios de movimiento de datos de Azure Storage
* [API de REST del servicio Storage Import/Export](storage-import-export-service.md)
* [Biblioteca de cliente de movimiento de datos de Storage para .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Herramientas y utilidades
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [Herramientas de cliente de Almacenamiento de Azure](storage-explorers.md)
* [SDK y herramientas de Azure](https://azure.microsoft.com/tools/)
* [Emulador de Azure Storage](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [Utilidad de línea de comandos AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre el almacenamiento de Azure, explorar estos recursos:

### <a name="documentation"></a>Documentación
* [Documentación de Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Cree una cuenta de almacenamiento](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Para administradores
* [Usar Azure PowerShell con Azure Storage](storage-powershell-guide-full.md)
* [Uso de la CLI de Azure con Azure Storage](storage-azure-cli.md)

### <a name="for-net-developers"></a>Para desarrolladores de .NET
* [Introducción a Azure Blob Storage mediante .NET](storage-dotnet-how-to-use-blobs.md)
* [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md)
* [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md)
* [Introducción a Azure File Storage en Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Para desarrolladores de Java/Android
* [¿Cómo toouse almacenamiento de blobs desde Java](storage-java-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Java](storage-java-how-to-use-table-storage.md)
* [¿Cómo toouse almacenamiento de cola en Java](storage-java-how-to-use-queue-storage.md)
* [¿Cómo toouse almacenamiento de archivos de Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Para desarrolladores de Node.js
* [¿Cómo toouse almacenamiento de blobs de Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Node.js](storage-nodejs-how-to-use-table-storage.md)
* [¿Cómo toouse almacenamiento de cola de Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Para desarrolladores de PHP
* [¿Cómo toouse almacenamiento de blobs de PHP](storage-php-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de tablas de PHP](storage-php-how-to-use-table-storage.md)
* [¿Cómo toouse almacenamiento de cola de PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Para desarrolladores de Ruby
* [¿Cómo toouse almacenamiento de blobs de Ruby](storage-ruby-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Ruby](storage-ruby-how-to-use-table-storage.md)
* [¿Cómo toouse Queue storage from. Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Para desarrolladores de Python
* [¿Cómo toouse almacenamiento de blobs de Python](storage-python-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Python](storage-python-how-to-use-table-storage.md)
* [¿Cómo toouse almacenamiento de cola de Python](storage-python-how-to-use-queue-storage.md)
* [¿Cómo toouse almacenamiento de archivos de Python](storage-python-how-to-use-file-storage.md)
