---
title: aaaUse moderna de copia de seguridad de almacenamiento con el servidor de copia de seguridad de Azure v2 | Documentos de Microsoft
description: "Obtenga información sobre las nuevas características de hello en el servidor de copia de seguridad de Azure v2. Este artículo se describe cómo tooupgrade la instalación del servidor de copia de seguridad."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Agregar almacenamiento tooAzure v2 del servidor de copia de seguridad

Azure Backup Server v2 incluye Modern Backup Storage de System Center 2016 Data Protection Manager. Modern Backup Storage proporciona ahorros de almacenamiento de hasta el 50 por ciento, copias de seguridad que son tres veces más rápidas y un almacenamiento más eficaz. También ofrece almacenamiento con reconocimiento de la carga de trabajo. 

> [!NOTE]
> toouse moderna almacenamiento de copia de seguridad, debe ejecutar v2 del servidor de copia de seguridad en Windows Server 2016. Si ejecuta Backup Server v2 en una versión anterior de Windows Server, Azure Backup Server no puede sacar partido de Modern Backup Storage. En su lugar, protege las cargas de trabajo como lo hace con Backup Server v1. Para obtener más información, vea la versión del servidor de copia de seguridad de hello [matriz protección](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volúmenes en Backup Server v2

Backup Server v2 acepta volúmenes de almacenamiento. Al agregar un volumen, el servidor de copia de seguridad da formato a Hola volumen tooResilient sistema de archivos (ReFS), que requiere almacenamiento de copia de seguridad actual. tooadd un volumen y tooexpand que más adelante si es necesitan, se recomienda que utilice este flujo de trabajo:

1.  Configure Backup Server v2 en una máquina virtual.
2.  Cree un volumen en un disco virtual en un grupo de almacenamiento:
    1.  Agregar un grupo de almacenamiento de disco tooa y crear un disco virtual con el diseño simple.
    2.  Agregar discos adicionales y extender disco virtual Hola.
    3.  Crear volúmenes en el disco virtual de Hola.
3.  Agregar Hola volúmenes tooBackup Server.
4.  Configure el almacenamiento con reconocimiento de la carga de trabajo.

## <a name="create-a-volume-for-modern-backup-storage"></a>Creación de un volumen para Modern Backup Storage

El uso de Backup Server v2 con volúmenes como almacenamiento en disco puede ayudarle a mantener el control sobre el almacenamiento. Un volumen puede ser un único disco. Sin embargo, si desea tooextend almacenamiento Hola futuras, crear un volumen en un disco creado mediante el uso de espacios de almacenamiento insuficiente. Esto puede ayudar a si desea tooexpand volumen de hello para el almacenamiento de copia de seguridad. En esta sección se ofrecen procedimientos recomendados para crear un volumen con esta configuración.

1. En Administrador del servidor, seleccione **Servicios de archivos y almacenamiento** > **Volúmenes** > **Grupos de almacenamiento**. En **DISCOS FÍSICOS**, seleccione **Nuevo grupo de almacenamiento**. 

    ![Creación de un nuevo grupo de almacenamiento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Hola **tareas** cuadro de lista desplegable, seleccione **nuevo disco Virtual**.

    ![Adición de un disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Seleccione el grupo de almacenamiento de hello y, a continuación, seleccione **Agregar disco físico**.

    ![Adición de un disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Seleccione disco físico de hello y, a continuación, seleccione **extender disco Virtual**.

    ![Extender disco virtual Hola](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Seleccione el disco virtual de hello y, a continuación, seleccione **nuevo volumen**.

    ![Creación de un nuevo volumen](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. Hola **Seleccionar servidor de Hola y el disco** cuadro de diálogo, el servidor de select Hola y el nuevo disco de Hola. Después, seleccione **Siguiente**.

    ![Seleccione el disco y el servidor de Hola](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Agregar almacenamiento en disco volúmenes tooBackup Server

un volumen tooBackup Server, en hello tooadd **administración** panel, vuelva a examinar almacenamiento hello y, a continuación, seleccione **agregar**. Aparece una lista de todos los Hola volúmenes disponibles toobe agregado para el almacenamiento del servidor de copia de seguridad. Después de volúmenes disponibles se agregan toohello lista de los volúmenes seleccionados, puede asignarles un toohelp nombre descriptivo que se administran. tooformat estas tooReFS de volúmenes para copia de seguridad de servidor puede usar los beneficios de Hola de almacenamiento de copia de seguridad moderna, seleccione **Aceptar**.

![Adición de volúmenes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configuración del almacenamiento con reconocimiento de la carga de trabajo

Con el almacenamiento de carga de trabajo, puede seleccionar volúmenes de Hola que almacenan de forma preferente ciertos tipos de cargas de trabajo. Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) toostore solo hello las cargas de trabajo que requieren copias de seguridad frecuentes de gran volumen. Un ejemplo es SQL Server con registros de transacciones. Otras cargas de trabajo que se copian con menos frecuencia, al igual que las máquinas virtuales, pueden hacer copia de volúmenes de costo toolow.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Puede configurar el almacenamiento con identificación de la carga de trabajo mediante Hola PowerShell cmdlet Update-DPMDiskStorage, que actualiza las propiedades de Hola de un volumen en el bloque de almacenamiento de hello en un servidor de Data Protection Manager.

Sintaxis:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Hello captura de pantalla siguiente muestra hello DPMDiskStorage actualización cmdlet en la ventana de PowerShell de hello.

![Hola DPMDiskStorage de actualización de comandos en la ventana de PowerShell de hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

cambios de Hola que realice mediante el uso de PowerShell se reflejan en hello consola de administrador del servidor de copia de seguridad.

![Discos y volúmenes de hello consola de administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Pasos siguientes
Después de instalar el servidor de copia de seguridad, obtenga información acerca de cómo tooprepare el servidor, o empezar a proteger una carga de trabajo.

- [Preparar cargas de trabajo de Backup Server](backup-azure-microsoft-azure-backup.md)
- [Usar tooback del servidor de copia de seguridad de un servidor de VMware](backup-azure-backup-server-vmware.md)
- [Usar tooback del servidor de copia de seguridad de SQL Server](backup-azure-sql-mabs.md)

