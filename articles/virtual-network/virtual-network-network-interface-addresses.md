---
title: aaaConfigure las direcciones IP de una interfaz de red de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd, cambiar y quitar las direcciones IP públicas y privadas para una interfaz de red."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Incorporación, cambio o eliminación de direcciones IP para una interfaz de red de Azure

Obtenga información acerca de cómo tooadd, cambiar y quitar direcciones IP públicas y privadas para una interfaz de red. Las direcciones IP privadas asignadas de interfaz de red de tooa habilitar un toocommunicate de máquina virtual con otros recursos de red virtual de Azure y las redes conectadas. Una dirección IP privada también permite la comunicación saliente toohello Internet con una dirección IP imprevisible. A [dirección IP pública](virtual-network-public-ip-address.md) asignado tooa interfaz de red permite la comunicación entrante tooa virtual máquina de hello Internet. dirección de Hello también permite la comunicación saliente de máquina virtual de hello toohello Internet con una dirección IP predecible. Para detalles, consulte [Comprender las conexiones salientes en Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Si necesita toocreate, cambiar o eliminar una interfaz de red, lea hello [administrar una interfaz de red](virtual-network-network-interface.md) artículo. Si necesita tooor quitar interfaces de red de una máquina virtual de interfaces de red de tooadd, leer hello [interfaces de red de agregar o quitar](virtual-network-network-interface-vm.md) artículo. 


## <a name="before-you-begin"></a>Antes de empezar

Hola completa después de tareas antes de completar cualquier pasos en cualquier sección de este artículo:

- Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn de artículo sobre los límites de direcciones IP públicas y privadas.
- Inicie sesión en Azure toohello [portal](https://portal.azure.com), interfaz de línea de comandos (CLI) de Azure o Azure PowerShell con una cuenta de Azure. Si todavía no tiene una cuenta de Azure, regístrese para obtener una [cuenta de evaluación gratuita](https://azure.microsoft.com/free).
- Si el uso de PowerShell comandos toocomplete tareas en este artículo, [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene Hola versión más reciente de los cmdlets de PowerShell de Azure de hello instalados. Ayuda de tooget para los comandos de PowerShell, con ejemplos, escriba `get-help <command> -full`.
- Si utiliza la interfaz de línea de comandos (CLI) de Azure comandos toocomplete tareas en este artículo, [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello en la nube Shell **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Incorporación de direcciones IP

Puede agregar tantos [privada](#private) y [público](#public) [IPv4](#ipv4) enumeran direcciones como interfaz de red necesarios tooa, dentro de los límites de Hola Hola [el límite de Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artículo. No se puede usar Hola portal tooadd una interfaz de red existente y tooan con direcciones IPv6 (aunque puede usar Hola portal tooadd una interfaz de red de IPv6 dirección tooa privada cuando se crea la interfaz de red de Hola). Puede usar PowerShell u Hola CLI tooadd una privada IPv6 dirección tooone [configuración IP secundaria](#secondary) (siempre y cuando no hay ninguna configuración de IP secundaria existente) para una red existente interfaz que no está conectado tooa virtual máquina. No se puede usar cualquier tooadd herramienta una interfaz de red de tooa de dirección IPv6 pública. Consulte [IPv6](#ipv6) para detalles sobre cómo usar las direcciones IPv6. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de Hola que desee dirección tooadd IPv4 para.
4. Haga clic en **configuraciones IP** en hello **configuración** sección de hoja de Hola de interfaz de red de Hola que seleccionó.
5. Haga clic en **+ agregar** en hoja Hola que se abre para las configuraciones de IP.
6. Especifique Hola siguiente, a continuación, haga clic en **Aceptar** tooclose hello **configuración IP agregar** hoja:

    |Configuración|¿Necesario?|Detalles|
    |---|---|---|
    |Nombre|Sí|Debe ser único para la interfaz de red de Hola|
    |Tipo|Sí|Dado que va a agregar una interfaz de red existente y tooan con configuración IP, y cada interfaz de red debe tener un [principal](#primary) es la única opción de configuración de IP, **secundaria**.|
    |Método de asignación de direcciones IP privadas|Sí|[**Dinámica** ](#dynamic) las direcciones pueden cambiar si se reinicia la máquina virtual de hello después de haber sido previamente Hola detenido estado (desasignada). Azure asigna una dirección disponible del espacio de direcciones de Hola Hola subred Hola interfaz de red está conectada a. [**Estática** ](#static) direcciones no se liberan hasta que se elimina la interfaz de red de Hola. Especifique una dirección IP del intervalo de espacio de direcciones de subred de Hola que no está actualmente en uso por otra configuración de IP.|
    |Dirección IP pública|No|**Deshabilitado:** ningún recurso de dirección IP pública está asociada actualmente toohello configuración de IP. **Habilitada:** seleccione una dirección IP pública IPv4 existente o cree una nueva. toolearn cómo leer toocreate una dirección IP pública, hello [direcciones IP públicas](virtual-network-public-ip-address.md#create-a-public-ip-address) artículo.|
7. Agregar manualmente secundaria privada IP direcciones toohello sistema operativo máquina virtual siguiendo las instrucciones de Hola Hola [asignar varias direcciones IP de los sistemas operativos de toovirtual máquina](virtual-network-multiple-ip-addresses-portal.md#os-config) artículo. Vea [privada](#private) direcciones IP para conocer consideraciones especiales antes de agregar manualmente el sistema operativo de la máquina virtual de tooa direcciones IP. No agregue ningún sistema de operativo máquina virtual pública del toohello de direcciones IP.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Cambio de configuración de las direcciones IP

Quizás necesite toochange método de asignación de hello de una dirección IPv4, dirección IPv4 estática a cambio hello, o dirección IP pública de cambio Hola asignado tooa interfaz de red. Si está cambiando la dirección IPv4 privada de Hola de una configuración IP secundaria asociada con una interfaz de red secundaria en una máquina virtual (obtener más información acerca de [interfaces de red principal y secundaria](virtual-network-network-interface-vm.md#about)), Hola lugar virtual máquina en hello detenida (desasignada) de estado antes de completar los pasos de hello: 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desee tooview o cambiar la configuración de dirección IP de.
4. Haga clic en **configuraciones IP** en hello **configuración** sección de hoja de Hola de interfaz de red de Hola que seleccionó.
5. Haga clic en configuración de IP de Hola que desee toomodify de lista de hello en la hoja de Hola que se abre para las configuraciones de IP.
6. Cambiar la configuración de hello, según sea necesario, con información de hello acerca de la configuración de hello en el paso 6 de hello [agregar una configuración IP](#create-ip-config) sección de este artículo. Haga clic en **guardar** tooclose hoja de hello para la configuración de IP de hello ha cambiado.

>[!NOTE]
>Si la interfaz de red principal de hello tiene varias configuraciones de IP y cambiar dirección IP privada de Hola Hola principal de configuración de IP, se debe reasignar manualmente Hola principal y secundaria IP direcciones toohello interfaz de red en Windows (no obligatorio para Linux). toomanually asignar la interfaz de red de tooa de direcciones IP dentro de un sistema operativo, leer hello [asignar varias direcciones IP toovirtual máquinas](virtual-network-multiple-ip-addresses-portal.md#os-config) artículo. Vea [privada](#private) direcciones IP para conocer consideraciones especiales antes de agregar manualmente el sistema operativo de la máquina virtual de tooa direcciones IP. No agregue ningún sistema de operativo máquina virtual pública del toohello de direcciones IP.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Eliminación de direcciones IP

Puede quitar [privada](#private) y [público](#public) direcciones IP desde una interfaz de red, pero una interfaz de red siempre debe tener al menos un tooit de dirección asignada de IPv4 privada.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desea tooremove las direcciones IP.
4. Haga clic en **configuraciones IP** en hello **configuración** sección de hoja de Hola de interfaz de red de Hola que seleccionó.
5. Haga clic en un [secundaria](#secondary) configuración de IP (no se puede eliminar hello [principal](#primary) configuración) desea toodelete, haga clic en **eliminar**, a continuación, haga clic en **sí**  eliminación de hello tooconfirm. Si la configuración de hello tenía un recurso de dirección IP público asociados tooit, recursos Hola se desasoció de configuración de IP de hello, pero no se elimina el recurso de Hola.
6. Hola cerrar **configuraciones IP** hoja.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Configuraciones IP

[Privada](#private) y (opcionalmente) [público](#public) direcciones IP se asignan tooone o más configuraciones de IP asignan tooa interfaz de red. Hay dos tipos de configuraciones IP:

### <a name="primary"></a>Principal

Cada interfaz de red tiene asignada una configuración IP principal. Una configuración IP principal:

- Tiene una [privada](#private) [IPv4](#ipv4) tooit dirección asignada. No se puede asignar una privada [IPv6](#ipv6) configuración de IP de dirección tooa primaria.
- También puede tener un [público](#public) tooit dirección asignada de IPv4. No se puede asignar una público tooa principal o secundaria IP configuración de direcciones IPv6. Sin embargo, puede, asigne un IPv6 público direcciones de equilibrador de carga de Azure tooan, que puede cargar equilibrar la dirección IPv6 privada de la máquina virtual de tráfico tooa. Para más información, consulte [detalles y limitaciones de IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secundario

Además tooa configuración de IP principal, una interfaz de red puede haber cero o más configuraciones de IP secundarias asignadas tooit. Una configuración IP secundaria:

- Debe tener un tooit privada de dirección asignada de IPv4 o IPv6. Si la dirección de hello es IPv6, la interfaz de red de hello solo puede tener una configuración IP secundaria. Si la dirección de hello es IPv4, interfaz de red de hello puede tener varias configuraciones de IP secundarias asignadas tooit. toolearn más información acerca de cuántas direcciones IPv4 públicas y privadas pueden asignarse tooa interfaz de red, consulte hello [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artículo.  
- También se puede tener un tooit de dirección asignada de IPv4 pública, si la dirección IP privada de hello es IPv4. Si la dirección IP privada de hello es IPv6, no se puede asignar una pública IPv4 o IPv6 dirección toohello configuración de IP. Asignación de interfaz de red de tooa de direcciones IP múltiples es útil en escenarios como:
    - Hospede varios sitios web o servicios con direcciones IP y certificados SSL diferentes en un único servidor.
    - Una máquina virtual que actúa como una aplicación virtual de red, por ejemplo, un firewall o un equilibrador de carga.
    - Hola tooadd capacidad cualquiera de hello direcciones IPv4 privadas para cualquier grupo de tooan back-end de equilibrador de carga de Azure de interfaces de red de Hola. Hola anteriores, sólo Hola principal dirección IPv4 para la interfaz de red principal de hello podría agregarse tooa grupo de back-end. toolearn más información acerca de cómo tooload equilibrar varias configuraciones de IPv4, vea hello [varias configuraciones de IP de equilibrio de carga](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo. 
    - tooload de capacidad de Hello equilibrar una interfaz de red de tooa asignado de dirección IPv6. toolearn más información acerca de cómo tooload equilibrar tooa direcciones privadas de IPv6, consulte hello [las direcciones IPv6 de equilibrar la carga](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.


## <a name="address-types"></a>Tipos de direcciones

Puede asignar los siguientes tipos de tooan de direcciones IP de hello [configuración IP](#ip-configurations):

### <a name="private"></a>Privada

Privada [IPv4](#ipv4) direcciones habilitar un toocommunicate de máquina virtual con otros recursos en una red virtual o en otras redes conectadas. Una máquina virtual no se puede comunicar entrante a, ni pueden comunicarse salientes con privado máquina virtual de hello [IPv6](#ipv6) dirección, con una excepción. Una máquina virtual pueden comunicarse con el equilibrador de carga de Azure de hello mediante una dirección IPv6. Para más información, consulte [detalles y limitaciones de IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

De forma predeterminada, los servidores DHCP de Azure Hola asignan dirección IPv4 privada de Hola para hello [configuración IP primaria](#primary) de interfaz de red de hello red interfaz toohello en el sistema operativo de máquina virtual de Hola. A menos que es necesario, se debe nunca manualmente establecer Hola dirección IP de una interfaz de red en el sistema operativo de la máquina virtual Hola. 

> [!WARNING]
> Si la dirección IPv4 de hello establece como dirección IP principal de Hola de una interfaz de red en el sistema operativo de una máquina virtual es alguna vez diferente a Hola dirección IPv4 privada asignada toohello de configuración de IP principal de interfaz de red principal de hello adjunta tooa máquina virtual dentro de Azure, perderá conectividad toohello virtual machine.

Existen escenarios donde es establecer la dirección IP toomanually necesarios Hola de una interfaz de red en el sistema operativo de la máquina virtual Hola. Por ejemplo, debe establecer manualmente direcciones IP de un sistema operativo Windows del principal y secundario del Hola al agregar varios tooan de direcciones IP máquina virtual de Azure. Para una máquina virtual de Linux, puede que solo tenga toomanually conjunto Hola secundaria las direcciones IP. Vea [direcciones de IP de Agregar sistema operativo de la VM de tooa](virtual-network-multiple-ip-addresses-portal.md#os-config) para obtener más información. Cuando se establece manualmente dirección IP de hello en el sistema operativo de hello, se recomienda que asigne siempre la configuración de IP de hello direcciones toohello para una interfaz de red con método de asignación estático (en lugar de dinámico) de Hola. Asignar dirección hello mediante el método estático de hello garantiza que la dirección de hello no cambia dentro de Azure. Si alguna vez necesita dirección de hello toochange asignado tooan configuración de IP, se recomienda:

1. máquina virtual de tooensure Hola está recibiendo una dirección de los servidores DHCP de Azure hello, modifique la asignación de Hola de hello IP dirección inversa tooDHCP dentro de sistema operativo de Hola y máquina virtual de Hola de reinicio.
2. Detener (desasignar) máquina virtual de Hola.
3. Cambiar la dirección IP de hello para la configuración de IP de hello dentro de Azure.
4. Inicie la máquina virtual de Hola.
5. [Configurar manualmente](virtual-network-multiple-ip-addresses-portal.md#os-config) Hola secundaria IP direcciones incluidas en el sistema operativo de hello (y también dirección IP principal de hello dentro de Windows) toomatch establece dentro de Azure.
 
Siguiendo los pasos anteriores de Hola Hola privada dirección asignada toohello interfaz de red IP en Azure y, en el sistema operativo de una máquina virtual, permanece igual Hola. tookeep realizar un seguimiento de los cuales máquinas virtuales dentro de la suscripción que haya configurado manualmente direcciones IP dentro de un sistema operativo, considere la posibilidad de agregar un Azure [etiqueta](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello las máquinas virtuales. Por ejemplo, puede usar "Asignación de dirección IP: estática". De esta manera, puede encontrar fácilmente máquinas virtuales de hello en la suscripción que haya configurado manualmente Hola dirección IP en el sistema operativo de Hola.

Además tooenabling un toocommunicate de máquina virtual con otros recursos dentro de hello mismo, o conectadas redes virtuales, una dirección IP privada de direcciones también permite un toohello saliente Internet toocommunicate de máquina virtual. Las conexiones salientes son traducido Azure tooan la dirección IP pública impredecible de dirección de red de origen. más información acerca de Azure conectividad saliente de Internet, leer hello toolearn [Azure conectividad a Internet saliente](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo. No se puede comunicar la dirección IP privada de la máquina virtual tooa entrantes de hello Internet.

### <a name="public"></a>Público

Las direcciones IP públicas permiten conectividad entrante tooa virtual machine de hello Internet. Las conexiones salientes toohello Internet use una dirección IP predecible. Consulte [Comprender las conexiones salientes en Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para detalles. Puede asignar una configuración de IP de tooan de direcciones IP pública, pero no es necesario. Si no asigna una máquina de virtual de tooa de dirección IP pública, todavía puede comunicarse toohello saliente de Internet a través de su dirección IP privada. más información acerca de las direcciones IP públicas, leer hello toolearn [dirección IP pública](virtual-network-public-ip-address.md) artículo.

Hay límites de número de toohello de privado y direcciones IP públicas que puede asignar tooa de interfaz de red. Para obtener más información, lea hello [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artículo.

> [!NOTE]
> Azure traduce privada tooa pública dirección IP una máquina virtual. Como resultado, no es consciente de las direcciones IP públicas asignadas tooit sistema operativo de hello, así que no hay ninguna necesidad de tooever manualmente, asigne una dirección IP pública en el sistema operativo de Hola.

## <a name="assignment-methods"></a>Métodos de asignación

Se asignan direcciones IP públicas y privadas mediante Hola siguientes métodos de asignación:

### <a name="dynamic"></a>Dinámica

Las direcciones IPv4 e IPv6 (opcionalmente) privadas dinámicas se asignan de manera predeterminada. Pueden cambiar las direcciones dinámicas si se pone de máquina virtual de hello en hello detenido (desasignado) de estado, a continuación, se inició. Si no desea toochange de direcciones IPv4 para la vida de la máquina virtual de Hola Hola, asigne direcciones de hello mediante el método estático de Hola. Solo se puede asignar una dirección IPv6 privada mediante el método de asignación dinámica de hello. No se puede asignar mediante cualquier método una configuración de IP de tooan de direcciones IPv6 pública.

### <a name="static"></a>estática

Direcciones asignadas mediante el método estático de hello no cambia hasta que se elimina una máquina virtual. Asignar manualmente una privada IPv4 dirección tooan configuración IP estática del espacio de direcciones de Hola de interfaz de red de Hola Hola subred se muestra en. (Opcionalmente) puede asignar una pública o privada IPv4 dirección tooan configuración IP estática. No se puede asignar una pública o privada IPv6 dirección tooan IP estática. toolearn más información acerca de cómo Azure asigna direcciones IPv4 públicas y estáticas, vea hello [dirección IP pública](virtual-network-public-ip-address.md) artículo.

## <a name="ip-address-versions"></a>Versiones de direcciones IP

Puede especificar hello las siguientes versiones cuando asignar direcciones:

### <a name="ipv4"></a>IPv4

Cada interfaz de red debe tener una configuración IP [principal](#primary) con una dirección [IPv4](#private) [privada](#ipv4)asignada. Puede agregar una o más configuraciones IP [secundarias](#secondary) en que cada una tenga una dirección IPv4 privada y, de manera opcional, una dirección IP [pública](#public) IPv4.

### <a name="ipv6"></a>IPv6

Puede asignar cero o una privada [IPv6](#ipv6) dirección tooone secundaria configuración IP de una interfaz de red. interfaz de red de Hello no puede tener cualquier configuración IP secundaria existente. No se puede agregar una configuración IP con una dirección IPv6 mediante el portal de Hola. Usar PowerShell o hello CLI tooadd una configuración de IP con una privada IPv6 dirección tooan interfaz de red existente. interfaz de red de Hello no puede ser tooan adjunto existente de la máquina virtual.

> [!NOTE]
> Aunque puede crear una interfaz de red con una dirección IPv6 mediante el portal de hello, no se puede agregar una red interfaz tooa nueva o existente máquina virtual existente, mediante el portal de Hola. Use PowerShell o hello Azure CLI 2.0 toocreate una interfaz de red con una dirección IPv6 privada, y asociar la interfaz de red de hello al crear una máquina virtual. No se puede adjuntar una interfaz de red con una dirección IPv6 privada tooit tooan existente virtual máquina asignada. No se puede agregar una configuración de IP privada de tooan dirección de IPv6 para cualquier máquina virtual de red interfaz conectada tooa utilizar alguna herramienta (portal, CLI o PowerShell).

No se puede asignar una público tooa principal o secundaria IP configuración de direcciones IPv6.

## <a name="next-steps"></a>Pasos siguientes
toocreate una máquina virtual con distintas configuraciones de IP, leer Hola siguientes artículos:

|Tarea|Herramienta|
|---|---|
|Creación de una máquina virtual con varias NIC|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creación de una máquina virtual con una sola interfaz de red y varias direcciones IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creación de una máquina virtual con una sola interfaz de red y una dirección IPv6 privada (detrás de Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Plantilla de Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
