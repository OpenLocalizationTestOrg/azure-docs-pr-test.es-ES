---
title: "configuración de aaaStorage para las máquinas virtuales de SQL Server | Documentos de Microsoft"
description: "En este tema se describe cómo Azure configura el almacenamiento para las máquinas virtuales de SQL Server durante el aprovisionamiento (modelo de implementación de Resource Manager). También se explica cómo configurar el almacenamiento para sus máquinas virtuales de SQL Server existentes."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Configuración del almacenamiento para máquinas virtuales de SQL Server
Al configurar una imagen de máquina virtual de SQL Server en Azure, Hola Portal le ayuda a tooautomate la configuración de almacenamiento. Esto incluye adjuntar almacenamiento toohello VM, hacer que ese servidor de almacenamiento accesibles tooSQL y configurar toooptimize para sus requisitos de rendimiento específicos.

Este tema explica cómo Azure configura el almacenamiento para sus máquinas virtuales de SQL Server durante el aprovisionamiento y para las máquinas virtuales existentes. Esta configuración se basa en hello [prácticas recomendadas de rendimiento](virtual-machines-windows-sql-performance.md) para máquinas virtuales de Azure que ejecuta SQL Server.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Requisitos previos
Hola toouse automatizada valores de configuración de almacenamiento, la máquina virtual requiere Hola siguientes características:

