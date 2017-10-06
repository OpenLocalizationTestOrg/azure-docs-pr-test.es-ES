---
title: aaaIntroduction tooAzure almacenamiento | Documentos de Microsoft
description: "Introducción tooAzure almacenamiento, almacenamiento de datos de Microsoft en la nube de Hola."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Introducción tooMicrosoft almacenamiento de Azure

Microsoft Azure Storage es un servicio en la nube administrado por Microsoft que proporciona almacenamiento altamente disponible, seguro, duradero, escalable y redundante. Microsoft se encarga del mantenimiento y soluciona automáticamente los problemas críticos. 

Azure Storage consta de tres servicios de datos: Blob Storage, File Storage y Queue Storage. Almacenamiento de BLOB admite almacenamiento estándar y premium, con el almacenamiento premium con solo SSD posibles de rendimiento más rápido de Hola. Otra característica es almacenamiento frío, permitiéndole toostorage grandes cantidades de datos rara vez acceso para un menor costo.

En este artículo, aprenderá sobre siguientes hello:
* Servicios de almacenamiento de Azure de Hola
* tipos de Hola de cuentas de almacenamiento
* El acceso a los blobs, las colas y los archivos
* El cifrado
* La replicación 
* La migración de datos de almacenamiento
* Hola muchas de las bibliotecas de cliente de almacenamiento disponibles. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Introducción a servicios de almacenamiento de Azure de Hola

toouse cualquiera de los servicios de hello había proporcionado por el almacenamiento de Azure: almacenamiento de blobs, almacenamiento de archivos y almacenamiento de cola--crear primero una cuenta de almacenamiento y, a continuación, puede transferir datos hacia y desde un servicio específico de esa cuenta de almacenamiento. 

## <a name="blob-storage"></a>Almacenamiento de blobs

Básicamente, los blobs son archivos como los que se almacenan en el equipo (o tableta, dispositivo móvil, etc.). Pueden ser imágenes, archivos de Microsoft Excel, archivos HTML, discos duros virtuales (VHD), macrodatos, como registros, copias de seguridad de bases de datos..., cualquier cosa. BLOB se almacenan en contenedores, que son toofolders similar. 

Después de almacenar archivos en almacenamiento de blobs, se pueden tener acceso a ellos desde cualquier lugar de Hola a todos mediante direcciones URL, Hola interfaz REST o una de las bibliotecas de cliente de almacenamiento de Azure SDK Hola. Las bibliotecas de cliente de almacenamiento están disponibles en varios lenguajes, como Node.js, Java, PHP, Ruby, Python y .NET. 

Hay tres tipos de blobs: blobs en bloques, blobs en anexos y blobs en páginas (para los archivos de disco duro virtual).

* Blobs en bloques son archivos normales de toohold usa seguridad tooabout 4,7 TB. 
* Blobs en páginas son archivos de acceso aleatorio de toohold usado hasta too8 TB de tamaño. Se usan para los archivos de disco duro virtual de Hola que realizar copias de las máquinas virtuales.
* Anexar blobs están formados por bloques como blobs en bloques hello, pero están optimizados para las operaciones de anexión. Se usan para cosas como registro toohello información mismo blob desde varias máquinas virtuales.

Para grandes conjuntos de datos donde las restricciones de red que cargar o descargar el almacenamiento de datos tooBlob a través de la conexión de hello poco realista, puede enviar un conjunto de unidades de disco duro tooMicrosoft tooimport o exportar datos directamente desde el centro de datos de Hola. Vea [usar Hola servicio de importación y exportación de Microsoft Azure tooTransfer datos tooBlob almacenamiento](../storage-import-export-service.md).

## <a name="file-storage"></a>File Storage

Hola servicio de archivos de Azure permite tooset los recursos compartidos de archivos de red de alta disponibilidad que se puede acceder mediante Protocolo de bloque de mensajes del servidor (SMB) estándar de Hola. Que significa que varias máquinas virtuales pueden compartir Hola mismo archivos con acceso de lectura y escritura. También puede leer archivos de hello mediante la interfaz REST de Hola o bibliotecas de cliente de almacenamiento de Hola. 

Único lo que distingue el almacenamiento de archivos de Azure de archivos en un recurso compartido de archivos corporativos es que puede tener acceso a archivos de Hola desde cualquier lugar de Hola a todos mediante una dirección URL que señala el archivo toohello e incluye un token de firma (SAS) de acceso compartido. Puede generar tokens SAS; le permiten a asset privada de tooa de acceso específico para un período de tiempo determinado. 

