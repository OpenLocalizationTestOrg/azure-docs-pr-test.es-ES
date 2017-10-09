---
title: aaaService tejido tipos de nodos y conjuntos de escalas de VM | Documentos de Microsoft
description: "Describe cómo los tipos de nodos de Service Fabric se relacionan con los conjuntos de escalas de tooVM y cómo se conectan tooremote tooa instancia de conjunto de escalado de VM o un nodo de clúster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>relación de Hello entre tipos de nodos de Service Fabric y conjuntos de escalas de máquina Virtual
Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure puede usar toodeploy y administrar una colección de máquinas virtuales como un conjunto. Cada tipo de nodo que se define en un clúster de Service Fabric está configurado como un conjunto de escalado de VM independiente. Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.

Hola siguiente captura de pantalla muestra un clúster que tiene dos tipos de nodo: front-end y back-end.  A su vez, cada tipo de nodo tiene cinco nodos.

![Captura de pantalla de un clúster que tiene dos tipos de nodos][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Asignación toonodes de instancias de conjunto de escala de VM.
Como puede ver anteriormente, Hola conjunto de escalado de máquinas virtuales se inician las instancias de la instancia 0 y, a continuación, aumenta. Hola numeración se refleja en los nombres de Hola. Por ejemplo, BackEnd_0 es instancia 0 de hello conjunto de escalado de la máquina virtual de back-end. En concreto, este conjunto de escalado de máquinas virtuales tiene cinco instancias, denominadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 y BackEnd_4.

Al escalar verticalmente un conjunto de escalado de máquinas virtuales, se crea una nueva instancia. Hola nuevo conjunto de escalado de VM nombre de instancia normalmente será el nombre de conjunto de escalado de VM de hello + número de instancia siguiente de Hola. En nuestro ejemplo, es BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Asignación de máquina virtual conjunto de escalas de carga equilibradores tooeach nodo tipo/VM conjunto de escala
Si ha implementado el clúster desde el portal de Hola o ha usado la plantilla de administrador de recursos de ejemplo de Hola que se proporciona, a continuación, cuando se obtiene una lista de todos los recursos en un grupo de recursos verá equilibradores de carga de Hola para cada tipo de nodo o conjunto de escalado de máquinas virtuales.

Hello nombre sería algo parecido a: **LB -&lt;NodeType nombre&gt;**. Por ejemplo, LB-sfcluster4doc-0, como se muestra en esta captura de pantalla:

![Recursos][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Instancia de conjunto de escalado de VM de tooa o un nodo de clúster de conexión remota
Cada tipo de nodo que se define en un clúster está configurado como un conjunto de escalado de VM independiente.  Que significa Hola tipos de nodo se puede escalar una copia de seguridad o el detalle de forma independiente y se pueden realizar de diferentes SKU de máquina virtual. A diferencia de las máquinas virtuales de instancia única, instancias de conjunto de escalado de VM de hello no obtiene una dirección IP virtual por sí mismos. Por lo que puede ser un poco complicado cuando se desea obtener una dirección IP dirección y el puerto que se puede usar tooremote conectan instancia específica de tooa.

Estos son los pasos de hello puede seguir toodiscover ellos.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Paso 1: Obtener dirección IP virtual de hello para el tipo de nodo de hello y, a continuación, las reglas de NAT de entrada para RDP
En tooget orden esto, necesita tooget Hola NAT de entrada de reglas de valores que se definieron como parte de la definición de recursos de Hola para **Microsoft.Network/loadBalancers**.

En el portal de hello, navegar por hoja de equilibrador de carga de toohello y, a continuación, **configuración**.

![LBBlade][LBBlade]

En **Configuración**, haga clic en **Reglas NAT de entrada**. Ahora Esto proporciona Hola dirección IP y puerto que se puede usar tooremote conectar toohello primera instancia del conjunto de escalado de máquinas virtuales. En la siguiente captura de pantalla de hello, es **104.42.106.156** y **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Paso 2: Obtenga más información sobre el puerto de Hola que puede usar tooremote conexión toohello conjunto de escalado de VM instancia/nodo específico
Anteriormente en este documento, describe cómo asignan los nodos toohello en instancias de conjunto de escalado de VM de Hola. Se usará ese toofigure puerto exacto de Hola de salida.

puertos de Hola se asignan en orden ascendente de instancia de conjunto de escalado de VM de Hola. por lo que en el ejemplo de Hola tipo de nodo de front-end, puertos de Hola para cada una de las cinco instancias de hello son siguiente Hola. Ahora necesita toodo Hola misma asignación para la instancia del conjunto de escalado de máquinas virtuales.

| **Instancia de conjunto de escalado de VM** | **Puerto** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Paso 3: Instancia de conjunto de escalado de VM de toohello específica de conexión remota
En la siguiente captura de pantalla de hello Usar conexión a Escritorio remoto tooconnect toohello FrontEnd_1:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Hola toochange puerto RDP cómo los valores de intervalo
### <a name="before-cluster-deployment"></a>Antes de la implementación del clúster
Cuando se configura usando una plantilla de administrador de recursos de clúster de hello, puede especificar el intervalo de Hola Hola **inboundNatPools**.

Ir a definición de recursos de toohello para **Microsoft.Network/loadBalancers**. En la que buscar descripción Hola para **inboundNatPools**.  Reemplace hello *frontendPortRangeStart* y *frontendPortRangeEnd* valores.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Después de la implementación del clúster
Esto es un poco más complicada y podría resultar en máquinas virtuales de Hola que se reciclen. Ahora tienes tooset nuevos valores mediante Azure PowerShell. Asegúrese de que Azure PowerShell 1.0 esté instalado en su equipo (o una versión posterior). Si no ha hecho esto antes, es recomendable que siga los pasos de Hola que se describen en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)

Inicie sesión en tooyour cuenta de Azure. Si este comando de PowerShell da error por algún motivo, debe comprobar si tiene instalado correctamente Azure PowerShell.

```
Login-AzureRmAccount
```

Ejecute hello tooget detalla en el equilibrador de carga y ver valores de hello para la descripción de Hola para **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Establecer ahora *frontendPortRangeEnd* y *frontendPortRangeStart* toohello los valores que desee.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Pasos siguientes
* [Información general sobre la característica de "En cualquier lugar para implementar" hello y hacer una comparación con clústeres administrado de Azure](service-fabric-deploy-anywhere.md)
* [Seguridad de clúster](service-fabric-cluster-security.md)
* [ SDK de Service Fabric e introducción](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
