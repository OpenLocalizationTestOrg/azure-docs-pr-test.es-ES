---
title: "¿aaaWhat es una lista de control de acceso de red de Azure?"
description: "Más información sobre las listas de control de acceso de Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>¿Qué es una lista de control de acceso de puntos de conexión?

> [!IMPORTANT]
> Azure tiene dos [modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) diferentes para crear recursos y trabajar con ellos: Resource Manager y el clásico. Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones utilizarán modelo de implementación del Administrador de recursos de Hola. 

Una lista de control de acceso (ACL) de puntos de conexión es una mejora de seguridad disponible para la implementación de Azure. Una ACL proporciona Hola capacidad tooselectively permitir o denegar el tráfico para un punto de conexión de máquina virtual. Esta capacidad de filtro de paquetes proporciona un nivel adicional de seguridad. Puede especificar ACL de red solo para extremos. No se puede especificar una ACL para una red virtual o para una subred específica contenida en una red virtual. Se recomienda toouse grupos de seguridad de red (NSG) en lugar de ACL, siempre que sea posible. toolearn más información acerca de los NSG, consulte [información general sobre el grupo de seguridad de red](virtual-networks-nsg.md)

Las ACL se pueden configurar con PowerShell u Hola portal de Azure. tooconfigure una ACL de red con PowerShell, vea [listas de control de acceso de administración para los puntos de conexión con PowerShell](virtual-networks-acl-powershell.md). tooconfigure una ACL de red mediante el uso de hello Azure portal, vea [cómo tooset la máquina virtual de los puntos de conexión tooa](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Con las ACL de red, puede hacer siguiente hello:

* Permitir o denegar el tráfico entrante en función de extremo de entrada de la máquina virtual de tooa de IPv4 dirección intervalo de subred remota de forma selectiva.
* Incluir en una lista negra direcciones IP
* Crear varias reglas por extremo de máquina virtual
* Usar regla orden tooensure Hola correcto de conjunto de reglas se aplican a un punto de conexión de máquina virtual dada (toohighest más bajo)
* Especificar una ACL para una dirección IPv4 de la subred remota específica.

Vea hello [Azure tiene una limitación](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) artículo para los límites de la ACL.

## <a name="how-acls-work"></a>Funcionamiento de las ACL
Una ACL es un objeto que contiene una lista de reglas. Al crear una ACL y aplicarla tooa extremo de máquina virtual, el filtrado de paquetes tiene lugar en el nodo de host de saludo de la máquina virtual. Esto significa que se filtra el tráfico de Hola desde direcciones IP remotas por nodo de host de Hola para reglas ACL coincidentes en lugar de en la máquina virtual. Esto evita que la máquina virtual de los gastos que preciosos ciclos de CPU de hello en el filtrado de paquetes.

Cuando se crea una máquina virtual, se coloca una ACL predeterminada en lugar tooblock todo el tráfico entrante. Sin embargo, si se crea un punto de conexión (puerto 3389), a continuación, Hola predeterminado que ACL es modificado tooallow todo el tráfico entrante para ese extremo. Tráfico entrante desde cualquier subred remota, a continuación, se permite el punto de conexión de toothat y aprovisionar ningún firewall es obligatorio. Todos los demás puertos se bloquean para el tráfico entrante a menos que se creen extremos para esos puertos. De forma predeterminada, se permite el tráfico saliente.

**Ejemplo de tabla de ACL predeterminada**

| **Nº de regla** | **Subred remota** | **Extremo** | **Permitir o denegar** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Permitir |

## <a name="permit-and-deny"></a>Permitir y denegar
Selectivamente puede permitir o denegar el tráfico de red para un extremo de entrada de la máquina virtual mediante la creación de reglas que especifiquen "permitir" o "denegar". Es importante toonote que de forma predeterminada, cuando se crea un punto de conexión, todo el tráfico se permite toohello extremo. Por esta razón, es importante toounderstand cómo toocreate las reglas de permitir/denegar y colocarlos en el orden de prioridad adecuado Hola si desea que un control granular sobre red Hola tráfico que elija el extremo de máquina virtual de tooallow tooreach Hola.

Tooconsider puntos:

1. **Ninguna ACL:** de forma predeterminada cuando se crea un punto de conexión, se permite todo para el punto de conexión de Hola.
2. **Permitir** : al agregar uno o más intervalos "permitidos", se deniegan todos los demás intervalos de forma predeterminada. Solo los paquetes del Hola permitida intervalo IP será capaz de toocommunicate con punto de conexión de máquina virtual de Hola.
3. **Denegar** : al agregar uno o más intervalos "denegados", se permiten todos los demás intervalos del tráfico de forma predeterminada.
4. **Combinación de permitir y denegar -** puede usar una combinación de "permitir" y "Denegar" Si desea toocarve espera una dirección IP específica rango toobe permitirá o denegará.

## <a name="rules-and-rule-precedence"></a>Reglas y precedencia de reglas
Las ACL de red se pueden configurar en los extremos de la máquina virtual específica. Por ejemplo, puede especificar una ACL de red para un extremo RDP creado en una máquina virtual que bloquee el acceso a determinadas direcciones IP. Hello tabla siguiente muestra un toopublic de acceso de manera toogrant direcciones IP virtuales (VIP) de un determinado acceso a los toopermit de intervalo para RDP. Se deniegan todas las direcciones IP remotas. Seguimos un orden de regla de la *inferior tiene prioridad* .

### <a name="multiple-rules"></a>Varias reglas
En el ejemplo de Hola siguiente, si desea que el punto de conexión de tooallow acceso toohello RDP solo desde dos IPv4 intervalos de direcciones públicas (65.0.0.0/8 y 159.0.0.0/8), puede conseguirlo mediante la especificación de dos *permitir* reglas. En este caso, como RDP se crea de forma predeterminada para una máquina virtual, puede que desee toolock hacia abajo el puerto RDP toohello de acceso basado en una subred remota. Hello ejemplo siguiente muestra un toopublic de acceso de manera toogrant direcciones IP virtuales (VIP) de un determinado acceso a los toopermit de intervalo para RDP. Se deniegan todas las direcciones IP remotas. Esto funciona porque las ACL de red se puede configurar para un extremo de máquina virtual específica y se deniega el acceso de forma predeterminada.

**Ejemplo: varias reglas**

| **Nº de regla** | **Subred remota** | **Extremo** | **Permitir o denegar** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Permitir |
| 200 |159.0.0.0/8 |3389 |Permitir |

### <a name="rule-order"></a>Orden de reglas
Porque pueden especificarse varias reglas para un punto de conexión, tiene que haber una manera tooorganize reglas en toodetermine orden qué regla tiene prioridad. orden de las reglas Hola especifica la prioridad. Las ACL de red siguen el orden de regla de la *inferior tiene prioridad* . En el siguiente ejemplo de Hola, endpoint hello en el puerto 80 se concede de forma selectiva acceso tooonly determinados intervalos de direcciones IP. tooconfigure, tenemos una regla de denegación (regla \# 100) para las direcciones de espacio 175.1.0.1/24 de Hola. A continuación, se especifica una segunda regla con prioridad 200 que permite tener acceso a tooall otras direcciones bajo 175.0.0.0/8.

**Ejemplo: precedencia de reglas**

| **Nº de regla** | **Subred remota** | **Extremo** | **Permitir o denegar** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Denegar |
| 200 |175.0.0.0/8 |80 |Permitir |

## <a name="network-acls-and-load-balanced-sets"></a>ACL de red y conjuntos de carga equilibrada
Las ACL de red pueden especificarse en un punto de conexión del conjunto de carga equilibrada. Si se especifica una ACL para un conjunto de carga equilibrada, ACL de red de hello es máquinas virtuales de tooall aplicado en ese conjunto de carga equilibrada. Por ejemplo, si se crea un conjunto de carga equilibrada con el "Puerto 80" y el conjunto de carga equilibrada de hello contiene 3 máquinas virtuales, red Hola ACL creada en el extremo "Puerto 80" de una que máquina virtual se configurará automáticamente aplicar toohello otras máquinas virtuales.

![ACL de red y conjuntos de carga equilibrada](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Pasos siguientes
[Administración de listas de control de acceso para puntos de conexión mediante PowerShell](virtual-networks-acl-powershell.md)

