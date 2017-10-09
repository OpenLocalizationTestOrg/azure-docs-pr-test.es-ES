---
title: "aaaAzure preguntas más frecuentes sobre mantenimiento de recursos | Documentos de Microsoft"
description: "Introducción a Azure Resource Health"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>P+F sobre Azure Resource Health
Obtenga información acerca de hello responde toocommon preguntas sobre el estado de recursos de Azure.

## <a name="what-is-azure-resource-health"></a>¿Qué es Azure Resource Health?
Resource Health le ayuda a diagnosticar y obtener soporte técnico cuando un problema de Azure afecta a sus recursos. Le informa sobre el estado de hello actuales y pasadas de los recursos y le ayuda a mitigar los problemas. Resource Health le proporciona soporte técnico si necesita ayuda con los problemas de los servicios de Azure.  

## <a name="what-is-hello-resource-health-intended-for"></a>¿Qué es hello destinado a estado de los recursos?
Una vez que se ha detectado un problema con un recurso, estado de los recursos puede ayudar a diagnosticar la causa de Hola. Proporciona ayuda toomitigate Hola problema y soporte técnico si necesita más ayuda con problemas de servicio de Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>¿Qué comprobaciones de estado realiza Resource Health?
Estado de los recursos realiza varias comprobaciones en función de hello [tipo de recurso](resource-health-checks-resource-types.md). Estas comprobaciones son tooimplement diseñada tres tipos de problemas: 
- Eventos no planeados, por ejemplo, un reinicio inesperado del host
- Eventos planeados, como actualizaciones programadas del sistema operativo del host
- Eventos desencadenados por acciones de usuario, por ejemplo, un usuario que reinicia una máquina virtual

## <a name="what-does-each-of-hello-health-status-mean"></a>¿Qué significa cada estado de mantenimiento de hello?
Hay tres estados de mantenimiento distintos:
- Disponible: No hay ningún problema conocido en hello plataforma Windows Azure que podría estar afectando a este recurso
- No disponible: Mantenimiento de recursos ha detectado problemas que afectan a los recursos de Hola
- Desconocido: Estado de los recursos no puede determinar estado Hola de un recurso porque se ha detenido recibir información sobre él. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>¿Qué Hola Media de estado desconocido? ¿Hay problemas con mi recurso?
estado de mantenimiento de Hola se establece toounknown al estado de los recursos deja de recibir información acerca de un recurso concreto. Aunque este estado no es una indicación definitiva del estado de saludo del recurso de hello, en casos donde están experimentando problemas, puede indicar que un problema de Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>¿Cómo puedo obtener ayuda para un recurso no disponible?
Puede enviar una solicitud de soporte técnico de la hoja de estado de los recursos de Hola. No es necesario un contrato de soporte técnico con Microsoft tooopen una solicitud al recurso de hello no está disponible porque eventos de la plataforma.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>¿Diferencia Resource Health entre la falta de disponibilidad por problemas de la plataforma o por alguna acción mía?
Sí, cuando un recurso no está disponible, mantenimiento de recursos identifica Hola causa dentro de una de estas categorías: 
-   Acción iniciada por el usuario
-   Evento planeado 
-   Evento no planeado

