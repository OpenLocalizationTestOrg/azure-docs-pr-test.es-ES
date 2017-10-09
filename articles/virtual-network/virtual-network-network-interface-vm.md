---
title: "quitar tooor de interfaces de red aaaAdd de máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooor de interfaces de red tooadd quitar interfaces de red de máquinas virtuales."
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Agregue las interfaces de red tooor quitar de máquinas virtuales

Obtenga información acerca de cómo tooadd una red existente al crear una máquina virtual de la interfaz o agregar o quitar interfaces de red de una máquina virtual existente en hello detenido estado (desasignada). Una interfaz de red permite un toocommunicate de máquina Virtual (VM) de Azure con Internet, Azure y recursos locales. Una máquina virtual puede tener una o varias interfaces de red. 

Si necesita tooadd, cambiar o quitar direcciones IP para una interfaz de red, lea hello [administrar direcciones IP de interfaz de red](virtual-network-network-interface-addresses.md) artículo. Si necesita toocreate, cambiar o eliminar interfaces de red, lea hello [administrar interfaces de red](virtual-network-network-interface.md) artículo.

## <a name="before"></a>Antes de empezar

Hola completa después de tareas antes de completar cualquier pasos en cualquier sección de este artículo:

- Obtenga información sobre cuántas interfaces de red admitidas por cada tamaño de máquina virtual de Windows y Linux revisando hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual.
- Inicie sesión en Azure toohello [portal](https://portal.azure.com), interfaz de línea de comandos (CLI) de Azure o Azure PowerShell con una cuenta de Azure. Si todavía no tiene una cuenta de Azure, regístrese para obtener una [cuenta de evaluación gratuita](https://azure.microsoft.com/free).
- Si el uso de PowerShell comandos toocomplete tareas en este artículo, [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene Hola versión más reciente de los cmdlets de PowerShell de Azure de hello instalados. Ayuda de tooget para los comandos de PowerShell, con ejemplos, escriba `get-help <command> -full`.
- Si utiliza la interfaz de línea de comandos (CLI) de Azure comandos toocomplete tareas en este artículo, [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello en la nube Shell **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com).

## <a name="about"></a>Sobre interfaces de red y máquinas virtuales

Puede agregar (adjuntar) un tooa de interfaz de red existente VM al crear Hola VM, proporciona la interfaz de red de hello no está actualmente conectado tooanother máquina virtual. Puede agregar una interfaz de red a, o quitar (desconectar) una red de la interfaz toofrom una máquina virtual existente, siempre Hola VM se detiene en hello estado (desasignada). Si crea una máquina virtual mediante el portal de Azure hello, portal de hello crea una interfaz de red automáticamente con la configuración predeterminada. portal de Hello ¿no le permite:

- Especifique un tooadd de interfaz de red existente al crear Hola VM
- Creación de una máquina virtual con varias interfaces de red
- Especifique un nombre para la interfaz de red de hello (portal de hello crea interfaz de red de hello con un nombre predeterminado)

Puede usar Azure PowerShell o CLI de hello toocreate una interfaz de red o la máquina virtual con todos los atributos anteriores Hola que no se puede usar portal de Hola de. Antes de completar las tareas de hello en las secciones siguientes de hello, tenga en cuenta los siguiente de hello las restricciones y los comportamientos:

- Todos los tamaños de máquina virtual admiten dos interfaces de red como mínimo, aunque algunos admiten más. Hola más allá, algunas VM tamaños solo admiten una interfaz de red. toolearn cuántas interfaces de red es compatible con el tamaño de cada máquina virtual, leer hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual. 
- Hola anteriores, interfaces de red sólo pudieron ser tooVMs agregada que admite varias interfaces de red y se crearon con al menos dos interfaces de red. No se pudo agregar un tooa de interfaz de red virtual que se creó con una interfaz de red, incluso si Hola tamaño de VM admite varias interfaces de red. Por el contrario, sólo se pueden quitar interfaces de red de una máquina virtual con al menos tres interfaces de red, porque las máquinas virtuales creadas con al menos dos interfaces de red siempre toohave no tenían al menos dos interfaces de red. Ninguna de estas restricciones se aplican ya. Ahora puede crear una máquina virtual con cualquier número de interfaces de red (el número de toohello admitidos Hola tamaño de máquina virtual) y agregar o quitar cualquier número de interfaces de red (desde el estado de las máquinas virtuales en hello detenido (desasignadas)), siempre y cuando Hola VM siempre tiene al menos una interfaz de red.
- De forma predeterminada, la primera interfaz de red hello en una máquina virtual se define como hello *principal* interfaz de red. Todas las demás interfaces de red en hello VM son *secundaria* interfaces de red.
- Interfaces de red principal están asignadas una puerta de enlace predeterminada por los servidores de DHCP de Azure de hello, pero no interfaces de red secundarias. Puesto que las interfaces de red secundarias no tienen asignada una puerta de enlace predeterminada, no se pueden comunicar con recursos ajenos a su subred de forma predeterminada. interfaces de red secundarias tooenable en un toocommunicate de máquina virtual de Windows con los recursos fuera de su subred, agregar rutas toohello SO con hello `route add` comando desde una línea de comandos de Windows. Para máquinas virtuales de Linux, puesto que el comportamiento predeterminado de hello utiliza host débil enrutamiento, es recomendable restringir el tráfico de red secundaria interfaces tooa sola subred. Si necesita conectividad fuera de la subred de Hola para las interfaces de red secundaria, habilitar enrutamiento tooensure esa entrada basada en directivas y el tráfico de salida utiliza Hola misma interfaz de red.
- De forma predeterminada, todo el tráfico saliente de Hola que se envía VM dirección IP de hello asigna toohello de configuración de IP principal de interfaz de red principal de Hola. Controlar la dirección IP que se usa para el tráfico saliente en el sistema operativo de la máquina virtual de hello, pero de forma predeterminada, es a través de la interfaz de red principal de Hola.
- En hello más allá, todas las máquinas virtuales dentro de hello mismo conjunto de disponibilidad eran toohave requiere una red única o varias interfaces. Las máquinas virtuales con cualquier número de red interfaces ahora pueden existir en Hola el mismo conjunto de disponibilidad, el número de toohello admitido Hola tamaño de máquina virtual. Solo puede agregar un conjunto cuando se crea aunque de disponibilidad de tooan de máquina virtual. más información acerca de los conjuntos de disponibilidad, leer hello toolearn [administrar Hola disponibilidad de máquinas virtuales en Azure](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) artículo.
- Mientras que las interfaces de red en hello misma máquina virtual puede ser toodifferent conectado subredes dentro de una red virtual, todas las interfaces de red de hello deben ser toohello conectado misma red virtual.
- Puede agregar cualquier dirección IP para cualquier configuración de IP de cualquier grupo de tooan back-end de equilibrador de carga de Azure de interfaz de red principal o secundaria. Hola anteriores, sólo Hola dirección IP principal para la interfaz de red principal de hello podría agregarse tooa grupo de back-end. más información acerca de las direcciones IP y las configuraciones, leer hello toolearn [agregar, cambiar o quitar las direcciones IP](virtual-network-network-interface-addresses.md) artículo.
- Eliminar una máquina virtual no elimina las interfaces de red de Hola que son tooit adjunto. Cuando se elimina una máquina virtual, interfaces de red de Hola se desasocian del Hola máquina virtual. Puede agregar toodifferent de interfaces de red de hello las máquinas virtuales o eliminarlas.
- Si una interfaz de red tiene una privada tooit dirección asignada de IPv6, puede adjuntarla tooa VM al crear Hola máquina virtual. No se puede adjuntar una interfaz de red con un tooa de dirección IPv6 asignado VM después de crea Hola máquina virtual. Si se asocia una interfaz de red con una dirección IPv6 privada asignada al crear una máquina virtual, solo puede adjuntar esa máquina virtual red interfaz toohello, independientemente de cuántas interfaces de red que admite el tamaño de la máquina virtual de Hola. Vea [direcciones IP de interfaz de red](virtual-network-network-interface-addresses.md) toolearn más información acerca de la asignación de IP direcciones toonetwork interfaces.

## <a name="vm-create"></a>Agregar existente tooa de interfaces de red nueva máquina virtual

Cuando se crea una máquina virtual a través del portal de hello, portal de hello crea una interfaz de red con la configuración predeterminada y lo adjunta toohello VM automáticamente. No se puede agregar tooa de interfaces de red existentes nueva máquina virtual, o cree una máquina virtual con varias interfaces de red con hello portal de Azure. Puede realizar tanto operaciones utilizando Hola CLI o PowerShell. Puede agregar como tooa VM de interfaces de red como Hola va a crear es compatible con el tamaño de máquina virtual. toolearn más información acerca de la red cuántas interfaces cada admite de tamaño VM, leer hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual. interfaces de red de Hello agregar tooa VM actualmente no pueden ser tooanother adjunto máquina virtual. más sobre la creación de interfaces de red, lea hello toolearn [administrar interfaces de red](virtual-network-network-interface.md#create-a-network-interface) artículo.

> [!WARNING]
> Si una interfaz de red tiene una dirección IPv6 privada asignada tooit, solo puede agregar Hola red interfaz toohello virtual machine al crear la máquina virtual de Hola. No se puede adjuntar más de una máquina de virtual de toohello de interfaz de red al crear máquinas virtuales de Hola o después de Hola se crea la máquina virtual, como una dirección IPv6 se asigna la máquina virtual de tooa red interfaz conectada tooa. Vea [direcciones IP de interfaz de red](virtual-network-network-interface-addresses.md) toolearn más información acerca de la asignación de IP direcciones toonetwork interfaces.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Agregar una existente tooan de interfaz de red existente de la máquina virtual

Puede agregar como tooa VM de interfaces de red como Hola tamaño de máquina virtual que se va a agregar toosupports de interfaces de red. toolearn cuántas interfaces de red es compatible con el tamaño de cada máquina virtual, leer hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual. Hola VM desea tooadd una toomust de interfaz de red compatible con número de Hola de interfaces de red que desee tooadd y debe estar en hello detenido (desasignado) estado. interfaces de red de Hello desea tooadd actualmente no pueden ser tooanother adjunto máquina virtual. No se puede agregar tooan de interfaces de red existente de la máquina virtual con hello portal de Azure. interfaces de red tooadd tooan existente de la máquina virtual, debe utilizar Hola CLI o PowerShell. 

> [!WARNING]
> Si una interfaz de red tiene una dirección IPv6 privada asignada tooit, no se puede agregar máquina virtual existente de tooan. Solo puede agregar una interfaz de red con una asignado privada IPv6 dirección tooa máquina virtual cuando se crea una máquina virtual. Vea [direcciones IP de interfaz de red](virtual-network-network-interface-addresses.md) toolearn más información acerca de la asignación de IP direcciones toonetwork interfaces.

|Herramienta|Comando|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (referencia) o [pasos detallados](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (referencia) o [pasos detallados](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a> Visualización de interfaces de red para una máquina virtual

Puede ver Hola red interfaces conectadas actualmente tooa VM toolearn acerca de la configuración de cada interfaz de red, y asignar las direcciones IP de hello tooeach interfaz de red. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que se asigna el rol de propietario, Colaborador o colaborador de la red de Hola para su suscripción. vea toolearn más información acerca de la asignación de roles tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *máquinas virtuales*. Cuando **máquinas virtuales** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **máquinas virtuales** hoja que aparece, haga clic en nombre de Hola de máquina virtual que desee tooview interfaces de red para hello.
4. Hola **configuración** sección de hoja de máquina virtual de Hola que aparece para hello VM que ha seleccionado, haga clic en **interfaces de red**. toolearn acerca de la configuración de la interfaz de red y cómo toochange usarlas, lea la sección hello [administrar interfaces de red](virtual-network-network-interface.md) artículo. toolearn acerca de cómo agregar, cambiar o quitar direcciones IP asignadas tooa interfaz de red, consulte [direcciones IP administrar](virtual-network-network-interface-addresses.md).

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a> Eliminación de interfaces de red de una máquina virtual

Hello VM desea tooremove (o separar) desde una interfaz de red debe estar en Hola detenida (desasignada) y deben haber interfaces de red al menos dos conectados actualmente tooit. Puede quitar cualquier interfaz de red, pero Hola VM siempre debe tener al menos una red interfaz conectada tooit. Si quita una interfaz de red principal, Azure asigna Hola atributo principal toohello interfaz de red ha sido toohello adjunto Hola VM más largo. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que se asigna el rol de propietario, Colaborador o colaborador de la red de Hola para su suscripción. vea toolearn más información acerca de la asignación de roles tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *máquinas virtuales*. Cuando **máquinas virtuales** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **máquinas virtuales** hoja que aparece, haga clic en nombre de Hola de hello VM desea tooremove una interfaz de red para.
4. Hola **configuración** sección de hoja de máquina virtual de Hola que aparece para hello VM que ha seleccionado, haga clic en **interfaces de red**. toolearn acerca de la configuración de la interfaz de red y cómo toochange usarlas, lea la sección hello [administrar interfaces de red](virtual-network-network-interface.md) artículo. toolearn acerca de cómo agregar, cambiar o quitar direcciones IP asignadas tooa interfaz de red, consulte [direcciones IP administrar](virtual-network-network-interface-addresses.md).
5. En hello hoja de interfaces de red que aparece, haga clic en hello **...**  toohello derecha de la interfaz de red de Hola que desea toodetach.
6. Haga clic en **Desasociar**. Si no hay sólo una red interfaz conectada toohello máquina virtual, Hola **separar** opción no está disponible. Haga clic en **Sí** en el cuadro de confirmación de Hola que aparece.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (referencia) o [pasos detallados](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (referencia) o [pasos detallados](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Pasos siguientes
toocreate una máquina virtual con varias interfaces de red o direcciones IP, leer Hola siguientes artículos:

**Comandos**

|Tarea|Herramienta|
|---|---|
|Creación de una máquina virtual con varias NIC|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creación de una máquina virtual con una sola interfaz de red y varias direcciones IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creación de una máquina virtual con una sola interfaz de red y una dirección IPv6 privada (detrás de Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Plantilla de Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