* Aprovisionada con una [imagen de la galería de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Hello usa [modelo de implementación del Administrador de recursos](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Usa [Almacenamiento premium](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Nuevas máquinas virtuales
Hello siguientes secciones se describen cómo tooconfigure almacenamiento de las nuevas máquinas virtuales de SQL Server.

### <a name="azure-portal"></a>Portal de Azure
Al aprovisionar una máquina virtual de Azure mediante una imagen de la Galería de SQL Server, puede elegir tooautomatically configurar el almacenamiento de hello para la nueva máquina virtual. Especifique el tamaño de almacenamiento de Hola y límites de rendimiento, tipo de carga de trabajo. Hello siguiente captura de pantalla muestra hoja de configuración de almacenamiento de hello usa durante la VM de SQL de aprovisionamiento.

![Configuración del almacenamiento de máquinas virtuales de SQL Server durante el aprovisionamiento](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

En función de las opciones, Azure realiza Hola después de las tareas de configuración de almacenamiento después de crear Hola VM:

* Crea y asocia la máquina virtual de toohello de discos de datos de premium almacenamiento.
* Configura Hola datos discos toobe accesible tooSQL Server.
* Configura los discos de datos de hello en el almacenamiento de un grupo en función de hello especifica requisitos de tamaño y rendimiento (IOPS y rendimiento).
* Grupo de almacenamiento de Hola se asocia con una nueva unidad en la máquina virtual de Hola.
* Optimiza esta nueva unidad en función de su tipo de carga de trabajo (almacenamiento de datos, procesamiento de transaccional o general).

Para obtener más información sobre cómo Azure define la configuración de almacenamiento, vea hello [sección de configuración de almacenamiento](#storage-configuration). Para ver un tutorial completo de cómo toocreate una VM de SQL Server en hello Portal de Azure, consulte [Hola aprovisionamiento tutorial](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Plantillas de Resource Manager
Si usas Hola siguiendo las plantillas de administrador de recursos, se adjuntan dos discos de datos premium de forma predeterminada, sin ninguna configuración de grupo de almacenamiento. Sin embargo, puede personalizar estas número de plantillas toochange Hola premium de discos de datos que se adjunta toohello virtual machine.

* [Creación de máquinas virtuales con copia de seguridad automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Creación de máquinas virtuales con la aplicación de revisión automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Creación de máquinas virtuales con la integración de AKV](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>Máquinas virtuales existentes
Para SQL Server las máquinas virtuales existentes, puede modificar algunas configuraciones de almacenamiento en hello portal de Azure. Seleccione la máquina virtual, vaya toohello área de configuración y, a continuación, seleccione Configuración de SQL Server. hoja de configuración de SQL Server de Hello muestra el uso de almacenamiento actual de hello de la máquina virtual. En este gráfico se muestran todas las unidades que existen en la máquina virtual. Para cada unidad, espacio de almacenamiento de Hola se muestra en cuatro secciones:

* Datos SQL
* Registro de SQL
* Otros (almacenamiento que no es de SQL)
* Disponible

![Configuración del almacenamiento para la máquina virtual de SQL Server existente](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure Hola tooadd una nueva unidad de almacenamiento o extender una unidad existente, haga clic en el vínculo de edición de hello encima del gráfico de Hola.

Opciones de configuración de Hola que se ven varía en función de si ha utilizado esta característica antes. Cuando se usa para hello primera vez, puede especificar los requisitos de almacenamiento para una nueva unidad. Si anteriormente usó esta toocreate característica una unidad, puede elegir tooextend almacenamiento de la unidad.

### <a name="use-for-hello-first-time"></a>Uso de hello primera vez
Si es la primera vez que usa esta característica, puede especificar los límites de tamaño y rendimiento de almacenamiento para una nueva unidad de Hola. Esta experiencia es similar toowhat que vería en tiempo de aprovisionamiento. Hola principal diferencia es que no se permite el tipo de carga de trabajo de hello toospecify. Esta restricción impide que interrumpir las configuraciones de SQL Server existentes en la máquina virtual de Hola.

![Configuración de los controles deslizantes del almacenamiento de SQL Server](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure crea una unidad en función de sus especificaciones. En este escenario, Azure realiza Hola siguiente las tareas de configuración de almacenamiento:

* Crea y asocia la máquina virtual de toohello de discos de datos de premium almacenamiento.
* Configura Hola datos discos toobe accesible tooSQL Server.
* Configura los discos de datos de hello en el almacenamiento de un grupo en función de hello especifica requisitos de tamaño y rendimiento (IOPS y rendimiento).
* Grupo de almacenamiento de Hola se asocia con una nueva unidad en la máquina virtual de Hola.

Para obtener más información sobre cómo Azure define la configuración de almacenamiento, vea hello [sección de configuración de almacenamiento](#storage-configuration).

### <a name="add-a-new-drive"></a>Incorporación de una nueva unidad
Si ya ha configurado el almacenamiento en la máquina virtual de SQL Server, al expandirlo aparecen dos nuevas opciones. Hola primera opción es tooadd una nueva unidad, lo que puede aumentar el nivel de rendimiento de saludo de la máquina virtual.

![Agregar un tooa unidad nueva VM de SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Sin embargo, después de agregar la unidad de hello, debe realizar algunos aumento de rendimiento de configuración manual adicional tooachieve Hola.

### <a name="extend-hello-drive"></a>Extienda el disco de Hola
Hola otra opción para expandir el almacenamiento es la unidad de tooextend Hola existente. Esta opción aumenta el almacenamiento disponible de hello para la unidad, pero no mejora el rendimiento. Con grupos de almacenamiento, no se puede modificar el número de Hola de columnas después de crea el grupo de almacenamiento de Hola. número de Hola de columnas determina número Hola de escrituras en paralelo, lo que puede crear bandas en discos de datos de Hola. Por lo tanto, los discos de datos agregados no pueden aumentar el rendimiento. Solo puede proporcionar más espacio de almacenamiento para datos de Hola que se escriben. Esta limitación también significa que, al extender unidad hello, número de Hola de columnas determina un mínimo de discos de datos que se pueden agregar Hola. Por lo que si crea un grupo de almacenamiento con discos de cuatro datos, Hola número de columnas también es cuatro. Cualquier momento que ampliar el almacenamiento de hello, debe agregar discos de datos al menos cuatro.

![Ampliación de una unidad para una máquina virtual de SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Configuración de almacenamiento
En esta sección se proporciona una referencia para cambios de configuración de almacenamiento de hello Azure realiza automáticamente durante el aprovisionamiento de VM de SQL o la configuración en hello Portal de Azure.

* Si ha seleccionado menos de dos TB de almacenamiento para la máquina virtual, Azure no crea ningún grupo de almacenamiento.
* Si ha seleccionado al menos dos TB de almacenamiento para la máquina virtual, Azure configura un grupo de almacenamiento. Hola siguiente sección de este tema proporcionan detalles de Hola Hola almacenamiento de información de configuración del grupo.
* La configuración automática del almacenamiento siempre utiliza discos de datos de [almacenamiento premium](../../../storage/common/storage-premium-storage.md) P30. Por lo tanto, hay una asignación 1:1 entre el número seleccionado de Terabytes y número de Hola de discos de datos adjuntos tooyour máquina virtual.

Para obtener más información, vea hello [precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage) página en hello **almacenamiento en disco** ficha.

### <a name="creation-of-hello-storage-pool"></a>Creación de grupos de almacenamiento de Hola
Azure utiliza Hola siguiente bloque de almacenamiento de configuración toocreate Hola de VM de SQL Server.

| Configuración | Valor |
| --- | --- |
| Stripe size (Tamaño de las franjas) |256 KB (almacenamiento de datos); 64 KB (transaccional) |
| Tamaños de disco |1 TB cada uno |
| Memoria caché |Lectura |
| Tamaño de la asignación |Tamaño de la unidad de asignación NTFS = 64 KB |
| Inicialización de archivo instantáneo |Enabled |
| Bloquear páginas en memoria |Enabled |
| Recuperación |Recuperación simple (sin resistencia) |
| Número de columnas |Número de discos de datos<sup>1</sup> |
| TempDB location (Ubicación de TempDB) |Almacenada en discos de datos<sup>2</sup> |

<sup>1</sup> después de crea el grupo de almacenamiento de hello, no se puede modificar el número de Hola de columnas de grupo de almacenamiento de Hola.

<sup>2</sup> esta configuración solo aplica toohello primera unidad se crea mediante la característica de configuración de almacenamiento de Hola.

## <a name="workload-optimization-settings"></a>Configuración de optimización de la carga de trabajo
Hello tabla siguiente describen Hola tres cargas de trabajo tipo opciones disponibles y sus optimizaciones correspondientes:

| Tipo de carga de trabajo | Description | Optimizaciones |
| --- | --- | --- |
| **General** |Configuración predeterminada que admite la mayoría de las cargas de trabajo |None |
| **Procesamiento transaccional** |Optimiza el almacenamiento de Hola para cargas de trabajo OLTP de base de datos tradicional |Marca de seguimiento 1117<br/>Marca de seguimiento 1118 |
| **Almacenamiento de datos** |Optimiza el almacenamiento de Hola para cargas de trabajo informes y análisis |Marca de seguimiento 610<br/>Marca de seguimiento 1117 |

> [!NOTE]
> Solo puede especificar el tipo de carga de trabajo de hello cuando aprovisiona una máquina virtual SQL, selecciónelo en el paso de configuración de almacenamiento de Hola.
>
>

## <a name="next-steps"></a>Pasos siguientes
Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-server-iaas-overview.md).