Los recursos compartidos de archivos se pueden utilizar para muchos escenarios comunes: 

* Muchas aplicaciones locales usan recursos compartidos de archivos. Esta característica hace más fácil toomigrate aquellas aplicaciones que comparten datos tooAzure. Si va a montar hello toohello del recurso compartido de archivo misma letra que Hola de unidad local aplicación usa, parte de saludo de la aplicación que tiene acceso a recurso compartido de archivos de Hola debe funcionar con unos cambios mínimos, si lo hay.

* Los archivos de configuración se pueden almacenar en un recurso compartido de archivos y se puede acceder a ellos desde varias máquinas virtuales. Herramientas y utilidades que se usan por varios desarrolladores en un grupo pueden almacenarse en un recurso compartido de archivos, asegurándose de que todo el mundo pueda encontrarlos, y que usan Hola misma versión.

* Registros de diagnóstico, métricas y volcados de memoria son sólo tres ejemplos de datos que se pueden escritos el recurso compartido de archivos de tooa y procesados o analizar más tarde.

En este tiempo, la autenticación basada en Active Directory y el acceso no se admiten listas de control (ACL), pero estarán en algún momento futuro Hola. credenciales de cuenta de almacenamiento de Hello son autenticación de tooprovide utilizado para el recurso compartido de archivos de toohello de acceso. Esto significa que cualquiera con el recurso compartido de hello montado tendrá el recurso compartido de toohello de acceso completo de lectura/escritura.

## <a name="queue-storage"></a>Queue Storage

Hola servicio cola de Azure es usado toostore y recuperar mensajes. Cola de mensajes puede ser up too64 KB de tamaño y una cola puede contener millones de mensajes. Las colas son listas de toostore utilizada normalmente de toobe de mensajes que se procesan de forma asíncrona. 

