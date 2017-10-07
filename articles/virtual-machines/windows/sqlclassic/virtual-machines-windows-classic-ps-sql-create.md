---
title: "aaaCreate una máquina Virtual de SQL Server en PowerShell de Azure (clásica) | Documentos de Microsoft"
description: "Ofrece pasos y scripts de PowerShell para crear una máquina virtual de Azure con imágenes de la galería de máquinas virtuales de SQL Server. En este tema usa el modo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (clásico)

Este artículo proporciona los pasos para cómo toocreate una máquina virtual de SQL Server en Azure mediante el uso de Hola cmdlets de PowerShell.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Para la versión del Administrador de recursos de Hola de este tema, consulte [aprovisionar una máquina virtual de SQL Server con el Administrador de recursos de Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Instalación y configuración de PowerShell:
1. Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Descargue e instale los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview).
3. Inicie Windows PowerShell y conectar tooyour suscripción de Azure con hello **Add-AzureAccount** comando.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Determinar su región de Azure de destino

La máquina virtual de SQL Server se hospedará en un servicio en la nube que reside en una región de Azure específica. Hello pasos siguientes ayudarán a toodetermine su región, la cuenta de almacenamiento y el servicio de nube que se usará para el resto de Hola de tutorial de Hola.

1. Determine el centro de datos de Hola que desea toouse toohost la VM de SQL Server. Hola siguiente comando de PowerShell muestra una lista de nombres de las regiones disponibles.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Una vez que haya identificado la ubicación preferida, Establece una variable denominada **$dcLocation** toothat región. Hola, por ejemplo, el siguiente comando establece Hola región demasiado "UU":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Establecimiento de la cuenta de suscripción y almacenamiento

1. Determinar Hola va a utilizar para la nueva máquina virtual de Hola de suscripción de Azure.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Asignar su toohello de suscripción de Azure de destino **$subscr** variable. Establézcala como su suscripción de Azure actual.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Luego busque las cuentas de almacenamiento existentes. Hello secuencia de comandos siguiente muestra todas las cuentas de almacenamiento que existen en su región elegido:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Si necesita una cuenta de almacenamiento, cree primero un nombre de cuenta de almacenamiento de todas las minúsculas con el comando hello AzureStorageAccount de nuevo como en el siguiente ejemplo de Hola:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Asignar toohello de nombre de cuenta de hello destino almacenamiento **$staccount**. A continuación, utilice **Set-AzureSubscription** tooset Hola suscripción y la cuenta de almacenamiento actual.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Seleccionar una imagen de máquina virtual de SQL Server

1. Obtener lista de Hola de imágenes de máquinas virtuales de SQL Server disponibles desde la Galería de Hola. Todas estas imágenes tendrán una propiedad **ImageFamily** que empieza por "SQL". Hola siguiente de consulta muestra hello imagen familia disponibles tooyou que tiene preinstalado de SQL Server.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Cuando encuentre la familia de imágenes de máquina virtual de hello, podría haber varias imágenes publicadas en esta familia. Script siguiente de Hola de uso se toofind hello más reciente publicada imagen nombre de máquina virtual su familia de la imagen seleccionada (como **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Crear la máquina virtual de Hola

Por último, crear máquina virtual de hello con PowerShell:

1. Crear una nube servicio toohost Hola nueva máquina virtual. Tenga en cuenta que también es posible toouse un servicio de nube existente en su lugar. Crear una nueva variable **$svcname** con nombre corto de hello del servicio de nube de Hola.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Especifique el nombre de la máquina virtual de Hola y un tamaño. Para obtener información sobre los tamaños de máquina virtual, consulte [Tamaños de máquina virtual para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Especifique la contraseña y la cuenta de administrador local de Hola.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Ejecute hello después de la máquina virtual de secuencia de comandos toocreate Hola.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Para obtener una explicación adicional y opciones de configuración, vea hello **el conjunto de comandos de compilación** sección [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Script de PowerShell de ejemplo

Hello script siguiente proporciona un ejemplo de un script completo que crea un **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2** máquina virtual. Si utiliza esta secuencia de comandos, debe personalizar variables iniciales Hola basadas en los pasos anteriores hello en este tema.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Conexión con el Escritorio remoto

1. Crear archivos RDP de hello en toolaunch de carpeta de documentos del usuario actual de hello estas máquinas virtuales toocomplete el programa de instalación:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. En el directorio de documentos de hello, inicie el archivo RDP de hello. Conectar con el nombre de usuario de administrador de Hola y la contraseña que proporcionó anteriormente (por ejemplo, si su nombre de usuario era VMAdmin, especifique "\VMAdmin" como usuario de Hola y proporcionar la contraseña de hello).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configuración de hello completa de hello equipo con SQL Server para el acceso remoto

Después de iniciar sesión en la máquina de toohello con Escritorio remoto, configure SQL Server según las instrucciones de hello en [pasos para configurar la conectividad de SQL Server en una máquina virtual de Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Pasos siguientes

Encontrará instrucciones adicionales para el aprovisionamiento de máquinas virtuales con PowerShell en hello [documentación de máquinas virtuales](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

En muchos casos, Hola siguiente paso es toomigrate su toothis de bases de datos nueva VM de SQL Server. Para obtener instrucciones de migración de base de datos, vea [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Si también está interesado en usar hello toocreate portal Azure máquinas virtuales de SQL, vea [aprovisionamiento de una máquina Virtual de SQL Server en Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Tenga en cuenta este tutorial Hola que le guían a través del portal de hello crea máquinas virtuales con los recorridos Hola modelo recomendado de administrador de recursos, en lugar de modelo clásico Hola utilizado en este tema de PowerShell.

Además recursos toothese, le recomendamos que revise [otros temas relacionados con SQL Server en máquinas virtuales Azure toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
