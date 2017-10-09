---
title: "aaaAdd un firewall de generación siguiente en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** agregar un Firewall de generación siguiente ** y ** tráfico de ruta a través de NGFW solo **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Adición de un firewall de próxima generación en Azure Security Center
Centro de seguridad de Azure puede recomienda agregar un servidor de seguridad de la generación siguiente (NGFW) desde un tooincrease de partner de Microsoft la protección de la seguridad. Este documento le guía a través de un ejemplo de cómo toodo esto.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **agregar un Firewall de generación siguiente**.
   ![Agregar un firewall de próxima generación][1]
2. Hola **agregar un Firewall de generación siguiente** hoja, seleccione un punto de conexión.
   ![Selección de un punto de conexión][2]
3. Se abrirá una segunda hoja **Add a Next Generation Firewall** (Agregar un firewall de próxima generación). Puede elegir a toouse una solución existente si está disponible o puede crear uno nuevo. En este ejemplo no hay ninguna solución existente disponible, por lo que vamos a crear un NGFW.
   ![Creación de un firewall de próxima generación][3]
4. toocreate un NGFW, seleccione una solución de lista de Hola de socios integrados. En este ejemplo se selecciona **Punto de comprobación**.
   ![Selección de una solución de firewall de próxima generación][4]
5. Hola **punto de comprobación** hoja abre, proporciona información sobre solución de socios de Hola. Seleccione **crear** en la hoja de información de Hola.
   ![Hoja de información del firewall][5]
6. Hola **crear máquina virtual** abre la hoja. Aquí puede introducir información toospin requiere una máquina virtual (VM) que se ejecuta Hola NGFW. Siga los pasos de Hola y proporcionar hello NGFW información necesaria. Seleccione Aceptar tooapply.
   ![Crear la máquina virtual toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>Enrutar el tráfico solo a través de NGFW
Devolver toohello **recomendaciones** hoja. Después de agregar un NGFW a través de Security Center, se genera una nueva entrada llamada **Enrutar el tráfico solo a través de un firewall de nueva generación**. Esta recomendación solo se crea si ha instalado el NGFW a través de Security Center. Si tiene extremos de conexión a Internet, el centro de seguridad recomienda configurar las reglas de grupo de seguridad de red que fuerce el tráfico entrante tooyour máquina virtual a través de su NGFW.

1. Hola **hoja de recomendaciones**, seleccione **enrutar el tráfico a través de NGFW solo**.
   ![Enrutar el tráfico solo a través de NGFW][7]
2. Esto abre una hoja de hello **enrutar el tráfico a través de NGFW solo**, que muestra las máquinas virtuales que se puede redirigir el tráfico a. Seleccione una máquina virtual de hello lista.
   ![Seleccionar una máquina virtual][8]
3. Una hoja de hello seleccionado se abre VM y muestra las reglas de entrada relacionadas. Una descripción proporciona más información sobre los posibles pasos posteriores. Seleccione **editar reglas de entrada** tooproceed con la edición de una regla de entrada. Hola expectativa es que **origen** no está establecido demasiado**cualquier** para los extremos de conexión a Internet de hello vinculado con Hola NGFW. toolearn más información sobre propiedades de Hola de regla de entrada de hello, consulte [reglas del NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Configurar el acceso de las reglas toolimit][9]
   ![Editar regla de entrada][10]

## <a name="see-also"></a>Otras referencias
Este documento se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Agregar un Firewall de generación siguiente." toolearn más información sobre NGFWs y Hola solución de socios de punto de comprobación, vea Hola recursos siguientes:

* [Firewall de próxima generación](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad en el centro de seguridad de Azure](security-center-policies.md) : Obtenga información acerca de cómo las directivas de seguridad de tooconfigure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
