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
# <a name="repairing-an-export-job"></a><span data-ttu-id="1a6c2-103">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="1a6c2-103">Repairing an export job</span></span>
<span data-ttu-id="1a6c2-104">Cuando haya finalizado un trabajo de exportación, puede ejecutar Hola herramienta de importación y exportación de Microsoft Azure en instalaciones locales:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="1a6c2-105">Descargue los archivos que el servicio de importación y exportación de Azure de hello fue tooexport no se puede.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="1a6c2-106">Validar que los archivos de hello en unidad de Hola se exportaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="1a6c2-107">Debe tener conectividad tooAzure almacenamiento toouse esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="1a6c2-108">comando de Hola para reparar un trabajo de importación es **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="1a6c2-109">Parámetros RepairExport</span><span class="sxs-lookup"><span data-stu-id="1a6c2-109">RepairExport parameters</span></span>

<span data-ttu-id="1a6c2-110">Hello siguientes se pueden especificar parámetros con **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="1a6c2-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1a6c2-111">Parameter</span></span>|<span data-ttu-id="1a6c2-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a6c2-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1a6c2-113">**/r:&lt;ArchivoReparación\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="1a6c2-114">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-114">Required.</span></span> <span data-ttu-id="1a6c2-115">Archivo de reparación de toohello de ruta de acceso, que realiza un seguimiento de progreso de Hola de reparación de Hola y permitiéndole tooresume una reparación interrumpida.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="1a6c2-116">Cada unidad debe tener un solo archivo de reparación.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="1a6c2-117">Cuando se inicia una reparación para una unidad determinada, se pasará en el archivo de reparación de tooa de ruta de acceso de Hola que aún no existe.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="1a6c2-118">tooresume una reparación interrumpida, debe pasar en nombre de Hola de un archivo de reparación existente.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="1a6c2-119">unidad de destino de Hello reparación archivo correspondiente toohello debe especificarse siempre.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="1a6c2-120">**/logdir:&lt;DirectorioRegistro\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="1a6c2-121">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-121">Optional.</span></span> <span data-ttu-id="1a6c2-122">directorio de registro de Hello.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-122">hello log directory.</span></span> <span data-ttu-id="1a6c2-123">Archivos de registro detallado se escribirán toothis directory.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="1a6c2-124">Si no se especifica ningún directorio de registro, se utilizará el directorio actual de hello como directorio de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="1a6c2-125">**/d:&lt;DirectorioDestino\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="1a6c2-126">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-126">Required.</span></span> <span data-ttu-id="1a6c2-127">Hola directory toovalidate y reparación.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="1a6c2-128">Esto suele ser directorio de raíz de Hola de unidad de exportación de hello, pero podría también ser un recurso compartido de red que contiene una copia de archivos de hello que exporta.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="1a6c2-129">**/bk:&lt;ClaveBitLocker\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="1a6c2-130">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-130">Optional.</span></span> <span data-ttu-id="1a6c2-131">Debe especificar la clave de BitLocker de hello si desea Hola herramienta toounlock cifrado Hola donde los archivos exportados se almacenan.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="1a6c2-132">**/sn:&lt;NombreCuentaAlmacenamiento\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="1a6c2-133">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-133">Required.</span></span> <span data-ttu-id="1a6c2-134">nombre de Hola de cuenta de almacenamiento de Hola para hello el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1a6c2-135">**/sk:&lt;ClaveCuentaAlmacenamiento\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="1a6c2-136">**Necesario** únicamente si no se especifica un SAS del contenedor.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="1a6c2-137">trabajo de exportación de la clave de cuenta de almacenamiento de Hola para Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1a6c2-138">**/csas:&lt;SasContenedor\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="1a6c2-139">**Requiere** si y solo si no se especifica la clave de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="1a6c2-140">contenedor de Hello SAS para tener acceso a blobs Hola asociados con el trabajo de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="1a6c2-141">**/CopyLogFile:&lt;ArchivoRegistroCopiaUnidad\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="1a6c2-142">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-142">Required.</span></span> <span data-ttu-id="1a6c2-143">archivo de registro de la copia de unidad de toohello con Hello ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="1a6c2-144">archivo Hello genera Hola servicio de importación y exportación de Windows Azure y puede descargarse desde almacenamiento de blobs de hello asociado Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="1a6c2-145">archivo de registro de copia de Hello contiene información sobre errores blobs o archivos que son toobe reparada.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="1a6c2-146">**/ManifestFile:&lt;ArchivoManifiestoUnidad\>**</span><span class="sxs-lookup"><span data-stu-id="1a6c2-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="1a6c2-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-147">Optional.</span></span> <span data-ttu-id="1a6c2-148">archivo de manifiesto de la unidad de exportación de Hello ruta de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="1a6c2-149">Este archivo es generado por el servicio de importación y exportación de Windows Azure de Hola y almacenado en la unidad de exportación de hello y, opcionalmente, en un blob de la cuenta de almacenamiento de hello asociada con el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="1a6c2-150">Hola contenido del programa Hola a archivos en la unidad de exportación de Hola se comprobará con los valores hash de MD5 de hello contenidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="1a6c2-151">Los archivos que se determina toobe dañado será directorios de destino toohello descargado y ha vuelto a escribir.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="1a6c2-152">Usar RepairExport toocorrect de modo no pudo exportaciones</span><span class="sxs-lookup"><span data-stu-id="1a6c2-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="1a6c2-153">Puede usar archivos de toodownload de herramienta de importación y exportación de Azure de Hola que no se pudieron tooexport.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="1a6c2-154">archivo de registro de copia de Hello contendrá una lista de archivos que no se pudieron tooexport.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="1a6c2-155">causas de Hola de errores de exportación incluyen hello siguientes posibilidades:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="1a6c2-156">Unidades dañadas</span><span class="sxs-lookup"><span data-stu-id="1a6c2-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="1a6c2-157">clave de cuenta de almacenamiento de Hello cambiado durante el proceso de transferencia de Hola</span><span class="sxs-lookup"><span data-stu-id="1a6c2-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="1a6c2-158">herramienta de hello toorun en **RepairExport** modo, primero necesita tooconnect Hola unidad que contiene el equipo de tooyour de los archivos exportados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="1a6c2-159">A continuación, ejecute la herramienta de importación y exportación de Azure, especificación de unidad de toothat de ruta de acceso de hello con hello hello `/d` parámetro.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="1a6c2-160">También necesita el archivo de registro de copia de la unidad de toohello de toospecify Hola ruta de acceso que ha descargado.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="1a6c2-161">Hello siguiente ejemplo de línea de comandos siguiente ejecuta Hola herramienta toorepair los archivos que no se pudo tooexport:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="1a6c2-162">Hola te mostramos un ejemplo de un archivo de registro de copia que muestra que un bloque de hello blob no se pudo tooexport:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="1a6c2-163">archivo de registro de copia de Hello indica que se produjo un error mientras Hola servicio de importación y exportación de Windows Azure descargaba uno de los archivos de toohello de bloques del blob de hello en unidad de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="1a6c2-164">Hola otros componentes del archivo de hello descargado correctamente y longitud del archivo Hola se estableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="1a6c2-165">En este caso, herramienta de hello abrir archivo hello en unidad de hello, descargar bloque Hola de cuenta de almacenamiento de Hola y escribir toohello intervalo de archivo a partir del desplazamiento 65536 con la longitud 65536.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="1a6c2-166">Uso de contenido de la unidad de RepairExport toovalidate</span><span class="sxs-lookup"><span data-stu-id="1a6c2-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="1a6c2-167">También puede utilizar la importación y exportación de Azure con hello **RepairExport** contenido en la unidad de Hola Hola de toovalidate las opciones es correcta.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="1a6c2-168">archivo de manifiesto de Hello en cada unidad de disco de exportación contiene MD5s para contenido de Hola de unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="1a6c2-169">Hola servicio de importación y exportación de Azure también puede guardar los archivos de manifiesto de hello tooa cuenta de almacenamiento durante el proceso de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="1a6c2-170">Hello ubicación de archivos de manifiesto de hello está disponible a través de hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación cuando se haya completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="1a6c2-171">Vea [servicio de importación y exportación de formato de archivo de manifiesto](storage-import-export-file-format-metadata-and-properties.md) para obtener más información acerca del formato de Hola de un archivo de manifiesto de unidad.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="1a6c2-172">Hello en el ejemplo siguiente se muestra cómo toorun Hola herramienta de importación y exportación de Azure con hello **/MANIFESTFILE** y **/CopyLogFile** parámetros:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="1a6c2-173">Hola te mostramos un ejemplo de un archivo de manifiesto:</span><span class="sxs-lookup"><span data-stu-id="1a6c2-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="1a6c2-174">Después de Terminar proceso de reparación de Hola Hola herramienta leer cada archivo al que hace referencia en el archivo de manifiesto de Hola y comprobar la integridad del archivo de hello con los valores hash MD5 de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="1a6c2-175">Para el manifiesto de hello anterior, repasará Hola de los componentes siguientes.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="1a6c2-176">Se descargará herramienta hello y volver a escribir cualquier componente de errores de comprobación de hello toohello mismo archivo en la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a6c2-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1a6c2-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a6c2-177">Next steps</span></span>
 
* [<span data-ttu-id="1a6c2-178">Setting Up Hola herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="1a6c2-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="1a6c2-179">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="1a6c2-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="1a6c2-180">Revisión del estado del trabajo con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="1a6c2-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="1a6c2-181">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="1a6c2-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="1a6c2-182">Solución de problemas de hello herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="1a6c2-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
