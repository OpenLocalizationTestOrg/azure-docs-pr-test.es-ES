---
title: aaaDeciding cuando toouse Blobs de Azure, archivos de Azure o discos de datos de Azure
description: "Obtener información sobre los datos de toostore y acceso de distintas maneras hello en Azure toohelp que decidir qué tecnología toouse."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: cd43abde43daf33dd7c43aa2696a9c8d5cd19612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Decidir cuándo toouse Blobs de Azure, archivos de Azure o discos de datos de Azure

Microsoft Azure proporciona varias características de almacenamiento de Azure para almacenar y tener acceso a los datos en la nube de Hola. Este artículo trata los archivos de Azure, Blobs y discos de datos y está diseñada toohelp elegir entre estas características.

## <a name="scenarios"></a>Escenarios

Hello en la tabla siguiente compara archivos, Blobs y discos de datos y muestra escenarios de ejemplo adecuado para cada uno.

| Característica | Descripción | Cuando toouse |
|--------------|-------------|-------------|
| **Archivos de Azure** | Proporciona una interfaz SMB, las bibliotecas de cliente y un [interfaz REST](/rest/api/storageservices/file-service-rest-api) que permite el acceso desde cualquier lugar toostored archivos. | Desea demasiado "Levantar y mover" una nube de toohello de aplicación que ya usa datos tooshare las API de sistema de archivos nativos de hello entre ella y otras aplicaciones que se ejecutan en Azure.<br/><br/>Se desea toostore desarrollo y herramientas de depuración que necesitan toobe acceso desde varias máquinas virtuales. |
| **Azure Blobs** | Proporciona bibliotecas de cliente y un [interfaz REST](/rest/api/storageservices/blob-service-rest-api) que permite que los datos no estructurados demasiado se almacenan y acceder a él a gran escala en los blobs en bloques. | Desea que la transmisión por secuencias de toosupport de aplicación y los escenarios de acceso aleatorio.<br/><br/>Desea que los datos de la aplicación pueda tooaccess toobe desde cualquier lugar. |
| **Azure Data Disks** | Proporciona bibliotecas de cliente y un [interfaz REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) que permite datos toobe almacenado de forma persistente y acceder desde un disco duro virtual conectado. | Desea toolift y mover aplicaciones que utilizan tooread de las API del sistema de archivos nativos y escriben toopersistent los discos de datos.<br/><br/>Desea toostore datos que no es necesario toobe tiene acceso desde el disco de hello toowhich de hello exterior máquina virtual está conectados. |

## <a name="comparison-files-and-blobs"></a>Comparación: Azure Files y Azure Blobs

Hello en la tabla siguiente compara los archivos de Azure con Blobs de Azure.  
  
||||  
|-|-|-|  
|**Atributo**|**Azure Blobs**|**Archivos de Azure**|  
|Opciones de durabilidad|LRS, ZRS y GRS (y RA-GRS para mayor disponibilidad)|LRS y GRS|  
|Accesibilidad|API de REST|API de REST<br /><br /> SMB 2.1 y SMB 3.0 (API del sistema de archivos estándar)|  
|Conectividad|API de REST: en todo el mundo|API de REST: en todo el mundo<br /><br /> SMB 2.1: dentro de región<br /><br /> SMB 3.0: en todo el mundo|  
|Extremos|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Directorios|Espacio de nombres plano|Objetos de directorio verdaderos|  
|Distingue mayúsculas de minúsculas en los nombres|Distingue mayúsculas de minúsculas|No distingue mayúsculas de minúsculas, pero las conserva|  
|Capacity|Los contenedores de too500 TB|Recursos compartidos de archivos de hasta 5 TB|  
|Rendimiento|Seguridad too60 MB/s por blob en bloques|Seguridad too60 MB/s por recurso compartido|  
|Tamaño de objeto|Seguridad de blob de too200 GB/bloque|Too1TB/archivo|  
|Capacidad facturada|En función de los bytes escritos|Según el tamaño de archivo|  
|Bibliotecas de clientes|Varios idiomas|Varios idiomas|  
  
## <a name="comparison-files-and-data-disks"></a>Comparación: Azure Files y Azure Data Disks

Azure Files complementa a Azure Data Disks. Un disco de datos solo puede ser adjunto tooone Máquina Virtual de Azure a la vez. Discos de datos están almacenados como blobs de página en el almacenamiento de Azure de discos duros virtuales de formato fijo y usan máquina virtual hello toostore los datos duraderos. Pueden tener acceso a recursos compartidos de archivos en archivos de Azure en Hola misma forma en que se tiene acceso a disco local de hello (mediante la API del sistema de archivos nativos) y se pueden compartir entre varias máquinas virtuales.  
 
Hello en la tabla siguiente compara los archivos de Azure con discos de datos de Azure.  
 
||||  
|-|-|-|  
|**Atributo**|**Azure Data Disks**|**Archivos de Azure**|  
|Scope|Máquina virtual única de tooa exclusivo|Acceso compartido entre varias máquinas virtuales|  
|Instantáneas y copia|Sí|No|  
|Configuración|Conexión al inicio de la máquina virtual de Hola|La conexión después de que ha iniciado la máquina virtual de Hola|  
|Autenticación|Característica integrada|Configurar con el uso de la red|  
|Limpieza|Automático|Manual|  
|Acceso con REST|No se pueden tener acceso a archivos dentro de hello VHD|Se puede acceder a archivos almacenados en un recurso compartido|  
|Tamaño máximo|Disco de 1 TB|Recurso compartido de archivos de 5 TB y archivo de 1 TB dentro del recurso compartido|  
|IOPS de 8 KB como máximo|500 IOPS|1000 IOPS|  
|Rendimiento|Seguridad too60 MB/s por disco|Seguridad too60 MB/s por recurso compartido de archivos|  

## <a name="next-steps"></a>Pasos siguientes

Al tomar decisiones sobre cómo se almacena y se tiene acceso a los datos, también debería considerar los costos de hello implicados. Para más información, consulte [Precios de Azure Blob Storage](https://azure.microsoft.com/pricing/details/storage/).
  
Algunas características SMB no están toohello aplicables en la nube. Para obtener más información, consulte [características no admitidas por hello servicio archivo de Azure](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Para obtener más información acerca de los discos de datos, vea [administrar discos e imágenes](../../virtual-machines/windows/about-disks-and-vhds.md) y [cómo tooAttach una máquina Virtual de Windows de disco de datos tooa](../../virtual-machines/windows/classic/attach-disk.md).
