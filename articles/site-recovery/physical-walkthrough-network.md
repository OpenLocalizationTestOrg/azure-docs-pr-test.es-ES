---
title: "aaaPlan de red de servidor físico replicación tooAzure | Documentos de Microsoft"
description: "Este artículo describe la planeación de una red requiere al replicar servidores físicos tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 71db2435-b5ce-4263-83f6-093d10d1d4e1
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e2ca2db2a1cb58ca5468d4ee2b0406f29ff09479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-physical-server-replication-tooazure"></a>Paso 4: Planificación de redes para tooAzure de replicación del servidor físico

En este artículo se resume red planificación de consideraciones al replicar locales tooAzure servidores físicos con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connect-tooreplica-azure-vms"></a>Conectar máquinas virtuales de Azure tooreplica

Al planear su estrategia de conmutación por error y replicación, uno de preguntas clave hello es cómo tooconnect toohello máquina virtual de Azure después de la conmutación por error. Hay un par de opciones al diseñar la estrategia de red para máquinas virtuales de réplica de Azure:

- **Usar una dirección IP diferente**: se puede seleccionar toouse un intervalo de direcciones IP diferente para saludo replica red de VM de Azure. En este escenario, la máquina de hello tiene una nueva dirección IP después de conmutación por error y actualización de DNS es necesario.
- **Use Hola misma dirección IP**: es recomendable toouse Hola mismo intervalo de direcciones IP que en el sitio local principal, para hello Azure red después de la conmutación por error. Mantener Hola simplifica la mismas direcciones IP recuperación Hola al reducir los problemas de red después de la conmutación por error. Sin embargo, cuando se está replicando tooAzure, necesitará tooupdate rutas con la nueva ubicación de direcciones IP de Hola de hello después de la conmutación por error.

## <a name="retain-ip-addresses"></a>Conservación de las direcciones IP

Recuperación de sitio proporciona las direcciones IP de hello capacidad tooretain fijada cuando se conmuta tooAzure, con una subred de conmutación por error.
Con la conmutación por error de subredes, una subred específica está presente en el sitio 1 o en el sitio 2, pero nunca en ambos sitios simultáneamente. En orden toomaintain Hola espacio de direcciones IP en el caso de hello de una conmutación por error, mediante programación se encargará de subredes de Hola Hola enrutador infraestructura toomove de tooanother de un sitio. Durante la conmutación por error, movimiento de subredes de hello con hello había asociado máquinas virtuales protegidas. Hola principal inconveniente es que en caso de hello de un error, tienes subred completa de toomove Hola.

### <a name="failover-example"></a>Ejemplo de conmutación por error

Veamos un ejemplo de tooAzure de conmutación por error.

- Una compañía ficticia, Woodgrove Bank, tiene una infraestructura local que hospeda sus aplicaciones empresariales. Las aplicaciones móviles se hospedan en Azure.
- Una conexión de sitio a sitio (VPN) entre hello red virtual de Azure y la red perimetral de hello local proporciona conectividad entre las máquinas virtuales de Woodgrove Bank en servidores Azure y local.
- Esto significa que VPN que Hola red virtual de la compañía en Azure aparece como una extensión de su red local.
- Woodgrove desea toouse Site Recovery tooreplicate local las cargas de trabajo tooAzure.
 - Woodgrove tiene toodeal con aplicaciones y configuraciones que dependen de las direcciones IP codificado de forma rígida y, por tanto, necesitan tooretain las direcciones IP para sus aplicaciones después de la conmutación por error tooAzure.
 - Woodgrove asigna direcciones IP desde intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos que se ejecutan en Azure.


Woodgrove toobe capaz de tooreplicate su tooAzure de servidores mientras conserva Hola IP direcciones, aquí es qué compañía Hola necesita toodo:

1. Cree una red virtual de Azure. Debe ser una extensión de hello red local para que las aplicaciones puedan conmutarse por error sin problemas.
2. Azure permite tooadd sitio a sitio VPN conectividad, además conectividad de sitio de toopoint toohello las redes virtuales creadas en Azure.
3. Al configurar la conexión de sitio a sitio hello, en hello Azure de red, puede enrutar tráfico toohello ubicación (red local) solo si el intervalo de direcciones IP de hello es diferente de intervalo de direcciones IP de hello en local.
    - Esto se debe a que Azure no admite subredes estiradas. Por lo que si tiene subred 192.168.1.0/24 local, no se puede agregar una red local 192.168.1.0/24 Hola red de Azure.
    - Esto es lo esperado porque Azure no sabe que no hay ninguna máquina activada en la subred de Hola y esa subred Hola se está creando para solo la recuperación ante desastres.
    - toobe toocorrectly puede redirigir el tráfico de red fuera de un subredes hello Azure en red de Hola y Hola de red local no debe entrar en conflicto.

![Antes de la conmutación por error de la subred](./media/physical-walkthrough-network/network-design7.png)

#### <a name="before-failover"></a>Antes de la conmutación por error

1. Cree una red adicional (por ejemplo, una red de recuperación). Se trata de red de hello en el que no se pudo a máquinas virtuales se crean.
2. tooensure que Hola dirección IP para una máquina se conserva después de una conmutación por error, en Propiedades de la máquina de hello > **configurar**, especifique Hola misma dirección IP que Hola server tiene en el servidor local y haga clic en **guardar**.
3. Cuando se conmuta máquina hello, Azure Site Recovery asignará Hola proporcionada tooit de dirección IP.
4. Una vez se activa el desencadenador y hello las máquinas virtuales se crean en Azure con la dirección IP de hello necesario conmutación por error, puede conectarse toohello de red mediante un [conexión de red virtual tooVnet](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Esta acción puede ejecutarse mediante scripts.
5. Rutas necesitan toobe modificado de forma adecuada, tooreflect ese 192.168.1.0/24 ahora se movió tooAzure.

    ![Después de la conmutación por error de la subred](./media/physical-walkthrough-network/network-design9.png)

#### <a name="after-failover"></a>Después de la conmutación por error

Si no dispone de una red Azure tal y como se ilustra arriba, puede crear una conexión de VPN de sitio a sitio entre el sitio primario y Azure después de la conmutación por error.

## <a name="change-ip-addresses"></a>Cambiar las direcciones IP

Esto [entrada de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica cómo aborda tooset seguridad hello Azure infraestructura de red cuando no se necesitan tooretain IP después de la conmutación por error. Empieza con una descripción de la aplicación, se centra en cómo tooset la red local y en Azure y concluye con información sobre la ejecución de las conmutaciones por error.  

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 5: preparar Azure](physical-walkthrough-prepare-azure.md)
