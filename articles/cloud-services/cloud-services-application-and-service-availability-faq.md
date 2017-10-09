---
title: "los problemas de disponibilidad aaaApplication y servicio de preguntas más frecuentes sobre servicios de nube de Microsoft Azure | Documentos de Microsoft"
description: "Este artículo enumeran Hola preguntas más frecuentes acerca de la aplicación y la disponibilidad del servicio para servicios de nube de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de disponibilidad de aplicaciones y servicios en Azure Cloud Services: preguntas frecuentes (P+F)| Microsoft Docs

En este artículo se incluyen preguntas frecuentes sobre la disponibilidad de aplicaciones y servicios en [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Mi rol se recicla. ¿Se ha implementado alguna actualización para el servicio en la nube?
Aproximadamente una vez al mes, Microsoft publica una nueva versión de SO invitado para máquinas virtuales PaaS de Azure en Windows. El SO invitado es solo una de estas actualizaciones en la canalización de Hola. Otros muchos factores pueden influir en una publicación. Además, Azure se ejecuta en cientos de miles de máquinas. Por lo tanto, resulta imposible toopredict Hola fecha y hora exacta cuando se reiniciarán los roles. Actualizamos Hola actualizar fuente RSS SO invitado con la información más reciente de Hola que tenemos, pero se recomienda que notifica un valor aproximado del tiempo toobe. Somos conscientes de que esto es problemático para los clientes y está trabajando en un plan toolimit ni con precisión los reinicios de tiempo.

Para obtener información detallada sobre las actualizaciones recientes del SO invitado, consulte [Matriz de compatibilidad del SDK y versiones del SO invitado de Azure](cloud-services-guestos-update-matrix.md).

Para obtener información útil sobre los detalles de tootechnical reinicios y punteros de actualizaciones de sistemas operativos Host e invitado, vea blogs MSDN de hello [actualizaciones de instancia de rol se reinicia debido tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>¿Por qué tarda más de lo habitual Hola primera solicitud toomy servicio en la nube después de servicio de hello ha estado inactivo durante algún tiempo?
Cuando Hola servidor Web recibe una solicitud primera hello, vuelve a compilar primero el código de hello y, a continuación, procesa la solicitud de saludo. Que es ¿por qué Hola primera solicitud tardará más de hello otros usuarios. De forma predeterminada, el grupo de aplicaciones de hello obtiene Apagar en los casos de inactividad del usuario. grupo de aplicaciones de Hello también se recicla de forma predeterminada cada 1.740 minutos (29 horas).

Grupos de aplicaciones de Internet Information Services (IIS) pueden ser Estados inestable tooavoid reciclan periódicamente que pueden causar tooapplication bloqueos, bloqueos o pérdidas de memoria.

Hola después de documentos le ayudará a comprender y mitigar este problema:
* [Fixing slow initial load for IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis) (Corrección de carga inicial lenta en IIS)
* [IIS 7.5 web application first request after app-pool recycle very slow](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow) (Primera solicitud de aplicación web de IIS.7.5 muy lenta después del reciclaje del grupo de aplicaciones)

Si desea que el comportamiento de toochange Hola predeterminado de IIS, debe toouse las tareas de inicio, porque si aplica manualmente instancias de rol Web de toohello de cambios, los cambios de hello finalmente se perderán.

Para obtener más información, consulte [cómo las tareas de inicio tooconfigure y ejecución de un servicio de nube](cloud-services-startup-tasks.md).
