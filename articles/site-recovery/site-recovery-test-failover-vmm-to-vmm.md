---
title: "aaaTest conmutación por error (tooVMM VMM) en Azure Site Recovery | Documentos de Microsoft"
description: "Azure Site Recovery coordina la replicación de hello, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Obtenga información acerca de la conmutación por error tooAzure o un centro de datos secundaria."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Probar la conmutación por error (tooVMM VMM) en Site Recovery


En este artículo se proporcionan información e instrucciones para realizar una conmutación por error de prueba o una exploración de recuperación ante desastres de máquinas virtuales y servidores físicos protegidos con Azure Site Recovery. Deberá usar un sitio administrado de System Center Virtual Machine Manager VMM local como sitio de recuperación de Hola.

Ejecutar un toovalidate de conmutación por error de prueba de la estrategia de replicación o realizar una exploración de recuperación ante desastres sin pérdida de datos o el tiempo de inactividad. Una prueba de conmutación por error no tiene ningún efecto en la replicación en curso de Hola o en el entorno de producción. Puede ejecutarla en una máquina virtual o en un [plan de recuperación](site-recovery-create-recovery-plans.md). Cuando está desencadenan una conmutación por error de prueba, es necesario red de hello toospecify que va a conectar máquinas virtuales de prueba de Hola. Puede realizar el seguimiento del progreso de Hola de conmutación por error de prueba de hello en hello **trabajos** página.  

Si tiene comentarios o preguntas, publique lo que necesite en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Preparar la infraestructura de Hola para conmutación por error de prueba
Si desea toorun una conmutación por error de prueba mediante el uso de una red existente, prepare Active Directory, DHCP y DNS en esa red.

Si desea toorun una conmutación por error de prueba mediante el uso de redes de VM de hello opción toocreate automáticamente, agregue un paso manual antes del grupo 1 Hola plan de recuperación que se vayan toouse para conmutación por error de prueba de Hola. A continuación, agregue toohello de recursos de infraestructura de hello creado automáticamente la red antes de ejecutar la conmutación por error de prueba de Hola.

### <a name="things-toonote"></a>Cosas toonote
Cuando se está replicando tooa sitio secundario, tipo de Hola de red que Hola réplica máquina usa no tiene tipo de hello toomatch de red lógica que usa para la conmutación por error, pero puede que algunas combinaciones no funcionen. Si la réplica de hello usa DHCP y el aislamiento basado en VLAN, red VM de Hola para réplica de hello no necesita un grupo de direcciones IP estáticas. Por lo que usar virtualización de red de Windows para la conmutación por error de prueba de hello no funcionará porque no hay disponible ningún grupo de direcciones. 

Además, Hola conmutación por error no funcionará si la red de réplica de hello no utiliza aislamiento y red de prueba de hello usa virtualización de red de Windows. Esto es porque la red sin aislamiento de hello no tiene Hola subredes necesario toocreate una red de virtualización de red de Windows.

Cómo máquinas virtuales de réplica son redes de VM conectados toomapped después de conmutación por error depende de la configuración de red VM de hello en la consola VMM Hola.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Red de máquinas virtuales configurada sin aislamiento o con aislamiento de VLAN
Si DHCP está definido para la red VM de hello, máquina virtual de réplica de hello es conectado toohello Id. de VLAN mediante la herramienta Configuración Hola que se especifican para el sitio de red de hello en red lógica asociada de Hola. máquina virtual de Hello recibe su dirección IP de servidor DHCP disponible de Hola. 

No es necesario toodefine un grupo de direcciones IP estáticas para red de máquina virtual de destino de Hola. Si se utiliza un grupo de direcciones IP estáticas para red de VM de hello, máquina virtual de réplica de hello es conectado toohello Id. de VLAN mediante la herramienta Configuración Hola que se especifican para el sitio de red de hello en red lógica asociada de Hola.

máquina virtual de Hello recibe su dirección IP de grupo de Hola que se define para la red de VM de Hola. Si un grupo de direcciones IP estáticas no está definido en la red de VM de destino de hello, se producirá un error en la asignación de direcciones IP. Crear grupo de direcciones IP de hello en los servidores VMM de origen y destino de Hola que va a utilizar para la protección y recuperación.

