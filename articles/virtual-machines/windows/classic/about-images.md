---
title: "aaaAbout imágenes para máquinas virtuales de Windows | Documentos de Microsoft"
description: "Obtenga información sobre cómo se usan las imágenes con máquinas virtuales con Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Acerca de las imágenes para máquinas virtuales Windows
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información acerca de cómo buscar y usar imágenes en el modelo de administrador de recursos de hello, consulte [aquí](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Trabajo con imágenes

Puede usar el módulo de PowerShell de Azure de Hola y Hola toomanage portal Azure Hola imágenes disponibles tooyour suscripción de Azure. módulo de Azure PowerShell Hola proporciona más opciones de comando, para que pueda localizar exactamente lo que desea toosee o siga. Hola portal de Azure proporciona una interfaz gráfica de usuario para muchas de las tareas administrativas diarias Hola.

Estos son algunos ejemplos que usan el módulo de Azure PowerShell Hola.

* **Obtener todas las imágenes de**:`Get-AzureVMImage`devuelve una lista de todas las imágenes de hello disponibles en su suscripción actual: las imágenes y las proporcionadas por Azure o sus asociados. lista de Hello resultante puede ser grande. Hola siguiente ejemplos se muestra cómo tooget una lista más corta.
* **Obtener familias de imágenes**: `Get-AzureVMImage | select ImageFamily` obtiene una lista de familias de imágenes mostrando cadenas de propiedad **ImageFamily**.
* **Obtener todas las imágenes de una familia concreta**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Buscar imágenes de máquina virtual**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` este cmdlet funciona mediante el filtrado de la propiedad DataDiskConfiguration de hello, que solo se aplica a imágenes de tooVM. En este ejemplo también filtra hello tooonly Hola label e image nombre de salida.
* **Guardar una imagen generalizada**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Guardar una imagen especializada**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > parámetro de Hello OSState es necesario toocreate una imagen de máquina virtual, lo que incluye el disco del sistema operativo de Hola y discos de datos conectados. Si no utiliza el parámetro hello, Hola cmdlet crea una imagen de sistema operativo. valor de Hola de parámetro hello indica si generalizada o especializada Hola imagen, en función de si se ha preparado el disco del sistema operativo Hola para su reutilización.

* **Eliminar una imagen**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Pasos siguientes
También puede [crear una máquina Windows con el portal de Azure hello](tutorial.md).
