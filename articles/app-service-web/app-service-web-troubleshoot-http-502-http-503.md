---
title: "aaaFix 502 puerta de enlace errónea, 503 Servicio disponible errores | Documentos de Microsoft"
description: "Solucionar los errores 502 Puerta de enlace no válida y 503 Servicio no disponible en su aplicación web hospedada en Servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 Puerta de enlace no válida, 503 Servicio no disponible, error 503, error 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Solucionar los errores HTTP de "502 Puerta de enlace no válida" y "503 Servicio no disponible" en las aplicaciones web de Azure
"502 Puerta de enlace no válida" y "503 Servicio no disponible" son errores comunes de su aplicación web hospedada en [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Este artículo le ayuda a solucionar estos errores.

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.

## <a name="symptom"></a>Síntoma
Al examinar la aplicación web de toohello, devuelve un HTTP error "502 pasarela incorrecta" o un HTTP error "503 Servicio no disponible".

## <a name="cause"></a>Causa
Con frecuencia este problema se debe a problemas en el nivel de la aplicación, como, por ejemplo:

* Solicitudes que tardan mucho tiempo
* Aplicaciones que hacen un uso elevado de memoria y CPU
* aplicación bloqueado debido a excepción de tooan.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Solución de problemas de errores de "503 Servicio no disponible" y pasos toosolve "502 puerta de enlace incorrecta"
El procedimiento de solución de problemas se puede dividir en tres tareas distintas, en orden secuencial:

1. [Observación y supervisión del comportamiento de la aplicación](#observe)
2. [Recopilación de datos](#collect)
3. [Mitigar el problema de Hola](#mitigate)

[Azure App Service Web Apps](/services/app-service/web/) ofrece diversas opciones en cada paso.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observación y supervisión del comportamiento de la aplicación
#### <a name="track-service-health"></a>Seguimiento del estado del servicio
Cada vez que hay una interrupción del servicio o una degradación del rendimiento, Microsoft Azure lo anuncia. Puede realizar el seguimiento del estado de saludo del servicio de hello en hello [Portal de Azure](https://portal.azure.com/). Para más información, consulte [Track service health](../monitoring-and-diagnostics/insights-service-health.md) (Seguimiento del estado del servicio).

#### <a name="monitor-your-web-app"></a>Supervisión de la aplicación web
Esta opción permite toofind out si la aplicación está teniendo problemas. En la hoja de la aplicación web, haga clic en hello **solicitudes y errores** icono. Hola **métrica** hoja mostrará todas las métricas de hello puede agregar.

Algunas de las métricas de Hola que podría interesarle toomonitor para su aplicación web son

* Espacio de trabajo de memoria promedio
* Tiempo medio de respuesta
* Tiempo de CPU
* Espacio de trabajo de memoria
* Solicitudes

![supervisar la aplicación web para solucionar los errores HTTP de 502 Puerta de enlace no válida y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Para más información, consulte:

* [Supervisión de Aplicaciones web en Servicio de aplicaciones de Azure](web-sites-monitor.md)
* [Recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Recopilación de datos
#### <a name="use-hello-azure-app-service-support-portal"></a>Usar hello Portal de soporte técnico de servicio de aplicación de Azure
Aplicaciones Web proporciona Hola capacidad tootroubleshoot problemas relacionados tooyour web app examinando los registros, registros de eventos, los volcados de proceso HTTP y más. Puede tener acceso a toda esta información con nuestro Portal de soporte técnico en **http://&lt;Nombre de la aplicación>.scm.azurewebsites.net/Support**.

portal de servicio de aplicaciones son compatibles con Azure Hola proporciona tres pestañas independientes toosupport Hola tres pasos de un escenario habitual de solución de problemas:

1. Observación del comportamiento actual
2. Analizar la recopilación de información de diagnóstico y ejecución Hola analizadores integrados
3. Mitigación

Si el problema de saludo se está realizando ahora mismo, haga clic en **analizar** > **diagnósticos** > **diagnosticar ahora** toocreate una sesión de diagnóstico para usted, que recopilará HTTP registra, registros del Visor de eventos, memoria volcados, registros de errores PHP y PHP procesan el informe.

Una vez que se recopilan los datos de hello, también se ejecutar un análisis de datos de Hola y proporcionarle un informe HTML.

En caso de que desea que toodownload Hola datos, de forma predeterminada, se almacenaría en la carpeta de D:\home\data\DaaS Hola.

Para obtener más información sobre el portal de servicio de aplicaciones son compatibles con Azure hello, consulte [tooSupport nuevas actualizaciones extensión del sitio para los sitios Web de Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Usar hello Kudu consola de depuración
El servicio Web Apps incluye una consola de depuración que puede usar para depurar, explorar o cargar archivos, e incluye también puntos de conexión JSON para obtener información sobre su entorno. Esto se denomina hello *Kudu consola* o hello *SCM panel* de la aplicación web.

Se puede tener acceso a este panel va toohello vínculo **https://&lt;el nombre de la aplicación >.scm.azurewebsites.net/**.

Algunos de los aspectos de Hola que Kudu ofrece son:

* Configuración del entorno de la aplicación
* transmisión de registro
* Volcado de diagnóstico
* Depuración de la consola en la que puede ejecutar cmdlets de Powershell y comandos básicos de DOS.

Otra característica útil de Kudu es que, en caso de que la aplicación es producir excepciones de primera oportunidad, puede usar Kudu y volcados de memoria de hello SysInternals herramienta Procdump toocreate. Estos archivos de volcado de memoria son instantáneas de proceso de Hola y a menudo le permitirá más complicados solucionar problemas relacionados con la aplicación web.

Para obtener más información sobre las características disponibles en Kudu, consulte [Herramientas en línea de Sitios web de Azure que debe conocer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Mitigar el problema de Hola
#### <a name="scale-hello-web-app"></a>Aplicación web de escala hello
En el servicio de aplicación de Azure, para aumentar el rendimiento y la capacidad, puede ajustar la escala de hello en el que se ejecuta la aplicación. El escalado de una aplicación web implica dos acciones relacionadas: cambiar la tooa del plan de servicio de aplicaciones más alto nivel de precios y configurar ciertas opciones de configuración una vez que haya cambiado toohello cuanto mayor sea el nivel de precios.

Para obtener más información sobre el escalado, consulte [Escalado de una aplicación web en Azure App Service](web-sites-scale.md).

Además, puede elegir toorun su aplicación en más de una instancia. Esto no solo le proporciona una mayor capacidad de procesamiento, sino también algo de tolerancia a errores. Si hello proceso deja de funcionar en una instancia, hello otra instancia todavía seguirá servir solicitudes.

Puede establecer Hola escalado toobe Manual o automático.

#### <a name="use-autoheal"></a>Uso de AutoHeal
AutoHeal recicla el proceso de trabajo de hello para la aplicación en función de la configuración que elija (como los cambios de configuración, las solicitudes, límites de memoria o el tiempo de hello es necesario tooexecute una solicitud). La mayoría de casos de hello, reciclar el proceso de hello es hello toorecover de manera más rápida de un problema. Aunque siempre puede reiniciar una aplicación Hola desde web directamente en hello Portal de Azure, AutoHeal hará automáticamente para usted. Todo lo que necesita toodo es agregar algunos de los desencadenadores en el archivo web.config de la raíz de hello para la aplicación web. Tenga en cuenta que esta configuración podría funcionar en hello igual manera, incluso si la aplicación no es un .net uno.

Para obtener más información, consulte [Recuperación automática de Sitios web de Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Reiniciar la aplicación web de Hola
Por lo general, suele ser hello toorecover de manera más sencilla de problemas puntuales. En hello [Portal de Azure](https://portal.azure.com/), en la hoja de la aplicación web, dispone de hello opciones toostop o reiniciar la aplicación.

 ![Reinicie los errores de aplicación toosolve HTTP 502 gateway erróneo y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

También puede administrar la aplicación web con Azure Powershell. Para obtener más información, vea [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).

