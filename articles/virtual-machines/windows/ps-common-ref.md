---
title: "aaaCommon PowerShell comandos máquinas virtuales de Azure | Documentos de Microsoft"
description: "Tooget de comandos de PowerShell comunes se inició la creación y administración de las máquinas virtuales de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Comandos comunes de PowerShell para crear y administrar máquinas virtuales de Azure

En este artículo se trata algunos de hello que comandos de PowerShell de Azure que puede usar toocreate y administrar máquinas virtuales en su suscripción de Azure.  Para obtener más ayuda con las opciones y los modificadores de línea de comandos específicos, puede utilizar el **comando** *Get-Help*.

Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.

Estas variables podrían ser útiles para si ejecuta más de uno de los comandos de hello en este artículo:

- $location - ubicación de Hola de máquina virtual de Hola. Puede usar [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind una [región geográfica](https://azure.microsoft.com/regions/) que se adapte a sus necesidades.
- $myResourceGroup - nombre de Hola Hola del grupo de recursos que contiene la máquina virtual de Hola.
- $myVM - nombre de Hola de máquina virtual de Hola.

## <a name="create-a-vm"></a>Creación de una VM

| Tarea | Get-Help |
| ---- | ------- |
| Creación de una configuración de máquina virtual |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>configuración de máquina virtual de Hello es configuraciones utilizadas de toodefine o actualización para hello máquina virtual. configuración de Hola se inicializa con el nombre de Hola de hello VM y su [tamaño](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Adición de valores de configuración |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>Configuración del sistema operativo incluido [credenciales](https://technet.microsoft.com/library/hh849815.aspx) se agregan el objeto de configuración de toohello que creó previamente mediante New-AzureRmVMConfig. |
| Adición de una interfaz de red |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>Una máquina virtual debe tener un [interfaz de red](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate en una red virtual. También puede usar [AzureRmNetworkInterface Get](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve un objeto de interfaz de red existente. |
| Especificación de una imagen de plataforma |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "nombre_publicador" -Offer "oferta_publicador" -Skus "sku_producto" -Version "más_reciente"<BR></BR><BR></BR>[Información de la imagen](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) se agrega el objeto de configuración de toohello que creó previamente mediante New-AzureRmVMConfig. objeto Hola devuelva este comando sólo se utiliza cuando se establece Hola SO disco toouse una imagen de plataforma. |
| Establecer toouse de disco de sistema operativo de una imagen de plataforma |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>nombre de Hello del disco del sistema operativo hello y su ubicación en [almacenamiento](../../storage/common/storage-powershell-guide-full.md) se agrega el objeto de configuración de toohello que creó anteriormente. |
| Establecer una imagen generalizada de toouse de disco de sistema operativo |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>nombre de Hello del disco del sistema operativo hello, la ubicación de Hola Hola imagen de origen y la ubicación del disco de hello en [almacenamiento](../../storage/common/storage-powershell-guide-full.md) se agrega el objeto de configuración de toohello. |
| Establecer una imagen especializada de toouse de disco de sistema operativo |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| Creación de una VM |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>Todos los recursos se crean en un [grupo de recursos](../../azure-resource-manager/powershell-azure-resource-manager.md). Antes de utilizar este comando, ejecute New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface y Set-AzureRmVMOSDisk. |

## <a name="get-information-about-vms"></a>Obtención de información sobre VM

| Tarea | Comando |
| ---- | ------- |
| Enumeración de las máquinas virtuales de una suscripción |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Enumeración de las máquinas virtuales de un grupo de recursos |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>grupos de una lista de recursos de tooget en su suscripción, utilice [AzureRmResourceGroup Get](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Obtención información acerca de una máquina virtual |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>Administración de máquinas virtuales
| Tarea | Comando |
| --- | --- |
| Inicio de una máquina virtual |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Detención de una máquina virtual |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Reinicio de una máquina virtual en ejecución |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Eliminación de una máquina virtual |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Generalización de una máquina virtual |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>Ejecute este comando antes de ejecutar Save-AzureRmVMImage. |
| Captura de una máquina virtual |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>Una máquina virtual debe estar [preparado, apague y generalizado](prepare-for-upload-vhd-image.md) toocreate toobe usa una imagen. Antes de utilizar este comando, ejecute Set-AzureRmVm. |
| Actualización de una máquina virtual |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Obtener Hola actual configuración de VM con Get-AzureRmVM, cambiar la configuración en el objeto de máquina virtual de hello y, a continuación, ejecute este comando. |
| Agregar un tooa de disco de datos VM |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Usar Get-AzureRmVM tooget Hola VM objeto. Especificar el número LUN de Hola y el tamaño de hello del disco de Hola. Ejecute Update-AzureRmVM tooapply Hola configuración cambios toohello máquina virtual. no se ha inicializado el disco de Hola que agregue. |
| Eliminación de un disco de datos de una máquina virtual |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Usar Get-AzureRmVM tooget Hola VM objeto. Ejecute Update-AzureRmVM tooapply Hola configuración cambios toohello máquina virtual. |
| Agregar una máquina virtual de extensión tooa |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Ejecute este comando con hello adecuado [información de configuración](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) para extensión de Hola que desea tooinstall. |
| Eliminación de una extensión de máquina virtual |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>Pasos siguientes
* Consulte los pasos básicos de Hola para crear una máquina virtual en [crear una máquina virtual de Windows mediante el Administrador de recursos y PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

