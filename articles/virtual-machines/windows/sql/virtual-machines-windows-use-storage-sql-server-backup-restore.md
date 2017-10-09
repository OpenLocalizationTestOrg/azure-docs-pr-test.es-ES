---
title: aaaHow toouse el almacenamiento de Azure para SQL Server backup y restore | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooback seguridad tooAzure almacenamiento de SQL Server. Explica las ventajas de Hola de copia de seguridad de bases de datos SQL tooAzure almacenamiento."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Uso de Almacenamiento de Azure para la copia de seguridad y la restauración de SQL Server
## <a name="overview"></a>Información general
A partir de SQL Server 2012 SP1 CU2, ahora puede escribir copias de seguridad de SQL Server directamente toohello servicio de almacenamiento de blobs de Azure. Puede usar este tooback funcionalidad de restauración tooand desde el servicio de blobs de Azure de hello con una base de datos de SQL Server local o una base de datos de SQL Server en una máquina virtual de Azure. Copia de seguridad toocloud ofrece ventajas de disponibilidad, almacenamiento externo de replicación geográfica ilimitado y facilidad de migración de datos tooand de nube de Hola. Puede emitir instrucciones BACKUP o RESTORE mediante T-SQL o SMO.

SQL Server 2016 incorpora nuevas capacidades; Puede usar [copia de seguridad de instantánea de archivos](http://msdn.microsoft.com/library/mt169363.aspx) tooperform copias de seguridad casi instantáneas y restauraciones increíblemente rápidas.

Este tema explica por qué podría elegir toouse almacenamiento de Azure para copias de seguridad SQL y, a continuación, se describen los componentes de hello implicados. Puede usar recursos de hello final Hola de hello artículo tooaccess tutoriales y toostart información adicional con las copias de seguridad de SQL Server en este servicio.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Ventajas de usar hello servicio Blob de Azure para copias de seguridad de SQL Server
A la hora de realizar una copia de seguridad de SQL Server, se enfrenta a varias dificultades. Estos desafíos incluyen la administración de almacenamiento, el riesgo de error de almacenamiento, acceso de almacenamiento del sitio toooff y configuración de hardware. Muchos de estos desafíos se direccionan mediante el servicio de almacenamiento de blobs de Azure de Hola para copias de seguridad de SQL Server. Considere la posibilidad de hello siguientes ventajas:

* **Facilidad de uso**: almacenar las copias de seguridad en blobs de Azure puede ser una opción externa cómoda, flexible y fácil tooaccess. Creación de almacenamiento externo para las copias de seguridad de SQL Server pueden ser tan sencillo como modificar sus toouse Hola de scripts y trabajos **tooURL de copia de seguridad** sintaxis. Almacenamiento externo normalmente debe estar suficientemente alejado de tooprevent de ubicación de base de datos de producción de hello un desastre que afecte a Hola fuera de las instalaciones y ubicaciones de la base de datos de producción. Si elige demasiado[blobs de Azure de replicar geográficamente](../../../storage/common/storage-redundancy.md), tiene un nivel adicional de protección en caso de hello de un desastre que podría afectar a la región de hello todo.
* **Archivo de copia de seguridad**: Hola servicio de almacenamiento de blobs de Azure ofrece una mejor cinta alternativo toohello utilizado a menudo copias de seguridad de opción tooarchive. Almacenamiento en cinta puede requerir el transporte físico tooan fuera de las instalaciones y medidas tooprotect Hola multimedia. Almacenar las copias de seguridad en el almacenamiento de blobs de Azure ofrece una opción de archivado instantánea, altamente disponible y resistente.
* **Hardware administrado**: con los servicios de Azure no hay sobrecarga por la administración del hardware. Los servicios de Azure administran hardware de Hola y proporcionan replicación geográfica para ofrecer redundancia y protección frente a errores de hardware.
* **Almacenamiento ilimitado**: al habilitar un BLOB tooAzure de copia de seguridad directa, tendrá acceso toovirtually almacenamiento ilimitado. Como alternativa, la copia de seguridad de disco de máquina virtual de Azure tooan tiene límites basados en el tamaño de la máquina. Hay un toohello limitar el número de discos puede adjuntar tooan máquina virtual de Azure para copias de seguridad. Este límite es de 16 discos para una instancia muy grande e inferior para las instancias menores.
* **Disponibilidad de la copia de seguridad**: copias de seguridad almacenadas en blobs de Azure están disponibles desde cualquier lugar y en cualquier momento y puede ascender fácilmente a acceso a ellas para restauraciones tooeither un servidor local de SQL u otro servidor de SQL que se ejecuta en una máquina Virtual de Azure, sin Hola necesita Para adjuntar o separar de base de datos o de descargar y conectar Hola VHD.
* **Costo**: solo se paga por servicio de Hola que se usa. Puede ser tan rentable como una opción de archivado de copias de seguridad externa. Vea hello [Calculadora de precios de Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "Calculadora de precios de"), hello y [precios de Azure artículo](http://go.microsoft.com/fwlink/?LinkId=277059 "precios artículo") para obtener más información información.
* **Instantáneas de almacenamiento**: si los archivos de base de datos se almacenan en un blob de Azure y que usa SQL Server 2016, puede utilizar [copia de seguridad de instantánea de archivos](http://msdn.microsoft.com/library/mt169363.aspx) tooperform copias de seguridad casi instantáneas y restauraciones increíblemente rápidas.

Para obtener más información, consulte [Copia de seguridad y restauración de SQL Server con el servicio de almacenamiento Blob de Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

Hola siguientes dos secciones presentan el servicio de almacenamiento de blobs de Azure de hello, incluidos los componentes de SQL Server de hello necesario. Es importante toounderstand componentes de Hola su interacción toosuccessfully use backup y restore y del servicio de almacenamiento de blobs de Azure de Hola.

## <a name="azure-blob-storage-service-components"></a>Componentes del servicio de almacenamiento de blobs de Azure
Hello componentes de Azure siguientes se usan al realizar copias de seguridad toohello servicio de almacenamiento de blobs de Azure.

| Componente | Description |
| --- | --- |
| **Storage Account** |cuenta de almacenamiento de Hello es hello punto de partida para todos los servicios de almacenamiento. tooaccess un servicio de almacenamiento de blobs de Azure, primero cree una cuenta de almacenamiento de Azure. Para obtener más información acerca del servicio de almacenamiento de blobs de Azure, vea [cómo toouse hello Azure Blob Storage Service](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Contenedor** |Un contenedor ofrece la agrupación de un conjunto de blobs y puede almacenar un número ilimitado de ellos. toowrite un tooan de copia de seguridad de SQL Server servicio Blob de Azure, debe tener al menos contenedor raíz de hello creado. |
| **Blob** |Un archivo de cualquier tipo y tamaño. Los blobs son direccionables mediante Hola siguiendo el formato de dirección URL: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Para más información sobre los blobs en páginas, consulte la [descripción de los blobs en bloques y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Componentes de SQL Server
Hello siguientes componentes de SQL Server se usan al realizar copias de seguridad toohello servicio de almacenamiento de blobs de Azure.

| Componente | Description |
| --- | --- |
| **URL** |Una dirección URL especifica un archivo de copia de seguridad único del tooa identificador uniforme de recursos (URI). dirección URL de Hello es tooprovide usado Hola ubicación y el nombre del archivo de copia de seguridad de SQL Server de hello. dirección URL de Hello debe apuntar tooan blob real, no solo a un contenedor. Si el blob de hello no existe, se crea. Si un blob existente se especifica, se produce un error en la copia de seguridad, a menos que hello > se especifica la opción WITH FORMAT. Hola siguiente es un ejemplo de dirección URL de hello especificaría Hola comando de copia de seguridad: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. Se recomienda HTTPS, pero no es obligatorio. |
| **Credential:** |información de Hola que es necesario tooconnect y autenticar tooAzure servicio de almacenamiento Blob se almacena como una credencial.  En orden para tooan de copias de seguridad de SQL Server toowrite blobs de Azure o la restauración a partir de él, debe crearse una credencial de SQL Server. Para obtener más información, vea [Credencial de SQL Server](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Si elige toocopy y cargar un servicio de almacenamiento de blobs de Azure de toohello de archivo de copia de seguridad, debe utilizar un tipo de blob de página como opción de almacenamiento si tiene previsto toouse este archivo para las operaciones de restauración. RESTORE desde un tipo de blob en bloques provocará un error.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
1. Cree una cuenta de Azure si aún no tiene una. Si va a evaluar Azure, considere la posibilidad de hello [evaluación gratuita](https://azure.microsoft.com/free/).
2. A continuación, realice uno de los tutoriales que le guían en la creación de una cuenta de almacenamiento y realizar una restauración de Hola.
   
   * **SQL Server 2014**: [Tutorial: copias de seguridad de SQL Server 2014 y restauración tooMicrosoft Azure Blob Storage Service](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [Tutorial: usar el servicio de almacenamiento de blobs de Microsoft Azure de hello con bases de datos de SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Revise la documentación adicional a partir [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Si tienes algún problema, revise el tema de hello [copias de seguridad de SQL Server tooURL Best Practices and Troubleshooting](https://msdn.microsoft.com/library/jj919149.aspx).

Para ver otras opciones de copia de seguridad y restauración de SQL Server, consulte [Copias de seguridad y restauración para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

