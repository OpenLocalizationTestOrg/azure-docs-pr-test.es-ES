---
title: "aaaAlerts validación en el centro de seguridad de Azure | Documentos de Microsoft"
description: Este documento le ayuda a alertas de seguridad de toovalidate hello en el centro de seguridad de Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Validación de alertas en Azure Security Center
Este documento le ayuda a saber cómo tooverify si el sistema está configurado correctamente para las alertas del centro de seguridad de Azure.

## <a name="what-are-security-alerts"></a>¿Qué son las alertas de seguridad?
Centro de seguridad recopila, analiza y se integra datos de registro de recursos de Azure, redes de Hola y soluciones de socios conectados, como soluciones de protección de firewall y de punto de conexión, toodetect y alerta toothreats automáticamente. Lectura [toosecurity responde y administrar las alertas en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para obtener más información acerca de las alertas de seguridad y lectura [descripción de las alertas de seguridad en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn más Hola diferentes tipos de alertas.

## <a name="alert-validation"></a>Validación de alertas
Después de instalar el agente de centro de seguridad en el equipo, siga los pasos de Hola a continuación desde el equipo de Hola donde desea toobe Hola atacada recursos de alerta de hello:

1. Copie el escritorio del equipo de un archivo ejecutable (por ejemplo calc.exe) toohello o en otro directorio de su comodidad.
2. Cambiar el nombre de este archivo demasiado**ASC_AlertTest_662jfi039N.exe**.
3. Abra símbolo del sistema de Hola y ejecute este archivo con un argumento (solo en un nombre de argumento falsa), como: *ASC_AlertTest_662jfi039N.exe - foo*
4. Espere 5 minutos too10 y abrir alertas del centro de seguridad. Se debería encontrar una alerta toofollowing similar uno:

    ![Validación de alertas](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Al revisar esta alerta, asegúrese de que habilita la auditoría de argumentos de campo de Hola aparece como true. Si muestra en false, deberá tooenable argumentos de línea de comandos de auditoría. Puede habilitar esta opción mediante Hola después de la línea de comandos:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Otras referencias
En este artículo se introdujo toohello proceso de validación de las alertas. Ahora que está familiarizado con esta validación, intente Hola siguientes artículos:

* [Toosecurity responde y administrar las alertas en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Obtenga información acerca de cómo toomanage alertas y responden toosecurity incidentes en el centro de seguridad.
* [Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md). Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Comprensión de las alertas de seguridad en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Obtenga información acerca de los tipos diferentes de hello de alertas de seguridad.
* [Guía de solución de problemas de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Obtenga información acerca de cómo problemas comunes de tootroubleshoot al centro de seguridad. 
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md). Busque las preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/). Encuentre artículos de blog sobre el cumplimiento y la seguridad de Azure.

