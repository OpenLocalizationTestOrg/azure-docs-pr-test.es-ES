---
title: "Inicio rápido de Azure: creación de máquinas virtuales con la CLI Microsoft Docs"
description: "Aprenda rápidamente a crear una máquina virtual Windows con la CLI de Azure."
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
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a>Creación de una máquina virtual Windows con la CLI de Azure

La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts. Esta guía se detalla cómo usar la CLI de Azure para implementar máquinas virtuales con Windows Server 2016.  Una vez completada la implementación, nos conectaremos al servidor e instalaremos IIS.


Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior. Ejecute `az --version` para encontrar la versión. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Cree un grupo de recursos con [az group create](/cli/azure/group#create). Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Crear máquina virtual

Cree la máquina virtual con [az vm create](/cli/azure/vm#create). 

En el ejemplo siguiente se crea una máquina virtual denominada *myVM*. En este ejemplo se utiliza *azureuser* como nombre de usuario administrativo y *myPassword12* como contraseña. Actualice estos valores a un valor apropiado para su entorno. Estos valores son necesarios cuando se crea una conexión con la máquina virtual.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Cuando se ha creado la máquina virtual, la CLI de Azure muestra información similar al ejemplo siguiente. Anote el valor de `publicIpAaddress`. Esta dirección se utiliza para tener acceso a la máquina virtual.

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

De forma predeterminada, solo se permiten conexiones RDP con las máquinas virtuales Windows implementadas en Azure. Si esta máquina virtual va a ser un servidor web, debe abrir el puerto 80 desde Internet. Use el comando [az vm open-port](/cli/azure/vm#open-port) para abrir el puerto deseado.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a>Conexión a la máquina virtual

Ejecute el comando siguiente para crear una sesión del Escritorio remoto con la máquina virtual. Reemplace la dirección IP con la dirección IP pública de la máquina virtual. Cuando se le solicite, escriba las credenciales usadas al crear la máquina virtual.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Instalación de IIS mediante PowerShell

Ahora que ha iniciado sesión en la máquina virtual de Azure, puede usar una sola línea de PowerShell para instalar IIS y habilitar la regla de firewall local para permitir el tráfico web. Abra una ventana de PowerShell y ejecute el siguiente comando:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a>Página principal de IIS

Con IIS instalado y el puerto 80 abierto en la máquina virtual desde Internet, puede usar el explorador web que elija para ver la página principal de IIS. Asegúrese de utilizar la dirección IP pública que ha anotado antes para visitar la página predeterminada. 

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no se necesiten, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web. Para más información acerca de las máquinas virtuales de Azure, continúe con el tutorial de máquinas virtuales Windows.

> [!div class="nextstepaction"]
> [Tutoriales de máquinas virtuales Windows de Azure](./tutorial-manage-vm.md)
