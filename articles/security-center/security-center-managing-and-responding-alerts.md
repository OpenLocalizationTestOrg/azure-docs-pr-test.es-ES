---
title: aaaManage las alertas de seguridad en el centro de seguridad de Azure | Documentos de Microsoft
description: Este documento le ayuda a toouse Azure Security Center capacidades toomanage y responde toosecurity alertas.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure
Este documento le ayuda a usar Azure Security Center toomanage y responder toosecurity alertas.

> [!NOTE]
> detecciones de tooenable avanzada, tooAzure actualización estándar de centro de seguridad. Hay disponible una versión de evaluación gratuita de 60 días. tooupgrade, seleccione nivel de precios en hello [directiva de seguridad](security-center-policies.md). Vea [precios de Azure Security Center](security-center-pricing.md) toolearn más.
>
>

## <a name="what-are-security-alerts"></a>¿Qué son las alertas de seguridad?
Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de los recursos de Azure, red de hello, soluciones de socios comerciales, así como soluciones de protección firewall y de punto de conexión, toodetect reales amenazas conectadas y reducir los falsos positivos. Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola y recomendaciones sobre cómo tooremediate un ataque.


> [!NOTE]
> Para más información acerca de cómo actúan las funcionalidades de detección de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Administración de alertas de seguridad
Puede revisar las alertas actuales examinando hello **alertas de seguridad** icono. Abra el Portal de Azure y siga estos pasos hello toosee más detalles sobre cada alerta:

1. En el panel del centro de seguridad de hello, verá hello **alertas de seguridad** icono.

    ![Icono Alertas de seguridad en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Haga clic en Hola mosaico tooopen Hola **alertas de seguridad** hoja que contiene información más detallada acerca de hello alertas tal y como se muestra a continuación.

   ![hoja de alertas de seguridad de Hello en el centro de seguridad](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

En la parte inferior de Hola de esta hoja son los detalles de Hola para cada alerta. toosort, haga clic en la columna de Hola que desea toosort por. definición de Hola para cada columna se indica a continuación:

* **Descripción**: una breve explicación de alerta de Hola.
* **Recuento**: una lista de todas las alertas de este tipo específico que se han detectado en un día concreto.
* **Detectado por**: Hola servicio que era responsable de activar la alerta de Hola.
* **Fecha**: Hola fecha ese evento Hola se ha producido.
* **Estado**: Hola estado actual de esa alerta. Existen dos tipos de servicios:
  * **Active**: se detectó la alerta de seguridad de Hola.
* **Gravedad**: nivel de gravedad de hello, que puede ser alta, Media o baja.

### <a name="filtering-alerts"></a>Filtrado de alertas
Puede filtrar alertas en función de la fecha, el estado y la gravedad. Filtrar las alertas puede ser útil para escenarios donde es necesario ámbito de hello toonarrow de presentación de las alertas de seguridad. Por ejemplo, puede que también desee tooaddress alertas de seguridad que se produzcan en hello últimas 24 horas dado que se está investigando una posible infracción en sistema Hola.

1. Haga clic en **filtro** en hello **alertas de seguridad** hoja. Hola **filtro** abre la hoja y seleccione valores de fecha, el estado y la gravedad de hello desea toosee.

    ![Filtrado de alertas en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Responder toosecurity alertas
Seleccione un toolearn de alerta de seguridad más información acerca de los eventos de Hola que desencadenó la alerta de Hola y qué, si existe, los pasos necesitan tootake tooremediate un ataque. Las alertas de seguridad se agrupan según el tipo y la fecha. Al hacer clic en una alerta de seguridad se abrirá una hoja que contiene una lista de alertas de hello agrupado.

![Responder toosecurity alertas en el centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

En este caso, las alertas de Hola que se han activado consulte toosuspicious actividad de protocolo de escritorio remoto (RDP). Hola primera columna muestra qué recursos atacados; en segundo lugar, Hello muestra cuántas veces se atacadas recursos Hola; Hola tercero muestra el tiempo de Hola de ataque de hello; Hola cuarto muestra el estado de alerta de hello; y Hola quinto muestra gravedad Hola de ataque de Hola. Después de revisar esta información, haga clic en recurso de Hola que estaba atacada y se abrirá una nueva hoja.

![Sugerencias para qué toodo sobre la seguridad de las alertas en el centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

Hola **descripción** campo de esta hoja encontrará más detalles sobre este evento. Estos detalles adicionales proporcionan una visión general de qué Hola desencadenadas seguridad alerta, Hola recurso de destino, cuando Hola procede del origen de dirección IP y recomendaciones sobre cómo tooremediate.  En algunos casos, dirección IP de origen de Hola se vaciará (no disponible) porque no todos los registros de eventos de seguridad de Windows incluyen la dirección IP de Hola.

corrección de Hello sugerido por centro de seguridad variará alerta de seguridad toohello correspondiente. En algunos casos, puede que tenga toouse otro tooimplement las capacidades de Azure Hola recomendada corrección. Por ejemplo, Hola corrección para este tipo de ataque es la dirección IP de tooblacklist Hola que genera este tipo de ataque mediante el uso de un [ACL de red](../virtual-network/virtual-networks-acl.md) o un [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) regla.

> [!NOTE]
> Para obtener más información acerca de diferentes tipos de alertas de hello, lea [alertas de seguridad por tipo de Azure Security Center](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo tooconfigure las directivas de seguridad en el centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Control de incidentes de seguridad en Azure Security Center](security-center-incident.md)
* [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md)
* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md)
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
