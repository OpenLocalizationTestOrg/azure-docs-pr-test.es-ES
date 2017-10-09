---
title: aaaIntegrate registros de recursos de Azure en los sistemas SIEM | Documentos de Microsoft
description: "Aprenda sobre la integración de registro de Azure, sus principales funcionalidades y cómo funciona."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Introducción tooMicrosoft integración de registros de Azure
Aprenda sobre la integración de registro de Azure, sus principales funcionalidades y cómo funciona.

## <a name="overview"></a>Información general

Integración de registros de Azure es una solución gratuita que le permite hacer toointegrate sin procesar registros de los recursos de Azure en sistemas de administración de eventos (SIEM) e información de seguridad local tooyour.

Integración de registro de Azure recopila eventos de Windows de los registros del Visor de eventos de Windows, los [registros de actividad de Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), las [alertas de Azure Security Center](../security-center/security-center-intro.md) y los [registros de Azure Diagnostics](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) de los recursos de Azure. Esta integración le ayuda a la solución SIEM proporcionan un panel unificado para todos sus activos, local o en la nube de hello, por lo que puede agregar, correlacionar, analizar y alertas para eventos de seguridad.

>[!NOTE]
En este momento, las nubes de hello solo admitido son comercial de Azure y Azure Government. No se admiten otras nubes.

![Integración de registro de Azure][1]

## <a name="what-logs-can-i-integrate"></a>¿Qué registros se pueden integrar?
Azure genera gran cantidad de registros para cada servicio. Estos registros representan tres tipos de registros:

* **Registros de control/management** proporcionar visibilidad de hello [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) operaciones CREATE, UPDATE y DELETE. Los registros de actividad de Azure son un ejemplo de este tipo de registro.
* **Datos plano registros** proporcionar visibilidad de los eventos de hello provoca como parte del uso de Hola de un recurso de Azure. Un ejemplo de este tipo de registro es del Visor de eventos de Windows hello **System**, **seguridad**, y **aplicación** canales en una máquina virtual de Windows. Otro ejemplo es el registro de diagnóstico configurado a través de Azure Monitor.
* **Eventos procesados**: proporcionan información de alertas y eventos analizados procesada en nombre del usuario. Un ejemplo de este tipo de evento es Azure Security Center alertas, donde tiene procesar y analizar su suscripción tooprovide alertas relevantes tooyour actual postura de seguridad de Azure Security Center.

Integración de registro de Azure admite ArcSight, QRadar y Splunk. En todas las circunstancias, compruebe con su tooassess de proveedores SIEM si tienen un conector nativo. En algunos casos, no necesitará toouse integración de registro de Azure cuando hay conectores nativo. Para obtener información adicional en el registro compatible, visitan tipos Hola preguntas más frecuentes.

>[!NOTE]
Aunque Azure registro integración es una solución disponible, hay costos de almacenamiento de Azure resultantes de almacenamiento de información del archivo de registro de hello.

Ayuda de la Comunidad está disponible a través de hello [foro de MSDN de integración de Azure registro](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Foro de Hello proporciona hello AzLog Comunidad Hola capacidad toosupport entre sí con preguntas, respuestas, consejos y sugerencias sobre cómo tooget más Hola de integración de registro de Azure. Además, el equipo de integración de registro de Azure de hello supervisa este foro y le ayudará a cada vez que se puede.

También puede abrir una [solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md). toodo, seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.

## <a name="next-steps"></a>Pasos siguientes
En este documento, eran tooAzure se ha introducido la integración de registro. toolearn más información sobre Azure registro integración y tipos de Hola de registros que se admiten, vea Hola recursos siguientes:

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324): Centro de descarga para obtener información, los requisitos del sistema y las instrucciones de instalación de Azure Log Integration.
* [Get started with Azure log integration](security-azure-log-integration-get-started.md) (Introducción a la integración de registros de Azure): este tutorial lo guía a través de la instalación de la integración de registros de Azure y de almacenamiento de Azure WAD, de registros de actividad de Azure, de alertas de Azure Security Center, y de registros de auditoría de Azure Active Directory.
* [Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : esta entrada de blog muestra cómo tooconfigure Azure registro toowork integración con soluciones de socios Splunk y ArcSight de HP, IBM QRadar. Este blog representa la posición actual sobre la configuración de soluciones de socios de Hola. En todos los casos, consulte documentación de solución de toopartner en primer lugar.
* [Alertas de actividad y ASC por encima de syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – este blog proporciona pasos de hello toosend alertas de actividad y el centro de seguridad de Azure a través de syslog tooQRadar
* [Preguntas más frecuentes sobre la integración de registro de Azure (P+F)](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre la integración de registro de Azure.
* [Integración de centro de seguridad de integración de registro de alertas con Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) : este documento muestra cómo toosync Azure Security Center alertas con la integración de registro de Azure.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
