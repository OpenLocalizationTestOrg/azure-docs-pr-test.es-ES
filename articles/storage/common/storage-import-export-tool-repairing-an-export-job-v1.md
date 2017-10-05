---
title: "Reparación de un trabajo de exportación de Azure Import/Export (versión 1) | Microsoft Docs"
description: "Obtenga información sobre cómo reparar un trabajo de exportación que se creó y ejecutó con el servicio Azure Import/Export."
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
ms.openlocfilehash: 57ab58fa1fd8371d0b6f019f94bb162bcc1e0e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="80382-103">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="80382-103">Repairing an export job</span></span>
<span data-ttu-id="80382-104">Cuando haya finalizado un trabajo de exportación, puede ejecutar la herramienta Microsoft Azure Import/Export de manera local para:</span><span class="sxs-lookup"><span data-stu-id="80382-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="80382-105">Descargar los archivos que el servicio Azure Import/Export no pudo exportar.</span><span class="sxs-lookup"><span data-stu-id="80382-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="80382-106">Validar que los archivos de la unidad se exportaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="80382-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="80382-107">Debe tener conectividad con Azure Storage para utilizar esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="80382-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="80382-108">El comando para reparar un trabajo de importación es **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="80382-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="80382-109">Parámetros RepairExport</span><span class="sxs-lookup"><span data-stu-id="80382-109">RepairExport parameters</span></span>

