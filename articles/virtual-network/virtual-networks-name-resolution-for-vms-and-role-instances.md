---
title: "aaaResolution para máquinas virtuales e instancias de rol"
description: "Escenarios de resolución de nombres para IaaS de Azure, soluciones híbridas, entre servicios en la nube diferentes, Active Directory y con su propio servidor DNS  "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Resolución de nombres para las máquinas virtuales e instancias de rol
Dependiendo de cómo utilice Azure toohost IaaS, PaaS y soluciones híbridas, puede que tenga tooallow Hola máquinas virtuales e instancias de rol que creas toocommunicate entre sí. Aunque esta comunicación se puede realizar mediante el uso de direcciones IP, es mucho más fácil nombres toouse que pueden recordarse fácilmente y no cambian. 

Cuando se requiere direcciones IP de toointernal de nombres de dominio de tooresolve para instancias de rol y las máquinas virtuales hospedadas en Azure, puede usar uno de estos dos métodos:

* [Resolución de nombres de Azure](#azure-provided-name-resolution)
* [Resolución de nombres con su propio servidor DNS](#name-resolution-using-your-own-dns-server) (que puede reenviar consultas toohello servidores DNS de Azure) 

tipo de Hola de resolución de nombres que se usa depende de cómo las máquinas virtuales y las instancias de rol necesitan toocommunicate entre sí.

**Hello tabla siguiente muestra escenarios y soluciones de resolución de nombre correspondientes:**

| **Escenario** | **Solución** | **Sufijo** |
| --- | --- | --- |
| Resolución de nombres entre instancias de rol o máquinas virtuales ubicadas en hello mismo servicio o red virtual en la nube |[Resolución de nombres de Azure](#azure-provided-name-resolution) |Nombre de host o FQDN |
| Resolución de nombres entre instancias de rol o máquinas virtuales ubicadas en diferentes redes virtuales |Servidores DNS administrados por el cliente que reenvían consultas entre redes virtuales para la resolución mediante Azure (proxy DNS).  Consulte [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server) |Solo FQDN |
| Resolución de nombres de servicios y de equipos locales desde instancias de rol o máquinas virtuales en Azure |Servidores DNS administrados por el cliente (por ejemplo, controlador de dominio local, controlador de dominio de solo lectura local o un DNS secundario sincronizado usando transferencias de zona).  See [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server) |Solo FQDN |
| Resolución de nombres de host de Azure desde equipos locales |Reenviar consultas tooa administrada por el cliente DNS servidor proxy en la red virtual correspondiente de hello, servidor de proxy de hello reenvía tooAzure de consultas para la resolución. See [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server) |Solo FQDN |
| DNS inverso para direcciones IP internas |[Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server) |N/D |
| Resolución de nombres entre máquinas virtuales o instancias de rol ubicadas en diferentes servicios en la nube y no en una red virtual |No aplicable. La conectividad entre máquinas virtuales e instancias de rol de servicios en la nube diferentes no es compatible fuera de una red virtual. |N/D |

## <a name="azure-provided-name-resolution"></a>Resolución de nombres de Azure
Junto con la resolución de nombres DNS públicos, Azure proporciona resolución de nombres interna para las máquinas virtuales e instancias de rol que residen dentro de Hola mismo servicio en la nube o de red virtual.  Máquinas virtuales o instancias de un servicio de nube compartir Hola DNS mismo sufijo (por lo que Hola independiente del nombre de host es suficiente) pero en servicios en la nube diferentes redes virtuales clásicas tienen distintos sufijos DNS para que hello FQDN es necesario tooresolve nombres entre servicios en la nube diferente.  En redes virtuales en el modelo de implementación del Administrador de recursos de hello, sufijo DNS de Hola sea coherente en la red virtual de hello (por lo que no es necesario Hola FQDN) y nombres DNS se pueden asignar tooboth NIC y las máquinas virtuales. Aunque la resolución de nombres que proporciona Azure no requiere ninguna configuración, no es Hola opción adecuada para todos los escenarios de implementación, tal como se muestra en la tabla de hello anterior.

> [!NOTE]
> En caso de hello de roles web y de trabajo, también puede tener acceso a direcciones IP internas de Hola de instancias de rol basadas en el número de instancia y el nombre de la función de hello mediante Hola API de REST de administración de servicios de Azure. Para obtener más información, consulte la [Referencia de la API de REST de la administración de servicios](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Características y consideraciones
**Características**

* Facilidad de uso: es necesario realizar ninguna configuración en orden toouse resolución de nombres que viene con Azure.
* servicio de resolución de nombres de viene con Azure Hello tiene una alta disponibilidad, guardando Hola necesita toocreate y administrar clústeres de sus propios servidores DNS.
* Puede utilizarse junto con su propios tooresolve de servidores DNS locales y los nombres de host de Azure.
* Resolución de nombres es siempre entre instancias de rol o máquinas virtuales dentro de hello mismo servicio en la nube sin necesidad de un FQDN.
* Se proporciona resolución de nombres entre máquinas virtuales en redes virtuales que utilizan el modelo de implementación de administrador de recursos de hello, sin necesidad de hello FQDN. Las redes virtuales en el modelo de implementación clásica de hello requieren Hola FQDN al resolver nombres de servicios en la nube diferente. 
* Puede usar los nombres de host que describan mejor las implementaciones, en lugar de trabajar con nombres generados automáticamente.

**Consideraciones:**

* no se puede modificar el sufijo DNS de Azure de Hola.
* No se pueden registrar manualmente los registros propios.
* No se admiten ni WINS ni NetBIOS. (Las máquinas virtuales no se pueden ver en el Explorador de Windows).
* Los nombres de host deben ser compatibles con el DNS (solamente pueden usar los caracteres 0-9, a-z y “-” y no pueden comenzar ni terminar con un “-”. Consulte la sección 2 de RFC 3696).
* El tráfico de consultas de DNS está limitado por cada máquina virtual. Esto no debería afectar a la mayoría de las aplicaciones.  Si se observa una limitación de solicitudes, asegúrese de que está habilitado el almacenamiento en caché del lado cliente.  Para obtener más información, consulte [obtener la mayoría de la resolución de nombres que viene con Azure de hello](#Getting-the-most-from-Azure-provided-name-resolution).
* Solo los nodos en los primeros servicios de nube 180 de Hola se registran para cada red virtual en un modelo de implementación clásica. No se aplica toovirtual redes en modelos de implementación del Administrador de recursos.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Obtener la mayoría de la resolución de nombres que viene con Azure de Hola
**Almacenamiento en caché del lado cliente:**

No todas las consultas DNS debe toobe enviado a través de la red de Hola.  Almacenamiento en caché de cliente le ayuda a reducir la latencia y mejorar señales de toonetwork de resistencia al resolver las consultas DNS periódicas desde una memoria caché local.  Los registros DNS contienen un período de vida (TTL) que permite el registro de hello caché toostore Hola tanto como sea posible sin afectar a la actualización del registro, por lo que el almacenamiento en caché de cliente es adecuado para la mayoría de los casos.

predeterminado de Hello cliente DNS de Windows tiene una memoria caché DNS integrada.  Algunos Linux distribuciones no incluyen el almacenamiento en caché de forma predeterminada, se recomienda que uno se agreguen tooeach VM de Linux (después de comprobar que no hay una memoria caché local ya).

Hay una serie de diferentes DNS almacenamiento en caché paquetes disponibles, por ejemplo, dnsmasq, presentamos Hola pasos tooinstall dnsmasq en distribuciones de hello más comunes:

* **Ubuntu (usa resolvconf)**:
  * solo tiene que instalar paquete de hello dnsmasq ("sudo instalación apt get dnsmasq").
* **SUSE (usa netconf)**:
  * instalar el paquete de hello dnsmasq ("sudo zypper install dnsmasq") 
  * habilitar el servicio de hello dnsmasq ("systemctl enable dnsmasq.service") 
  * iniciar servicio de hello dnsmasq ("systemctl inicio dnsmasq.service") 
  * Editar "/ etcetera/sysconfig/red/config" y cambiar NETCONFIG_DNS_FORWARDER = "" demasiado "dnsmasq"
  * actualizar resolv.conf ("actualización de netconfig") tooset Hola caché como Hola a resolución DNS local
* **OpenLogic (usa NetworkManager)**:
  * instalar el paquete de hello dnsmasq ("sudo yum install dnsmasq")
  * habilitar el servicio de hello dnsmasq ("systemctl enable dnsmasq.service")
  * iniciar servicio de hello dnsmasq ("systemctl inicio dnsmasq.service")
  * Agregar "anteponer servidores de nombres de dominio 127.0.0.1;" too"/etc/dhclient-eth0.conf"
  * Reinicie caché de Hola de tooset ("reinicio de red de servicio") del servicio de la red hello como Hola a resolución DNS local

> [!NOTE]
> paquete de 'dnsmasq' Hello es solo una de hello muchas memorias caché DNS disponibles para Linux.  Antes de usarlo, compruebe su idoneidad para sus necesidades concretas y que no se instale ninguna otra memoria caché.
> 
> 

**Reintentos de cliente:**

DNS es principalmente un protocolo UDP.  Como Hola protocolo UDP no garantiza la entrega de mensajes, lógica de reintento se controla en el propio protocolo DNS Hola.  Cada cliente DNS (sistema operativo) puede ofrecer una lógica de reintento diferentes según la preferencia de creadores de hello:

* Los sistemas operativos Windows realizan un intento tras un segundo y después tras otros 2, 4 y otros 4 segundos. 
* Hola reintentos del programa de instalación de Linux de manera predeterminada después de 5 segundos.  Es recomendable toochange esta tooretry 5 veces intervalos de 1 segundo.  

toocheck Hola configuración actual en una VM de Linux, 'cat /etc/resolv.conf' y buscar en línea de 'options' hello, p. ej.:

    options timeout:1 attempts:5

archivo de Hello resolv.conf es normalmente autogenerada y no debe editarse.  pasos específicos de Hola para agregar la línea hello 'opciones' varían según la distribución:

* **Ubuntu** (usa resolvconf):
  * Agregar Hola opciones línea too'/etc/resolveconf/resolv.conf.d/head' 
  * Ejecute 'resolvconf -u' tooupdate
* **SUSE** (usa netconf):
  * Agregue 'timeout:1 intentos: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parámetro en '/ etcetera/sysconfig/red/config' 
  * Ejecute 'netconfig update' tooupdate
* **OpenLogic** (usa NetworkManager):
  * Agregar 'eco "opciones timeout:1 intentos: 5" ' too'/etc/NetworkManager/dispatcher.d/11-dhclient' 
  * ejecutar tooupdate "restart de red de servicio"

## <a name="name-resolution-using-your-own-dns-server"></a>Resolución de nombres mediante su propio servidor DNS
Hay una serie de situaciones que sus necesidades de resolución de nombres pueden ir más allá de características de hello proporcionadas por Azure, por ejemplo al usar dominios de Active Directory o cuando se requieren la resolución DNS entre redes virtuales (redes virtuales).  toocover estos escenarios, Azure proporciona capacidad de Hola para toouse sus propios servidores DNS.  

Los servidores DNS en una red virtual pueden reenviar a solucionadores del tooAzure de las consultas DNS recursivas tooresolve los nombres de host dentro de esa red virtual.  Por ejemplo, un controlador de dominio (DC) ejecuta en Azure puede responder consultas tooDNS para sus dominios y reenviar todos los demás tooAzure de las consultas.  Esto permite que las máquinas virtuales toosee los recursos locales (a través de Hola DC) y el proporcionado por Azure nombres de host (a través de reenviador de hello).  Solucionadores de recursiva del acceso tooAzure se proporciona a través de la dirección IP virtual de hello 168.63.129.16.

El reenvío de DNS también habilita la resolución DNS de red virtual entre redes y permite la tooresolve de máquinas locales los nombres de host proporcionado por Azure.  En orden tooresolve nombre de host de la máquina virtual, la máquina virtual del servidor DNS de hello debe residir en hello mismo virtual de red y ser tooAzure de consultas de nombre de host tooforward configurado.  Como sufijo DNS de hello es diferente en cada red virtual, puede utilizar el reenvío condicional reglas toosend DNS consulta toohello corregir red virtual para la resolución.  Hola siguiente imagen muestra dos redes virtuales y una red local realizar la resolución DNS de red virtual entre redes mediante este método.  Un reenviador DNS de ejemplo está disponible en hello [Galería de plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) y [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS entre redes virtuales](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Cuando se utiliza la resolución de nombres que viene con Azure, un sufijo DNS interno (*. internal.cloudapp.net) proporcionado tooeach VM usa DHCP.  Esto habilita la resolución de nombre de host como nombre de host de hello registros se encuentran en la zona de internal.cloudapp.net Hola.  Cuando se utiliza su propia solución de resolución de nombre, Hola IDN sufijo no es proporciona tooVMs puesto que interfiere con otras arquitecturas DNS (por ejemplo, en escenarios unidos a un dominio).  En su lugar, proporcionamos un marcador de posición no funcional (reddog.microsoft.com).  

Si es necesario, se puede determinar sufijo de DNS interno de hello mediante API de PowerShell o hello:

* Para las redes virtuales en modelos de implementación del Administrador de recursos, está disponible a través de hello sufijo hello [tarjeta de interfaz de red](https://msdn.microsoft.com/library/azure/mt163668.aspx) recurso o a través de hello [AzureRmNetworkInterface Get](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* En los modelos de implementación clásica, está disponible a través de hello sufijo hello [obtener API de implementación](https://msdn.microsoft.com/library/azure/ee460804.aspx) llamar o a través de hello [Get-AzureVM-depurar](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

Si el reenvío de las consultas tooAzure no se ajusta a sus necesidades, deberá tooprovide su propia solución DNS.  La solución de DNS deberá cumplir estos requisitos:

* Proporcionar la resolución adecuada de nombres de host, por ejemplo, mediante [DDNS](virtual-networks-name-resolution-ddns.md).  Tenga en cuenta que si utiliza DDNS debe toodisable DNS borrado de registros de concesiones DHCP de Azure son muy largos y eliminación de registros obsoletos puede quitar DNS registra prematuramente. 
* Proporcionar resolución recursiva adecuado de tooallow de resolución de nombres de dominio externos.
* Se puede tener acceso (TCP y UDP en el puerto 53) de los clientes de hello sirve y ser capaz de tooaccess Hola internet.
* Protegerse contra el acceso de hello internet, toomitigate amenazas agentes externos.

> [!NOTE]
> Para obtener el mejor rendimiento, cuando se usa máquinas virtuales de Azure como servidores DNS, se debe deshabilitar IPv6 y un [IP pública a nivel de instancia](virtual-networks-instance-level-public-ip.md) debe asignarse la máquina virtual del servidor DNS de tooeach.  Si elige toouse Windows Server como el servidor DNS, [este artículo](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) proporciona análisis de rendimiento adicionales y las optimizaciones.
> 
> 

### <a name="specifying-dns-servers"></a>Especificar los servidores DNS
Al utilizar sus propios servidores DNS, Azure proporciona Hola capacidad toospecify varios servidores DNS por cada red virtual o por red (Administrador de recursos) de la interfaz / servicio (clásica) en la nube.  Los servidores DNS especificados para una interfaz de red o servicio de nube obtienen prioridad frente a las especificadas para la red virtual de Hola.

> [!NOTE]
> Propiedades de conexión de red, como el servidor DNS de direcciones IP, no debe editarse directamente dentro de máquinas virtuales de Windows tal y como puede obtener borran durante el servicio de reparación cuando se reemplaza el adaptador de red virtual de Hola. 
> 
> 

Cuando se usa el modelo de implementación del Administrador de recursos de hello, servidores DNS pueden especificarse en hello Portal, API/plantillas ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) o PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Cuando se usa el modelo de implementación clásica de hello, servidores DNS de red virtual de hello puede especificarse en Hola Portal o [hello *configuración de red* archivo](https://msdn.microsoft.com/library/azure/jj157100).  Servicios de nube, los servidores DNS Hola se especifican a través de [hello *configuración del servicio* archivo](https://msdn.microsoft.com/library/azure/ee758710) o en PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Si cambiar la configuración de DNS de Hola para una máquina virtual/red virtual que ya se ha implementado, necesitará toorestart cada VM afectado para hello cambios tootake efecto.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Modelo de implementación de Resource Manager:

* [Creación o actualización de una red virtual](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Creación o actualización de una tarjeta de interfaz de red](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Modelo de implementación clásico:

* [Esquema de configuración del servicio de Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Esquema de configuración de Red virtual](https://msdn.microsoft.com/library/azure/jj157100)
* [Configuración de una red virtual con un archivo de configuración de red](virtual-networks-using-network-configuration-file.md) 

