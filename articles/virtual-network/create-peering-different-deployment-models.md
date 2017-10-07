---
title: "aaaCreate un virtual de Azure de red emparejamiento - diferentes modelos de implementación - misma suscripción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un emparejamiento de red virtual entre redes virtuales creados a través de modelos de implementación de Azure diferentes que existen en hello mismo suscripción de Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Creación de un emparejamiento de red virtual: distintos modelos de implementación, la misma suscripción 

En este tutorial, aprenderá toocreate una emparejamiento entre redes virtuales creadas a través de diferentes modelos de implementación de red virtual. Ambas redes virtuales residen en hello misma suscripción. Emparejamiento dos redes virtuales permite recursos en diferentes redes virtuales toocommunicate entre sí con Hola mismo ancho de banda y latencia como si estuvieran recursos Hola Hola misma red virtual. Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md). 

Hello pasos toocreate un emparejamiento de red virtual son diferentes, dependiendo de si son redes virtuales de hello en hello iguales o distinto, suscripciones y que [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello las redes virtuales se crean a través de. Obtenga información acerca de cómo toocreate un virtual red emparejamiento en otros escenarios, haga clic en el escenario de Hola de hello en la tabla siguiente:

|Modelo de implementación de Azure  | Suscripción de Azure  |
|--------- |---------|
|[Ambas mediante Resource Manager](virtual-network-create-peering.md) |Iguales|
|[Ambas mediante Resource Manager](create-peering-different-subscriptions.md) |Diferentes|
|[Una mediante Resource Manager y la otra clásica](create-peering-different-deployment-models-subscriptions.md) |Diferentes|

No se puede crear un intercambio de tráfico de red virtual entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola. Un intercambio de tráfico de red virtual solo puede crearse entre dos redes virtuales que existen en hello misma región de Azure. Si necesita tooconnect las redes virtuales que se crearon a través del modelo de implementación clásica de hello, o que existen en diferentes regiones de Azure, puede usar un Azure [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hola redes virtuales. 

Puede usar hello [portal de Azure](#portal), hello Azure [interfaz de línea de comandos](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un emparejamiento de red virtual. Haga clic en cualquiera de hello anterior herramienta vínculos toogo directamente toohello los pasos para crear un intercambio de tráfico de red virtual mediante la herramienta de elección.

## <a name="cli"></a>Creación de emparejamiento: portal

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
2. Haga clic en **+ Nuevo**, **Redes** y, luego, en **Red virtual**.
3. Hola **crear red virtual** hoja, escriba, o seleccionar los valores de hello después de la configuración, haga clic en **crear**:
    - **Nombre**: *myVnet1*
    - **Espacio de direcciones**: *10.0.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.0.0.0/24*
    - **Suscripción**: seleccione la suscripción
    - **Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroup*
    - **Ubicación**: *este de EE. UU.*
4. Haga clic en **+ Nuevo**. Hola **Hola búsqueda Marketplace** , escriba *red Virtual*. Haga clic en **red Virtual** cuando aparece en los resultados de búsqueda de Hola. 
5. Hola **red Virtual** hoja, seleccione **clásico** en hello **seleccionar un modelo de implementación** cuadro y, a continuación, haga clic en **crear**.
6. Hola **crear red virtual** hoja, escriba, o seleccionar los valores de hello después de la configuración, haga clic en **crear**:
    - **Nombre**: *myVnet2*
    - **Espacio de direcciones**: *10.1.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.1.0.0/24*
    - **Suscripción**: seleccione la suscripción
    - **Grupo de recursos**: seleccione **Usar existente** y seleccione *myResourceGroup*
    - **Ubicación**: *este de EE. UU.*
7. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myResourceGroup*. Haga clic en **myResourceGroup** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myresourcegroup** grupo de recursos. grupo de recursos de Hello contiene Hola dos redes virtuales creadas en los pasos anteriores.
8. Haga clic en **myVNet1**.
9. Hola **myVnet1** hoja que aparece, haga clic en **emparejamientos** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.
10. Hola **myVnet1 - emparejamientos** hoja que aparece, haga clic en **+ agregar**
11. Hola **agregar emparejamiento** hoja que aparece, escriba, o seleccione Hola siguientes opciones, haga clic en **Aceptar**:
     - **Nombre**: *myVnet1ToMyVnet2*
     - **Modelo de implementación de red virtual**: seleccione **Clásico**. 
     - **Suscripción**: seleccione la suscripción
     - **Red virtual**: haga clic en **Elegir una red virtual** y, luego, en **myVnet2**.
     - **Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.
    En este tutorial no se usa ninguna otra configuración. leer toolearn sobre todas las opciones de intercambio de tráfico, [administrar emparejamientos de red virtual](virtual-network-manage-peering.md#create-a-peering).
12. Tras hacer clic en **Aceptar** en el paso anterior de hello, Hola **agregar emparejamiento** hoja se cierra y vea hello **myVnet1 - emparejamientos** hoja de nuevo. Después de unos segundos, Hola emparejamiento que ha creado aparece en la hoja de Hola. **Conectado** aparece en hello **estado EMPAREJAMIENTO** columna para hello **myVnet1ToMyVnet2** emparejamiento se creó.

    Ahora se establece el emparejamiento de Hola. Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
14. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete-portal) sección de este artículo.

## <a name="cli"></a>Creación de emparejamiento: CLI de Azure

1. [Instalar](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) red virtual de hello Azure CLI 1.0 toocreate Hola (clásico).
2. Abra una sesión de comandos e inicie sesión tooAzure con hello `azure login` comando.
3. Ejecute hello CLI en modo de administración de servicio escribiendo hello `azure config mode asm` comando.
4. Escriba Hola siguiente comando toocreate Hola red virtual (clásica):
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Cree un grupo de recursos y una red virtual (Resource Manager). Puede usar Hola CLI 1.0 o 2.0 ([instalar](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). En este tutorial, Hola CLI 2.0 es red virtual de toocreate usado hello (Administrador de recursos), ya que 2.0 debe ser usado toocreate Hola emparejamiento. Ejecute hello siguiente bash secuencias de comandos CLI desde el equipo local con hello CLI 2.0.4 o posterior instalado. Para opciones de ejecución bash secuencias de comandos CLI en el cliente de Windows, consulte [ejecuta Hola CLI de Azure en Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). También puede ejecutar el script de Hola mediante Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Haga clic en hello **Pruébelo** botón en el script de Hola que se indica a continuación, que invoca un Shell en la nube que registra se puede iniciar sesión en tooyour cuenta de Azure con. tooexecute hello secuencia de comandos, haga clic en hello **copia** botón y pegar, contenido de hello en el comando de Shell en la nube, a continuación, presione `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Crear una red virtual emparejamiento entre Hola dos redes virtuales creadas a través de hello diferentes modelos de implementación. Copie Hola después de editor de texto de script tooa en su PC. Reemplace `<subscription id>` con el Id. de suscripción. Si no conoce el Id. de suscripción, escriba Hola `az account show` comando. Hola valor para **identificador** Hola salida es el identificador de suscripción. Pegue el script de Hola modificado en la sesión CLI tooyour y, a continuación, presione `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Después de ejecuta el script de Hola, revise el emparejamiento hello para la red virtual de hello (Administrador de recursos). Copia Hola comando siguiente, péguelo en la sesión CLI y, a continuación, presione `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hola resultado muestra **conectado** en hello **PeeringState** columna. 

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
9. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.

## <a name="powershell"></a>Creación de emparejamiento: PowerShell

1. Instale Hola la versión más reciente de hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) y [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulos. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie una sesión de PowerShell.
3. En PowerShell, inicie sesión en tooAzure escribiendo hello `Add-AzureAccount` comando.
4. toocreate una red virtual (clásica) con PowerShell, debe crear un nuevo, o modificar una existente, el archivo de configuración de red. Obtenga información acerca de cómo demasiado[exportar, actualizar e importar archivos de configuración de red](virtual-networks-using-network-configuration-file.md). Hello archivo debe incluir siguiente hello **VirtualNetworkSite** , elemento de red virtual de hello usada en este tutorial:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar un archivo de configuración de red modificado puede provocar cambios tooexisting redes virtuales (clásicas) en su suscripción. Asegúrese de sólo agregar red virtual anterior de Hola y que no cambiar o quitar cualquier red virtual existente de su suscripción. 
5. Inicie sesión en la red virtual de tooAzure toocreate Hola (Administrador de recursos) mediante la especificación de hello `login-azurermaccount` comando. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
6. Cree un grupo de recursos y una red virtual (Resource Manager). Copie el script de Hola, péguela en PowerShell y, a continuación, presione `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Crear una red virtual emparejamiento entre Hola dos redes virtuales creadas a través de hello diferentes modelos de implementación. Copie Hola después de editor de texto de script tooa en su PC. Reemplace `<subscription id>` con el Id. de suscripción. Si no conoce el Id. de suscripción, escriba Hola `Get-AzureRmSubscription` tooview comando lo. Hola valor para **identificador** Hola devuelve el resultado es el identificador de suscripción. script de Hola tooexecute, Hola copia modifica script desde el editor de texto, a continuación, haga clic en la sesión de PowerShell y, a continuación, presione `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Después de ejecuta el script de Hola, revise el emparejamiento hello para la red virtual de hello (Administrador de recursos). Copia Hola comando siguiente, péguelo en la sesión de PowerShell y, a continuación, presione `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hola resultado muestra **conectado** en hello **PeeringState** columna.

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
10. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.
 
## <a name="permissions"></a>Permisos

cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos. Por ejemplo, si se emparejamiento dos redes virtuales denominadas myVnet1 y myVnet2, su cuenta se debe asignar Hola después de función mínima o los permisos para cada red virtual:
    
|Red virtual|Modelo de implementación|Rol|Permisos|
|---|---|---|---|
|myVnet1|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnet2|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).

## <a name="delete"></a>Eliminación de recursos
Cuando haya terminado este tutorial, conviene toodelete recursos de Hola que creó en el tutorial de hello, por lo que no se incurre en cargos por uso. Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.

### <a name="delete-portal"></a>Azure Portal

1. En el cuadro de búsqueda del portal de hello, escriba **myResourceGroup**. En los resultados de la búsqueda de hello, haga clic en **myResourceGroup**.
2. En hello **myResourceGroup** hoja, haga clic en hello **eliminar** icono.
3. eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroup**y, a continuación, haga clic en **eliminar**.

### <a name="delete-cli"></a>Azure CLI

1. Usar red virtual de hello Azure CLI 2.0 toodelete Hola (Administrador de recursos) con hello siguiente comando:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Usar red virtual de Hola de toodelete de hello 1.0 de CLI de Azure (clásica) con hello siguientes comandos:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Escriba Hola siguiente comando toodelete Hola (Administrador de recursos) de red virtual:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete Hola red virtual (clásica) con PowerShell, debe modificar un archivo de configuración de red existente. Obtenga información acerca de cómo demasiado[exportar, actualizar e importar archivos de configuración de red](virtual-networks-using-network-configuration-file.md). Quitar Hola siguiente elemento VirtualNetworkSite de red virtual de hello usada en este tutorial:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar un archivo de configuración de red modificado puede provocar cambios tooexisting redes virtuales (clásicas) en su suscripción. Asegúrese de solo quitar red virtual anterior de Hola y que no cambia o quita otras redes virtuales existentes de la suscripción. 

## <a name="next-steps"></a>Pasos siguientes

- Conozca en profundidad las [restricciones y comportamientos importantes del emparejamiento de redes virtuales](virtual-network-manage-peering.md#requirements-and-constraints) antes de crear un emparejamiento de redes virtuales para su uso en el entorno de producción.
- Conozca toda la [configuración de emparejamiento de redes virtuales](virtual-network-manage-peering.md#create-a-peering).
- Obtenga información acerca de cómo demasiado[crear un concentrador y radio de la topología de red](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con intercambio de tráfico de red virtual.