<span data-ttu-id="80382-110">Se pueden modificar los parámetros siguientes con **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="80382-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="80382-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="80382-111">Parameter</span></span>|<span data-ttu-id="80382-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="80382-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="80382-113">**/r:<ArchivoReparación\>**</span><span class="sxs-lookup"><span data-stu-id="80382-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="80382-114">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="80382-114">Required.</span></span> <span data-ttu-id="80382-115">Ruta de acceso al archivo de reparación, que realiza un seguimiento del progreso de la reparación y le permite reanudar una reparación interrumpida.</span><span class="sxs-lookup"><span data-stu-id="80382-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="80382-116">Cada unidad debe tener un solo archivo de reparación.</span><span class="sxs-lookup"><span data-stu-id="80382-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="80382-117">Cuando inicie una reparación para una unidad determinada, pasará la ruta de acceso a un archivo de reparación que aún no existe.</span><span class="sxs-lookup"><span data-stu-id="80382-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="80382-118">Para reanudar una reparación interrumpida, debe pasar el nombre de un archivo de reparación existente.</span><span class="sxs-lookup"><span data-stu-id="80382-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="80382-119">Siempre se debe especificar el archivo de reparación correspondiente a la unidad de destino.</span><span class="sxs-lookup"><span data-stu-id="80382-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="80382-120">**/logdir:<DirectorioRegistro\>**</span><span class="sxs-lookup"><span data-stu-id="80382-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="80382-121">Opcional.</span><span class="sxs-lookup"><span data-stu-id="80382-121">Optional.</span></span> <span data-ttu-id="80382-122">El directorio de registro.</span><span class="sxs-lookup"><span data-stu-id="80382-122">The log directory.</span></span> <span data-ttu-id="80382-123">Los archivos de registro detallados se escribirán en este directorio.</span><span class="sxs-lookup"><span data-stu-id="80382-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="80382-124">Si no se especifica un directorio de registro, se usará el directorio actual como directorio de registro.</span><span class="sxs-lookup"><span data-stu-id="80382-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="80382-125">**/d:<DirectorioDestino\>**</span><span class="sxs-lookup"><span data-stu-id="80382-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="80382-126">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="80382-126">Required.</span></span> <span data-ttu-id="80382-127">El directorio para validar y reparar.</span><span class="sxs-lookup"><span data-stu-id="80382-127">The directory to validate and repair.</span></span> <span data-ttu-id="80382-128">Suele ser el directorio raíz de la unidad de exportación, pero podría también ser un recurso compartido de archivos de red que contiene una copia de los archivos exportados.</span><span class="sxs-lookup"><span data-stu-id="80382-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="80382-129">**/bk:<ClaveBitLocker\>**</span><span class="sxs-lookup"><span data-stu-id="80382-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="80382-130">Opcional.</span><span class="sxs-lookup"><span data-stu-id="80382-130">Optional.</span></span> <span data-ttu-id="80382-131">Debe especificar la clave de BitLocker si desea que la herramienta desbloquee una unidad de cifrado donde se almacenan los archivos exportados.</span><span class="sxs-lookup"><span data-stu-id="80382-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="80382-132">**/sn:<NombreCuentaAlmacenamiento\>**</span><span class="sxs-lookup"><span data-stu-id="80382-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="80382-133">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="80382-133">Required.</span></span> <span data-ttu-id="80382-134">El nombre de la cuenta de almacenamiento para el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="80382-135">**/sk:<ClaveCuentaAlmacenamiento\>**</span><span class="sxs-lookup"><span data-stu-id="80382-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="80382-136">**Necesario** únicamente si no se especifica un SAS del contenedor.</span><span class="sxs-lookup"><span data-stu-id="80382-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="80382-137">La clave de cuenta para la cuenta de almacenamiento correspondiente al trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="80382-138">**/csas:<SasContenedor\>**</span><span class="sxs-lookup"><span data-stu-id="80382-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="80382-139">**Requerido** únicamente si no se especifica la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="80382-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="80382-140">El SAS del contenedor para acceder a los blobs asociados al trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="80382-141">**/CopyLogFile:<ArchivoRegistroCopiaUnidad\>**</span><span class="sxs-lookup"><span data-stu-id="80382-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="80382-142">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="80382-142">Required.</span></span> <span data-ttu-id="80382-143">La ruta de acceso al archivo de registro de copia de la unidad.</span><span class="sxs-lookup"><span data-stu-id="80382-143">The path to the drive copy log file.</span></span> <span data-ttu-id="80382-144">El archivo lo genera el servicio Microsoft Windows Import/Export y se puede descargar desde el almacenamiento de blobs asociado al trabajo.</span><span class="sxs-lookup"><span data-stu-id="80382-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="80382-145">El archivo de registro de copia contiene información sobre blobs con errores o archivos que deben repararse.</span><span class="sxs-lookup"><span data-stu-id="80382-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="80382-146">**/ManifestFile:<ArchivoManifiestoUnidad\>**</span><span class="sxs-lookup"><span data-stu-id="80382-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="80382-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="80382-147">Optional.</span></span> <span data-ttu-id="80382-148">La ruta de acceso al archivo de manifiesto de la unidad de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="80382-149">Este archivo lo genera el servicio Microsoft Azure Import/Export y lo almacena en la unidad de exportación y, opcionalmente, en un blob de la cuenta de almacenamiento asociada al trabajo.</span><span class="sxs-lookup"><span data-stu-id="80382-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="80382-150">El contenido de los archivos de la unidad de exportación se comprobará con los hash MD5 contenidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="80382-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="80382-151">Todos los archivos que se determine que están dañados se descargarán y reescribirán en los directorios de destino.</span><span class="sxs-lookup"><span data-stu-id="80382-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="80382-152">Uso del modo RepairExport para corregir las exportaciones con error</span><span class="sxs-lookup"><span data-stu-id="80382-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="80382-153">Puede utilizar la herramienta Azure Import/Export para descargar los archivos que no se pudieron exportar.</span><span class="sxs-lookup"><span data-stu-id="80382-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="80382-154">El archivo de registro de copia contendrá una lista de archivos que no se pudieron exportar.</span><span class="sxs-lookup"><span data-stu-id="80382-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="80382-155">Las causas de errores de exportación incluyen las siguientes posibilidades:</span><span class="sxs-lookup"><span data-stu-id="80382-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="80382-156">Unidades dañadas</span><span class="sxs-lookup"><span data-stu-id="80382-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="80382-157">La clave de cuenta de almacenamiento cambiada durante el proceso de transferencia</span><span class="sxs-lookup"><span data-stu-id="80382-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="80382-158">Para ejecutar la herramienta en el modo **RepairExport**, primero debe conectar la unidad que contiene los archivos exportados al equipo.</span><span class="sxs-lookup"><span data-stu-id="80382-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="80382-159">A continuación, ejecute la herramienta Azure Import/Export, especificando la ruta de acceso a esa unidad con el parámetro `/d`.</span><span class="sxs-lookup"><span data-stu-id="80382-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="80382-160">También debe especificar la ruta de acceso al archivo de registro de copia de la unidad que descargó.</span><span class="sxs-lookup"><span data-stu-id="80382-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="80382-161">El siguiente ejemplo de línea de comandos ejecuta la herramienta para reparar todos los archivos que no se pudieron exportar:</span><span class="sxs-lookup"><span data-stu-id="80382-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="80382-162">A continuación se muestra un ejemplo de un archivo de registro de copia que muestra que un bloque del blob no se pudo exportar:</span><span class="sxs-lookup"><span data-stu-id="80382-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
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
  
