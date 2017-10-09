---
title: aaaIntroduction tooAzure almacenamiento de archivo | Documentos de Microsoft
description: "Información general del almacenamiento de archivos de Azure, un servicio que permite toocreate y use red el archivo de recursos compartidos de hello mediante estándar del sector Hola de nube de Microsoft."
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introducción tooAzure almacenamiento de archivos
Almacenamiento de archivos de Azure ofrece recursos compartidos de archivos de red de la nube de hello mediante estándar del sector hello [protocolo de bloque de mensajes del servidor (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) y [sistema de archivos Internet comunes (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Los recursos compartidos de archivos de Azure se pueden montar de modo concurrente por los clientes, como las implementaciones locales de Windows, Mac OS y Linux o Azure Virtual Machines. Proporciona de cuenta de almacenamiento general acceso tooAzure almacenamiento de archivos y otros servicios, como Blobs, discos de máquina virtual de Azure, las colas en una sola cuenta.



## <a name="videos"></a>Vídeos
| Introducción a Azure File Storage (27 minutos) | Tutorial de Azure File Storage (5 minutos)  |
|-|-|
| [![ScreenCap de vídeo de almacenamiento de introducción a Azure archivo hello: haga clic en tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![ScreenCap hello Azure del almacenamiento de archivos Tutorial: haga clic en tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>¿Por qué es útil Azure File Storage?
Almacenamiento de archivos de Azure permite tooreplace Windows Server, Linux, o servidores de archivos de NAS hospedan en local o en la nube de hello con un archivo de nube sin SO compartan. Esto tiene Hola siguientes ventajas:

* **Acceso compartido:**. Protocolo SMB estándar, lo que significa que puede reemplazar perfectamente los recursos compartidos de archivos de local con recursos compartidos de archivos de Azure sin preocuparse de compatibilidad de aplicaciones del sector Hola compatibilidad con uso compartido de archivos de Azure. Ser capaz de tooshare un sistema de archivos entre varios equipos, aplicaciones o instancias es una ventaja importante de almacenamiento de archivos de Azure para las aplicaciones que necesitan la posibilidad de compartir. 
* **Completamente administrado**. Se pueden crear recursos compartidos de archivos Azure sin hardware de hello necesidad toomanage o un sistema operativo. Esto significa que no tiene toodeal con revisión de SO de servidor de Hola a las actualizaciones de seguridad críticas o reemplazar los discos duros defectuosos.
* **Herramientas y Scripting**. Cmdlets de PowerShell y la CLI de Azure pueden ser usado toocreate, monte y administrar recursos compartidos de almacenamiento de archivos como parte de la administración de Hola de aplicaciones de Azure. Puede crear y administrar recursos compartidos de archivos de Azure mediante el Portal de Azure y el Explorador de almacenamiento de Azure. 
* **Resistencia**. Almacenamiento de archivos de Azure se ha generado desde Hola masa seguridad toobe siempre está disponible. Reemplazar los recursos compartidos de archivos local con archivos de Azure almacenamiento significa que ya no tiene toowake una toodeal con problemas de red o interrupciones del suministro eléctrico local. 
* **Programación amigable**. Aplicaciones que se ejecutan en Azure pueden tener acceso a datos en el recurso compartido de Hola a través de archivo [sistema I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx). Por lo tanto, los desarrolladores pueden aprovechar sus aplicaciones existentes de conocimientos toomigrate y el código existentes. Además tooSystem las API de E/S, puede usar [bibliotecas de cliente de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) o hello [API de REST de almacenamiento de Azure](/rest/api/storageservices/file-service-rest-api).

Los recursos compartidos de archivos de Azure se pueden usar para:

* **Reemplazar servidores de archivos locales**:  
    Almacenamiento de archivos de Azure puede ser toocompletely usa recursos compartidos de archivos de reemplazo en servidores de archivos local tradicional o dispositivos NAS. Sistemas operativos como Windows, Mac OS y Linux fácilmente puede montar un recurso compartido de archivos de Azure estén donde estén en Hola a todos.

* **Aplicaciones "Levantar y mover"**:  
    Almacenamiento de archivos de Azure facilita demasiado "Levantar y mover" aplicaciones toohello en la nube que utilicen el archivo local comparte datos tooshare entre las partes de la aplicación hello. toomake esto ocurre, cada máquina virtual conecta a recurso compartido de archivos de toohello y, a continuación, puede leer y escribir archivos tal como haría en un archivo local recurso compartido.

* **Simplificar el desarrollo en la nube**:  
    Almacenamiento de archivos de Azure puede utilizarse en un número de proyectos de desarrollo de maneras diferentes toosimplify nueva en la nube.
    * **Configuración de aplicaciones compartida**:  
        Un patrón común para las aplicaciones distribuidas es toohave archivos de configuración en una ubicación centralizada donde puede tener acceso desde muchas máquinas virtuales diferentes. Estos archivos de configuración ahora se pueden almacenar en un recurso compartido de archivos de Azure para que lo lean todas las instancias de la aplicación. Esta configuración también se puede administrar a través de la interfaz REST de hello, que permite el acceso en todo el mundo toohello los archivos de configuración.

    * **Recurso compartido de diagnóstico**:  
        Un recurso compartido de archivos de Azure también puede ser archivos de diagnóstico de toosave usado como registros, métricas y volcados de memoria. Si se dispone de estos a través de SMB de Hola y de interfaz REST permite que aplicaciones toobuild o aprovechar una variedad de herramientas de análisis para procesar y analizar datos de diagnóstico de Hola.

    * **Desarrollo, pruebas y depuración**:  
        Cuando los desarrolladores o los administradores trabajan en máquinas virtuales en la nube de hello, que a menudo necesitan un conjunto de herramientas o utilidades. La instalación y distribución de estas utilidades en cada una de las máquinas virtuales en las que se necesiten requiere mucho tiempo. Con el almacenamiento de archivos de Azure, un desarrollador o administrador puede almacenar sus herramientas favoritas en un recurso compartido de archivos, que puede ser fácilmente conectado toofrom cualquier máquina virtual.
        
## <a name="how-does-it-work"></a>¿Cómo funciona?
La administración de recursos compartidos de archivos de Azure es mucho más simple que la administración de recursos compartidos de archivos en local. Hola siguiente diagrama muestra construcciones de administración de almacenamiento de archivos de Azure hello:

![Estructura de archivos](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Cuenta de almacenamiento**: todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Consulte Objetivos de escalabilidad y rendimiento del almacenamiento de Azure para obtener información sobre la capacidad de la cuenta de almacenamiento.
* **Recurso compartido:** un recurso compartido de almacenamiento de archivos es un recurso compartido de archivos de SMB en Azure. Todos los directorios y archivos se deben crear en un recurso compartido principal. Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, la capacidad total de 5 TB toohello Hola recurso compartido de archivos.
* **Directorio:** una jerarquía de directorios opcional.
* **Archivo**: un archivo en el recurso compartido de Hola. Puede ser un archivo up too1 TB de tamaño.
* **Formato de dirección URL**: archivos son direccionables mediante Hola siguiendo el formato de dirección URL:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Pasos siguientes
* [Creación de un recurso compartido de archivos de Azure](storage-file-how-to-create-file-share.md)
* [Conexión y montaje en Windows](storage-file-how-to-use-files-windows.md)
* [Conexión y montaje en Linux](storage-how-to-use-files-linux.md)
* [Conexión y montaje en macOS](storage-file-how-to-use-files-mac.md)
* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Artículos y vídeos conceptuales
* [Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Compatibilidad de herramientas con Azure File Storage
* [Usar Azure PowerShell con Almacenamiento de Azure](storage-powershell-guide-full.md)
* [Cómo toouse AzCopy con almacenamiento de Microsoft Azure](storage-use-azcopy.md)
* [Uso de hello CLI de Azure con el almacenamiento de Azure](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Publicaciones de blog
* [El almacenamiento de archivos de Azure ya está disponible de manera general](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [En el interior de Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migración de datos tooAzure archivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referencia
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referencia de la API REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
