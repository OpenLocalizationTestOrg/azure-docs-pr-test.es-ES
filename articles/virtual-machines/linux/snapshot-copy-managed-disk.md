---
title: aaaCopy un administrado de Azure en disco para copia de seguridad | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de un toouse de disco administrado de Azure para volver arriba o hacia la solución de problemas de disco emite."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Creación de una copia de un VHD almacenado como un disco administrado de Azure mediante instantáneas administradas
Crear una instantánea de un disco administrado para copia de seguridad o crear un disco administrado desde la instantánea de Hola y adjuntarlo tootroubleshoot de máquina virtual de prueba tooa. Una instantánea administrada es una copia completa a partir de un momento específico de un disco administrado de VM. Crea una copia de solo lectura del VHD y, de forma predeterminada, se almacena como un Disco administrado estándar. 

Para información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Usar cualquier hello tootake de CLI de Azure 2.0 portal o hello Azure una instantánea de hello disco administrado.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Usar Azure CLI 2.0 tootake una instantánea

> [!NOTE] 
> Hello en el ejemplo siguiente se requiere hello Azure CLI 2.0 instalado y registrado en su cuenta de Azure.

Hello pasos siguientes muestran cómo tooobtain y tome una instantánea de un sistema operativo administrado disco mediante hello `az snapshot create` comando con hello `--source-disk` parámetro. Hello en el ejemplo siguiente se supone que existe una máquina virtual denominada `myVM` creado con un disco de sistema operativo administrado de hello `myResourceGroup` grupo de recursos.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

salida de Hello debe ser similar:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Usar tootake portal Azure una instantánea 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. A partir de hello superior izquierda, haga clic en **New** y busque **instantánea**.
3. En la hoja de la instantánea de hello, haga clic en **crear**.
4. Escriba un **nombre** para instantáneas de Hola.
5. Seleccione una existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo. 
6. Seleccione una ubicación del centro de datos de Azure.  
7. Para **el disco de origen**, seleccione Hola toosnapshot administrado por disco.
8. Seleccione hello **tipo de cuenta** instantánea de toouse toostore Hola. Se recomienda **Standard_LRS**, a menos que necesite almacenarla en un disco de alto rendimiento.
9. Haga clic en **Crear**.

Si piensa toouse Hola instantánea toocreate un disco administrado y adjuntar una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `--sku Premium_LRS` con hello `az snapshot create` comando. Esto crea la instantánea de Hola para que se almacena como un disco de Premium administrados. Los Managed Disks Premium tienen un rendimiento mayor porque son discos de estado sólido (SSD), pero cuestan más que los discos estándar (HDD).


