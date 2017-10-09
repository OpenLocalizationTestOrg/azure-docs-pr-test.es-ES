---
title: "aaaOverview de SQL Server en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorun completa ediciones de SQL Server en máquinas virtuales de Azure. Obtener imágenes de VM de SQL Server tooall de vínculos directos y contenido relacionado."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Información general de SQL Server en máquinas virtuales de Azure
En este tema se describe las opciones para ejecutar SQL Server en máquinas virtuales (VM), Azure junto con [vincula imágenes tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) y una visión general de [tareas comunes](#manage-your-sql-vm).

> [!NOTE]
> Si ya está familiarizado con SQL Server y simplemente desea toosee toodeploy una VM de SQL Server, vea [aprovisionar una máquina virtual de SQL Server en el portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Información general
Si eres un administrador de base de datos o un programador, máquinas virtuales de Azure proporcionan una manera toomove su SQL Server de local las cargas de trabajo y aplicaciones toohello en la nube. Hello vídeo siguiente proporciona una descripción general técnica de Azure VM de SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hola vídeo cubre Hola siguientes áreas:

| Hora | Ámbito |
| --- | --- |
| 00:21 |¿Qué son las máquinas virtuales de Azure? |
| 01:45 |Seguridad |
| 02:50 |Conectividad |
| 03:30 |Rendimiento y confiabilidad del almacenamiento |
| 05:20 |Tamaños de VM |
| 05:54 |Alta disponibilidad y Acuerdo de Nivel de Servicio |
| 07:30 |Compatibilidad de configuración |
| 08:00 |Supervisión |
| 08:32 |Demostración: Creación de una máquina virtual de SQL Server 2016 |

> [!NOTE]
> Hola vídeo se centra en SQL Server 2016, pero Azure proporciona imágenes de máquina virtual en muchas versiones de SQL Server, incluido 2012, 2014 y 2016. 
> 
> 

## <a name="scenarios"></a>Escenarios
Hay muchas razones que puede elegir toohost los datos en Azure. Si la aplicación está moviendo tooAzure, mejora el rendimiento tooalso mover Hola datos. Pero hay otras ventajas. Automáticamente se tiene acceso toomultiple centros de datos para una recuperación de desastres y la presencia global. datos de Hello también están muy segura y duradero.

La ejecución de SQL Server en una máquina virtual de Azure es una opción para el almacenamiento de datos relacionales en Azure. Esta es una buena opción para varios escenarios. Por ejemplo, conviene tooconfigure Hola VM de Azure como del mismo modo como máquina de SQL Server local tooan posibles. También puede toorun aplicaciones y servicios adicionales en hello mismo servidor de base de datos. Hay dos recursos principales que pueden ayudarle a plantearse aún más escenarios y consideraciones:

* [SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) proporciona información general de escenarios de hello recomendadas para utilizar SQL Server en máquinas virtuales de Azure. 
* [Selección de una opción de SQL Server en la nube: Azure SQL (PaaS) Database o SQL Server en máquinas virtuales de Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) proporciona una comparación detallada entre la ejecución de SQL Database y SQL Server en una máquina virtual.

## <a name="create-a-new-sql-vm"></a>Creación de una máquina virtual de SQL
Hello las secciones siguientes proporcionan vínculos directos toohello portal de Azure para imágenes de la Galería de máquina virtual de hello SQL Server. Función que seleccione la imagen de hello, también puede cualquier opción de pago para los costos de licencia de SQL Server en una base por minuto, o puede hacer que su propia licencia (BYOL).

Buscar una guía paso a paso para crear una nueva VM de SQL en el tutorial de hello, [aprovisionar una máquina virtual de SQL Server en el portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Además, revise hello [procedimientos recomendados para las VM de SQL Server](virtual-machines-windows-sql-performance.md), que explica cómo equipo adecuado de tooselect Hola tamaño y otro características que están disponible durante el aprovisionamiento.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Opción 1: Crear una VM de SQL con licencias por minuto
Hello tabla siguiente proporciona una matriz de las imágenes de SQL Server más recientes de hello en Galería de máquinas virtuales de Hola. Haga clic en cualquier toobegin vínculo crear una nueva VM de SQL con la versión especificada, la edición y el sistema operativo. 

> [!TIP]
> Hola toounderstand VM y precios de SQL para estas imágenes, vea [precios orientación para máquinas virtuales de Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Versión | Sistema operativo | Edition |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Además toothis lista, hay otras combinaciones de sistemas operativos y versiones de SQL Server están disponibles. Buscar otras imágenes a través de una búsqueda de marketplace en hello portal de Azure. 

## <a id="BYOL"></a> Opción 2: Crear una VM de SQL con una licencia ya existente
También puede traer su propia licencia (BYOL). En este escenario, solo se paga por hello VM sin los cargos adicionales para la licencia de SQL Server. toouse su propia licencia, use Hola matriz de versiones de SQL Server, ediciones y los sistemas operativos siguientes. En el portal de hello, estos nombres de imagen van precedidos de **{BYOL}**.

> [!TIP]
> Aportar su propia licencia puede ahorrar dinero con el tiempo en cargas de trabajo de producción continuas. Para más información, consulte [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Orientación de precios de máquinas virtuales de SQL Server en Azure).

| Versión | Sistema operativos | Edition |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Además toothis lista, hay otras combinaciones de sistemas operativos y versiones de SQL Server están disponibles. Buscar otras imágenes a través de una búsqueda de marketplace en hello portal de Azure (busque "{BYOL} SQL Server").

> [!IMPORTANT]
> imágenes de toouse BYOL VM, debe tener un contrato Enterprise con [movilidad de licencias a través de Software Assurance en Azure](https://azure.microsoft.com/pricing/license-mobility/). También necesita una licencia válida de Hola o edición de la versión de SQL Server que desee toouse. Debe [proporcionar Hola necesarios BYOL información tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) en **10** días de aprovisionamiento de la máquina virtual. 

> [!NOTE]
> No es hello toochange posible su propia licencia de modelo de un toouse de VM de SQL Server de pago por minuto de licencias. En este caso, debe crear una nueva VM BYOL y migrar su toohello de bases de datos nueva máquina virtual. 

## <a name="manage-your-sql-vm"></a>Administración de la máquina virtual de SQL
Después de aprovisionar la máquina virtual de SQL Server, hay varias tareas de administración opcionales. En muchos aspectos, SQL Server se configura y se administra exactamente igual que si se tratara de una instancia local. Sin embargo, algunas tareas son tooAzure específico. Hello siguientes secciones destacan algunas de estas áreas con la información de toomore de vínculos.

### <a name="connect-toohello-vm"></a>Conectar toohello VM
Uno de los pasos de administración más sencilla de hello es tooconnect tooyour VM de SQL Server a través de herramientas, como SQL Server Management Studio (SSMS). Para obtener instrucciones sobre cómo tooconnect tooyour nuevo SQL Server VM, consulte [conectar tooa Máquina Virtual de SQL Server en Azure](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Migración de los datos
Si tiene una base de datos existente, es conveniente toomove ese toohello recién aprovisionados VM de SQL. Para obtener una lista de opciones de migración e instrucciones, consulte [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Configuración para alta disponibilidad
Si requiere alta disponibilidad, considere la posibilidad de configurar grupos de disponibilidad de SQL Server. Esto implica varias máquinas virtuales de Azure en una red virtual. Hola portal de Azure tiene una plantilla que configura esta configuración automáticamente. Para más información, consulte [Configuración de un grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Si desea toomanually configurar el grupo de disponibilidad y el agente de escucha asociado, consulte [configurar grupos de disponibilidad AlwaysOn en Azure VM](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Para otras consideraciones sobre alta disponibilidad, consulte [Alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Realización de una copia de seguridad de los datos
Máquinas virtuales de Azure pueden aprovechar las ventajas de [copia de seguridad automatizada](virtual-machines-windows-sql-automated-backup.md), que crea periódicamente copias de seguridad de su almacenamiento de tooblob de base de datos. También puede utilizar esta técnica manualmente. Para más información, consulte [Uso de Azure Storage para la copia de seguridad y la restauración de SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Para obtener información general sobre las opciones de copia de seguridad y restauración, consulte [Copias de seguridad y restauración para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Automatización de las actualizaciones
Pueden usar máquinas virtuales de Azure [aplicación de revisiones automatizada](virtual-machines-windows-sql-automated-patching.md) tooschedule una ventana de mantenimiento para instalar importantes de windows y SQL Server se actualiza automáticamente.

### <a name="customer-experience-improvement-program-ceip"></a>Programa para la mejora de la experiencia del usuario (CEIP)
Hola programa de mejora de experiencia del usuario (CEIP) está habilitada de forma predeterminada. Este método cada cierto envía informes tooMicrosoft toohelp mejorar SQL Server. No hay ninguna tarea de administración necesaria con CEIP a menos que desee toodisable después de aprovisionamiento. Puede personalizar o deshabilitar Hola CEIP mediante la conexión toohello máquina virtual con Escritorio remoto. A continuación, ejecute hello **informes de uso y errores de SQL Server** utilidad. Siga Hola instrucciones toodisable reporting. 

Para obtener más información, consulte la sección CEIP de Hola Hola [Aceptar los términos de licencia](https://msdn.microsoft.com/library/ms143343.aspx) tema. 

## <a name="next-steps"></a>Pasos siguientes

Si tiene preguntas sobre los precios, consulte [precios orientación para máquinas virtuales de Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md) hello y [Azure página de precios](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Seleccione la edición de destino de SQL Server en hello **OS/Software** lista. A continuación, ver los precios de Hola para máquinas virtuales de tamaños diferentes.

¿Más preguntas? En primer lugar, vea hello [preguntas más frecuentes de Azure máquinas virtuales de SQL Server](virtual-machines-windows-sql-server-iaas-faq.md). Pero también agregar la parte inferior toohello de preguntas o comentarios de cualquier toointeract de temas de VM de SQL con la Comunidad de Microsoft y Hola.
