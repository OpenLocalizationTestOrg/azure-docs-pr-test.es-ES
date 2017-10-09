---
title: "aaaTroubleshooting ningún dato - Application Insights para .NET"
description: "¿No ve los datos en Azure Application Insights? Pruebe aquí."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Solución de problemas cuando no hay datos: Application Insights para .NET
## <a name="some-of-my-telemetry-is-missing"></a>Falta parte de mi telemetría
*En Application Insights, sólo vea una fracción de los eventos de hello generados por la aplicación.*

* Si ve constantemente Hola mismo fracción, su probablemente due tooadaptive [muestreo](app-insights-sampling.md). tooconfirm, abra búsqueda (desde la hoja de información general de hello) y buscar en una instancia de una solicitud u otro evento. En parte inferior de Hola de sección de propiedades de hello haga clic en detalles de la propiedad completa de tooget "...". Si Recuento de solicitudes > 1, hay un muestreo en curso. 
* De lo contrario, es posible que se esté aproximando a un [límite de velocidad de datos](app-insights-pricing.md#limits-summary) para su plan de precios. Estos límites se aplican por minuto.

## <a name="no-data-from-my-server"></a>No hay datos de mi servidor
*He instalado mi aplicación en el servidor web y ahora no veo ninguna telemetría procedente de ella. Funcionaba correctamente en mi equipo de desarrollo.*

* Probablemente sea un problema de firewall. [Establecer las excepciones del firewall para los datos de Application Insights toosend](app-insights-ip-addresses.md).

*¿ [Instalado el Monitor de estado](app-insights-monitor-performance-live-website-now.md) en mi servidor toomonitor existente las aplicaciones web. No se ve ningún resultado.*

* Consulte [Solución de problemas del Monitor de estado](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>No hay ninguna opción "Agregar Application Insights" en Visual Studio
*Cuando hago clic con el botón derecho en un proyecto existente en el Explorador de soluciones, no veo ninguna opción de Application Insights.*

* No todos los tipos de proyecto .NET son compatibles con herramientas de Hola. Se admiten los proyectos WCF y Web. Para otros tipos de proyecto, como aplicaciones de escritorio o el servicios, se puede seguir haciendo [agregar manualmente un proyecto de aplicación visión SDK tooyour](app-insights-windows-desktop.md).
* Asegúrese de que tiene [Visual Studio 2013 Update 3 o posterior](http://go.microsoft.com/fwlink/?LinkId=397827). Viene preinstalado con las herramientas de análisis de desarrollador, logrando así Hola Application Insights SDK.
* Seleccione **Herramientas**, **Extensiones y actualizaciones** y compruebe que **Developer Analytics Tools** está instalado y habilitado. Si es así, haga clic en **actualizaciones** toosee si hay una actualización disponible.
* Abrir el cuadro de diálogo de hello nuevo proyecto y elija aplicación Web ASP.NET. Si ve hello no existe la opción de Application Insights, a continuación, se instalan herramientas de Hola. Si no es así, pruebe a desinstalar y, a continuación, volver a instalar herramientas de hello Application Insights.

## <a name="q02"></a>Error al agregar Application Insights
*Cuando intento proyecto existente de tooadd Application Insights tooan, veo un mensaje de error.*

Causas probables:

* Un error de comunicación con el portal de Application Insights Hola; o
* hay algún problema con su cuenta de Azure,
* Solo tiene [suscripción toohello de acceso de lectura o el grupo donde estaba intentando nuevo recurso de toocreate hello](app-insights-resources-roles-access-control.md).

Solución:

* Compruebe que proporciona credenciales de inicio de sesión para el derecho de hello cuenta de Azure. 
* En el explorador, compruebe que tiene acceso a toohello [portal de Azure](https://portal.azure.com). Abra Configuración y compruebe si hay alguna restricción.
* [Proyecto existente de agregar Application Insights tooyour](app-insights-asp-net.md): en el Explorador de soluciones, haga clic con el proyecto y elija "Agregar Application Insights".
* Si sigue sin funcionar, siga hello [procedimiento manual](app-insights-windows-services.md) tooadd un recurso en el portal de hello y, a continuación, agregue el proyecto de tooyour del SDK de Hola. 

## <a name="emptykey"></a>Aparece el mensaje de error "La clave de instrumentación no puede estar vacía".
Parece que algo salió mal durante la instalación de Application Insights o puede ser un adaptador del registro.

En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y elija **Application Insights > Configurar Application Insights**. Obtendrá un cuadro de diálogo que le invita toosign en tooAzure y cree un recurso de Application Insights, o volver a utilizar uno existente.

## <a name="NuGetBuild"></a> "Faltan paquetes NuGet" en el servidor de compilación
*Todo lo que crea Aceptar cuando estoy la depuración en mi equipo de desarrollo, pero obtengo un error de NuGet en el servidor de compilación Hola.*

Consulte [Restauración de paquetes NuGet](http://docs.nuget.org/Consume/Package-Restore) y [Restauración automática de paquetes](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Falta tooopen de comando de menú Application Insights de Visual Studio
*Al hacer clic con el botón derecho en el Explorador de soluciones del proyecto, no se ve ningún comando de Application Insights o no se ve un comando Abrir Application Insights.*

Causas probables:

* Si ha creado manualmente los recursos de Application Insights de Hola o proyecto hello es de un tipo que no es compatible con herramientas de Application Insights Hola.
* herramientas de análisis de desarrollador de Hello están deshabilitadas en la Visual Studio. 
* Visual Studio es anterior a la actualización 3 de 2013.

Solución:

* Compruebe que la versión de Visual Studio sea la actualización 3 de 2013 o posterior.
* Seleccione **Herramientas**, **Extensiones y actualizaciones** y compruebe que **Developer Analytics Tools** está instalado y habilitado. Si es así, haga clic en **actualizaciones** toosee si hay una actualización disponible.
* En el Explorador de soluciones, haga clic con el botón derecho en el proyecto. Si ve el comando hello **Application Insights > configurar Application Insights**, utilice tooconnect el recurso de toohello proyecto Hola servicio Application Insights.

En caso contrario, el tipo de proyecto no es compatible directamente con herramientas de Application Insights Hola. toosee la telemetría, inicio de sesión toohello [portal de Azure](https://portal.azure.com), elija Application Insights en la barra de navegación izquierda de Hola y seleccione la aplicación.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>'Acceso denegado' al abrir Application Insights desde Visual Studio
*comando de menú 'Abrir Application Insights' Hello toma me toohello portal de Azure, pero obtengo un error "acceso denegado".*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Hola inicio de sesión de Microsoft que utilizó por última vez en el explorador predeterminado no tiene acceso demasiado[Hola recursos que se crean al agregar Application Insights toothis aplicación](app-insights-asp-net.md). Hay dos causas probables: 

* ¿Tiene más de una cuenta de Microsoft: puede ser un trabajo y una cuenta Microsoft personal? Hello inicio de sesión de que utilizó por última vez en el explorador predeterminado era para una cuenta diferente de Hola que tiene acceso demasiado[agregar Application Insights toohello proyecto](app-insights-asp-net.md). 
  
  * Corrección: Haga clic en su nombre en parte superior derecha de la ventana del explorador de Hola y cerrar la sesión. A continuación, inicie sesión con cuenta de hello que tenga acceso. A continuación, en la barra de navegación izquierda de hello, haga clic en información de la aplicación y seleccione la aplicación.
* Alguien agrega el proyecto toohello de Application Insights y han olvidado toogive se [grupo de recursos de acceso toohello](app-insights-resources-roles-access-control.md) en que se creó. 
  
  * Corrección: Si utiliza una cuenta profesional, pueden agregar también toohello equipo; o bien, puede conceder también acceso individual toohello grupo de recursos.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>'No se encuentra ningún activo' al abrir Application Insights desde Visual Studio
*comando de menú 'Abrir Application Insights' Hello toma me toohello portal de Azure, pero obtengo un error 'no se encuentra activo'.*

Causas probables:

* se ha eliminado el recurso de Application Insights para su aplicación Hola; o
* clave de instrumentación de Hello estaba establecida o cambiada en ApplicationInsights.config editando directamente, sin actualizar el archivo de proyecto de hello. 

clave de instrumentación de Hello en los controles de ApplicationInsights.config donde se envía la telemetría de Hola. Una línea en el archivo de proyecto de hello controla qué recurso se abre cuando se usa el comando hello en Visual Studio. 

Solución:

* En el Explorador de soluciones, haga clic en proyecto de Hola y elija Application Insights, configurar Application Insights. En el cuadro de diálogo de hello, puede elegir tooan de telemetría toosend recurso existente o cree uno nuevo. O:
* Abrir el recurso de hello directamente. Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com), haga clic en información de la aplicación en la barra de navegación izquierda de hello y, a continuación, seleccione la aplicación.

## <a name="where-do-i-find-my-telemetry"></a>¿Dónde se encuentra la telemetría?
*Se han firmado en toohello [portal de Microsoft Azure](https://portal.azure.com), y que me interesa en hello Azure panel principal. ¿Dónde se encuentran los datos de Application Insights?*

* En la barra de navegación izquierda de hello, haga clic en Application Insights, a continuación, el nombre de la aplicación. Si no tiene ningún proyecto no existe, necesita demasiado[agregar o configurar Application Insights en el proyecto web](app-insights-asp-net.md).
  
    Ahí verá algunos gráficos de resumen. Puede hacer clic en ellos toosee más detalles.
* En Visual Studio, mientras está depurando la aplicación, haga clic en botón de Application Insights Hola.

## <a name="q03"></a> No hay datos de servidor (o ningún tipo de datos)
*Ejecuté mi aplicación y, a continuación, abre el servicio de Application Insights de Hola en Microsoft Azure, pero todos los gráficos se muestran de Hola ' aprender cómo toocollect...' o 'No está configurado.'* O bien, *solo vista de página y datos de usuario, pero no hay datos de servidor.*

* Ejecute la aplicación en modo de depuración en Visual Studio (F5). Usar aplicación hello así como toogenerate algunos telemetría. Compruebe que puede ver los eventos registrados en la ventana de salida de hello Visual Studio. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* En el portal de Application Insights hello, abra [búsqueda diagnóstico](app-insights-diagnostic-search.md). Los datos suelen aparecer aquí en primer lugar.
* Haga clic en el botón de actualización de Hola. hoja de Hello propio actualiza periódicamente, pero también se puede hacer manualmente. intervalo de actualización de Hello es más larga para intervalos de tiempo mayor.
* Compruebe que coinciden con las claves de instrumentación de Hola. En la hoja principal de hello para la aplicación de portal de Application Insights hello, Hola **Essentials** lista desplegable, examine **clave de instrumentación**. A continuación, en el proyecto en Visual Studio, abra ApplicationInsights.config y busque hello `<instrumentationkey>`. Compruebe que Hola dos claves son iguales. Si no es así:
  
  * En el portal de hello, haga clic en Application Insights y buscar recursos de aplicación Hola con tecla Hola; o
  * En Visual Studio Solution Explorer, haga clic en proyecto de Hola y elija Application Insights, configurar. Restablecer hello toosend telemetría toohello derecho recurso.
  * Si no puede encontrar Hola claves coincidentes, compruebe que está usando Hola mismo credenciales de inicio de sesión en Visual Studio como en el portal de toohello.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* Hola [panel principal de Microsoft Azure](https://portal.azure.com), mire el mapa de estado del servicio de Hola. Si hay alguna alerta indicaciones, espere hasta que hayan devuelto tooOK y, a continuación, cierre y vuelva a abrir la hoja de la aplicación Application Insights.
* Compruebe también [nuestro blog de estado](http://blogs.msdn.com/b/applicationinsights-status/).
* ¿Ha escrito ningún código de hello [servidor SDK](app-insights-api-custom-events-metrics.md) que podría cambiar clave de instrumentación de hello en `TelemetryClient` instancias o en `TelemetryContext`? ¿O ha escrito una [configuración de filtro o muestreo](app-insights-api-filtering-sampling.md) que pueda estar filtrando demasiado?
* Si edita ApplicationInsights.config, compruebe con cuidado la configuración Hola de [TelemetryInitializers y TelemetryProcessors](app-insights-api-filtering-sampling.md). Un parámetro o un tipo denominado incorrectamente no puede provocar Hola SDK toosend ningún dato.

## <a name="q04"></a>No hay datos en Vistas de página, Explorador o Uso
*Ver datos en tiempo de respuesta de servidor y gráficos de solicitudes de servidor, pero ningún dato en tiempo de carga de la vista de página o en el Explorador de Hola o las hojas de uso.*

datos de Hello proceden de las secuencias de comandos en las páginas web Hola. 

* Si agregó tooan Application Insights existente proyecto web, [tiene scripts de hello tooadd manualmente](app-insights-javascript.md).
* Asegúrese de que Internet Explorer no muestra el sitio en modo de compatibilidad.
* Usar la característica de depuración del explorador de hello (F12 en algunos exploradores, a continuación, elija red) tooverify que se envían datos demasiado`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>No hay datos de excepción o dependencia
Consulte [telemetría de dependencias](app-insights-asp-net-dependencies.md) y [telemetría de excepciones](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Sin datos de rendimiento
Los datos de rendimiento (CPU, velocidad de E/S, etc.) están disponibles para [servicios web de Java](app-insights-java-collectd.md), [aplicaciones de escritorio de Windows](app-insights-windows-desktop.md), [servicios y aplicaciones web IIS si instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md) y [Azure Cloud Services](app-insights-azure.md). Los encontrará en la sección Configuración > Servidores.

No están disponible para los sitios web de Azure.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>No hay datos (servidor) desde que publicó Hola toomy servidor de aplicación
* Compruebe que ha copiado realmente Hola todos los Microsoft. Archivos DLL de ApplicationInsights toohello server, junto con Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* En el firewall, es posible que tenga demasiado[abrir algunos puertos TCP](app-insights-ip-addresses.md#data-access-api).
* Si tiene toouse un toosend proxy fuera de la red corporativa, establezca [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) en el archivo Web.config
* Windows Server 2008: Asegúrese de que ha instalado Hola siguiendo las actualizaciones: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>He usado toosee datos, pero se ha detenido
* Comprobar hello [estado blog](http://blogs.msdn.com/b/applicationinsights-status/).
* ¿Ha alcanzado su cuota mensual de puntos de datos? Abra Hola configuración/cuotas y precios toofind out. Si es así, puede actualizar el plan o pagar para obtener capacidad adicional. Vea hello [precios esquema](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>No veo todos los datos de hello que estoy esperando
Si la aplicación envía una gran cantidad de datos y se usa hello Application Insights SDK para ASP.NET versión 2.0.0-beta3 o una versión posterior, Hola [muestreo adaptativo](app-insights-sampling.md) característica puede funcionar y enviar solamente un porcentaje de la telemetría. 

Se puede deshabilitar, pero no se recomienda. El muestreo está diseñado para que la telemetría relacionada se transmita correctamente, con fines de diagnóstico. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Datos geográficos incorrectos en la telemetría de usuario
dimensiones de país, región y ciudad Hola se derivan de direcciones IP y no siempre están precisas.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Excepción "Método no encontrado" en la ejecución en Servicios en la nube de Azure
¿Ha realizado la compilación para .NET 4.6? 4.6 no se admite automáticamente en los roles de Servicios en la nube de Azure. [Instale 4.6 en cada rol](../cloud-services/cloud-services-dotnet-install-dotnet.md) antes de ejecutar la aplicación.

## <a name="still-not-working"></a>Sigue sin funcionar...
* [Foro de Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

