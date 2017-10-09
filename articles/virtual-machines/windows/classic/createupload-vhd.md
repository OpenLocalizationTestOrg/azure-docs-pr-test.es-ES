---
title: "las imágenes aaaCreate y carga una máquina virtual mediante Powershell | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate y cargar una imagen generalizada de Windows Server (VHD) mediante el modelo de implementación clásica de Hola y Powershell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Crear y cargar un VHD de Windows Server tooAzure
Este artículo muestra cómo tooupload su propio generalizada imágenes de máquina virtual como un disco duro virtual (VHD) por lo que puede usar máquinas virtuales de toocreate. Para más información sobre discos y VHD en Microsoft Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. También puede [cargar](../upload-generalized-managed.md) una máquina virtual mediante el modelo de administrador de recursos de Hola.

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ya dispones de:

* **Una suscripción a Azure** : si no tiene una, puede [abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -tienen Hola Microsoft Azure PowerShell módulo instalado y configurado toouse su suscripción.
* **UN ARCHIVO. Archivo de disco duro virtual** : almacenado en un archivo .vhd y la máquina virtual de tooa adjunto de sistema operativo de Windows compatibles. Compruebe toosee si los roles de servidor hello con hello VHD son compatibles con Sysprep. Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)(Compatibilidad de Sysprep con roles de servidor).

    > [!IMPORTANT]
    > no se admite el formato VHDX Hello en Microsoft Azure. Puede convertir el formato de tooVHD de disco hello mediante el Administrador de Hyper-V o hello [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Para obtener más información, consulta esta [publicación de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Paso 1: Preparar el disco duro virtual de Hola
Antes de cargar hello tooAzure de disco duro virtual, debe toobe generalizado con la herramienta Sysprep de Hola. Esto prepara Hola VHD toobe utilizado como una imagen. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx). Respaldar Hola VM antes de ejecutar Sysprep.

En la máquina virtual Hola Hola sistema operativo se instaló para completar Hola siguiendo el procedimiento:

1. Inicie sesión en el sistema operativo de toohello.
2. Abra una ventana del símbolo del sistema como administrador. Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.

    ![Abrir una ventana de símbolo del sistema](./media/createupload-vhd/sysprep_commandprompt.png)
3. Hola **herramienta de preparación del sistema** aparece el cuadro de diálogo.

   ![Iniciar Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. Hola **herramienta de preparación del sistema**, seleccione **escriba sistema fuera de cuadro de experiencia de configuración rápida (OOBE)** y asegúrese de que **generalizar** está activada.
5. En **Opciones de apagado**, seleccione **Apagar**.
6. Haga clic en **Aceptar**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Paso 2: Crear una cuenta de almacenamiento y un contenedor
Necesita una cuenta de almacenamiento de Azure para tener un archivo .vhd de lugar tooupload Hola. Este paso muestra cómo toocreate una cuenta o get Hola información que necesita de una cuenta existente. Reemplace las variables de hello en &lsaquo; corchetes &rsaquo; con su propia información.

1. Inicio de sesión

    ```powershell
    Add-AzureAccount
    ```

2. Establezca su suscripción a Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Cree una cuenta de almacenamiento nueva. Hola nombre de cuenta de almacenamiento de hello debe ser único, 3 y 24 caracteres. nombre de Hello puede ser cualquier combinación de letras y números. También debe toospecify una ubicación como "Este nosotros"

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Predeterminar nueva cuenta de almacenamiento Hola Hola.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Cree un contenedor nuevo.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Paso 3: Cargar archivo .vhd de hello
Hola de uso [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello tooupload disco duro virtual.

Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba lo siguiente Hola comando y reemplace las variables de hello en &lsaquo; corchetes &rsaquo; con su propia información.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Paso 4: Agregar lista de hello imágenes tooyour de imágenes personalizadas
Hola de uso [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) lista cmdlet tooadd Hola imagen toohello de sus imágenes personalizadas.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Pasos siguientes
Ahora puede [crear una máquina virtual personalizada](createportal.md) utilizando hello de la imagen que ha cargado.
