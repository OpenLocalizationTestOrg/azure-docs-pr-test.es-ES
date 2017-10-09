---
title: aaaAdd, cambiar o eliminar una subred de red virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd, cambiar o eliminar una subred de red virtual en Azure."
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
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Incorporación, cambio o eliminación de una subred de red virtual

Obtenga información acerca de cómo tooadd, cambiar o eliminar una subred de red virtual. 

Si no está familiarizado con las redes virtuales, antes de agregar una subred, cambiarla o eliminarla, es recomendable leer la [introducción a Azure Virtual Network](virtual-networks-overview.md) y [Crear, cambiar o eliminar una red virtual](virtual-network-manage-network.md). Todos los recursos de Azure implementados en una red virtual se implementan en una subred de esa red virtual. Normalmente, se crean varias subredes en una red virtual para:
- **Filtrar el tráfico entre subredes**. Puede aplicar red seguridad grupos toosubnets toofilter entrante y saliente tráfico de red para todos los recursos (por ejemplo, máquinas virtuales) que se encuentran en la red virtual de Hola. toolearn Obtenga más información sobre cómo toocreate un grupo de seguridad de red, consulte [crear grupos de seguridad de red](virtual-networks-create-nsg-arm-pportal.md).
- **Controlar el enrutamiento entre subredes**. Azure crea rutas predeterminadas para que el tráfico se enrute automáticamente entre subredes. Puede reemplazar las rutas predeterminadas de Azure creando rutas definidas por el usuario. toolearn más información acerca de las rutas definidas por el usuario, consulte [crear rutas definidas por el usuario](virtual-network-create-udr-arm-ps.md). 

Este artículo explica cómo tooadd, cambiar y eliminar una subred para redes virtuales que se crearon con el modelo de implementación de hello Azure Resource Manager.
 
## <a name="before"></a>Antes de empezar

Antes de comenzar las tareas de Hola que se describen en este artículo, completar Hola siguiendo los requisitos previos:

