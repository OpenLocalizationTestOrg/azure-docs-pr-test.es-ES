---
title: aaaTools para el almacenamiento de la pila de Azure
description: "Obtenga información acerca de las herramientas de transferencia de datos de Azure Stack Storage"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a>Herramientas de Azure Stack Storage

Pila de Microsoft Azure proporciona un conjunto de servicios de almacenamiento de Hola para discos, blobs, tablas, colas y funcionalidad de administración de cuentas. Puede usar un conjunto de herramientas de almacenamiento de Azure si desea toomanage o mover datos tooor pila del almacenamiento de Azure. Este artículo proporciona una introducción rápida de herramientas de hello disponibles.

depende de la herramienta Hola que mejor se adapte a sus requisitos:
* [AzCopy](#azcopy)

    Una utilidad de línea de comandos específicos del almacenamiento que puede descargar toocopy datos de un objeto tooanother dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.

* [Azure PowerShell](#azure-powershell)

    Un shell de línea de comandos basado en tareas y un lenguaje de scripts diseñado especialmente para la administración del sistema.

* [CLI de Azure](#azure-cli)

    Una herramienta de código abierto, multiplataforma que proporciona un conjunto de comandos para trabajar con las plataformas de Azure y Azure pila Hola.

* [Explorador de Microsoft Azure Storage (versión preliminar)](#microsoft-azure-storage-explorer)

    Una aplicación independiente de toouse fácil con una interfaz de usuario.

Debido a diferencias de servicios de almacenamiento de toohello entre Azure y la pila de Azure, puede haber algunos requisitos específicos para cada herramienta que se describe en las secciones siguientes de Hola. Para ver una comparación entre Azure Stack Storage y Azure Storage, consulte [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones).


## <a name="azcopy"></a>AzCopy
AzCopy es una tooand de datos de utilidad de línea de comandos diseñada toocopy desde el almacenamiento de blobs de Microsoft Azure y la tabla mediante comandos simples con un rendimiento óptimo. Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento. Hay dos versiones de Hola AzCopy: AzCopy en Windows y AzCopy en Linux. Pila de Azure solo admite la versión de Windows hello. 
 
### <a name="download-and-install-azcopy"></a>Descarga e instalación de AzCopy 
[Descargar](https://aka.ms/azcopyforazurestack) Hola admitida la versión de Windows de AzCopy para la pila de Azure. Puede instalar y usar AzCopy en Hola de pila de Azure igual que Azure. más información, consulte toolearn [transferir datos con la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md). 

### <a name="azcopy-command-examples-for-data-transfer"></a>Ejemplos del comando AzCopy para la transferencia de datos
Hello en los ejemplos siguientes muestra algunos escenarios típicos para copiar datos tooand de blobs de la pila de Azure. más información, consulte toolearn [transferir datos con la utilidad de línea de comandos de AzCopy hello](../storage/storage-use-azcopy.md). 
#### <a name="download-all-blobs-toolocal-disk"></a>Descargue todos los blobs toolocal disco
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a>Cargar archivo único directorio toovirtual 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>Movimiento de datos entre Azure y Azure Stack Storage 
No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack. necesita transferencia de hello toospecify con hello `/SyncCopy` opción. 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Problemas conocidos de Azcopy
* Las operaciones de AzCopy en File Storage no están disponible porque File Storage aún no está disponible en Azure Stack.
* No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack. Puede especificar Hola transferencia con hello `/SyncCopy` opción datos de hello toocopy.
* no se admite la versión de Linux de Hola de Azcopy para el almacenamiento de la pila de Azure. 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell es un módulo que proporciona cmdlets para administrar servicios tanto en Azure como en Azure Stack. Se trata de un shell de línea de comandos basado en tareas y un lenguaje de scripts especialmente diseñados para administración del sistema.

### <a name="install-and-configure-powershell-for-azure-stack"></a>Instalación y configuración de PowerShell para Azure Stack
Módulos de PowerShell de Azure compatibles de pila de Azure son necesario toowork con la pila de Azure. Para obtener más información, consulte [instale PowerShell para Azure pila](azure-stack-powershell-install.md) y [configurar el entorno de PowerShell del usuario de hello Azure pila](azure-stack-powershell-configure-user.md) toolearn más.

### <a name="powershell-sample-script-for-azure-stack"></a>Script de ejemplo de PowerShell para Azure Stack 
En este ejemplo se supone que ha [instalado PowerShell para Azure Stack](azure-stack-powershell-install.md) correctamente. Este script le ayudarán conplete configuración de Hola y pedir que credenciales de su inquilino de Azure pila tooadd su entorno de PowerShell cuenta toohello local. A continuación, Hola script establezca el valor predeterminado de hello suscripción de Azure, crear una nueva cuenta de almacenamiento de Azure, cree un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente. Después de script de Hola enumera todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargar el archivo de imagen de Hola.

1. Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  
2. Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).  
3. Abra **Windows PowerShell ISE** y **ejecutar como administrador**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script.
4. Copie el siguiente script de Hola y pegue toohello nuevo archivo de script.
5. Actualice las variables de secuencia de comandos de hello en función de las opciones de configuración. 
6. Nota: esta secuencia de comandos tiene toobe se ejecutan en la raíz de Hola de descargado **AzureStack_Tools**. 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a>Problemas conocidos de PowerShell 
Hola actual compatible con Azure PowerShell versión del módulo para la pila de Azure es 1.2.10. Es diferente de la versión más reciente de Hola de PowerShell de Azure. La principal diferencia afecta al funcionamiento de los servicios de almacenamiento:

* formato de valor devuelto de Hola de `Get-AzureRmStorageAccountKey` en la versión 1.2.10 tiene dos propiedades: `Key1` y `Key2`, mientras que la versión de Azure actual Hola devuelve una matriz que contiene todas las claves de cuenta de hello.
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   Para más información, consulte [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).

## <a name="azure-cli"></a>CLI de Azure
Hola CLI de Azure es la experiencia de línea de comandos de Azure para administrar recursos de Azure. Puede instalar en Windows, Linux y Mac OS y ejecútelo desde la línea de comandos de Hola. 

CLI de Azure está optimizado para administrar recursos de Azure desde la línea de comandos de Hola y para generar scripts de automatización que trabajan con hello Azure Resource Manager. Ofrece muchas Hola mismas funciones que se encuentra en el portal de Azure pila hello, incluido el acceso de datos enriquecidos.

Azure Stack requiere la versión 2.0 de la CLI de Azure. Para más información acerca de cómo instalar y Azure PowerShell con Azure Stack, consulte [Install and configure Azure Stack CLI](azure-stack-connect-cli.md) (Instalación y configuración de la CLI de Azure Stack). Para obtener más información acerca de cómo toouse hello Azure CLI 2.0 tooperform varias tareas trabajar con recursos de la cuenta de almacenamiento de la pila de Azure, consulte [Using hello CLI2.0 de Azure con el almacenamiento de Azure](../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>Script de ejemplo de la CLI de Azure para Azure Stack 
Cuando haya completado la instalación de CLI de Hola y configuración, puede intentar Hola siguiendo los pasos toowork con un toointeract de secuencia de comandos de shell pequeño ejemplo con los recursos de almacenamiento de la pila de Azure. script de Hola primero crea un nuevo contenedor en la cuenta de almacenamiento, a continuación, carga un contenedor existente de toothat de archivo (como un blob), enumera todos los blobs en el contenedor de Hola y por último, descarga tooa destino de archivo de hello en el equipo local que especifique. Antes de ejecutar este script, asegúrese de que se haya conectado correctamente y de inicio de sesión toohello destino pila de Azure. 
1. Abra el editor de texto, a continuación, copie y pegue Hola anteponer la secuencia de comandos en el editor de Hola.
2. Actualizar tooreflect de variables del script de Hola las opciones de configuración. 
3. Después de actualizar las variables necesarias de hello, Guardar script de Hola y salir del editor. Hola siguiente da por sentado que ha denominado el my_storage_sample.sh de secuencia de comandos.
4. Marcar el script de Hola como archivo ejecutable, si es necesario:`chmod +x my_storage_sample.sh`
5. Ejecutar script de Hola. Por ejemplo, en Bash: `./my_storage_sample.sh`

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a>Explorador de almacenamiento de Microsoft Azure

El Explorador de Microsoft Azure Storage es una aplicación independiente de Microsoft Permite trabajar de tooeasily con datos de almacenamiento de Azure y Azure pila de almacenamiento en Windows, Mac OS y Linux. Si desea un toomanage fácilmente los datos de almacenamiento de la pila de Azure, considere la posibilidad de mediante el Explorador de almacenamiento de Microsoft Azure.

Para obtener más información acerca de cómo configurar Azure Storage Explorer toowork con la pila de Azure, consulte [conectar Explorador de almacenamiento tooan suscripción de Azure pila](azure-stack-storage-connect-se.md).

Para más información acerca del Explorador de Microsoft Azure Storage, consulte [Introducción al Explorador de Storage (versión preliminar)](../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>Pasos siguientes
* [Conectar Explorador de almacenamiento tooan Azure pila suscripción](azure-stack-storage-connect-se.md)
* [Introducción al Explorador de Storage (versión preliminar)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones)
* [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md)

