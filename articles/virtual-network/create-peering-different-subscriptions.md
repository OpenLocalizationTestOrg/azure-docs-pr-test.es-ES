---
title: emparejamiento - Administrador de recursos - diferentes suscripciones de red aaaCreate un virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una emparejamiento entre redes virtuales de red virtual creado mediante el Administrador de recursos que existen en diferentes suscripciones de Azure."
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Crear un emparejamiento de redes virtuales: Resource Manager, suscripciones diferentes 

En este tutorial, aprenderá toocreate una emparejamiento entre redes virtuales creadas mediante el Administrador de recursos de red virtual. redes virtuales de Hello residen en distintas suscripciones. Emparejamiento dos redes virtuales permite recursos en diferentes redes virtuales toocommunicate entre sí con Hola mismo ancho de banda y latencia como si estuvieran recursos Hola Hola misma red virtual. Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md). 

Hello pasos toocreate un emparejamiento de red virtual son diferentes, dependiendo de si son redes virtuales de hello en hello iguales o distinto, suscripciones y que [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello las redes virtuales se crean a través de. Obtenga información acerca de cómo toocreate un virtual red emparejamiento en otros escenarios, haga clic en el escenario de Hola de hello en la tabla siguiente:

|Modelo de implementación de Azure  | Suscripción de Azure  |
|--------- |---------|
|[Ambas mediante Resource Manager](virtual-network-create-peering.md) |Iguales|
|[Una mediante Resource Manager y la otra clásica](create-peering-different-deployment-models.md) |Iguales|
|[Una mediante Resource Manager y la otra, clásico](create-peering-different-deployment-models-subscriptions.md) |Diferentes|

No se puede crear un intercambio de tráfico de red virtual entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola. Un intercambio de tráfico de red virtual solo puede crearse entre dos redes virtuales que existen en hello misma región de Azure. Al crear una red virtual emparejamiento entre redes virtuales que existan en distintas suscripciones, hello las suscripciones deben estar asociada toohello mismo Azure Active Directory de los inquilinos. Si todavía no tiene un inquilino de Azure Active Directory, puede [crear uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rápidamente. Si necesita tooconnect virtual redes que se crearon a través del modelo de implementación clásica de hello, o que se encuentren en diferentes regiones de Azure o que existen en las suscripciones asociadas a los inquilinos de Azure Active Directory toodifferent, puede usar un Azure [Puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hola redes virtuales. 

Puede usar hello [portal de Azure](#portal), hello Azure [interfaz de línea de comandos](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un emparejamiento de red virtual. Haga clic en cualquiera de hello anterior herramienta vínculos toogo directamente toohello los pasos para crear un intercambio de tráfico de red virtual mediante la herramienta de elección.

## <a name="portal"></a>Creación de emparejamiento: Azure Portal

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para iniciar sesión en el portal de Hola y omita los pasos de Hola para asignar a otro usuario redes virtuales de toohello de permisos.

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
8. Hola **seleccione** cuadro, seleccione un UserB o escriba toosearch de dirección de correo electrónico del usuariob para él. Hola lista de usuarios que se muestra es de hello mismo inquilino de Azure Active Directory como la red virtual de hello está configurando Hola emparejamiento para.
9. Haga clic en **Guardar**.
10. Hola **myVnetA - control de acceso (de índices IAM)** hoja, haga clic en **propiedades** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola. Hola copia **Id. de recurso**, que se usa en un paso posterior. Identificador de recurso de Hello es similar toohello siguiente ejemplo: / Subscriptions /<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Cierre sesión en el portal de hello como UserA, a continuación, inicie sesión como UserB.
12. Complete los pasos 2 y 3, escribir o seleccionar Hola después los valores en el paso 3:

    - **Nombre**: *myVnetB*
    - **Espacio de direcciones**: *10.1.0.0/16*
    - **Nombre de subred**: *default*
    - **Intervalo de direcciones de subred**: *10.1.0.0/24*
    - **Suscripción**: seleccione la suscripción B
    - **Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroupB*
    - **Ubicación**: *este de EE. UU.*

13. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetB*. Haga clic en **myVnetB** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnetB** red virtual.
14. Hola **myVnetB** hoja que aparece, haga clic en **propiedades** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola. Hola copia **Id. de recurso**, que se usa en un paso posterior. Identificador de recurso de Hello es similar toohello siguiente ejemplo: / Subscriptions /<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Haga clic en **(de índices IAM) de control de acceso** en hello **myVnetB** hoja y, a continuación, completar los pasos 5-10 para myVnetB, escriba **UserA** en el paso 8.
16. Cierre sesión en el portal de hello como UserB e inicie sesión como usuario.
17. Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myVnetA*. Haga clic en **myVnetA** cuando aparece en los resultados de búsqueda de Hola. Aparece una hoja de hello **myVnet** red virtual.
18. Haga clic en **myVnetA**.
19. Hola **myVnetA** hoja que aparece, haga clic en **emparejamientos** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.
20. Hola **myVnetA - emparejamientos** hoja que aparece, haga clic en **+ agregar**
21. Hola **agregar emparejamiento** hoja que aparece, escriba, o seleccione Hola siguientes opciones, haga clic en **Aceptar**:
     - **Nombre**: *myVnetAToMyVnetB*
     - **Modelo de implementación de red virtual**: seleccione **Resource Manager**.
     - **Conozco mi id. de recurso**: active esta casilla.
     - **Id. de recurso**: escriba el Id. de recurso de hello del paso 14.
     - **Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.
    En este tutorial no se usa ninguna otra configuración. leer toolearn sobre todas las opciones de intercambio de tráfico, [administrar emparejamientos de red virtual](virtual-network-manage-peering.md#create-a-peering).
22. Tras hacer clic en **Aceptar** en el paso anterior de hello, Hola **agregar emparejamiento** hoja se cierra y vea hello **myVnetA - emparejamientos** hoja de nuevo. Después de unos segundos, Hola emparejamiento que ha creado aparece en la hoja de Hola. **Inicia** aparece en hello **estado EMPAREJAMIENTO** columna para hello **myVnetAToMyVnetB** emparejamiento se creó. Ha emparejar myVnetA toomyVnetB, pero ahora debe del mismo nivel myVnetB toomyVnetA. Hola emparejamiento debe crearse en ambas direcciones tooenable recursos en hello toocommunicate de redes virtuales entre sí.
23. Cierre sesión en el portal de hello como UserA e inicie sesión como UserB.
24. Complete nuevamente los pasos del 17 al 21 para MyVnetB. En el paso 21, nombre de emparejamiento de hello *myVnetBToMyVnetA*, seleccione *myVnetA* para **red Virtual**y escriba el Id. de hello del paso 10 en hello **Id. de recurso** cuadro.
25. Unos pocos segundos después de hacer clic **Aceptar** toocreate Hola emparejamiento para myVnetB, hello **myVnetBToMyVnetA** emparejamiento que acaba de crear aparece con **conectado** en hello  **ESTADO de EMPAREJAMIENTO** columna.
26. Cierre sesión en el portal de hello como UserB e inicie sesión como usuario.
27. Complete nuevamente los pasos del 17 al 19. Hola **estado EMPAREJAMIENTO** para hello **myVnetAToVNetB** emparejamiento ahora también es **conectado**. Hola emparejamiento se ha establecido correctamente después de ver **conectado** en hello **estado EMPAREJAMIENTO** columna para ambas redes virtuales en el emparejamiento de Hola de. Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
29. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete-portal) sección de este artículo.

## <a name="cli"></a>Creación de emparejamiento: CLI de Azure

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para el registro fuera de Azure y quitar líneas de Hola de script que cree asignaciones de roles de usuario. Reemplace UserA@azure.com y UserB@azure.com de hello siguientes secuencias de comandos con nombres de usuario de Hola que está usando para UserA y UserB todos.

Hola siguiente secuencia de comandos:

- Requiere hello Azure CLI versión 2.0.4 o versiones posteriores. versión de hello toofind, ejecute `az --version`. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funciona en un shell de Bash. Para opciones sobre cómo ejecutar las secuencias de comandos de CLI de Azure en el cliente de Windows, vea [ejecuta Hola CLI de Azure en Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

En lugar de instalar Hola CLI y sus dependencias, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Haga clic en hello **Pruébelo** botón en hello secuencia de comandos siguiente, que invoca un Shell en la nube que se puede iniciar sesión en tooyour cuenta de Azure con. 

1. Abra una sesión CLI e inicie sesión tooAzure como UserA con hello `azure login` comando. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
2. Copiar Hola después de editor de texto de script tooa en su PC, reemplace `<SubscriptionA-Id>` con hello Id. de Suscripcióna, a continuación, Hola de copia modifica script, péguelo en la sesión CLI y presione `Enter`. Si no conoce el Id. de suscripción, escriba del comando 'show de cuenta az' hello. Hola valor para **identificador** Hola salida es el identificador de suscripción.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     asignación de permisos de Hola para UserB no es un requisito. Emparejamiento se puede establecer incluso si los usuarios generar individualmente las solicitudes de emparejamiento de sus respectivas redes virtuales, como Hola solicita la coincidencia. Agregar un usuario con privilegios de myVNetB como colaborador de red en la red virtual local de hello facilita la instalación más sencilla de hello toodo.
3. Cierre la sesión de Azure como UserA con hello `az logout` comando, a continuación, inicie sesión en tooAzure como UserB. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
4. Cree myVnetB. Copie el contenido del script de Hola en editor de texto tooa 2 de paso en su PC. Reemplace `<SubscriptionA-Id>` con hello Id. de Suscripciónb. Cambiar 10.0.0.0/16 too10.1.0.0/16, el cambio todos como tooB y todos los tooA Bs. Copie el script de Hola modificado, péguelo en la sesión CLI tooyour y presione `Enter`. 
5. Cierre la sesión de Azure como UserB e inicie sesión tooAzure como UserA.
6. Crear una red virtual de emparejamiento de myVnetA toomyVnetB. Copie Hola después de editor de texto de script contenido tooa en su PC. Reemplace `<SubscriptionB-Id>` con hello Id. de Suscripciónb. script de Hola tooexecute, copie el script de Hola modificado, péguela en la sesión CLI y presione ENTRAR.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Ver estado de emparejamiento de Hola de myVnetA.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    estado de Hello es **inició**. También cambia**conectado** una vez que cree toomyVnetA de emparejamiento de Hola desde myVnetB.

8. Cierre sesión UserA de Azure e inicie sesión tooAzure como UserB.
9. Crear Hola emparejamiento de myVnetB toomyVnetA. Copie el contenido del script de Hola en editor de texto de paso 6 tooa en su PC. Reemplace `<SubscriptionB-Id>` con el identificador de Hola para Suscripcióna y cambiar todos como tooB y todos los tooA Bs. Una vez realizados los cambios de hello, Hola copia modifica script, péguelo en la sesión CLI y presione `Enter`.
10. Ver estado de emparejamiento de Hola de myVnetB. Copie el contenido del script de Hola en editor de texto de paso 7 tooa en su PC. Cambiar un tooB para el grupo de recursos de Hola y nombres de red virtual, copie el script de Hola, pegue el script de Hola modificado en la sesión CLI tooyour y, a continuación, presione `Enter`. Hello emparejamiento estado es **conectado**. Hola demasiado emparejamiento cambia estado de myVnetA**conectado** después de haber creado Hola emparejamiento de myVnetB toomyVnetA. Puede registrar UserA en tooAzure y realiza el paso 7 nuevo estado de emparejamiento de hello tooverify de myVnetA. 

    > [!NOTE]
    > Hola emparejamiento no se establece hasta que el estado de emparejamiento de hello es **conectado** para ambas redes virtuales.

11. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
12. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.

Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Creación de emparejamiento: PowerShell

En este tutorial se usan cuentas diferentes para cada suscripción. Si está utilizando una cuenta que tenga permisos tooboth suscripciones, puede usar Hola misma cuenta para todos los pasos, omita los pasos de hello para el registro fuera de Azure y quitar líneas de Hola de script que cree asignaciones de roles de usuario. Reemplace UserA@azure.com y UserB@azure.com de hello siguientes secuencias de comandos con nombres de usuario de Hola que está usando para UserA y UserB todos.

1. Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie una sesión de PowerShell.
3. En PowerShell, inicie sesión en tooAzure como UserA escribiendo hello `login-azurermaccount` comando. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
4. Cree un grupo de recursos y la red virtual copia r. Hola siguiendo el texto del script tooa editor en su PC. Reemplace `<SubscriptionA-Id>` con hello Id. de Suscripcióna. Si no conoce el Id. de suscripción, escriba Hola `Get-AzureRmSubscription` tooview comando lo. Hola valor para **identificador** Hola devuelve el resultado es el identificador de suscripción. script de Hola tooexecute, Hola copia modifica script, péguelo en tooPowerShell y, a continuación, presione `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    asignación de permisos de Hola para UserB no es un requisito. Emparejamiento se puede establecer incluso si los usuarios generar individualmente las solicitudes de emparejamiento de sus respectivas redes virtuales, como Hola solicita la coincidencia. Agregar un usuario con privilegios de hello otra red virtual como un usuario de red virtual local de hello facilita la instalación más sencilla de hello toodo.
5. Cierre sesión en Azure como UserA e inicie sesión como UserB. cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual. Vea hello [permisos](#permissions) sección de este artículo para obtener más información.
6. Copie el contenido del script de Hola en editor de texto de paso 4 tooa en su PC. Reemplace `<SubscriptionA-Id>` con el identificador de Hola para suscripción B. cambio 10.0.0.0/16 too10.1.0.0/16. Cambie todos como tooB y todos los tooA Bs. script de Hola tooexecute, Hola copia modificó la secuencia de comandos, pegue en PowerShell y, a continuación, presione `Enter`.
7. Cierre sesión como UserB en Azure e inicie sesión como UserA.
8. Crear Hola emparejamiento de myVnetA toomyVnetB. Copie Hola después de editor de texto de script tooa en su PC. Reemplace `<SubscriptionB-Id>` con hello Id. de suscripción de script de Hola B. tooexecute, copie el script de Hola modificar, pegue en tooPowerShell y, a continuación, presione `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Ver estado de emparejamiento de Hola de myVnetA.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    estado de Hello es **inició**. También cambia**conectado** una vez que el programa de instalación hello toomyVnetA de emparejamiento de myVnetB.

10. Cierre sesión en Azure como UserA e inicie sesión como UserB.
11. Crear Hola emparejamiento de myVnetB toomyVnetA. Copie el contenido del script de Hola en editor de texto de 8 tooa de paso en su PC. Reemplace `<SubscriptionB-Id>` con el Id. de Hola de cambio y suscripción A tooB la y tooA la b. todos. script de Hola tooexecute, Hola copia modifica script, péguelo en tooPowerShell y, a continuación, presione `Enter`.
12. Ver estado de emparejamiento de Hola de myVnetB. Copie el contenido del script de Hola en editor de texto de paso 9 tooa en su PC. Cambiar un tooB para el grupo de recursos de Hola y nombres de red virtual. script de Hola tooexecute, pegue el script de Hola modificado en PowerShell y, a continuación, presione `Enter`. estado de Hello es **conectado**. Hola estado emparejamiento de **myVnetA** cambia demasiado**conectado** después de haber creado Hola emparejamiento de **myVnetB** demasiado**myVnetA**. Puede registrar UserA en tooAzure y realiza el paso 9 nuevo estado de emparejamiento de hello tooverify de myVnetA. 

    > [!NOTE]
    > Hola emparejamiento no se establece hasta que el estado de emparejamiento de hello es **conectado** para ambas redes virtuales.

    Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP. Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola. Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS. Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.
14. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.

## <a name="permissions"></a>Permisos

cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos. Por ejemplo, si se emparejamiento dos redes virtuales denominadas **myVnetA** y **myVnetB**, su cuenta debe tener asignado Hola después de función mínima o los permisos para cada red virtual:
    
|Red virtual|Rol|Permisos|
|---|---|---|
|myVnetA|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).

## <a name="delete"></a>Eliminación de recursos
Cuando haya terminado este tutorial, conviene toodelete recursos de Hola que creó en el tutorial de hello, por lo que no se incurre en cargos por uso. Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.

### <a name="delete-portal"></a>Azure Portal

1. Inicie sesión en toohello portal de Azure como UserA.
2. En el cuadro de búsqueda del portal de hello, escriba **myResourceGroupA**. En los resultados de la búsqueda de hello, haga clic en **myResourceGroupA**.
3. En hello **myResourceGroupA** hoja, haga clic en hello **eliminar** icono.
4. eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroupA**y, a continuación, haga clic en **eliminar**.
5. Cierre sesión en el portal de hello como UserA e inicie sesión como UserB.
6. Complete los pasos del 2 al 4 para myResourceGroupB.

### <a name="delete-cli"></a>Azure CLI

1. Inicie sesión en tooAzure como UserA y ejecute el siguiente comando de hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Cierre sesión en Azure como UserA e inicie sesión como UserB.
3. Ejecute el siguiente comando de hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Inicie sesión en tooAzure como UserA y ejecute el siguiente comando de hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Cierre sesión en Azure como UserA e inicie sesión como UserB.
3. Ejecute el siguiente comando de hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Pasos siguientes

- Conozca en profundidad las [restricciones y comportamientos importantes del emparejamiento de redes virtuales](virtual-network-manage-peering.md#requirements-and-constraints) antes de crear un emparejamiento de redes virtuales para su uso en el entorno de producción.
- Conozca toda la [configuración de emparejamiento de redes virtuales](virtual-network-manage-peering.md#create-a-peering).
- Obtenga información acerca de cómo demasiado[crear un concentrador y radio de la topología de red](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con intercambio de tráfico de red virtual.
