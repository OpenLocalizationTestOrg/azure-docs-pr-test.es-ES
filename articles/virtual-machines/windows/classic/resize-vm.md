---
title: "aaaResize una VM de Windows en el modelo de implementación clásica de hello - Azure | Documentos de Microsoft"
description: "Cambiar el tamaño de una máquina virtual de Windows creada en el modelo de implementación clásica de hello, uso de Powershell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Cambiar el tamaño de una VM de Windows creados en el modelo de implementación clásica de Hola
Este artículo muestra cómo tooresize una VM de Windows, creado en el modelo de implementación clásica de hello mediante Powershell de Azure.

Al considerar Hola capacidad tooresize una máquina virtual, hay dos conceptos que controlan el intervalo de Hola de máquina virtual de los tamaños disponibles tooresize Hola. concepto primera Hello es región hello en el que se implementa la máquina virtual. lista de Hola de tamaños de máquina virtual disponibles en la región está en la ficha de servicios de Hola de página web de hello regiones de Azure. concepto de segundo de Hello es hardware físico Hola hospeda actualmente la máquina virtual. servidores físicos Hola hospeda máquinas virtuales se agrupan en clústeres de hardware físico comunes. método Hello del cambio de tamaño de máquina virtual es diferente en función de si hello deseado nuevo tamaño VM admite clústeres de hardware de hello hospedando Hola máquina virtual.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. También puede [cambiar el tamaño de una máquina virtual que creó en el modelo de implementación del Administrador de recursos de hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Adición de la cuenta
Debe configurar Azure PowerShell toowork con recursos de Azure clásicos. Siga los pasos de hello debajo de PowerShell de Azure tooconfigure toomanage los recursos clásicos.

1. En el símbolo del sistema de PowerShell hello, escriba `Add-AzureAccount` y haga clic en **ENTRAR**. 
2. Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**. 
3. Escribir contraseña de Hola para su cuenta. 
4. Haga clic en **Iniciar sesión**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Cambiar el tamaño en hello mismo clúster de hardware
tooresize un tamaño de tooa de memoria virtual disponible en el clúster de hardware de hello hospedaje Hola de máquina virtual, realice Hola pasos.

1. Ejecute hello siguiente comando de PowerShell Hola de tamaños de máquinas virtuales de hello toolist disponibles en el clúster de hardware de hello hospedaje de servicio de nube de Hola que contiene máquinas virtuales.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Ejecute hello después comandos tooresize Hola máquina virtual.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Cambio de tamaño en un nuevo clúster de hardware
tooresize tooa tamaño no está disponible en el clúster de hardware de hello, que hospeda Hola VM, hello todas las máquinas virtuales en el servicio de nube de Hola y servicio en la nube deben volver a crearse. Cada servicio en la nube se hospeda en un clúster de hardware único para que todas las máquinas virtuales en el servicio de nube de hello deben tener un tamaño que se admite en un clúster de hardware. Hello pasos siguientes describen cómo tooresize una máquina virtual, eliminar y volver a crear a continuación, Hola nube servicio.

1. Ejecute hello después PowerShell comando toolist Hola tamaños de máquina virtual disponibles en la región de Hola. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Tome nota de todos los valores de configuración para cada máquina virtual Hola del servicio en nube que contiene Hola VM toobe cambia de tamaño. 
3. Eliminar todas las máquinas virtuales en el servicio de nube de hello seleccionar discos de hello opción tooretain Hola para cada máquina virtual.
4. Vuelva a crear Hola VM toobe cambiar de tamaño mediante el tamaño de la máquina virtual de hello deseado.
5. Volver a crear todas las demás máquinas virtuales que estaban en el servicio de nube de hello con un tamaño de memoria virtual disponible en el clúster de hardware de hello hospedando, entonces, servicio de nube de Hola.

[Aquí](https://github.com/Azure/azure-vm-scripts) puede encontrar un script de ejemplo para eliminar y volver a crear un servicio en la nube con un nuevo tamaño de máquina virtual. 

## <a name="next-steps"></a>Pasos siguientes
* [Cambiar el tamaño de una máquina virtual que creó en el modelo de implementación del Administrador de recursos de hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

