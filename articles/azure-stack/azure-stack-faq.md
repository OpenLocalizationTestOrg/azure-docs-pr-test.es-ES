---
title: "aaaFrequently pila Azure preguntas más frecuentes | Documentos de Microsoft"
description: "Pila Azure preguntas más frecuentes."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a>Pila de Azure preguntas más frecuentes
## <a name="deployment"></a>Implementación
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a>¿Necesito tooformat Mis discos de datos antes de iniciar o reiniciar una instalación?
Discos deben estar en formato sin procesar. Si reinstala el sistema operativo de hello, puede necesita toocheck si el bloque de almacenamiento antiguo Hola aún está presente y eliminar con hello pasos:

1. Abra el Administrador del servidor.
2. Seleccione los grupos de almacenamiento.
3. Vea si aparece un bloque de almacenamiento.
4. Haga clic en **bloque de almacenamiento** si aparece y habilitar la lectura / escritura.
5. Haga clic en **disco duro Virtual** (esquina inferior izquierda) y seleccione Eliminar.
6. Haga clic en **Storage Pool** y haga clic en eliminar.
7. Vuelva a iniciar el script de la pila de Azure y compruebe que supere la comprobación de disco de Hola.

Si lo desea, puede utilizarse Hola siguiente secuencia de comandos:

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a>¿Puedo usar todos los discos SSD para bloque de almacenamiento de Hola Hola instalación de prueba de concepto?
Para obtener más información sobre las configuraciones de almacenamiento, vea hello [requisitos guía](azure-stack-deploy.md).

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a>¿Puedo usar discos de datos de NVMe para hello prueba de concepto de pila de Microsoft Azure?
Mientras que espacios de almacenamiento directo admite discos de NVMe, pila de Azure solo admite un subconjunto de los tipos de unidad posibles hello y combinaciones posibles para espacios de almacenamiento directo.  Vea hello [requisitos guía](azure-stack-deploy.md) para obtener más información. 

### <a name="how-can-i-reinstall-azure-stack"></a>¿Cómo puedo volver a instalar la pila de Azure?
Puede seguir los pasos de Hola Hola [guía reimplementación](azure-stack-redeploy.md).  

## <a name="tenant"></a>Inquilino
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a>¿Puedo implementar Mis propio imágenes como inquilino?
Sí, al igual que en Azure, un inquilino puede cargar imágenes en la pila de Azure, además imágenes de hello toousing de hello Administrador de servicios. Para obtener información general, vea hello [agregar una imagen de máquina virtual](azure-stack-add-vm-image.md). 

## <a name="testing"></a>Prueba
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a>¿Puedo usar hello de la virtualización anidada tootest prueba de concepto de pila de Microsoft Azure?
La virtualización anidada no se admite o no se probó con Azure pila Technical Preview 3.

## <a name="virtual-machines"></a>Máquinas virtuales
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a>¿Azure pila admite discos dinámicos para las máquinas virtuales?
Pila de Azure no admite discos dinámicos.


## <a name="next-steps"></a>Pasos siguientes
[Solución de problemas](azure-stack-troubleshooting.md)