<span data-ttu-id="80382-163">El archivo de registro de copia indica que se produjo un error mientras el servicio Microsoft Windows Import/Export descargaba uno de los bloques del blob en el archivo de la unidad de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="80382-164">Los demás componentes del archivo se descargaron correctamente y la longitud del archivo se estableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="80382-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="80382-165">En este caso, la herramienta abrirá el archivo en la unidad, descargará el bloque de la cuenta de almacenamiento y lo escribirá en el intervalo de archivo a partir del desplazamiento 65536 con la longitud 65536.</span><span class="sxs-lookup"><span data-stu-id="80382-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="80382-166">Uso de RepairExport para validar el contenido de la unidad</span><span class="sxs-lookup"><span data-stu-id="80382-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="80382-167">También puede usar Azure Import/Export con la opción **RepairExport** para validar que el contenido de la unidad es correcto.</span><span class="sxs-lookup"><span data-stu-id="80382-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="80382-168">El archivo de manifiesto de cada unidad de exportación contiene MD5 para el contenido de la unidad.</span><span class="sxs-lookup"><span data-stu-id="80382-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="80382-169">El servicio Azure Import/Export también puede guardar los archivos de manifiesto en una cuenta de almacenamiento durante el proceso de exportación.</span><span class="sxs-lookup"><span data-stu-id="80382-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="80382-170">La ubicación de los archivos de manifiesto estará disponible a través de la operación [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) cuando se haya completado el trabajo.</span><span class="sxs-lookup"><span data-stu-id="80382-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="80382-171">Vea [Import-Export Service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) (Formato del archivo de manifiesto del servicio Import/Export) para obtener más información sobre el formato de un archivo de manifiesto de unidad.</span><span class="sxs-lookup"><span data-stu-id="80382-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="80382-172">En el ejemplo siguiente se muestra cómo ejecutar la herramienta Azure Import/Export con los parámetros **/MANIFESTFILE** y **/CopyLogFile**:</span><span class="sxs-lookup"><span data-stu-id="80382-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="80382-173">A continuación se muestra un ejemplo de un archivo de manifiesto:</span><span class="sxs-lookup"><span data-stu-id="80382-173">The following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="80382-174">Después de finalizar el proceso de reparación, la herramienta leerá por completo los archivos a los que hace se referencia en el archivo de manifiesto y comprobará la integridad de dichos archivos con los hash MD5.</span><span class="sxs-lookup"><span data-stu-id="80382-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="80382-175">Para el manifiesto anterior, recorrerá los siguientes componentes.</span><span class="sxs-lookup"><span data-stu-id="80382-175">For the manifest above, it will go through the following components.</span></span>  

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

<span data-ttu-id="80382-176">Cualquier componente que no supere la comprobación lo descargará la herramienta y se reescribirá en el mismo archivo en la unidad.</span><span class="sxs-lookup"><span data-stu-id="80382-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="80382-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80382-177">Next steps</span></span>
 
* [<span data-ttu-id="80382-178">Configuración de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="80382-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="80382-179">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="80382-179">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="80382-180">Revisión del estado del trabajo con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="80382-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="80382-181">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="80382-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="80382-182">Solución de problemas de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="80382-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
