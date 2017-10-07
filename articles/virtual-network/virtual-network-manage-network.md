---
title: aaaCreate, cambiar o eliminar una red virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate, cambiar o eliminar una red virtual en Azure."
services: virtual-network
documentationcenter: na
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
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Crear, cambiar o eliminar una red virtual

Obtenga información acerca de cómo toocreate y eliminar una configuración de red y cambio virtual, como servidores DNS y dirección IP espacios, para una red virtual existente.

Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es un aislamiento lógico de hello nube de Azure que está dedicado tooyour suscripción de Azure. Para cada red virtual que cree, puede:
- Elija un tooassign de espacio de dirección. Un espacio de direcciones se compone de uno o más intervalos de direcciones que se definen mediante la notación de Enrutamiento de interdominios sin clases (CIDR), como 10.0.0.0/16.
- Elegir servidor DNS que viene con Azure de toouse hello, o usar su propio servidor DNS. Todos los recursos que están conectados toohello red virtual se asignan este nombres de tooresolve de servidor DNS en la red virtual de Hola.
- Segmento Hola red virtual en subredes, cada uno con su propio intervalo de direcciones, Hola espacio de direcciones de red virtual de Hola. toolearn toocreate, cambiar y eliminar subredes, vea [agregar, cambiar o eliminar subredes](virtual-network-manage-subnet.md).

Este artículo explica cómo toocreate, cambiar y eliminar redes virtuales mediante el modelo de implementación de hello Azure Resource Manager.

## <a name="before"></a>Antes de empezar

Antes de comenzar las tareas de Hola que se describen en este artículo, completar Hola siguiendo los requisitos previos:

