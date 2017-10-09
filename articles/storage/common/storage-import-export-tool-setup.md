---
title: "aaaSetting una herramienta de importación y exportación de Azure Hola | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset seguridad Hola unidad preparación y la herramienta de reparación de servicio de importación y exportación de Azure de Hola."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3d8897f2783112e07123669f1ba5b22576770e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Cómo configurar Hola herramienta de importación y exportación de Azure

Hola, herramienta de importación y exportación de Microsoft Azure es Hola unidad herramienta de preparación y reparación que puede usar con hello servicio de importación y exportación de Microsoft Azure. Puede utilizar herramienta de Hola para hello siguientes funciones:

* Antes de crear un trabajo de importación, puede usar esta herramienta toocopy datos toohello unidades de disco duro va centro de datos de Azure de tooship tooan.
* Cuando haya finalizado un trabajo de importación, puede usar esta herramienta toorepair los blobs que estaban dañados que falten o que entran en conflicto con otros blobs.
* Después de recibir las unidades de Hola de un trabajo de exportación completado, puede usar esta herramienta toorepair los archivos que estaban dañados o que faltan en las unidades de Hola.

## <a name="prerequisites"></a>Requisitos previos

Si está **preparar las unidades** para un trabajo de importación, debe cumplirse Hola siguiendo los requisitos previos:

* Debe contar con una suscripción de Azure activa.
* La suscripción debe incluir una cuenta de almacenamiento con suficientes archivos de hello toostore de espacio disponible que va tooimport.
* Se necesita al menos una de las claves de acceso de cuenta de almacenamiento de Hola.
* Se necesita un equipo (Hola "equipo de copia") con Windows 7, Windows Server 2008 R2 o un sistema operativo de Windows más reciente instalado.
* Hola .NET Framework 4 debe instalarse en el equipo de copia de Hola.
* BitLocker debe habilitarse en el equipo de copia de Hola.
* Se necesita una o más vacía 3,5 discos duros SATA conectado toohello equipo de copia.
* archivos de Hello piensa tooimport deben ser accesibles desde el equipo de copia de hello, independientemente de si están en un recurso compartido de red o una unidad de disco duro local.

Si estás intentando demasiado**reparar una importación** que se produjo un error parcial, debe:

* archivos de registro de copia de Hola
* clave de cuenta de almacenamiento de Hola

Si estás intentando demasiado**reparar una exportación** que se produjo un error parcial, debe:

* archivos de registro de copia de Hola
* archivos de manifiesto de Hello (opcionales)
* clave de cuenta de almacenamiento de Hola

## <a name="installing-hello-azure-importexport-tool"></a>Hola instalar herramienta de importación y exportación de Azure

En primer lugar, [descargar la herramienta de importación y exportación de Azure hello](https://www.microsoft.com/download/details.aspx?id=55280) y extráigalo tooa directorio en el equipo, por ejemplo `c:\WAImportExport`.

Hola, herramienta de importación y exportación de Azure consta de hello siguientes archivos:

* dataset.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

A continuación, abra una ventana de símbolo del sistema en **modo de administrador**, y cambiar al directorio de Hola que contiene Hola extrajo los archivos.

Ayuda de toooutput de comando de hello, ejecute la herramienta de hello (`WAImportExport.exe`) sin parámetros:

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a>Pasos siguientes

* [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import.md)
* [Vista previa de uso de disco para un trabajo de exportación](../storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [Revisión del estado del trabajo con archivos de registro de copia](../storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparación de un trabajo de importación](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparación de un trabajo de exportación](../storage-import-export-tool-repairing-an-export-job-v1.md)
* [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
