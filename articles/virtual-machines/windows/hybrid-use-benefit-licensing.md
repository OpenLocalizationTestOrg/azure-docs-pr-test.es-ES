---
title: "aaaAzure híbrido ventaja de uso para cliente de Windows y Windows Server | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomaximize su toobring de ventajas de Windows Software Assurance local licencias tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Ventaja de uso híbrido de Azure para Windows Server y cliente de Windows
Para los clientes con Software Assurance, ventaja de uso de Azure híbrida permite toouse sus licencias de Windows Server y cliente de Windows local y las máquinas de virtuales de Windows ejecución en Azure a bajo costo. La ventaja de uso híbrido de Azure para Windows Server incluye Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 y Windows Server 2016. Ventaja de uso híbrido de Azure para cliente de Windows incluye Windows 10. Para obtener más información, vea hello [página licencias de beneficio de uso de Azure híbrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure híbrida uso ventajas para cliente de Windows está actualmente en vista previa con imagen de Windows 10 de hello en hello Azure Marketplace. Solo los clientes de Enterprise con Windows 10 Enterprise E3/E5 por usuario o VDA de Windows por usuario (licencias de suscripción de usuario o licencias de suscripción de usuario de complemento) ("licencias aplicables") son válidos.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Formas toouse ventaja de usar híbrida de Azure
Hay un par de maneras toodeploy máquinas virtuales de Windows con hello ventaja de usar híbrida de Azure:

1. Puede implementar máquinas virtuales a partir de [imágenes concretas de Marketplace](#deploy-a-vm-using-the-azure-marketplace) preconfiguradas con la ventaja de uso híbrido de Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 SP1.
2. Puede [cargar una máquina virtual personalizada](#upload-a-windows-vhd) e [implementar mediante una plantilla de Resource Manager](#deploy-a-vm-via-resource-manager) o [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Implementar una máquina virtual mediante hello Azure Marketplace
Las imágenes siguientes están disponibles en hello Marketplace configurado previamente con la ventaja de usar híbrida de Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008SP1. Estas imágenes se pueden implementar directamente de hello portal de Azure, las plantillas de administrador de recursos o Azure PowerShell.

Puede implementar estas imágenes directamente desde Hola portal de Azure. Para su uso en las plantillas de administrador de recursos y con Azure PowerShell, vea lista Hola de imágenes de la siguiente manera:

Para Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter versión 2016.127.20170406 o superior

- 2012-R2-Datacenter versión 4.127.20170406 o superior

- 2012-Datacenter versión 3.127.20170406 o superior

- 2008-R2-SP1 versión 2.127.20170406 o superior

Para cliente de Windows:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Carga de un VHD de Windows Server
toodeploy una VM de Windows Server en Azure, primero debe toocreate un disco duro virtual que contiene la compilación de Windows base. Este disco duro virtual debe estar preparado correctamente a través de Sysprep para poder cargar tooAzure. También puede [leer más acerca de los requisitos de disco duro virtual de Hola y el proceso de Sysprep](upload-generalized-managed.md) y [compatibilidad con Sysprep para Roles de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Respaldar Hola VM antes de ejecutar Sysprep. 

Asegúrese de que tiene [instalado y está configurado hello más reciente Azure PowerShell](/powershell/azure/overview). Una vez que ha preparado el disco duro virtual, cargarlo Hola VHD tooyour almacenamiento de Azure cuenta con hello `Add-AzureRmVhd` cmdlet como sigue:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server y Dynamics también pueden utilizar una concesión de licencias de Software Assurance. Imagen de Windows Server tooprepare Hola todavía es necesario al instalar los componentes de aplicación y proporciona las claves de licencia según corresponda y, a continuación, cargar tooAzure de imagen de disco de Hola. Revise la documentación adecuada de Hola para ejecutar Sysprep con la aplicación, como [consideraciones para instalar SQL Server con Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) o [generar una imagen de referencia de SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

También puede obtener más información [Hola VHD tooAzure proceso de carga](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Implementación de una máquina virtual a través de una plantilla de Resource Manager
En las plantillas de Resource Manager, se puede especificar un parámetro adicional para `licenseType` . En [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md), puede encontrar más información al respecto. Una vez que tenga su tooAzure VHD cargado, modificar, el Administrador de recursos tooinclude Hola licencia tipo de plantilla como parte del programa Hola a proveedor de proceso e implementar la plantilla de forma habitual:

Para Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Para con la imagen de Marketplace de Azure solo pueden ser toouse de cliente de Windows:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Implementación de una máquina virtual a través del inicio rápido de PowerShell
Cuando se implementa una máquina virtual de Windows Server mediante PowerShell, se dispone de un parámetro adicional para `-LicenseType`. Una vez que tenga su tooAzure VHD cargado, crear una VM con `New-AzureRmVM` y especificar el tipo de licencia de hello como sigue:

Para Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Para con la imagen de Marketplace de Azure solo pueden ser toouse de cliente de Windows:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

También puede [leer un tutorial más detallado sobre la implementación de una máquina virtual en Azure a través de PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) siguiente o leer una guía más descriptiva en Hola pasos diferentes demasiado[crear una máquina virtual de Windows mediante el Administrador de recursos y PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Compruebe que la máquina virtual está utilizando la ventaja de licencias de Hola
Una vez que se ha implementado la máquina virtual a través de PowerShell de Hola o método de implementación del Administrador de recursos, comprobar el tipo de licencia de hello con `Get-AzureRmVM` como se indica a continuación:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Hola de salida es similar toohello siguiente ejemplo para Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Este resultado se compara con las Hola que VM siguiente implementa sin licencias ventaja de usar híbrida de Azure, como una máquina virtual implementada directamente desde Hola Galería de Azure:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Tutorial de implementación de PowerShell detallado
siguiente Hola había detallada mostrar pasos de PowerShell una implementación completa de una máquina virtual. Puede leer más contexto como cmdlets real toohello y diferentes componentes que se creen en [crear una máquina virtual de Windows mediante el Administrador de recursos y PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Con estos pasos, crea el grupo de recursos, la cuenta de almacenamiento y las redes virtuales, definirá la máquina virtual y, por último, la creará.

En primer lugar, obtenga credenciales de forma segura, establezca una ubicación y defina un nombre para el grupo de recursos:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Cree una dirección IP pública:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Defina la subred, la NIC y la red virtual:

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

Asigne un nombre a la máquina virtual y cree una configuración de máquina virtual:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Defina el sistema operativo:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Agregue su toohello NIC virtual:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Definir toouse de cuenta de almacenamiento de hello:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Cargar un VHD, preparado adecuadamente y asociar tooyour máquina virtual para su uso:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Finalmente, cree la máquina virtual y definir Hola licencias tipo tooutilize ventaja de usar híbrida de Azure:

Para Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Implemente un conjunto de escalado de máquinas virtuales con una plantilla de Resource Manager
En las plantillas de Resource Manager del conjunto de escalado de máquinas virtuales, se puede especificar un parámetro adicional para `licenseType`. En [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md), puede encontrar más información al respecto. Editar la propiedad Resource Manager plantilla tooinclude Hola licenseType como parte de virtualMachineProfile del conjunto de escalas de Hola e implementar la plantilla como normal: vea el ejemplo siguiente utiliza la imagen de Windows Server 2016:


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> Próximamente estará disponible la compatibilidad para implementar un conjunto de escalado de máquinas virtuales con ventajas AHUB a través de PowerShell y otras herramientas SDK.
>

## <a name="next-steps"></a>Pasos siguientes
Más información sobre las [ventajas del uso híbrido de Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Más información sobre el [uso de plantillas de Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Obtenga más información sobre [ventaja de usar híbrida de Azure y Azure Site Recovery Asegúrese de migración de aplicaciones tooAzure aún más rentable](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