- Si le tooworking nueva con las redes virtuales, se recomienda que revise ejercicio hello en [crear la primera red virtual Azure](virtual-network-get-started-vnet-subnet.md). Este ejercicio puede ayudarle a familiarizarse más con las redes virtuales.
- toolearn sobre los límites de las redes virtuales, revisión [el límite de Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Inicie sesión en toohello portal de Azure, hello Azure de línea de comandos (CLI de Azure), PowerShell o la herramienta Azure utilizando su cuenta de Azure. Si no tiene una cuenta de Azure, regístrese para obtener una [cuenta de prueba gratuita](https://azure.microsoft.com/free).
- Si tiene previsto toouse comandos de PowerShell tareas de hello toocomplete descritas en este artículo, primero debe [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello cmdlets de PowerShell de Azure instalado. Ayuda de tooget para los comandos de PowerShell en los ejemplos de hello, escriba `get-help <command> -full`.
- Si tiene previsto toouse tareas de hello toocomplete descritas en este artículo de comandos de CLI de Azure, primero debe [instalar y configurar Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de CLI de Azure instalado. Ayuda de tooget con los comandos de CLI de Azure, escriba `az <command> --help`.


## <a name="create-vnet"></a>Creación de una red virtual

toocreate una red virtual:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Haga clic en **Nuevo** > **Redes** > **Red virtual**.
3. En hello **red Virtual** hoja en hello **seleccionar un modelo de implementación** cuadro, deje **el Administrador de recursos** seleccionada y, a continuación, haga clic en **crear**.
4. En hello **crear red virtual** hoja, escriba o seleccione valores para hello después de la configuración, haga clic en **crear**:
    - **Nombre**: Hola nombre debe ser único en hello [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) Seleccionar red virtual de hello toocreate en. No se puede cambiar nombre de hello después de crea la red virtual de Hola. Puede crear varias redes virtuales con el tiempo. Vea [Convenciones de nomenclatura](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) para obtener sugerencias de nombres. Siga una convención de nomenclatura puede ayudar a que sea más fácil toomanage varias redes virtuales.
    - **Espacio de direcciones**: especificar el espacio de direcciones de hello en la notación CIDR. espacio de direcciones de Hello que define puede ser público o privado (RFC 1918). Si define el espacio de direcciones de hello como público o privado, el espacio de direcciones de hello es accesible sólo desde dentro de la red virtual de hello, de redes virtuales conectadas entre sí y de las redes locales que se ha conectado a red virtual toohello. No se puede agregar Hola después de espacios de direcciones:
        - 224.0.0.0/4 (multidifusión)
        - 255.255.255.255/32 (difusión)
        - 127.0.0.0/8 (bucle invertido)
        - 169.254.0.0/16 (local de vínculo)
        - 168.63.129.16/32 (DNS interno)

      Aunque puede definir un único espacio de direcciones cuando cree una red virtual de hello, puede agregar varios espacios de direcciones una vez creada la red virtual de Hola. toolearn la tooadd una dirección de espacio tooan red virtual existente, vea [agregar o quitar un espacio de direcciones](#add-address-spaces) en este artículo.

      >[!WARNING]
      >Si una red virtual no tiene espacios de direcciones que se superponen con otra red virtual de red o de forma local, no se puede conectar redes Hola dos. Antes de definir un espacio de direcciones, considere si puede ser conveniente tooconnect Hola red virtual tooother las redes virtuales o redes locales en hello futuras.
      >
      >

    - **Nombre de subred**: Hola subred nombre debe ser único dentro de la red virtual de Hola. No se puede cambiar nombre de la subred de hello después de que se crea la subred de Hola. portal de Hello requiere que se defina una subred cuando se crea una red virtual, aunque una red virtual no es necesario toohave ninguna subred. En el portal de hello, puede definir solo una subred cuando se crea una red virtual. Puede agregar más redes virtuales de subredes toohello más adelante, una vez creada la red virtual de Hola. tooadd una red virtual tooa de subred, consulte [crear una subred](virtual-network-manage-subnet.md#create-subnet) en [crear, cambiar o eliminar subredes](virtual-network-manage-subnet.md). Puede crear una red virtual que tenga varias subredes mediante la CLI de Azure o PowerShell.

      >[!TIP]
      >A veces, administradores crean subredes diferentes enrutamiento entre subredes Hola del tráfico toofilter o control. Antes de definir subredes, tenga en cuenta cómo podría desea toofilter y enrutar el tráfico entre las subredes. toolearn más información acerca de filtran el tráfico entre subredes, vea [grupos de seguridad de red](virtual-networks-nsg.md). Azure realiza el enrutamiento de tráfico entre subredes automáticamente, pero puede invalidar las rutas predeterminadas de Azure. toolearn cómo toooverride Azure predeterminado de enrutamiento de tráfico de subred, consulte [rutas definidas por el usuario](virtual-networks-udr-overview.md).
      >

    - **Intervalo de direcciones de subred**: Hola intervalo debe ser Hola espacio de direcciones que especificó para la red virtual de Hola. intervalo más pequeño de Hello que puede especificar es / 29, lo que proporciona ocho direcciones IP de subred Hola. Recursos en reserva en Azure Hola primero y última de las direcciones de cada subred de conformidad con el protocolo. Otras tres direcciones están reservadas para el uso del servicio de Azure. Como resultado, una red virtual con un intervalo de direcciones de subred de /29 tiene solo tres direcciones IP utilizables. Si tiene previsto tooconnect una puerta de enlace VPN de red virtual tooa, debe crear una subred de puerta de enlace. Más información sobre las [consideraciones específicas del intervalo de direcciones de las subredes de puerta de enlace](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Puede cambiar el intervalo de direcciones de hello después de que se crea la subred de hello, en condiciones específicas. toolearn toochange un intervalo de direcciones de subred, vea [cambiar la configuración de subred](#change-subnet) en [agregar, cambiar o eliminar subredes](virtual-network-manage-subnet.md).
    - **Suscripción**: seleccione una [suscripción](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). No se puede usar hello misma red virtual en más de una suscripción de Azure. Sin embargo, puede conectar una red virtual en una red de toovirtual de suscripción en otras suscripciones. tooconnect redes virtuales en distintas suscripciones, use la puerta de enlace de VPN de Azure o el intercambio de tráfico de red virtual. Cualquier recurso de Azure que conectar toohello de red virtual debe estar en hello misma suscripción que la red virtual de Hola.
    - **Grupo de recursos**: seleccione un [grupo de recursos existente](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) o cree uno nuevo. Puede ser un recurso de Azure que conecta la red virtual toohello Hola mismo grupo de recursos como la red virtual de Hola o en otro grupo de recursos.
    - **Ubicación**: seleccione una [ubicación](https://azure.microsoft.com/regions/) de Azure, también conocida como región. Una red virtual solo puede estar en una ubicación de Azure. Sin embargo, puede conectar una red virtual en una red virtual de tooa de ubicación en otra ubicación mediante el uso de una puerta de enlace VPN. Cualquier recurso de Azure que conectar toohello de red virtual debe estar en hello misma ubicación que la red virtual de Hola.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Visualización de las redes virtuales y su configuración

las redes virtuales tooview y configuración:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, haga clic en **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en hello red virtual que se desea establecer la configuración tooview.
4. Hello siguientes opciones aparecen en hoja hello para la red virtual de hello seleccionado:
    - **Información general sobre**: proporciona información acerca de la red virtual de hello, incluido el espacio de direcciones y los servidores DNS. Hello captura de pantalla siguiente muestra valores de información general de Hola para una red virtual denominada **MyVNet**:

        ![Información general de interfaz de red](./media/virtual-network-manage-network/vnet-overview.png)

      En hello **Introducción** hoja, puede mover un red virtual tooa diferentes suscripción o grupo de recursos. toolearn toomove una red virtual, vea [mover recursos tooa otro grupo de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Hola artículo enumeran los requisitos previos y cómo toomove recursos mediante el uso de Hola portal de Azure, PowerShell y CLI de Azure. Deben mover todos los recursos que son redes virtuales toohello conectado con la red virtual de Hola.
    - **Espacio de direcciones**: se enumeran los espacios de direcciones de Hola que se asignan toohello de red virtual. toolearn cómo completar tooadd y quite un espacio de direcciones, Hola pasos en [agregar o quitar un espacio de direcciones](#address-spaces) en este artículo.
    - **Los dispositivos conectados**: se muestran todos los recursos que están conectados toohello red virtual. Hola anterior captura de pantalla, tres interfaces de red y un equilibrador de carga son toohello conectado de red virtual. Se enumeran los recursos nuevos que cree y conectar la red virtual toohello. Si elimina un recurso que estaba conectado toohello red virtual, ya no aparece en la lista de Hola.
    - **Subredes**: se muestra una lista de subredes que existen dentro de la red virtual de Hola. toolearn tooadd y quitar una subred, vea [crear una subred](virtual-network-manage-subnet.md#create-subnet) y [eliminar una subred](virtual-network-manage-subnet.md#delete-subnet) en [agregar, cambiar o eliminar subredes](virtual-network-manage-subnet.md).
    - **Servidores DNS**: puede especificar si hello Azure interno del servidor DNS o un servidor DNS personalizado proporciona resolución de nombres para dispositivos de red virtual toohello conectado. Cuando crea una red virtual mediante Hola portal de Azure, los servidores DNS de Azure se utilizan para la resolución de nombres en una red virtual, de forma predeterminada. los servidores DNS de hello toomodify, Hola completa los pasos de [agregar, cambiar o quitar un servidor DNS](#dns-servers) en este artículo.
    - **Emparejamientos**: si hay emparejamientos existente en la suscripción de hello, que aparecen aquí. Puede ver la configuración de emparejamientos existentes, o crear, cambiar o eliminar emparejamientos. toolearn más información sobre los emparejamientos, consulte [intercambio de tráfico de red Virtual](virtual-network-peering-overview.md).
    - **Propiedades**: muestra la configuración de sobre Hola red virtual, incluidos los Id. de recurso de la red virtual de Hola y Hola suscripción de Azure se encuentra en.
    - **Diagrama**: diagrama de hello proporciona una representación visual de todos los dispositivos de red virtual toohello conectado. diagrama de Hello tiene alguna información clave acerca de los dispositivos de Hola. toomanage un dispositivo en esta vista, en el diagrama de hello, haga clic en el dispositivo de Hola.
    - **Configuración común de Azure**: toolearn más información acerca de la configuración común de Azure, vea Hola siguiente información:
        *   [Registro de actividad](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Control de acceso (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Etiquetas](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Bloqueos](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Script de automatización](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Agregar o quitar un espacio de direcciones

Puede agregar y quitar espacios de direcciones de una red virtual. Un espacio de direcciones debe especificarse en notación CIDR y no pueden solaparse con otros espacios de direcciones dentro de hello misma red virtual. espacios de direcciones de Hello que define pueden ser público o privado (RFC 1918). Si define el espacio de direcciones de hello como público o privado, el espacio de direcciones de hello es accesible sólo desde dentro de la red virtual de hello, de redes virtuales conectadas entre sí y de las redes locales que se ha conectado a red virtual toohello. No se puede agregar Hola después de espacios de direcciones:

- 224.0.0.0/4 (multidifusión)
- 255.255.255.255/32 (difusión)
- 127.0.0.0/8 (bucle invertido)
- 169.254.0.0/16 (local de vínculo)
- 168.63.129.16/32 (DNS interno)

tooadd o quitar un espacio de direcciones:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, seleccione **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en la red virtual de hello para el que desee tooadd o quitar un espacio de direcciones.
4. En hello virtual de red hoja, en **configuración**, haga clic en **espacio de direcciones**.
5. En la hoja de hello para el espacio de direcciones de hello, complete uno de hello siguientes opciones:
    - **Agregar un espacio de direcciones**: especifique Hola nuevo espacio de direcciones. espacio de direcciones de Hello no puede solaparse con un espacio de direcciones existente que se define para la red virtual de Hola.
    - **Quitar un espacio de direcciones**: haga clic con el botón derecho en un espacio de direcciones y, después, haga clic en **Quitar**. Si existe una subred en el espacio de direcciones de hello, no se puede quitar el espacio de direcciones de Hola. tooremove un espacio de direcciones, primero debe eliminar las subredes (y todos los recursos que están conectados toohello subredes) que existen en el espacio de direcciones de Hola.
6. Haga clic en **Guardar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|Solo Resource Manager|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Agregar, cambiar o quitar un servidor DNS

Registran todas las máquinas virtuales que están conectados toohello red virtual con los servidores DNS de Hola que especifique para la red virtual de Hola. También usan Hola especificado servidor DNS para la resolución de nombres. Cada interfaz de red (NIC) en una máquina virtual puede tener su propia configuración de servidor DNS. Si una NIC tiene su propia configuración del servidor DNS, invalidan la configuración Hola del servidor DNS para la red virtual de Hola. toolearn más información acerca de la configuración de NIC DNS, consulte [tareas de la interfaz y la configuración de red](virtual-network-network-interface.md#change-dns-servers). toolearn más información acerca de la resolución de nombres para máquinas virtuales e instancias de rol de servicios de nube de Azure, consulte [la resolución de nombres para máquinas virtuales e instancias de rol](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, cambiar o quitar un servidor DNS:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, seleccione **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en hello red virtual que desea establecer la configuración del DNS toochange.
4. En hello virtual de red hoja, en **configuración**, haga clic en **servidores DNS**.
5. Seleccione una de las siguientes opciones en la hoja de Hola que enumera los servidores DNS de hello:
    - **Predeterminado (viene con Azure)**: todos los nombres de los recursos y las direcciones IP privadas son servidores de DNS de Azure de toohello registrados automáticamente. Puede resolver nombres entre todos los recursos que están conectado toohello misma red virtual. No puede utilizar los nombres de tooresolve de esta opción a través de redes virtuales. nombres de tooresolve varias redes virtuales, debe usar un servidor DNS personalizado.
    - **Personalizado**: puede agregar uno o varios servidores, seguridad de Azure toohello limitar para una red virtual. toolearn más información acerca de los límites del servidor DNS, consulte [el límite de Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Tener Hola siguientes opciones:
        - **Agregar una dirección**: agrega la lista de servidores DNS de hello server tooyour red virtual. Esta opción también registra el servidor DNS de hello con Azure. Si ya ha registrado un servidor DNS con Azure, puede seleccionar ese servidor DNS en la lista de Hola.
        - **Quitar una dirección**: haga clic en siguiente servidor toohello que desea tooremove, **X**. Eliminar servidor hello quita servidor hello solo de esta lista de red virtual. servidor DNS de Hello permanece registrado en Azure para los otro toouse de redes virtuales.
        - **Reordenar las direcciones de servidor DNS**: es importante tooverify que estos se enumeran los servidores DNS en hello corregir orden para el entorno. Se utilizan listas de servidores DNS en orden de Hola que se especifican. No funcionan como una instalación round robin. Si puede tener acceso el primer servidor DNS hello en lista de Hola, cliente hello usa ese servidor DNS, independientemente de si el servidor DNS de hello está funcionando correctamente. Quitar todos los servidores DNS de Hola que aparecen y, a continuación, agregarlos en orden de Hola que desee.
        - **Cambiar una dirección**: Resalte servidor DNS de hello en la lista de hello y, a continuación, escriba Hola nuevo nombre.
6. Haga clic en **Guardar**.
7. Reinicie las máquinas virtuales de Hola que están conectados toohello red virtual, por lo que, se les asignará la nueva configuración de servidor DNS Hola. VM continúan toouse su configuración de DNS actual hasta que se reinicien.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Eliminación de una red virtual

Puede eliminar una red virtual solo si no hay ningún tooit conectado de recursos. Si no hay recursos de subred de tooany conectado en red virtual de hello, primero debe eliminar recursos Hola subredes tooall conectados en red virtual de Hola. pasos de Hola que seguir toodelete un recurso varían en función recursos Hola. toolearn cómo leer recursos toodelete toosubnets conectado, Hola documentación para cada tipo de recurso que desee toodelete. toodelete una red virtual:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, haga clic en **redes virtuales**.
3. En hello **redes virtuales** hoja, red virtual seleccione Hola desea toodelete.
4. En la hoja de la red virtual de hello, tooconfirm que no hay ningún dispositivo conectado toohello red virtual, en **configuración**, haga clic en **dispositivos conectados**. Si hay dispositivos conectados, debe eliminarlas antes de poder eliminar la red virtual de Hola. Si no hay ningún dispositivo conectado, haga clic en **Información general**.
5. Hola parte superior de la hoja de hello, haga clic en hello **eliminar** icono.
6. eliminación de hello tooconfirm de red virtual de hello, haga clic en **Sí**.


**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Pasos siguientes

- toocreate una máquina virtual y, a continuación, conéctelo tooa de red virtual, vea [crear una red virtual y conectar máquinas virtuales](virtual-network-get-started-vnet-subnet.md#create-vms).
- tráfico de red de toofilter entre subredes dentro de una red virtual, vea [crear grupos de seguridad de red](virtual-networks-create-nsg-arm-pportal.md).
- toopeer una red virtual tooanother de red virtual, vea [crear una red virtual emparejamiento](virtual-network-create-peering.md#portal).
- toolearn sobre las opciones para conectar una red local de tooan de red virtual, vea [acerca de la puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
