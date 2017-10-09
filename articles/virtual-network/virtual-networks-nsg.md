---
title: aaaNetwork grupos de seguridad de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo fluyen tooisolate y controlar el tráfico dentro de las redes virtuales con firewall de hello distribuida en Azure con grupos de seguridad de red."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Filtrado del tráfico de red con grupos de seguridad de red

Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooresources de tráfico de red conectados a redes virtuales tooAzure (VNet). Los NSG pueden ser toosubnets asociado, máquinas virtuales individuales (clásico), o interfaces de red individuales (NIC) adjunta tooVMs (Administrador de recursos). Cuando un NSG está asociado tooa subred, Hola reglas aplican tooall recursos toohello conectado subred. Tráfico puede restringir aún más mediante la asociación también un tooa NSG VM o NIC.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de ambos modelos, pero Microsoft recomienda más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

## <a name="nsg-resource"></a>Recurso NSG
Los NSG contienen Hola propiedades siguientes:

| Propiedad | Description | Restricciones | Consideraciones |
| --- | --- | --- | --- |
| Nombre |Nombre de hello NSG |Debe ser único dentro de la región de Hola.<br/>Puede incluir letras, números, caracteres de subrayado, puntos y guiones.<br/>Debe empezar por una letra o un número.<br/>Debe finalizar en una letra, un número o un carácter de subrayado.<br/>No puede superar los 80 caracteres. |Puesto que puede que necesite toocreate varios NSG, asegúrese de que tiene una convención de nomenclatura que facilita la función de hello tooidentify fácil de sus NSG. |
| Region |Azure [región](https://azure.microsoft.com/regions) donde hello NSG se crea. |Los NSG solo pueden ser tooresources asociado dentro de hello misma región que hello NSG. |toolearn sobre cuántos NSG puede tener por región, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#virtual-networking-limits-classic) artículo.|
| Grupos de recursos |Hola [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) hello NSG existe en. |Aunque un NSG existe en un grupo de recursos, puede ser tooresources asociados en un grupo de recursos, como recurso de hello forma parte del programa Hola misma región de Azure como hello NSG. |Grupos de recursos es toomanage usa varios recursos de forma conjunto como una unidad de implementación.<br/>Considere la agrupación hello NSG con está asociado a los recursos. |
| Reglas |Las reglas de entrada o de salida que definen qué tráfico se permite o deniega. | |Vea hello [reglas del NSG](#Nsg-rules) sección de este artículo. |

> [!NOTE]
> Las ACL basadas en el punto de conexión y seguridad de red no se admiten grupos en Hola la misma instancia de máquina virtual. Si desea toouse un NSG y tiene un punto de conexión ACL ya en su lugar, primero quite el extremo de hello ACL. toolearn cómo leer tooremove una ACL hello [administrar Access Control Lists (ACL) para extremos usando PowerShell](virtual-networks-acl-powershell.md) artículo.
> 

### <a name="nsg-rules"></a>Reglas de grupo de seguridad de red
Reglas NSG contienen Hola propiedades siguientes:

| Propiedad | Description | Restricciones | Consideraciones |
| --- | --- | --- | --- |
| **Name** |Nombre de regla de Hola. |Debe ser único dentro de la región de Hola.<br/>Puede incluir letras, números, caracteres de subrayado, puntos y guiones.<br/>Debe empezar por una letra o un número.<br/>Debe finalizar en una letra, un número o un carácter de subrayado.<br/>No puede superar los 80 caracteres. |Puede tener varias reglas dentro de un NSG, por lo tanto, asegúrese de que seguir una convención de nomenclatura que permite la función de Hola de tooidentify de la regla. |
| **Protocolo** |Protocolo toomatch de regla de Hola. |TCP, UDP o *. |Utilizar * como un protocolo incluye ICMP (solo el tráfico este-oeste), como así como UDP y TCP y puede reducir el número de Hola de reglas que necesita.<br/>Hola al mismo tiempo, con * podría ser demasiado amplio un enfoque, por lo que se recomienda que utilice * solo cuando sea necesario. |
| **Intervalo de puertos de origen** |Toomatch de intervalo de puerto de origen para la regla de Hola. |Solo el número de puerto de 1 too65535, intervalo de puertos (ejemplo: 1-65535), o * (para todos los puertos). |Los puertos de origen podrían ser transitorios. A menos que el programa cliente use un puerto concreto, utilice * en la mayoría de los casos.<br/>Intente intervalos de puertos de toouse tooavoid posible Hola imprescindible para varias reglas.<br/>Los distintos puertos o intervalos de puertos no se pueden agrupar mediante una coma. |
| **Intervalo de puertos de destino** |Toomatch de intervalo de puerto de destino para la regla de Hola. |Solo el número de puerto de 1 too65535, intervalo de puertos (ejemplo: 1-65535), o \* (para todos los puertos). |Intente intervalos de puertos de toouse tooavoid posible Hola imprescindible para varias reglas.<br/>Los distintos puertos o intervalos de puertos no se pueden agrupar mediante una coma. |
| **Prefijo de dirección de origen** |Origen dirección prefijo o etiqueta toomatch de regla de Hola. |Dirección IP única (ejemplo: 10.10.10.10), subred IP (ejemplo: 192.168.1.0/24), [etiqueta predeterminada](#default-tags) o * (para todas las direcciones). |Considere el uso de intervalos, las etiquetas predeterminadas, y * número de hello tooreduce de reglas. |
| **Prefijo de dirección de destino** |Destino dirección prefijo o etiqueta toomatch de regla de Hola. | Dirección IP única (ejemplo: 10.10.10.10), subred IP (ejemplo: 192.168.1.0/24), [etiqueta predeterminada](#default-tags) o * (para todas las direcciones). |Considere el uso de intervalos, las etiquetas predeterminadas, y * número de hello tooreduce de reglas. |
| **Dirección** |Dirección del tráfico toomatch de regla de Hola. |De entrada o de salida. |Las reglas de entrada y de salida se procesan por separado, en función de la dirección. |
| **Prioridad** |Se comprueban las reglas en orden de Hola de prioridad. Una vez que se aplica una regla, no se comprueba si las demás coinciden. | Número entre 100 y 4096. | Considere la posibilidad de crear reglas de salto prioridades por 100 por cada espacio de tooleave de regla para las nuevas reglas que puede crear en hello futuras. |
| **Access** |Tipo de acceso tooapply si coincide con la regla de Hola. | Permítalo o deniéguelo. | Tenga en cuenta que si no se encuentra una regla de permiso para un paquete, paquete de saludo se quita. |

Los grupos de seguridad de red contienen dos tipos de reglas: de entrada y de salida. prioridad de Hola para una regla debe ser único dentro de cada conjunto. 

![Procesamiento de reglas de NSG](./media/virtual-network-nsg-overview/figure3.png) 

imagen de Hello anterior muestra cómo se procesan las reglas NSG.

### <a name="default-tags"></a>Etiquetas predeterminadas
Etiquetas predeterminadas son identificadores proporcionados por el sistema tooaddress una categoría de direcciones IP. Puede utilizar las etiquetas predeterminadas en hello **prefijo de dirección de origen** y **prefijo de dirección de destino** propiedades de cualquier regla. Hay tres etiquetas predeterminadas que puede utilizar:

* **VirtualNetwork** (Administrador de recursos) (**VIRTUAL_NETWORK** para clásico): esta etiqueta incluye el espacio de direcciones de red virtual de hello (intervalos CIDR definidos en Azure), todos conectados espacios de direcciones local y conectado Redes virtuales Azure (redes locales).
* **AzureLoadBalancer** (Resource Manager) (**AZURE_LOADBALANCER** para el modelo clásico): esta etiqueta denota el equilibrador de carga de la infraestructura de Azure. etiqueta de Hello traduce tooan IP de centro de datos Azure comprobaciones de mantenimiento de Azure donde se originan.
* **Internet** (Administrador de recursos) (**INTERNET** para clásico): esta etiqueta denota el espacio de direcciones IP de Hola que está fuera de la red virtual de Hola y es accesible por Internet pública. intervalo de Hello incluye hello [Azure propiedad espacio de IP públicas](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Reglas predeterminadas
Todos los grupos de seguridad de red contienen un conjunto de reglas predeterminadas. no se puede eliminar las reglas predeterminadas de Hello, pero dado que se asignan prioridad más baja de hello, pueden reemplazarse por reglas de Hola que cree. 

las reglas predeterminadas de Hello permiten y denegar el tráfico como se indica a continuación:
- **Red virtual:** el tráfico que se origina y termina en una red virtual se permite en las direcciones tanto de entrada como de salida.
- **Internet:** se permite el tráfico saliente, pero se bloquea el entrante.
- **El equilibrador de carga:** estado hello tooprobe de equilibrador de carga de Azure permiten de las máquinas virtuales y las instancias de rol. Si no va a usar un conjunto con equilibrio de carga, puede invalidar esta regla.

**Reglas predeterminadas de entrada**

| Nombre | Prioridad | IP de origen | Puerto de origen | IP de destino | Puerto de destino | Protocolo | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | PERMITIR |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | PERMITIR |
| DenyAllInBound |65500 | * | * | * | * | * | DENEGAR |

**Reglas predeterminadas de salida**

| Nombre | Prioridad | IP de origen | Puerto de origen | IP de destino | Puerto de destino | Protocolo | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | PERMITIR |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | PERMITIR |
| DenyAllOutBound | 65500 | * | * | * | * | * | DENEGAR |

## <a name="associating-nsgs"></a>Asociación de grupos de seguridad de red 
Puede asociar un NSG tooVMs, NIC y subredes, según el modelo de implementación de hello que usa, como se indica a continuación:

* **Máquina virtual (solo clásico):** se aplican las reglas de seguridad tooall tráfico hacia y desde Hola VM. 
* **NIC (solo el Administrador de recursos):** se aplican las reglas de seguridad tooall tráfico hacia y desde Hola Hola NIC NSG está asociado a. En una VM de varias NIC, puede aplicar diferentes (u Hola igual) NSG tooeach NIC individualmente. 
* **Subred (Administrador de recursos y clásico):** se aplican las reglas de seguridad tooany tráfico hacia y desde los recursos conectado toohello red virtual.

Puede asociar diferentes NSG tooa VM (o NIC, según el modelo de implementación de hello) y Hola subred que una NIC o la máquina virtual está conectado a. Reglas de seguridad de tráfico de toohello aplicado, por prioridad, en cada NSG, Hola siguientes está orden:

- **Tráfico de entrada**

  1. **NSG aplica toosubnet:** si una subred NSG tiene un tráfico de toodeny regla coincidente, se quita el paquete de saludo.

  2. **NSG aplica tooNIC** (Administrador de recursos) o la máquina virtual (clásica): NSG VM\NIC si tiene una regla de coincidencia que deniega el tráfico, los paquetes se quitan en hello VM\NIC, aun cuando un NSG de subred tiene una regla de coincidencia que permita el tráfico.

- **Tráfico de salida**

  1. **NSG aplica tooNIC** (Administrador de recursos) o la máquina virtual (clásica): si un NSG VM\NIC tiene una regla de coincidencia que deniega el tráfico, se quitan los paquetes.

  2. **NSG aplica toosubnet:** si una subred NSG tiene una regla de coincidencia que deniega el tráfico, se quitan los paquetes, aun cuando un NSG VM\NIC tiene una regla de coincidencia que permita el tráfico.

> [!NOTE]
> Aunque sólo se puede asociar una única subred tooa NSG, VM o NIC; puede asociar Hola mismo tooas NSG muchos recursos, como desee.
>

## <a name="implementation"></a>Implementación
Puede implementar los NSG de Hola Administrador de recursos o modelos de implementación clásica mediante Hola siguientes herramientas:

| Herramienta de implementación | Clásico | Resource Manager |
| --- | --- | --- |
| Azure Portal   | Sí | [Sí](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Sí](virtual-networks-create-nsg-classic-ps.md) | [Sí](virtual-networks-create-nsg-arm-ps.md) |
| CLI de Azure **V1**   | [Sí](virtual-networks-create-nsg-classic-cli.md) | [Sí](virtual-networks-create-nsg-cli-nodejs.md) |
| CLI de Azure **V2**   | No | [Sí](virtual-networks-create-nsg-arm-cli.md) |
| Plantilla del Administrador de recursos de Azure   | No  | [Sí](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planificación
Antes de implementar los NSG, necesita hello tooanswer siguientes preguntas:

1. ¿Qué tipos de recursos desea toofilter tráfico tooor de? Puede conectarse a recursos como interfaces de red (Resource Manager), máquinas virtuales (clásicas), Cloud Services, entornos de servicio de aplicación y conjuntos de escalado de máquinas virtuales. 
2. ¿Son los recursos de hello desea toofilter tráfico hacia/desde toosubnets conectado en redes virtuales existentes?

Para obtener más información sobre la planeación de seguridad de red en Azure, lea hello [servicios de nube y seguridad de red](../best-practices-network-security.md) artículo. 

## <a name="design-considerations"></a>Consideraciones de diseño
Una vez que sepa respuestas hello toohello preguntas en hello [planificación](#Planning) sección, revise hello las secciones siguientes antes de definir sus NSG:

### <a name="limits"></a>límites
Hay límites de número de toohello de NSG puede tener en una suscripción y el número de reglas por NSG. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.

### <a name="vnet-and-subnet-design"></a>Diseño de red virtual y subred
Puesto que los NSG pueden ser toosubnets aplicado, se puede minimizar el número de Hola de NSG agrupar los recursos de subred, y aplicando los NSG toosubnets.  Si decide tooapply NSG toosubnets, es posible que redes virtuales existentes y las subredes que tiene no se definieron con NSG en mente. Puede necesita toodefine toosupport de redes virtuales y subredes de nuevo el diseño NSG e implementar las nuevos recursos tooyour nuevas subredes. A continuación, podría definir una toomove de estrategia de migración existente toohello nuevas subredes de recursos. 

### <a name="special-rules"></a>Reglas especiales
Si bloquea el tráfico permitido por hello siguiendo las reglas, la infraestructura no puede comunicarse con servicios esenciales de Azure:

* **Dirección IP virtual del nodo de host de hello:** servicios de infraestructura básica, como DHCP, DNS y supervisión de estado se proporcionan a través del host virtualizado Hola dirección IP 168.63.129.16. Esta dirección IP pública pertenece tooMicrosoft y es Hola única dirección IP virtualizada utilizado en todas las regiones para este propósito. Esta dirección IP asigna toohello dirección IP física del equipo del servidor hello (nodo de host) Hola VM de hospedaje. nodo de host de Hello actúa como retransmisión DHCP de hello, resolución recursiva de DNS de Hola y origen de sondeo de Hola para hello cargan sondeo del equilibrador de mantenimiento y sondeo de estado de máquina de Hola. Dirección IP de toothis de comunicación no es un ataque.
* **Licencias (Servicio de administración de claves):** las imágenes de Windows que se ejecutan en máquinas virtuales deben contar con licencia. tooensure licencias, una solicitud se envía a servidores de host de servicio de administración de claves de toohello que administran dichas consultas. Hola se solicita saliente a través del puerto 1688.

### <a name="icmp-traffic"></a>Tráfico ICMP
reglas Hola actuales del NSG solo permiten los protocolos *TCP* o *UDP*. No hay una etiqueta específica para *ICMP*. Sin embargo, se permite el tráfico ICMP dentro de una red virtual ninguna regla de hello AllowVNetInBound predeterminado, que permite tooand de tráfico de cualquier puerto y protocolo de red virtual de Hola.

### <a name="subnets"></a>Subredes
* Tenga en cuenta el número de Hola de niveles que requiere la carga de trabajo. Cada nivel se pueden aislar mediante el uso de una subred, con una subred de toohello NSG aplica. 
* Si necesita tooimplement una subred de puerta de enlace VPN o de circuito de ExpressRoute, **no** una subred de toothat NSG se aplican. Si lo hace, es posible que la conectividad entre entornos locales o entre redes virtuales no funcione. 
* Si necesita un dispositivo de red virtual (NVA) tooimplement, conectar propia subred de hello NVA tooits y crear rutas definidas por el usuario (UDR) tooand de hello NVA. Puede implementar un nivel de subred tráfico de toofilter NSG dentro y fuera de esta subred. más información acerca de UDRs, leer hello toolearn [rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.

### <a name="load-balancers"></a>Equilibradores de carga
* Considere la posibilidad de dirección de red y el equilibrio de carga de hello las reglas de conversión (NAT) para cada equilibrador de carga utilizados por cada una de las cargas de trabajo. Las reglas NAT son grupo back-end de tooa enlazado que contiene instancias de rol de servicios en la nube y máquinas virtuales (clásicas) o NICs (Administrador de recursos). Considere la posibilidad de crear un NSG para cada grupo back-end, lo que permite solo el tráfico asignado a través de reglas de hello implementadas en los equilibradores de carga de Hola. Crear un NSG para cada grupo back-end, se garantiza que el tráfico que llegue grupo back-end de toohello directamente (en lugar de a través del equilibrador de carga de hello), también se filtra.
* En las implementaciones de clásicas, cree los extremos que se asignan los puertos en un tooports de equilibrador de carga en sus máquinas virtuales o instancias de rol. También puede crear su propio equilibrador de carga de acceso público individual mediante Resource Manager. puerto de destino de Hello para el tráfico entrante es el puerto real de Hola Hola máquina virtual o instancia de rol, no es puerto Hola expuesto por un equilibrador de carga. puerto de origen de Hola y dirección Hola conexión toohello en que VM es un puerto y dirección Hola equipo remoto en hello Internet, no el puerto de Hola y la dirección expuestos por el equilibrador de carga de Hola.
* Cuando se crea el tráfico de toofilter NSG que llegue a través de un equilibrador de carga interno (ILB), intervalo de puerto y la dirección de la fuente de hello aplica provienen de Hola, equipo, no el equilibrador de carga Hola de origen. intervalo de puerto y la dirección de destino de Hello son aquellos Hola equipo de destino, no el equilibrador de carga Hola.

### <a name="other"></a>Otros
* Listas de control de punto de conexión de acceso (ACL) y los NSG no se admiten en hello misma instancia de máquina virtual. Si desea toouse un NSG y tiene un punto de conexión ACL ya en su lugar, primero quite el extremo de hello ACL. Para obtener información acerca de cómo tooremove un extremo ACL, vea hello [administrar las ACL de extremo](virtual-networks-acl-powershell.md) artículo.
* En el Administrador de recursos, puede usar un tooa NSG asociado NIC para las máquinas virtuales con varias NIC tooenable administración (acceso remoto) en una base por cada NIC. Asociar único NSG tooeach NIC permite la separación de tipos de tráfico a través de la NIC.
* Use toohello similar de equilibradores de carga, cuando se filtran el tráfico de otras redes virtuales, debe usar el intervalo de direcciones de origen Hola del equipo remoto hello, no Hola puerta de enlace de conexión Hola redes virtuales.
* Muchos servicios de Azure no pueden ser tooVNets conectado. Si un recurso de Azure no está conectado tooa red virtual, no puede usar un recurso de toohello NSG toofilter tráfico.  Leer documentación de Hola para los servicios de hello utilizarás toodetermine si el servicio de hello puede estar conectado tooa red virtual.

## <a name="sample-deployment"></a>Ejemplo de implementación
aplicación de hello tooillustrate de información de hello en este artículo, considere un escenario común de una aplicación de dos niveles se muestra en hello después de imagen:

![Grupos de seguridad de red](./media/virtual-network-nsg-overview/figure1.png)

Como se muestra en el diagrama de hello, Hola *Web1* y *Web2* máquinas virtuales están conectada toohello *front-end* hello y subred *DB1* y *DB2* máquinas virtuales están conectada toohello *back-end* subred.  Ambas subredes forman parte del programa Hola a *TestVNet* red virtual. componentes de aplicación de Hello cada ejecutarán dentro de una red virtual de máquina virtual de Azure conectada tooa. escenario de Hello tiene Hola según los requisitos:

1. Separación del tráfico entre hello WEB y servidores de base de datos.
2. Reenvíe el tráfico de servidores web tooall de equilibrador de carga de hello en el puerto 80 reglas de equilibrio de carga.
3. La carga del tráfico de reenvíos equilibrador NAT reglas entran equilibrador de carga de hello en tooport 50001 puerto 3389 en hello VM WEB1.
4. Ningún acceso toohello máquinas virtuales de front-end o back-end de hello Internet, excepto los requisitos de 2 y 3.
5. Sin el acceso a Internet de servidores WEB o de base de datos de Hola.
6. Se permite el acceso de la subred de front-end de hello tooport 3389 de cualquier servidor web.
7. Se permite el acceso de la subred de front-end de hello tooport 3389 de cualquier servidor de base de datos.
8. Se permite el acceso de la subred de front-end de hello tooport 1433 de todos los servidores de base de datos.
9. Separación del tráfico de administración (puerto 3389) y el de base de datos (1433) en diferentes interfaces de red en servidores de bases de datos.

Requisitos de 1 a 6 (excepto los requerimientos 3 y 4) son todos los espacios toosubnet reducidos. Hello NSG siguientes sus requisitos Hola anterior, y reduce su número de Hola de NSG requerido:

### <a name="frontend"></a>FrontEnd
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | PERMITIR | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | PERMITIR | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | DENEGAR | 300 | Internet | * | * | * | TCP |

**Reglas de salida**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |DENEGAR |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | DENEGAR | 100 | Internet | * | * | * | * |

**Reglas de salida**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | DENEGAR | 100 | * | * | Internet | * | * |

Hola NSG siguientes se crean y asociados tooNICs Hola después de las máquinas virtuales:

### <a name="web1"></a>WEB1
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | PERMITIR | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | PERMITIR | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> intervalo de direcciones de origen de Hola para las reglas anteriores de hello es **Internet**, no Hola una dirección IP virtual del equilibrador de carga de Hola. puerto de origen de Hello es *, no 500001. Las reglas NAT de equilibradores de carga no se Hola igual que las reglas de seguridad NSG. Las reglas de seguridad NSG son siempre toohello relacionados de origen y destino final de tráfico, **no** equilibrador de carga de hello entre Hola dos. 
> 
> 

### <a name="web2"></a>WEB2
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | DENEGAR | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | PERMITIR | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>Servidores de bases de datos (interfaz de red de administración)
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | PERMITIR | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>Servidores de bases de datos (interfaz de red de tráfico de base de datos)
**Reglas de entrada**

| Regla | Access | Prioridad | Intervalo de direcciones de origen | Puerto de origen | Intervalo de direcciones de destino | Puerto de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | PERMITIR | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Puesto que algunos de los NSG Hola son tooindividual asociado de NIC, reglas de hello están destinadas a los recursos implementados a través del Administrador de recursos. Las reglas se combinan para la subred y la interfaz de red, en función de cómo estén asociadas. 

## <a name="next-steps"></a>Pasos siguientes
* [Implementación de grupos de seguridad de red (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [Implementación de grupos de seguridad de red (clásicos)](virtual-networks-create-nsg-classic-ps.md).
* [Administración de registros de grupo de seguridad de red](virtual-network-nsg-manage-log.md).
* [Solución de problemas de grupo de seguridad de red] (virtual-network-nsg-troubleshoot-portal.md)