Por ejemplo, supongamos que desea que las imágenes de los clientes toobe tooupload capaz de y desea toocreate vistas en miniatura de cada imagen. Podría tener que su cliente esperará que las miniaturas de hello toocreate al cargar imágenes de Hola. Una alternativa sería toouse una cola. Cuando el cliente de hello finaliza su carga, escribir una cola de toohello de mensajes. A continuación, debe tener una función de Azure recuperar mensajes de bienvenida de cola de Hola y crear miniaturas de Hola. Cada una de las partes de Hola de este procesamiento se puede escalar por separado, lo que le proporciona mayor control al optimizar para su uso.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Almacenamiento de tablas
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
Azure Table Storage estándar ahora forma parte de Cosmos DB. Para Azure Table Storage también hay tablas premium disponibles, que ofrecen tablas con rendimiento optimizado, distribución global e índices secundarios automáticos. toolearn más y probar Hola premium experiencia, consulte [base de datos de Azure Cosmos: API de tabla](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Almacenamiento en disco

equipo de almacenamiento de Azure de Hello también es el propietario de los discos, que incluye todos los de hello administrado y capacidades de los discos no administrados utilizadas por máquinas virtuales. Para obtener más información acerca de estas características, vea hello [documentación del servicio de proceso](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Tipos de cuentas de almacenamiento 

Esta tabla muestra hello distintos tipos de cuentas de almacenamiento y los objetos que pueden utilizarse con cada uno de ellos.

|**Tipo de cuenta de almacenamiento**|**Uso general estándar**|**Uso general premium**|**Niveles de acceso frecuente y esporádico de Blob Storage**|
|-----|-----|-----|-----|
|**Servicios admitidos**| Servicios de blobs, archivos y colas | Blob Service | Blob Service|
|**Tipos de blobs compatibles**|Blobs en bloques, blobs en páginas y blobs en anexos | Blobs en páginas | Blobs en bloques y blobs en anexos|

### <a name="general-purpose-storage-accounts"></a>Cuentas de almacenamiento de uso general

Hay dos tipos de cuentas de almacenamiento de uso general. 

#### <a name="standard-storage"></a>Standard storage 

Hola más usada de almacenamiento tienen las cuentas de almacenamiento estándar, que se pueden usar para todos los tipos de datos. Cuentas de almacenamiento estándar usan datos de medios magnéticos toostore.

#### <a name="premium-storage"></a>Premium Storage

Premium Storage proporciona almacenamiento de alto rendimiento para blobs en páginas, que se utiliza principalmente para los archivos de disco duro virtual. Cuentas de almacenamiento Premium usan datos de toostore SSD. Microsoft recomienda usar Premium Storage para todas las máquinas virtuales.

### <a name="blob-storage-accounts"></a>Cuentas de Blob Storage

cuenta de almacenamiento de blobs de Hello es una cuenta de almacenamiento especializado usado toostore blobs en bloques y blobs en anexos. En estas cuentas no se pueden almacenar blobs en páginas, como los de archivos de disco duro virtual. Estas cuentas permiten tooset un tooHot de nivel de acceso o bien; nivel de Hello puede modificarse en cualquier momento. 

nivel de acceso activa de Hola se utiliza para los archivos que se accede con frecuencia: pagar un costo mayor para el almacenamiento, pero es mucho menor costo de Hola de tener acceso a blobs de Hola. Para los blobs almacenados en el nivel de acceso de acceso esporádico de Hola, usted paga un costo mayor para tener acceso a blobs de hello, pero es mucho menor costo de Hola de almacenamiento.

## <a name="accessing-your-blobs-files-and-queues"></a>Acceso a los blobs, las colas y los archivos

Cada cuenta de almacenamiento tiene dos claves de autenticación y ambas sirven para cualquier operación. Hay dos claves para que pueda recuperar a través de hello ocasionalmente claves de seguridad tooenhance. Es fundamental que estas claves se mantenga segura porque su posesión, junto con el nombre de la cuenta de hello, permite que los datos de tooall acceso ilimitado de cuenta de almacenamiento de Hola. 

Esta sección se examinan cuenta de almacenamiento Hola de dos maneras toosecure y sus datos. Para obtener información detallada acerca de cómo proteger su cuenta de almacenamiento y los datos, vea hello [Guía de seguridad de almacenamiento de Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Proteger el acceso cuentas toostorage con Azure AD

Toosecure una manera de obtener acceso a datos de almacenamiento de tooyour es mediante el control de acceso a claves de cuenta de almacenamiento de toohello. Con el Administrador de recursos del Control de acceso basado en roles (RBAC), puede asignar roles toousers, grupos o las aplicaciones. Estas funciones están vinculadas tooa conjunto específico de acciones permitidas o denegadas. Cuenta de almacenamiento de toogrant acceso tooa mediante RBAC solo administra operaciones de administración de Hola para esa cuenta de almacenamiento, como el cambio de nivel de acceso de Hola. No puede utilizar objetos RBAC toogrant acceso toodata como un recurso compartido de archivo o contenedor específico. Sin embargo, puede usar RBAC toogrant toohello almacenamiento cuenta teclas de acceso, que pueden ser, a continuación, los objetos de datos de hello tooread usado. 

### <a name="securing-access-using-shared-access-signatures"></a>Protección del acceso con firmas de acceso compartido 

Puede usar firmas de acceso compartido y almacenan toosecure de directivas de acceso a los objetos de datos. Una firma de acceso compartido (SAS) es una cadena que contiene un token de seguridad que puede ser adjunta toohello URI para un activo que permite a los objetos de almacenamiento de toodelegate acceso toospecific y restricciones toospecify como permisos y el intervalo de fecha y hora de Hola de acceso. Esta característica tiene amplias funcionalidades. Para obtener información detallada, consulte demasiado[utilizando firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Acceso público tooblobs

Hola servicio le permite tooprovide acceso público tooa contenedor y sus blobs o un blob en cuestión. Cuando se indica que un contenedor o blob es público, todos los usuarios pueden leerlo de forma anónima: no se requiere autenticación. Un ejemplo de cuándo se desea toodo es cuando tiene un sitio Web que está usando imágenes, vídeo o documentos desde almacenamiento de blobs. Para obtener más información, vea [administrar acceso de lectura anónimo toocontainers y blobs](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Cifrado

Hay un par de tipos básicos de cifrado disponibles para los servicios de almacenamiento de Hola. 

### <a name="encryption-at-rest"></a>Cifrado en reposo 

Puede habilitar el cifrado de servicio de almacenamiento (SSE) en cualquier servicio de archivos de hello (versión preliminar) u Hola servicio Blob para una cuenta de almacenamiento de Azure. Si está habilitada, se cifran todos los datos escritos servicio específico de toohello antes de escribir. Cuando se leen datos de hello, se descifra antes de devolver. 

### <a name="client-side-encryption"></a>cifrado de cliente

bibliotecas de cliente de almacenamiento Hello tienen métodos que se puede llamar a tooprogrammatically cifrar los datos antes de enviarlo a través de conexión de Hola de hello cliente tooAzure. Se almacenan cifrados, lo que significa que también se cifran en reposo. Al leer datos hello, descifrar información Hola después de recibirlo. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Cifrado durante el tránsito con recursos compartidos de archivos de Azure

Para más información sobre firmas de acceso compartido, consulte [Uso de firmas de acceso compartido (SAS)](../storage-dotnet-shared-access-signature-part-1.md) . Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](../blobs/storage-manage-access-to-resources.md) y [autenticación para servicios de almacenamiento de Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) para obtener más información sobre la cuenta de almacenamiento de tooyour un acceso seguro.

Para obtener más información acerca de cómo proteger su cuenta de almacenamiento y el cifrado, vea hello [Guía de seguridad de almacenamiento de Azure](storage-security-guide.md).

## <a name="replication"></a>Replicación

En orden tooensure que los datos sean duraderos, el almacenamiento de Azure tiene Hola capacidad tookeep (y administrar) varias copias de los datos. Esto se denomina replicación o, a veces, redundancia. Al configurar la cuenta de almacenamiento, seleccione el tipo de replicación. En la mayoría de los casos, puede modificar esta configuración después de configura la cuenta de almacenamiento de Hola. 

Todas las cuentas de almacenamiento tienen **almacenamiento con redundancia local (LRS)**. Esto significa que tres copias de los datos administrados por el almacenamiento de Azure en el centro de datos de hello especificado cuando se configuró la cuenta de almacenamiento de Hola. Cuando los cambios son tooone confirmar copiar, otros dos copias hello se actualizan una antes de devolver el correcto. Esto significa que las tres réplicas de hello siempre están sincronizadas. Además, Hola tres copias residen en dominios de error independientes y dominios de actualización, lo que significa que los datos están disponibles incluso si se produce un error en un nodo de almacenamiento que contiene los datos o se actualiza tomada toobe sin conexión. 

**Almacenamiento con redundancia local (LRS)**

Como se explicó anteriormente, con el almacenamiento con redundancia local tiene tres copias de los datos en un único centro de datos. Esto controla el problema de Hola de datos pase a ser no está disponible si un nodo de almacenamiento se produce un error o se realiza sin conexión toobe actualizado, pero no Hola caso de todo un centro de datos pase a ser no está disponible.

**Almacenamiento con redundancia de zona (ZRS)**

Almacenamiento con redundancia de zona (ZRS) mantiene tres copias locales Hola de los datos, así como otro conjunto de tres copias de los datos. Hello segundo conjunto de tres copias se replica de forma asincrónica en centros de datos dentro de una o dos regiones. Tenga en cuenta que ZRS solo está disponible para los blobs en bloques de cuentas de almacenamiento de uso general. Además, una vez que ha creado la cuenta de almacenamiento y selecciona ZRS, no se puede convertir toouse tooany otro tipo de replicación, o viceversa.

Las cuentas de ZRS proporcionan mayor durabilidad que LRS, pero las cuentas con ZRS no tienen métricas ni la funcionalidad de registro. 

**Almacenamiento con redundancia geográfica (GRS)**

Almacenamiento con redundancia geográfica (GRS) mantiene tres copias locales Hola de los datos en una región principal y otro conjunto de tres copias de los datos en una región secundaria a cientos de millas fuera de la región principal de Hola. En caso de hello de un error en la región principal de hello, se producirá un error de almacenamiento de Azure a través de la región secundaria toohello. 

**Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).** 

Almacenamiento con redundancia geográfica con acceso de lectura es exactamente igual que GRS salvo que obtendrá datos toohello de acceso de lectura en la ubicación secundaria Hola. Si el centro de datos principal de hello deja de estar disponible temporalmente, puede continuar datos de hello tooread desde la ubicación secundaria Hola. Esto puede resultar muy útil. Por ejemplo, podría tener una aplicación web que cambia en modo de solo lectura y señala toohello copia secundaria, algunos acceso aunque no haya actualizaciones disponibles. 

> [!IMPORTANT]
> Puede cambiar cómo los datos se replican una vez creada la cuenta de almacenamiento, a menos que especifique ZRS cuando se creó la cuenta de hello. Sin embargo, tenga en cuenta que puede conllevar una coste si se cambia de LRS tooGRS o RA-GRS de transferencia de datos adicionales de un solo uso.
>

Para más información sobre la replicación, consulte [Azure Storage replication](storage-redundancy.md) (Replicación de Azure Storage).

Para obtener información de recuperación ante desastres, consulte [qué toodo si se produce una interrupción de almacenamiento de Azure](storage-disaster-recovery-guidance.md).

Para obtener un ejemplo de cómo tooleverage RA-GRS almacenamiento tooensure lograr alta disponibilidad, vea [diseñar aplicaciones altamente disponibles con RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transferencia de datos tooand de almacenamiento de Azure

Puede usar hello AzCopy utilidad de línea de comandos toocopy datos de blob y archivos dentro de su cuenta de almacenamiento o a través de las cuentas de almacenamiento. Vea uno de los siguientes Hola artículos de ayuda:

* [Transfer data with AzCopy for Windows](storage-use-azcopy.md) (Transferencia de datos con AzCopy en Windows)
* [Transfer data with AzCopy for Linux](storage-use-azcopy-linux.md) (Transferencia de datos con AzCopy en Linux)

AzCopy se basa en hello [biblioteca de movimiento de datos de Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), que está disponible actualmente en vista previa.

Hola servicio de importación y exportación de Azure puede ser usado tooimport o exportar grandes cantidades de tooor de datos de blob de la cuenta de almacenamiento. Preparar y combinar varios centros de datos de Azure de tooan de unidades de disco duro, donde se transfieren los datos de Hola de unidades de disco duro de Hola y devuelva los discos duros de hello tooyou. Para obtener más información acerca de hello servicio de importación/exportación, consulte [usar Hola servicio de importación y exportación de Microsoft Azure tooTransfer datos tooBlob almacenamiento](../storage-import-export-service.md).

## <a name="pricing"></a>Precios

Para obtener información detallada sobre los precios para el almacenamiento de Azure, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>API, bibliotecas y herramientas de Storage
Es posible acceder a los recursos de Azure Storage por medio de cualquier lenguaje que pueda realizar solicitudes HTTP/HTTPS. Además, ofrece bibliotecas de programación para varios lenguajes de amplio uso. Estas bibliotecas simplifican muchos aspectos relacionados con el uso de Azure Storage, ya que abordan detalles como la invocación sincrónica y asincrónica, el procesamiento por lotes de las operaciones, la administración de excepciones, los reintentos automáticos y el comportamiento operativo, entre otros. Bibliotecas están actualmente disponibles para hello siguientes lenguajes y plataformas, con otras personas en Hola canalización:

### <a name="azure-storage-data-services"></a>Servicios de datos de Azure Storage
* [API de REST de servicios de almacenamiento](/rest/api/storageservices/)
* [Biblioteca de cliente de Storage para .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Biblioteca de cliente de almacenamiento para C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteca de cliente de Storage para Java/Android](https://azure.microsoft.com/develop/java/)
* [Biblioteca de cliente de Storage para Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteca de cliente de Storage para PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteca de cliente de Storage para Python](https://azure.microsoft.com/develop/python/)
* [Biblioteca de cliente de Storage para Ruby](https://azure.microsoft.com/develop/ruby/)
* [Cmdlets de Storage para PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Comandos de Storage para la CLI 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Pasos siguientes

* [Más información sobre Blob Storage](../blobs/storage-blobs-introduction.md)
* [Más información sobre File Storage](../storage-files-introduction.md)
* [Más información sobre Queue Storage](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Para administradores
* [Usar Azure PowerShell con Azure Storage](storage-powershell-guide-full.md)
* [Uso de la CLI de Azure con Azure Storage](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Para desarrolladores de .NET
* [Introducción a Azure Blob Storage mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Introducción a Azure Table Storage mediante .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introducción a Azure Queue Storage mediante .NET](../storage-dotnet-how-to-use-queues.md)
* [Introducción a Azure File Storage en Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Para desarrolladores de Java/Android
* [¿Cómo toouse almacenamiento de blobs desde Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [¿Cómo toouse almacenamiento de cola en Java](../storage-java-how-to-use-queue-storage.md)
* [¿Cómo toouse almacenamiento de archivos de Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Para desarrolladores de Node.js
* [¿Cómo toouse almacenamiento de blobs de Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [¿Cómo toouse almacenamiento de cola de Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Para desarrolladores de PHP
* [¿Cómo toouse almacenamiento de blobs de PHP](../blobs/storage-php-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de tablas de PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [¿Cómo toouse almacenamiento de cola de PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Para desarrolladores de Ruby
* [¿Cómo toouse almacenamiento de blobs de Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [¿Cómo toouse Queue storage from. Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Para desarrolladores de Python
* [¿Cómo toouse almacenamiento de blobs de Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de tablas de Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [¿Cómo toouse almacenamiento de cola de Python](../storage-python-how-to-use-queue-storage.md)   
* [¿Cómo toouse almacenamiento de archivos de Python](../storage-python-how-to-use-file-storage.md) 
-->