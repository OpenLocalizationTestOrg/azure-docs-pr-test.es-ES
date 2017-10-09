---
title: "aaaRestrict acceso a través de extremos de conexión a Internet en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** restringir el acceso a través de Internet orientada hacia el extremo **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Restricción del acceso a través de puntos de conexión accesibles desde Internet en Azure Security Center
Azure Security Center recomendará restringir el acceso a través de puntos de conexión accesibles desde Internet si alguno de los grupos de seguridad de red (NSG) tiene una o varias reglas de entrada que permitan el acceso desde cualquier dirección IP de origen. Abrir acceso demasiado "any" puede habilitar los atacantes tooaccess sus recursos. Centro de seguridad se recomienda editar estas direcciones IP de las reglas de entrada toorestrict acceso toosource que realmente necesitan tener acceso.

Esta recomendación se genera para cualquier puerto no web que tenga la opción Cualquiera como origen.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **hoja de recomendaciones**, seleccione **restringir el acceso a través de Internet orientada hacia el extremo**.

   ![Restricción del acceso a través de puntos de conexión accesibles desde Internet][1]
2. Esto abre una hoja de hello **restringir el acceso a través de Internet orientada hacia el extremo**. Esta hoja enumera hello las máquinas virtuales (VM) con las reglas de entrada que crean un posible riesgo de seguridad. Seleccione una máquina virtual.

   ![Seleccionar una máquina virtual][2]
3. Hola **NSG** hoja muestra la información de grupo de seguridad de red, las reglas de entrada relacionadas, y Hola asociados máquina virtual. Seleccione **editar reglas de entrada** tooproceed con la edición de una regla de entrada.

   ![Hoja Grupo de seguridad de red][3]
4. En hello **reglas de seguridad de entrada** seleccione hoja Hola tooedit de regla de entrada. En este ejemplo, vamos a seleccionar **AllowWeb**.

   ![Reglas de seguridad de entrada][4]

   Tenga en cuenta que también puede seleccionar **reglas predeterminadas** toosee Hola formado por las reglas predeterminadas que contiene todos los NSG. no se puede eliminar las reglas predeterminadas de Hello pero, dado que se asignan una prioridad más baja, puede reemplazarse por reglas de Hola que cree. Obtenga más información sobre [reglas predeterminadas](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Reglas predeterminadas][5]
5. En hello **AllowWeb** hoja, modificar las propiedades de regla de entrada de Hola para que Hola Hola **origen** es una dirección IP o un bloque de direcciones IP. toolearn más información sobre propiedades de Hola de regla de entrada de hello, consulte [reglas del NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Editar regla de entrada][6]

## <a name="see-also"></a>Otras referencias
En este artículo se ha mostrado cómo tooimplement Hola centro de seguridad recomendación "restringir el acceso a través de Internet orientada hacia el punto de conexión." toolearn más acerca de cómo habilitar los NSG y reglas, vea Hola recursos siguientes:

* [¿Qué es un grupo de seguridad de red?](../virtual-network/virtual-networks-nsg.md)
* [Cómo NSG toomanage mediante Hola portal de Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
