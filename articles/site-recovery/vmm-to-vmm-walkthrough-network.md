---
title: "aaaPlan de red de Hyper-V replicación tooa VMM sitio secundario con Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo describe la planeación de una red al replicar las máquinas virtuales de Hyper-V tooa secundaria sitio de System Center VMM con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Paso 3: Planear la red para el sitio VMM secundario de tooa de replicación de máquina virtual de Hyper-V

Después de revisar los requisitos previos de implementación, lea este tooplan artículo redes al replicar Hyper-v. las máquinas virtuales (VM) administradas en nubes de System Center Virtual Machine Manager (VMM), uso de sitio secundario de tooa [deAzureSiteRecovery](site-recovery-overview.md) Hola portal de Azure. 

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Información general de asignación de red

Asignación de red se utiliza al replicar el centro de datos secundario tooa de máquinas virtuales de Hyper-V (que se administren en VMM). La asignación de red se produce entre redes de máquinas virtuales en un servidor VMM de origen y redes de máquinas virtuales en un servidor VMM de destino. Asignación Hola siguientes:

- **Conexión de red**: redes de máquinas virtuales se conecta tooappropriate después de la conmutación por error. VM de réplica de Hello será toohello conectado red de destino que está asignada toohello red de origen.
- **Una ubicación óptima**: óptimamente lugares Hola máquinas virtuales de réplica en los servidores de host de Hyper-V. Máquinas virtuales de réplica se colocan en hosts que pueden asignar Hola de acceso a redes de máquinas virtuales.
- **Ninguna asignación de red**: si no configura la asignación de red, las máquinas virtuales de réplica no estará conectado tooany redes de máquinas virtuales después de la conmutación por error.


### <a name="example"></a>Ejemplo

Este es un ejemplo tooillustrate este mecanismo. Vamos a utilizar una organización con dos ubicaciones en Nueva York y Chicago.

**Ubicación** | **Servidor VMM** | **Redes de máquinas virtuales** | **Asignado a**
---|---|---|---
Nueva York | VMM-NewYork| VMNetwork1-NewYork | TooVMNetwork1-Chicago asignada
 |  | VMNetwork2-NewYork | No asignado
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork asignada
 | | VMNetwork1-Chicago | No asignado

En este ejemplo:

- Cuando se crea una máquina virtual de réplica para cualquier máquina virtual que está conectado tooVMNetwork1-NewYork, estará conectado tooVMNetwork1-Chicago.
- Cuando se crea una máquina virtual de réplica para VMNetwork2-NewYork o VMNetwork2-Chicago, no estará conectada tooany red.

Aquí es cómo se configuran las nubes de VMM en nuestra organización de ejemplo y redes lógicas Hola asociadas a nubes de Hola.

#### <a name="cloud-protection-settings"></a>Configuración de la protección de la nube

**Nube protegida** | **Proteger nube** | **Red lógica (Nueva York)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Configuración de la red lógica y máquinas virtuales

**Ubicación** | **Red lógica** | **Red de VM asociada**
---|---|---
Nueva York | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Configuración de red de destino

Según estos valores, al seleccionar red de VM de destino de hello, hello en la tabla siguiente muestra las opciones de Hola que estarán disponibles.

**Selección** | **Nube protegida** | **Proteger nube** | **Red de destino disponible**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponible
 | GoldCloud1 | GoldCloud2 | Disponible
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | No disponible
 | GoldCloud1 | GoldCloud2 | Disponible


Si la red de destino de hello tiene varias subredes y una de dichas subredes tiene Hola mismo nombre como Hola subred en qué Hola máquina virtual de origen se encuentra, a continuación, Hola máquina virtual de réplica será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.


#### <a name="failback-behavior"></a>Comportamiento de conmutación por recuperación

toosee lo que ocurre en el caso de hello de conmutación por recuperación (replicación inversa), vamos a suponer que VMNetwork1-NewYork está asignada tooVMNetwork1-Chicago, con hello después de la configuración.


**Máquina virtual** | **Red tooVM conectado**
---|---
VM1 | VMNetwork1-Network
VM2 (réplica de VM1) | VMNetwork1-Chicago

Con esta configuración, revisemos lo que ocurre en un par de escenarios posibles.

**Escenario** | **Resultado**
---|---
Ningún cambio hello en Propiedades de red de VM-2 después de la conmutación por error. | VM-1 permanece conectado toohello red de origen.
Las propiedades de red de VM-2 cambian después de la conmutación por error y está desconectada. | VM-1 se desconecta.
Propiedades de red de VM-2 cambian después de la conmutación por error y está conectado tooVMNetwork2-Chicago. | Si no está asignada VMNetwork2-Chicago, se desconectará VM-1.
Se cambia la asignación de redes de VMNetwork1-Chicago. | VM-1 será toohello conectado red ahora asignada tooVMNetwork1-Chicago.



