---
title: "aaaMonitoring y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría | Documentos de Microsoft"
description: "Este documento le ayuda a toouse Hola threat intelligence opción esté disponible en toomonitor de auditoría y seguridad de OMS y responde toosecurity alertas."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Supervisar y responder toosecurity alertas en Operations Management Suite solución de seguridad y auditoría
Este documento le ayuda a usar Hola amenaza intelligence opción disponible en toomonitor de auditoría y seguridad de OMS y responder toosecurity alertas.

## <a name="what-is-oms"></a>¿Qué es OMS?
Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local. Para obtener más información acerca de OMS, lea el artículo de hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Información sobre amenazas
En un entorno empresarial donde los usuarios tienen acceso amplio toohello red y utilizan una variedad de dispositivos tooconnect toocorporate datos, es imperativo que puede supervisar activamente los recursos y responder rápidamente toosecurity incidentes. Esto es especialmente importante desde la perspectiva de ciclo de vida de seguridad de hello porque algunos ciberseguridad amenazas no pueden generar alertas o las actividades sospechosas que pueden identificarse por los controles técnicos de seguridad tradicionales. 

Mediante el uso de hello **inteligencia sobre amenazas** opción disponibles en OMS seguridad y auditoría, los administradores de TI puede identificar las amenazas de seguridad en el entorno de hello, por ejemplo, identificar si un determinado equipo forma parte de un [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Los equipos pueden resultar nodos en una red de zombis cuando los atacantes instalación de forma ilegal malware que conecta secretamente este comando toohello el equipo y el control. También puede identificar posibles amenazas procedentes de canales de comunicación de tipo underground, como [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

En orden toobuild esta inteligencia sobre amenazas de seguridad de OMS y auditoría usan datos procedentes de varios orígenes en Microsoft. Auditoría y seguridad de OMS aprovechará esta amenazas potenciales de tooidentify de datos en su entorno.

panel de Hello inteligencia sobre amenazas está compuesto por tres opciones principales:

* Servidores con tráfico malintencionado saliente
* Tipos de amenazas detectadas
* Mapa de información sobre amenazas

> [!NOTE]
> Para obtener una descripción general de todas estas opciones, lea [Introducción a la solución Seguridad y auditoría de Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Responde toosecurity alertas
Uno de los pasos de Hola de un [respuesta a incidentes seguridad](https://technet.microsoft.com/library/cc512623.aspx) proceso es la gravedad de Hola de tooidentify de sistemas de poner en peligro de Hola. En esta fase debe realizar Hola siguientes tareas:

* Determinar la naturaleza de Hola de ataque de Hola
* Determinar el punto de ataque de Hola de origen
* Determinar la intención de Hola de ataque de Hola. Estaba dirigido específicamente a la información específica de tooacquire de organización de ataques de Hola o ha sido aleatorio?
* Identificar los sistemas de Hola que han estado en peligro
* Identificar los archivos de Hola que se ha obtenido acceso y determinan la confidencialidad de Hola de esos archivos

Puede aprovechar **inteligencia sobre amenazas** información de auditoría y seguridad de OMS toohelp de solución con estas tareas. Siga estos pasos hello tooaccess esto **inteligencia sobre amenazas** opciones:

1. Hola **Microsoft Operations Management Suite** panel principal haga clic en **seguridad y auditoría** icono.
   
    ![Seguridad y auditoría](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Hola **seguridad y auditoría** panel, verá hello **inteligencia sobre amenazas** opciones a la derecha hello, tal y como se muestra a continuación:
   
    ![Información sobre amenazas](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Estos tres iconos le dará una visión general de las amenazas actuales de Hola. Hola **servidor con tráfico malintencionado saliente** será capaz de tooidentify si hay cualquier equipo que se está supervisando (dentro o fuera de la red) que es enviar tráfico malintencionado toohello Internet. 

Hola **detecta los tipos de amenazas** icono muestra un resumen de las amenazas de hello actuales "en hello comodín", si hace clic en este icono podrá ver más detalles acerca de estas amenazas como se muestra a continuación:

![Tipos de amenazas detectadas](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

Para obtener más información sobre cada amenaza, haga clic en ella. ejemplo de Hola siguiente muestra más detalles sobre Botnet:

![más información sobre una amenaza](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Como se describe en el principio de Hola de esta sección, esta información puede ser muy útil durante un caso de respuesta a incidentes. También puede ser importante durante una investigación forense, en las que necesite toofind origen de Hola de ataque de hello, qué sistema se pone en peligro y Hola escala de tiempo. En este informe se pueden identificar fácilmente algunos detalles clave de ataque de hello, como: Hola origen del ataque de hello, Hola IP local que se ha puesto en peligro y Hola estado de la sesión actual de la conexión de Hola. 

Hola **mapa de inteligencia de amenazas** le ayudará a tooidentify Hola actual ubicaciones de todo el mundo de Hola que tienen tráfico malintencionado. Existen naranja (entrante) y (salientes) las flechas rojas en este mapa que identifican la dirección del tráfico de hello, si hace clic en una de estas flechas, mostrará tipo hello de hello y amenaza para la dirección del tráfico tal y como se muestra a continuación:

![mapa de información sobre amenazas](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Puede ver una demostración sobre cómo toouse esta capacidad durante una respuesta a incidentes proceso, inspeccionando la presentación de hello [mitigar las amenazas de seguridad del centro de datos interactiva investigando mediante Operations Management Suite](https://myignite.microsoft.com/videos/5000) entrega en Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Responde toodistinct IP malintencionado obtener acceso a
En algunos escenarios, puede que observe una posible dirección IP malintencionada a la que se accedió desde un equipo supervisado:

![mapa de información sobre amenazas](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Esta alerta etc. en Hola misma categoría, se generan a través de la seguridad de OMS mediante el aprovechamiento de [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Hola datos de inteligencia sobre amenazas es recopilada por Microsoft, así como adquiridas a través de los principales proveedores de inteligencia de amenazas. Estos datos se actualizan con frecuencia y adaptación mover toofast amenazas. Debido a la naturaleza tooits, debe combinarse con otras fuentes de información de seguridad al [investigando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) una alerta de seguridad. 

## <a name="customize-alerts-received-via-e-mail"></a>Personalización de las alertas que se reciben por correo electrónico

Puede personalizar los usuarios de la organización que recibirán notificación cuando Seguridad de OMS desencadena alertas de seguridad. Esta opción está disponible en la información general sobre / Hola de configuración en el panel de OMS:

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo hello toouse **inteligencia sobre amenazas** opción de auditoría y seguridad de OMS alertas de toosecurity toorespond de solución. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Introducción a la solución Seguridad y auditoría de Operations Management Suite](oms-security-getting-started.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

