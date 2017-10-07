---
title: "Discos de datos conectados de máquina Virtual escala conjuntos aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse adjuntar discos de datos con conjuntos de escalas de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Conjuntos de escalado de máquinas virtuales de Azure y discos de datos conectados
Los [conjuntos de escalado de máquinas virtuales](/azure/virtual-machine-scale-sets/) de Azure ahora son compatibles con máquinas virtuales con discos de datos conectados. Discos de datos se pueden definir en el perfil de almacenamiento de Hola para conjuntos de escala que se han creado con discos de Azure administrados. Anteriormente hello únicas opciones de almacenamiento directamente conectado disponibles con las máquinas virtuales en conjuntos de escalas eran unidad Hola sistema operativo y unidades temporales.

> [!NOTE]
>  Cuando se crea una escala establecida con discos de datos adjuntos definidos, todavía necesita toomount y Hola formato discos desde dentro de una máquina virtual toouse ellos (al igual que para máquinas virtuales de Azure independiente). Una manera cómoda de toodo es toouse una extensión de script personalizado que llama a una secuencia de comandos estándar toopartition y dar formato a todos los discos de datos de hello en una máquina virtual.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Creación de un conjunto de escalado con discos de datos conectados
Un toocreate de forma sencilla una escala configurada con discos conectados es hello de toouse [CLI de Azure](https://github.com/Azure/azure-cli) _vmss crear_ comando. Hola de ejemplo siguiente crea un grupo de recursos de Azure y un conjunto de escala de la máquina virtual de 10 Ubuntu máquinas virtuales, cada uno con discos de datos adjuntos 2, de 50 GB y 100 GB, respectivamente.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Tenga en cuenta que hello _vmss crear_ ciertos valores de configuración si no los especifica valores predeterminados de comando. toosee Hola opciones disponibles que puede invalidar try:
```bash
az vmss create --help
```
Incluir otro toocreate de manera que una escala establecida con discos de datos adjuntos es toodefine una escala establecida en una plantilla de Azure Resource Manager, un _dataDisks_ sección Hola _storageProfile_e implementar Hola plantilla. Hola 50 y 100 GB disco ejemplo anterior se definiría como esta plantilla hello:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Puede ver un ejemplo completo, listo toodeploy de una plantilla de conjunto de escala con un disco conectado definido aquí: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Agregar una escala existente de datos disco tooan conjunto
> [!NOTE]
>  Sólo se puede asociar el conjunto de escala de tooa de discos de datos que se ha creado con [discos de Azure administrados](./virtual-machine-scale-sets-managed-disks.md).

Puede agregar una escala de VM tooa de disco de datos establecida mediante Azure CLI _adjuntar disco de az vmss_ comando. Asegúrese de que especifica un valor de lun que ya no esté en uso. Hola CLI ejemplo siguiente agrega un toolun de unidad de 50 GB 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Hola PowerShell ejemplo siguiente agrega un toolun de unidad de 50 GB 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Diferentes tamaños de máquinas virtuales tienen distintos límites en números de Hola de unidades adjuntas que admiten. Comprobar hello [características de tamaño de máquina virtual](../virtual-machines/windows/sizes.md) antes de agregar un nuevo disco.

También puede agregar un disco mediante la adición de un nuevo toohello entrada _dataDisks_ propiedad Hola _storageProfile_ de una escala establece definición y aplicar cambios de Hola. tootest, buscar una definición de conjunto de escala existente en hello [Explorador de recursos de Azure](https://resources.azure.com/). Seleccione _modificar_ y agregar una nueva lista de toohello de disco de los discos de datos. Por ejemplo, uso de ejemplo de Hola anterior:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

A continuación, seleccione _colocar_ tooapply Hola cambia el conjunto de escalas de tooyour. Este ejemplo podría funcionar siempre y cuando se utilice un tamaño de máquina virtual que admite más de dos discos de datos conectados.

> [!NOTE]
> Cuando realice definición como agregar o quitar un disco de datos del conjunto de una escala de tooa de cambio, se aplica a las máquinas virtuales de tooall recién creado, pero solo se aplica tooexisting las máquinas virtuales si hello _upgradePolicy_ propiedad se establece demasiado "automática". Si se establece demasiado "Manual", debe toomanually aplicar Hola nuevo modelo tooexisting máquinas virtuales. Para hacer esto en el portal de hello, con hello _actualización AzureRmVmssInstance_ PowerShell comando, o mediante hello _az vmss update-instancias_ comando de CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Agregar conjunto de escalas existente de tooan de discos de datos rellenada previamente 
> Al agregar discos tooan existente conjunto de escalado de modelo, por diseño, disco de hello siempre se pueden crear vacío. Este escenario también incluye nuevas instancias creadas por conjunto de escalas de Hola. Este comportamiento es porque la definición de scaleset hello tiene un disco de datos vacía. En orden toocreate unidades de datos rellenada previamente para un modelo de conjunto de escala existente, puede elegir cualquiera de las dos opciones siguientes:

* Copiar datos de discos de datos de hello instancia 0 VM toohello Hola otras máquinas virtuales mediante la ejecución de un script personalizado.
* Crea una imagen administrada con disco Hola SO más disco de datos (con datos de hello necesaria) y cree un nuevo scaleset con imagen Hola. Esta manera cada nueva máquina virtual creado tendrá un datos en disco que se proporciona en la definición de Hola de hello scaleset. Puesto que esta definición hará referencia tooan imagen con un disco de datos que ha personalizado datos, cada máquina virtual en hello scaleset automáticamente aparecerá con estos cambios.

> Hola toocreate de manera que una imagen personalizada se puede encontrar aquí: [crear una imagen administrada de una VM generalizada en Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> Hello usuario necesita toocapture Hola instancia 0 de máquina virtual que ha Hola datos necesarios y, a continuación, usar ese archivo vhd para la definición de la imagen de Hola.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Supresión de un disco de datos de un conjunto de escalado
Puede quitar un disco de datos de un conjunto de escalado de la máquina virtual mediante el comando _az vmss disk detach_ de la CLI de Azure. Por ejemplo hello comando siguiente quita Hola disco definido en el lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
De igual forma también puede quitar un disco de una escala establecida mediante la eliminación de una entrada de hello _dataDisks_ propiedad Hola _storageProfile_ y aplicar cambios de Hola. 

## <a name="additional-notes"></a>Notas adicionales
Soporte para discos de datos adjuntos del conjunto de discos administrados de Azure y la escala está disponible en la versión de API [ _2016-04-30-versión preliminar_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) o una versión posterior de hello Microsoft.Compute API.

En implementación inicial de Hola de soporte técnico de disco conectado para conjuntos de escalas, no se puede conectar o desconectar discos de datos de máquinas virtuales individuales en un conjunto de escala.

La compatibilidad con Azure Portal para discos de datos conectados en los conjuntos de escalado está limitada inicialmente. Dependiendo de los requisitos que se puede usar plantillas de Azure, toomanage CLI, PowerShell, SDK y API de REST de los discos conectados.


