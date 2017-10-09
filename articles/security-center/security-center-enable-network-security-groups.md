---
title: aaaEnable grupos de seguridad de red en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** Habilitar red seguridad grupos **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Habilitación de los grupos de seguridad de red en Azure Security Center
Azure Security Center recomienda habilitar un grupo de seguridad de red (NSG) si no hay ninguno habilitado. Los NSG contienen una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan el tráfico de red tooyour instancias de máquina virtual en una red Virtual. Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred. Además, el tráfico tooan máquina virtual individual se puede restringir aún más mediante asociar un NSG directamente toothat máquina virtual. toolearn más vea [¿qué es un grupo de seguridad de red (NSG)?](../virtual-network/virtual-networks-nsg.md)

Si no tiene habilitado el NSG, centro de seguridad presenta dos tooyou recomendaciones: habilitar grupos de seguridad de red en subredes y habilitar a los grupos de seguridad de red en máquinas virtuales. Elija qué nivel, la subred o la máquina virtual, tooapply NSG.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **habilitar grupos de seguridad de red** en subredes o en máquinas virtuales.
   ![Habilitar los grupos de seguridad de red][1]
2. Esto abre una hoja de hello **configurar grupos de seguridad de red falta** para subredes o para las máquinas virtuales, según la recomendación de Hola que seleccionó. En, seleccione una subred o un tooconfigure un NSG de máquina virtual.

   ![Configurar NSG para subred][2]

   ![Configurar NSG para máquina virtual][3]
3. En hello **elegir grupo de seguridad de red** hoja, seleccione un NSG existente o **crear nuevo** toocreate un NSG.

   ![Elegir grupo de seguridad de red][4]

Si crea un NSG, siga los pasos de hello en [cómo NSG toomanage mediante Hola portal de Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un NSG y establecer las reglas de seguridad.

## <a name="see-also"></a>Otras referencias
En este artículo se ha explicado cómo tooimplement Hola centro de seguridad recomendación "habilitar grupos de seguridad red" para subredes o máquinas virtuales. toolearn más acerca de cómo habilitar los NSG, vea Hola recursos siguientes:

* [¿Qué es un grupo de seguridad de red?](../virtual-network/virtual-networks-nsg.md)
* [Cómo NSG toomanage mediante Hola portal de Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
