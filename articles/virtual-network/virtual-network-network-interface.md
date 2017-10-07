---
title: aaaCreate, cambiar o eliminar una interfaz de red de Azure | Documentos de Microsoft
description: "Obtenga información sobre qué es una interfaz de red y cómo cambiar la configuración de toocreate y elimine uno."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Creación, cambio o eliminación de una interfaz de red

Obtenga información acerca de cómo cambiar la configuración de toocreate y eliminar una interfaz de red. Una interfaz de red permite un toocommunicate de máquina Virtual de Azure con Internet, Azure y recursos locales. Al crear una máquina virtual mediante el portal de Azure hello, portal de hello crea una interfaz de red con la configuración predeterminada para usted. En su lugar, puede elegir toocreate interfaces de red con una configuración personalizada y agregar uno o más red interfaces tooa máquina virtual al crearlo. También puede ser conveniente configuración de interfaz de red toochange predeterminada para una interfaz de red existente. Este artículo explica cómo toocreate una interfaz de red con una configuración personalizada, cambiar la configuración existente, como la asignación de red filtro (grupo de seguridad de red), asignación de subred, configuración del servidor DNS y el reenvío IP y eliminar una interfaz de red.

Si necesita tooadd, cambiar o quitar direcciones IP para una interfaz de red, lea hello [direcciones IP administrar](virtual-network-network-interface-addresses.md) artículo. Si necesita tooadd a interfaces de red, o quitar interfaces de red de máquinas virtuales, lea hello [interfaces de red de agregar o quitar](virtual-network-network-interface-vm.md) artículo.


## <a name="before-you-begin"></a>Antes de empezar

Hola completa después de tareas antes de completar cualquier pasos en cualquier sección de este artículo:

- Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn de artículo sobre los límites de interfaces de red.
- Inicie sesión en Azure toohello [portal](https://portal.azure.com), interfaz de línea de comandos (CLI) de Azure o Azure PowerShell con una cuenta de Azure. Si todavía no tiene una cuenta de Azure, regístrese para obtener una [cuenta de evaluación gratuita](https://azure.microsoft.com/free).
- Si el uso de PowerShell comandos toocomplete tareas en este artículo, [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene Hola versión más reciente de los cmdlets de PowerShell de Azure de hello instalados. Ayuda de tooget para los comandos de PowerShell, con ejemplos, escriba `get-help <command> -full`.
- Si utiliza la interfaz de línea de comandos (CLI) de Azure comandos toocomplete tareas en este artículo, [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello en la nube Shell **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Crear una interfaz de red

Al crear una máquina virtual mediante el portal de Azure hello, portal de hello crea una interfaz de red con la configuración predeterminada para usted. Si prefiere especificar toda la configuración de la interfaz de red, puede crear una interfaz de red con una configuración personalizada y adjuntar la máquina virtual de hello red interfaz tooa al crear la máquina virtual de hello (con PowerShell u Hola CLI de Azure). También puede crear una interfaz de red y agregar máquina virtual existente tooan (con PowerShell u Hola CLI de Azure). toolearn cómo toocreate una máquina virtual a otra red interfaz o tooadd a o quitar interfaces de red de máquinas virtuales existentes, leer hello [interfaces de red de agregar o quitar](virtual-network-network-interface-vm.md) artículo. Antes de crear una interfaz de red, debe tener una existente [red virtual](virtual-networks-create-vnet-arm-pportal.md) en Hola la misma ubicación y suscripción crear una interfaz de red en.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en **+ agregar**.
4. Hola **crear interfaz de red** hoja que aparece, escriba, o seleccionar los valores de hello después de la configuración, haga clic en **crear**:

    |Configuración|¿Necesario?|Detalles|
    |---|---|---|
    |Nombre|Sí|Hola nombre debe ser único en el grupo de recursos de Hola que seleccione. Con el tiempo, probablemente tendrá varias interfaces de red en la suscripción de Azure. Hola de lectura [convenciones de nomenclatura](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) artículo para sugerencias cuando se crea un toomake de convención de nomenclatura administrar varias interfaces sea más fáciles de red. no se puede cambiar el nombre de Hello después de crea la interfaz de red de Hola.|
    |Red virtual|Sí|Seleccione Hola red virtual para la interfaz de red de Hola. Solo se puede asignar una red virtual de tooa de interfaz de red que existe en hello misma suscripción y la ubicación como interfaz de red de Hola. Una vez que se crea una interfaz de red, no se puede cambiar la red virtual de Hola se asigna a. Hello máquina virtual que agregue toomust de interfaz de red de hello también existe en hello misma ubicación y la suscripción como interfaz de red de Hola.|
    |Subred|Sí|Seleccione una subred dentro de la red virtual de Hola que seleccionó. Puede cambiar la subred de hello interfaz de red de Hola se asigna tooafter se crea.|
    |Asignación de la dirección IP privada|Sí| En esta configuración, elegir método de asignación de hello para hello dirección IPv4. Elegir entre los siguientes métodos de asignación de Hola: **dinámico:** al seleccionar esta opción, Azure asigna automáticamente una dirección disponible del espacio de direcciones de Hola de subred de Hola que seleccionó. Azure puede asignar una interfaz de red de tooa de dirección diferente cuando se inicia la máquina virtual de Hola en que se encuentra tras haber sido previamente Hola Detener estado (desasignada). Hola dirección permanece igual Hola si se reinicia la máquina virtual de hello sin haber sido previamente Hola había detenido estado (desasignada). **Estático:** al seleccionar esta opción, debe asignar manualmente una dirección IP disponible de hello espacio de direcciones de subred de Hola que seleccionó. Direcciones estáticas no cambia hasta que se cambien o se elimina la interfaz de red de Hola. Puede cambiar el método de asignación de hello después de crea la interfaz de red de Hola. servidor de DHCP de Azure de Hello asigna esta interfaz de red de dirección toohello en sistema de operativo Hola de máquina virtual de Hola.|
    |Grupo de seguridad de red|No| Déjelo establecido demasiado**ninguno**, seleccione una existente [grupo de seguridad de red](virtual-networks-nsg.md), o [crear un grupo de seguridad de red](virtual-networks-create-nsg-arm-pportal.md). Grupos de seguridad de red permiten el tráfico de red toofilter dentro y fuera de una interfaz de red. Puede aplicar una o ninguna seguridad grupo tooa red interfaz de red. Cero o un grupo de seguridad de red también puede aplicarse interfaz de red de toohello subred Hola se asigna a. Cuando un grupo de seguridad de red es tooa aplicado interfaz de red y la interfaz de red de Hola de subred de hello tiene asignado, se producen resultados inesperados en ocasiones. grupos de seguridad de red de tootroubleshoot interfaces toonetwork aplicados y subredes, leer hello [solucionar problemas de grupos de seguridad de red](virtual-network-nsg-troubleshoot-portal.md#nsg) artículo.|
    |La suscripción|Sí|Seleccione una de las [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) de Azure. máquina virtual de Hello adjuntar una red tooand Hola virtual red de la interfaz que lo conecte toomust existe en hello misma suscripción.|
    |Dirección IP privada (IPv6)|No| Si activa esta casilla, una dirección IPv6 es la interfaz de red de toohello asignado, además toohello dirección IPv4 asignada toohello interfaz de red. Vea hello [IPv6](#IPv6) sección de este artículo para obtener información importante sobre el uso de IPv6 con interfaces de red. No se puede seleccionar un método de asignación para hello dirección IPv6. Si elige tooassign una dirección IPv6, se asigna con el método dinámico Hola.
    |Nombre de IPv6 (solo aparece cuando hello **(IPv6) de la dirección IP privada** está activada la casilla de verificación) |Sí, si hello **(IPv6) de la dirección IP privada** casilla de verificación está activada.| Este nombre se asigna tooa de configuración de IP secundaria para la interfaz de red de Hola. Más información acerca de las configuraciones de IP en hello [ver configuración de la interfaz de red](#view-network-interface-settings) sección de este artículo.|
    |Grupos de recursos|Sí|Seleccione un [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) existente o cree uno. Una interfaz de red puede estar en hello igual u otro grupo de recursos, que se adjunta, las máquinas virtuales Hola o hello virtual de red se conecta.|
    |Ubicación|Sí|máquina virtual de Hello adjuntar una red tooand Hola virtual red de la interfaz que lo conecte toomust existe en hello mismo [ubicación](https://azure.microsoft.com/regions), también denominado tooas una región.|

portal de Hello no proporciona Hola opción tooassign una interfaz de red de toohello de dirección IP pública al crearlo, aunque portal hello cree una dirección IP pública y asígnela tooa interfaz de red cuando se crea una máquina virtual mediante el portal de Hola. toolearn cómo tooadd una red de toohello de dirección IP pública de la interfaz después de crear, leer hello [direcciones IP administrar](virtual-network-network-interface-addresses.md) artículo. Si desea toocreate una interfaz de red con una dirección IP pública, debe usar Hola CLI o PowerShell toocreate Hola interfaz de red.

>[!Note]
> Azure asigna una interfaz de red de MAC dirección toohello solo después de interfaz de red de hello esté adjunto tooa virtual machine y máquina virtual de hello es inicia Hola por primera vez. No se puede especificar la dirección MAC de Hola que Azure asigna toohello interfaz de red. Hola de interfaz de red de MAC dirección permanece asignada toohello hasta que se elimina la interfaz de red de Hola o se cambia la dirección IP privada Hola asignado toohello de configuración de IP principal de interfaz de red principal de Hola. más información acerca de las direcciones IP y las configuraciones de IP, leer hello toolearn [direcciones IP administrar](virtual-network-network-interface-addresses.md) artículo.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Visualización de la configuración de la interfaz de red

Puede ver y cambiar la mayoría de las opciones de una interfaz de red después de crearla.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desee tooview o cambiar la configuración de.
4. Hello siguientes opciones aparecen en hoja Hola que aparece para la interfaz de red de hello seleccionado:
    - **Información general:** proporciona información acerca de la interfaz de red de hello, como asignar las direcciones IP de hello tooit, interfaz de red de Hola Hola/subred de red virtual se asigna a e interfaz de red de Hola Hola máquina virtual está conectado demasiado (if se ha asociado tooone). Hello imagen siguiente muestra valores de información general de Hola para una interfaz de red denominado **mywebserver256**: ![información general de interfaz de red](./media/virtual-network-network-interface/nic-overview.png) puede mover un grupo de recursos distinto de tooa de interfaz de red o suscripción, haga clic en (**cambiar**) siguiente toohello **grupo de recursos** o **nombre de la suscripción**. Si mueve la interfaz de red de hello, debe mover toda la interfaz de red relacionados toohello recursos con él. Si la interfaz de red de hello es un equipo virtual tooa adjunto, por ejemplo, también debe mover máquina virtual de Hola y otros recursos relacionados con la máquina virtual. toomove una interfaz de red, lea hello [mover el tooa nuevo grupo de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) artículo. Hola artículo enumeran los requisitos previos y cómo recursos toomove usando Hola portal de Azure, PowerShell y Hola CLI de Azure.
    - **Las configuraciones de IP:** direcciones públicas y privadas de IPv4 e IPv6 tooIP configuraciones asignadas se enumeran aquí. Si una dirección IPv6 se asigna la configuración de IP tooan, no se muestra la dirección de Hola. Más información sobre las configuraciones de IP y cómo aborda tooadd y quitar direcciones IP en hello [direcciones IP configurar para una interfaz de red de Azure](virtual-network-network-interface-addresses.md) artículo. El reenvío de IP y la asignación de subred también se configuran en esta sección. más información acerca de estas opciones, lea hello toolearn [habilitar o deshabilitar el reenvío IP](#enable-or-disable-ip-forwarding) y [cambiar la asignación de subred](#change-subnet-assignment) secciones de este artículo.
    - **Servidores DNS:** puede especificar qué servidor DNS una interfaz de red asigna Hola servidores DHCP de Azure. Hello interfaz de red puede heredar configuración de Hola desde Hola se asigna a interfaz de red de red virtual hello, o tiene una configuración personalizada que reemplaza la configuración de Hola de red virtual de Hola se asigna a. toomodify lo que se muestra, Hola completa los pasos de hello [servidores DNS de cambio](#change-dns-servers) sección de este artículo.
    - **Grupo de seguridad de red (NSG):** muestra qué NSG está asociado toohello interfaz de red (si existe). Un NSG contiene reglas entrantes y salientes el tráfico de red de toofilter de interfaz de red de Hola. Si un NSG está asociado toohello interfaz de red, nombre Hola de hello que NSG asociado se muestra. toomodify lo que se muestra, Hola completa los pasos de hello [administrar asociaciones de grupos de seguridad de red](virtual-network-manage-nsg-arm-portal.md#manage-associations) artículo.
    - **Propiedades:** muestra la clave de configuración sobre la interfaz de red de hello, incluyendo su dirección MAC (en blanco si la interfaz de red de hello no está adjunto tooa virtual machine) y Hola suscripción se encuentra en.
    - **Las reglas de seguridad eficaz:** se enumeran las reglas de seguridad si interfaz de red de hello está adjunto tooa máquina virtual en ejecución y un NSG está asociado toohello interfaz de red, subred Hola se asigna a o ambos. toolearn más información acerca de lo que se muestra, leer hello [solucionar problemas de grupos de seguridad de red](virtual-network-nsg-troubleshoot-portal.md#nsg) artículo. más información acerca de los NSG, leer hello toolearn [grupos de seguridad de red](virtual-networks-nsg.md) artículo.
    - **Rutas efectivas:** rutas se muestran si la interfaz de red de hello es adjunto tooa máquina virtual en ejecución. rutas de Hello son una combinación de rutas de saludo predeterminado de Azure, las rutas definidas por el usuario (UDR) y las rutas BGP que puedan existir para la interfaz de red de Hola Hola subred se asigna a. toolearn más información acerca de lo que se muestra, leer hello [solucionar problemas de rutas](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) artículo. más información acerca de predeterminado de Azure y UDRs, leer hello toolearn [rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.
    - **Opciones de configuración comunes de Azure Resource Manager:** toolearn más información acerca de la configuración común de Azure Resource Manager, lea hello [registro de actividad](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [(de índices IAM) de control de acceso](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [etiquetas ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Bloquea](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), y [script de automatización](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) artículos.

**Comandos**

Si una dirección IPv6 se asigna la interfaz de red tooa, Hola salida PowerShell devuelve hechos de Hola que se asigna la dirección de hello, pero no devolver dirección Hola asignado. De forma similar, Hola CLI devuelve el hecho de Hola Hola dirección está asignada, pero devuelve *null* en su salida para la dirección de Hola.

|Herramienta|Comando|
|---|---|
|CLI|[lista de nic de red AZ](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview interfaces de red en la suscripción de hello; [show de nic de red az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview configuración para una interfaz de red|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview interfaces de red en la configuración de suscripción o una vista de Hola para una interfaz de red|

## <a name="change-dns-servers"></a>Cambio de los servidores DNS

interfaz de red de hello Azure DHCP server toohello en el sistema operativo de máquina virtual de Hola asigna el servidor DNS de Hola. servidor DNS de Hello asignado es la configuración del servidor DNS de hello es para una interfaz de red. toolearn más sobre la configuración de resolución de nombre de una interfaz de red, consulte [la resolución de nombres para las máquinas virtuales](virtual-networks-name-resolution-for-vms-and-role-instances.md). interfaz de red de Hello puede heredar la configuración de Hola de red virtual de Hola o usar su propia configuración única que invalidan la configuración de hello para la red virtual de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desee tooview o cambiar la configuración de.
4. En la hoja de hello para la interfaz de red de hello seleccionado, haga clic en **servidores DNS** en **configuración**.
5. Haga clic en:
    - **Heredar de red virtual (valor predeterminado)**: elija esta opción de servidor DNS de Hola para opción tooinherit definida para la interfaz de red de Hola Hola red virtual se asigna a. En el nivel de red virtual de hello, se define un servidor DNS personalizado o un servidor DNS que viene con Azure de Hola. Hello viene con Azure servidor DNS puede resolver nombres de host de recursos asignados toohello misma red virtual. FQDN debe ser tooresolve usado para los recursos asignados toodifferent las redes virtuales.
    - **Personalizado**: puede configurar sus propios nombres de tooresolve de servidor DNS a través de varias redes virtuales. Escriba la dirección IP de Hola de servidor hello desea toouse como un servidor DNS. Especifica la dirección del servidor DNS de Hola se asigna sólo interfaz de red de toothis e invalida a que cualquier configuración de DNS de la interfaz de red de Hola Hola red virtual se asigna.
6. Haga clic en **Guardar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Habilitación o deshabilitación del reenvío IP

El reenvío IP permite que máquina virtual de hello a que una interfaz de red está conectada:
- Recibir tráfico de red no destinado a uno de direcciones IP de hello asignadas tooany Hola de configuraciones de IP asignada toohello interfaz de red.
- Enviar tráfico de red con una dirección IP de origen diferente que tooone asignado uno de Hola de configuraciones de IP de la interfaz de red.

opción de Hello debe estar habilitada para cada interfaz de red que es un equipo virtual toohello adjunto que recibe el tráfico que Hola tooforward de necesidades de máquina virtual. Una máquina virtual puede reenviar el tráfico tanto si tiene varias interfaces de red o un tooit de red única interfaz conectada. Mientras el reenvío IP es una configuración de Azure, máquina virtual de hello también debe ejecutar un aplicación tooforward capaz de hello el tráfico, como firewall y optimización de la WAN, las aplicaciones de equilibrio de carga. Cuando una máquina virtual se ejecutan aplicaciones de red, máquina virtual de hello suele ser tooas que se hace referencia un dispositivo virtual de la red. Puede ver una lista de dispositivos virtuales de red toodeploy listo en hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). El reenvío IP normalmente se usa con rutas definidas por el usuario. más información acerca de las rutas definidas por el usuario, leer hello toolearn [rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desee tooenable o deshabilitar el reenvío de IP.
4. En la hoja de hello para la interfaz de red de hello seleccionado, haga clic en **configuraciones IP** en hello **configuración** sección.
5. Haga clic en **habilitado** o **deshabilitado** configuración de hello toochange (valor predeterminado).
6. Haga clic en **Guardar**.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Cambio de la asignación de subred

Puede cambiar la subred de hello, pero no Hola red virtual, que se asigna una interfaz de red a.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **interfaces de red** hoja que aparece, haga clic en la interfaz de red de hello desee tooview o cambiar la configuración de.
4. Haga clic en **configuraciones IP** en **configuración** en hoja Hola de interfaz de red de Hola que seleccionó. Si la lista de todas las direcciones IP privadas de las configuraciones IP tenga **(estático)** toothem siguiente, debe cambiar toodynamic de método de asignación de hello IP dirección siguiendo los pasos de Hola que siguen. Todas las direcciones IP privadas deben asignarse con asignación de subred de hello toochange método de asignación dinámica Hola de interfaz de red de Hola. Si se asignan direcciones de hello con el método dinámico de hello, continuar toostep cinco. Si se asignan las direcciones IPv4 con el método de asignación estática hello, complete Hola siguiendo los pasos toochange Hola asignación método toodynamic:
    - Haga clic en configuración de IP de Hola que desee hello toochange método de asignación de direcciones IPv4 para de lista de Hola de configuraciones de IP.
    - En la hoja de Hola que aparece para la configuración de IP de hello, haga clic en **dinámica** para hello **asignación** método. No se puede asignar una dirección IPv6 con el método de asignación estática hello.
    - Haga clic en **Guardar**.
5. Seleccione subred Hola desea tooconnect Hola Hola de toofrom de interfaz de red **subred** lista desplegable.
6. Haga clic en **Guardar**. Asigna las direcciones dinámicas nueva Hola dirección intervalo de subred para la subred nueva Hola. Después de asignar Hola interfaz tooa nueva subred, puede asignar una dirección IPv4 estática del nuevo intervalo de direcciones de subred Hola si elige. más información acerca de agregar, cambiar y quitar direcciones IP para una interfaz de red, lea hello toolearn [direcciones IP administrar](virtual-network-network-interface-addresses.md) artículo.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Eliminar una interfaz de red

Puede eliminar una interfaz de red siempre y cuando no sea máquina virtual de tooa adjunto. Si no adjunta tooa virtual machine, primero debe primer estado de la máquina virtual en hello detenido (desasignado) de Hola lugar, desasociar, a continuación, la interfaz de red de saludo de la máquina virtual de hello, antes de poder eliminar la interfaz de red de Hola. toodetach una interfaz de red de una máquina virtual, Hola completa los pasos de hello [desasociar una interfaz de red de una máquina virtual](virtual-network-network-interface-vm.md#vm-remove-nic) sección de hello [interfaces de red de agregar o quitar](virtual-network-network-interface-vm.md) artículo. Al eliminar una máquina virtual desasocia todos los tooit adjunta interfaces de red, pero no elimina las interfaces de red de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *interfaces de red*. Cuando **interfaces de red** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Menú contextual de la interfaz de red de Hola que desee toodelete y haga clic en **eliminar**.
4. Haga clic en **Sí** tooconfirm eliminación de interfaz de red de Hola.

Cuando se elimina una interfaz de red, cualquier MAC o direcciones IP asignadas tooit se liberan.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Pasos siguientes
direcciones de una máquina virtual con varias interfaces de red o una dirección IP de toocreate, lea Hola siguientes artículos:

**Comandos**

|Tarea|Herramienta|
|---|---|
|Creación de una máquina virtual con varias NIC|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creación de una máquina virtual con una sola interfaz de red y varias direcciones IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creación de una máquina virtual con una sola interfaz de red y una dirección IPv6 privada (detrás de Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Plantilla de Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
