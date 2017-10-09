---
title: aaaCreate una copia de un disco administrado de Azure para copia de seguridad | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de un toouse de disco administrado de Azure para volver arriba o hacia la solución de problemas de disco emite."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Creación de una copia de un VHD almacenado como un disco administrado de Azure mediante instantáneas administradas
Crear una instantánea de un disco administrado para copia de seguridad o crear un disco administrado desde la instantánea de Hola y adjuntarlo tootroubleshoot de máquina virtual de prueba tooa. Una instantánea administrada es una copia completa a partir de un momento específico de un disco administrado de VM. Crea una copia de solo lectura del VHD y, de forma predeterminada, se almacena como un Disco administrado estándar. Para más información sobre Managed Disks, consulte [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Introducción a Azure Managed Disks).

Para información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Antes de empezar
Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Copiar Hola VHD con una instantánea
Usar Hola portal de Azure o PowerShell tootake una instantánea de hello disco administrado.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Usar tootake portal Azure una instantánea 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. A partir de la parte superior izquierda de hello, haga clic en **New** y busque **instantánea**.
3. En la hoja de la instantánea de hello, haga clic en **crear**.
4. Escriba un **nombre** para instantáneas de Hola.
5. Seleccione una existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo. 
6. Seleccione una ubicación del centro de datos de Azure.  
7. Para **el disco de origen**, seleccione Hola toosnapshot administrado por disco.
8. Seleccione hello **tipo de cuenta** instantánea de toouse toostore Hola. Se recomienda **Standard_LRS**, a menos que necesite almacenarla en un disco de alto rendimiento.
9. Haga clic en **Crear**.

### <a name="use-powershell-tootake-a-snapshot"></a>Usar PowerShell tootake una instantánea
Hello pasos siguientes muestran cómo tooget Hola VHD disco toobe copiar, crear Hola configuraciones de instantáneas y tomar una instantánea del disco de hello utilizando el cmdlet New-AzureRmSnapshot Hola<!--Add link toocmdlet when available-->. 

1. Configure algunos parámetros. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Reemplace los valores de parámetro hello:
  -  "myResourceGroup" con el grupo de recursos de la máquina virtual de Hola.
  -  "southeastasia" con la ubicación geográfica de Hola donde desea que la instantánea administrados almacenados. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" con el nombre de Hola de disco del disco duro virtual de Hola que desea toocopy.
  -  Nombre de "ContosoMD_datadisk1_snapshot1" con hello desea toouse para la nueva instantánea de Hola.

2. Obtener toobe de disco VHD Hola copiado.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Crear configuraciones de instantáneas de Hola. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Tomar instantánea de Hola.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Si piensa toouse Hola instantánea toocreate un disco administrado y adjuntar una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `-AccountType Premium_LRS` con el comando hello AzureRmSnapshot de nuevo. parámetro Hello crea instantáneas de Hola para que se almacena como un disco de Premium administrados. Managed Disks Premium son más costosos que los Estándar. Por lo tanto, asegúrese de que realmente necesita discos Premium antes de usar el parámetro.


