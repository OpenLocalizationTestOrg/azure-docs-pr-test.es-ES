---
title: "aaaApplication integración de puerta de enlace con el centro de seguridad de Azure | Documentos de Microsoft"
description: "Esta página proporciona información sobre cómo se integra Application Gateway en Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Introducción a la integración entre Application Gateway y Azure Security Center

Conozca más información acerca de cómo Application Gateway y Security Center le ayudan a proteger los recursos de la aplicación web. Servidor de aplicaciones web de aplicación puerta de enlace (WAFS) se integra con [centro de seguridad](../security-center/security-center-intro.md) tooprovide un tooprevent vista integrada, detectar y responder a las aplicaciones web de toothreats toounprotected en su entorno.

## <a name="overview"></a>Información general

El WAF de Application Gateway es una recomendación de Security Center para proteger las aplicaciones web frente a ataques y vulnerabilidades. Recursos de Web habilitado que no están protegidos por WAFS se muestran en el centro de seguridad de hello como recomendaciones de gravedad alta. Recomendaciones para los firewalls de aplicación web se muestran en hello **Introducción** página, en **aplicaciones**.

![integración con security center][1]

Al pulsar ninguna recomendación relacionada con el servidor de aplicaciones web, abre una nueva hoja muestra los detalles de saludo de la recomendación de Hola.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Agregar un recurso web de aplicación firewall tooan existente

Navegue demasiado**más servicios** > **seguridad e identidad** > **centro de seguridad** y en hello **centro de seguridad - información general**  hoja, haga clic en **aplicaciones**. En hello **centro de seguridad - aplicaciones** hoja, tabla de hello contiene una lista de aplicaciones que el centro de seguridad ha detectado en su suscripción.

![aplicaciones web][3]

Al hacer clic en una aplicación web con un problema crítico, obtendrá hello **estado de seguridad de la aplicación** hoja. En la imagen de hello siguiente, Hola aplicación web que no está protegido por un servidor de seguridad de la aplicación web. 

![recursos web no protegidos][2]

Haga clic en **agregar un servidor de seguridad de la aplicación web** en **recomendaciones** tooopen hello **agregar un servidor de seguridad de la aplicación Web** hoja.

Si no tiene una puerta de enlace de la aplicación existente, o desea toocreate uno nuevo, haga clic en **crear nuevo** y en hello **crear un nuevo servidor de aplicaciones Web** hoja y haga clic en **Microsoft: Puerta de enlace de aplicaciones**. Esto le llevará a través de hello pasos toocreate una puerta de enlace de la aplicación. En este punto, la aplicación web se agrega como un recurso protegido y Security Center realiza un seguimiento para asegurarse de que este recurso está protegido por un firewall de aplicaciones web. No se agrega como miembro del grupo de back-end.

Si ya tiene una instancia de Application Gateway, puede elegirla en **Usar solución existente**

![hoja de adición de firewall de aplicaciones web][4]

Agregar que una puerta de enlace de web application tooan aplicación a través del centro de seguridad no agrega recursos Hola como un miembro del grupo back-end, debe hacerlo en el recurso de puerta de enlace de aplicación Hola directamente.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Agregar un servidor de aplicaciones de web existente de recursos tooan

Navegue demasiado**más servicios** > **seguridad e identidad** > **centro de seguridad** y en hello **centro de seguridad - información general**  hoja, haga clic en **soluciones de asociados**. Puertas de enlace de aplicación compatible con el centro de seguridad existentes se muestran en hello **soluciones de socios** hoja.

![soluciones de asociados][7]

Haga clic en **aplicación vínculo** tooopen hello **aplicaciones de vínculo** hoja, aquí se proporcionan aplicaciones existentes de hello opciones tooselect. Elija Hola aplicaciones tooprotect y haga clic en **Aceptar**. Este método no agrega grupo hello web aplicación toohello back-end de puerta de enlace de aplicación Hola. Recursos de Hola se establece como un recurso protegido para que el centro de seguridad puede realizar un seguimiento. recurso de hello tooadd como un miembro del grupo back-end, esto debe hacerse en puerta de enlace de aplicación Hola, desde la hoja actual de hello puede hacer clic **consola de solución** toobe realizada toohello de recursos de puerta de enlace de aplicación donde puede agregar web Hola grupo de aplicaciones toohello back-end.

![aplicaciones de soluciones de asociados][6]

## <a name="finalize-configuration"></a>Finalización de la configuración

Las aplicaciones de las pistas del centro de seguridad agregan tooan puerta de enlace de aplicaciones como un recurso protegido.  Supervisa el estado de Hola de este recurso y se asegura de que está protegida por una puerta de enlace de la aplicación. Hola siguiente paso es tooadd Hola privada IP, IP pública o NIC de su grupo de back-end de toohello de máquina virtual de puerta de enlace de aplicación Hola. Hasta que esto se hace una recomendación adicional de **finalizar la protección de la aplicación** se muestra hasta que se agregan recursos de Hola.

![hoja de adición de firewall de aplicaciones web][5]

## <a name="security-alerts"></a>Alertas de seguridad

En el centro de seguridad desplazarse demasiado**detección** > **alertas de seguridad**.  Aquí encontrará las alertas de WAF para las instancias de Application Gateway. Las alertas se desglosan según las reglas de WAF.

![alertas de seguridad][8]

Si hace clic en una regla proporcionará una lista de alertas para esa regla de WAF específica. Cada alerta muestra detalles adicionales acerca de cómo buscar Hola. detalles de Hello proporcionan una puerta de enlace de aplicaciones de toohello de vínculo.
 
![detalles de alertas][9]

## <a name="next-steps"></a>Pasos siguientes

toolearn cómo tooenable firewall de aplicación web en una puerta de enlace de aplicación existente, visite [crear o actualizar una puerta de enlace de aplicaciones de Azure con firewall de aplicación web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png