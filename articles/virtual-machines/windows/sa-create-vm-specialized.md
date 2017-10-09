---
title: "aaaCreate máquina virtual desde un disco especializado en Azure | Documentos de Microsoft"
description: "Crear una nueva máquina virtual si se adjunta un disco especializado no administrado, en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Crear una máquina virtual a partir de un VHD especializado en una cuenta de almacenamiento

Crear una nueva máquina virtual si se adjunta un disco especializado no administrado como disco del sistema operativo hello mediante Powershell. Un disco especializado es una copia de disco duro virtual de una máquina virtual existente que mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original. 

Tiene dos opciones:
* [Carga de un disco duro virtual](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Copiar Hola VHD de una máquina virtual de Azure existente](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Antes de empezar
Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

```powershell
Install-Module AzureRM.Compute 
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


## <a name="option-1-upload-a-specialized-vhd"></a>Opción 1: Cargar un VHD especializado

Puede cargar Hola que VHD de una máquina virtual especializada creado con una herramienta de virtualización local, como Hyper-V o una máquina virtual exportado desde otra nube.

### <a name="prepare-hello-vm"></a>Preparar Hola VM
Puede cargar un VHD especializado que se haya creado con una máquina virtual local o un VHD exportado desde otra nube. Un disco duro virtual especializado mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original. Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos. 
  
  * [Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **No** generalizar Hola VM con Sysprep.
  * Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (es decir, herramientas de VMware).
  * Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP. Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia. 


### <a name="get-hello-storage-account"></a>Obtener la cuenta de almacenamiento de Hola
Necesita una cuenta de almacenamiento en la imagen de máquina virtual de Azure toostore Hola cargado. Puede usar una cuenta de almacenamiento existente o crear una nueva. 

cuentas de almacenamiento disponibles de hello tooshow, escriba:

```powershell
Get-AzureRmStorageAccount
```

Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [imagen de máquina virtual de carga hello](#upload-the-vm-vhd-to-your-storage-account) sección.

Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:

1. Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola. toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un grupo de recursos denominado **myResourceGroup** Hola **West US** región, escriba:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Crear una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Cargar la cuenta de almacenamiento de hello VHD tooyour
Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola imagen tooa en su cuenta de almacenamiento. En este ejemplo Hola a cargas de archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada **mystorageaccount** en hello **myResourceGroup** grupo de recursos. archivo Hello se colocarán en el contenedor de hello denominado **mycontainer** y nombre de archivo nuevo de hello será **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Si se realiza correctamente, obtendrá una respuesta que busca toothis similar:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Opción 2: Copiar Hola VHD de una máquina virtual de Azure existente

Puede copiar un toouse de cuenta de almacenamiento de disco duro virtual tooanother al crear una máquina virtual nueva y duplicada.

### <a name="before-you-begin"></a>Antes de empezar
Asegúrese de todo esto:

* Tener información sobre hello **cuentas de almacenamiento de origen y destino**. Para hello una VM de origen, deberá toohave Hola cuenta nombres almacenamiento y contenedor. Normalmente, será el nombre del contenedor de hello **discos duros virtuales**. También debe toohave una cuenta de almacenamiento de destino. Si aún no tiene uno, puede crear uno mediante cualquier portal hello (**más servicios** > cuentas de almacenamiento > Agregar) o mediante hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet. 
* Ha descargado e instalado hello [herramienta AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Cancela la asignación de hello VM
Cancela la asignación de hello VM, lo que libera hello toobe de disco duro virtual copiado. 

* **Portal**: haga clic en **Máquinas virtuales** > **myVM** &gt; Detener
* **PowerShell**: Use [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (desasignarlos) Hola máquina virtual denominada **myVM** en grupo de recursos **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Hola **estado** para hello VM en hello Azure portal cambia de **detenido** demasiado**detenido (desasignado)**.

### <a name="get-hello-storage-account-urls"></a>Obtener direcciones URL de cuenta de almacenamiento de Hola
Necesita hello las direcciones URL de cuentas de almacenamiento de origen y destino Hola. Hello direcciones URL aspecto: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Si ya sabe el nombre de cuenta y el contenedor de almacenamiento de hello, simplemente puede reemplazar la dirección URL de información de hello entre Hola corchetes toocreate. 

Puede usar Hola portal de Azure o Azure Powershell tooget Hola URL:

* **Portal de**: haga clic en hello  **>**  para **más servicios** > **cuentas de almacenamiento**  >   *cuenta de almacenamiento* > **Blobs** y el archivo de disco duro virtual de origen es probablemente Hola **discos duros virtuales** contenedor. Haga clic en **propiedades** de contenedor de Hola y con la etiqueta de texto de copia hello **URL**. Necesitará hello las direcciones URL de los contenedores de origen y destino Hola. 
* **PowerShell**: Use [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget información de hello para la máquina virtual denominada **myVM** en grupo de recursos de hello **myResourceGroup**. En los resultados de hello, buscar en hello **perfil de almacenamiento** sección para hello **Uri de Vhd**. Hola primera parte del Uri de hello es contenedor de toohello de dirección URL de Hola y Hola última parte es Hola nombre de disco duro virtual del sistema operativo para hello máquina virtual.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Obtener claves de acceso de almacenamiento de Hola
Buscar claves de acceso de Hola de hello las cuentas de almacenamiento de origen y de destino. Para más información acerca de las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../../storage/common/storage-create-storage-account.md).

* **Portal**: haga clic en **Más servicios** > **Cuentas de almacenamiento** > *cuenta de almacenamiento* > **Claves de acceso**. Clave de copia Hola etiquetada como **key1**.
* **PowerShell**: Use [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Hola almacenamiento clave Hola cuenta de almacenamiento **mystorageaccount** en grupo de recursos de hello  **myResourceGroup**. Clave de hello copia con la etiqueta **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Copiar Hola VHD
Puede copiar archivos entre cuentas de almacenamiento con AzCopy. Para el contenedor de destino de hello, si no existe el contenedor especificado de hello, se creará automáticamente. 

toouse AzCopy, abra un símbolo del sistema en el equipo local y desplazarse por las carpetas de toohello donde está instalado AzCopy. Será similar demasiado*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

toocopy todos Hola archivos dentro de un contenedor, utiliza hello **/S** cambiar. Esto puede ser usado toocopy Hola VHD de sistema operativo y todos los discos de datos de hello si están en Hola mismo contenedor. Este ejemplo se muestra cómo toocopy todos los de hello archivos de contenedor de hello **mysourcecontainer** en la cuenta de almacenamiento **mysourcestorageaccount** toohello contenedor **mydestinationcontainer**  en hello **mydestinationstorageaccount** cuenta de almacenamiento. Reemplazar nombres de Hola de cuentas de almacenamiento de Hola y de contenedores por los suyos propios. Reemplace `<sourceStorageAccountKey1>` y `<destinationStorageAccountKey1>` por sus propias claves.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Si solo desea toocopy un VHD específico en un contenedor con varios archivos, también puede especificar el nombre de archivo de hello mediante el modificador de /Pattern Hola. En este ejemplo, solo Hola archivo denominado **myFileName.vhd** se va a copiar.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Cuando haya finalizado, obtendrá un mensaje parecido a este:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Solución de problemas
* Cuando usas AZCopy, si ve el error de Hola "Servidor no pudo solicitud de hello tooauthenticate", asegúrese de que valor Hola de encabezado de autorización de hello está formado correctamente incluye firma de Hola. Si usas 2 de clave o la clave de almacenamiento secundaria hello, pruebe a usar la clave de almacenamiento principal o el 1 de Hola.

## <a name="create-hello-new-vm"></a>Crear nueva máquina virtual de Hola 

Necesita toocreate redes y otro toobe de recursos de máquina virtual usa Hola nueva máquina virtual.

### <a name="create-hello-subnet-and-vnet"></a>Crear red virtual y subred de Hola

Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).

1. Crear una subred de Hola. Este ejemplo crea una subred denominada **mySubNet**, en el grupo de recursos de hello **myResourceGroup**, y conjuntos de Hola prefijo de dirección de subred demasiado**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crear red virtual de Hola. Este ejemplo establece Hola toobe de nombre de red virtual **myVnetName**, Hola ubicación demasiado**oeste de Estados Unidos**, y Hola prefijo de dirección de red virtual de hello demasiado**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Creación de una dirección IP pública y una NIC
tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.

1. Crear dirección IP pública de Hola. En este ejemplo, nombre de dirección IP pública de Hola se establece demasiado**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Crear NIC de Hola. En este ejemplo, nombre de la NIC de Hola se establece demasiado**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Crear grupo de seguridad de red de hello y una regla de RDP
toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que concede acceso RDP en el puerto 3389. Porque especializados hello VHD para hello que nueva máquina virtual creada a partir de una existente máquina virtual, una vez creado Hola VM puede usar una cuenta existente de la máquina virtual de hello origen que tenía permiso toolog sobre el uso de RDP.
Este ejemplo establece Hola nombre NSG demasiado**myNsg** y nombre de regla Hola RDP demasiado**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Para obtener más información acerca de los puntos de conexión y las reglas NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Establecer nombre de máquina virtual de Hola y el tamaño

En este ejemplo Hola de conjuntos de nombre de máquina virtual demasiado hello VM y "myVM" tamaño demasiado "Standard_A2".
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Agregar Hola NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Configurar el disco de SO Hola

1. URI del conjunto hello para hello VHD que cargado o copiado. En este ejemplo, Hola archivo de disco duro virtual denominado **myOsDisk.vhd** se mantiene en una cuenta de almacenamiento denominada **myStorageAccount** en un contenedor denominado **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Agregar disco de SO Hola. En este ejemplo, cuando se crea el disco del sistema operativo de hello, Hola término "osDisk" es appened toohello VM nombre toocreate Hola SO nombre del disco. En este ejemplo también se especifica que este disco duro virtual basado en Windows debe ser adjunto toohello máquina virtual como disco de SO Hola.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Opcional: Si tiene discos de datos que toobe necesidad adjunta toohello VM, agregue más discos de datos de hello mediante direcciones URL de Hola de VHD de datos y Hola número de unidad lógica (Lun) correspondiente.

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Cuando se usa una cuenta de almacenamiento, datos de Hola y direcciones URL de disco del sistema operativo este aspecto: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. Puede encontrar en el portal de hello examinando el contenedor de almacenamiento de destino de toohello, haga clic en el sistema operativo de Hola o datos del disco duro virtual que se ha copiado, y, a continuación, copiar contenido de hello de la dirección URL de Hola.


### <a name="complete-hello-vm"></a>Completar Hola VM 

Crear Hola VM usando configuraciones de Hola que acaba de crear.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

Si este comando es correcto, verá un resultado similar al siguiente:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Debería ver Hola recién creado máquina virtual en hello [portal de Azure](https://portal.azure.com), en **examinar** > **máquinas virtuales**, o mediante el uso de hello después de PowerShell comandos:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes
toosign en tooyour nueva máquina virtual, examinar toohello VM en hello [portal](https://portal.azure.com), haga clic en **conectar**y el archivo de escritorio remoto RDP Hola abierto. Usar credenciales de cuenta de hello de su toosign de máquina virtual original en la nueva máquina virtual de tooyour. Para obtener más información, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md).

