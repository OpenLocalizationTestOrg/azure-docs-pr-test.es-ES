---
title: "imágenes de máquina virtual personalizadas aaaCreate con hello CLI de Azure | Documentos de Microsoft"
description: "Tutorial: crear una imagen de máquina virtual personalizada con hello CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Crear una imagen personalizada de una máquina virtual de Azure con hello CLI

Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo. Imágenes personalizadas pueden ser configuraciones toobootstrap usado como carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo. En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure. Aprenderá a:

> [!div class="checklist"]
> * Desaprovisionar y generalizar máquinas virtuales
> * Crear una imagen personalizada
> * Crear una imagen personalizada a partir de una máquina virtual
> * Una lista de todas las imágenes de hello en su suscripción
> * Eliminar una imagen


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de empezar

Hola los pasos siguientes detalla cómo tootake una máquina virtual existente y a su vez en un personalizado reutilizable de la imagen que pueden usar toocreate nuevas instancias de máquina virtual.

ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente. Si es necesario, este [script de ejemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) puede crear una. Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.

## <a name="create-a-custom-image"></a>Crear una imagen personalizada

toocreate una imagen de una máquina virtual, deberá tooprepare Hola VM, desaprovisionamiento, desasignar y, a continuación, marcando una VM como generalizado de origen Hola. Una vez Hola que se ha preparado la máquina virtual, puede crear una imagen.

### <a name="deprovision-hello-vm"></a>Desaprovisionar Hola VM 

Desaprovisionamiento generaliza Hola VM mediante la eliminación de información específica de la máquina. Esta generalización hace posible toodeploy muchas máquinas virtuales desde una sola imagen. Durante la cancelación del aprovisionamiento, nombre de host de Hola se restablece demasiado*localhost.localdomain*. También se eliminan las claves de host SSH, las configuraciones de servidor de nombres, la contraseña raíz y las concesiones DHCP almacenadas en caché.

Hola toodeprovision máquina virtual, use el agente de máquina virtual de Azure de hello (waagent). agente de máquina virtual de Azure de Hola se instala en hello VM y administra el aprovisionamiento e interactuar con hello controlador de tejido de Azure. Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](agent-user-guide.md).

Conectar tooyour VM mediante SSH y ejecución Hola comando toodeprovision Hola máquina virtual. Con hello `+user` argumento, la última cuenta de usuario aprovisionado hello y ningún dato asociado también se elimina. Reemplace la dirección IP de ejemplo de Hola con dirección IP pública de saludo de la máquina virtual.

SSH toohello máquina virtual.
```bash
ssh azureuser@52.174.34.95
```
Desaprovisionar Hola máquina virtual.

```bash
sudo waagent -deprovision+user -force
```
Cerrar sesión de SSH Hola.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Cancelar la asignación y marcar Hola VM como generalizado

toocreate una imagen, Hola VM debe toobe desasignado. Cancela la asignación de hello VM con [cancelar la asignación de máquina virtual az](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Por último, establecer estado de Hola de hello VM tal y como se ha generalizado con [az vm generalizar](/cli//azure/vm#generalize) para que sepa de hello plataforma Windows Azure Hola VM se haya generalizado. Solo se puede crear una imagen de una máquina virtual generalizada.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Crear imagen de Hola

Ahora puede crear una imagen de máquina virtual de hello mediante [crear imagen az](/cli//azure/image#create). Hello en el ejemplo siguiente se crea una imagen denominada *myImage* desde una máquina virtual denominada *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Crear máquinas virtuales de la imagen de Hola

Ahora que tiene una imagen, puede crear una o varias nuevas máquinas virtuales de hello imágenes mediante [crear vm az](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMfromImage* de imagen de hello denominada *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Administración de imágenes 

Estos son algunos ejemplos de tareas de administración de imágenes comunes y cómo toocomplete mediante Hola CLI de Azure.

Una lista de todas las imágenes por nombre en un formato de tabla.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Elimine una imagen. Este ejemplo elimina Hola imagen denominada *myOldImage* de hello *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado una imagen de máquina virtual personalizada. Ha aprendido a:

> [!div class="checklist"]
> * Desaprovisionar y generalizar máquinas virtuales
> * Crear una imagen personalizada
> * Crear una imagen personalizada a partir de una máquina virtual
> * Una lista de todas las imágenes de hello en su suscripción
> * Eliminar una imagen

Avanzar toohello toolearn de tutorial siguiente sobre máquinas virtuales de alta disponibilidad.

> [!div class="nextstepaction"]
> [Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).

