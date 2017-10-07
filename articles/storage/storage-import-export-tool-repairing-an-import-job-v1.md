---
title: "un trabajo de importación de importación y exportación de Azure - v1 aaaRepairing | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorepair un trabajo de importación que se creó y se ejecutan utilizando Hola importación/exportación de Azure servicio."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Reparación de un trabajo de importación
Hola servicio de importación y exportación de Microsoft Azure puede producir un error toocopy algunos de los archivos o partes de un servicio de Windows Azure Blob toohello de archivo. Estas son algunas razones de los errores:  
  
-   Archivos dañados  
  
-   Unidades dañadas  
  
-   clave de cuenta de almacenamiento de Hello cambiado mientras se transfería el archivo hello.  
  
Puede ejecutar Hola herramienta de importación y exportación de Microsoft Azure con la importación de hello archivos de registro de copia del trabajo y herramienta de hello cargará los archivos que faltan de hello (o partes de un archivo) trabajo de importación de toocomplete de cuenta almacenamiento de Windows Azure de tooyour.  
  
## <a name="repairimport-parameters"></a>Parámetros de RepairImport

Hello siguientes se pueden especificar parámetros con **RepairImport**: 
  
|||  
|-|-|  
|**/r:**&lt;ArchivoReparación\>|**Requerido.** Archivo de reparación de toohello de ruta de acceso, que realiza un seguimiento de progreso de Hola de reparación de Hola y permitiéndole tooresume una reparación interrumpida. Cada unidad debe tener un solo archivo de reparación. Cuando se inicia una reparación para una unidad determinada, se pasará en el archivo de reparación de tooa de ruta de acceso de Hola que aún no existe. tooresume una reparación interrumpida, debe pasar en nombre de Hola de un archivo de reparación existente. unidad de destino de Hello reparación archivo correspondiente toohello debe especificarse siempre.|  
|**/logdir:**&lt;DirectorioRegistro\>|**Opcional.** directorio de registro de Hello. Archivos de registro detallado se escribirán toothis directory. Si no se especifica ningún directorio de registro, se utilizará el directorio actual de hello como directorio de registro de hello.|  
|**/d:**&lt;DirectoriosDestino\>|**Requerido.** Uno o varios directorios de separados por punto y coma que contienen Hola archivos originales que se importaron. unidad de importación de Hello también puede utilizarse, pero no es necesario si están disponibles las ubicaciones alternativas de archivos originales.|  
|**/bk:**&lt;ClaveBitLocker\>|**Opcional.** Debe especificar la clave de BitLocker de hello si desea Hola herramienta toounlock una unidad cifrada donde están disponibles los archivos originales de Hola.|  
|**/sn:**&lt;NombreCuentaAlmacenamiento\>|**Requerido.** nombre de Hola de cuenta de almacenamiento de Hola para hello el trabajo de importación.|  
|**/sk:**&lt;ClaveCuentaAlmacenamiento\>|**Necesario** únicamente si no se especifica un SAS del contenedor. clave de cuenta de almacenamiento de Hola para Hola Hola el trabajo de importación.|  
|**/csas:**&lt;SasContenedor\>|**Requiere** si y solo si no se especifica la clave de cuenta de almacenamiento de Hola. contenedor de Hello SAS para tener acceso a blobs Hola asociados con el trabajo de importación de Hola.|  
|**/CopyLogFile:**&lt;ArchivoRegistroCopiaUnidad\>|**Requerido.** Ruta de acceso toohello unidad copiar archivo de registro (registro detallado o registro de errores). archivo Hello genera Hola servicio de importación y exportación de Windows Azure y puede descargarse desde almacenamiento de blobs de hello asociado Hola trabajo. archivo de registro de copia de Hello contiene información sobre errores blobs o archivos que son toobe reparada.|  
|**/PathMapFile:**&lt;ArchivoAsignaciónRutaAccesoUnidad\>|**Opcional.** Archivo de texto tooa de ruta de acceso que se puede usar tooresolve ambigüedades si tiene varios archivos con el mismo nombre que se importaron en hello Hola mismo trabajo. Hola primera hora Hola herramienta se ejecuta, puede rellenar este archivo con todos los nombres ambiguos de Hola. Las ejecuciones posteriores de la herramienta de hello usará este ambigüedades de hello tooresolve de archivo.|  
  
