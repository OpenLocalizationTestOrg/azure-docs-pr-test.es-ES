---
title: "aaaBackup y restauración para SQL Server | Documentos de Microsoft"
description: "Describe las consideraciones de copia de seguridad y restauración de bases de datos de SQL Server que se ejecutan en Máquinas virtuales de Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Copias de seguridad y restauración para SQL Server en Máquinas virtuales de Azure
## <a name="overview"></a>Información general
Almacenamiento de Azure mantiene 3 copias de cada protección contra la pérdida de datos o daños en los datos físicos tooguarantee de disco de máquina virtual de Azure. Por lo tanto, a diferencia de forma local, no es necesario tooworry acerca de estos. Sin embargo, todavía debe backup su tooprotect de bases de datos de SQL Server frente a errores de aplicación o un usuario (por ejemplo, insertar datos incorrectos o eliminar una tabla) y que se va a toorestore pueda tooa al momento dado.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Para SQL Server en máquinas virtuales de Azure, puede usar copia de seguridad original y restaurar técnicas de uso de discos conectados para destino Hola de archivos de copia de seguridad de Hola. Sin embargo, hay un toohello limitar el número de discos que puede conectar tooan máquina virtual de Azure, en función de hello [tamaño de máquina virtual de hello](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). También hay sobrecarga de Hola de tooconsider de administración de disco.

