---
title: "base de datos de Analysis Services aaaAzure de copia de seguridad y restauración | Documentos de Microsoft"
description: "Describe cómo toobackup y restauración un análisis de Azure de servicios de base de datos."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Copia de seguridad y restauración

Copia de seguridad de bases de datos de modelo tabular de Analysis Services de Azure es mucho Hola igual que en local de Analysis Services. Hola principal diferencia es donde se almacenan los archivos de copia de seguridad. Archivos de copia de seguridad deben guardarse contenedor tooa en una [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md). Puede usar una cuenta de almacenamiento y un contenedor que ya tenga o puede crear estos al configurar el almacenamiento para el servidor.

> [!NOTE]
> La creación de una cuenta de almacenamiento puede dar lugar a un nuevo servicio facturable. más información, consulte toolearn [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Las copias de seguridad se guardan con extensión abf. Para los modelos tabulares en memoria, se almacenan los datos y los metadatos del modelo. Para los modelos tabulares de consulta directa, solo se almacenan los metadatos del modelo. Las copias de seguridad se pueden comprimir y cifrar, según las opciones de Hola que elija. 



## <a name="configure-storage-settings"></a>Configuración de los valores de almacenamiento
Antes de realizar copias de seguridad, se necesita una configuración de almacenamiento tooconfigure para el servidor.


### <a name="tooconfigure-storage-settings"></a>configuración de almacenamiento de tooconfigure
1.  En el portal de Azure > **Configuración**, haga clic en **Backup**.

    ![Copias de seguridad en Configuración](./media/analysis-services-backup/aas-backup-backups.png)

2.  Haga clic en **Habilitado** y, luego, haga clic en **Configuración de Storage**.

    ![Habilitar](./media/analysis-services-backup/aas-backup-enable.png)

3. Seleccione su cuenta de almacenamiento o cree una nueva.

4. Seleccione un contenedor o cree uno nuevo.

    ![Seleccionar el contenedor](./media/analysis-services-backup/aas-backup-container.png)

5. Guarde la configuración de copia de seguridad.

    ![Guardar la configuración de copia de seguridad](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Backup

### <a name="toobackup-by-using-ssms"></a>toobackup mediante SSMS

1. En SSMS, haga clic con el botón derecho en una base de datos > **Copia de seguridad**.

2. En **Copia de seguridad de la base de datos** > **Archivo de copia de seguridad**, haga clic en **Examinar**.

3. Hola **Guardar archivo como** cuadro de diálogo, compruebe la ruta de acceso de carpeta de hello y, a continuación, escriba un nombre para el archivo de copia de seguridad de hello. 

4. Hola **base de datos de copia de seguridad** cuadro de diálogo, seleccione opciones.

    **Permite el archivo sobrescribir** -Seleccione este opción toooverwrite copias de hello mismo nombre. Si no se selecciona esta opción, que va a guardar el archivo de Hola no puede tener Hola mismo nombre como un archivo que ya existe en hello misma ubicación.

    **Aplicar compresión** -Seleccione este archivo de copia de seguridad de opción toocompress Hola. Los archivos de copia de seguridad comprimidos ahorran espacio en disco, pero requieren un uso de CPU algo mayor. 

    **Cifrar archivo de copia de seguridad** -Seleccione este archivo de copia de seguridad de opción tooencrypt Hola. Esta opción requiere un archivo de copia de seguridad de contraseña proporcionado por el usuario toosecure Hola. contraseña de Hola evita la lectura de datos de copia de seguridad de saludo de alguna otra forma de una operación de restauración. Si elige las copias de seguridad tooencrypt, almacenar contraseña hello en una ubicación segura.

5. Haga clic en **Aceptar** toocreate y guarde el archivo de copia de seguridad de hello.


### <a name="powershell"></a>PowerShell
Use el cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).

## <a name="restore"></a>Restauración
Cuando se restaura, debe ser el archivo de copia de seguridad de cuenta de almacenamiento de Hola que ha configurado para el servidor. Si necesita un archivo de copia de seguridad de una cuenta de almacenamiento local ubicación tooyour toomove, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o hello [AzCopy](../storage/common/storage-use-azcopy.md) utilidad de línea de comandos. 



> [!NOTE]
> Si va a restaurar desde un servidor local, debe quitar todos los usuarios del dominio Hola de roles del modelo de Hola y agregarlos hacer copia de roles de toohello como usuarios de Azure Active Directory.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore mediante SSMS

1. En SSMS, haga clic con el botón derecho en una base de datos > **Restaurar**.

2. Hola **base de datos de copia de seguridad** cuadro de diálogo, en **archivo de copia de seguridad**, haga clic en **examinar**.

3. Hola **buscar archivos de base de datos** cuadro de diálogo, seleccione Hola archivo toorestore.

4. En **Restaurar base de datos**, seleccione la base de datos de Hola.

5. Especifique las opciones. Opciones de seguridad deben coincidir con opciones de copia de seguridad de Hola que usó al realizar copias de seguridad.


### <a name="powershell"></a>PowerShell

Use el cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).


## <a name="related-information"></a>Información relacionada

[Cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md)  
[Alta disponibilidad](analysis-services-bcdr.md)     
[Administración de Azure Analysis Services](analysis-services-manage.md)
