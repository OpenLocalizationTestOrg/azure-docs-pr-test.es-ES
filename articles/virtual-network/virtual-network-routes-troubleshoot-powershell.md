---
title: rutas de aaaTroubleshoot - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot enruta en modelo de implementación de Azure Resource Manager Hola con Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Solución de problemas de rutas mediante Azure PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

Si se producen tooor de problemas de conectividad de red de la máquina Virtual (VM) de Azure, las rutas que pueden influir en los flujos de tráfico de máquina virtual. Este artículo proporciona información general sobre las capacidades de diagnóstico para rutas toohelp seguir solucionando el problema.

Las tablas de rutas están asociadas con subredes y son eficaces en todas las interfaces de red (NIC) en cada subred específica. Hola siguientes tipos de rutas puede ser aplicados tooeach interfaz de red:

* **Rutas del sistema:** de forma predeterminada, cada subred creada en Azure Virtual Network (VNet) tiene tablas de rutas del sistema que permiten el tráfico de red virtual local, el tráfico local a través de las puertas de enlace VPN y el tráfico de Internet. Las rutas del sistema existen también para las redes virtuales emparejadas.
* **Las rutas BGP:** propaga toonetwork interfaces a través de ExpressRoute o las conexiones VPN de sitio a sitio. Obtener más información sobre el enrutamiento de BGP leyendo hello [BGP con puertas de enlace VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) y [ExpressRoute Introducción](../expressroute/expressroute-introduction.md) artículos.
* **Rutas definidas por el usuario (UDR):** si se utilizan los dispositivos de red virtual o se fuerza el túnel tráfico tooan de red local a través de una VPN de sitio a sitio, puede tener rutas definidas por el usuario (UDRs) asociadas a la tabla de rutas de subred. Si no está familiarizado con UDRs, leer hello [rutas definidas por el usuario](virtual-networks-udr-overview.md#user-defined-routes) artículo.

Con hello varias rutas que pueden ser aplicados tooa interfaz de red, puede ser difícil toodetermine rutas que agregado entrarán en vigor. toohelp solucionar problemas de conectividad de red de máquina virtual, puede ver todas las rutas efectivas de Hola para una interfaz de red en el modelo de implementación de hello Azure Resource Manager.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Uso de flujo de tráfico VM de rutas efectivas tootroubleshoot
Este artículo usa Hola siguiendo el escenario como un tooillustrate de ejemplo cómo enruta tootroubleshoot Hola efectivo para una interfaz de red:

Una máquina virtual (*VM1*) conectado toohello red virtual (*VNet1*, prefijo: 10.9.0.0/16) se produce un error tooconnect tooa VM(VM3) en una red virtual recién peered (*VNet3*, prefijo 10.10.0.0/16). No hay ningún UDRs o BGP enruta aplicada tooVM1-NIC1 red interfaz conectada toohello VM, se aplican sólo las rutas del sistema.

Este artículo explica cómo toodetermine Hola causa de errores de conexión de hello, con capacidad de rutas efectivas en el modelo de implementación de administración de recursos de Azure.
Aunque ejemplo de Hola utiliza sólo las rutas del sistema, Hola mismos pasos puede ser usado toodetermine errores de conexión entrantes y salientes a través de cualquier tipo de ruta.

> [!NOTE]
> Si la máquina virtual tiene más de una NIC conectada, compruebe rutas efectivas para cada uno de hello tooand problemas conectividad de red de toodiagnose de NIC de una máquina virtual.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>Visualización de las rutas eficaces para una máquina virtual
toosee Hola agregado rutas que se aplica tooa VM, Hola completa siguiendo los pasos:

### <a name="view-effective-routes-for-a-network-interface"></a>Visualización de las rutas eficaces para una interfaz de red
toosee Hola agregado rutas de interfaz de red tooa aplicado, Hola completa pasos:

1. Inicie un tooAzure de sesión y de inicio de sesión de PowerShell de Azure. Si no está familiarizado con PowerShell de Azure, lea hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. Hello siguiente comando devuelve toda la interfaz de red de tooa rutas aplicadas denominado *VM1 NIC1* en grupo de recursos de hello *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Si no conoce el nombre de Hola de una interfaz de red, escriba Hola siguiendo los nombres de comando tooretrieve Hola de todas las interfaces de red en un group.* de recursos
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Hello salida siguiente busca un resultado similar toohello cada Hola de subred de ruta aplicado toohello A que NIC está conectada:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Tenga en cuenta siguiente de hello en la salida de hello:
   
   * **Nombre**: nombre de ruta efectiva Hola puede estar vacío, a menos que especifique explícitamente para rutas definidas por el usuario. 
   * **Estado**: indica el estado de ruta efectiva Hola. Los valores posibles son "Activo" o "No válido"
   * **AddressPrefixes**: especifica el prefijo de dirección de Hola de ruta efectiva de hello en la notación CIDR. 
   * **nextHopType**: indica el próximo salto de Hola para hello dada la ruta. Los valores posibles son *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* o *Null*. Un valor de *Null* para **nextHopType** en un UDR puede indicar una ruta no válida. Por ejemplo, si **nextHopType** es *VirtualAppliance* y Hola network appliance virtual VM no está en un estado de aprovisionamiento/ejecución. Si **nextHopType** es *VPNGateway* y no hay ninguna puerta de enlace aprovisionado/ejecución Hola red virtual especificada, ruta de hello puede no ser válida.
   * **NextHopIpAddress**: especifica Hola dirección IP de próximo salto de Hola de ruta efectiva Hola.
   
   Hello siguiente comando devuelve las rutas de hello en una tabla tooview más fácil:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Hola salida siguiente es algunos de los resultados de hello recibidos de escenario de hello descrito anteriormente:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. No hay ninguna ruta aparece toohello *oesteee. UU.-VNet3* red virtual (prefijo 10.10.0.0/16)** de *VNet1 oesteee. UU.* (prefijo 10.9.0.0/16) en la salida de hello del paso anterior de Hola. Como se muestra en hello después de la imagen, Hola vínculo de intercambio de tráfico de red virtual con hello *oesteee. UU.-VNet3* red virtual está en hello *Disconnected* estado.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    vínculo de Hello bidireccional de emparejamiento de Hola se interrumpe, que explica por qué VM1 no se pudo conectar tooVM3 Hola *oesteee. UU.-VNet3* red virtual. Configure un vínculo de emparejamiento de red virtual bidireccional para las redes virtuales *WestUS-VNet1* y *WestUS-VNet3*. salida de Hello devuelto después de vínculo de intercambio de tráfico de red virtual de Hola se establece correctamente la siguiente:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Una vez que determine el problema de hello, puede agregar, quitar, o cambiar las rutas y tablas de rutas. Hola de tipo siguientes comando toosee una lista de comandos de hello usa toodo así:
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>Consideraciones
Unos tookeep cosas en cuenta al revisar la lista de Hola de rutas devuelve:

* El enrutamiento se basa en coincidencia de prefijo más larga (LPM) entre las rutas UDR, BGP y del sistema. Si hay más de una ruta con hello mismo LPM coinciden, entonces se seleccionará una ruta en función de su origen en hello siguiendo el orden:
  
  * Ruta definida por el usuario
  * Ruta BGP
  * Ruta del sistema (predeterminado)
    
    Con rutas efectivas, sólo puede ver las rutas efectivas que sean iguales LPM basado en todas las rutas de hello disponible. Mostrando cómo rutas Hola se evalúan realmente de una NIC determinada, resulta mucho más fácil tootroubleshoot específico las rutas que pueden afectar a la conectividad de la máquina virtual.
* Si tiene UDRs y envían tráfico tooa virtual otros dispositivos de red (NVA), con *VirtualAppliance* como **nextHopType**, compruebe que el reenvío IP está habilitado en el tráfico de hello NVA receptora Hola o se quitan los paquetes. 
* Si está habilitado el protocolo de túnel forzado, todo el tráfico saliente de Internet será local tooon enrutado. RDP/SSH de tooyour Internet que VM no funcionen con esta configuración, dependiendo de cómo Hola local controla este tráfico. 
  Puede habilitar la tunelización forzada:
  * Si utiliza VPN de sitio a sitio, estableciendo una ruta definida por el usuario (UDR) con nextHopType como VPN Gateway
  * Si se anuncia una ruta predeterminada a través de BGP
* Para la red virtual emparejamiento tráfico toowork correctamente, una ruta de sistema con **nextHopType** *VNetPeering* debe existir para hello emparejar el intervalo de prefijo de la red virtual. Si una ruta de este tipo no existe y Hola de intercambio de tráfico de red virtual vínculo parece correcta:
  * Espere unos segundos y vuelva a intentar si es un vínculo de emparejamiento recién establecido. En ocasiones, toma más rutas toopropagate tooall interfaces de red de hello en una subred.
  * Las reglas del grupo de seguridad de red (NSG) que pueden influir en los flujos de tráfico de Hola. Para obtener más información, vea hello [solucionar problemas de grupos de seguridad de red](virtual-network-nsg-troubleshoot-powershell.md) artículo.

