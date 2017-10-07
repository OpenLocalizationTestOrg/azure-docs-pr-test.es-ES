---
title: P+F de red Virtual aaaAzure | Documentos de Microsoft
description: "Respuestas toohello preguntas más frecuentes sobre las redes virtuales de Microsoft Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Preguntas más frecuentes (P+F) acerca de Azure Virtual Network

## <a name="virtual-network-basics"></a>Conceptos básicos de Virtual Network

### <a name="what-is-an-azure-virtual-network-vnet"></a>¿Qué es una red virtual de Azure?
Una red Virtual de Azure (VNet) es una representación de su propia red en la nube de Hola. Es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción. Puede utilizar tooprovision de redes virtuales y administrar redes privadas virtuales (VPN) en Azure y, opcionalmente, Hola redes virtuales con otras redes virtuales en Azure, o con el entorno local de vínculo toocreate híbrido o entre entornos soluciones de infraestructura de TI. Cada red virtual que se crea tiene su propio bloque CIDR y puede ser tooother vinculado redes de redes virtuales y local siempre y cuando no se superponen los bloques CIDR Hola. También tiene un control de configuración del servidor DNS para redes virtuales y segmentación de red virtual de hello en subredes.

Use las redes virtuales para:

* Crear una red virtual solo en una nube privada dedicada. A veces no se requiere una configuración entre entornos para una solución. Cuando se crea una red virtual, los servicios y máquinas virtuales dentro de la red virtual pueden comunicarse directa y segura entre sí en la nube de Hola. Esto mantiene el tráfico de manera segura en hello red virtual, pero sí permite conexiones de punto de conexión de tooconfigure para hello las máquinas virtuales y servicios que requieren una comunicación de Internet como parte de la solución.
* Ampliar su centro de datos con las redes virtuales de forma segura, puede compilar la capacidad del centro de datos tradicional escala de toosecurely (S2S) VPN de sitio a sitio. Las VPN de S2S utilizan IPSEC tooprovide una conexión segura entre la puerta de enlace VPN y Azure corporativa.
* Habilitar escenarios de nube híbrida que redes virtuales proporcionan Hola flexibilidad toosupport una gama de escenarios de nube híbrida. Tipo de tooany de las aplicaciones basadas en la nube de sistema local como grandes sistemas y sistemas Unix se puede conectar de forma segura.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>¿Cómo sé si necesito una red virtual?
Hola [información general de red Virtual](virtual-networks-overview.md) artículo proporciona una tabla de decisiones que le ayudará a decidir Hola mejor opción de diseño de red por usted.