## <a name="prepare-for-network-mapping"></a>Preparar la asignación de red

1. En los servidores VMM de origen y destino hello, debe tener una red lógica asociada con nubes de origen y destino de Hola. 
2. En servidores de origen y destino de hello, debe tener una red lógica de VM red toohello vinculado.
3. Máquinas virtuales en hosts de Hyper-V en la ubicación de origen de hello deben estar vinculados toohello red de VM de origen. Si solo usa un único servidor VMM, puede configurar la asignación entre redes de VM de hello mismo servidor.

Esto es lo que sucede al configurar la asignación de red durante la implementación de Site Recovery:

- Al configurar la asignación de red y seleccionar una red de máquina virtual de destino, nubes de origen VMM de Hola que usan la red de VM de origen Hola se mostrarán junto con redes de VM de destino disponibles de hello en nubes de destino de Hola.
- - Cuando se configura correctamente la asignación y está habilitada la replicación, un origen de máquina virtual estará conectado tooits red de VM de origen y se conectará su réplica en la ubicación de destino de hello tooits asignar red de máquina virtual.
- Si la red de destino de hello tiene varias subredes y una de dichas subredes tiene Hola mismo nombre como Hola subred en qué Hola máquina virtual de origen se encuentra, a continuación, Hola máquina virtual de réplica será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, Hola VM estará conectado toohello primera subred de red de Hola.

## <a name="connect-toovms-after-failover"></a>Conectarse tooVMs después de la conmutación por error

Al planear su estrategia de conmutación por error y replicación, uno de preguntas clave hello es cómo tooconnect toohello réplica después de la conmutación por error. Hay dos opciones: 

- **Usar una dirección IP diferente**: se puede seleccionar toouse una dirección IP diferente para hello replica la máquina virtual. En este Hola escenario VM Obtiene una nueva dirección IP después de la conmutación por error y se requiere una actualización DNS.
- **Conservar Hola la misma dirección IP**: es recomendable toouse Hola la misma dirección IP para VM de réplica de Hola. Mantener Hola simplifica la mismas direcciones IP recuperación Hola al reducir los problemas de red después de la conmutación por error. 

## <a name="retain-ip-addresses"></a>Conservación de las direcciones IP

Si desea que las direcciones IP de tooretain Hola desde el sitio primario de hello después de sitio secundario de conmutación por error toohello, puede realizar una conmutación por error de subred completa y actualizar rutas tooindicate Hola nueva ubicación de direcciones IP de Hola o alternativa implementar una subred con Stretch entre Hola principal y Hola sitios de recuperación.

### <a name="stretched-subnet"></a>Subred estirada

En una subred con Stretch, subred Hola está disponible al mismo tiempo en el sitio principal y secundaria de Hola. Si mueve un servidor y su sitio secundario de IP (nivel 3) configuración toohello, red Hola enrutará nueva ubicación de hello tráfico toohello automáticamente. 

Desde una perspectiva del nivel 2 (nivel de vínculo de datos), necesita un equipo de redes que pueda administrar una red VLAN estirada. Además, por hello ampliar VLAN, dominio de error posibles Hola extiende sitios tooboth, básicamente se convierta en un único punto de error. Aunque es poco probable, podría ocurrir que se iniciara una tormenta de difusión y no se pudiera aislar. 


### <a name="subnet-failover"></a>Conmutación por error de subred

Puede ejecutar un hello tooobtain de conmutación por error de subred ventajas de subred de hello ajustarse, sin realmente la ampliación. En esta solución, una subred estará disponible en el sitio de origen o destino de hello, pero no en ambos al mismo tiempo. toomaintain Hola espacio de direcciones IP en el caso de hello de una conmutación por error, se pueden organizar mediante programación para subredes Hola enrutador infraestructura toomove Hola de tooanother de un sitio. Una vez cuando se produce conmutación por error, subredes pasaban con hello había asociado las máquinas virtuales. Hola principal inconveniente es que en caso de hello de un error, tienes subred completa de toomove Hola.

### <a name="example"></a>Ejemplo

