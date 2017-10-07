---
title: "establece aaaCreate una disponibilidad de la máquina virtual en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo establece toocreate una disponibilidad administrada o conjunto para sus máquinas virtuales mediante PowerShell de Azure de disponibilidad no administrado u Hola portal en el modelo de implementación del Administrador de recursos de Hola."
keywords: conjunto de disponibilidad
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Aumento de la disponibilidad de máquinas virtuales mediante la creación de un conjunto de disponibilidad de Azure 
Los conjuntos de disponibilidad proporcionan aplicaciones de tooyour de redundancia. Se recomienda agrupar dos máquinas virtuales o más en un conjunto de disponibilidad. Esta configuración garantiza que durante un evento de mantenimiento planeado o no, al menos una máquina virtual estará disponible y cumple Hola 99,95% SLA de Azure. Para obtener más información, vea hello [SLA para las máquinas virtuales](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Las máquinas virtuales se deben crear en hello mismo grupo de recursos como conjunto de disponibilidad de Hola.
> 

Si desea que su parte de toobe de máquina virtual de un conjunto de disponibilidad, deberá disponibilidad de hello toocreate establecer primera o mientras el equipo está creando la primera máquina virtual en el conjunto de Hola. Si la máquina virtual va a utilizar discos administrados, conjunto de disponibilidad de hello debe crearse como un conjunto de disponibilidad administrada.

Para obtener más información sobre cómo crear y utilizar conjuntos de disponibilidad, consulte [administrar Hola disponibilidad de máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Usar Hola portal toocreate un conjunto antes de crear las máquinas virtuales de disponibilidad
1. En el menú del concentrador hello, haga clic en **examinar** y seleccione **conjuntos de disponibilidad**.
2. En hello **hoja de conjuntos de disponibilidad**, haga clic en **agregar**.
   
    ![Captura de pantalla que muestra hello Agregar botón para crear un nuevo conjunto de disponibilidad.](./media/create-availability-set/add-availability-set.png)
3. En hello **crear conjunto de disponibilidad** hoja, la información de hello completa para el conjunto.
   
    ![Captura de pantalla que muestra Hola información que necesita la disponibilidad de hello toocreate tooenter establecido.](./media/create-availability-set/create-availability-set.png)
   
   * **Nombre de** -nombre de hello debe tener caracteres de 1-80 consta de números, letras, puntos, guiones bajos y guiones. Hola primer carácter debe ser una letra o un número. último carácter de Hello debe ser una letra, número o un carácter de subrayado.
   * **Dominios de error** -dominios de error definen grupo Hola de máquinas virtuales que comparten un conmutador de origen y de red común de energía. De forma predeterminada, hello las máquinas virtuales están separadas a través de dominios de error toothree y pueden ser modificado toobetween 1 y 3.
   * **Actualizar dominios** : cinco dominios de actualización se asignan de forma predeterminada y se puede establecer toobetween 1 y 20. Dominios de actualización indican los grupos de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo. Por ejemplo, si se especifica update cinco dominios, cuando más de cinco máquinas virtuales se configuran en un único conjunto de disponibilidad, máquina virtual de la sexta Hola se colocarán en Hola mismo dominio de actualización como máquina virtual de la primera hello, hello séptimo en Hola igual UD como segundo Hola una máquina virtual y así sucesivamente. orden de Hola de hello reinicios no sea secuencial, pero solo una actualización de dominio se reiniciará a la vez.
   * **Suscripción** -seleccione Hola toouse suscripción si tiene más de uno.
   * **Grupo de recursos** -seleccione un grupo de recursos existente haciendo clic en la flecha de Hola y seleccionar un grupo de recursos de Hola de lista desplegable. Otra manera de crear un nuevo grupo de recursos es escribir un nombre. Hello nombre puede contener ninguno de hello siguientes caracteres: letras, números, puntos, guiones, caracteres de subrayado y apertura o paréntesis de cierre. Hola nombre no puede terminar en un período. Todos hello las máquinas virtuales en el grupo de disponibilidad de hello necesitan toobe creado en hello mismo grupo de recursos como conjunto de disponibilidad de Hola.
   * **Ubicación** -seleccionar una ubicación de Hola de lista desplegable.
   * **Administrado** : seleccione esta opción *Sí* toocreate una disponibilidad administrada establece toouse con las máquinas virtuales que usan discos administrados para el almacenamiento. Seleccione **n** si las máquinas virtuales que se incluirán en el conjunto de Hola Hola usa discos de no administrados en una cuenta de almacenamiento.
   
4. Cuando haya terminado de escribir información de hello, haga clic en **crear**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Usar hello toocreate portal una máquina virtual y una disponibilidad establecen en hello mismo tiempo
Si va a crear una nueva máquina virtual mediante el portal de hello, también puede crear un nuevo conjunto de disponibilidad para hello VM mientras crea Hola primera VM en el conjunto de Hola. Si elige discos de toouse administrados para la máquina virtual, se creará un conjunto de disponibilidad administrada.

![Captura de pantalla que muestra el proceso de Hola para crear un nuevo conjunto durante la creación de hello VM de disponibilidad.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Agregar una nueva máquina virtual tooan existente conjunto de disponibilidad en el portal de Hola
Para cada máquina virtual adicional que cree que deben pertenecer en conjunto de Hola, asegúrese de que la cree en Hola mismo **grupo de recursos** y, a continuación, seleccione Hola conjunto en el paso 3 de disponibilidad existente. 

![Captura de pantalla que muestra cómo tooselect un grupo de disponibilidad había establecido toouse para la máquina virtual.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Usar PowerShell toocreate una disponibilidad establecido
Este ejemplo crea un conjunto con nombre de disponibilidad **myAvailabilitySet** en hello **myResourceGroup** grupo de recursos de hello **West US** ubicación. Esta tarea debe toobe hacer antes de crear Hola primera máquina virtual que se incluirán en el conjunto de Hola.

Antes de comenzar, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


Si usa discos administrados para las VM, escriba:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Si usa sus propias cuentas de almacenamiento para las VM, escriba:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Para más información, consulte [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Solución de problemas
* Cuando se crea una máquina virtual, si el conjunto de disponibilidad de Hola que desea no está en la lista desplegable de hello en el portal de Hola puede crearla en otro grupo de recursos. Si desconoce el grupo de recursos de Hola para su disponibilidad establece, vaya el menú del concentrador toohello y haga clic en Examinar > toosee establece una lista de la disponibilidad y los grupos de recursos que pertenecen a conjuntos de disponibilidad.

## <a name="next-steps"></a>Pasos siguientes
Agregar almacenamiento adicional tooyour VM agregando más [disco de datos](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

