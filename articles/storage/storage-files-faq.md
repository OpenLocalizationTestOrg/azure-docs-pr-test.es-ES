---
title: "aaaFrequently preguntas más frecuentes sobre el almacenamiento de archivos de Azure | Documentos de Microsoft"
description: "Encuentre respuestas toofrequently preguntas más frecuentes sobre el almacenamiento de archivos de Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Preguntas más frecuentes sobre Azure File Storage

## <a name="general"></a>General
* **P. ¿Qué es Azure File Storage?**  
   
    Azure File Storage es un sistema de archivos distribuido de Azure. Proporciona una interfaz de protocolo SMB que permite que los usuarios toomount Hola almacenamiento como un recurso compartido de nativo en Máquina Virtual de Azure admitidas o máquina local.

* **P. ¿Por qué es útil Azure File Storage?**  
   
    Azure File Storage proporciona acceso a datos compartidos por varias máquinas virtuales y plataformas. Consulte demasiado[el almacenamiento de archivos de Azure por qué es útil](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **P. ¿Cuándo debo usar Azure Files en lugar de Azure Blobs o Azure Disks?**  
   
    Microsoft Azure proporciona varias maneras de toostore y acceso a datos en la nube de Hola.  
   
    Almacenamiento de Azure archivo - proporciona una interfaz SMB, las bibliotecas de cliente y una interfaz REST que permite un fácil acceso desde cualquier lugar toostored archivos.  
   
    Azure Blobs: proporciona bibliotecas de cliente y una interfaz REST que permite que los datos no estructurados toobe almacenados y acceder a él a gran escala en los blobs en bloques.  
   
    Datos de Azure discos: proporciona bibliotecas de cliente y una interfaz REST que permite datos toobe almacenado de forma persistente y acceder desde un disco duro virtual conectado.  
   
    Obtenga más información en [decidir cuando toouse Blobs de Azure, archivos de Azure o discos de datos de Azure](storage-decide-blobs-files-disks.md)

* **P. ¿Cómo puedo empezar a usar Azure File Storage?**  
   
    Para empezar, puede crear un recurso compartido de Azure File. Puede crear recursos compartidos de archivos de Azure mediante Portal de Azure, los cmdlets de PowerShell de almacenamiento de Azure de hello, bibliotecas de cliente de almacenamiento de Azure de Hola u Hola API de REST de almacenamiento de Azure. En este tutorial, obtendrá información sobre:

    * [Obtenga información acerca de cómo toocreate archivos de Azure compartir el uso de hello Portal](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Obtenga información acerca de cómo toocreate archivos de Azure compartir con Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Obtenga información acerca de cómo toocreate archivos de Azure compartir con CLI](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **P. ¿Qué replicaciones admite Azure File Storage?**  
   
    Por ahora, Azure File Storage solo admite LRS y GRS. Tenemos previsto toosupport RA-GRS, pero todavía no hay ningún tooshare de escala de tiempo.

## <a name="security-authentication-and-access-control"></a>Seguridad, autenticación y control de acceso

* **P. Qué son los archivos de tooaccess de maneras diferentes en el almacenamiento de archivos de Azure**
    
    Puede montar el recurso compartido de archivos de hello en el equipo local mediante el protocolo SMB 3.0 o usar herramientas como [Explorador de almacenamiento](http://storageexplorer.com/) tooaccess archivos en el recurso compartido de archivos. Desde su aplicación, puede utilizar las bibliotecas de cliente de almacenamiento, las API de REST o tooaccess Powershell que compartan los archivos en archivos de Azure.

* **P. ¿Cómo puedo proporcionan acceso tooa determinado archivo con un explorador web?**
    
    Con SAS se pueden generar tokens con permisos específicos que son válidos durante un intervalo de tiempo determinado. Por ejemplo, puede generar un token con el archivo en particular tooa acceso de solo lectura para un período de tiempo específico. Cualquier persona que posee esta dirección url puede tener acceso a archivo hello directamente desde cualquier explorador web mientras es válido. Las claves SAS se pueden generar fácilmente desde una interfaz de usuario, como el Explorador de Storage.

* **P. ¿Es posible toospecify permisos de solo lectura o de solo escritura en carpetas de recurso compartido de hello?**
    
    No tiene este nivel de control sobre los permisos si va a montar Hola de recurso compartido de archivos a través de SMB. Sin embargo, puede conseguirlo mediante la creación de una firma de acceso compartido (SAS) a través de la API de REST de Hola o bibliotecas de cliente.  

* **P. ¿Cómo se puede habilitar el cifrado del lado del servidor en Azure File Storage?**

    El [cifrado del lado del servidor](storage-service-encryption.md) para Azure File Storage se encuentra disponible con carácter general en todas las regiones y nubes públicas y nacionales. Puede habilitar el cifrado del lado del servidor para Azure File Storage mediante [Azure Portal](https://portal.azure.com/), la [API del proveedor de recursos de Microsoft Azure Storage](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) o la [CLI de Azure](storage-azure-cli.md).
    
    Después de habilitar SSE en almacenamiento de archivos de Azure, se cifrará automáticamente los datos nuevos escritos toohello el almacenamiento de archivos en esa cuenta de almacenamiento. Esta característica está disponible para todos los datos nuevos escritos tooexisting o nuevos recursos compartidos en una cuenta de almacenamiento nueva o existente. No se aplica ningún cargo adicional por habilitar esta característica. Obtenga más información en [cómo tooenable SSE en almacenamiento de Azure archivos](storage-service-encryption.md).

* **P. ¿Azure File Storage admite la autenticación basada en Active Directory?**
   
    En la actualidad no se admite la autenticación basada en AD ni las ACL, pero se admitirá en un futuro cercano. Por ahora, las claves de cuenta de almacenamiento de Azure Hola son recurso compartido de archivos de toohello de tooprovide usa la autenticación. Se ofrece una solución mediante firmas de acceso compartido (SAS) a través de bibliotecas de cliente de API de REST u Hola Hola. Con SAS se pueden generar tokens con permisos específicos que son válidos durante un intervalo de tiempo determinado. Por ejemplo, puede generar un token con tooa de acceso de solo lectura tiene el archivo con la expiración de 10 minutos. Cualquier persona que posee este token mientras es válido tiene el archivo de toothat de acceso de solo lectura para los 10 minutos.
   
    SAS solo se admite a través de bibliotecas de cliente o la API de REST de Hola. Cuando monte Hola de recurso compartido de archivos a través del protocolo SMB hello, no puede usar un contenido de tooits SAS toodelegate acceso. 
    
* **P. ¿Cuáles son las directivas de cumplimiento de datos Hola compatibles para almacenar archivos de Azure?**

   Almacenamiento de archivos de Azure se ejecuta en la parte superior de Hola misma arquitectura de almacenamiento como otro tipo de almacenamiento de servicios de almacenamiento de Azure y aplica Hola mismas directivas de cumplimiento de normas de datos. Obtener más información sobre la conformidad de datos de almacenamiento de Azure, puede descargar y consulte demasiado[documento de protección de datos de Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Acceso local

* **¿Q.Do tengo almacenamiento toouse ExpressRoute de Azure tooconnect tooAzure archivos desde una máquina virtual local?**
   
    No. Si no dispone de ExpressRoute, puede acceder Hola recurso compartido de archivos desde el entorno local siempre y cuando tenga el puerto 445 (TCP de salida) abierto para acceso a Internet. Pero si está interesado en hacerlo, puede usar ExpressRoute con Azure File Storage.

* **P. ¿Cómo puedo montar un recurso compartido de Azure File en mi máquina local?** 
    
    Puede montar Hola de recurso compartido de archivos a través del protocolo SMB Hola mientras está abierto el puerto 445 (TCP de salida) y el cliente es compatible con el protocolo de SMB 3.0 hello (por ejemplo, que está utilizando Windows 10 o Windows Server 2012). Trabaje con su ISP proveedor toounblock Hola el puerto local. Hola provisional, puede ver los archivos con [Explorador de almacenamiento](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Precios y facturación
* **P. ¿Hola tráfico de red entre una máquina virtual de Azure y un número de recurso compartido de archivos como el ancho de banda externo que se cobra toohello suscripción?**
   
    Si el recurso compartido de archivos de Hola y máquinas virtuales están en Hola misma región de Azure, hello tráfico entre ellas es gratuito. Si se encuentran en regiones diferentes, se cobrará como externos de ancho banda tráfico Hola entre ellos.

## <a name="backup"></a>Backup

* **P. ¿Cómo puedo realizar una copia de seguridad de mi recurso compartido de Azure Files?**
    
    Puede usar AzCopy, RoboCopy o una herramienta de copia de seguridad de terceros que pueda hacer una copia de seguridad de un recurso compartido de archivos montado. Esperamos que las instantáneas de capacidad tootake Hola de toohave de recursos compartidos de archivos en hello próximas; será capaz de toouse compartir de esta característica toobackup el archivo de Azure.

## <a name="performance"></a>Rendimiento

* **P. ¿Cuáles son los límites de escala de Hola de almacenamiento de archivos de Azure?**
    Para obtener información sobre los objetivos de escalabilidad y rendimiento de Azure File Storage, vea [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **P. Mi rendimiento resultó lenta al tratar de toounzip archivos en el almacenamiento de archivos de Azure. ¿qué debo hacer?**
    
    tootransfer un gran número de archivos en el almacenamiento de archivos de Azure, se recomienda encarecidamente usar AzCopy (Windows, vista previa para Unix/Linux) o Powershell de Azure, estas herramientas se han optimizado para la transferencia de red.

* **P. ¿Cuál ha sido revisiones publicadas toofix problema de rendimiento lento con almacenamiento de archivos de Azure?**
    
    el equipo de Windows Hello publicó recientemente una toofix revisión un problema de rendimiento lento cuando el cliente de hello tiene acceso a almacenamiento de archivos de Azure de Windows 8.1 o Windows Server 2012 R2. Para obtener más información, póngase desprotección Hola asociados artículo de Knowledge Base [ralentizar el rendimiento cuando se tiene acceso a almacenamiento de archivos de Azure desde Windows 8.1 o Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Características e interoperabilidad con otros servicios
* **P. ¿Es un "testigo de recurso compartido de archivos" para un clúster de conmutación por error puede ser de hello casos de uso para almacenar archivos de Azure?**
   
    Actualmente no se admite.

* **P. ¿Hay una operación de cambio de nombre en hello API de REST?**
   
    De momento, no.

* **P. ¿Es posible tener recursos compartidos anidados, es decir, un recurso compartido en un recurso compartido?**
    
    No. recurso compartido de archivos de Hello es controlador virtual Hola que se puede montar, por lo que no se admiten recursos compartidos anidados.

* **P. ¿Cómo se usa Azure File Storage con IBM MQ?**
    
    IBM ha lanzado a un clientes MQ de IBM tooguide documento al configurar el almacenamiento de archivos de Azure con su servicio. Para obtener más información, consulte la [cómo el Administrador de cola con el servicio de archivo de Microsoft Azure de la instancia de toosetup múltiple de MQ de IBM](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Solución de problemas
* **P. ¿Cómo se pueden solucionar los errores de Azure File Storage?**
    
    Puede hacer referencia demasiado[artículo de solución de problemas de almacenamiento de archivos de Azure](storage-troubleshoot-file-connection-problems.md) para obtener instrucciones para solucionar problemas de-to-end. 


## <a name="see-also"></a>Otras referencias
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

### <a name="conceptual-articles-and-videos"></a>Artículos y vídeos conceptuales
* [Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [¿Cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Compatibilidad de herramientas con el almacenamiento de archivos
* [Usar Azure PowerShell con Almacenamiento de Azure](storage-powershell-guide-full.md)
* [Cómo toouse AzCopy con almacenamiento de Microsoft Azure](storage-use-azcopy.md)
* [Uso de hello CLI de Azure con el almacenamiento de Azure](storage-azure-cli.md)
* [Solución de problemas de Azure File Storage](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Publicaciones de blog
* [El almacenamiento de archivos de Azure ya está disponible de manera general](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [En el interior de Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrar datos tooAzure almacenamiento de archivos](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referencia
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referencia de la API REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
