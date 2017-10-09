---
title: "aaaDNS opciones de resolución de nombres para las máquinas virtuales de Linux en Azure"
description: "Escenarios de resolución de nombres DNS para máquinas virtuales Linux en IaaS de Azure, incluidos los servicios DNS proporcionados y el servidor DNS externo híbrido y Bring Your Own DNS."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opciones de resolución de nombres DNS para máquinas virtuales Linux en Azure
Azure proporciona resolución de nombres DNS de forma predeterminada para todas las máquinas virtuales de una única red virtual. Puede implementar su propia solución de resolución de nombre DNS si configura sus propios servicios DNS en las máquinas virtuales hospedadas de Azure. Hello siguientes escenarios deben ayudarle a elegir Hola uno que funciona para su situación.

* [Resolución de nombres que proporciona Azure](#azure-provided-name-resolution)
* [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server)

tipo Hello de resolución de nombres que utilice depende de cómo las máquinas virtuales y las instancias de rol necesitan toocommunicate entre sí.

Hello tabla siguiente muestra escenarios y soluciones de resolución de nombre correspondientes:

| **Escenario** | **Solución** | **Sufijo** |
| --- | --- | --- |
| Resolución de nombres entre instancias de rol o máquinas virtuales en hello misma red virtual |[Resolución de nombres que proporciona Azure](#azure-provided-name-resolution) |El nombre de host o el nombre de dominio completo (FQDN) |
| Resolución de nombres entre instancias de rol o máquinas virtuales de redes virtuales diferentes |Servidores DNS administrados por el cliente que reenvían consultas entre redes virtuales para la resolución mediante Azure (proxy DNS). Consulte [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server). |Solo FQDN |
| Resolución de nombres de servicios y de equipos locales desde instancias de rol o máquinas virtuales en Azure |Servidores DNS administrados por el cliente (por ejemplo, controlador de dominio local, controlador de dominio de solo lectura local o un DNS secundario sincronizado mediante transferencias de zona). Consulte [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server). |Solo FQDN |
| Resolución de nombres de host de Azure desde equipos locales |Reenviar consultas tooa administrada por el cliente DNS servidor proxy en la red virtual de hello correspondiente. servidor proxy de Hello reenvía tooAzure de consultas para la resolución. Consulte [Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server). |Solo FQDN |
| DNS inverso para direcciones IP internas |[Resolución de nombres mediante su propio servidor DNS](#name-resolution-using-your-own-dns-server) |N/D |

## <a name="name-resolution-that-azure-provides"></a>Resolución de nombres que proporciona Azure
Junto con la resolución de nombres DNS públicos, Azure proporciona resolución de nombres interna para máquinas virtuales e instancias de rol que se encuentran en Hola misma red virtual. En redes virtuales que se basan en el Administrador de recursos de Azure, sufijo DNS de hello es coherente a través de la red virtual de hello; Hola FQDN no es necesaria. Los nombres DNS pueden asignarse tooboth tarjetas de interfaz de red (NIC) y máquinas virtuales. Aunque la resolución de nombres Hola que proporciona Azure no requiere ninguna configuración, no es Hola opción adecuada para todos los escenarios de implementación, tal como se muestra en la tabla anterior de Hola.

### <a name="features-and-considerations"></a>Características y consideraciones
**Características**

* Toouse requiere la resolución de nombres que proporciona Azure no es ninguna configuración.
* servicio de resolución de nombres de Hola que proporciona Azure está altamente disponible. No necesita toocreate y administrar clústeres de sus propios servidores DNS.
* servicio de resolución de nombres de Hola que proporciona Azure puede utilizarse junto con su propios tooresolve de servidores DNS locales y los nombres de host de Azure.
* Se proporciona resolución de nombres entre máquinas virtuales en redes virtuales sin necesidad de hello FQDN.
* Puede usar los nombres de host que describan mejor las implementaciones, en lugar de trabajar con nombres generados automáticamente.

**Consideraciones:**

* no se puede modificar el sufijo DNS de Hola que Azure crea.
* No se pueden registrar manualmente los registros propios.
* No se admiten ni WINS ni NetBIOS.
* Los nombres de host deben ser compatibles con DNS.
    Los nombres solamente pueden contener caracteres 0-9, a-z y "-", y no pueden comenzar ni terminar por "-". Consulte la sección 2 de RFC 3696.
* El tráfico de consultas de DNS está limitado en cada máquina virtual. La limitación no debería afectar a la mayoría de las aplicaciones.  Si se observa una limitación de solicitudes, asegúrese de que está habilitado el almacenamiento en caché del lado cliente.  Para obtener más información, consulte [obtener la mayoría de resolución de nombres que proporciona Azure hello](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Obtener la mayoría de resolución de nombres que proporciona Azure Hola
**Almacenamiento en caché del lado cliente:**

Algunas consultas DNS no se envían a través de red de Hola. Almacenamiento en caché de cliente le ayuda a reducir la latencia y mejorar las incoherencias de toonetwork de resistencia al resolver las consultas DNS periódicas desde una memoria caché local. Los registros DNS contienen un período de vida (TTL), lo que permite el registro de hello caché toostore Hola tanto como sea posible sin afectar a la actualización del registro. Por ello, la caché del cliente es adecuada para la mayoría de las situaciones.

Algunas distribuciones de Linux no incluyen el almacenamiento en caché de forma predeterminada. Se recomienda agregar una máquina virtual de Linux de tooeach de memoria caché después de comprobar que no hay una memoria caché local ya.

Hay disponibles varios paquetes de almacenamiento en caché DNS, como dnsmasq. Estos son Hola pasos tooinstall dnsmasq en distribuciones de hello más comunes:

**Ubuntu (usa resolvconf)**
  * Instalar paquetes de saludo dnsmasq ("sudo instalación apt get dnsmasq").

**SUSE (usa netconf)**:
1. Instalar paquetes de saludo dnsmasq ("sudo zypper install dnsmasq").
2. Habilitar hello dnsmasq servicio ("systemctl enable dnsmasq.service").
3. Iniciar servicio de hello dnsmasq ("systemctl inicio dnsmasq.service").
4. Editar "/ etcetera/sysconfig/red/config" y cambiar NETCONFIG_DNS_FORWARDER = "" demasiado "dnsmasq".
5. Actualizar resolv.conf ("actualización de netconfig") tooset Hola caché como Hola a resolución DNS local.

**CentOS de Rogue Wave Software (anteriormente OpenLogic; usa NetworkManager)**
1. Instalar paquetes de saludo dnsmasq ("sudo yum install dnsmasq").
2. Habilitar hello dnsmasq servicio ("systemctl enable dnsmasq.service").
3. Iniciar servicio de hello dnsmasq ("systemctl inicio dnsmasq.service").
4. Agregar "anteponer servidores de nombres de dominio 127.0.0.1;" too"/etc/dhclient-eth0.conf".
5. Reinicie caché de Hola de tooset ("reinicio de red de servicio") del servicio de la red hello como Hola a resolución DNS local

> [!NOTE]
> : paquete de 'dnsmasq' hello es solo una de hello muchos DNS almacena en caché que están disponibles para Linux. Antes de usarlo, compruebe su idoneidad para sus necesidades y asegúrese de que no haya instalada ninguna otra memoria caché.
>
>

**Reintentos del cliente:**

DNS es principalmente un protocolo UDP. Dado que Hola protocolo UDP no garantiza la entrega de mensajes, Hola propio protocolo DNS controla lógica de reintento. Cada cliente DNS (sistema operativo) puede ofrecer una lógica de reintento diferentes según la preferencia del creador de hello:

* Los sistemas operativos Windows realizan un reintento tras un segundo y después tras otros dos, cuatro y otros cuatro segundos.
* Hola reintentos del programa de instalación de Linux de manera predeterminada después de cinco segundos.  Debe cambiar este tooretry cinco veces en intervalos de un segundo.  

toocheck Hola configuración actual en una máquina virtual de Linux, 'cat /etc/resolv.conf' y busque en línea de hello 'options', por ejemplo:

    options timeout:1 attempts:5

archivo de Hello resolv.conf generado automáticamente y no debe editarse. Hola pasos concretos que agregar hello 'options' línea varían según la distribución:

**Ubuntu** (usa resolvconf)
1. Agregar Hola opciones línea too'/etc/resolveconf/resolv.conf.d/head'.
2. Ejecute 'resolvconf -u' tooupdate.

**SUSE** (usa netconf)
1. Agregue 'timeout:1 intentos: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parámetro en '/ etcetera/sysconfig/red/config'.
2. Ejecute tooupdate 'netconfig update'.

**CentOS de Rogue Wave Software (anteriormente OpenLogic)** (usa NetworkManager)
1. Agregar too'/etc/NetworkManager/dispatcher.d/11-dhclient "eco" opciones timeout:1 intentos: 5"" '.
2. Ejecute tooupdate 'reinicio de la red de servicio'.

## <a name="name-resolution-using-your-own-dns-server"></a>Resolución de nombres mediante su propio servidor DNS
Sus necesidades de resolución de nombres pueden ir más allá de las características de Hola que proporciona Azure. Por ejemplo, puede necesitar resolución DNS entre redes virtuales. toocover este escenario, puede utilizar sus propios servidores DNS.  

Los servidores DNS de DNS reenviar consultas a toorecursive resoluciones de nombres de host de Azure tooresolve un puede red virtual que se encuentran en Hola misma red virtual. Por ejemplo, un servidor DNS que se ejecuta en Azure puede responder consultas tooDNS para su propio DNS archivos de la zona y reenvían todos los demás tooAzure de las consultas. Esta funcionalidad permite toosee de máquinas virtuales tanto las entradas de los archivos de zona y los nombres de host que Azure proporciona (a través de reenviador de hello). Solucionadores de recursiva toohello de acceso de Azure se proporciona a través de la dirección IP virtual de hello 168.63.129.16.

El reenvío de DNS también habilita la resolución DNS entre redes virtuales y permite que los nombres de host de tooresolve local de máquinas que proporciona Azure. tooresolve nombre de host de una máquina virtual, máquina virtual de hello DNS server debe residir en Hola misma red virtual y ser tooAzure de consultas de nombre de host tooforward configurado. Como sufijo DNS de hello es diferente en cada red virtual, puede utilizar el reenvío condicional reglas toosend DNS consulta toohello corregir una red virtual para la resolución. Hello siguiente imagen muestra dos redes virtuales y una red local realizar la resolución DNS entre redes virtuales con este método:

![Resolución DNS entre redes virtuales](./media/azure-dns/inter-vnet-dns.png)

Cuando se utiliza la resolución de nombres que proporciona Azure, sufijo DNS interno de Hola se proporciona tooeach virtual machine mediante DHCP. Cuando se usa su propia solución de resolución de nombre, este sufijo no es máquinas toovirtual proporcionado porque sufijo Hola interfiere con otras arquitecturas DNS. toorefer toomachines por FQDN o tooconfigure sufijo hello en sus máquinas virtuales, puede usar PowerShell o hello sufijo Hola de API toodetermine:

* Para redes virtuales que están administradas por el Administrador de recursos de Azure, está disponible a través de hello sufijo hello [tarjeta de interfaz de red](https://msdn.microsoft.com/library/azure/mt163668.aspx) recursos. También puede ejecutar hello `azure network public-ip show <resource group> <pip name>` comando detalles de hello toodisplay del IP pública, que incluye Hola FQDN de hello NIC.

Si el reenvío de las consultas tooAzure no se ajusta a sus necesidades, deberá tooprovide su propia solución DNS.  La solución DNS debe:

* Proporcionar la resolución adecuada de nombres de host, por ejemplo, mediante [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Si usas DDNS, tendrá que la limpieza de registros DNS de toodisable. Las concesiones DHCP de Azure son muy largas y la limpieza puede eliminar registros DNS de forma prematura.
* Proporcionar resolución recursiva adecuado de tooallow de resolución de nombres de dominio externos.
* Estar accesible (TCP y UDP en el puerto 53) de los clientes de hello atienda y estar hello tooaccess capaz de Internet.
* Protegerse contra el acceso hello toomitigate las amenazas de Internet que suponen los agentes externos.

> [!NOTE]
> Para obtener el mejor rendimiento, cuando se usa máquinas virtuales en los servidores DNS de Azure, deshabilitar IPv6 y asignar un [IP pública a nivel de instancia](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS servidor virtual machine.  
>
>