En el portal de hello, las acciones iniciadas por el usuario se muestran con un icono de notificación azul, mientras que los eventos previstos e imprevistos se muestran con un icono de advertencia rojo. Se proporcionan más detalles en hello [información general del estado de los recursos](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>¿Puedo integrar Resource Health con mis herramientas de supervisión?
Estado del recurso es un toohelp servicio diseñado diagnosticar y mitigar los problemas de servicio de Azure que afectan a los recursos. Aunque puede usar Hola API de mantenimiento de recursos tooprogrammatically obtener estado de mantenimiento de hello, se recomienda que usar las métricas toomonitor los recursos. Una vez que se detecta un problema, estado de los recursos le ayuda a determinar la causa principal de Hola y le guía a través de acciones tooaddress ellos. Visite [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn más información acerca de cómo se pueden utilizar los recursos de toocheck de métricas.

## <a name="where-do-i-find-resource-health"></a>¿Dónde se encuentra Resource Health?
Después de iniciar sesión en toohello portal de Azure, hay varias formas que puede tener acceso a mantenimiento de recursos:
- Navegar tooyour recurso. En el panel de navegación izquierdo hello, seleccione **mantenimiento de recursos**
- Vaya toohello hoja de Monitor de Azure.  En el panel de navegación izquierdo hello, seleccione **estado de los recursos**.
- Abra hello **ayuda y soporte técnico** hoja seleccionando Hola de signo de interrogación en hello superior derecho del portal de hello y, a continuación, seleccione **ayuda y soporte técnico**. Una vez que se abre la hoja de hello, seleccione **mantenimiento de recursos**

También puede utilizar Hola API de mantenimiento de recursos tooobtain obtener información sobre el estado de saludo de los recursos.

## <a name="is-resource-health-available-for-all-resource-types"></a>¿Está Resource Health disponible para todos los tipos de recursos?
Hello lista de comprobaciones de mantenimiento y tipos de recursos admitidos a través de estado de los recursos puede encontrarse [aquí](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>¿Qué debo hacer si mi recurso aparece como disponible pero creo que no lo está?
Cuando la comprobación de estado de Hola de un recurso, justo debajo de estado de mantenimiento de hello puede hacer clic en **informan del estado de mantenimiento incorrecto**. Antes de enviar informes de hello, tendrá posibilidad de Hola de proporcionar detalles adicionales sobre por qué crees estado actual de hello es incorrecta.

## <a name="is-resource-health-available-for-all-azure-regions"></a>¿Está Resource Health disponible en todas las regiones de Azure? 
Está disponible en estado de los recursos a través de todas las zonas geográficas: Azure excepto Hola siguientes regiones:
- Gobierno de EE. UU. - Virginia
- Gobierno de EE. UU. - Iowa
- Departamento de Defensa de EE. UU. Este
- Departamento de Defensa de EE. UU. Centro
- Centro de Alemania
- Noreste de Alemania
- Este de China
- Norte de China

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>¿Cómo es diferente de hello panel Estado del servicio o hello Azure service portal notificaciones de estado de los recursos?
información de Hello proporcionada por estado de los recursos es más específica que lo que se proporciona por hello panel de estado del servicio de Azure.

Mientras que [estado de Azure](https://status.azure.com) y notificaciones del servicio del portal de Hola que le informan sobre los problemas de servicio que afectan a un amplio conjunto de clientes (por ejemplo, una región de Azure), estado de los recursos expone eventos más granulares que solo son relevantes toohello recurso específico. Por ejemplo, si un host se reinicia de improviso, Resource Health solo alerta a los clientes cuyas máquinas virtuales se ejecutaban en ese host.

Es importante toonotice ese tooprovide que termine la visibilidad de los eventos que afectan a los recursos, también se publican los eventos de superficies en las notificaciones del servicio de mantenimiento de recursos y Hola panel Estado del servicio.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>¿Es necesario tooactivate mantenimiento de recursos para cada recurso?
No, la información de estado está disponible para todos los tipos de recursos a través de Resource Health. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>¿Tenemos tooenable estado de los recursos para mi organización?
No.  Mantenimiento de recursos de Azure es accesible dentro de hello portal de Azure sin ningún requisito de instalación.

## <a name="is-resource-health-available-free-of-charge"></a>¿Está Resource Health disponible de forma gratuita?
Sí.  Azure Resource Health es gratuito.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>¿Cuáles son las recomendaciones de Hola que proporciona el estado de los recursos?
En función de estado de mantenimiento de hello, mantenimiento de recursos proporciona recomendaciones con el objetivo de Hola de reducir el tiempo de hello dedicado a solucionar problemas. Para los recursos disponibles, las recomendaciones de hello centran en cómo encuentran los clientes de problemas más comunes de toosolve Hola. Si no está disponible debido a recursos de hello tooan Azure evento no planeado, Hola se centrará en asistencia durante y después del proceso de recuperación de Hola. 

## <a name="next-steps"></a>Pasos siguientes

Más información sobre Resource Health:
-  [Información general sobre Azure Resource Health](Resource-health-overview.md)
-  [Tipos de recursos y comprobaciones de estado disponibles con Azure Resource Health](resource-health-checks-resource-types.md)
