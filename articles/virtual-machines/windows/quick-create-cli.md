---
title: "aaaAzure inicio rápido: crear Windows VM CLI | Documentos de Microsoft"
description: "Aprender toocreate rápidamente una máquina virtual de Windows con hello CLI de Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Crear una máquina virtual de Windows con hello CLI de Azure

Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía se detalla con hello Azure CLI toodeploy una máquina virtual ejecuta Windows Server 2016. Una vez completada la implementación, se conecte toohello servidor e instale IIS.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Cree un grupo de recursos con [az group create](/cli/azure/group#create). Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

Cree la máquina virtual con [az vm create](/cli/azure/vm#create). 

Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*. Este ejemplo se utiliza *azureuser* para un nombre de usuario administrativo y *myPassword12* como contraseña de Hola. Actualice estos entorno de valores toosomething tooyour adecuado. Estos valores son necesarios cuando se crea una conexión con la máquina virtual de Hola.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. Tome nota de hello `publicIpAaddress`. Esta dirección es hello tooaccess usa máquinas virtuales.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Apertura del puerto 80 para el tráfico web 

De forma predeterminada, solo las conexiones RDP se permiten en tooWindows las máquinas virtuales implementadas en Azure. Si esta máquina virtual va toobe un servidor Web, deberá tooopen puerto 80 de hello Internet. Hola de uso [az de vm abrir puerto](/cli/azure/vm#open-port) comando tooopen hello deseado puerto.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola. Reemplace la dirección IP de Hola por dirección IP pública de saludo de la máquina virtual. Cuando se le solicite, escriba credenciales de hello usadas al crear la máquina virtual de Hola.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Instalación de IIS mediante PowerShell

Ahora que ha iniciado en toohello máquina virtual de Azure, puede usar una sola línea de PowerShell tooinstall IIS y permitir el tráfico de web de tooallow de regla de hello firewall local. Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando de hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Hola de vista Página de bienvenida de IIS

Con IIS instalado y el puerto 80 ahora abierta en la máquina virtual de hello Internet, puede usar un explorador web de la página de bienvenida de IIS de elección tooview Hola predeterminado. Ser seguro toouse Hola dirección IP pública que documentó anteriormente página predeterminada de toovisit Hola. 

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web. toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Windows.

> [!div class="nextstepaction"]
> [Tutoriales de máquinas virtuales Windows de Azure](./tutorial-manage-vm.md)
