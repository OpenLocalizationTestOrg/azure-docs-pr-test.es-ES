---
title: "aaaCreate una máquina virtual en hello portal de Azure | Documentos de Microsoft"
description: "Crear una máquina virtual Windows Hola portal de Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Crear una máquina virtual que ejecuta Windows en hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](tutorial.md)
> * [PowerShell: implementación clásica](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo de implementación del Administrador de recursos de hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con hello **portal de Azure**.

Este tutorial muestra cómo toocreate una Azure la máquina virtual (VM) ejecuta Windows en hello portal de Azure. Vamos a usar una imagen de Windows Server como un ejemplo, pero que es simplemente una de hello muchas imágenes de Azure ofrece. Tenga en cuenta que las opciones de imagen dependen de su suscripción. Por ejemplo, imágenes de escritorio de Windows pueden ser suscriptores tooMSDN disponible.

Esta sección muestra cómo hello toouse **panel** en Hola tooselect de portal de Azure y, a continuación, crear la máquina virtual de Hola.

También puede crear máquinas virtuales con sus [propias imágenes](createupload-vhd.md). toolearn sobre este y otros métodos, vea [toocreate de distintas formas una máquina virtual Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Crear la máquina virtual de Hola
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[crear una máquina virtual mediante el modelo de implementación del Administrador de recursos de hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Hola portal de Azure.
* Inicie sesión en la máquina virtual de toohello. Para obtener instrucciones, consulte [inicie sesión en la máquina virtual de tooa ejecuta Windows Server](connect-logon.md).
* Adjuntar una toostore de datos de disco. Puede acoplar tanto discos vacíos como discos que contienen datos. Para obtener instrucciones, consulte hello [conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de hello](attach-disk.md).
