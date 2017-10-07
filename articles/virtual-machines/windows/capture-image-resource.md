---
title: aaaCreate una imagen administrada en Azure | Documentos de Microsoft
description: "Cree una imagen administrada de un VHD o de una VM generalizada en Azure. Las imágenes puede ser utilizado toocreate varias máquinas virtuales que usan discos administrados."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Captura de una imagen administrada de una máquina virtual generalizada en Azure

Se puede crear un recurso de imagen administrado a partir de una máquina virtual generalizada que se almacena como un disco administrado o como un disco no administrado en una cuenta de almacenamiento. a continuación, Hola imagen puede ser toocreate usa varias máquinas virtuales. 


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


## <a name="create-a-managed-image-in-hello-portal"></a>Crear una imagen administrada en el portal de Hola 

1. Abra hello [portal](https://portal.azure.com).
2. Haga clic en Hola signo toocreate un nuevo recurso.
3. En la búsqueda del filtro de hello, escriba **imagen**.
4. Seleccione **imagen** de resultados de Hola.
5. Hola **imagen** hoja, haga clic en **crear**.
6. En **nombre**, escriba un nombre para la imagen de Hola.
7. Si tiene más de una suscripción, seleccione Hola uno correcto de hello **suscripción** lista desplegable.
7. En **grupo de recursos** seleccione **crear nuevo** y escriba un nombre o seleccione **de existentes** y seleccione un toouse de grupo de recursos de la lista desplegable de Hola.
8. En **ubicación**, Elegir ubicación de Hola de su grupo de recursos.
9. En **tipo de SO** Seleccionar tipo de Hola de sistema operativo Windows o Linux.
11. En **blob de almacenamiento**, haga clic en **examinar** toolook para hello VHD en el almacenamiento de Azure.
12. En **Tipo de cuenta**, elija Standard_LRS o Premium_LRS. Standard utiliza unidades de disco duro y Premium utiliza unidades de estado sólido. Ambas opciones emplean almacenamiento con redundancia local.
13. En **almacenamiento en caché de disco** seleccione Hola opción de caché de disco adecuado. Opciones de Hello son **ninguno**, **de sólo lectura** y **lectura/escritura**.
14. Opcional: También puede agregar una imagen de toohello de disco de datos existente, haga clic en **+ Agregar disco de datos**.  
15. Cuando haya terminado de realizar todas las selecciones, haga clic en **Crear**.
16. Después de crea la imagen de hello, verá como un **imagen** recurso en la lista de Hola de recursos de grupo de recursos de Hola que eligió.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Creación de una imagen administrada de una VM mediante PowerShell

Crear una imagen directamente a partir de hello que VM garantiza esa imagen Hola incluye todos los discos de hello asociados Hola máquina virtual, incluyendo hello disco del sistema operativo y los discos de datos.


Antes de comenzar, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


1. Cree algunas variables.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Asegúrese de hello seguro que se ha desasignado la máquina virtual.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Establecer el estado de saludo de la máquina virtual de hello demasiado**generalizado**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Obtenga la máquina virtual de Hola. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Crear configuración de la imagen de Hola.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Crear imagen de Hola.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Creación de una imagen administrada de un VHD en PowerShell

Cree una imagen administrada con el VHD del SO generalizado.


1.  En primer lugar, establezca los parámetros comunes de hello:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Hola Step\deallocate máquina virtual.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Marcar Hola VM tal y como se ha generalizado.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Crear imagen de hello con el disco duro virtual generalizado de sistema operativo.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Creación de una imagen administrada a partir de una instantánea mediante PowerShell

También puede crear una imagen administrada de una instantánea de hello VHD de una máquina virtual generalizada.

    
1. Cree algunas variables. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Obtener instantáneas de Hola.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Crear configuración de la imagen de Hola.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Crear imagen de Hola.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Pasos siguientes
- Ahora podrá [crear una máquina virtual de imagen administrada Hola generalizado](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

