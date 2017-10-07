---
title: aaaCreate una VM de Linux en Azure desde una plantilla | Documentos de Microsoft
description: "¿Cómo toouse Hola CLI de Azure 2.0 toocreate una VM de Linux desde una plantilla de administrador de recursos"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>¿Cómo toocreate una máquina virtual de Linux con plantillas del Administrador de recursos de Azure
Este artículo muestra cómo tooquickly implementar una máquina virtual de Linux (VM) con hello Azure CLI 2.0 y plantillas del Administrador de recursos de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Introducción a las plantillas
Plantillas de administrador de recursos de Azure son archivos JSON que definen la infraestructura de Hola y la configuración de la solución de Azure. Mediante una plantilla, puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente. toolearn más información acerca del formato de Hola de plantilla de Hola y cómo se crea, consulte [crear la primera plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Hola tooview sintaxis de JSON para los tipos de recursos, consulte [definir los recursos en las plantillas de Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Creación de un grupo de recursos
Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. Se debe crear un grupo de recursos antes de una máquina virtual. Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupVM* en hello *eastus* región:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine
Hello en el ejemplo siguiente se crea una máquina virtual desde [esta plantilla de Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) con [Crear implementación de grupo az](/cli/azure/group/deployment#create). Proporcionar valor Hola de su propia clave pública SSH, como contenido de Hola de *~/.ssh/id_rsa.pub*. Si necesita toocreate un par de claves de SSH, consulte [cómo toocreate y use un SSH par de claves para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

En este ejemplo, especificó una plantilla almacenada en GitHub. También puede descargar o crear una plantilla y especificar la ruta de acceso local de hello con hello mismo `--template-file` parámetro.

tooSSH tooyour VM, obtener dirección IP pública de hello con [show de public-ip de red az](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

A continuación puede SSH tooyour VM como normal:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, creó una máquina virtual Linux básica. Para obtener más plantillas de administrador de recursos que incluyen marcos de aplicaciones o crear entornos más complejos, examinar hello [Galería de plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).
