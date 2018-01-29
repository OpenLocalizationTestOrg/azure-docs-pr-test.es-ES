---
title: "Detección inteligente: Security Detection Pack con Azure Application Insights | Microsoft Docs"
description: Supervise las aplicaciones con Azure Application Insights para detectar posibles problemas de seguridad.
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: mbullwin
ms.openlocfilehash: 837525d70f28c0710b8a8b86d411a7854402207f
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="application-security-detection-pack-preview"></a>Application Security Detection Pack (versión preliminar)

Application Insights analiza automáticamente la telemetría generada por la aplicación y detecta posibles problemas de seguridad. Esta funcionalidad permite identificar los posibles problemas de seguridad y controlarlos corrigiendo la aplicación o tomando las medidas de seguridad necesarias.

Esta característica no requiere ninguna configuración especial, excepto [configurar la aplicación para que envíe la telemetría](https://docs.microsoft.com/azure/application-insights/app-insights-usage-overview).

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a>¿Cuándo recibiré este tipo de notificación de detección inteligente?
Se detectan tres tipos de problemas de seguridad:
1. Acceso a direcciones URL no seguro: se está accediendo a una dirección URL en la aplicación a través de HTTP y HTTPS. Normalmente, una dirección URL que acepta solicitudes HTTPS no debe aceptar solicitudes HTTP. Esto puede indicar un problema de seguridad o errores en la aplicación.
2. Formulario no seguro: un formulario (u otra solicitud "POST") en la aplicación usa HTTP en lugar de HTTPS. El uso de HTTP puede poner en peligro los datos del usuario que envía el formulario.
3. Actividad del usuario sospechosa: el mismo usuario está accediendo a la aplicación desde varios países aproximadamente al mismo tiempo. Por ejemplo, el mismo usuario accedió a la aplicación desde España y desde Estados Unidos durante la misma hora. Esta detección indica un intento de acceso a la aplicación potencialmente malintencionado.

## <a name="does-my-app-definitely-have-a-security-issue"></a>¿Significa esto que la aplicación tiene un problema de seguridad?
No, una notificación no significa que la aplicación tenga un problema de seguridad. En muchos casos, una detección de cualquiera de los escenarios anteriores puede indicar un problema de seguridad. Sin embargo, la detección puede tener una justificación comercial natural y se puede omitir.

## <a name="how-do-i-fix-the-insecure-url-access-detection"></a>¿Cómo se soluciona una detección de "Acceso a direcciones URL no seguro"?
1. **Evaluación de errores.** La notificación proporciona el número de usuarios que accedieron a direcciones URL no seguras y la dirección URL más afecta por acceso no seguro. Esto puede ayudarlo a asignar una prioridad al problema.
2. **Ámbito.** ¿Qué porcentaje de usuarios obtienen acceso a direcciones URL no seguras? ¿Cuántas direcciones URL se vieron afectadas? Esta información puede obtenerse de la notificación.
3. **Diagnóstico.** La detección proporciona la lista de solicitudes no seguras y la lista de direcciones URL y usuarios que se vieron afectados, para ayudar a efectuar un diagnóstico exhaustivo del problema.

## <a name="how-do-i-fix-the-insecure-form-detection"></a>¿Cómo se soluciona la detección "Formulario no seguro"?
1. **Evaluación de errores.** La notificación informa del número de formularios no seguros y del número de usuarios cuyos datos estuvieron potencialmente en peligro. Esto puede ayudarlo a asignar una prioridad al problema.
2. **Ámbito.** ¿Qué formulario estuvo implicado en el mayor número de transmisiones no seguras y cuál es la distribución de las transmisiones no seguras a lo largo del tiempo? Esta información puede obtenerse de la notificación.
3. **Diagnóstico.** La detección proporciona la lista de formularios no seguros y desglosa el número de transmisiones no seguras de cada formulario, para ayudar a efectuar un diagnóstico exhaustivo del problema.

## <a name="how-do-i-fix-the-suspicious-user-activity-detection"></a>¿Cómo se soluciona la detección "Actividad del usuario sospechosa"?
1. **Evaluación de errores.** La notificación proporciona el número de los diferentes usuarios que exhibieron este comportamiento sospechoso. Esto puede ayudarlo a asignar una prioridad al problema.
2. **Ámbito.** ¿Desde qué países se originó la solicitud sospechosa? ¿Qué usuario era más sospechoso? Esta información puede obtenerse de la notificación.
3. **Diagnóstico.** La detección proporciona la lista de usuarios sospechosos y la lista de países para cada usuario, para ayudarle a efectuar un diagnóstico exhaustivo del problema.