Este es un ejemplo de conmutación por error de la subred completa. sitio primario de Hello tiene aplicaciones que se ejecutan en la subred 192.168.1.0/24. En la conmutación por error, Hola todas las máquinas virtuales en esta subred se conmutan por sitio secundario toohello y conservan sus direcciones IP. Rutas necesidad toobe modifica hechos de hello tooreflect que todas las máquinas de virtuales VM de Hola que pertenecen toosubnet 192.168.1.0/24 ahora se han movido toohello de sitio secundario.

Hello gráficos siguientes muestran subredes Hola antes y después de la conmutación por error:

- Antes de la conmutación por error, subred 192.168.0.1/24 está activo en el sitio de origen Hola activarse en el sitio secundario de hello después de la conmutación por error.
- Hola enruta entre sitio primario y sitio de recuperación, tercer sitio y el sitio primario y sitio terceros y el sitio de recuperación tendrá toobe modificado correctamente.

**Antes de la conmutación por error**

![Antes de la conmutación por error](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Después de la conmutación por error**

![Después de la conmutación por error](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Después de la conmutación por error, esto es lo que sucede:

- Recuperación del sitio asigna una dirección IP para cada interfaz de red en Hola de máquina virtual, del grupo de direcciones IP estática de hello en red relevantes de hello, para cada instancia VMM.
- Si es el grupo de direcciones IP de hello en el sitio secundario de Hola Hola igual que en el sitio de origen de hello, Site Recovery asigna Hola misma réplica de toohello de dirección (de hello una VM de origen) de IP virtual. dirección IP de Hello está reservada en VMM, pero no está configurada como dirección IP de conmutación por error de hello en el host de Hyper-V de Hola. dirección IP de conmutación por error de Hello en un host de Hyper-v se establece justo antes de la conmutación por error de Hola.
- Si hello misma dirección IP no está disponible, Site Recovery asigna otra dirección IP disponible de grupo de Hola.
- Si las máquinas virtuales usan DHCP, Site Recovery no administrar direcciones IP de Hola. Necesita toocheck que Hola DHCP server en el sitio secundario de hello puede asignar la dirección de hello mismo intervalo como sitio de origen de Hola.

### <a name="validate-hello-ip-address"></a>Validar la dirección IP de Hola

Después de habilitar la protección de una máquina virtual, puede usar los siguientes ejemplo script tooverify hello dirección asignada toohello máquina virtual. Hola la misma dirección IP se establezca como dirección IP de conmutación por error de Hola y se asignó toohello VM en tiempo de Hola de conmutación por error:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Cambio de las direcciones IP

En este escenario, se cambian las direcciones IP Hola de máquinas virtuales que conmutarán por error. desventaja de Hola de esta solución es requerido el mantenimiento de Hola. Normalmente, DNS se actualizará una vez iniciadas las máquinas virtuales de réplica. Las entradas de DNS podrían necesita toobe cambiado o fluster en red y las entradas en caché actualizadas. Esto puede dar lugar a un tiempo de inactividad. El tiempo de inactividad puede mitigarse del siguiente modo:

- Utilice valores de TTL bajos para las aplicaciones de intranet.
- Usar hello siguiente secuencia de comandos en un plan de recuperación de Site Recovery, tooupdate Hola DNS server tooensure oportuna actualización. Script de Hola no es necesario si utiliza el registro DNS dinámico.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Ejemplo 

Echemos un vistazo a un escenario en el que piensa toouse direcciones IP a través de hello principal y los sitios de recuperación de Hola. En este ejemplo contamos con direcciones IP a través de sitios primarios y secundarios, y existe; se puede tener acceso a sitio s una tercera de las aplicaciones hospedadas en el sitio principal o de recuperación de Hola.

- Antes de la conmutación por error, aplicaciones son 192.168.1.0/24 subred hospedado en el sitio principal de Hola y están toobe configurado en la subred 172.16.1.0/24 en el sitio secundario de hello después de una conmutación por error.
- Las rutas de red/conexiones de VPN se han configurado correctamente de forma que los tres sitios son accesibles entre sí.
- Después de la conmutación por error, las aplicaciones se restaurará en la subred de la recuperación de Hola. En este escenario no hay ninguna necesidad de toofail por subred todo Hola y rutas de red o VPN tooreconfigure necesarios no es ningún cambio. conmutación por error de Hola y algunas actualizaciones DNS, aseguran de que las aplicaciones sean accesibles.
- Si DNS no está configurado tooallow de actualizaciones dinámicas, a continuación, hello las máquinas virtuales se registrarán con hello nueva dirección IP, cuando se inician después de la conmutación por error.

**Antes de la conmutación por error**

![Otra dirección IP: antes de la conmutación por error](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Después de la conmutación por error**

![Otra dirección IP: después de la conmutación por error](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 4: preparar VMM y Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


