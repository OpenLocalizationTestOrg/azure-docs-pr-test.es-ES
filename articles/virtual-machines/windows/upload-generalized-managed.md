---
title: aaaCreate una VM de Azure administrado desde un VHD local generalizado | Documentos de Microsoft
description: "Cargar un tooAzure de disco duro virtual generalizado y usar toocreate nuevas máquinas virtuales, en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Cargar un disco duro virtual generalizado y usar toocreate nuevas máquinas virtuales en Azure

Este tema le guía a través mediante PowerShell tooupload un VHD de un tooAzure generalizado de VM, cree una imagen de hello VHD y crear una nueva máquina virtual desde esa imagen. Puede cargar un VHD exportado de una herramienta de visualización local o desde otra nube. Usar [discos administrados](managed-disks-overview.md) para hello nueva máquina virtual simplifica la administración de máquinas virtuales de Hola y proporciona una mejor disponibilidad Hola VM se coloca en un conjunto de disponibilidad. 

Si desea toouse un script de ejemplo, vea [tooupload tooAzure de un disco duro virtual de secuencia de comandos de ejemplo y crear una nueva máquina virtual](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Antes de empezar

- Antes de cargar cualquier tooAzure de disco duro virtual, debe seguir [preparar una tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Revisión [planear la migración de Hola de discos tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) antes de iniciar la migración demasiado[discos administrados](managed-disks-overview.md).
- Asegúrese de que tiene Hola versión más reciente de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalizar Hola VM de Windows con Sysprep

Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).

Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep. Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si está ejecutando Sysprep antes de cargar su tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep. 
> 
> 

1. Inicie sesión en toohello máquina virtual de Windows.
2. Abra la ventana de símbolo del sistema de hello como administrador. Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.
3. Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.
4. En **Opciones de apagado**, seleccione **Apagar**.
5. Haga clic en **Aceptar**.
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Cuando Sysprep finalice, se apaga máquina virtual de Hola. No se reinician Hola máquina virtual.



## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure
Si aún no tiene PowerShell versión 1.4 o posterior instalado, leer [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

1. Abra PowerShell de Azure e inicie sesión tooyour cuenta de Azure. Abre una ventana emergente para tooenter sus credenciales de cuenta de Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Obtener identificadores de suscripción de Hola para las suscripciones disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Conjunto Hola suscripción correcta con el identificador de suscripción de Hola. Reemplace  *<subscriptionID>*  con el Id. de Hola de hello corregir la suscripción.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Obtener la cuenta de almacenamiento de Hola
Necesita una cuenta de almacenamiento en la imagen de máquina virtual de Azure toostore Hola cargado. Puede usar una cuenta de almacenamiento existente o crear una nueva. 

Si va a usar Hola VHD toocreate un disco administrado para una máquina virtual, ubicación hello de la cuenta de almacenamiento debe indicarlo Hola donde creará Hola VM.

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

    toocreate un grupo de recursos denominado **myResourceGroup** en hello **UU** región, escriba:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Crear una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Los valores válidos para - SkuName son los siguientes:
   
   * **Standard_LRS**: Almacenamiento con redundancia local. 
   * **Standard_ZRS**: Almacenamiento con redundancia de zona.
   * **Standard_GRS**: Almacenamiento con redundancia geográfica. 
   * **Standard_RAGRS**: Almacenamiento con redundancia geográfica con acceso de lectura. 
   * **Premium_LRS**: Almacenamiento con redundancia local premium. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Cargar la cuenta de almacenamiento de hello VHD tooyour

Hola de uso [AzureRmVhd agregar](https://msdn.microsoft.com/library/mt603554.aspx) contenedor cmdlet tooupload Hola VHD tooa en su cuenta de almacenamiento. En este ejemplo Hola a cargas de archivo *myVHD.vhd* de *"discos duros de C:\Users\Public\Documents\Virtual\"*  tooa cuenta de almacenamiento denominada *mystorageaccount*Hola *myResourceGroup* grupo de recursos. archivo Hello se colocarán en el contenedor de hello denominado *mycontainer* y nombre de archivo nuevo de hello será *myUploadedVHD.vhd*.

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

Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete

Guardar hello **URI de destino** toouse de ruta de acceso más adelante si va toocreate un disco administrado o una nueva máquina virtual con hello carga VHD.

### <a name="other-options-for-uploading-a-vhd"></a>Otras opciones para cargar un disco duro virtual
 
 
También puede cargar una cuenta de almacenamiento de disco duro virtual tooyour mediante uno de hello siguientes:

- [AzCopy](http://aka.ms/downloadazcopy)
- [API de tipo Copy Blob de Almacenamiento Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Blobs de carga de Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)
- [Referencia de la API de REST de servicios de importación y exportación de almacenamiento](https://msdn.microsoft.com/library/dn529096.aspx)
-   Se recomienda utilizar el servicio Import/Export si se calcula que el tiempo de carga va a ser superior a siete días. Puede usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tiempo de Hola de unidad de tamaño y la transferencia de datos. 
    Importación/exportación puede ser usar cuenta de almacenamiento estándar tooa toocopy. Necesitará toocopy de cuenta de almacenamiento de almacenamiento estándar toopremium mediante una herramienta como AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Crear un administrado imagen de hello cargar VHD 

Cree una imagen administrada con el VHD del SO generalizado. Reemplace los valores de hello con su propia información.


1.  En primer lugar, establezca los parámetros comunes de hello:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Crear imagen de hello con el disco duro virtual generalizado de sistema operativo.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Crear una red virtual
Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).

1. Crear una subred de Hola. Este ejemplo crea una subred denominada *mySubnet* con prefijo de dirección de hello *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crear red virtual de Hola. Este ejemplo crea una red virtual denominada *myVnet* con prefijo de dirección de hello *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Creación de una dirección IP y una interfaz de red

tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.

1. Cree una dirección IP pública. Este ejemplo crea una dirección IP pública denominada "*myPip*". 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Crear NIC de Hola. Este ejemplo crea una NIC denominada "**myNic**". 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Crear grupo de seguridad de red de hello y una regla de RDP

toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad de red (NSG) que permite el acceso RDP en el puerto 3389. 

Este ejemplo crea un NSG denominado"*myNsg*" que contiene una regla llamada "*myRdpRule*" que permita el tráfico RDP en el puerto 3389. Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Cree una variable para la red virtual de Hola

Cree una variable para la red virtual de hello completado. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obtener las credenciales de Hola Hola VM

Hello siguiente cmdlet abrirá una ventana donde se incluirá un nuevo toouse de nombre y la contraseña de usuario como cuenta de administrador local de Hola de tengan acceso remoto a Hola VM. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Agregar nombre de máquina virtual de Hola y de configuración de máquina virtual de tamaño toohello.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Imagen de máquina virtual de hello conjunto como imagen de origen para hello nueva máquina virtual

Establecer la imagen de origen de hello con el Id. de Hola de imagen de VM de hello administrado.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Establecer la configuración del sistema operativo hello y agregue NIC de Hola.

Escriba el tipo de almacenamiento de hello (PremiumLRS o StandardLRS) y el tamaño de Hola de disco del sistema operativo Hola. Este ejemplo establece el tipo de cuenta de hello demasiado*PremiumLRS*, Hola demasiado de tamaño de disco*128 GB* y disco, almacenamiento en caché demasiado*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Crear hello VM

Crear nueva máquina virtual con configuración de hello almacenado en Hola de hello **$vm** variable.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes

toosign en tooyour nueva máquina virtual, examinar toohello VM en hello [portal](https://portal.azure.com), haga clic en **conectar**y el archivo de escritorio remoto RDP Hola abierto. Usar credenciales de cuenta de hello de su toosign de máquina virtual original en la nueva máquina virtual de tooyour. Para obtener más información, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

