---
title: "aaaCreate, cambiar o eliminar una dirección IP pública Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate, cambiar o eliminar una dirección IP pública."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Creación, modificación o eliminación de una dirección IP pública

Obtenga información sobre una IP pública de direcciones y cómo toocreate, cambiar y eliminar uno. Una dirección IP pública es un recurso con sus propios valores de configuración. Permite asignar una tooother de dirección IP pública recursos de Azure:
- Entrada tooresources de conectividad de Internet, como máquinas virtuales (VM) de Azure, conjuntos de escalas de máquina Virtual de Azure, puerta de enlace de VPN de Azure, las puertas de enlace de la aplicación y equilibradores de carga de Azure con conexión a Internet. Recursos de Azure no pueden recibir comunicaciones entrantes de hello Internet sin una dirección IP pública asignada. Aunque algunos recursos de Azure son intrínsecamente accesibles a través de direcciones IP públicas, otros recursos deben tener direcciones IP públicas asignadas toothem toobe accesible desde Internet Hola.
- Conectividad saliente toohello Internet con una dirección IP predecible. Por ejemplo, una máquina virtual pueden comunicarse saliente toohello Internet sin un tooit dirección asignada de IP pública, pero su dirección es la dirección de red que se traducirá dirección pública de Azure tooan imprevisible. Asignar un recurso de tooa de dirección IP público permite tooknow dirección IP que se utiliza para la conexión saliente de Hola. Aunque predecible, puede cambiar dirección de hello, según el método de asignación de hello elegido. Para más información, consulte [Creación de una dirección IP pública](#create-a-public-ip-address). más información acerca de las conexiones salientes en recursos de Azure, lea hello toolearn [comprender las conexiones salientes](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.

## <a name="before-you-begin"></a>Antes de empezar

Hola completa después de tareas antes de completar cualquier pasos en cualquier sección de este artículo:

- Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn de artículo sobre los límites de las direcciones IP públicas.
- Inicie sesión en Azure toohello [portal](https://portal.azure.com), interfaz de línea de comandos (CLI) de Azure o Azure PowerShell con una cuenta de Azure. Si todavía no tiene una cuenta de Azure, regístrese para obtener una [cuenta de evaluación gratuita](https://azure.microsoft.com/free).
- Si el uso de PowerShell comandos toocomplete tareas en este artículo, [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene Hola versión más reciente de los cmdlets de PowerShell de Azure de hello instalados. Ayuda de tooget para los comandos de PowerShell, con ejemplos, escriba `get-help <command> -full`.
- Si utiliza la interfaz de línea de comandos (CLI) de Azure comandos toocomplete tareas en este artículo, [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello en la nube Shell **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com).

Las direcciones IP públicas tienen un precio simbólico. tooview Hola precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. 

## <a name="create-a-public-ip-address"></a>Crear una dirección IP pública

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *dirección ip pública*. Cuando **direcciones IP públicas** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Haga clic en **+ agregar** en hello **dirección IP pública** hoja que aparece.
4. Escriba o seleccione valores de hello después configuración Hola **Crear dirección IP pública** hoja que aparece, haga clic en **crear**:

    |Configuración|¿Necesario?|Detalles|
    |---|---|---|
    |Nombre|Sí|Hola nombre debe ser único en el grupo de recursos de Hola que seleccione.|
    |Versión de la dirección IP|Sí| Seleccione IPv4 o IPv6. Mientras IPv4 públicas las direcciones pueden estar asignados a tooseveral recursos de Azure, una dirección IP pública de IPv6 puede solo asignarse equilibrador de carga tooan orientado a Internet. equilibrador de carga de Hello puede cargar máquinas virtuales de saldo IPv6 tráfico tooAzure. Obtenga más información sobre [máquinas de toovirtual de tráfico de IPv6 de equilibrio de carga](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Asignación de dirección IP|Sí|**Dinámico:** asigna las direcciones dinámicas solo después de asociar la dirección IP pública de hello tooa NIC conectado tooa VM y hello máquina virtual se inicia para hello primera vez. Pueden cambiar las direcciones dinámicas si Hola Hola VM NIC es toois adjunto detenido (desasignado). Hola dirección permanece igual Hola si hello VM se reinicia o detenida (pero no cancela la asignación). **Estático:** direcciones estáticas se asignan cuando se crea la dirección IP pública Hola. Direcciones estáticas es no cambiar incluso que si hello máquina virtual se pone en hello detenido (desasignado) el estado. dirección de Hola sólo se lanza cuando se elimina Hola NIC. Puede cambiar el método de asignación de hello después de crea Hola NIC. Si selecciona IPv6 para hello **IP versión**, método de asignación solo está disponible de hello es **dinámica**.|
    |Tiempo de espera de inactividad (minutos)|No|¿Cuántos minutos tookeep una conexión TCP o HTTP abierta sin tener que depender de mensajes de mantenimiento de clientes toosend. Si selecciona IPv6 como la **versión de dirección IP**, no se puede cambiar este valor. |
    |Etiqueta de nombre DNS|No|Debe ser único dentro de hello ubicación de Azure para crear el nombre de hello en (a través de todas las suscripciones y todos los clientes). Hello Azure servicio DNS público registra automáticamente Hola nombre y dirección IP para que pueda conectarse tooa recursos con nombre de Hola. Anexa Azure *location.cloudapp.azure.com* (donde ubicación es la ubicación de Hola que seleccione) nombre toohello proporcionar toocreate Hola totalmente nombre DNS completo. Si elige toocreate ambas versiones de dirección, hello mismo nombre DNS se asigna tooboth Hola IPv4 y las direcciones IPv6. Hola servicio DNS de Azure contiene registros de nombre A IPv4 y IPv6 AAAA y responde con ambos registros al nombre DNS de Hola se busca. cliente de Hello elige qué toocommunicate de dirección (IPv4 o IPv6) con.|
    |Creación de una dirección IPv6 (o IPv4)|No| Se muestra IPv6 o IPv4, dependiendo de lo que selecciona en la **versión de dirección IP**. Por ejemplo, si selecciona **IPv4** en la **versión de dirección IP**, aquí se muestra **IPv6**.
    |Nombre (solo visible si ha activado hello **crear una dirección IPv6 (o IPv4)** casilla)|Sí, si selecciona hello **crear IPv6** (o IPv4) casilla de verificación.|Hello nombre debe ser distinto Hola nombre que escriba en primer lugar para hello **nombre** en esta lista. Si elige toocreate tanto IPv4 como una dirección IPv6, el portal de hello crea dos independiente públicos recursos de dirección IP, uno con cada versión de dirección IP asignada tooit.|
    |Asignación de direcciones IP (solo visible si ha activado hello **crear una dirección IPv6 (o IPv4)** casilla)|Sí, si selecciona hello **crear IPv6** (o IPv4) casilla de verificación.|Si dice Hola casilla **crear una dirección IPv4**, puede seleccionar un método de asignación. Si dice Hola casilla **crear una dirección IPv6**, no puede seleccionar un método de asignación, ya que debe ser **dinámica**.|
    |La suscripción|Sí|Debe existir en hello mismo [suscripción](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) como recurso de Hola desee tooassociate Hola pública dirección IP.|
    |Grupos de recursos|Sí|Pueden existir en hello iguales o distinto, [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) como recurso de Hola desee tooassociate Hola pública dirección IP.|
    |Ubicación|Sí|Debe existir en hello mismo [ubicación](https://azure.microsoft.com/regions), también denominada región tooas, recursos de Hola que desee tooassociate Hola pública dirección IP.|

**Comandos**

Aunque Hola portal le proporciona Hola opción toocreate dos públicos recursos de dirección IP (una IPv4 y uno IPv6), Hola siga los comandos CLI y PowerShell crea un recurso con una dirección para una versión IP o hello otras. Si desea que dos públicos recursos de dirección IP, uno para cada versión IP, debe ejecutar el comando de hello dos veces, especificar diferentes nombres y las versiones de recursos de dirección IP públicas de Hola. 

|Herramienta|Comando|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Visualización, cambio de la configuración o eliminación de una dirección IP pública

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que es permisos asignados (como mínimo) para el rol de colaborador de la red de Hola para su suscripción. Hola de lectura [funciones integradas para el control de acceso basado en roles de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn artículo más sobre la asignación de roles y permisos tooaccounts.
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *dirección ip pública*. Cuando **direcciones IP públicas** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **direcciones IP públicas** hoja que aparece, haga clic en nombre de Hola de hello dirección IP pública que desea tooview, cambia la configuración de o elimina.
4. En la hoja de Hola que aparece para la dirección IP pública hello, realice una de hello siguientes opciones dependiendo de si desea tooview, eliminar o cambiar la dirección IP pública Hola.
    - **Vista**: Hola **Introducción** sección de hoja de hello muestra valores de clave para la dirección IP pública hello, como la interfaz de red de hello tiene asociados demasiado (si dirección hello es la interfaz de red de tooa asociados). portal de Hello no muestre la versión de Hola de dirección de hello (IPv4 o IPv6). información de versión de hello tooview, Hola use PowerShell o CLI comando tooview Hola dirección IP pública. Si la versión de dirección IP de hello es IPv6, hello dirección asignada no se muestra de Hola portal, PowerShell o CLI Hola. 
    - **Eliminar**: dirección IP pública a toodelete hello, haga clic en **eliminar** en hello **Introducción** sección de hoja de Hola. Si dirección hello es la configuración de IP tooan asociados actualmente, no se puede eliminar. Si la dirección Hola está asociada actualmente a una configuración, haga clic en **desasócielo** toodissociate dirección de Hola de configuración de IP de Hola.
    - **Cambio**: haga clic en **Configuración**. Cambiar la configuración mediante la información de hello en el paso 4 de hello [crear una dirección IP pública](#create-a-public-ip-address) sección de este artículo. asignación de hello toochange para una dirección IPv4 de toodynamic estático, primero debe desasociar la dirección IPv4 pública de Hola desde la está asociado a la configuración de IP de Hola. A continuación, puede cambiar toodynamic de método de asignación de Hola y haga clic en **asociar** toohello de dirección IP de tooassociate Hola mismo IP configuración, una configuración diferente o puede dejar que se deben separar. una dirección IP pública, Hola toodissociate **Introducción** sección, haga clic en **desasócielo**.

>[!WARNING]
>Cuando se cambia el método de asignación de hello toodynamic estático, perderá dirección IP de Hola que se asignó la dirección IP pública de toohello. Aunque hello Azure servidores DNS públicos mantienen una asignación entre direcciones estáticas o dinámicas y cualquier etiqueta de nombre DNS (si se ha definido uno), una dirección IP dinámica puede cambiar cuando se inicia Hola VM después de hello detención estado (desasignada). dirección de hello tooprevent cambien, asigne una dirección IP estática.

**Comandos**

|Herramienta|Comando|
|---|---|
|CLI|[AZ red public-ip-list](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) las direcciones IP públicas toolist, [az red public-ip-mostrar](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow configuración; [actualizar la ip pública de red az](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [eliminar az red public-ip](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve una IP pública direccionar objeto y ver su configuración, [AzureRmPublicIpAddress conjunto](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate configuración; [Remove-AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Pasos siguientes
Asignar direcciones IP públicas al crear hello Azure recursos siguientes:

- Máquinas virtuales [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Load Balancer accesible desde Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Introducción a Puerta de enlace de aplicaciones](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Conexión de sitio a sitio con Azure VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Conjunto de escalado de máquinas virtuales de Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
