---
title: "aaaCreate un emparejamiento de red virtual de Azure - Administrador de recursos - misma suscripción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un emparejamiento de red virtual entre redes virtuales creado mediante el Administrador de recursos que existen en hello misma suscripción de Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Creación de un emparejamiento de redes virtuales: Resource Manager, misma suscripción

En este tutorial, aprenderá toocreate una emparejamiento entre redes virtuales creadas mediante el Administrador de recursos de red virtual. Ambas redes virtuales residen en hello misma suscripción. Emparejamiento dos redes virtuales permite recursos en diferentes redes virtuales toocommunicate entre sí con Hola mismo ancho de banda y latencia como si estuvieran recursos Hola Hola misma red virtual. Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md). 

Hello pasos toocreate un emparejamiento de red virtual son diferentes, dependiendo de si son redes virtuales de hello en hello iguales o distinto, suscripciones y que [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello las redes virtuales se crean a través de. Obtenga información acerca de cómo toocreate un virtual red emparejamiento en otros escenarios, haga clic en el escenario de Hola de hello en la tabla siguiente:

|Modelo de implementación de Azure  | Suscripción de Azure  |
|--------- |---------|
|[Ambas mediante Resource Manager](create-peering-different-subscriptions.md) |Diferentes|
|[Una mediante Resource Manager y la otra, clásico](create-peering-different-deployment-models.md) |Iguales|
|[Una mediante Resource Manager y la otra, clásico](create-peering-different-deployment-models-subscriptions.md) |Diferentes|

No se puede crear un intercambio de tráfico de red virtual entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola. Un intercambio de tráfico de red virtual solo puede crearse entre dos redes virtuales que existen en hello misma región de Azure. Si necesita tooconnect las redes virtuales que se crearon a través del modelo de implementación clásica de hello, o que existen en diferentes regiones de Azure, puede usar un Azure [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hola redes virtuales. 

Puede usar hello [portal de Azure](#portal), hello Azure [interfaz de línea de comandos](#cli) (CLI), Azure [PowerShell](#powershell), o un [plantilla de Azure Resource Manager](#template) toocreate un emparejamiento de red virtual. Haga clic en cualquiera de hello anterior herramienta vínculos toogo directamente toohello los pasos para crear un intercambio de tráfico de red virtual mediante la herramienta de elección.

## <a name="portal"></a>Creación de emparejamiento: Azure Portal

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
4. Complete los pasos 2 y 3, vuelva a especificar Hola después los valores en el paso 3:
    - **Nombre**: *myVnet2*
    - **Espacio de direcciones**: *10.1.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.1.0.0/24*
    - **Suscripción**: seleccione la suscripción
    - **Grupo de recursos**: seleccione **Usar existente** y seleccione *myResourceGroup*
    - **Ubicación**: *este de EE. UU.*
5. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myResourceGroup*. Haga clic en **myResourceGroup** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myresourcegroup** grupo de recursos. grupo de recursos de Hello contiene Hola dos redes virtuales creadas en los pasos anteriores.
6. Haga clic en **myVNet1**.
7. Hola **myVnet1** hoja que aparece, haga clic en **emparejamientos** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.
8. Hola **myVnet1 - emparejamientos** hoja que aparece, haga clic en **+ agregar**
9. Hola **agregar emparejamiento** hoja que aparece, escriba, o seleccione Hola siguientes opciones, haga clic en **Aceptar**:
     - **Nombre**: *myVnet1ToMyVnet2*
     - **Modelo de implementación de red virtual**: seleccione **Resource Manager**. 
     - **Suscripción**: seleccione la suscripción
     - **Red virtual**: haga clic en **Elegir una red virtual** y, luego, en **myVnet2**.
     - **Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.
    En este tutorial no se usa ninguna otra configuración. leer toolearn sobre todas las opciones de intercambio de tráfico, [administrar emparejamientos de red virtual](virtual-network-manage-peering.md#create-a-peering).
10. Tras hacer clic en **Aceptar** en el paso anterior de hello, Hola **agregar emparejamiento** hoja se cierra y vea hello **myVnet1 - emparejamientos** hoja de nuevo. Después de unos segundos, Hola emparejamiento que ha creado aparece en la hoja de Hola. **Inicia** aparece en hello **estado EMPAREJAMIENTO** columna para hello **myVnet1ToMyVnet2** emparejamiento se creó. Ha emparejar tooVnet2 Vnet1, pero ahora debe del mismo nivel myVnet2 toomyVnet1. Hola emparejamiento debe crearse en ambas direcciones tooenable recursos en hello toocommunicate de redes virtuales entre sí.
11. Complete nuevamente los pasos del 5 al 10 para myVnet2.  Nombre hello emparejamiento *myVnet2ToMyVnet1*.
12. Unos pocos segundos después de hacer clic **Aceptar** toocreate Hola emparejamiento para MyVnet2, hello **myVnet2ToMyVnet1** emparejamiento que acaba de crear aparece con **conectado** en hello  **ESTADO de EMPAREJAMIENTO** columna.
13. Complete nuevamente los pasos del 5 al 7 para MyVnet1. Hola **estado EMPAREJAMIENTO** para hello **myVnet1ToVNet2** emparejamiento ahora también es **conectado**. Hola emparejamiento se ha establecido correctamente después de ver **conectado** en hello **estado EMPAREJAMIENTO** columna para ambas redes virtuales en el emparejamiento de Hola de.
14. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
15. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete-portal) sección de este artículo.

Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Creación de emparejamiento: CLI de Azure

Hola siguiente secuencia de comandos:

- Requiere hello Azure CLI versión 2.0.4 o versiones posteriores. versión de hello toofind, ejecute hello `az --version` comando. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funciona en un shell de Bash. Para opciones sobre cómo ejecutar las secuencias de comandos de CLI de Azure en el cliente de Windows, vea [ejecuta Hola CLI de Azure en Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

En lugar de instalar Hola CLI y sus dependencias, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Haga clic en hello **Pruébelo** botón en el script de Hola que se indica a continuación, que invoca un Shell en la nube que registra se puede iniciar sesión en tooyour cuenta de Azure con. tooexecute hello secuencia de comandos, haga clic en hello **copia** botón y pegue el contenido de hello en el Shell de nube.

1. Cree un grupo de recursos y dos redes virtuales.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Crear una red virtual emparejamiento entre las dos redes virtuales de Hola.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Después de ejecuta el script de Hola, revise los emparejamientos de Hola para cada red virtual. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hola anterior vuelva a ejecutar comando, reemplazando *myVnet1* con *myVnet2*. salida de Hello de ambos comandos muestra **conectado** en hello **PeeringState** columna.

     Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
5. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.


## <a name="powershell"></a>Creación de emparejamiento: PowerShell

1. Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart una sesión de PowerShell, vaya demasiado**iniciar**, escriba **powershell**y, a continuación, haga clic en **PowerShell**.
3. En PowerShell, inicie sesión en tooAzure escribiendo hello `login-azurermaccount` comando. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
4. Cree un grupo de recursos y dos redes virtuales. script de Hola tooexecute, copia Hola siguiente script, péguelo en PowerShell y presione `Enter` después de hello última línea aparece en la pantalla de bienvenida:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Crear una red virtual emparejamiento entre las dos redes virtuales de Hola. Siguiente Hola de copia de scripts, pegue en tooPowerShell y, a continuación, presione `Enter` después de hello última línea aparece en la pantalla de bienvenida:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. subredes de hello tooreview para la red virtual de hello, copia Hola comando siguiente, pegue en tooPowerShell y, a continuación, presione `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hola anterior vuelva a ejecutar comando, reemplazando *myVnet1* con *myVnet2*. salida de Hello de ambos comandos muestra **conectado** en hello **PeeringState** columna.
7. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
8. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.

Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Creación de emparejamiento: plantilla de Resource Manager

1. Consulte [Creación de un emparejamiento de red virtual](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) mediante una plantilla de Resource Manager. Las instrucciones están proporcionados con la plantilla de hello para la implementación de plantilla de hello utilizando Hola portal de Azure, PowerShell u Hola CLI de Azure. Registro en la herramienta toowhichever elige toodeploy Hola plantilla con el uso de una cuenta que tenga Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
2. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
3. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete) sección de este artículo, mediante Hola Hola CLI de Azure, PowerShell o portal de Azure.

## <a name="permissions"></a>Permisos

cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos. Por ejemplo, si se emparejamiento dos redes virtuales denominadas VNet1 y VNet2, su cuenta se debe asignar Hola después de función mínima o los permisos para cada red virtual:
    
|Red virtual|Rol|Permisos|
|---|---|---|
|VNet1|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).

## <a name="delete"></a>Eliminación de recursos
Cuando haya terminado este tutorial, conviene toodelete recursos de Hola que creó en el tutorial de hello, por lo que no se incurre en cargos por uso. Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.

### <a name="delete-portal"></a>Azure Portal

1. En el cuadro de búsqueda del portal de hello, escriba **myResourceGroup**. En los resultados de la búsqueda de hello, haga clic en **myResourceGroup**.
2. En hello **myResourceGroup** hoja, haga clic en hello **eliminar** icono.
3. eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroup**y, a continuación, haga clic en **eliminar**.

### <a name="delete-cli"></a>Azure CLI

Escriba el siguiente comando de hello:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Escriba el siguiente comando de hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Pasos siguientes

- Conozca en profundidad las [restricciones y comportamientos importantes del emparejamiento de redes virtuales](virtual-network-manage-peering.md#requirements-and-constraints) antes de crear un emparejamiento de redes virtuales para su uso en el entorno de producción.
- Conozca toda la [configuración de emparejamiento de redes virtuales](virtual-network-manage-peering.md#create-a-peering).
- Obtenga información acerca de cómo demasiado[crear un concentrador y radio de la topología de red](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con intercambio de tráfico de red virtual.