### <a name="how-do-i-get-started"></a>¿Cómo empiezo?
Visite hello [documentación de su red Virtual](https://docs.microsoft.com/azure/virtual-network/) tooget iniciado. Este contenido proporciona información de introducción e implementación para todas las características de red virtual de Hola.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>¿Puedo usar redes virtuales sin conectividad entre entornos?
Sí. Las redes virtuales se pueden usar sin emplear la conectividad híbrida. Esto es especialmente útil si desea que los controladores de dominio de Active Directory de Microsoft Windows Server toorun y granjas de servidores de SharePoint en Azure.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>¿Se puede realizar la optimización de una WAN entre redes virtuales o entre una red virtual y un centro de datos local?

Sí. Puede implementar un [dispositivo virtual de red de optimización de la WAN](https://azure.microsoft.com/marketplace/?term=wan+optimization) de varios proveedores a través de hello Azure Marketplace.

## <a name="configuration"></a>Configuración

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>¿Qué herramientas usar toocreate una red virtual?
Puede usar Hola después herramientas toocreate o configurar una red virtual:

* Portal de Azure (para redes virtuales clásicas y del Administrador de recursos).
* Un archivo de configuración de red (netcfg; solo para redes virtuales clásicas). Vea hello [configurar una red virtual con un archivo de configuración de red](virtual-networks-using-network-configuration-file.md) artículo.
* PowerShell (para redes virtuales clásicas y del Administrador de recursos).
* CLI de Azure (para redes virtuales clásicas y del Administrador de recursos).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>¿Qué intervalos de direcciones puedo usar en mis redes virtuales?
Cualquier intervalo de direcciones IP definido en [RFC 1918](http://tools.ietf.org/html/rfc1918). Por ejemplo, 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>¿Puedo tener direcciones IP públicas en mis redes virtuales?
Sí. Para obtener más información acerca de los intervalos de direcciones IP públicas, vea hello [espacio de direcciones IP públicas en una red virtual](virtual-networks-public-ip-within-vnet.md) artículo. Las direcciones IP públicas no será accesibles directamente desde Internet Hola.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>¿Hay un toohello limitar el número de subredes en mi red virtual?
Sí. Hola de lectura [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo para obtener más información. Los espacios de direcciones de las subredes no pueden superponerse entre sí.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>¿Hay alguna restricción en el uso de direcciones IP dentro de estas subredes?
Sí. Azure reserva algunas direcciones IP dentro de cada subred. Hello primeros y últimas direcciones IP de subredes de hello están reservadas para la conformidad con el protocolo, junto con 3 direcciones más utilizadas para los servicios de Azure.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>¿Qué tamaños mínimo y máximo pueden tener las redes virtuales y las subredes?
subred Hello más pequeño que se admite es/29 y Hola mayor es/8 (mediante las definiciones de subred CIDR).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>¿Puedo llevar Mis tooAzure de VLAN mediante redes virtuales?
No. Las redes virtuales son superposiciones de nivel 3. Azure no admite ninguna semántica de nivel 2.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>¿Puedo especificar directivas de enrutamiento personalizadas en mis redes virtuales y subredes?
Sí. Puede usar el enrutamiento definido por usuario (UDR). Para obtener más información acerca de UDR, visite [Rutas definidas por el usuario y reenvío IP](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>¿Las redes virtuales admiten la multidifusión o la difusión?
No. No se admite la multidifusión ni la difusión.

### <a name="what-protocols-can-i-use-within-vnets"></a>¿Qué protocolos puedo usar en las redes virtuales?
En las redes virtuales se pueden usar los protocolos TCP, UDP e ICMP TCP/IP. La multidifusión, la difusión, los paquetes encapsulados IP en IP y los paquetes de encapsulación de enrutamiento genérico (GRE) se bloquean en las subredes. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>¿Puedo hacer ping a mis enrutadores predeterminados dentro de una red virtual?
No.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>¿Puedo usar tracert toodiagnose conectividad?
No.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>¿Puedo agregar subredes después Hola que se crea la red virtual?
Sí. Subredes pueden agregarse tooVNets en cualquier momento como dirección de subred de hello no forma parte de otra subred de red virtual de Hola.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>¿Puedo modificar tamaño de Hola de mi subred después de crearla?
Sí. Puede agregar, quitar, expandir o contraer una subred si no hay máquinas virtuales ni servicios implementados en ella.

### <a name="can-i-modify-subnets-after-i-created-them"></a>¿Puedo modificar subredes después de crearlas?
Sí. Puede agregar, quitar y modificar Hola CIDR bloques utilizados por una red virtual.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>¿Puedo conectar toohello internet si estoy ejecutando Mis servicios en una red virtual?
Sí. Todos los servicios implementados en una red virtual pueden conectarse toohello internet. Cada servicio en la nube implementado en Azure tiene asignada tooit una VIP direccionable de forma pública. Tendrá toodefine extremos de entrada para los roles PaaS y extremos para máquinas virtuales tooenable estas conexiones de tooaccept de servicios de hello internet.

### <a name="do-vnets-support-ipv6"></a>¿Las redes virtuales admiten IPv6?
No. No se admite IPv6 con redes virtuales en este momento.

### <a name="can-a-vnet-span-regions"></a>¿Puede una red virtual abarcar varias regiones?
No. Una red virtual es limitado tooa única región.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>¿Puedo conectar una red virtual en Azure tooanother de red virtual?
Sí. Puede conectarse a una red virtual tooanother red virtual que use:
- Azure VPN Gateway. Hola de lectura [configurar una conexión de red virtual a red virtual](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artículo para obtener más información. 
- Emparejamiento de VNET. Hola de lectura [información general de intercambio de tráfico de red virtual](virtual-network-peering-overview.md) artículo para obtener más información.

## <a name="name-resolution-dns"></a>resolución de nombres DNS

### <a name="what-are-my-dns-options-for-vnets"></a>¿Qué opciones de DNS hay para las redes virtuales?
Tabla de decisiones de uso hello en hello [resolución de nombres para las máquinas virtuales e instancias de rol](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooguide de página que le guíe por todos Hola DNS opciones disponibles.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>¿Puedo especificar servidores DNS para una red virtual?
Sí. Puede especificar direcciones IP del servidor DNS en la configuración de red virtual de Hola. Esto se aplicará como servidores DNS de hello predeterminados para todas las máquinas virtuales en hello red virtual.

### <a name="how-many-dns-servers-can-i-specify"></a>¿Cuántos servidores DNS puedo especificar?
Hola de referencia [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo para obtener más información.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>¿Puedo modificar mis servidores DNS después de haber creado red Hola?
Sí. Puede cambiar la lista de servidores DNS de hello para la red virtual en cualquier momento. Si cambia la lista de servidores DNS, deberá toorestart de máquinas virtuales de hello en la red virtual puedan toopick nuevo servidor de DNS Hola.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>¿Qué es un DNS proporcionado por Azure? ¿Funciona con las redes virtuales?
Un DNS proporcionado por Azure es un servicio DNS multiempresa ofrecido por Microsoft. Azure registra en este servicio todas las máquinas virtuales y las instancias de rol de servicio en la nube. Este servicio proporciona resolución de nombres por nombre de host para máquinas virtuales e instancias de rol dentro de hello mismo servicio en la nube y FQDN para máquinas virtuales e instancias de rol de Hola misma red virtual. Hola de lectura [resolución de nombres para las máquinas virtuales e instancias de rol](virtual-networks-name-resolution-for-vms-and-role-instances.md) artículo toolearn más información acerca de DNS.

> [!NOTE]
> Hay una limitación en este momento toohello primero 100 servicios en la nube en una red virtual para la resolución de nombres entre inquilinos mediante DNS proporcionado por Azure. Si usa  su propio servidor DNS, esta limitación no es aplicable.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>¿Puedo invalidar mi configuración de DNS por máquina virtual o servicio?
Sí. Puede configurar los servidores DNS en una configuración de red según la nube servicio base toooverride Hola predeterminada. Sin embargo, recomendamos usar DNS en toda la red siempre que sea posible.

### <a name="can-i-bring-my-own-dns-suffix"></a>¿Puedo usar mi propio sufijo DNS?
No. No puede especificar un sufijo DNS personalizado para sus redes virtuales.

## <a name="connecting-virtual-machines"></a>Conexión de máquinas virtuales

### <a name="can-i-deploy-vms-tooa-vnet"></a>¿Puedo implementar máquinas virtuales tooa red virtual?
Sí. Todos los tooa de interfaces (NIC) que están conectados de red implementa la máquina virtual a través del modelo de implementación del Administrador de recursos de hello debe estar conectado tooa red virtual. Máquinas virtuales implementadas a través del modelo de implementación clásica de hello, opcionalmente, pueden ser conectado tooa red virtual.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>¿Cuáles son los tipos diferentes de hello de direcciones IP pueden asignar tooVMs?
* **Privado:** asignado tooeach NIC dentro de cada máquina virtual. dirección de Hola se asigna mediante cualquier método hello, estática o dinámica. Se asignan las direcciones IP privadas de intervalo de Hola que especificó hello en configuración de subred de la red virtual. Recursos implementados a través del modelo de implementación clásica de Hola se asignan direcciones IP privadas, incluso si no están conectados tooa red virtual. Una dirección IP privada asignada con hello método dinámico permanece asignada tooa recurso hasta que se elimine el recurso de hello (máquinas virtuales o servicio en la nube ranuras de implementación). Una dirección IP privada asignada con el método dinámico Hola puede cambiar cuando se reinicia una máquina virtual después de haber sido previamente Hola detenido estado (desasignada). Una dirección IP privada asignada con hello método estático permanece asignada tooa recurso hasta que se elimine el recurso de Hola. Si necesita tooensure esa dirección IP privada de Hola para un recurso nunca cambia hasta que se elimine el recurso de hello, asigne una dirección IP privada con el método estático de Hola.
* **Público:** tooNICs opcionalmente asignado adjunta tooVMs implementado a través del modelo de implementación de hello Azure Resource Manager. Hola dirección puede asignarse con el método de asignación estática o dinámica de Hola. Instancias de rol de todas las máquinas virtuales y servicios en la nube implementadas a través del modelo de implementación clásica de hello existen dentro de un servicio de nube, que se asigna un *dinámica*, pública dirección IP virtual (VIP). Si se desea, una dirección IP pública *estática*, que se denomina [dirección IP reservada](virtual-networks-reserved-public-ip.md), puede asignarse como si fuera una VIP. Puede asignar tooindividual de direcciones IP pública implementan instancias de rol de VM o servicios en la nube a través del modelo de implementación clásica de Hola. Estas direcciones se denominan direcciones [IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) y se puede asignar dinámicamente.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>¿Puedo reservar una dirección IP interna para una máquina virtual que crearé más adelante?
No. Las direcciones IP privadas no se pueden reservar. Si hay una dirección IP privada se le asignará tooa máquina virtual o instancia de rol servidor de DHCP de Hola. Que la máquina virtual puede o no puede ser Hola uno que desee Hola privada IP dirección toobe asignado a. Sin embargo, puede cambiar la dirección IP privada de Hola de una ya se ha creado VM tooany privada dirección IP disponible.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>¿Cambian las direcciones IP privadas de las máquinas virtuales en una red virtual?
Depende. Las direcciones IP privadas dinámicas permanecen en una máquina virtual hasta que se detenga (se desasigne) o se elimine. Las direcciones IP privadas estáticas no se liberan de una máquina virtual hasta que esta se elimina.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>¿Puedo asignar manualmente tooNICs de direcciones IP en el sistema operativo de la VM de hello?
Sí, pero no se recomienda. Modificar manualmente la dirección IP de Hola de una NIC en el sistema operativo de la máquina virtual podría causar toolosing conectividad toohello VM si la dirección IP de hello asignada tooa NIC dentro de hello Azure VM estaban toochange.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Las direcciones IP toomy ¿qué ocurre si se detiene una ranura de implementación de servicio en la nube o el cierre una máquina virtual desde dentro de sistema operativo de hello?
Nada. direcciones IP de Hello (VIP pública, pública y privada) permanecen ranura de implementación de servicio de nube toohello asignado o la máquina virtual. Las direcciones dinámicas solo se liberan si una máquina virtual se detiene (se desasigna) o se elimina, o si se elimina una ranura de implementación de un servicio en la nube. Si hace clic en hello **detener** botón para una máquina virtual dentro de hello portal de Azure, establece su tooStopped de estado (desasignado). En este caso, Hola VM perderá sus direcciones IP.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>¿Puedo mover las máquinas virtuales de una subred de tooanother de subred en una red virtual sin volver a implementar?
Sí. Puede encontrar más información en hello [cómo toomove una máquina virtual o el rol de instancia tooa otra subred](virtual-networks-move-vm-role-to-subnet.md) artículo.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>¿Puedo configurar una dirección MAC estática para mi máquina virtual?
No. Una dirección MAC no se puede configurar de forma estática.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>¿Permanecerá Hola dirección MAC Hola igual a la máquina virtual una vez que se ha creado?
Sí, Hola dirección MAC permanece Hola que iguales para una máquina virtual implementadas a través de Hola, Administrador de recursos y modelos de implementación clásica hasta que se elimina. Anteriormente, se ha liberado Hola dirección MAC si hello máquina virtual se ha detenido (desasignado), pero ahora se conserva la dirección MAC de hello aunque Hola VM está en hello cancela la asignación de estado.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>¿Puedo conectar toohello internet desde una máquina virtual en una red virtual?
Sí. Instancias de rol de todas las máquinas virtuales y servicios en la nube implementadas en una red virtual pueden conectarse toohello Internet.

## <a name="azure-services-that-connect-toovnets"></a>Servicios de Azure que se conectan tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>¿Se puede usar Azure App Service Web Apps con una red virtual?
Sí. Web Apps se puede implementar en una red virtual mediante ASE (App Service Environment). Web Apps puede conectarse de forma segura y acceder a los recursos de una red virtual de Azure si hay una conexión de punto a sitio configurada para la red virtual. Para obtener más información, vea Hola siguientes artículos:

* [Creación de Aplicaciones web en un entorno del Servicio de aplicaciones](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Integración de una aplicación con Azure Virtual Network](../app-service-web/web-sites-integrate-with-vnet.md)
* [Uso de la integración de la red virtual y de conexiones híbridas con Aplicaciones web](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>¿Puedo implementar Cloud Services con los roles web y de trabajo (PaaS) en una red virtual?
Sí. Opcionalmente, es posible implementar instancias de rol de Cloud Services en redes virtuales. toodo así pues, especifique los nombre de red virtual de Hola y asignaciones de rol/subred de hello en la sección de configuración de red de saludo de la configuración del servicio. No es necesario tooupdate cualquiera de los archivos binarios.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>¿Puedo conectar una red virtual de conjunto de escala en la máquina Virtual (VMSS) tooa?
Sí. Debe conectarse un tooa VMSS red virtual.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>¿Puedo mover mis servicios dentro y fuera de las redes virtuales?
No. No se pueden mover los servicios dentro y fuera de las redes virtuales. Tendrá toodelete y volver a implementar Hola servicio toomove se tooanother red virtual.

## <a name="security"></a>Seguridad

### <a name="what-is-hello-security-model-for-vnets"></a>¿Qué es el modelo de seguridad de Hola para redes virtuales?
Redes virtuales están completamente aisladas entre sí y otros servicios hospeden en hello infraestructura de Azure. Una máquina virtual es un límite de confianza.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>¿Se puede restringir los recursos conectado tooVNet de flujo de tráfico entrante o saliente?
Sí. Puede aplicar [grupos de seguridad de red](virtual-networks-nsg.md) tooindividual subredes dentro de una red virtual, NIC conectado tooa red virtual, o ambos.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>¿Se puede implementar un firewall entre los recursos conectados a una red virtual?
Sí. Puede implementar un [dispositivo virtual de red firewall](https://azure.microsoft.com/en-us/marketplace/?term=firewall) de varios proveedores a través de hello Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>¿Hay información disponible acerca la protección de las redes virtuales?
Sí. Vea hello [información general sobre la seguridad de red de Azure](../security/security-network-overview.md) artículo para obtener más información.

## <a name="apis-schemas-and-tools"></a>API, esquemas y herramientas

### <a name="can-i-manage-vnets-from-code"></a>¿Puedo administrar redes virtuales mediante programación?
Sí. Puede usar las API de REST para redes virtuales en hello [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) y [clásico (administración de servicios)](http://go.microsoft.com/fwlink/?LinkId=296833)) modelos de implementación.

### <a name="is-there-tooling-support-for-vnets"></a>¿Hay compatibilidad con las herramientas para redes virtuales?
Sí. Más información acerca del uso de:
- Hola toodeploy Azure portal redes virtuales a través de hello [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) y [clásico](virtual-networks-create-vnet-classic-pportal.md) modelos de implementación.
- Toomanage PowerShell redes virtuales se implementan a través de hello [el Administrador de recursos](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) y [clásico](/powershell/module/azure/?view=azuresmps-3.7.0) modelos de implementación.
- Hola [Azure interfaz de línea de comandos (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage redes virtuales que se implementan a través de ambos modelos de implementación.  