#### <a name="vm-network-with-windows-network-virtualization"></a>Red de máquinas virtuales con virtualización de red de Windows
Si se configura una red de VM con virtualización de red de Windows, debe definir un grupo estático para red de VM de destino de hello, independientemente de si la red de VM de origen de hello es toouse configurado DHCP o un grupo de direcciones IP estáticas. 

Si define DHCP, servidor VMM de destino de hello actúa como un servidor DHCP y proporciona una dirección IP del grupo de Hola que se define para red de VM de destino de Hola. Si se define el uso de un grupo de direcciones IP estáticas para el servidor de origen de hello, servidor VMM de destino de hello asigna una dirección IP del grupo de Hola. En ambos casos, se producirá un error en la asignación de direcciones IP si no se define un grupo de direcciones IP estáticas.


### <a name="prepare-dhcp"></a>Preparación de DHCP
Si las máquinas virtuales Hola participa en la conmutación por error de prueba usan DHCP, cree un servidor DHCP de prueba dentro de la red aislada de hello para el propósito de Hola de conmutación por error de prueba.

### <a name="prepare-active-directory"></a>Preparación de Active Directory
toorun una conmutación por error de prueba para probar la aplicación, necesitará una copia del entorno de Active Directory de producción de hello en el entorno de prueba. Para obtener más información, consulte hello [consideraciones de conmutación por error para Active Directory de prueba](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>Preparación de DNS
Prepare un servidor DNS para la conmutación por error de prueba de hello como sigue:

* **DHCP**: si máquinas virtuales usan DHCP, dirección IP de Hola de prueba de hello DNS debe actualizarse en el servidor DHCP de prueba de Hola. Si usa un tipo de red de virtualización de red de Windows, servidor VMM Hola actúa como servidor DHCP de Hola. Por lo tanto, la dirección IP de Hola de DNS debe actualizarse en red de conmutación por error de prueba de Hola. En este caso, las máquinas virtuales Hola registran servidor DNS que corresponda toohello.
* **Dirección estática**: si las máquinas virtuales utilizan una dirección IP estática, Hola dirección IP del servidor DNS debe actualizarse en la red de prueba de conmutación por error de prueba de Hola. Puede que tenga tooupdate DNS con la dirección IP de Hola de máquinas virtuales de prueba de Hola. Puede usar Hola siguiente secuencia de comandos de ejemplo para este propósito:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
Este procedimiento describe cómo toorun una conmutación por error de prueba para una recuperación del plan. Como alternativa, puede ejecutar Hola conmutación por error para una sola máquina virtual en hello **máquinas virtuales** ficha.

![Hoja de la conmutación por error de prueba](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Seleccione **Recovery Plans** > *nombreDePlanDeRecuperación*. Haga clic en **Conmutación por error** > **Test Conmutación por error**.
1. En hello **probar conmutación por error** hoja, especifique cómo máquinas virtuales deben estar conectados toonetworks después de la conmutación por error de prueba de Hola. Para obtener más información, vea hello [opciones de red](#network-options-in-site-recovery).
1. Realizar el seguimiento de progreso de la conmutación por error en hello **trabajos** ficha.
1. Una vez completada la conmutación por error, compruebe que las máquinas virtuales de Hola se inician correctamente.
1. Cuando haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Este paso elimina hello las máquinas virtuales y redes que se crearon durante la conmutación por error de prueba.


## <a name="network-options-in-site-recovery"></a>Opciones de red en Site Recovery

Cuando se ejecuta una prueba de conmutación por error, se le pide tooselect de configuración de red de máquinas de réplica de prueba. Existen varias opciones.  

| **Opción de conmutación por error de prueba** | **Descripción** | **Verificación de la conmutación por error** | **Detalles** |
| --- | --- | --- | --- |
| **Conmutar por sitio VMM secundario tooa--sin red** |No seleccione una red de máquinas virtuales. |La conmutación por error comprueba que se crean las máquinas de prueba.<br/><br/>máquina virtual de prueba de Hola se crea en el host de Hola donde existe la máquina virtual de réplica de Hola. No se agrega en la nube toohello donde se encuentra la máquina virtual de réplica de Hola. |<p>Hola se conmutó por error máquina no se encuentra conectado tooany red.<br/><br/>equipo de Hello puede ser red de VM conectados tooa después de que se ha creado. |
| **Conmutar por sitio VMM secundario tooa--con la red** |Seleccione una red de máquinas virtuales existente. |La conmutación por error comprueba que se crean las máquinas virtuales. |máquina virtual de prueba de Hola se crea en el host de Hola donde existe la máquina virtual de réplica de Hola. No se agrega en la nube toohello donde se encuentra la máquina virtual de réplica de Hola.<br/><br/>Cree una red de máquinas virtuales aislada de la red de producción.<br/><br/>Si utiliza una red basada en VLAN, se recomienda crear una red lógica independiente en VMM para este propósito (no se utiliza en producción). Esta red lógica es redes de VM toocreate usado para las conmutaciones por error de prueba.<br/><br/>red lógica Hola debe asociarse con al menos uno de los adaptadores de red de Hola de todos los servidores de Hyper-V de Hola que hospedan máquinas virtuales.<br/><br/>Para redes lógicas de VLAN, Hola sitios de red que agregue la red lógica toohello debe estar aislado.<br/><br/>Si utiliza una red lógica basada en virtualización de red de Windows, Azure Site Recovery crea automáticamente redes de máquinas virtuales aisladas. |
| **Producirá un error con el sitio VMM secundario tooa--crear una red** |Se crea automáticamente en función de la configuración de Hola que especifique en una red de prueba temporal **red lógica** y sus sitios de red relacionados. |La conmutación por error comprueba que se crean las máquinas virtuales. |Utilice esta opción si el plan de recuperación de hello usa más de una red de máquina virtual. Si usa redes de virtualización de red de Windows, esta opción puede crear automáticamente redes de VM con hello misma configuración (las subredes y grupos de direcciones IP) de red de Hola Hola máquina virtual de réplica. Estas redes VM se limpian automáticamente una vez completada la conmutación por error de prueba de Hola.</p><p>máquina virtual de prueba de Hola se crea en el host de Hola donde existe la máquina virtual de réplica de Hola. No se agrega en la nube toohello donde se encuentra la máquina virtual de réplica de Hola. |

> [!TIP]
> dirección IP asignada a tooa virtual máquina durante la conmutación por error de prueba Hello es hello misma dirección IP que Hola máquina virtual recibiría una planeada o no planeada conmutación por error (suponiendo que la dirección IP de hello está disponible en la red de conmutación por error de prueba de hello). Si hello misma dirección IP no está disponible en la red de conmutación por error de prueba de hello, máquina virtual de hello recibe otra dirección IP que está disponible en la red de conmutación por error de prueba de Hola.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Red de producción de tooa de conmutación por error de prueba en un sitio de recuperación
Se recomienda que, al realizar una conmutación por error de prueba, elija una red diferente de la del sitio de recuperación de producción que proporcionara en la [asignación de red](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Pero si realmente desea toovalidate conectividad de red de extremo a extremo en una máquina virtual de se conmutó por error, tenga en cuenta Hola siguientes puntos:

* Asegúrese de que la máquina virtual principal Hola se apaga cuando se está realizando la conmutación por error de prueba de Hola. Si no lo hace, dos máquinas virtuales con hello misma identidad se ejecutará en hello igual de red en Hola mismo tiempo. Esta situación puede provocar tooundesired consecuencias.
* Los cambios que realice toohello máquinas virtuales de conmutación por error de prueba se pierden al limpiar Hola probar conmutación por error las máquinas virtuales. Estos cambios no son máquina virtual principal de toohello atrás replicada.
* Esta manera de hacer las pruebas toodowntime de clientes potenciales para la aplicación de producción. Pedir a los usuarios de la aplicación hello no toouse aplicación de hello cuando Hola DR explorar está en curso.  


## <a name="next-steps"></a>Pasos siguientes
Después de ejecutar correctamente una conmutación por error de prueba, puede intentar una [conmutación por error](site-recovery-failover.md).