A partir de SQL Server 2014, puede realizar copias de y restaurar tooMicrosoft almacenamiento de blobs de Azure. SQL Server 2016 también proporciona mejoras para esta opción. Además, para archivos de base de datos almacenados en Almacenamiento de blobs de Microsoft Azure, SQL Server 2016 proporciona una opción para copias de seguridad prácticamente instantáneas y para restauraciones rápidas con capturas de pantalla de Azure. En este artículo se proporciona una introducción de estas opciones, y puede encontrar información adicional en [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Para obtener una explicación de las opciones de Hola para copia de seguridad de bases de datos muy grandes, consulte [estrategias de copia de seguridad de base de datos de varios terabytes SQL Server máquinas virtuales de Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Hola las siguientes secciones incluyen diferentes versiones de toohello específico de información de SQL Server compatible en una máquina virtual de Azure.

## <a name="sql-server-virtual-machines"></a>Máquinas virtuales de SQL Server
Cuando la instancia de SQL Server se ejecuta en una máquina virtual de Azure, los archivos de base de datos ya residen en discos de datos en Azure. Estos discos residen en el almacenamiento de blobs de Azure. Por lo tanto Hola motivos para realizar copias de seguridad de los enfoques de hello y base de datos que permitirán cambiar ligeramente. Tenga en cuenta Hola siguiente. 

* Ya no necesita tooperform protección de tooprovide de las copias de seguridad de bases de datos frente a errores de hardware o medios porque Microsoft Azure proporciona esta protección como parte del programa Hola a servicio de Microsoft Azure.
* Todavía necesita tooprovide protección contra errores de usuario o para fines administrativos, motivos normativos o archivarlo de tooperform bases de datos las copias de seguridad.
* Puede almacenar el archivo de copia de seguridad de hello directamente en Azure. Para obtener más información, vea Hola siguientes secciones que proporcionan instrucciones para hello distintas versiones de SQL Server.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 admite las características de [copia de seguridad y restauración mediante blobs de Azure](https://msdn.microsoft.com/library/jj919148.aspx) de SQL Server 2014. Sino que también incluye Hola siguientes mejoras:

| Mejoras de la versión de 2016 | Detalles |
| --- | --- |
| **Seccionamiento** |Cuando copia de seguridad tooMicrosoft almacenamiento de blobs de Azure, SQL Server 2016 admite la copia de seguridad toomultiple blobs tooenable copia de seguridad de bases de datos grandes, una tooa máximo de 12,8 TB. |
| **Copia de seguridad de instantáneas** |Mediante el uso de Hola de instantáneas de Azure, copia de seguridad de instantánea de archivos de SQL Server proporciona copias de seguridad casi instantáneas y restauraciones rápidas de archivos de base de datos almacenados mediante el servicio de almacenamiento de blobs de Azure de Hola. Esta función permite toosimplify las directivas de copia de seguridad y restauración. Copia de seguridad de instantáneas de archivos también es compatible con la restauración a un momento dado. Para obtener más información, vea [Copias de seguridad de instantáneas para archivos de base de datos en Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Programación de copia de seguridad administrada** |SQL Server Managed Backup tooAzure ahora es compatible con programaciones personalizadas. Para obtener más información, consulte [tooMicrosoft de SQL Server Managed Backup Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Para obtener un tutorial de capacidades de Hola de SQL Server 2016 al usar el almacenamiento de blobs de Azure, consulte [Tutorial: usar el servicio de almacenamiento de blobs de Microsoft Azure de hello con bases de datos de SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 incluye Hola siguientes mejoras:

1. **Copia de seguridad y restauración tooAzure**:
   
   * *Copia de seguridad de SQL Server tooURL* tiene ahora compatibilidad en SQL Server Management Studio. Hola opción tooback seguridad tooAzure ahora está disponible cuando se utiliza la tarea de copia de seguridad o restauración, o el Asistente para planes de mantenimiento en SQL Server Management Studio. Para obtener más información, consulte [tooURL de copia de seguridad de SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *SQL Server Managed Backup tooAzure* tiene una nueva funcionalidad que permite la administración de copia de seguridad automatizada. Esto es especialmente útil para la administración de copia de seguridad automatizada para instancias de SQL Server 2014 que se ejecuta en Máquina de Azure. Para obtener más información, consulte [tooMicrosoft de SQL Server Managed Backup Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Copia de seguridad automatizada* proporciona automatización adicionales tooautomatically permiten *tooAzure de SQL Server Managed Backup* en todas las bases de datos nuevas y existentes para una VM de SQL Server en Azure. Para obtener más información, vea [Copia de seguridad automatizada para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).
   * Para obtener información general de todas las opciones de Hola para tooAzure de copia de seguridad de SQL Server 2014, vea [SQL Server Backup and Restore con el servicio de almacenamiento de blobs de Microsoft Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Cifrado**: SQL Server 2014 es compatible con el cifrado de datos cuando se crea una copia de seguridad. Admite varios algoritmos de cifrado y hello usa osf un certificado o clave asimétrica. Para obtener más información, vea [Cifrado de copia de seguridad](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Para obtener información detallada sobre Copia de seguridad y restauración de SQL Server en SQL Server 2012, vea [Copia de seguridad y restauración de bases de datos de SQL Server (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

A partir de SQL Server 2012 SP1 actualización acumulativa 2, hacer copias de seguridad tooand restauración de hello servicio de almacenamiento de blobs de Azure. Esta mejora puede ser tooback usa seguridad de bases de datos de SQL Server en un servidor de SQL que se ejecutan en máquinas virtuales de Azure o una instancia local. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Algunas de las ventajas de Hola de usar el servicio de almacenamiento de blobs de Azure de hello son Hola capacidad toobypass Hola 16 límite de disco para los discos conectados, facilidad de administración, disponibilidad directa de Hola de instancia de tooanother del archivo de copia de seguridad de Hola de instancia de SQL Server que se ejecutan en un Azure máquina virtual o una instancia local para fines de recuperación ante desastres o de migración. Para obtener una lista completa de beneficios toousing un servicio de almacenamiento de blobs de Azure para copias de seguridad de SQL Server, vea hello *ventajas* sección [SQL Server Backup and Restore con el servicio de almacenamiento de blobs de Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Para obtener recomendaciones sobre prácticas recomendadas e información sobre solución de problemas, vea [Prácticas recomendadas de copia de seguridad y restauración (servicio de Almacenamiento de blobs de Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Para obtener información sobre Copia de seguridad y restauración de SQL Server en SQL Server 2008 R2, vea [Copia de seguridad y restauración de bases de datos en SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Para obtener información sobre Copia de seguridad y restauración de SQL Server en SQL Server 2008, vea [Copia de seguridad y restauración de bases de datos en SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Pasos siguientes
Si planea la implementación de SQL Server en una máquina virtual de Azure, puede encontrar instrucciones de aprovisionamiento en hello sigue tutorial: [aprovisionamiento de una máquina Virtual de SQL Server en Azure con el Administrador de recursos de Azure](virtual-machines-windows-portal-sql-server-provision.md).

Aunque una copia de seguridad y restauración puede ser utilizado toomigrate los datos, hay tooSQL de rutas de acceso de migración de datos potencialmente más fácil Server en una máquina virtual de Azure. Para obtener una explicación completa de opciones de migración y recomendaciones, consulte [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](virtual-machines-windows-migrate-sql.md).

Revise otros [recursos para ejecutar SQL Server en Máquinas virtuales de Azure](virtual-machines-windows-sql-server-iaas-overview.md).

