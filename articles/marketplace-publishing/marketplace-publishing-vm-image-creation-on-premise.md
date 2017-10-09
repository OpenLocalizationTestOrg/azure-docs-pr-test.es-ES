---
title: "aaaCreating una imagen de máquina virtual local para hello Azure Marketplace | Documentos de Microsoft"
description: "Entender y ejecutar Hola pasos toocreate una imagen de máquina virtual local e implementar toohello Azure Marketplace para que otros lo toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Desarrollar una imagen de máquina virtual local para hello Azure Marketplace
Se recomienda encarecidamente que desarrollar Azure discos duros virtuales (VHD) directamente en la nube de hello mediante Protocolo de escritorio remoto. Sin embargo, si es necesario, es posible toodownload un disco duro virtual y desarrollar mediante la infraestructura local.  

Para el desarrollo local, debe descargar el sistema de operativo Hola VHD de hello creado máquina virtual. Estos pasos tendrán lugar como parte del paso 3.3, arriba.  

## <a name="download-a-vhd-image"></a>Descargar una imagen de disco duro virtual
### <a name="locate-a-blob-url"></a>Búsqueda de la dirección URL de blob
Hola toodownload de orden VHD, buscar dirección URL de blob de hello para el disco del sistema operativo de Hola.

Buscar la dirección URL de blob de Hola de hello nueva [portal de Microsoft Azure](https://portal.azure.com):

1. Vaya demasiado**examinar** > **máquinas virtuales**, y, a continuación, seleccione Hola implementa VM.
2. En **configurar**, seleccione hello **discos** icono, que abre una hoja de discos de Hola.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Seleccione hello **disco del sistema operativo**, que abre otra hoja que se muestra las propiedades de disco, incluida la ubicación del VHD Hola.
4. Copie esta dirección URL de blob.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Ahora, eliminar Hola implementa VM sin eliminar los discos de copia de seguridad de Hola. También puede detener Hola VM en lugar de eliminarlo. Descargar VHD del sistema operativo hello cuando Hola máquina virtual se está ejecutando.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Descarga de un disco duro virtual
Una vez que sepa Hola URL del blob, puede descargar Hola VHD mediante hello [portal de Azure](http://manage.windowsazure.com/) o PowerShell.  

> [!NOTE]
> En tiempo de saludo de la creación de esta guía, toodownload de funcionalidad de hello un disco duro virtual aún no está presente en el nuevo portal de Microsoft Azure Hola.  
> 
> 

**Descargar Hola VHD del sistema operativo a través de hello actual [portal de Azure](http://manage.windowsazure.com/)**

1. Inicie sesión en toohello portal de Azure si aún no lo ha hecho.
2. Haga clic en hello **almacenamiento** ficha.
3. Seleccione la cuenta de almacenamiento de hello en qué Hola se almacena el disco duro virtual.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. De este modo se muestran las propiedades de la cuenta de almacenamiento. Seleccione hello **contenedores** ficha.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Seleccionar contenedor de hello en qué Hola se almacena el disco duro virtual. De forma predeterminada, cuando se creó desde el portal de hello, Hola VHD se almacena en un contenedor de discos duros virtuales.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Seleccione VHD de sistema operativo correcto de hello comparando toohello de dirección URL de hello uno que guardó.
7. Haga clic en **Descargar**.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Descarga de un disco duro virtual mediante PowerShell
Además toousing Hola portal de Azure, puede usar hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) sistema de operativo de cmdlet toodownload Hola VHD.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Por ejemplo, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** también tiene un **NumberOfThreads** opción que se puede usar tooincrease paralelismo toomake Hola mejor uso del ancho de banda disponible para su descarga Hola.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Cargar la cuenta de almacenamiento de Azure de tooan de discos duros virtuales
Si prepara los discos duros virtuales locales, deberá tooupload en un almacenamiento de la cuenta en Azure. Este paso tendrá lugar después de crear su disco duro virtual de forma local, pero antes de obtener la certificación para la imagen de máquina virtual.

### <a name="create-a-storage-account-and-container"></a>Creación de una cuenta de almacenamiento y un contenedor
Se recomienda que los discos duros virtuales se carga en una cuenta de almacenamiento en una región de Estados Unidos de Hola. Todos los discos duros virtuales de un SKU único deben colocarse en un contenedor único dentro de una cuenta de almacenamiento única.

toocreate una cuenta de almacenamiento, puede usar hello [portal de Microsoft Azure](https://portal.azure.com/), PowerShell, o la herramienta de línea de comandos de Linux Hola.  

**Crear una cuenta de almacenamiento desde el portal de Microsoft Azure Hola**

1. Haga clic en **Nuevo**.
2. Seleccione **Almacenamiento**.
3. Rellene el nombre de cuenta de almacenamiento de hello y, a continuación, seleccione una ubicación.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Haga clic en **Crear**.
5. hoja de Hola para hello creado la cuenta de almacenamiento debe estar abierto. Si no es así, seleccione **Examinar** > **Cuentas de almacenamiento**. En hello almacenamiento cuenta de hoja, seleccione la cuenta de almacenamiento de hello creada.
6. Seleccione **Contenedores**.
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. En la hoja de contenedores de hello, seleccione **agregar**y, a continuación, escriba un permisos del contenedor de hello y nombre de contenedor. Seleccione **Privado** para los permisos del contenedor.

> [!TIP]
> Le recomendamos que cree un contenedor por SKU que tiene previsto toopublish.
> 
> 

  ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Creación de una cuenta de almacenamiento mediante PowerShell
Uso de PowerShell, crear una cuenta de almacenamiento mediante el uso de hello [AzureStorageAccount New](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

A continuación, puede crear un contenedor dentro de esa cuenta de almacenamiento mediante hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Estos comandos dan por hecho que ese contexto de cuenta de almacenamiento actual de hello ya se ha establecido en PowerShell.   Consulte demasiado[configurar Azure PowerShell](marketplace-publishing-powershell-setup.md) para obtener más detalles sobre el programa de instalación de PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Crear una cuenta de almacenamiento mediante la herramienta de línea de comandos de Hola para Mac y Linux
> En la [Herramienta de línea de comandos de Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), cree una cuenta de almacenamiento de la manera siguiente.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Cree un contenedor de la manera siguiente.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Carga de un disco duro virtual
Después de crean cuenta de almacenamiento de Hola y de contenedor, puede cargar el VHD preparada. Puede usar otras herramientas de administración de almacenamiento de Azure, herramienta de línea de comandos de Linux de Hola o PowerShell.

### <a name="upload-a-vhd-via-powershell"></a>Cargar un disco duro virtual a través de PowerShell
Hola de uso [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Cargar un disco duro virtual mediante la herramienta de línea de comandos de Hola para Mac y Linux
Con hello [herramienta de línea de comandos de Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilice Hola siguiente: crear la imagen de máquina virtual de azure <image name> --ubicación <Location of hello data center> --sistema operativo Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Otras referencias
* [Crear una imagen de máquina virtual para hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [Configuración de Azure PowerShell](marketplace-publishing-powershell-setup.md)

