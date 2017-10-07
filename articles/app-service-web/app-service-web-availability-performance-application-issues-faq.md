---
title: "Preguntas más frecuentes del aaaApplication rendimiento para aplicaciones web de Azure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre la disponibilidad, rendimiento y problemas de la aplicación en función de las aplicaciones Web de Hola de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Preguntas más frecuentes sobre el rendimiento de aplicaciones para aplicaciones web de Azure

Este artículo tiene toofrequently respuestas preguntas frecuentes (P+f) sobre problemas de rendimiento de aplicaciones para hello [característica de las aplicaciones Web de servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>¿Por qué mi aplicación es lenta?

Varios factores podría contribuir tooslow rendimiento de la aplicación. Para obtener los pasos detallados de solución de problemas, consulte [Solucionar los problemas de rendimiento reducido de aplicaciones web en Azure Web Apps](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>¿Cómo puedo solucionar problemas en un escenario de consumo elevado de CPU?

En algunos escenarios de consumo elevado de CPU, es probable que la aplicación realmente requiera más recursos informáticos. En ese caso, considere la posibilidad de escalar tooa mayor nivel de servicio para que la aplicación hello Obtiene todos los recursos de hello necesarios. En otras ocasiones, el consumo elevado de CPU podría deberse a un bucle incorrecto o una práctica de codificación. Obtener una visión general de lo que está desencadenando ese mayor consumo de CPU es un proceso de dos partes. En primer lugar, cree un volcado de proceso y, a continuación, analizar el volcado de memoria de proceso de Hola. Para más información, consulte la entrada de blog [Capture and analyze a dump file for high CPU consumption for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/) (Captura y análisis de un archivo de volcado de memoria para un consumo elevado de CPU para Web Apps).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>¿Cómo puedo solucionar problemas en un escenario de consumo elevado de memoria?

En algunos escenarios de consumo elevado de memoria, es probable que la aplicación realmente requiera más recursos informáticos. En ese caso, considere la posibilidad de escalar tooa mayor nivel de servicio para que la aplicación hello Obtiene todos los recursos de hello necesarios. En otras ocasiones, un error en código de hello puede provocar una pérdida de memoria. Una práctica de codificación también podría aumentar el consumo de memoria. Obtener una visión general de lo que está desencadenando ese mayor consumo de memoria es un proceso de dos partes. En primer lugar, cree un volcado de proceso y, a continuación, analizar el volcado de memoria de proceso de Hola. Diagnóstico de bloqueo de hello Galería de extensiones de sitio de Azure puede realizar de manera eficaz estos dos pasos. Para más información, consulte la entrada de blog [How to capture and analyze dump for intermittent High Memory on Azure Web App](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/) (Captura y análisis de un archivo de volcado de memoria para un consumo elevado intermitente de memoria para Web Apps).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>¿Cómo se puede automatizar App Service Web Apps mediante PowerShell?

Puede usar toomanage de cmdlets de PowerShell y mantener aplicaciones de servicio de aplicaciones web. En la entrada de blog [automatizar aplicaciones web hospedadas en el servicio de aplicación de Azure mediante PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), se describe cómo tareas comunes de toouse basada en el Administrador de recursos de Azure PowerShell cmdlets tooautomate. entrada de blog de Hello también incluye código de ejemplo para diversas tareas de administración de aplicaciones web. Para obtener descripciones y sintaxis de todos los cmdlets de App Service Web Apps, consulte [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>¿Cómo se pueden ver los registros de eventos de mi aplicación web?

registros de eventos de la aplicación web de tooview:

1. Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. En el menú de hello, seleccione **consola de depuración** > **CMD**.
3. Seleccione hello **LogFiles** carpeta.
4. registros de eventos de tooview, seleccione icono de lápiz Hola siguiente demasiado**eventlog.xml**.
5. registros de hello toodownload, ejecute el cmdlet de PowerShell de hello `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>¿Cómo se puede capturar un volcado de memoria de modo de usuario de la aplicación web?

toocapture un volcado de memoria de modo de usuario de la aplicación web:

1. Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Seleccione hello **Process Explorer** menú.
3. Menú contextual hello **w3wp.exe** proceso o el proceso de trabajo Web.
4. Seleccione **Download Memory Dump** > **Full Dump** (Descargar volcado de memoria > Volcado de memoria completo).

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>¿Cómo se puede ver la información de nivel de proceso para mi aplicación web?

Tiene dos opciones para ver la información de nivel de proceso para la aplicación web:

*   Hola portal de Azure:
    1. Abra hello **Process Explorer** para la aplicación web de Hola.
    2. detalles de hello toosee, seleccione hello **w3wp.exe** proceso.
*   En la consola de Hola Kudu:
    1. Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Seleccione hello **Process Explorer** menú.
    3. Para hello **w3wp.exe** proceso, seleccione **propiedades**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Cuando examina aplicación toomy, veo "Error 403 - esta aplicación web se detuvo." ¿Cómo se resuelve este problema?

Este error pueden deberse a tres condiciones:

* aplicación web de Hello ha alcanzado un límite de facturación y el sitio se ha deshabilitado.
* se ha detenido la aplicación web de Hello en el portal de Hola.
* aplicación web de Hello ha alcanzado un límite de cuota de recursos que se puede aplicar tooa gratuito o compartido el plan de servicio de escala.

toosee cuál es la causa error hello y problema de hello tooresolve, Hola siga los pasos de [aplicaciones Web: "Error 403: esta aplicación web se detuvo"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>¿Dónde puedo obtener más información sobre cuotas y límites de los diversos planes de App Service?

Para más información sobre cuotas y límites, consulte [Límites de App Service](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>¿Cómo se puede reducir el tiempo de respuesta de Hola para hello primera solicitud después de tiempo de inactividad?

De forma predeterminada, las aplicaciones web se descargan si están inactivas durante algún tiempo. De esta manera, el sistema de hello puede conservar los recursos. el inconveniente de Hello es que hello respuesta toohello primera solicitud después de descargar la aplicación web de hello es más grande, tooallow Hola tooload de aplicación web e iniciar el envío de respuestas. En los planes de servicio básico y estándar, puede activar hello **Always On** configuración tookeep Hola aplicación siempre se cargan. Esto elimina el tiempo de carga después de aplicación hello está inactivo. Hola toochange **Always On** configuración:

1. Hola portal de Azure, vaya tooyour web app.
2. Seleccione **Configuración de la aplicación**.
3. Para **Siempre activado**, seleccione **Activado**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>¿Cómo se activa el seguimiento de solicitudes con error?

tooturn sobre el seguimiento de solicitudes con error:

1. Hola portal de Azure, vaya tooyour web app.
3. Seleccione **Toda la configuración** > **Registros de diagnóstico**.
4. En **Seguimiento de solicitudes con error**, seleccione **Activado**.
5. Seleccione **Guardar**.
6. En la hoja de la aplicación hello web, seleccione **herramientas**.
7. Seleccione **Visual Studio Online**.
8. Si no se Hola configuración **en**, seleccione **en**.
9. Seleccione **Ir**.
10. Seleccione **Web.config**.
11. En system.webServer, agregue esta configuración (toocapture una dirección URL específica):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. problemas de rendimiento lento de tootroubleshoot, agregue esta configuración (si Hola solicitud de captura está tardando más de 30 segundos):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. Hola toodownload no pudo seguimientos de solicitud, en hello [portal](https://portal.azure.com), vaya sitio Web de tooyour.
15. Seleccione **Herramientas** > **Kudu** > **Ir**.
18. En el menú de hello, seleccione **consola de depuración** > **CMD**.
19. Seleccione hello **LogFiles** y, a continuación, seleccione Hola carpeta con un nombre que comienza con **W3SVC**.
20. archivo XML toosee hello, icono de lápiz que seleccione Hola.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Consulte el mensaje de bienvenida de "proceso de trabajo solicitó el reciclaje de vencimiento too'Percent memoria ' límite." ¿Cómo se soluciona este problema?

Hola máxima cantidad de memoria disponible para un proceso de 32 bits (incluso en un sistema operativo de 64 bits) es 2 GB. De forma predeterminada, el proceso de trabajo de Hola se establece too32 bits en el servicio de aplicaciones (por compatibilidad con aplicaciones web heredados).

Considere la posibilidad de procesos too64 bits por lo que puede aprovechar las ventajas de hello adicionales de memoria disponible en el rol de trabajo Web. Esto desencadena un reinicio de la aplicación web, por lo que programe en consecuencia.

Tenga en cuenta que un entorno de 64 bits requiere un plan de servicio Básico o Estándar. Los planes Gratis y Compartido siempre se ejecutan en un entorno de 32 bits.

Para más información, consulte [Configuración de aplicaciones web en Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>¿Por qué se agota el tiempo de espera de la solicitud después de 240 segundos?

Azure Load Balancer tiene un valor de tiempo de expiración de inactividad predeterminado de cuatro minutos. Por lo general, suele ser un límite de tiempo de respuesta razonable para una solicitud web. Si la aplicación web requiere un procesamiento en segundo plano, se recomienda el uso de WebJobs de Azure. aplicación web de Azure de Hello puede llamar a trabajos Web y recibir una notificación cuando haya finalizado el procesamiento en segundo plano. Puede elegir entre varios métodos para usar WebJobs, incluidos las colas y los desencadenadores.

WebJobs está pensado para el procesamiento en segundo plano. Puede realizar tanto procesamiento en segundo plano como desee en un WebJob. Para más información, consulte [Ejecutar tareas en segundo plano con WebJobs](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>Las aplicaciones de ASP.NET Core hospedadas en App Service a veces dejan de responder. ¿Cómo se corrige este problema?

Un problema conocido con un anteriores [versión Kestrel](https://github.com/aspnet/KestrelHttpServer/issues/1182) puede provocar una aplicación de ASP.NET Core 1.0 que se hospeda en servicio de aplicaciones toointermittently no responda. También puede ver este mensaje: "hello especifica aplicación CGI encontró un proceso de hello servidor terminada hello y error."

Este problema está corregido Kestrel versión 1.0.2. Esta versión se incluye en la actualización de ASP.NET Core 1.0.3 Hola. tooresolve este problema, asegúrese de actualizar su toouse de dependencias de aplicación Kestrel versión 1.0.2. Como alternativa, puede usar uno de dos soluciones alternativas que se describen en la entrada de blog de hello [problemas de rendimiento lento de ASP.NET Core 1.0 en aplicaciones de servicio de aplicaciones web](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>No se encuentra Mis archivos de registro en la estructura de archivos de Hola de mi aplicación web. ¿Cómo se pueden encontrar?

Si usa características de caché Local de Hola de servicio de aplicaciones, carpetas de datos para la instancia de servicio de aplicaciones y estructura de carpetas de Hola de hello LogFiles se ven afectadas. Cuando se utiliza la memoria caché Local, se crean subcarpetas en carpetas de datos y almacenamiento de hello LogFiles. uso de las subcarpetas de Hola Hola nomenclatura patrón "identificador" + marca de tiempo. Cada subcarpeta corresponde la instancia de máquina virtual de tooa en qué Hola aplicación web se está ejecutando o se ha ejecutado.

toodetermine independientemente de si se usa la memoria caché Local, compruebe el servicio de aplicación **configuración de la aplicación** ficha. Si se utiliza la memoria caché Local, configuración de la aplicación de Hola `WEBSITE_LOCAL_CACHE_OPTION` se establece demasiado`Always`. Para obtener más información acerca de la memoria caché Local, vea hello [información general de la caché Local del servicio de aplicación](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Si no se está usando la memoria caché local y está experimentando este problema, envíe una solicitud de soporte técnico.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Aparece el mensaje de Hola "fue un intento realizado tooaccess un socket de una manera prohibida por los permisos de acceso." ¿Cómo se resuelve este problema?

Este error suele producirse si se agotan hello las conexiones TCP salientes en la instancia de la máquina virtual de Hola. En el servicio de aplicaciones, los límites se aplican para el número máximo de Hola de conexiones salientes que pueden realizarse para cada instancia de máquina virtual. Para más información, consulte la sección [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits) (Límites numéricos entre máquinas virtuales).

Este error también puede producirse si intenta tooaccess una dirección local de la aplicación. Para más información, consulte la sección [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests) (Peticiones de direcciones locales).

Para obtener más información acerca de las conexiones salientes en la aplicación web, vea Hola entrada de blog sobre [sitios Web de tooAzure de las conexiones de salida](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>¿Cómo se usa depuración de Visual Studio tooremote mi aplicación de servicio de aplicaciones web?

Para obtener un tutorial detallado que muestra cómo toodebug su aplicación web mediante Visual Studio, vea [remoto depurar la aplicación de servicio de aplicaciones web](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
