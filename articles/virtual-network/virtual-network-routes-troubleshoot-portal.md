---
title: rutas de aaaTroubleshoot - Portal | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot rutas en el modelo de implementación de Azure Resource Manager de hello utilizando Hola Portal de Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Solucionar problemas de rutas con hello Portal de Azure
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
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

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **más servicios**, a continuación, haga clic en **máquinas virtuales** en lista de Hola que aparece.
3. Seleccione una máquina virtual tootroubleshoot de lista de Hola que aparece y aparece una hoja de máquina virtual con opciones.
4. Haga clic en **Diagnosticar y solucionar problemas** y, a continuación, seleccione un problema común. En este ejemplo, **toomy VM de Windows no se puede conectar** está seleccionada.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Pasos aparecen bajo el problema de hello, como se muestra en hello después de imagen:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Haga clic en *rutas efectivas* en lista de Hola de pasos recomendados.
6. Hola **rutas efectivas** aparece hoja, como se muestra en hello después de imagen:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Si la máquina virtual tiene solo una NIC, está seleccionada de forma predeterminada. Si tiene más de una NIC, seleccione NIC hello para el que desea rutas efectivas de tooview Hola.

   > [!NOTE]
   > Si hello VM asociados hello NIC no está en un estado de ejecución, no se mostrarán las rutas efectivas. Solo hello 200 primeras rutas efectivas se muestran en el portal de Hola. En la lista completa de hello, haga clic en **descargar**. Puede filtrar aún más en los resultados de Hola de archivo .csv descargado de hello.
   >
   >

    Tenga en cuenta siguiente de hello en la salida de hello:

   * **Origen**: indica el tipo de saludo de la ruta. Las rutas del sistema se muestran como *Predeterminado*, los UDR se muestran como *Usuario* y las rutas de puerta de enlace (estáticas o BGP) se muestran como *VPNGateway*.
   * **Estado**: indica el estado de ruta efectiva Hola. Los valores posibles son *Activo* o *No válido*.
   * **AddressPrefixes**: especifica el prefijo de dirección de Hola de ruta efectiva de hello en la notación CIDR.
   * **nextHopType**: indica el próximo salto de Hola para hello dada la ruta. Los valores posibles son *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* o *Null*. Un valor de *Null* para **nextHopType** en un UDR puede indicar una ruta no válida. Por ejemplo, si **nextHopType** es *VirtualAppliance* y Hola network appliance virtual VM no está en un estado de aprovisionamiento/ejecución. Si **nextHopType** es *VPNGateway* y no hay ninguna puerta de enlace aprovisionado/ejecución Hola red virtual especificada, ruta de hello puede no ser válida.
7. No hay ningún toohello ruta aparece *oesteee. UU.-VNET3* (prefijo 10.10.0.0/16) de red virtual de hello *VNet1 oesteee. UU.* (prefijo 10.9.0.0/16) en la imagen de hello en el paso anterior de Hola. Hola después de la imagen, el vínculo emparejamiento hello es hello *Disconnected* estado:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    vínculo de Hello bidireccional de emparejamiento de Hola se interrumpe, que explica por qué VM1 no se pudo conectar tooVM3 Hola *oesteee. UU.-VNet3* red virtual.
8. Hello imagen siguiente muestran las rutas de hello después de establecer el vínculo de interconexión de hello bidireccional:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Para escenarios de solución de problemas más de tunelización forzada y ruta de la evaluación, leer hello [consideraciones](virtual-network-routes-troubleshoot-portal.md#considerations) sección de este artículo.

### <a name="view-effective-routes-for-a-network-interface"></a>Visualización de las rutas eficaces para una interfaz de red
Si el flujo de tráfico de red se ve afectado para una interfaz de red (NIC) determinada, puede ver una lista completa de rutas eficaces directamente en una NIC. toosee Hola agregado rutas que se aplica tooa NIC, Hola completa siguiendo los pasos:

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **Más servicios** y, a continuación, haga clic en **Interfaces de red**.
3. Buscar lista Hola nombre Hola de una NIC o selecciónelo en la lista de Hola que aparece. En este ejemplo está seleccionada **VM1 NIC1** .
4. Seleccione **rutas efectivas** en hello **interfaz de red** hoja, como se muestra en hello después de imagen:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Hola **ámbito** interfaz de red de toohello valores predeterminados seleccionado.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Visualización de las rutas eficaces para una tabla de rutas
Cuando se modifica rutas definidas por el usuario (UDRs) en una tabla de ruta, puede que desee impacto de hello tooreview de rutas de Hola que se agrega en una máquina virtual concreta. Una tabla de rutas se puede asociar con cualquier número de subredes. Ahora puede ver todas las rutas efectivas de Hola para todos Hola NIC que se aplica una tabla de ruta especificado, sin necesidad de contexto tooswitch de hello dada la hoja de la tabla de ruta.

En este ejemplo, se ha especificado una UDR (*UDRoute*) en una tabla de rutas (*UDRouteTable*). Esta ruta envía todo el tráfico de Internet de *subred1* en hello *oesteee. UU.-VNet1* red virtual, a través de un dispositivo de red virtual (NVA) en *subred2* de Hola misma red virtual. ruta de Hola se muestra en hello después de imagen:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee Hola agregado las rutas para una tabla de ruta completa Hola pasos:

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **Más servicios** y, a continuación, haga clic en **Tablas de rutas**.
3. Lista de Hola de búsqueda para la tabla de rutas de hello desea toosee agregado rutas para y selecciónelo. En este ejemplo, **UDRouteTable** está seleccionada. Aparece una hoja de una tabla de rutas Hola seleccionado, como se muestra en hello después de imagen:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Seleccione **rutas efectivas** en hello **una tabla de rutas** hoja. Hola **ámbito** se establece toohello ha seleccionado una tabla de rutas.
5. Una tabla de rutas puede ser subredes toomultiple aplicada. Seleccione hello **subred** desea tooreview de lista de Hola. En este ejemplo está seleccionada **Subnet1** .
6. Seleccione una **Interfaz de red**. Se muestran todas las NIC conectado toohello seleccionado subred. En este ejemplo está seleccionada **VM1 NIC1** .

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Si Hola NIC no está asociado a una máquina virtual en ejecución, no se muestran rutas efectivas.
   >
   >

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
  * Las reglas del grupo de seguridad de red (NSG) que pueden influir en los flujos de tráfico de Hola. Para obtener más información, vea hello [solucionar problemas de grupos de seguridad de red](virtual-network-nsg-troubleshoot-portal.md) artículo.