- Si le tooworking nueva con las redes virtuales, se recomienda que revise ejercicio hello en [crear la primera red virtual Azure](virtual-network-get-started-vnet-subnet.md). Este ejercicio puede ayudarle a familiarizarse más con las redes virtuales.
- toolearn sobre los límites de las redes virtuales, revisión [el límite de Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Inicie sesión en toohello portal de Azure, hello Azure de línea de comandos (CLI de Azure), PowerShell o la herramienta Azure utilizando su cuenta de Azure. Si no tiene una cuenta de Azure, regístrese para obtener una [cuenta de prueba gratuita](https://azure.microsoft.com/free).
- Si tiene previsto toouse comandos de PowerShell tareas de hello toocomplete descritas en este artículo, primero debe [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello cmdlets de PowerShell de Azure instalado. Ayuda de tooget para los comandos de PowerShell en los ejemplos de hello, escriba `get-help <command> -full`.
- Si tiene previsto toouse que tareas de hello toocomplete descritas en este artículo de comandos de CLI de Azure, debe:
    - [Instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de CLI de Azure instalado.
    - Usar hello Shell en la nube de Azure. En lugar de instalar Hola CLI y sus dependencias, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello Shell en la nube (**> _**) situado en parte superior de Hola de hello portal de Azure. 

  Ayuda de tooget con los comandos de CLI de Azure, escriba `az <command> --help`.

## <a name="create-subnet"></a>Agregar una subred

tooadd una subred:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, haga clic en **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en red virtual de hello desea tooadd una subred.
4. En la hoja de la red virtual de hello, haga clic en **subredes**.
5. Haga clic en **+Subred**.
6. En hello **Agregar subred** hoja, escriba los valores de hello parámetros siguientes:
    - **Nombre**: Hola nombre debe ser único dentro de la red virtual de Hola.
    - **Intervalo de direcciones**: Hola intervalo debe ser único dentro del espacio de direcciones de hello para la red virtual de Hola. intervalo de Hello no puede solaparse con otros intervalos de direcciones de subred dentro de la red virtual de Hola. espacio de direcciones de Hello debe especificarse mediante la notación de enrutamiento entre dominios sin clase (CIDR). Por ejemplo, en una red virtual con el espacio de direcciones 10.0.0.0/16, podría definir el espacio de direcciones de subred 10.0.0.0/24. intervalo más pequeño de Hello que puede especificar es / 29, lo que proporciona ocho direcciones IP de subred Hola. Recursos en reserva en Azure Hola primero y última de las direcciones de cada subred de conformidad con el protocolo. Otras tres direcciones están reservadas para el uso del servicio de Azure. Como resultado, definir una subred con/29 intervalo, se genera en tres direcciones IP utilizables en la subred de Hola de direcciones. Si tiene previsto tooconnect una puerta de enlace VPN de red virtual tooa, debe crear una subred de puerta de enlace. Más información sobre las [consideraciones específicas del intervalo de direcciones de las subredes de puerta de enlace](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Puede cambiar el intervalo de direcciones de hello después de agrega subred de hello, en condiciones específicas. toolearn toochange un intervalo de direcciones de subred, vea [cambiar la configuración de subred](#change-subnet) en este artículo.
    - **Grupo de seguridad de red**: si lo desea, puede asociar un grupo de seguridad de red existente Hola subred toocontrol filtrado para la subred de hello del tráfico de red entrantes y salientes. Hello grupo de seguridad de red debe existir en hello misma suscripción y ubicación de red virtual de Hola. También debe crearse mediante el modelo de implementación del Administrador de recursos de Hola. toolearn Obtenga más información sobre cómo toocreate un grupo de seguridad de red, consulte [grupos de seguridad de red](virtual-networks-create-nsg-arm-pportal.md).
    - **Tabla de rutas**: si lo desea, puede asociar una tabla de ruta existente con tráfico de red Hola subred toocontrol enrutamiento tooother redes. Hello tabla de ruta debe existir en hello misma suscripción y ubicación de red virtual de Hola. También debe crearse mediante el modelo de implementación del Administrador de recursos de Hola. toolearn Obtenga más información sobre cómo ver tablas de rutas de toocreate [rutas definidas por el usuario](virtual-network-create-udr-arm-ps.md).
    - **Los usuarios**: puede controlar acceso toohello subred mediante el uso de funciones integradas o sus propias funciones personalizadas. toolearn más información acerca de la asignación de subred de hello tooaccess roles y usuarios, consulte [usar rol asignación toomanage acceso tooyour Azure recursos](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd Hola subred toohello red virtual que ha seleccionado, haga clic en **Aceptar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Cambio de configuración de subred

Puede cambiar los grupos de seguridad de red, tablas de rutas y subred de tooa de acceso de usuario mediante la administración de recursos que están en una subred. toolearn acerca de estas opciones, en [agregar una subred](#create-subnet), vea el paso 6. Si desea que el espacio de direcciones de hello toochange de una subred, primero debe eliminar todos los recursos que se encuentran en la subred de Hola. pasos de Hola que seguir toodelete un recurso varían en función recursos Hola. toolearn cómo toodelete recursos que se encuentran en subredes, documentación de Hola de lectura para cada recurso de tipo, que desea toodelete. intervalo de direcciones de hello toochange para una subred:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, haga clic en **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en el que se desea toochange un intervalo de direcciones de subred de red virtual de Hola.
4. Haga clic en la subred de hello para el que desea intervalo de direcciones de toochange Hola.
5. En el módulo de subred hello, Hola **intervalo de direcciones** cuadro, escriba el nuevo intervalo de direcciones Hola. Hola intervalo debe ser único dentro del espacio de direcciones de hello para la red virtual de Hola. intervalo de Hello no puede solaparse con otros intervalos de direcciones de subred dentro de la red virtual de Hola. espacio de direcciones de Hello debe especificarse utilizando la notación CIDR. Por ejemplo, en una red virtual con el espacio de direcciones 10.0.0.0/16, podría definir el espacio de direcciones de subred 10.0.0.0/24. intervalo más pequeño de Hello que puede especificar es / 29, lo que proporciona ocho direcciones IP de subred Hola. Recursos en reserva en Azure Hola primero y última de las direcciones de cada subred de conformidad con el protocolo. Otras tres direcciones están reservadas para el uso del servicio de Azure. Como resultado, una subred con un intervalo de direcciones /29 tiene tres direcciones IP utilizables. Si tiene previsto tooconnect una puerta de enlace VPN de red virtual tooa, debe crear una subred de puerta de enlace. Más información sobre las [consideraciones específicas del intervalo de direcciones de las subredes de puerta de enlace](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Puede cambiar el intervalo de direcciones de hello después de que se crea la subred de hello, en condiciones específicas. toolearn toochange un intervalo de direcciones de subred, vea [cambiar la configuración de subred](#change-subnet) en este artículo.
6. Haga clic en **Guardar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Eliminación de una subred

Puede eliminar una subred sólo si no hay recursos en la subred de Hola. Si no hay recursos en la subred de hello, debe eliminar los recursos de Hola que se encuentran en la subred de hello antes de poder eliminar subred Hola. pasos de Hola que seguir toodelete un recurso varían en función recursos Hola. toolearn cómo toodelete recursos que se encuentran en subredes, documentación de Hola de lectura para cada recurso de tipo, que desea toodelete. toodelete una subred:

1. Inicie sesión en toohello [portal](https://portal.azure.com) con una cuenta que se le asignan permisos para el rol de colaborador de la red de hello (como mínimo) para su suscripción. vea toolearn más información acerca de la asignación de roles y permisos tooaccounts, [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. En el cuadro de búsqueda del portal de hello, escriba **redes virtuales**. En los resultados de la búsqueda de hello, haga clic en **redes virtuales**.
3. En hello **redes virtuales** hoja, haga clic en la red virtual de hello desea toodelete una subred de.
4. En hello virtual de red hoja, en **configuración**, haga clic en **subredes**.
5. Desea toodelete de lista de Hola de subredes que aparece en el módulo de subredes hello, subred Hola de menú contextual, haga clic en **eliminar**y, a continuación, haga clic en **Sí** subred de hello toodelete.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI de Azure|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Pasos siguientes

toocreate una máquina virtual en una subred, consulte [crear una red virtual e implementar máquinas virtuales en la subred de hello](virtual-network-get-started-vnet-subnet.md#create-vms).
