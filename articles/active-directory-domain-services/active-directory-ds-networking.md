---
title: 'Azure AD Domain Services: directrices de redes | Microsoft Docs'
description: Consideraciones de red de Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Consideraciones de red de Azure AD Domain Services
## <a name="how-tooselect-an-azure-virtual-network"></a>¿Cómo tooselect una red virtual de Azure
Hello instrucciones siguientes le ayudarán a seleccionar una toouse de red virtual con los servicios de dominio de Active Directory de Azure.

### <a name="type-of-azure-virtual-network"></a>Tipo Azure Virtual Network
* Azure AD Domain Services se puede habilitar en una instancia clásica de Azure Virtual Network.
* Azure AD Domain Services **no se puede habilitar en las redes virtuales creadas mediante Azure Resource Manager**.
* Puede conectar una red virtual basada en el Administrador de recursos tooa clásico red virtual en el que se habilita servicios de dominio de Azure AD. Por lo tanto, puede usar servicios de dominio de AD de Azure en red virtual basada en el Administrador de recursos de Hola. Para obtener más información, vea hello [conectividad de red](active-directory-ds-networking.md#network-connectivity) sección.
* **Redes virtuales regionales**: si tiene previsto toouse una red virtual existente, asegúrese de que es una red virtual regional.

  * Redes virtuales que utilizan el mecanismo de grupos de afinidad heredados hello no se puede usar con los servicios de dominio de Active Directory de Azure.
  * Servicios de dominio de AD de Azure, toouse [migrar redes virtuales de redes virtuales heredados tooregional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Región de Azure para la red virtual de Hola
* Los servicios de dominio de AD de Azure dominio administrado se implementa en Hola la misma región de Azure como red virtual de hello en que elegir servicio de hello tooenable.
* Seleccione una red virtual en una región de Azure compatible con Azure AD Domain Services.
* Vea hello [servicios de Azure por región](https://azure.microsoft.com/regions/#services/) página tooknow Hola regiones de Azure en que los servicios de dominio de Azure AD está disponible.

### <a name="requirements-for-hello-virtual-network"></a>Requisitos de red virtual de Hola
* **Proximidad tooyour Azure cargas de trabajo**: seleccione Hola red virtual que hospeda actualmente/va a hospedar las máquinas virtuales que necesitan tener acceso a los servicios de dominio de AD tooAzure.
* **Los servidores DNS personalizado/bring your own**: asegúrese de que no hay ningún servidor DNS personalizado configurado para la red virtual de Hola.
* **Hola de dominios existentes con mismo nombre de dominio**: asegúrese de que no tiene un dominio existente con hello mismo nombre de dominio disponible en la red virtual. Por ejemplo, suponga que tiene un dominio denominado "contoso.com" ya está disponible en la red virtual seleccionada de Hola. Más adelante, intente tooenable un dominio administrado de los servicios de dominio de AD de Azure con hello mismo nombre de dominio (es decir, "contoso.com") en la red virtual. Detecta un error al tratar de servicios de dominio de tooenable Azure AD. Este error es debido a conflictos de tooname por nombre de dominio de hello en la red virtual. En esta situación, debe usar un nombre diferente tooset su dominio administrado de los servicios de dominio de AD de Azure. Como alternativa, puede Desaprovisionamiento de dominio existente de hello y, a continuación, continuar tooenable Azure AD los servicios de dominio.

> [!WARNING]
> No se puede mover la red virtual de servicios de dominio tooa diferente después de haber habilitado el servicio de Hola.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Grupos de seguridad de red y diseño de subred
A [grupo de seguridad de red (NSG)](../virtual-network/virtual-networks-nsg.md) contiene una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan el tráfico de red tooyour instancias de máquina virtual en una red Virtual. Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred. Además, el tráfico tooan máquina virtual individual se puede restringir aún más mediante asociar un NSG directamente toothat máquina virtual.

![Diseño de subred recomendado](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Procedimientos recomendados para elegir una subred
* Implementar servicios de dominio de AD de Azure tooa **separar subred dedicada** dentro de la red virtual de Azure.
* No se aplican los NSG toohello dedicado subred para el dominio administrado. Si debe aplicar los NSG toohello dedicado subred, asegúrese de **no bloquear Hola puertos necesarios tooservice y administrar el dominio**.
* No restringen demasiado el número de Hola de direcciones IP disponibles dentro de la subred de hello dedicado para el dominio administrado. Esta restricción impide que el servicio de Hola que dos controladores de dominio esté disponible para el dominio administrado.
* **No habilite servicios de dominio de AD de Azure en la subred de puerta de enlace de hello** de la red virtual.

> [!WARNING]
> Al asociar un NSG a una subred en el que Servicios de dominio de AD de Azure está habilitado, puede interferir con tooservice de capacidad de Microsoft y administrar el dominio de Hola. Además, se interrumpe la sincronización entre el inquilino de Azure AD y el dominio administrado. **Hola SLA no aplica toodeployments donde un NSG se ha aplicado que bloquea los servicios de dominio de AD de Azure de actualizar y administrar el dominio.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Puertos necesarios para Azure AD Domain Services
Hello siguientes puertos son necesarios para los servicios de dominio de Azure AD tooservice y mantienen el dominio administrado. Asegúrese de que estos puertos no estén bloqueados para la subred de hello en el que se ha habilitado el dominio administrado.

| Número de puerto | Propósito |
| --- | --- |
| 443 |Sincronización con el inquilino de Azure AD |
| 3389 |Administración del dominio |
| 5986 |Administración del dominio |
| 636 |LDAP (LDAPS) acceso tooyour administrado dominio seguro |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Grupo de seguridad de red (NSG) de ejemplo para redes virtuales con Azure AD Domain Services
Hello en la tabla siguiente muestra un ejemplo de NSG que se puede configurar para una red virtual con un dominio administrado de los servicios de dominio de AD de Azure. Esta regla permite el tráfico entrante de Hola por encima de los puertos especificados tooensure el dominio administrado permanece revisarse, actualiza y puede supervisarse por Microsoft. Hello 'DenyAll' reglas predeterminadas aplican tooall otro tráfico entrante de hello internet.

Además, hello NSG también muestra cómo Hola a toolock hacia abajo el acceso LDAP seguro a través de internet. Omitir esta regla si no ha habilitado LDAP acceso tooyour administrado dominio seguro sobre Hola internet. Hola NSG contiene un conjunto de reglas que permitan el acceso de entrada LDAPS a través del puerto TCP 636 solo de un conjunto especificado de direcciones IP. regla de acceso LDAPS NSG tooallow sobre Hola Hola internet desde direcciones IP especificadas tiene una prioridad más alta que Hola regla DenyAll NSG.

![Acceso de ejemplo NSG toosecure LDAPS sobre Hola internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Más información** - [Creación de un grupo de seguridad de red](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Conectividad de red
Un dominio administrado de Azure AD Domain Services solo se puede habilitar dentro de una única instancia de clásica de Azure Virtual Network. No se admiten las redes virtuales creadas mediante Azure Resource Manager.

### <a name="scenarios-for-connecting-azure-networks"></a>Escenarios para la conexión de Azure Networks
Conectar redes virtuales de Azure toouse Hola dominio administrado en cualquiera de hello los escenarios de implementación siguientes:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Hola uso administrados dominio en más de una red virtual de Azure clásica
Puede conectar otro toohello de redes virtuales de Azure clásico Azure clásico red virtual en el que ha habilitado los servicios de dominio de AD de Azure. Esta conexión VPN permite toouse Hola administrado dominio con las cargas de trabajo implementados en otras redes virtuales.

![Conectividad de red virtual clásica](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Utilizar el dominio administrado hello en una red virtual basada en el Administrador de recursos
Puede conectarse un toohello de red virtual basada en el Administrador de recursos de Azure clásico red virtual en el que ha habilitado los servicios de dominio de AD de Azure. Esta conexión permite toouse Hola administrado dominio con las cargas de trabajo implementados en la red virtual basada en el Administrador de recursos de Hola.

![Conectividad de red virtual del Administrador de recursos tooclassic](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Opciones de conexión de red
* **Las conexiones de red virtual a red virtual con conexiones VPN de sitio a sitio**: conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE.

    ![Conectividad de Virtual Network mediante VPN Gateway](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Más información: conectar redes virtuales mediante VPN Gateway](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **Intercambio de tráfico de red de las conexiones de red virtual a red virtual con virtual**: intercambio de tráfico de red Virtual es un mecanismo que conecta dos redes virtuales en hello misma región a través de la red troncal de Azure de Hola. Una vez emparejar, aparecerán las dos redes virtuales de hello uno para todos los propósitos de conectividad. No obstante, se administran como recursos independientes, pero las máquinas virtuales de estas redes virtuales pueden comunicarse entre sí directamente mediante sus direcciones IP privadas.

    ![Conectividad de Virtual Network mediante emparejamiento](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Más información: emparejamiento de red virtual](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Contenido relacionado
* [Emparejamiento de Azure Virtual Network](../virtual-network/virtual-network-peering-overview.md)
* [Configurar una conexión de red virtual a red virtual para el modelo de implementación clásica de Hola](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Grupos de seguridad de la red de Azure](../virtual-network/virtual-networks-nsg.md)
* [Creación de un grupo de seguridad de red](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