## <a name="using-hello-repairimport-command"></a>Usar comandos de hello RepairImport  
toorepair importar datos mediante el streaming de datos de Hola a través de red de hello, debe especificar directorios de Hola que contienen Hola archivos originales que se importaron con Hola `/d` parámetro. También debe especificar el archivo de registro de copia de Hola que descargó desde su cuenta de almacenamiento. Una línea de comandos típica toorepair un trabajo de importación con errores parciales el siguiente aspecto:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Hola aquí te mostramos un ejemplo de un archivo de registro de copia. En este caso, un fragmento de 64 K de un archivo estaba dañado en la unidad de Hola que se envió para el trabajo de importación de Hola. Puesto que es único error Hola indicado, rest Hola de blobs de hello en el trabajo de Hola se han importado correctamente.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Cuando este registro de copia se pasa toohello herramienta de importación y exportación de Azure, Hola intentará toofinish importación Hola del archivo copiar contenido de falta de Hola a través de la red de Hola. Siguiendo con el ejemplo hello anterior, herramienta de hello buscará archivo original de hello `\animals\koala.jpg` en directorios de hello dos `C:\Users\bob\Pictures` y `X:\BobBackup\photos`. Si hello archivo `C:\Users\bob\Pictures\animals\koala.jpg` existe, Hola herramienta de importación y exportación de Azure copiará el intervalo de falta de Hola de blob de datos correspondiente del toohello `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Resolución de conflictos cuando se usa RepairImport  
En algunas situaciones, no puede ser herramienta hello toofind pueda ni Hola abierto necesario archivo uno de hello siguientes motivos: no se encontró el archivo hello, archivo hello no es accesible, nombre de archivo de hello es ambiguo o contenido Hola de archivo hello ya no es correcta.  
  
Podría producirse un error ambiguo si está tratando de herramienta de hello toolocate `\animals\koala.jpg` y hay un archivo con ese nombre en `C:\Users\bob\pictures` y `X:\BobBackup\photos`. Es decir, ambos `C:\Users\bob\pictures\animals\koala.jpg` y `X:\BobBackup\photos\animals\koala.jpg` existe en unidades de trabajo de importación de Hola.  
  
Hola `/PathMapFile` opción le permitirá tooresolve estos errores. Puede especificar el nombre de hello del archivo de Hola que contendrá la lista de Hola de archivos que Hola herramienta no pudo identificar toocorrectly. Hola siguiente es una línea de comandos de ejemplo que rellenaría `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
herramienta de Hello, a continuación, escribirá las rutas de acceso de archivo problemáticas de hello demasiado`9WM35C2V_pathmap.txt`, uno en cada línea. Por ejemplo, archivo hello puede contener Hola siguiendo las entradas después de ejecutar el comando de hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Para cada archivo de lista de hello, debe intentar toolocate y abra Hola archivo tooensure es herramienta toohello disponible. Si lo desea herramienta de hello tootell explícitamente donde toofind un archivo, puede modificar la ruta de acceso de hello archivo de asignación y agregar archivo de tooeach de ruta de acceso de hello en hello misma línea, separados por un carácter de tabulación:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Después de realizar la herramienta de hello archivos necesarios toohello disponibles, o archivo de mapa de ruta de acceso de actualización hello, puedes repetir el proceso de importación de hello herramienta toocomplete Hola.  
  
## <a name="next-steps"></a>Pasos siguientes
 
* [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup-v1.md)   
* [Preparación de unidades de disco duro para un trabajo de importación](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisión del estado del trabajo con archivos de registro de copia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparación de un trabajo de exportación](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
