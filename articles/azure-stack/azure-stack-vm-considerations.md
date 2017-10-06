---
title: "aaaDifferences y consideraciones para las máquinas virtuales en la pila de Azure | Documentos de Microsoft"
description: "Aprenda sobre las diferencias y consideraciones al trabajar con máquinas virtuales en Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/4/2017
ms.author: sngun
ms.openlocfilehash: cee03e3e83b54efabaecd2647ec7defe371ee870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Consideraciones sobre máquinas virtuales en Azure Stack

Las máquinas virtuales son recursos informáticos escalables y a petición que ofrece Azure Stack. Si usa máquinas virtuales, debe saber que existen diferencias entre las características de Hola que están disponibles en Azure y pila de Azure. Este artículo proporciona información general sobre consideraciones únicas de Hola para máquinas virtuales y sus características en la pila de Azure. toolearn acerca de alto nivel diferencias entre la pila de Azure y Azure, vea hello [clave consideraciones](azure-stack-considerations.md) tema.

## <a name="cheat-sheet-virtual-machine-differences"></a>Hoja de referencia rápida: Diferencias entre máquinas virtuales

| Característica | Azure (global) | Azure Stack |
| --- | --- | --- |
| Imágenes de máquinas virtuales | Hello Azure Marketplace contiene imágenes que se puede usar toocreate una máquina virtual. Vea hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) lista de páginas tooview Hola de imágenes que están disponibles en hello Azure Marketplace. | De forma predeterminada, no hay ninguna imagen disponible en marketplace de Azure pila Hola. Administrador de la nube de Hello Azure pila debe [publicar](azure-stack-add-default-image.md) o [descargar imágenes](azure-stack-download-azure-marketplace-item.md) toohello marketplace de pila de Azure antes de que los usuarios puedan usarlos. |
| Tamaños de máquina virtual | Azure admite una amplia variedad de tamaños para máquinas virtuales. toolearn acerca de los tamaños disponibles de Hola y las opciones, consulte toohello [tamaños de máquinas virtuales de Windows](../virtual-machines/virtual-machines-windows-sizes.md) y [tamaños de máquina virtual Linux](../virtual-machines/linux/sizes.md) temas. | Azure Stack admite un subconjunto de tamaños de máquinas virtuales que están disponibles en Azure. lista de hello tooview de tamaños admitidos, consulte toohello [tamaños de máquina virtual](#virtual-machine-sizes) sección de este artículo. |
| Cuotas de máquinas virtuales | [Límites de cuota](../azure-subscription-service-limits.md#service-specific-limits) establecidos por Microsoft | Administrador de la nube de Hello Azure pila debe [asignar cuotas](azure-stack-setting-quotas.md) antes de que ofrecen a los usuarios de máquinas virtuales tootheir. |
| Extensiones de máquina virtual |Azure admite una amplia variedad de extensiones para máquinas virtuales. toolearn sobre las extensiones disponibles hello, consulte toohello [extensiones de máquina virtual y las características](../virtual-machines/windows/extensions-features.md) tema.| Pila de Azure admite un subconjunto de las extensiones que están disponibles en Azure y de extensión de hello tienen versiones específicas. Administrador de la pila de Azure nube Hola puede elegir qué toobe extensiones realiza toofor disponible a los usuarios. lista de hello tooview de extensiones admitidas, consulte toohello [extensiones de máquina virtual](#virtual-machine-extensions) sección de este artículo. |
| Red de máquinas virtuales | Direcciones IP públicas asignadas tootenant virtual machine son accesibles a través de Internet de Hola.<br><br><br>Azure Virtual Machines tiene un nombre de DNS fijo | Direcciones IP públicas asignadas tooa las máquinas virtuales están accesibles desde el entorno del Kit de desarrollo de pila de Azure de hello exclusivamente. El usuario debe tener acceso toohello Kit de desarrollo de pila de Azure a través de [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) máquina virtual de tooconnect tooa que se crea en la pila de Azure.<br><br>Máquinas virtuales creadas dentro de una instancia específica de la pila de Azure tienen un nombre DNS basado en valor de hello configurada por el Administrador de la nube de Hola. |
| Almacenamiento de máquina virtual | Admite [discos administrados](../virtual-machines/windows/managed-disks-overview.md). | Los discos administrados no se admiten todavía en Azure Stack. |
| Versiones de API | Azure siempre tiene Hola últimas versiones de API para todas las características de la máquina virtual de Hola. | Azure Stack es compatible con servicios específicos de Azure y versiones de API específicas para estos servicios. lista de hello tooview de admite versiones de API, consulte toohello [versiones de API](#api-versions) sección de este artículo. |
|Conjuntos de disponibilidad de máquinas virtuales|Varios dominios de error (2 o 3 por región)<br>Varios dominios de actualización<br>Compatible con el disco administrado|Dominio de error único<br>Dominio actualizado único<br>No compatible con el disco administrado|
|Conjuntos de escalado de máquinas virtuales|Compatible con escalado automático|No compatible con escalado automático.<br>Agregar varios conjuntos de escala de tooa instancias mediante el portal de hello, plantillas de administrador de recursos o PowerShell.

## <a name="virtual-machine-sizes"></a>Tamaños de máquina virtual 

Hola Kit de desarrollo de pila de Azure admite Hola después tamaños: 

| Tipo | Tamaño | Intervalo de tamaños admitidos |
| --- | --- | --- |
|Uso general |A básico|A0-A4|
|Uso general |Estándar A|A0-A7|
|Uso general |Estándar D|D1-D4|
|Uso general |Estándar Dv2|D1v2-D5v2|
|Memoria optimizada|Serie D|D11-D14|
|Memoria optimizada |Serie Dv2|D11v2-D14v2|

Tamaños de máquina virtual en la pila de Azure y Azure son coherentes en cuanto a memoria hello, núcleos de CPU, ancho de banda de red, el rendimiento del disco y otros factores que definen el tamaño de Hola. Por ejemplo, D estándar de máquina virtual Hola tamaño de pila de Azure y Azure es coherente. 

## <a name="virtual-machine-extensions"></a>Extensiones de máquina virtual 

 Hola Kit de desarrollo de pila de Azure admite Hola siguientes versiones de extensiones de máquina virtual:

![Extensiones de máquina virtual](media/azure-stack-vm-considerations/vm-extensions.png)

Usar hello PowerShell script tooget Hola lista de extensiones de máquina virtual que están disponibles en su entorno de Azure pila siguiente:

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>Versiones de API 

Características de la máquina virtual en el Kit de desarrollo de pila de Azure admiten Hola siguientes versiones de API:

![Tipos de recursos de máquinas virtuales](media/azure-stack-vm-considerations/vm-resoource-types.png)

Puede usar Hola siguientes versiones de API de PowerShell script tooget Hola para las características de la máquina virtual de Hola que están disponibles en el entorno de pila de Azure:

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
lista de Hola de admite tipos de recursos y versiones de API pueden variar si el operador de la nube de hello actualiza la versión más reciente de Azure pila entorno tooa.

## <a name="next-steps"></a>Pasos siguientes

[Cree una máquina virtual Windows con PowerShell en Azure Stack](azure-stack-quick-create-vm-powershell.md)
