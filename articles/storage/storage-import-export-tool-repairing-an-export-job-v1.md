---
title: "un trabajo de exportación de importación y exportación de Azure - v1 aaaRepairing | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorepair un trabajo de exportación que se creó y se ejecutan utilizando Hola importación/exportación de Azure servicio."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Reparación de un trabajo de exportación
Cuando haya finalizado un trabajo de exportación, puede ejecutar Hola herramienta de importación y exportación de Microsoft Azure en instalaciones locales:  
  
1.  Descargue los archivos que el servicio de importación y exportación de Azure de hello fue tooexport no se puede.  
  
2.  Validar que los archivos de hello en unidad de Hola se exportaron correctamente.  
  
Debe tener conectividad tooAzure almacenamiento toouse esta funcionalidad.  
  
comando de Hola para reparar un trabajo de importación es **RepairExport**.

## <a name="repairexport-parameters"></a>Parámetros RepairExport

Hello siguientes se pueden especificar parámetros con **RepairExport**:  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|**/r:&lt;ArchivoReparación\>**|Necesario. Archivo de reparación de toohello de ruta de acceso, que realiza un seguimiento de progreso de Hola de reparación de Hola y permitiéndole tooresume una reparación interrumpida. Cada unidad debe tener un solo archivo de reparación. Cuando se inicia una reparación para una unidad determinada, se pasará en el archivo de reparación de tooa de ruta de acceso de Hola que aún no existe. tooresume una reparación interrumpida, debe pasar en nombre de Hola de un archivo de reparación existente. unidad de destino de Hello reparación archivo correspondiente toohello debe especificarse siempre.|  
|**/logdir:&lt;DirectorioRegistro\>**|Opcional. directorio de registro de Hello. Archivos de registro detallado se escribirán toothis directory. Si no se especifica ningún directorio de registro, se utilizará el directorio actual de hello como directorio de registro de hello.|  
|**/d:&lt;DirectorioDestino\>**|Necesario. Hola directory toovalidate y reparación. Esto suele ser directorio de raíz de Hola de unidad de exportación de hello, pero podría también ser un recurso compartido de red que contiene una copia de archivos de hello que exporta.|  
|**/bk:&lt;ClaveBitLocker\>**|Opcional. Debe especificar la clave de BitLocker de hello si desea Hola herramienta toounlock cifrado Hola donde los archivos exportados se almacenan.|  
|**/sn:&lt;NombreCuentaAlmacenamiento\>**|Necesario. nombre de Hola de cuenta de almacenamiento de Hola para hello el trabajo de exportación.|  
|**/sk:&lt;ClaveCuentaAlmacenamiento\>**|**Necesario** únicamente si no se especifica un SAS del contenedor. trabajo de exportación de la clave de cuenta de almacenamiento de Hola para Hola Hola.|  
|**/csas:&lt;SasContenedor\>**|**Requiere** si y solo si no se especifica la clave de cuenta de almacenamiento de Hola. contenedor de Hello SAS para tener acceso a blobs Hola asociados con el trabajo de exportación de Hola.|  
|**/CopyLogFile:&lt;ArchivoRegistroCopiaUnidad\>**|Necesario. archivo de registro de la copia de unidad de toohello con Hello ruta de acceso. archivo Hello genera Hola servicio de importación y exportación de Windows Azure y puede descargarse desde almacenamiento de blobs de hello asociado Hola trabajo. archivo de registro de copia de Hello contiene información sobre errores blobs o archivos que son toobe reparada.|  
|**/ManifestFile:&lt;ArchivoManifiestoUnidad\>**|Opcional. archivo de manifiesto de la unidad de exportación de Hello ruta de acceso toohello. Este archivo es generado por el servicio de importación y exportación de Windows Azure de Hola y almacenado en la unidad de exportación de hello y, opcionalmente, en un blob de la cuenta de almacenamiento de hello asociada con el trabajo de Hola.<br /><br /> Hola contenido del programa Hola a archivos en la unidad de exportación de Hola se comprobará con los valores hash de MD5 de hello contenidos en este archivo. Los archivos que se determina toobe dañado será directorios de destino toohello descargado y ha vuelto a escribir.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Usar RepairExport toocorrect de modo no pudo exportaciones  
Puede usar archivos de toodownload de herramienta de importación y exportación de Azure de Hola que no se pudieron tooexport. archivo de registro de copia de Hello contendrá una lista de archivos que no se pudieron tooexport.  
  
causas de Hola de errores de exportación incluyen hello siguientes posibilidades:  
  
-   Unidades dañadas  
  
-   clave de cuenta de almacenamiento de Hello cambiado durante el proceso de transferencia de Hola  
  
herramienta de hello toorun en **RepairExport** modo, primero necesita tooconnect Hola unidad que contiene el equipo de tooyour de los archivos exportados de Hola. A continuación, ejecute la herramienta de importación y exportación de Azure, especificación de unidad de toothat de ruta de acceso de hello con hello hello `/d` parámetro. También necesita el archivo de registro de copia de la unidad de toohello de toospecify Hola ruta de acceso que ha descargado. Hello siguiente ejemplo de línea de comandos siguiente ejecuta Hola herramienta toorepair los archivos que no se pudo tooexport:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Hola te mostramos un ejemplo de un archivo de registro de copia que muestra que un bloque de hello blob no se pudo tooexport:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
archivo de registro de copia de Hello indica que se produjo un error mientras Hola servicio de importación y exportación de Windows Azure descargaba uno de los archivos de toohello de bloques del blob de hello en unidad de exportación de Hola. Hola otros componentes del archivo de hello descargado correctamente y longitud del archivo Hola se estableció correctamente. En este caso, herramienta de hello abrir archivo hello en unidad de hello, descargar bloque Hola de cuenta de almacenamiento de Hola y escribir toohello intervalo de archivo a partir del desplazamiento 65536 con la longitud 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>Uso de contenido de la unidad de RepairExport toovalidate  
También puede utilizar la importación y exportación de Azure con hello **RepairExport** contenido en la unidad de Hola Hola de toovalidate las opciones es correcta. archivo de manifiesto de Hello en cada unidad de disco de exportación contiene MD5s para contenido de Hola de unidad de Hola.  
  
Hola servicio de importación y exportación de Azure también puede guardar los archivos de manifiesto de hello tooa cuenta de almacenamiento durante el proceso de exportación de Hola. Hello ubicación de archivos de manifiesto de hello está disponible a través de hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación cuando se haya completado el trabajo de Hola. Vea [servicio de importación y exportación de formato de archivo de manifiesto](storage-import-export-file-format-metadata-and-properties.md) para obtener más información acerca del formato de Hola de un archivo de manifiesto de unidad.  
  
Hello en el ejemplo siguiente se muestra cómo toorun Hola herramienta de importación y exportación de Azure con hello **/MANIFESTFILE** y **/CopyLogFile** parámetros:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Hola te mostramos un ejemplo de un archivo de manifiesto:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Después de Terminar proceso de reparación de Hola Hola herramienta leer cada archivo al que hace referencia en el archivo de manifiesto de Hola y comprobar la integridad del archivo de hello con los valores hash MD5 de Hola. Para el manifiesto de hello anterior, repasará Hola de los componentes siguientes.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Se descargará herramienta hello y volver a escribir cualquier componente de errores de comprobación de hello toohello mismo archivo en la unidad de Hola.  
  
## <a name="next-steps"></a>Pasos siguientes
 
* [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup-v1.md)   
* [Preparación de unidades de disco duro para un trabajo de importación](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisión del estado del trabajo con archivos de registro de copia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparación de un trabajo de importación](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
