---
title: "Red Virtual (VNet) aaaAzure Guía de diseño y Plan | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooplan y diseño de redes virtuales en Azure según sus requisitos de aislamiento, la conectividad y la ubicación."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planeación y diseño de redes virtuales de Azure
Crear un tooexperiment de red virtual con es bastante fácil, pero lo más probable es que se va a implementar varias redes virtuales a través de necesidades de producción de hello tiempo toosupport de su organización. Con cierta planificación y diseño, debe ser capaz de toodeploy redes virtuales y conectarse a recursos de hello que necesita más eficazmente. Si no está familiarizado con las redes virtuales, se recomienda que se [obtener información sobre redes virtuales](virtual-networks-overview.md) y [cómo toodeploy](virtual-networks-create-vnet-arm-pportal.md) uno antes de continuar.

## <a name="plan"></a>Plan
Un conocimiento detallado de las suscripciones, las regiones y los recursos de red de Azure resulta fundamental para obtener éxito. Puede usar la lista Hola consideraciones a continuación como punto de partida. Una vez que comprenda las consideraciones, puede definir requisitos de hello para el diseño de red.

### <a name="considerations"></a>Consideraciones
Antes de contestar Hola siguientes preguntas de planificación, tenga en cuenta Hola siguiente:

* Todo lo que se crea en Azure consta de uno o más recursos. Una máquina virtual (VM) es un recurso, Hola adaptador interfaz de red (NIC) utilizada por una máquina virtual es un recurso, dirección IP pública Hola utilizado por una NIC es un recurso, red virtual de Hola Hola NIC es toois conectado un recurso.
* Puede crear recursos dentro de una suscripción y una [región de Azure](https://azure.microsoft.com/regions/#services) . Recursos solo pueden ser tooa conectado red virtual que existe en hello mismo recurso de Hola de región y la suscripción se encuentra en.
* Puede conectar redes virtuales tooeach otros mediante:
    * **[Intercambio de tráfico de red virtual](virtual-network-peering-overview.md)**: redes virtuales Hola deben existir en hello misma región de Azure. Ancho de banda entre los recursos en redes virtuales emparejar es Hola mismo como si fueron de los recursos de hello toohello conectado misma red virtual.
    * **Un Azure [puerta de enlace VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: redes virtuales Hola pueden existir en hello iguales, o en diferentes regiones de Azure. Ancho de banda entre los recursos en redes virtuales conectadas a través de una puerta de enlace de VPN está limitado por el ancho de banda de Hola de hello puerta de enlace VPN.
* Puede conectar red local de redes virtuales tooyour mediante uno de hello [opciones de conectividad](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) disponibles en Azure.
* Varios recursos pueden agruparse en [grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), lo que sea más fácil recursos de hello toomanage como una unidad. Un grupo de recursos puede contener recursos de varias regiones, siempre que pertenecen los recursos de hello toohello misma suscripción.

### <a name="define-requirements"></a>Definición de los requisitos
Usar preguntas de Hola a continuación como un punto de partida para el diseño de red de Azure.    

1. ¿Qué ubicaciones de Azure en el que podrá usar toohost redes virtuales?
2. ¿Necesita tooprovide comunicación entre estas ubicaciones de Azure?
3. ¿Necesita tooprovide comunicación entre el VNet(s) de Azure y su datacenter(s) local?
4. ¿Cuántas máquinas virtuales de infraestructura como servicio (IaaS), roles de servicios en la nube y aplicaciones web necesita para su solución?
5. ¿Necesita tráfico tooisolate basado en grupos de máquinas virtuales (es decir, front-end web servidores y servidores de base de datos de back-end)?
6. ¿Necesita que el flujo de tráfico de toocontrol con dispositivos virtuales?
7. ¿Hacer los usuarios necesidad de distintos conjuntos de permisos toodifferent recursos de Azure?

### <a name="understand-vnet-and-subnet-properties"></a>Descripción de las propiedades de las redes virtuales y las subredes
Los recursos de las redes virtuales y las subredes ayudan a definir un límite de seguridad para las cargas de trabajo que se ejecutan en Azure. Una red virtual se caracteriza por una colección de espacios de direcciones, también denominados bloques CIDR.

> [!NOTE]
> Los administradores de red ya están familiarizados con la notación CIDR. Si no está familiarizado con el formato CIDR, [puede obtener más información](http://whatismyipaddress.com/cidr).
>
>

Redes virtuales contienen Hola propiedades siguientes.

| Propiedad | Description | Restricciones |
| --- | --- | --- |
| **name** |Nombre de red virtual |Cadena de caracteres too80. Puede incluir letras, números, caracteres de subrayado, puntos o guiones. Debe empezar por una letra o un número. Debe finalizar en una letra, un número o un carácter de subrayado. Puede incluir letras mayúsculas o minúsculas. |
| **ubicación** |Ubicación de Azure (también denominado tooas región). |Debe ser uno de hello ubicaciones válidas de Azure. |
| **addressSpace** |Colección de prefijos de direcciones que constituyen Hola red virtual en la notación CIDR. |Debe ser una matriz de bloques de direcciones CIDR válidos, incluidos intervalos de direcciones IP públicas. |
| **subredes** |Colección de subredes que componen Hola red virtual |vea la tabla de propiedades de subred de hello siguiente. |
| **dhcpOptions** |El objeto que contiene una propiedad requerida única llamada **dnsServers**. | |
| **dnsServers** |Matriz de servidores DNS usados por hello red virtual. Si no se especifica ningún servidor, se usa la resolución interna de nombres de Azure. |Debe ser una matriz de los servidores DNS too10, mediante una dirección IP. |

Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP. Pueden agregarse NIC toosubnets y tooVMs conectados, proporcionar conectividad para diversas cargas de trabajo.

Subredes contienen Hola propiedades siguientes.

| Propiedad | Description | Restricciones |
| --- | --- | --- |
| **name** |Nombre de subred |Cadena de caracteres too80. Puede incluir letras, números, caracteres de subrayado, puntos o guiones. Debe empezar por una letra o un número. Debe finalizar en una letra, un número o un carácter de subrayado. Puede incluir letras mayúsculas o minúsculas. |
| **ubicación** |Ubicación de Azure (también denominado tooas región). |Debe ser uno de hello ubicaciones válidas de Azure. |
| **addressPrefix** |Prefijo de dirección única que componen la subred de hello en la notación CIDR |Debe ser un único bloque CIDR que forma parte de uno de los espacios de direcciones de la red virtual de Hola. |
| **networkSecurityGroup** |NSG aplica toohello subred | |
| **routeTable** |Tabla de ruta aplicado toohello subred | |
| **ipConfigurations** |Colección de objetos de configuración de IP usa NIC conectado toohello subred | |

### <a name="name-resolution"></a>Resolución de nombres
De forma predeterminada, se utiliza la red virtual [resolución de nombres que viene con Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nombres Hola red virtual y en Hola Internet pública. Sin embargo, si se conectan a los centros de datos de redes virtuales tooyour local, deberá tooprovide [su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nombres entre las redes.  

### <a name="limits"></a>límites
Revise los límites de red de hello en hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) tooensure de artículo que su diseño no entra en conflicto con alguno de los límites de Hola. Algunos límites se pueden aumentar con la apertura de una incidencia de soporte técnico.

### <a name="role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC)
Puede usar [RBAC de Azure](../active-directory/role-based-access-built-in-roles.md) nivel de hello toocontrol de usuarios diferentes de acceso puede tener toodifferent recursos en Azure. De este modo puede dividir el trabajo de hello realizado por el equipo según sus necesidades.

En lo que las redes virtuales están en cuestión, los usuarios de hello **red colaborador** rol tiene control total sobre los recursos de red virtual de Azure Resource Manager. De igual forma, los usuarios de hello **clásico colaborador de red** rol tiene control total sobre los recursos de red virtual clásica.

> [!NOTE]
> También puede [crear sus propios roles](../active-directory/role-based-access-control-configure.md) tooseparate sus necesidades administrativas.
>
>

## <a name="design"></a>Diseño
Una vez que sepa respuestas hello toohello preguntas en hello [planear](#Plan) sección, revise los siguientes Hola antes de definir las Vnet.

### <a name="number-of-subscriptions-and-vnets"></a>Cantidad de suscripciones y redes virtuales
Considere la posibilidad de crear varias redes virtuales en hello los escenarios siguientes:

* **Máquinas virtuales que necesitan toobe situada en ubicaciones diferentes de Azure**. Las redes virtuales de Azure son regionales. No pueden abarcar ubicaciones. Por lo tanto, necesitará al menos una red virtual para cada ubicación de Azure que desee toohost las máquinas virtuales en.
* **Las cargas de trabajo que necesitan toobe completamente aislada entre sí**. Puede crear redes virtuales independientes, ese Hola de uso incluso mismo espacios de direcciones IP, tooisolate distintas cargas de trabajo entre sí.

Tenga en cuenta que los límites de Hola que se ven arriba son por cada región por suscripción. Esto significa que puede utilizar varias suscripciones tooincrease Hola límite de recursos, puede mantener en Azure. Puede usar una VPN de sitio a sitio o un circuito de ExpressRoute, tooconnect redes virtuales en distintas suscripciones.

### <a name="subscription-and-vnet-design-patterns"></a>Patrones de diseño de redes virtuales y suscripciones
Hola tabla siguiente muestran algunos patrones de diseño común para el uso de suscripciones y redes virtuales.

| Escenario | Diagrama | Ventajas | Desventajas |
| --- | --- | --- | --- |
| Suscripción única, dos redes virtuales por aplicación. |![Suscripción única](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Una sola suscripción toomanage. |Número máximo de redes virtuales por región de Azure. Necesita más suscripciones después de ese límite. Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo para obtener más información. |
| Una suscripción por aplicación, dos redes virtuales por aplicación. |![Suscripción única](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Usa solo dos redes virtuales por suscripción. |Toomanage más difícil cuando hay demasiadas aplicaciones. |
| Una suscripción por unidad de negocio, dos redes virtuales por aplicación. |![Suscripción única](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Equilibrio entre la cantidad de suscripciones y las redes virtuales. |Número máximo de redes virtuales por unidad de negocio (suscripción). Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo para obtener más información. |
| Una suscripción por unidad de negocio, dos redes virtuales por grupo de aplicaciones. |![Suscripción única](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Equilibrio entre la cantidad de suscripciones y las redes virtuales. |Las aplicaciones se deben aislar mediante subredes y NSG. |

### <a name="number-of-subnets"></a>Cantidad de subredes
Debe considerar varias subredes en una red virtual en hello los escenarios siguientes:

* **No hay direcciones IP privadas suficientes para todas las NIC de una subred**. Si el espacio de direcciones de subred no contiene suficientes direcciones IP para número de Hola de NIC en la subred de hello, deberá toocreate varias subredes. Tenga en cuenta que Azure reserva 5 direcciones IP privadas de cada subred que no se puede usar: Hola primero y último direcciones de espacio de direcciones de hello (para la dirección de subred de Hola y multidifusión) y toobe 3 direcciones utilizado internamente (para fines de DHCP y DNS).
* **Seguridad**. Puede utilizar grupos de tooseparate de subredes de máquinas virtuales entre sí para las cargas de trabajo que tienen una capa de la estructura y aplicar diferentes [grupos de seguridad (NSG) de red](virtual-networks-nsg.md#subnets) para esas subredes.
* **Conectividad híbrida**. Puede utilizar puertas de enlace VPN y circuitos ExpressRoute demasiado[conectar](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) su tooone de redes virtuales otro, y tooyour centros de datos local. Las puertas de enlace VPN y circuitos ExpressRoute requieren una subred de su propios toobe creado.
* **Aplicaciones virtuales**. Puede utilizar una aplicación virtual, como un firewall, un acelerador de WAN o una puerta de enlace de VPN en una red virtual de Azure. Al hacerlo, necesita demasiado[enrutar el tráfico](virtual-networks-udr-overview.md) aparatos de toothose y aislarlos en su propia subred.

### <a name="subnet-and-nsg-design-patterns"></a>Patrones de diseño de subredes y NSG
Hola tabla siguiente muestran algunos modelos de diseño comunes de uso de subredes.

| Escenario | Diagrama | Ventajas | Desventajas |
| --- | --- | --- | --- |
| Una sola subred, NSG por nivel de aplicación, por aplicación. |![Subred única](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Solo un toomanage de subred. |Varios tooisolate necesario de NSG cada aplicación. |
| Una subred por aplicación, NSG por nivel de aplicación. |![Subred por aplicación](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Menos toomanage de NSG. |Toomanage de varias subredes. |
| Una sola subred por nivel de aplicación, NSG por aplicación. |![Subred por nivel](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Equilibrio entre la cantidad de subredes y los NSG. |Número máximo de NSG por suscripción. Hola de revisión [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo para obtener más información. |
| Una subred por nivel de aplicación, por aplicación, NSG por subred. |![Subred por nivel por aplicación](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Posiblemente, una cantidad menor de NSG. |Toomanage de varias subredes. |

## <a name="sample-design"></a>Ejemplo de diseño
aplicación de hello tooillustrate de información de hello en este artículo, considere la posibilidad de hello siguiendo el escenario.

Trabaja para una empresa que tiene 2 centros de datos en Norteamérica y dos centros de datos en Europa. Ha identificado 6 a aplicaciones de nuestros clientes diferentes mantenida por 2 diferentes unidades de negocio que desea toomigrate tooAzure como una prueba piloto. arquitectura básica de Hola para aplicaciones de hello son los siguientes:

* App1, App2, App3 y App4 son aplicaciones web hospedadas en servidores Linux que ejecutan Ubuntu. Cada aplicación conecta a servidor de aplicaciones independientes de tooa que hospeda los servicios RESTful en servidores Linux. servicios RESTful Hola conectan la base de datos de MySQL tooa back-end.
* App5 y App6 son aplicaciones web hospedadas en servidores Windows que ejecutan Windows Server 2012 R2. Cada aplicación conecta a base de datos de SQL Server de back-end de tooa.
* Todas las aplicaciones están hospedadas actualmente en uno de los centros de datos de la compañía de hello en América del Norte.
* centros de datos locales de Hello usar espacio de direcciones de hello 10.0.0.0/8.

Necesita una solución de red virtual que cumpla Hola según los requisitos de toodesign:

* El consumo de recursos de las unidades de negocio no debería afectar a ninguna otra unidad de negocio.
* Debería minimizar la cantidad de Hola de redes virtuales y subredes toomake la administración sea más fácil.
* Cada unidad de negocio debe tener una sola red virtual de prueba/desarrollo para usar para todas las aplicaciones.
* Cada aplicación se hospeda en 2 centros de datos de Azure distintos por continente (Norteamérica y Europa).
* Las aplicaciones están completamente aisladas entre sí.
* Cada aplicación puede tener acceso los clientes a través de hello Internet mediante HTTP.
* Puede tener acceso a cada aplicación por centros de datos de los usuarios conectados toohello local mediante el uso de un túnel cifrado.
* Centros de datos de conexión local tooon deben usar los dispositivos VPN existentes.
* Hello grupo de red de la compañía debe tener un control total sobre la configuración de redes virtuales de Hola.
* Los desarrolladores en cada unidad de negocio solo deben ser capaz de toodeploy máquinas virtuales tooexisting subredes.
* Todas las aplicaciones se migrarán tal como están tooAzure (elevación y MAYÚS).
* las bases de datos de Hello en cada ubicación deben replicar tooother Azure ubicaciones una vez al día.
* Cada aplicación deberá usar 5 servidores front-end web, 2 servidores de aplicaciones (cuando corresponda) y 2 servidores de bases de datos.

### <a name="plan"></a>Plan
Debe iniciar el diseño de la planificación contestar la pregunta de hello en hello [definir requisitos](#Define-requirements) sección tal y como se muestra a continuación.

1. ¿Qué ubicaciones de Azure en el que podrá usar toohost redes virtuales?

    2 ubicaciones en Norteamérica y 2 ubicaciones en Europa. Debe elegirlos basados en la ubicación física de Hola de los centros de datos local existente. De este modo la conexión de su tooAzure ubicaciones físicas tendrá una mejor latencia.
2. ¿Necesita tooprovide comunicación entre estas ubicaciones de Azure?

    Sí. Puesto que las bases de datos de hello deben ser replicados tooall ubicaciones.
3. ¿Necesita tooprovide comunicación entre el VNet(s) de Azure y los centros de datos local?

    Sí. Puesto que los usuarios conectados centros de datos locales de toohello deben ser tooaccess capaz de aplicaciones de Hola a través de un túnel cifrado.
4. ¿Cuántas máquinas virtuales IaaS necesita para su solución?

    200 máquinas virtuales IaaS. App1, App2, App3 y App4 requieren, cada una, 5 servidores web, 2 servidores de aplicaciones y 2 servidores de bases de datos. Hablamos de un total de 9 máquinas virtuales IaaS por aplicación, es decir, 36 máquinas virtuales IaaS. App5 y App6 requieren, cada una, 5 servidores web y 2 servidores de bases de datos. Hablamos de un total de 7 máquinas virtuales IaaS por aplicación, es decir, 14 máquinas virtuales IaaS. Por lo tanto, necesita 50 máquinas virtuales IaaS para todas las aplicaciones en cada una de las regiones de Azure. Puesto que necesitamos toouse 4 regiones, habrá 200 máquinas virtuales de IaaS.

    También necesitará tooprovide los servidores DNS en cada red virtual o en el nombre de tooresolve de centros de datos local entre las máquinas virtuales de IaaS de Azure y la red local.
5. ¿Necesita tráfico tooisolate basado en grupos de máquinas virtuales (es decir, front-end web servidores y servidores de base de datos de back-end)?

    Sí. Todas las aplicaciones deberán estar completamente aisladas entre sí y cada nivel de aplicación también deberá estar aislado.
6. ¿Necesita que el flujo de tráfico de toocontrol con dispositivos virtuales?

    No. Aparatos virtuales pueden ser utilizado tooprovide más control sobre el flujo de tráfico, incluido el registro más detallado del plano de datos.
7. ¿Hacer los usuarios necesidad de distintos conjuntos de permisos toodifferent recursos de Azure?

    Sí. Hola red equipo necesita control total sobre la configuración de red virtual de hello, mientras que los desarrolladores solo deben ser capaz de toodeploy sus subredes toopre existente de las máquinas virtuales.

### <a name="design"></a>Diseño
Debe seguir especificando las suscripciones, las redes virtuales, subredes y los NSG de diseño de Hola. Si bien aquí los analizaremos, deberá obtener más información sobre los [NSG](virtual-networks-nsg.md) antes de finalizar el diseño.

**Cantidad de suscripciones y redes virtuales**

Hola según los requisitos es toosubscriptions relacionados y redes virtuales:

* El consumo de recursos de las unidades de negocio no debería afectar a ninguna otra unidad de negocio.
* Debería minimizar la cantidad de Hola de redes virtuales y subredes.
* Cada unidad de negocio debe tener una sola red virtual de prueba/desarrollo para usar para todas las aplicaciones.
* Cada aplicación se hospeda en 2 centros de datos de Azure distintos por continente (Norteamérica y Europa).

Según esos requisitos, necesitará una suscripción para cada unidad de negocio. De ese modo, el consumo de recursos de una unidad de negocio no se contará de cara a los límites de otras unidades de negocio. Y puesto que desea que el número de hello toominimize de redes virtuales, debe considerar el uso de hello **una suscripción por unidad de negocio, dos redes virtuales por grupo de aplicaciones** modelo tal como se muestra a continuación.

![Suscripción única](./media/virtual-network-vnet-plan-design-arm/figure9.png)

También se necesita espacio de direcciones de hello toospecify para cada red virtual. Puesto que necesita conectividad entre Hola centros de datos locales y hello regiones de Azure, espacio de direcciones de hello usado para las redes virtuales de Azure no puede entrar en conflicto con la red local de Hola y espacio de direcciones de hello usado por cada red virtual no debe entrar en conflicto con otras redes virtuales existentes. Puede usar espacios de direcciones de hello en tabla de hello siguiente toosatisfy estos requisitos.  

| **Suscripción** | **Red virtual** | **Región de Azure** | **Espacio de direcciones** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Oeste de EE. UU. |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Este de EE. UU. |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Europa del Norte |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europa occidental |172.19.0.0/16 |
| BU1 |TestDevBU1 |Oeste de EE. UU. |172.20.0.0/16 |
| BU2 |TestDevBU2 |Oeste de EE. UU. |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Oeste de EE. UU. |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Este de EE. UU. |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Europa del Norte |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europa occidental |172.25.0.0/16 |

**Cantidad de subredes y NSG**

Hola según los requisitos es toosubnets relacionados y los NSG:

* Debería minimizar la cantidad de Hola de redes virtuales y subredes.
* Las aplicaciones están completamente aisladas entre sí.
* Cada aplicación puede tener acceso los clientes a través de hello Internet mediante HTTP.
* Puede tener acceso a cada aplicación por centros de datos de los usuarios conectados toohello local mediante el uso de un túnel cifrado.
* Centros de datos de conexión local tooon deben usar los dispositivos VPN existentes.
* las bases de datos de Hello en cada ubicación deben replicar tooother Azure ubicaciones una vez al día.

En función de los requisitos, podría usar una subred por nivel de aplicación y utilizar los NSG toofilter tráfico por aplicación. De ese modo, solo tiene 3 subredes en cada red virtual (front-end, nivel de aplicación y nivel de datos) y un NSG por aplicación por subred. En este caso, puede utilizar hello **una subred por nivel de aplicación, los NSG por aplicación** modelo de diseño. Hola siguiente ilustración muestra el uso de hello del patrón de diseño de Hola que representa hello **ProdBU1US1** red virtual.

![Una subred por nivel, un NSG por aplicación por nivel](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Sin embargo, también debe toocreate una subred adicional para la conectividad VPN de hello entre Hola redes virtuales y los centros de datos local. Y debe tener un espacio de direcciones de hello toospecify para cada subred. Hola siguiente ilustración muestra una solución de ejemplo para **ProdBU1US1** red virtual. Este escenario se podría replicar para cada red virtual. Cada color representa una aplicación distinta.

![Red virtual de ejemplo](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Control de acceso**

Hello requisitos siguientes son tooaccess relacionados control:

* Hello grupo de red de la compañía debe tener un control total sobre la configuración de redes virtuales de Hola.
* Los desarrolladores en cada unidad de negocio solo deben ser capaz de toodeploy máquinas virtuales tooexisting subredes.

En función de los requisitos, puede agregar usuarios de hello toohello de equipo integrada a redes **red colaborador** rol en cada suscripción; y crear un rol personalizado para hello los desarrolladores de aplicaciones en cada suscripción que proporciona subredes tooexisting de estos derechos tooadd máquinas virtuales.

## <a name="next-steps"></a>Pasos siguientes
* [Implementar una red virtual](virtual-networks-create-vnet-arm-template-click.md) en función de un escenario.
* Comprender cómo demasiado[equilibrar la carga](../load-balancer/load-balancer-overview.md) las máquinas virtuales IaaS y [administrar el enrutamiento a través de varias regiones de Azure](../traffic-manager/traffic-manager-overview.md).
* Obtenga más información sobre [NSG y cómo tooplan y diseño](virtual-networks-nsg.md) una solución NSG.
* Obtener más información sobre las [opciones de conectividad local y redes virtuales](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
