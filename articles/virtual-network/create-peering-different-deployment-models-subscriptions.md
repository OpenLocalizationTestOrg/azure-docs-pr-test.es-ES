---
title: "aaaCreate un emparejamiento de red virtual de Azure - implementación diferentes modelos - distintas suscripciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate creado de una red virtual emparejamiento entre redes virtuales a través de modelos de implementación de Azure diferentes que existen en diferentes suscripciones de Azure."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Crear un emparejamiento de redes virtuales de Azure: diferentes modelos de implementación y suscripciones

En este tutorial, aprenderá toocreate una emparejamiento entre redes virtuales creadas a través de diferentes modelos de implementación de red virtual. redes virtuales de Hello residen en distintas suscripciones. Emparejamiento dos redes virtuales permite recursos en diferentes redes virtuales toocommunicate entre sí con Hola mismo ancho de banda y latencia como si estuvieran recursos Hola Hola misma red virtual. Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md). 

Hello pasos toocreate un emparejamiento de red virtual son diferentes, dependiendo de si son redes virtuales de hello en hello iguales o distinto, suscripciones y que [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello las redes virtuales se crean a través de. Obtenga información acerca de cómo toocreate un virtual red emparejamiento en otros escenarios, haga clic en el escenario de Hola de hello en la tabla siguiente:

|Modelo de implementación de Azure  | Suscripción de Azure  |
|--------- |---------|
|[Ambas mediante Resource Manager](virtual-network-create-peering.md) |Iguales|
|[Ambas mediante Resource Manager](create-peering-different-subscriptions.md) |Diferentes|
|[Una mediante Resource Manager y la otra, clásico](create-peering-different-deployment-models.md) |Iguales|

No se puede crear un intercambio de tráfico de red virtual entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola. Un intercambio de tráfico de red virtual solo puede crearse entre dos redes virtuales que existen en hello misma región de Azure. Al crear una red virtual emparejamiento entre redes virtuales que existan en distintas suscripciones, hello las suscripciones deben estar asociada toohello mismo Azure Active Directory de los inquilinos. Si todavía no tiene un inquilino de Azure Active Directory, puede [crear uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rápidamente. Si necesita tooconnect virtual redes que se crearon a través del modelo de implementación clásica de hello, o que se encuentren en diferentes regiones de Azure o que existen en las suscripciones asociadas a los inquilinos de Azure Active Directory toodifferent, puede usar un Azure [Puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hola redes virtuales. 

> [!WARNING]
> La creación de un emparejamiento de redes virtuales entre redes virtuales creadas mediante diferentes modelos de implementación de Azure que existen en diferentes suscripciones de Azure se encuentra actualmente en versión preliminar. Emparejamientos de red virtual que creó en este escenario no pueden tener Hola de mismo nivel de disponibilidad y confiabilidad como crear una red virtual emparejamiento en escenarios, por lo general, versión de disponibilidad. Los emparejamientos de redes virtuales que se crean en este escenario no se admiten, pueden tener capacidades limitadas y pueden no estar disponibles en todas las regiones de Azure. Para hello más las notificaciones de actualización de disponibilidad y estado de esta característica, consulte hello [red Virtual de Azure actualiza](https://azure.microsoft.com/updates/?product=virtual-network) página.

Puede usar hello [portal de Azure](#portal), hello Azure [interfaz de línea de comandos](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un emparejamiento de red virtual. Haga clic en cualquiera de hello anterior herramienta vínculos toogo directamente toohello los pasos para crear un intercambio de tráfico de red virtual mediante la herramienta de elección.

## <a name="register"></a>Registro para la vista previa de Hola

tooregister para la vista previa de hello, los pasos de hello completa que siguen para ambas suscripciones que contienen las redes virtuales Hola desee toopeer. Hello solo se puede usar tooregister para la vista previa de hello herramienta es PowerShell.

1. Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie una sesión de PowerShell e inicie sesión en tooAzure con hello `login-azurermaccount` comando.
3. Registrar la suscripción para la vista previa de hello escribiendo Hola siguientes comandos:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    No se completan los pasos de hello en secciones de Portal, Azure CLI o PowerShell Hola de este artículo hasta hello **RegistrationState** salida recibirá después de escribir el siguiente comando de hello **registrado** para ambas suscripciones:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Creación de emparejamiento: Azure Portal

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para iniciar sesión en el portal de Hola y omita los pasos de Hola para asignar a otro usuario redes virtuales de toohello de permisos. Antes de realizar cualquiera de los pasos de hello, debe registrar para la vista previa de Hola. tooregister, Hola completa los pasos de hello [registrar para la vista previa de hello](#register) sección de este artículo. No continúe con hello restantes pasos hasta que se registran las suscripciones para la vista previa de Hola.
 
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como UserA. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
2. Haga clic en **+ Nuevo**, **Redes** y, luego, en **Red virtual**.
3. Hola **crear red virtual** hoja, escriba, o seleccionar los valores de hello después de la configuración, haga clic en **crear**:
    - **Nombre**: *myVnetA*
    - **Espacio de direcciones**: *10.0.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.0.0.0/24*
    - **Suscripción**: seleccione la suscripción A
    - **Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroupA*
    - **Ubicación**: *este de EE. UU.*
4. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetA*. Haga clic en **myVnetA** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnetA** red virtual.
5. Hola **myVnetA** hoja que aparece, haga clic en **(de índices IAM) de control de acceso** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.
6. Hola **myVnetA - control de acceso (de índices IAM)** hoja que aparece, haga clic en **+ agregar**.
7. Hola **agregar permisos** hoja que aparece, seleccione **colaborador de red** en hello **rol** cuadro.
8. Hola **seleccione** cuadro, seleccione UserB o escriba toosearch de dirección de correo electrónico del usuariob para él. Hola lista de usuarios que se muestra es de hello mismo inquilino de Azure Active Directory como la red virtual de hello está configurando Hola emparejamiento para. Haga clic en UserB cuando aparece en la lista de Hola.
9. Haga clic en **Guardar**.
10. Cierre sesión en el portal de hello como UserA, a continuación, inicie sesión como UserB.
11. Haga clic en **+ nuevo**, tipo *red Virtual* en hello **Hola búsqueda Marketplace** cuadro, a continuación, haga clic en **red Virtual** en los resultados de búsqueda de Hola .
12. Hola **red Virtual** hoja que aparece, seleccione **clásico** en hello **seleccionar un modelo de implementación** cuadro, a continuación, haga clic en **crear**.
13.   En cuadro de la red virtual (clásica) de crear Hola que aparece, escriba Hola después de valores:

    - **Nombre**: *myVnetB*
    - **Espacio de direcciones**: *10.1.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.1.0.0/24*
    - **Suscripción**: seleccione la suscripción B
    - **Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroupB*
    - **Ubicación**: *este de EE. UU.*

14. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetB*. Haga clic en **myVnetB** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnetB** red virtual.
15. Hola **myVnetB** hoja que aparece, haga clic en **propiedades** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola. Hola copia **Id. de recurso**, que se usa en un paso posterior. Identificador de recurso de Hello es similar toohello siguiente ejemplo: / Subscriptions /<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Complete los pasos 5 a 9 para myVnetB y escriba **UserA** en el paso 8.
17. Cierre sesión en el portal de hello como UserB e inicie sesión como usuario.
18. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetA*. Haga clic en **myVnetA** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnet** red virtual.
19. Haga clic en **myVnetA**.
20. Hola **myVnetA** hoja que aparece, haga clic en **emparejamientos** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.
21. Hola **myVnetA - emparejamientos** hoja que aparece, haga clic en **+ agregar**
22. Hola **agregar emparejamiento** hoja que aparece, escriba, o seleccione Hola siguientes opciones, haga clic en **Aceptar**:
     - **Nombre**: *myVnetAToMyVnetB*
     - **Modelo de implementación de red virtual**: seleccione **Clásico**.
     - **Conozco mi id. de recurso**: active esta casilla.
     - **Id. de recurso**: escriba el identificador de recurso de Hola de myVnetB del paso 15.
     - **Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.
    En este tutorial no se usa ninguna otra configuración. leer toolearn sobre todas las opciones de intercambio de tráfico, [administrar emparejamientos de red virtual](virtual-network-manage-peering.md#create-a-peering).
23. Tras hacer clic en **Aceptar** en el paso anterior de hello, Hola **agregar emparejamiento** hoja se cierra y vea hello **myVnetA - emparejamientos** hoja de nuevo. Después de unos segundos, Hola emparejamiento que ha creado aparece en la hoja de Hola. **Conectado** aparece en hello **estado EMPAREJAMIENTO** columna para hello **myVnetAToMyVnetB** emparejamiento se creó. Ahora se establece el emparejamiento de Hola. No hay ninguna necesidad de toopeer Hola red virtual (clásica) toohello red virtual (Administrador de recursos).

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
25. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete-portal) sección de este artículo.

## <a name="cli"></a>Creación de emparejamiento: CLI de Azure

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para el registro fuera de Azure y quitar líneas de Hola de script que cree asignaciones de roles de usuario. Reemplace UserA@azure.com y UserB@azure.com de hello siguientes secuencias de comandos con nombres de usuario de Hola que está usando para UserA y UserB todos. 

Antes de realizar cualquiera de los pasos de hello, debe registrar para la vista previa de Hola. tooregister, Hola completa los pasos de hello [registrar para la vista previa de hello](#register) sección de este artículo. No continúe con hello restantes pasos hasta que se registran las suscripciones para la vista previa de Hola.

1. [Instalar](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) red virtual de hello Azure CLI 1.0 toocreate Hola (clásico).
2. Abra una sesión CLI e inicie sesión tooAzure como UserB con hello `azure login` comando.
3. Ejecute hello CLI en modo de administración de servicio escribiendo hello `azure config mode asm` comando.
4. Escriba Hola siguiente comando toocreate Hola red virtual (clásica):
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Hola restantes pasos debe realizarse con un shell de bash hello Azure CLI 2.0.4 o posterior [instalado](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), o mediante el uso de hello Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Haga clic en hello **Pruébelo** botón en hello las secuencias de comandos siguientes, que abre un Shell en la nube que se registra en tooyour cuenta de Azure. Para opciones de ejecución bash secuencias de comandos CLI en un cliente de Windows, consulte [ejecuta Hola CLI de Azure en Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Copie Hola después de editor de texto de script tooa en su PC. Reemplace `<SubscriptionB-Id>` con el Id. de suscripción. Si no conoce el Id. de suscripción, escriba Hola `az account show` comando. Hola valor para **identificador** Hola salida es el identificador de suscripción. Copie el script de Hola modificado, péguelo en la sesión tooyour CLI 2.0 y, a continuación, presione `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Al crear red virtual de hello (clásica) en el paso 4, Azure crea red virtual de Hola Hola *predeterminado redes* grupo de recursos.
7. Inicie sesión UserB fuera de Azure e inicie sesión como UserA Hola CLI 2.0.
8. Cree un grupo de recursos y una red virtual (Resource Manager). Siguiente Hola de copia de script, péguelo en la sesión CLI tooyour y, a continuación, presione `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Crear una red virtual emparejamiento entre Hola dos redes virtuales creadas a través de hello diferentes modelos de implementación. Copie Hola después de editor de texto de script tooa en su PC. Reemplace `<SubscriptionB-id>` con el Id. de suscripción. Si no conoce el Id. de suscripción, escriba Hola `az account show` comando. Hola valor para **identificador** Hola salida es el identificador de suscripción. Azure creado la red virtual de hello (clásico) que creó en el paso 4 en un grupo de recursos denominado *redes predeterminado*. Pegue el script de Hola modificado en la sesión CLI y, a continuación, presione `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Después de ejecuta el script de Hola, revise el emparejamiento hello para la red virtual de hello (Administrador de recursos). Copie la siguiente secuencia de comandos de hello y, a continuación, péguelo en la sesión CLI:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Hola resultado muestra **conectado** en hello **PeeringState** columna.

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
12. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.

## <a name="powershell"></a>Creación de emparejamiento: PowerShell

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para el registro fuera de Azure y quitar líneas de Hola de script que cree asignaciones de roles de usuario. Reemplace UserA@azure.com y UserB@azure.com de hello siguientes secuencias de comandos con nombres de usuario de Hola que está usando para UserA y UserB todos. 

Antes de realizar cualquiera de los pasos de hello, debe registrar para la vista previa de Hola. tooregister, Hola completa los pasos de hello [registrar para la vista previa de hello](#register) sección de este artículo. No continúe con hello restantes pasos hasta que se registran las suscripciones para la vista previa de Hola.

1. Instale Hola la versión más reciente de hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) y [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulos. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie una sesión de PowerShell.
3. En PowerShell, inicie sesión en la suscripción del tooUserB UserB escribiendo hello `Add-AzureAccount` comando.
4. toocreate una red virtual (clásica) con PowerShell, debe crear un nuevo, o modificar una existente, el archivo de configuración de red. Obtenga información acerca de cómo demasiado[exportar, actualizar e importar archivos de configuración de red](virtual-networks-using-network-configuration-file.md). Hello archivo debe incluir siguiente hello **VirtualNetworkSite** , elemento de red virtual de hello usada en este tutorial:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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

5. Inicie sesión en la suscripción del tooUserB UserB toouse los comandos del Administrador de recursos mediante la especificación de hello `login-azurermaccount` comando.
6. Red de toovirtual de permisos de asignar UserA siguiente de hello B. copia tooa editor de texto en su PC de secuencias de comandos y reemplace `<SubscriptionB-id>` con el Id. de Hola de suscripción B. Si no conoce el Id. de suscripción de hello, escriba Hola `Get-AzureRmSubscription` tooview comando lo. Hola valor para **identificador** Hola devuelve el resultado es el identificador de suscripción. Azure creado la red virtual de hello (clásico) que creó en el paso 4 en un grupo de recursos denominado *redes predeterminado*. script de Hola tooexecute, Hola copia modifica script, péguelo en tooPowerShell y, a continuación, presione `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Cerrar sesión en Azure como UserB y de registro en la suscripción del tooUserA UserA escribiendo hello `login-azurermaccount` comando. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
8. Crear red virtual de hello (Administrador de recursos) copiando Hola siguiente secuencia de comandos, pegarlo en tooPowerShell y, a continuación, presione `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Asignar UserB permisos toomyVnetA. Siguiente de hello copia tooa editor de texto en su PC de secuencias de comandos y reemplace `<SubscriptionA-Id>` con el Id. de Hola de suscripción A. Si no conoce el Id. de suscripción de hello, escriba Hola `Get-AzureRmSubscription` tooview comando lo. Hola valor para **identificador** Hola devuelve el resultado es el identificador de suscripción. Pegue Hola versión modificada del script de Hola de PowerShell y, a continuación, presione `Enter` tooexecute lo.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Siguiente Hola de copia tooa editor de texto en su PC de secuencias de comandos y reemplace `<SubscriptionB-id>` con hello del identificador de suscripción B. toopeer myVnetA toomyVNetB, copie el script de Hola modificado, péguelo en tooPowerShell y, a continuación, presione `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Ver estado de emparejamiento de Hola de myVnetA copiando Hola siguiente secuencia de comandos, pegarla en PowerShell y presione `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    estado de Hello es **conectado**. También cambia**conectado** una vez que el programa de instalación hello toomyVnetA de emparejamiento de myVnetB.

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
13. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.

## <a name="permissions"></a>Permisos

cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos. Por ejemplo, si se emparejamiento dos redes virtuales denominadas myVnetA y myVnetB, su cuenta se debe asignar Hola después de función mínima o los permisos para cada red virtual:
    
|Red virtual|Modelo de implementación|Rol|Permisos|
|---|---|---|---|
|myVnetA|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).

## <a name="delete"></a>Eliminación de recursos
Cuando haya terminado este tutorial, conviene toodelete recursos de Hola que creó en el tutorial de hello, por lo que no se incurre en cargos por uso. Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.

### <a name="delete-portal"></a>Azure Portal

1. En el cuadro de búsqueda del portal de hello, escriba **myResourceGroupA**. En los resultados de la búsqueda de hello, haga clic en **myResourceGroupA**.
2. En hello **myResourceGroupA** hoja, haga clic en hello **eliminar** icono.
3. eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroupA**y, a continuación, haga clic en **eliminar**.
4. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetB*. Haga clic en **myVnetB** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnetB** red virtual.
5. Hola **myVnetB** hoja, haga clic en **eliminar**.
6. eliminación de hello tooconfirm, haga clic en **Sí** en hello **red virtual de Delete** cuadro.

### <a name="delete-cli"></a>Azure CLI

1. Inicio de sesión tooAzure con hello red virtual de CLI 2.0 toodelete Hola (Administrador de recursos) con hello siguiente comando:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Inicio de sesión tooAzure con hello red virtual de Azure CLI 1.0 toodelete Hola (clásico) con hello siguientes comandos:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. En la línea de comandos de PowerShell de hello, escriba Hola siguiente comando toodelete Hola (Administrador de recursos) de red virtual:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete Hola red virtual (clásica) con PowerShell, debe modificar un archivo de configuración de red existente. Obtenga información acerca de cómo demasiado[exportar, actualizar e importar archivos de configuración de red](virtual-networks-using-network-configuration-file.md). Quitar Hola siguiente elemento VirtualNetworkSite de red virtual de hello usada en este tutorial:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
