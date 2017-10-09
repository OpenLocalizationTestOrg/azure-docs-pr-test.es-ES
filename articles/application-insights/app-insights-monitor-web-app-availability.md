---
title: aaaMonitor disponibilidad y capacidad de respuesta de cualquier sitio web | Documentos de Microsoft
description: Configure pruebas web en Application Insights. Obtenga alertas si un sitio web deja de estar disponible o responde con lentitud.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Supervisión de la disponibilidad y la capacidad de respuesta de cualquier sito web
Después de implementar la aplicación web o el servidor de tooany del sitio web, puede configurar pruebas toomonitor su disponibilidad y capacidad de respuesta. [Azure Application Insights](app-insights-overview.md) envía las solicitudes web tooyour aplicación a intervalos regulares desde puntos de Hola a todos. Le alerta si la aplicación no responde o lo hace lentamente.

Se pueden definir las pruebas de disponibilidad para cualquier HTTP u Hola de extremo HTTPS que sea accesible desde internet público. No tiene nada de nada tooadd toohello sitio de web que se está probando. Incluso no tiene toobe su sitio: puede probar un servicio de API de REST de los que dependen.

Hay dos tipos de pruebas de disponibilidad:

* [Prueba de ping de la dirección URL](#create): una prueba sencilla que se puede crear en hello portal de Azure.
* [Prueba web de varios pasos](#multi-step-web-tests): que se crea en Visual Studio Enterprise y carga toohello portal.

Puede crear las pruebas de disponibilidad too25 por cada recurso de la aplicación.

## <a name="create"></a>1. Apertura de un recurso para los informes de pruebas de disponibilidad

**Si ya ha configurado Application Insights** para la aplicación web, abra su recurso de Application Insights en hello [portal de Azure](https://portal.azure.com).

**O bien, si desea toosee los informes en un nuevo recurso,** registrarse demasiado[Microsoft Azure](http://azure.com), vaya toohello [portal de Azure](https://portal.azure.com)y crear un recurso de Application Insights.

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Haga clic en **todos los recursos** tooopen hoja de información general de hello para el nuevo recurso de Hola.

## <a name="setup"></a>2. Creación de una prueba de ping de la dirección URL
Abra la hoja de la disponibilidad de Hola y agregue una prueba.

![Relleno Hola al menos la dirección URL del sitio Web](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **dirección URL de Hello** puede ser cualquier página web que desee tootest, pero debe ser visible desde Hola internet pública. dirección URL de Hello puede incluir una cadena de consulta. Así, por ejemplo, se puede ejercitar un poco la base de datos. Si Hola URL resuelve tooa redirección, se siga la too10 redirecciones.
* **Analizar las solicitudes dependientes**: si se activa esta opción, prueba Hola solicita imágenes, scripts, archivos de estilo y otros archivos que forman parte de la página web de hello sometida a prueba. Hello tiempo de respuesta grabada incluye Hola tiempo tooget estos archivos. se produce un error en la prueba de Hola si todos estos recursos no se puede descargar correctamente en tiempo de espera de Hola de pruebas completo Hola. 

    Si no se activa la opción de hello, prueba Hola solo solicita archivo hello en dirección URL de Hola que especificó.
* **Habilitar reintentos**: si se activa esta opción, cuando se produce un error en la prueba de hello, se reintenta después de un intervalo más corto. Se notifica un error únicamente si los tres intentos sucesivos producen un error. Las pruebas siguientes, a continuación, se realizan con frecuencia de prueba habituales de Hola. Vuelva a intentar se suspenderá temporalmente hasta que se consiga siguiente Hola. Esta regla se aplica independientemente en cada ubicación de la prueba. Se recomienda esta opción. Como media, cerca del 80 % de los errores desaparecen al reintentar.
* **Frecuencia de prueba**: establece la frecuencia con hello prueba se ejecuta en cada ubicación de la prueba. Con una frecuencia de cinco minutos y cinco ubicaciones de prueba, el sitio se prueba, de media, cada minuto.
* **Ubicaciones de prueba** son Hola coloca que nuestros servidores envían dirección URL de tooyour de las solicitudes web. Elija más de una de tal forma que pueda distinguir los problemas del sitio web a partir de los problemas de red. Puede seleccionar las ubicaciones de too16.
* **Criterios de éxito**:

    **Tiempo de espera de pruebas**: disminuir este toobe valor le alerte lentitud. prueba de Hola se cuenta como un error si no se recibieron respuestas de Hola desde su sitio dentro de este período. Si seleccionó **analizar las solicitudes dependientes**, a continuación, todos los Hola imágenes, archivos de estilo, scripts y otros recursos dependientes se deben haber recibido dentro de este período.

    **Respuesta HTTP**: Hola devolvió el código de estado que se cuenta como un estado correcto. 200 es código de hello que indica que se ha devuelto una página web normal.

    **Coincidencia de contenido**: una cadena, como "Bienvenido". Probamos que se produce una coincidencia exacta entre mayúsculas y minúsculas en todas las respuestas. Debe ser una cadena sin formato, sin caracteres comodín. No olvide que if los cambios de contenido de página es posible que tenga tooupdate.
* **Alertas** son, de forma predeterminada, envían tooyou si hay errores en tres ubicaciones en cinco minutos. Un error en una ubicación es toobe es probable que un problema de red y no un problema con el sitio. Pero puede cambiar Hola umbral toobe más o menos confidencial y, puede también cambiar quién Hola mensajes de correo electrónico se enviarán a.

    Puede configurar un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) que se llama cuando se genera una alerta. (Pero tenga en cuenta que, en la actualidad, los parámetros de consulta no se pasan como propiedades).

### <a name="test-more-urls"></a>Prueba de más URL
Agregue más pruebas. Por ejemplo, en suma tootesting la página principal, puede Asegúrese de que está ejecutando la base de datos al probar la dirección URL de Hola para realizar una búsqueda.


## <a name="monitor"></a>3. Visualización de los resultados de las pruebas de disponibilidad

Después de unos minutos, haga clic en **actualizar** toosee los resultados de pruebas. 

![Resumen de resultados en la hoja principal de Hola](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Hola scatterplot muestra ejemplos de hello resultados de pruebas que tienen el detalle de paso de prueba de diagnóstico en ellos. motor de pruebas de Hello almacena los detalles de diagnóstico para pruebas con errores. Para las pruebas correctas, los detalles de diagnóstico se almacenan para un subconjunto de las ejecuciones de Hola. Mantenga el mouse sobre alguna de Hola puntos verde/roja toosee Hola prueba marca de tiempo, la duración de la prueba, la ubicación y nombre de la prueba. Haga clic en cualquier punto en hello dispersión trazado toosee Hola detalles del resultado de la prueba de Hola.  

Seleccione una prueba determinada, ubicación, o reducir el tiempo de hello toosee período más resultados alrededor de hello período de tiempo de interés. Use resultados de búsqueda del explorador toosee de todas las ejecuciones, o informes personalizados de toorun de las consultas de análisis en estos datos.

En los resultados sin formato de toohello de adición, hay dos métricas de disponibilidad en el Explorador de métricas: 

1. Disponibilidad: Porcentaje de pruebas de Hola que obtuvieron resultados satisfactorios, a través de todas las ejecuciones de prueba. 
2. Duración de la prueba: duración media de las pruebas en todas las ejecuciones de prueba.

Puede aplicar filtros en el nombre de la prueba de hello, las tendencias de tooanalyze de ubicación de una prueba determinada o la ubicación.

## <a name="edit"></a> Inspección y edición de pruebas

En la página de resumen de hello, seleccione una prueba concreta. Allí, puede ver sus resultados específicos y editarla o deshabilitarla temporalmente.

![Edit or disable a web test](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Quizás desee pruebas de disponibilidad de toodisable o alerta Hola reglas asociadas a ellos mientras se esté realizando el mantenimiento en el servicio. 

## <a name="failures"></a>Si ve errores
Haga clic en un punto rojo.

![Click a red dot](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


Desde un resultado de la prueba de disponibilidad, puede hacer lo siguiente:

* Inspeccionar la respuesta de hello recibida desde el servidor.
* Abra telemetría Hola enviado por la aplicación de servidor al procesar la instancia de solicitudes con error de Hola.
* Un problema de registro o elemento de trabajo de problema de hello tootrack Git o VSTS. Error de Hello contendrá un evento de toothis de vínculo.
* Abra el resultado de la prueba de hello web en Visual Studio.


*¿Parece que se ha completado correctamente pero se notifica como un error?* Compruebe todas las imágenes de hello, scripts, hojas de estilos y cualquier otro archivo cargado por página de Hola. Si se produce un error en cualquiera de ellos, prueba Hola se notifica como error, incluso si la página html principal de hello carga Aceptar.

*¿No hay elementos relacionados?* Si tiene Application Insights configurado para la aplicación de servidor, esto puede deberse a que se está llevando a cabo un [muestreo](app-insights-sampling.md). 

## <a name="multi-step-web-tests"></a>Pruebas web de varios pasos
Puede supervisar un escenario que implique una secuencia de direcciones URL. Por ejemplo, si va a supervisar un sitio Web de ventas, puede probar que la adición de elementos toohello carro de la compra funciona correctamente.

> [!NOTE] 
> Las pruebas web de varios pasos conllevan un coste. [Esquema de precios](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate una prueba de varios pasos, grabar el escenario de hello mediante Visual Studio Enterprise y, a continuación, cargar Hola grabación tooApplication visión. Application Insights reproduce el escenario de Hola a intervalos y comprueba las respuestas de saludo.

> [!NOTE]
> No puede usar funciones codificadas ni bucles en las pruebas. prueba de Hello debe estar contenido completamente en el script de WebTest Hola. Sin embargo, puede usar complementos estándar.
>

#### <a name="1-record-a-scenario"></a>1. Grabar un escenario
Usar Visual Studio Enterprise toorecord una sesión web.

1. Cree un proyecto de prueba de rendimiento web.

    ![En las ediciones de Visual Studio Enterprise, cree un proyecto de plantilla de prueba de carga y rendimiento Web Hola.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *¿No se ve hello rendimiento Web y la plantilla de prueba de carga?* - Cierre Visual Studio Enterprise. Abra **instalador de Visual Studio** toomodify la instalación de Visual Studio Enterprise. En **Componentes individuales**, seleccione **Herramientas de prueba de carga y rendimiento web**.

2. Abra el archivo de WebTest hello y empiece a grabar.

    ![Abra el archivo de WebTest hello y haga clic en registro.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Hola las acciones del usuario que desee toosimulate en la prueba: abra el sitio Web, agregar un carro de toohello de producto y así sucesivamente. Después, detenga la prueba.

    ![ejecuciones de la grabadora de prueba de web de Hello en Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    No cree un escenario largo. Existe un límite de 100 pasos y 2 minutos.
4. Editar pruebas de hello para:

   * Agregar validaciones toocheck Hola recibido respuesta y texto códigos.
   * Quite las interacciones que sean superfluas. También puede quitar las solicitudes dependientes para las imágenes o tooad o seguimiento de los sitios.

     Recuerde que puede editar script de prueba de hello, no se puede agregar código personalizado o llamar a otras pruebas web. No inserte bucles en prueba Hola. Puede utilizar complementos de prueba web estándar.
5. Ejecutar prueba de hello en Visual Studio toomake seguro de que funciona.

    Ejecutor de pruebas de Hello web abre un explorador web y se repite Hola acciones grabadas. Asegúrese de que funciona como se esperaba.

    ![En Visual Studio, abra el archivo de WebTest hello y haga clic en ejecutar.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Cargar pruebas tooApplication visión de hello web
1. En el portal de Application Insights hello, crear una prueba web.

    ![En la hoja de pruebas de hello web, elija Agregar.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Seleccione la prueba de varios pasos y cargar archivo de WebTest hello.

    ![Seleccione la prueba web de varios pasos.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Establecer hello las ubicaciones de prueba, la frecuencia y los parámetros de alerta en hello misma forma que para ping prueba.

#### <a name="3-see-hello-results"></a>3. Ver resultados de Hola

Ver la prueba de resultados y errores en Hola mismas pruebas de forma como direcciones url.

Además, puede descargar tooview de resultados de pruebas de hello usarlas en Visual Studio.

#### <a name="too-many-failures"></a>¿Hay demasiados errores?

* Una causa habitual de error es que esa prueba Hola dura demasiada. No deben ejecutar durante más de dos minutos.

* No olvide que todos los recursos de Hola de una página se deben cargar correctamente para hello pruebas toosucceed, incluidas las secuencias de comandos, hojas de estilos, imágenes y así sucesivamente.

* Hello prueba web debe estar completamente incluida en script de Hola WebTest: no puede usar funciones codificadas en pruebas de Hola.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Conexión de tiempo y números aleatorios a su prueba de varios pasos
Suponga que está probando una herramienta que obtiene datos que dependen del tiempo, como acciones de una fuente externa. Al grabar la prueba web, tienen toouse determinadas horas y establecerlos como parámetros de hello de prueba, StartTime y EndTime.

![Una prueba web con parámetros.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Al ejecutar prueba de hello, le gustaría EndTime siempre toobe Hola presentar tiempo y StartTime debe ser de 15 minutos hace.

Complementos de prueba Web proporcionan forma hello toodo parametrizar veces.

1. Agregue un complemento de prueba de web a cada valor variable que desee. En la barra de herramientas de pruebas de hello web, elija **agregar complemento de prueba Web**.

    ![Elija Agregar complemento de prueba web y seleccione un tipo.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    En este ejemplo, utilizamos dos instancias de hello complemento de tiempo de fecha. Una instancia es para "hace 15 minutos" y otra para "ahora".
2. Abra las propiedades de Hola de cada complemento. Asígnele un nombre y establézcalo toouse Hola hora actual. En cada uno de ellos, establezca Añadir minutos = -15.

    ![Establezca el nombre, Usar hora actual y Agregar minutos.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. En parámetros de prueba de hello web, use {{nombre del complemento}} tooreference un nombre del complemento.

    ![En los parámetros de prueba hello, utilice {{nombre del complemento}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

Ahora, cargue el portal de toohello de prueba. Usa valores dinámicos hello en cada ejecución de la prueba de Hola.

## <a name="dealing-with-sign-in"></a>Tratamiento del inicio de sesión
Si los usuarios inician sesión en la aplicación tooyour, tienes varias opciones para simular inicio de sesión para que pueda probar páginas detrás de inicio de sesión en Hola. método Hello utilizado depende de tipo de Hola de seguridad proporcionada por la aplicación hello.

En todos los casos, debe crear una cuenta en la aplicación solo para el propósito de Hola de las pruebas. Si es posible, restrinja los permisos de Hola de esta cuenta de prueba para que no hay ninguna posibilidad de hello las pruebas web que afecte a los usuarios reales.

### <a name="simple-username-and-password"></a>Nombre de usuario y la contraseña simples
Grabar una prueba web en hello forma habitual. Elimine las cookies en primer lugar.

### <a name="saml-authentication"></a>Autenticación SAML
Usar el complemento SAML de Hola que está disponible para las pruebas web.

### <a name="client-secret"></a>Secreto del cliente
Si la aplicación tiene una ruta de inicio de sesión que implica un secreto de cliente, utilícela. Azure Active Directory (AAD) es un ejemplo de un servicio que proporciona inicio de sesión del secreto de cliente. En AAD, el secreto del cliente de hello es Hola clave de aplicación.

Esta es una prueba web de ejemplo de una aplicación web de Azure que usa una clave de aplicación:

![Ejemplo de secreto de cliente](./media/app-insights-monitor-web-app-availability/110.png)

1. Obtener el token de AAD mediante el secreto de cliente (AppKey).
2. Extraer el token de portador de la respuesta.
3. Llamar a API con el token de portador de encabezado de autorización de Hola.

Asegúrese de que la prueba de web hello es un cliente real, es decir, tiene su propia aplicación en AAD - y utilice su clientId + appkey. El servicio sometida a prueba también tiene su propia aplicación de AAD: Hola appID URI de esta aplicación se refleja en la prueba web de hello en el campo de "recurso" Hola.

### <a name="open-authentication"></a>Autenticación abierta
Un ejemplo de autenticación abierta es el iniciar sesión con una cuenta de Microsoft o Google. Muchas aplicaciones que usan OAuth proporcionar Hola a alternativa secreto de cliente, por lo que su primera táctica debe ser tooinvestigate esa posibilidad.

Si la prueba debe iniciar sesión con OAuth, es el enfoque general de hello:

* Usar una herramienta como Fiddler tooexamine Hola el tráfico entre el explorador web, sitio de autenticación de hello y la aplicación.
* Realizar dos o más inicios de sesión con distintas máquinas o exploradores, o a intervalos de tiempo (tooallow tokens tooexpire).
* Al comparar diferentes sesiones, identificar símbolo (token) de hello pasado desde Hola sitio, que, a continuación, se pasa el servidor de aplicaciones de tooyour después de inicio de sesión de autenticación.
* Grabe una prueba web con Visual Studio.
* Parametrizar tokens hello, estableciendo parámetro hello cuando se devuelve el token de Hola de autenticador de Hola y su uso en el sitio de hello consulta toohello.
  (Visual Studio intenta prueba de hello tooparameterize, pero no parametriza correctamente los tokens de Hola.)


## <a name="performance-tests"></a>Pruebas de rendimiento
Puede ejecutar una prueba de carga en el sitio web. Como prueba de disponibilidad de hello, puede enviar solicitudes sencillas o las solicitudes de varios pasos de nuestro puntos alrededor de Hola a todos. A diferencia de una prueba de disponibilidad, se envían muchas solicitudes, que simulan a varios usuarios simultáneos.

En la hoja de información general de hello, abra **configuración**, **pruebas de rendimiento**. Cuando se crea una prueba, se le invita tooconnect tooor crear una cuenta de Visual Studio Team Services.

Una vez completada la prueba de hello, se muestran los tiempos de respuesta y las tasas de éxito.


![Prueba de rendimiento](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> efectos de hello tooobserve de una prueba de rendimiento, use [secuencia en directo](app-insights-live-stream.md) y [Profiler](app-insights-profiler.md).
>

## <a name="automation"></a>Automation
* [Usar tooset de secuencias de comandos de PowerShell una prueba de disponibilidad](app-insights-powershell.md#add-an-availability-test) automáticamente.
* Configure un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) que se llama cuando se genera una alerta.

## <a name="qna"></a>¿Tiene preguntas? ¿Tiene problemas?
* *¿Puedo llamar el código desde mi prueba web?*

    No. pasos de Hola de prueba de hello deben estar en archivo de WebTest hello. Y no se puede llamar a otras pruebas web ni utilizar bucles. Pero hay varios complementos que pueden resultarle útiles.
* *¿Se admite HTTPS?*

    Admitimos TLS 1.1 y TLS 1.2.
* *¿Existe alguna diferencia entre las "pruebas web" y las "pruebas de disponibilidad"?*

    Hola dos términos puede hacer referencia a indistintamente. Pruebas de disponibilidad es un término más genérico que incluye ping de dirección URL única de hello además pruebas toohello las pruebas web de varios pasos.
* *Me gustaría toouse disponibilidad pruebas en nuestro servidor interno que ejecuta detrás de un firewall.*

    Hay dos soluciones posibles:
    
    * Configurar las firewall toopermit las solicitudes entrantes de hello [agentes de prueba de direcciones IP de nuestra web](app-insights-ip-addresses.md).
    * Escribir su propio código de prueba de tooperiodically su interno del servidor. Ejecutar código de hello como un proceso en segundo plano en un servidor de prueba detrás del firewall. El proceso de prueba puede enviar sus resultados tooApplication visión mediante [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API en el paquete del SDK de hello core. Para ello, el prueba toohave saliente acceso toohello Application Insights ingesta extremo del servidor, pero que es un riesgo de seguridad mucho más pequeño que alternativa de Hola de permitir las solicitudes entrantes. resultados de Hello no aparecerán en hojas de las pruebas web de disponibilidad de hello, pero aparece como resultado de la disponibilidad de análisis, búsqueda y el Explorador de métrica.
* *Al cargar una prueba web de varios pasos, se produce un error*

    Hay un límite de tamaño de 300 000.

    No se admiten los bucles.

    No se admiten referencias tooother web pruebas.

    No se admiten orígenes de datos.
* *No se completa la prueba de varios pasos*

    Hay un límite de 100 solicitudes por prueba.

    prueba de Hola se detiene si se ejecuta más de dos minutos.
* *¿Cómo se puede ejecutar una prueba con certificados de cliente?*

    Lo sentimos, pero eso no está admitido.


## <a name="next"></a>Pasos siguientes
[Búsqueda de registros de diagnóstico][diagnostic]

[Solución de problemas][qna]

[Direcciones IP de agentes de pruebas web](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
