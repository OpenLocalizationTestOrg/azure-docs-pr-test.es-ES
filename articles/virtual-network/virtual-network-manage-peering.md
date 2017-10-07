---
title: aaaCreate, cambiar o eliminar el emparejamiento de una red virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate, cambiar o eliminar el emparejamiento de una red virtual."
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Crear, cambiar o eliminar un emparejamiento de red virtual

Obtenga información acerca de cómo toocreate, cambiar o eliminar el emparejamiento de una red virtual. Intercambio de tráfico de red virtual permite tooconnect dos redes virtuales en Hola misma ubicación de Azure a través de Hola red troncal de Azure. Una vez emparejar, se siguen administrando a las dos redes virtuales de hello como recursos separados. Recursos de cualquier red virtual comunican con hello mismo ancho de banda y latencia como si estuvieran recursos hello en Hola misma red virtual. Si no está familiarizado con el intercambio de tráfico de red virtual, le recomendamos que lea hello [introducción de intercambio de tráfico de red Virtual](virtual-network-peering-overview.md) y completar hello [crear un tutorial de intercambio de tráfico de red virtual](virtual-network-create-peering.md), antes de finalizar tareas de Hello en este artículo.

## <a name="before-you-begin"></a>Antes de empezar

Hola completa después de tareas antes de completar los pasos en cualquier sección de este artículo:

- Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn de artículo sobre los límites de emparejamiento.
- Inicie sesión en toohello portal de Azure, interfaz de línea de comandos (CLI) de Azure o Azure PowerShell con una cuenta de Azure. Si todavía no tiene una cuenta de Azure, regístrese para obtener una [cuenta de evaluación gratuita](https://azure.microsoft.com/free).
- Si el uso de PowerShell comandos toocomplete tareas en este artículo, [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Compruebe que tiene versión más reciente de Hola de cmdlets de PowerShell de Azure Hola instalados. Ayuda de tooget para los comandos de PowerShell, con ejemplos, escriba `get-help <command> -full`.
- Si utiliza la interfaz de línea de comandos (CLI) de Azure comandos toocomplete tareas en este artículo, [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Hola Shell en la nube tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello en la nube Shell **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Creación de un emparejamiento

>[!NOTE]
>Hay varios requisitos, las restricciones, y consideraciones toosuccessfully crear un intercambio de tráfico de red virtual. Antes de crear un emparejamiento, asegúrese de que se haya familiarizado con hello [requisitos y restricciones](#requirements-and-constraints) y [los permisos necesarios](#permissions).
>

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se asigna es necesario hello [roles o permisos](#permissions).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *redes virtuales*. Cuando **redes virtuales** aparece en los resultados de búsqueda de hello, haga clic en él. No seleccione **redes virtuales (clásicas)** si aparece en la lista de hello, tal y como no se puede crear un emparejamiento de una red virtual que se implementan a través del modelo de implementación clásica de Hola.
3. Hola **redes virtuales** hoja que aparece, haga clic en la red virtual de hello desea toocreate un emparejamiento para.
4. En el panel de Hola que aparece para la red virtual de hello seleccionado, haga clic en **emparejamientos** en hello **configuración** sección.
5. Haga clic en **+ Agregar**. 
6. <a name="add-peering"></a>Hola **agregar emparejamiento** hoja, escriba o seleccione valores de hello después de configuración:
    - **Nombre:** nombre hello para el emparejamiento de hello debe ser único dentro de la red virtual de Hola.
    - **Modelo de implementación de red virtual:** Seleccione qué Hola de modelo de implementación virtual de red desea toopeer con se implementa a través de.
    - **Sé mi Id. de recurso:** si tiene acceso de lectura toohello red virtual que desee toopeer con, deje desactivada esta casilla de verificación. Si no tiene acceso de lectura toohello una red virtual o la suscripción que desea toopeer con, Active esta casilla. Escriba el Id. de recurso completo de Hola de red virtual de Hola que desea toopeer con Hola **Id. de recurso** cuadro que aparece cuando se activa la casilla de Hola. recursos de Hello ID que especifique debe ser para una red virtual que existe en hello Azure mismo [ubicación](https://azure.microsoft.com/regions) como esta red virtual. Id. de recurso completo de Hello parece similardemasiado/suscripciones/<Id>/providers/Microsoft.Network/virtualNetworks//ResourceGroups / < nombre de grupo de recursos > <--nombre de red virtual >. Puede obtener Id. de recurso de Hola para una red virtual viendo las propiedades de Hola para una red virtual. toolearn propiedades de hello tooview para una red virtual, vea [administrar redes virtuales](virtual-network-manage-network.md#view-vnet).
    - **Suscripción:** Hola seleccione [suscripción](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) de red virtual de hello desea toopeer con. Se muestran una o varias suscripciones, en función del número de suscripciones al que tenga acceso de lectura su cuenta. Si ha activado hello **Id. de recurso** casilla de verificación, esta opción no está disponible. Puede emparejar redes virtuales en suscripciones diferentes siempre y cuando ambas redes virtuales se hayan creado mediante el Administrador de recursos. Hola capacidad toopeer a través de las suscripciones creadas a través de diferentes modelos de implementación está en versión preliminar. Registrar para la vista previa de hello antes de crear un emparejamiento entre redes virtuales que se implementan a través de diferentes modelos de implementación que existan en distintas suscripciones. Más información acerca de cómo tooregister para la vista previa de Hola y [del mismo nivel redes virtuales creadas a través de diferentes modelos de implementación en distintas suscripciones](create-peering-different-deployment-models-subscriptions.md).
    - **Red virtual:** seleccione Hola red virtual que desea toopeer con. Puede seleccionar una red virtual creada a través de cualquier modelo de implementación de Azure, pero debe ser red virtual de Hola Hola misma ubicación que está iniciando de red virtual de Hola Hola emparejamiento de. Debe tener de lectura red virtual de toohello de acceso para él toobe visible en la lista de Hola. Si se muestra una red virtual, pero gris, puede deberse a que el espacio de direcciones de hello para la red virtual de Hola se superpone con el espacio de direcciones de Hola para esta red virtual. Si los espacios de direcciones de las redes virtuales se superponen, no se pueden emparejar. Si ha activado hello **Id. de recurso** casilla de verificación, esta opción no está disponible.
    - **Permitir el acceso de red virtual:** seleccione **habilitado** (valor predeterminado) si desea que tooenable la comunicación entre redes virtuales Hola dos. Cómo habilitar la comunicación entre redes virtuales permite recursos conectado tooeither toocommunicate de red virtual entre sí con Hola mismo ancho de banda y latencia como si estuvieran conectado toohello misma red virtual. Todas las comunicaciones entre los recursos en las dos redes virtuales de hello es sobre hello Azure red privada. Hola **VirtualNetwork** abarca la etiqueta predeterminada para los grupos de seguridad de red red virtual de Hola y emparejar la red virtual. toolearn Obtenga más información sobre la red etiquetas de predeterminado del grupo de seguridad, leer hello [información general de grupos de seguridad de red](virtual-networks-nsg.md#default-tags) artículo.  Seleccione **deshabilitado** si no desea que el tráfico tooflow toohello emparejar red virtual. Puede seleccionar **deshabilitado** si ha emparejar una red virtual con otra red virtual, pero en ocasiones desee toodisable el flujo de tráfico entre redes virtuales Hola dos. Le resultará más cómoda la opción de habilitar y deshabilitar que eliminar y volver a crear emparejamientos. Si esta opción está deshabilitada, el tráfico no fluya entre Hola emparejar las redes virtuales.
    - **Permitir el tráfico reenviado:** comprobar este toohello de tráfico reenviado tooallow cuadro emparejar red virtual (tráfico que no se originan en la red virtual de hello emparejar) red virtual de tooflow toothis. Reenvío del tráfico es habitual cuando se ha implementado un dispositivo virtual de red en la red virtual de Hola que está emparejamiento con y ha creado las rutas definidas por el usuario tooforward tráfico a través del dispositivo virtual de red de Hola. Si deja esta casilla no está activada (valor predeterminado), tráfico reenviado desde Hola emparejar la red virtual no puede fluir toothis de red virtual. Al habilitar esta capacidad permite el tráfico de hello reenviado a través de emparejamiento de hello, no crear ninguna ruta definida por el usuario o dispositivos virtuales de red. Las rutas definidas por el usuario y las aplicaciones virtuales de red se crean por separado. Obtenga información sobre las [rutas definidas por el usuario](virtual-networks-udr-overview.md).
    - **Permitir tránsito de puerta de enlace:** Active esta casilla si tiene una red virtual de red virtual puerta de enlace toothis conectados y desea tooallow tráfico de hello emparejar tooflow de red virtual a través de puerta de enlace de Hola. Por ejemplo, esta red virtual puede ser tooan adjunto de red de local a través de una puerta de enlace de red virtual. Comprobación de que este cuadro permite el tráfico desde Hola emparejar tooflow de red virtual a través de la red virtual de hello puerta de enlace toothis adjunto. Si activa esta casilla, red virtual de hello emparejar no puede tener configurada una puerta de enlace. red virtual de Hello emparejar debe tener hello **usar puerta de enlace remota** casilla de verificación activada al configurar Hola emparejamiento de Hola otra red virtual de toothis de red virtual. Si deja esta casilla no está activada (valor predeterminado), el tráfico de red virtual de hello emparejar todavía flujos de red virtual toothis, pero no puede fluir a través de una red virtual de red virtual puerta de enlace toothis adjunto. Obtenga más información sobre las [puertas de enlace de red virtual](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    No puede habilitar esta opción si está emparejando una red virtual (Administrador de recursos) con una red virtual (clásica). Aunque el tráfico Hola fluye entre las dos redes virtuales de hello, Hola virtual (clásica) el tráfico de red no puede fluir a través de una red virtual de red puerta de enlace toohello adjunto (Administrador de recursos).
    - **Usar puertas de enlace remotos:** comprobar este tráfico de tooallow cuadro desde este tooflow de red virtual a través de una red virtual puerta de enlace toohello adjunto red virtual está emparejamiento con. Por ejemplo, hello red virtual con que está emparejamiento no tiene una puerta de enlace VPN conectado que permite la comunicación de red de local de tooan.  Activar esta casilla permite el tráfico desde este tooflow de red virtual a través de hello red VPN de puerta de enlace toohello adjunto emparejar virtual. Si activa esta casilla, red virtual de hello emparejar debe tener un tooit de asociado de puerta de enlace de red virtual y debe tener hello **permiten el tránsito de puerta de enlace** casilla de verificación activada. Si deja esta casilla no está activada (valor predeterminado), el tráfico de red virtual de hello emparejar todavía puede fluir toothis virtual de red, pero no puede fluir a través de una red virtual de red virtual puerta de enlace toothis adjunto. 
    
    No puede habilitar esta opción si está emparejando una red virtual (Administrador de recursos) con una red virtual (clásica). Aunque el tráfico Hola fluye entre las dos redes virtuales de hello, tráfico de red virtual (Administrador de recursos) de hello no puede fluir a través de una red puerta de enlace toohello adjunto red virtual (clásica).
7. Haga clic en hello **Aceptar** botón tooadd Hola subred toohello red virtual que seleccionó.

### <a name="commands"></a>Comandos:

|Herramienta|Comando|
|---|---|
|CLI|[az network vnet peering create](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Escenarios

Un intercambio de tráfico de red virtual se crea entre redes virtuales creadas a través de hello mismo o diferentes modelos de implementación que existen en Hola suscripciones iguales o distintas. Completar un tutorial paso a paso para uno de hello los escenarios siguientes:
 
|Modelo de implementación de Azure  | La suscripción  |
|---------|---------|
|Ambas mediante Resource Manager |[La misma](virtual-network-create-peering.md)|
| |[Diferente](create-peering-different-subscriptions.md)|
|Una mediante Resource Manager y la otra clásica     |[La misma](create-peering-different-deployment-models.md)|
| |[Diferente](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Visualización o cambio de la configuración de emparejamiento

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se asigna es necesario hello [roles o permisos](#permissions).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *redes virtuales*. Cuando **redes virtuales** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **redes virtuales** hoja que aparece, haga clic en la red virtual de hello desea toocreate un emparejamiento para.
4. En el panel de Hola que aparece para la red virtual de hello seleccionado, haga clic en **emparejamientos** en hello **configuración** sección.
5. Haga clic en hello emparejamiento desee tooview o cambiar la configuración de.
6. Cambiar la configuración adecuada del saludo. Leer acerca de las opciones de Hola para cada valor de [paso 6](#add-peering) de hello, cree una sección de emparejamiento de este artículo. 

    >[!NOTE]
    >Hay varios requisitos, las restricciones, y consideraciones toosuccessfully crear un intercambio de tráfico de red virtual. Antes de crear un emparejamiento, asegúrese de que se haya familiarizado con hello [requisitos y restricciones](#requirements-and-constraints) y [los permisos necesarios](#permissions).
    >

7. Haga clic en **Guardar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[lista de intercambio de tráfico de red virtual de red AZ](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist emparejamientos de una red virtual, [az mostrar intercambio de tráfico de red virtual de red](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow configuración para un emparejamiento específico, y [az actualización de intercambio de tráfico de red virtual de red](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) configuración de emparejamiento de toochange.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve ver configuración de emparejamiento y [AzureRmVirtualNetworkPeering conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange configuración.|

## <a name="delete-a-peering"></a>Eliminación de un emparejamiento
Cuando se elimina un emparejamiento, el tráfico de una red virtual ya no fluye emparejar toohello de red virtual. Cuando se implementa a través del Administrador de recursos de redes virtuales estén al mismo nivel, cada red virtual tiene un emparejamiento toohello otra red virtual. Aunque eliminar Hola emparejamiento desde una red virtual deshabilitará la comunicación de hello entre redes virtuales hello, no elimina Hola emparejamiento de hello otra red virtual. Hola estado emparejamiento de hello emparejamiento que existe en hello es otra red virtual **Disconnected**. No se puede volver a crear Hola emparejamiento hasta que se vuelvan a crea emparejamiento hello en la primera red virtual de Hola y estado de emparejamiento de Hola para ambos virtual redes cambios demasiado*conectado*. 

Si desea que las redes virtuales toocommunicate a veces, pero no siempre, en lugar de eliminar un emparejamiento, puede establecer hello **permitir el acceso de red virtual** configuración demasiado**deshabilitado** en su lugar. toolearn cómo hacerlo, vea el paso 6 de hello [crear un emparejamiento](#create-peering) sección de este artículo. Probablemente le resulte más fácil deshabilitar y habilitar el acceso a la red que eliminar y volver a crear emparejamientos.

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se asigna es necesario hello [roles o permisos](#permissions).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *redes virtuales*. Cuando **redes virtuales** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **redes virtuales** hoja que aparece, haga clic en la red virtual de hello desea toodelete un emparejamiento de.
4. En la hoja de Hola que aparece para la red virtual de hello seleccionado, haga clic en **emparejamientos** en **configuración**.
5. En la lista Hola de emparejamientos que aparece en la hoja de emparejamientos de hello, Hola contextual emparejamiento desee toodelete, haga clic en **eliminar**, a continuación, **Sí** hello toodelete emparejamiento desde la primera red virtual de Hola.
6. Hola completa anterior pasos toodelete Hola emparejamiento de Hola otra red virtual en el emparejamiento de Hola de.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network vnet peering delete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Requisitos y restricciones 

- redes virtuales Hello que del mismo nivel deben tener espacios de direcciones IP no se superponen.
- Una vez que una red virtual se ha emparejado con otra red virtual, no se pueden agregar espacios de direcciones a una red virtual ni eliminarse de esta. espacios de direcciones tooadd o remove, Hola delete emparejamiento, agregarán o quitar espacios de direcciones de Hola y luego volver a crear el emparejamiento de Hola. espacios de direcciones tooadd o quitar espacios de direcciones de redes virtuales, lea hello [crear, cambiar o eliminar las redes virtuales](virtual-network-manage-network.md#add-address-spaces) artículo. 
- Puede del mismo nivel dos redes virtuales que se implementan a través del Administrador de recursos o una red virtual que se implementa a través del Administrador de recursos con una red virtual que se implementan a través del modelo de implementación clásica de Hola. No se puede del mismo nivel dos redes virtuales creadas a través del modelo de implementación clásica de Hola. Si no está familiarizado con los modelos de implementación de Azure, lea hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo. Puede usar un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dos redes virtuales creadas a través del modelo de implementación clásica de Hola.
- Cuando emparejamiento dos redes virtuales creadas mediante el Administrador de recursos, debe configurarse un emparejamiento para cada red virtual en el emparejamiento de Hola de. Cuando creas Hola emparejamiento toohello segunda red virtual de la primera red virtual de hello, estado de emparejamiento de hello es *inició*.  Cuando creas Hola Intercambio de tráfico de red virtual de la primera de toohello Hola red virtual en segundo lugar, su estado de intercambio de tráfico es *conectado*. Si ver estado de emparejamiento de hello para la primera red virtual de hello, verá que su estado cambia de *inició* demasiado*conectado*. Hola emparejamiento no está correctamente establecida hasta que el estado de emparejamiento de Hola para ambos emparejamientos de red virtual es *conectado*. 
- Cuando emparejamiento una red virtual creada mediante el Administrador de recursos con una red virtual que se creó mediante el modelo de implementación clásica de hello, solo se configura un emparejamiento para la red virtual de hello implementado a través del Administrador de recursos. No se puede configurar el emparejamiento de una red virtual (clásica), o entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola. Cuando se crea Hola Intercambio de tráfico de red virtual de red virtual (Administrador de recursos) toohello de hello (clásico), estado de emparejamiento de hello es *actualizar*, en breve demasiado cambia*conectado*.   
- El emparejamiento se establece entre dos redes virtuales. Los emparejamientos no son transitivos. Si crea emparejamientos entre:
    - VirtualNetwork1 y VirtualNetwork2
    - VirtualNetwork2 y VirtualNetwork3

  No hay ningún emparejamiento entre VirtualNetwork1 y VirtualNetwork3 a través de VirtualNetwork2. Si desea toocreate una emparejamiento entre VirtualNetwork1 y VirtualNetwork3 de red virtual, deberá toocreate un emparejamiento entre VirtualNetwork1 y VirtualNetwork3.
- No se pueden resolver nombres en redes virtuales emparejadas mediante la resolución de nombres predeterminada de Azure. nombres de tooresolve en otras redes virtuales, debe usar un servidor DNS personalizado. toolearn cómo leer tooset su propio servidor DNS, hello [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artículo.
- Recursos en ambas redes virtuales en el emparejamiento de Hola de que puedan comunicarse entre sí con hello mismo ancho de banda y latencia como si estuvieran en Hola misma red virtual. A pesar de ello, el tamaño de cada máquina virtual tiene su propio ancho de banda de red máximo. más información acerca de ancho de banda de red máximo para tamaños de máquina virtual diferente, leer hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual.
- Puede explorar redes virtuales implementadas a través del Administrador de recursos que están en Hola iguales, o distintas suscripciones.
- Puede explorar redes virtuales que se implementan a través de diferentes modelos de implementación que están en Hola iguales, o diferentes suscripciones (versión preliminar). 
- Hello las suscripciones que ambas redes virtuales están en deben estar asociado toohello mismo inquilino de Azure Active Directory. Si todavía no tiene un inquilino de AD, puede [crear uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rápidamente. Puede usar un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dos redes virtuales que existan en distintas suscripciones asociadas toodifferent inquilinos de Active Directory.
- Una red virtual puede ser emparejar tooanother red virtual y también ser tooanother conectada ninguna red virtual con una puerta de enlace de red virtual de Azure. Cuando las redes virtuales están conectadas a través de emparejamiento y una puerta de enlace, el tráfico entre redes virtuales Hola fluye a través de la configuración de emparejamiento de hello, en lugar de puerta de enlace de Hola.
- Hay un cargo nominal para el tráfico de entrada y salida que utiliza un emparejamiento de red virtual. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Permisos

cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos. Por ejemplo, si se emparejamiento dos redes virtuales denominadas myVnetA y myVnetB, su cuenta se debe asignar Hola después de función mínima o los permisos para cada red virtual:
    
|Red virtual|Modelo de implementación|Rol|Permisos|
|---|---|---|---|
|myVnetA|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Resource Manager|[Colaborador de la red](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clásico|[Colaborador de la red clásica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toocreate un [topología de red de concentrador y radio](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
