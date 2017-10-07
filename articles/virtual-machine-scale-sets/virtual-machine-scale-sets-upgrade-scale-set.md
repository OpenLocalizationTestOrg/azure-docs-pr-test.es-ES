---
title: "conjunto de aaaUpgrade una escala de la máquina virtual de Azure | Documentos de Microsoft"
description: "Actualización de un conjunto de escalado de máquinas virtuales de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Actualización de un conjunto de escalado de máquinas virtuales
Este artículo describe cómo puede revertir una escala de máquina virtual de Azure tooan de actualización de sistema operativo establecido sin tiempo de inactividad. En este contexto, una actualización del SO implica cambiar versión de Hola o SKU de hello SO u Hola URI de una imagen personalizada. Para actualizar sin tiempos de inactividad, las máquinas virtuales deben actualizarse una a una o en grupos (por ejemplo, un dominio de error a la vez), en lugar de todas a la vez. Al hacerlo, todas las máquinas virtuales que no se estén actualizando siguen funcionando.

tooavoid ambigüedad, vamos a distinguir cuatro tipos de actualización del SO puede tooperform:

* Cambiar la versión de Hola o SKU de una imagen de plataforma. Por ejemplo, cambiar Ubuntu versión 14.04.2-LTS desde 14.04.201506100 too14.04.201507060 o el cambio de hello Ubuntu 15.10 ni la última SKU too16.04.0-LTS/latest. Este escenario se describe en este artículo.
* Cambiar Hola URI que señala tooa nueva versión de una imagen personalizada que se compiló (**propiedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagen** > **uri**). Este escenario se describe en este artículo.
* Cambiar la referencia a imagen Hola de un conjunto de escala que se creó mediante discos de Azure administrados.
* Aplicación de revisiones Hola OS desde dentro de una máquina virtual (ejemplos de esto son instalar una revisión de seguridad y ejecutar Windows Update). Este escenario es posible, pero no se trata en este artículo.

No hablaremos de los conjuntos de escalado de máquinas virtuales que se implementan como parte de un clúster de [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) . Consulte [Aplicación de revisiones del sistema operativo Windows en el clúster de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obtener más información sobre aplicación de revisiones a Service Fabric.

Hola básica Hola de secuencia para cambiar la versión de SO o SKU de una imagen de plataforma u Hola URI de una imagen personalizada tiene el siguiente aspecto:

1. Obtener el modelo de conjunto de escala de hello máquina virtual.
2. Cambiar la versión de hello, SKU, referencia de la imagen o valor URI en el modelo de Hola.
3. Actualizar modelo Hola.
4. Hacer un *manualUpgrade* llamar en máquinas virtuales de hello en el conjunto de escalas de Hola. Este paso solo es pertinente si *upgradePolicy* se establece demasiado**Manual** en la escala de conjunto. Si se establece demasiado**automática**, todas las máquinas virtuales de Hola se actualizan al mismo tiempo, lo que produce el tiempo de inactividad.

Con esta información en mente, veamos cómo puede actualizar versión Hola de una escala establecida en PowerShell y mediante el uso de hello API de REST. Estos ejemplos cubren el caso de hello de una imagen de plataforma, pero en este artículo proporciona información suficiente para tooadapt esta imagen personalizada de proceso tooa.

## <a name="powershell"></a>PowerShell
Este ejemplo actualiza un conjunto de escalas de máquina virtual de Windows (creación toohello nueva versión 4.0.20160229. Después de actualizar el modelo de hello, realiza una actualización de una instancia de máquina virtual a la vez.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Si va a actualizar hello URI para una imagen personalizada en lugar de cambiar una versión de la imagen de plataforma, reemplace Hola "conjunto Hola nueva versión" línea con un comando que se actualizará Hola URI de la imagen de origen. Por ejemplo, si se creó el conjunto de escala de hello sin usar discos de Azure administrados, actualización de hello sería similar al siguiente:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Si una imagen personalizada en función de conjunto de escalas de se creó con discos de Azure administrados, a continuación, la referencia a imagen Hola se actualizaría. Por ejemplo:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Hola API de REST
Aquí se muestran un par de ejemplos de Python que utilizan hello tooroll de API de REST de Azure espera una actualización de versión de sistema operativo. Ambos utilizan ligero hello [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca de API de REST de Azure contenedor funciones toodo una operación GET en escala de hello establece modelo, seguidas por una operación PUT con un modelo actualizado. También examinen en vistas de instancias de máquina virtual tooidentify Hola máquinas virtuales de dominio de actualización.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) es un script de Python que ha usado tooroll espera un tooa de actualización de sistema operativo ejecuta escalas de máquina virtual establece un dominio de actualización a la vez.

![Script vmssupgrade para elegir las máquinas virtuales o un dominio de actualización](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Esta secuencia de comandos le permite elegir tooupdate de máquinas virtuales específicas o especificar un dominio de actualización. Admite cambiar una versión de la imagen de plataforma u Hola URI de una imagen personalizada.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) es un editor general para conjuntos de escalado de máquinas virtuales que muestra el estado estas en un mapa térmico, donde cada fila representa un dominio de actualización. Entre otras cosas, puede actualizar el modelo de Hola para un conjunto de escala con una nueva versión, la SKU o el URI de la imagen personalizada y, a continuación, elija tooupgrade de dominios de error. Al hacer esto, todas las máquinas virtuales de hello en ese dominio de actualización son toohello actualizado nuevo modelo. Como alternativa, puede realizar una actualización gradual basada en el tamaño de lote de Hola de su elección.  

Hello captura de pantalla siguiente muestra un modelo de una escala establecida para Ubuntu 14.04-2LTS versión 14.04.201507060. Muchas más opciones se han agregado toothis herramienta desde que se tomó esta captura de pantalla.

![Modelo de vmsseditor de conjunto de escalado para Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Tras hacer clic en **actualizar** y, a continuación, **obtener los detalles de**, tooupdate de inicio de máquinas virtuales en UD 0.

![Vmsseditor con la actualización en curso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

