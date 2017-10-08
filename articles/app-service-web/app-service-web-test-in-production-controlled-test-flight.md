---
title: "implementación de aaaFlighting (beta prueba) en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo tooflight nuevas características en su aplicación o la versión beta de probar las actualizaciones en este tutorial to-end. Reúne las características del Servicio de aplicaciones como publicación continua, ranuras, enrutamiento de tráfico y la integración de Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Implementación de la distribución de paquetes piloto (pruebas beta) en el Servicio de aplicaciones de Azure
Este tutorial muestra cómo toodo *las implementaciones de programa Windows Insider* mediante la integración de Hola varias funciones de [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) y [Azure Application Insights](/services/application-insights/).

*La distribución de paquetes piloto* es un proceso de implementación que valida una nueva característica o cambio con un número limitado de clientes reales, y es una prueba importante en el escenario de producción. Es toobeta analogía pruebas y a veces se conoce como "vuelo de pruebas controlado". Muchas grandes empresas con una presencia web usan este enfoque para obtener validación temprana en las actualizaciones de sus aplicaciones dentro de su prácticas de [desarrollo ágil](https://en.wikipedia.org/wiki/Agile_software_development). Servicio de aplicaciones de Azure le permite toointegrate prueba en producción con la publicación continua y Application Insights tooimplement Hola mismo escenario de DevOps. Las ventajas de este enfoque incluyen:

* **Obtener comentarios real *antes de* las actualizaciones están publicada tooproduction** -Hola solo lo mejor que tengan comentarios tan pronto como la versión está adquiriendo cada vez comentarios antes de liberar. Puede probar las actualizaciones con tráfico de usuario real y comportamientos tan pronto como se desee en el ciclo de vida de productos de Hola.
* **Mejora [del desarrollo continuo controlado por pruebas (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** a través de la integración de pruebas en la producción, con integración continua e instrumentación con Application Insights, la validación de usuario se produce al principio y de forma automática dentro del ciclo de vida del producto. Esto ayuda a reducir las inversiones de tiempo de ejecución de pruebas manuales.
* **Optimizar el flujo de trabajo de prueba** -mediante la automatización de prueba en producción con la instrumentación de supervisión continua, puede potencialmente lograr Hola objetivos de varias clases de pruebas en un único proceso, como [integración](https://en.wikipedia.org/wiki/Integration_testing), [regresión](https://en.wikipedia.org/wiki/Regression_testing), [facilidad de uso](https://en.wikipedia.org/wiki/Usability_testing), accesibilidad, localización, [rendimiento](https://en.wikipedia.org/wiki/Software_performance_testing), [seguridad](https://en.wikipedia.org/wiki/Security_testing), y [ aceptación](https://en.wikipedia.org/wiki/Acceptance_testing).

En una implementación de distribución de paquetes piloto, no se trata solamente del enrutamiento de tráfico real. En ese tipo de implementación que desee toogain una visión general de lo más rápido posible, ya sea un error inesperado, degradación del rendimiento, problemas de la experiencia de usuario. Recuerde que se trata de los clientes reales. Toodo por lo que, a la derecha, debe asegurarse de que ha configurado el programa Windows Insider toogather implementación todos los datos de Hola que necesita en orden toomake una decisión informada para el paso siguiente. Este tutorial muestra cómo toocollect de datos con Application Insights, pero se puede utilizar New Relic u otras tecnologías que se adapte a su escenario.

## <a name="what-you-will-do"></a>Lo que hará
En este tutorial, aprenderá cómo toobring Hola siguientes escenarios juntos tootest la aplicación de servicio de aplicaciones de producción:

* [Redirigir el tráfico de producción](app-service-web-test-in-production-get-start.md) tooyour beta aplicación
* [Instrumentar la aplicación](../application-insights/app-insights-web-track-usage.md) tooobtain útil métricas
* Implementar la aplicación beta y realizar un seguimiento de las métricas de aplicación de forma continua
* Las métricas de comparación entre la aplicación de producción de hello y cómo cambia el código de hello beta aplicación toosee traducen tooresults

## <a name="what-you-will-need"></a>Qué necesita
* Una cuenta de Azure
* Una cuenta [GitHub](https://github.com/)
* Visual Studio 2015: puede descargar hello [edición Community](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* GIT Shell (instalado con [GitHub para Windows](https://windows.github.com/))-Esto permite toorun ambos comandos de PowerShell y Git Hola Hola misma sesión
* Bits más recientes de [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)
* Conocimientos básicos de los siguientes hello:
  * Implementación de plantillas de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (consulte [Aprovisionamiento e implementación predecibles de microservicios en Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Necesita una cuenta de Azure toocomplete este tutorial:
>
> * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/) -obtendrá créditos puede usar tootry los servicios de Azure de pago e incluso después de que agoten puede mantener la cuenta de hello y libre de usar servicios de Azure, como las aplicaciones Web.
> * Puede [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : su suscripción a Visual Studio le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.
>
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
>
>

## <a name="set-up-your-production-web-app"></a>Configuración de la aplicación web de producción
> [!NOTE]
> script de Hola utilizado en este tutorial configurará automáticamente la publicación continua desde el repositorio de GitHub. Esto requiere que las credenciales de GitHub ya están almacenadas en Azure, en caso contrario hello mediante secuencias de comandos se producirá un error al intentar tooconfigure configuración de control de código fuente para las aplicaciones web de Hola.
>
> toostore su GitHub credenciales de Azure, cree una aplicación web en hello [Portal de Azure](https://portal.azure.com/) y [configurar la implementación de GitHub](app-service-continuous-deployment.md). Solo necesita esta vez toodo.
>
>

En un escenario típico de DevOps, tiene una aplicación que se ejecuta en Azure y desea toomake cambios tooit a través de la publicación continua. En este escenario, implementará tooproduction una plantilla que haya desarrollado y probado.

1. Crear su propia bifurcación de hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositorio. Para obtener información sobre la creación de la bifurcación, consulte [Bifurcación de un repositorio](https://help.github.com/articles/fork-a-repo/). Una vez creada la bifurcación, puede verla en el explorador.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Abra una sesión del Shell de Git. Si aún no tiene el Shell de Git, instale ahora [GitHub para Windows](https://windows.github.com/) .
3. Crear un clon de la bifurcación local mediante la ejecución de hello siguiente comando:

     git clone https://github.com/<su_bifurcación>/ToDoApp.git
4. Una vez que tenga el clon local, vaya demasiado*&lt;repository_root >*\ARMTemplates y ejecución hello deploy.ps1 secuencia de comandos con un sufijo único, como se muestra a continuación:

     .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix>
5. Cuando se le solicite, escriba el nombre de usuario de hello deseado y una contraseña para el acceso a la base de datos. Recordar las credenciales de la base de datos ya que necesitará toospecify implementarlos de nuevo cuando la actualización Hola grupo de recursos.

   Debería ver Hola aprovisionamiento progreso por varios recursos de Azure. Cuando se completa la implementación, el script de Hola Iniciar aplicación hello en el Explorador de Hola y proporcionarle un bip descriptivo.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. De nuevo en la sesión del Shell de Git, ejecute:

     .\swap –Name ToDoApp<su_sufijo>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Cuando finaliza el script de Hola, vuelva atrás toobrowse toohello dirección del front-end (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee Hola ejecuta aplicación en producción.
8. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/) y eche un vistazo a lo que se crea.

   Debe ser capaz de toosee dos aplicaciones de web Hola mismo grupo de recursos, uno con hello `Api` sufijo de nombre de Hola. Si observa en vista de grupo de recursos de hello, también verá Hola base de datos SQL y servidor, Hola plan de servicio de aplicaciones y zonas de ensayo de Hola para las aplicaciones web de Hola. Examine los distintos recursos de Hola y compararlos con  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json cómo estén configuradas en la plantilla de Hola.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Ha configurado la aplicación de producción de hello.  Ahora, imaginemos que recibe información que es insuficiente para la aplicación hello facilidad de uso. Por lo que decida tooinvestigate. Se vayan tooinstrument toogive de su aplicación, comentarios.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Investigación: instrumentar la aplicación de cliente para supervisión y métricas
1. Abra *&lt;raíz_repositorio>*\src\MultiChannelToDo.sln en Visual Studio.
2. Restaure todos los paquetes de Nuget haciendo clic con el botón derecho en la solución > **Administrar paquetes de NuGet para la solución** > **Restaurar**.
3. Haga clic en **MultiChannelToDo.Web** > **Agregar aplicación visión telemetría** > **configurar opciones de** > grupo de recursos de cambio tooToDoApp*&lt;your_suffix >* > **tooProject agregar Application Insights**.
4. Hola Portal de Azure, abra hoja Hola para hello **MultiChannelToDo.Web** recursos Application Insight. A continuación, en hello **estado de la aplicación** parte, haga clic en **Obtenga información acerca de la página del explorador toocollect cargar datos** > Copiar el código.
5. Agregar Hola copia código de instrumentación de JS demasiado*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, justo antes de cerrarse de hello `<heading>` etiqueta. Debe incluir Hola Instrumental única clave del recurso Application Insight.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Enviar eventos personalizados tooApplication visión de clics del mouse mediante la adición de hello después de la parte inferior de toohello de código del cuerpo:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Este fragmento de código de JavaScript envía un evento personalizado tooApplication información cada vez que un usuario hace clic en cualquier lugar en la aplicación web de hello.
7. En el Shell de Git, confirme e inserte la bifurcación de tooyour cambios en GitHub. A continuación, espere explorador toorefresh de los clientes.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Hola de intercambio implementado tooproduction de cambios de aplicación:

     .\swap –Name ToDoApp<su_sufijo>
9. Examinar los recursos de Application Insights toohello que ha configurado. Haga clic en Eventos personalizados

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Si no ve las métricas para los eventos personalizados, espere unos minutos y haga clic en **Actualizar**.

Supongamos que ve un gráfico como el siguiente:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

Y cuadrícula de eventos de Hola por debajo de él:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Según el código de la aplicación de tooyour ToDoApp, Hola **botón** evento corresponde hello y botón de envío de toohello **entrada** evento corresponde toohello cuadro de texto. Hasta aquí, todo está claro. Sin embargo, parece que hay una gran cantidad de clics y muy pocos clics en los elementos de tareas pendientes de hello (hello **LI** eventos).

A partir de este, formulario esas hipótesis que algunos usuarios confundir qué parte del programa Hola a interfaz de usuario es interactivo y es porque el estilo del cursor de hello para la selección de texto cuando mantiene el mouse sobre elementos de lista de Hola y sus iconos.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Este podría ser un ejemplo inventado. No obstante, está continuo toomake una aplicación de tooyour mejora y, a continuación, realizar un programa Windows Insider comentarios de facilidad de uso de tooget de implementación de clientes en vivo.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumentación de la aplicación del servidor para supervisión y métricas
Se trata de una tangente puesto que el escenario de Hola que se muestran en este tutorial solo se ocupa de la aplicación de cliente de hello. Sin embargo, a efectos de integridad a configurar aplicación de servidor hello.

1. Haga clic en **MultiChannelToDo** > **Agregar aplicación visión telemetría** > **configurar opciones de** > grupo de recursos de cambio tooToDoApp*&lt;your_suffix >* > **tooProject agregar Application Insights**.
2. En el Shell de Git, confirme e inserte la bifurcación de tooyour cambios en GitHub. A continuación, espere explorador toorefresh de los clientes.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Hola de intercambio implementado tooproduction de cambios de aplicación:

     .\swap –Name ToDoApp<su_sufijo>

Eso es todo.

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Investigar: Agregar métricas de aplicación de cliente de etiquetas específicas de la ranura tooyour
En esta sección, configurará Hola implementación diferentes ranuras toosend telemetría específica de la ranura toohello mismo recurso de Application Insights. De esta manera, puede comparar la telemetría datos entre el tráfico de ranuras diferentes (entornos de implementación) tooeasily ver el efecto de Hola de los cambios de la aplicación. Hola al mismo tiempo, puede separar el tráfico de producción de hello de rest de Hola para que pueda continuar toomonitor la aplicación de producción según sea necesario.

Puesto que va a recopilar datos en el comportamiento del cliente, que se van a [agregar un tooyour de inicializador de telemetría código JavaScript](../application-insights/app-insights-api-filtering-sampling.md) en index.cshtml. Si desea que el rendimiento del servidor de tootest, por ejemplo, también puede hacer de forma similar en el código del servidor (consulte [API de visión de la aplicación para eventos personalizados y las métricas](../application-insights/app-insights-api-custom-events-metrics.md).

1. En primer lugar, agregue Hola de fuente del código de hello dos `//` comentarios a continuación en el bloque de JavaScript de Hola que ha agregado toohello `<heading>` etiqueta anteriormente.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Este código de inicializador hace hello `appInsights` tooadd objeto Hola una propiedad personalizada denominada `Environment` tooevery parte de telemetría envía.
2. A continuación, agregue esta propiedad personalizada como una [configuración de ranura](web-sites-staged-publishing.md#AboutConfiguration) para la aplicación web en Azure. toodo, Hola ejecución siga los comandos en la sesión de Git Shell.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Hola Web.config en el proyecto ya define hello `environment` configuración de la aplicación. Con esta configuración, al probar la aplicación hello localmente, las métricas se etiqueta con `VS Debugger`. Sin embargo, cuando realice una inserción su tooAzure cambios, Azure se encuentra y usar hello `environment` aplicación establecer en la configuración de la aplicación hello web en su lugar y la métrica se etiqueta con `Production`.
3. Confirmar inserción la bifurcación de tooyour de cambios de código en GitHub y esperar a que la aplicación nueva de los usuarios toouse Hola (necesidad toorefresh Hola explorador). Ocupe Hola nueva propiedad tooshow unos 15 minutos en la información de la aplicación `MultiChannelToDo.Web` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Ahora, vaya toohello **eventos personalizados** hoja nuevo y filtro Hola métricas en `Environment=Production`. Ahora debe ser capaz de toosee todos los Hola nuevos eventos personalizados en producción de hello zona con este filtro.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Haga clic en hello **favoritos** como botón toosave Hola actual explorador métricas configuración toosomething **eventos personalizados: producción**. Más adelante puede cambiar fácilmente entre esta vista y la vista de una ranura de implementación.

   > [!TIP]
   > Para realizar análisis aún más eficaces, considere la posibilidad de la [integración de los recursos de Application Insights con Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Agregar etiquetas específicas de la ranura tooyour server aplicación métricas
Una vez más, por integridad, se establecerá una aplicación de servidor hello. A diferencia de la aplicación de cliente de hello que se indique en JavaScript, etiquetas específicos de la ranura de aplicación de servidor hello se ha instrumentado con código. NET.

1. Abra *&lt;raíz_repositorio>*\src\MultiChannelToDo\Global.asax.cs. Agregar bloque de código de hello a continuación, justo antes de hello Cerrar llave de espacio de nombres.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Corregir errores de resolución de nombres de hello agregando hello `using` instrucciones a continuación toohello a partir del archivo hello:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Agregue código de hello debajo toohello a partir de hello `Application_Start()` método:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Confirmar inserción la bifurcación de tooyour de cambios de código en GitHub y esperar a que la aplicación nueva de los usuarios toouse Hola (necesidad toorefresh Hola explorador). Ocupe Hola nueva propiedad tooshow unos 15 minutos en la información de la aplicación `MultiChannelToDo` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Actualización: configurar la bifurcación de la versión beta
1. Abra  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json y buscar hello `appsettings` recursos (buscar `"name": "appsettings"`). Hay 4 de ellos, uno para cada ranura.
2. Para cada `appsettings` recursos, agregue un `"environment": "[parameters('slotName')]"` toohello final de configuración de aplicación de hello `properties` matriz. No olvide la línea anterior de hello tooend con una coma.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Acaba de agregar hello `environment` aplicación establecer tooall ranuras de hello en plantilla Hola.
3. En Hola el mismo archivo, busque hello `slotconfignames` recursos (buscar `"name": "slotconfignames"`). Hay 2 de ellos, uno para cada aplicación.
4. Para cada `slotconfignames` recursos, agregue `"environment"` toohello final de hello `appSettingNames` matriz. No olvide la línea anterior de hello tooend con una coma.

    Acaba de crear hello `environment` configuración stick tooits implementación respectivos la ranura de aplicación para las aplicaciones.  
5. En la sesión de Git Shell, siguiente ejecución Hola comandos con hello mismo sufijo de grupo de recursos que usó anteriormente.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Cuando se le solicite, especifique Hola mismas credenciales de base de datos SQL como antes. A continuación, cuando solicita el grupo de recursos de hello tooupdate, tipo `Y`, a continuación, `ENTER`.

    Una vez que finaliza el script de Hola, se conservan todos los recursos en el grupo de recursos de hello original, pero una ranura nueva denominada "beta" que se crea en él con hello mismo configuración como ranura de "Ensayo" hello que se creó en el principio de Hola.

   > [!NOTE]
   > Este método de creación de diferentes entornos de implementación es diferente del método hello en [desarrollo de software ágil con el servicio de aplicación de Azure](app-service-agile-software-development.md). Aquí puede crear entornos de implementación con las ranuras de implementación, mientras que en el otro caso los entornos de implementación se crean con grupos de recursos. La administración de entornos de implementación con grupos de recursos permite toodevelopers off-limits del entorno de producción hello tookeep, pero no resulta fácil toodo pruebas en producción, lo que puede hacer fácilmente con ranuras.
   >
   >

Si lo desea, también puede crear una aplicación alfa ejecutando

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Para este tutorial, continúe usando la aplicación beta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Actualización: La aplicación de actualizaciones toohello beta de inserción
Realice una copia de aplicación de tooyour que desea que se tooimprove.

1. Asegúrese de que se encuentra ahora en la bifurcación de la versión beta

        git checkout beta
2. En  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, buscar hello `<li>` etiquetar y agregar hello `style="cursor:pointer"` atributo, tal y como se muestra a continuación.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Confirme e inserte tooAzure.
4. Comprobar que el cambio de Hola se reflejan en la ranura de la versión beta de hello desplazándose toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Si no ve Hola cambiar todavía, actualice el explorador tooget Hola nuevo código de javascript.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Ahora que tiene el cambio que se ejecuta en la ranura de la versión beta de hello, está listo tooperform una implementación programa Windows Insider.

## <a name="validate-route-traffic-toohello-beta-app"></a>Validar: Enrutar el tráfico toohello beta aplicación
En esta sección, enrutará el tráfico toohello beta aplicación. Por motivos de claridad de la demostración, va tooroute una parte significativa de tooit de tráfico de usuario de Hola. En realidad, Hola cantidad de tráfico que desee tooroute dependerá de su situación concreta. Por ejemplo, si el sitio está a escala Hola de microsoft.com, a continuación, deberá menor que uno por ciento del tráfico total de datos útiles de orden toogain.

1. En la sesión de Git Shell, ejecute hello después comandos tooroute la mitad de la ranura beta toohello tráfico de producción de hello:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Hola `ReroutePercentage=50` propiedad especifica que el 50% del tráfico de producción de hello será URL de la aplicación de toohello enrutado beta (especificado por hello `ActionHostName` propiedad).
2. Ahora, explore toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% del tráfico de hello ahora debería ranura de beta toohello redirigida.
3. En el recurso de Application Insights, filtrar las métricas de hello entorno = "beta".

   > [!NOTE]
   > Si guarda esta vista filtrada como favorito otro, puede examinar fácilmente vistas del explorador de métrica de hello entre producción y vistas de la versión beta.
   >
   >

Suponga que en Application Insights ve toohello algo similar a continuación:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

No solo Esto muestra que hay muchos más clics en hello `<li>` etiquetas, pero parece que hay toobe una sobrecarga de clics en `<li>` etiquetas. A continuación, puede estar seguro de que personas han descubierto Hola nuevo `<li>` las etiquetas son seleccionables y ahora está borrando todas sus tareas completados anteriormente en la aplicación hello.

En función de datos de saludo de la implementación del programa Windows Insider, decide que la nueva interfaz de usuario está listo para producción.

## <a name="go-live-move-your-new-code-into-production"></a>Puesta en marcha: mover el código nuevo a producción
Se está ahora listo toomove su tooproduction de actualización. ¿Qué es grande es que ahora sabe que la actualización ya se ha validado *antes de* se inserta tooproduction. Ahora puede implementarlo con confianza. Desde que realizó una aplicación de cliente de actualización toohello AngularJS, sólo se valida el código del lado cliente de Hola. Si se encontraba aplicaciones de API Web de back-end de toomake cambios toohello, pudo validar los cambios de forma similar y sencilla.

1. En el Shell de Git, quite la regla de enrutamiento de tráfico de hello ejecutando Hola siguiente comando:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Ejecute comandos de Git de hello:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Espere unos minutos para hello nuevo código toohello toobe implementado ranura de ensayo y vuelva a iniciar http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net que Hola nueva actualización se activa en almacenamiento provisional de Hola ranura. Recuerde que Hola bifurcación principal de la bifurcación está vinculado toohello ensayo ranura de la aplicación.
4. Ahora, intercambiar Hola ranura de ensayo a producción

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Resumen
Servicio de aplicaciones de Azure facilita toomedium pequeña empresas tootest sus aplicaciones orientado al cliente en producción, algo que se ha realizado tradicionalmente en grandes empresas. Con suerte, este tutorial le ha concedido Hola conocimientos necesarios toobring juntos servicio de aplicaciones y Application Insights toomake programa Windows Insider implementación posibles e incluso otros escenarios de prueba en producción, en el mundo de DevOps.

## <a name="more-resources"></a>Más recursos
* [Agile Software Development con el Servicio de aplicaciones de Azure](app-service-agile-software-development.md)
* [Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-staged-publishing.md)
* [Implementación predecible de una aplicación compleja en Azure](app-service-deploy-complex-application-predictably.md)
* [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Hola validador de JSON](http://jsonlint.com/)
* [Creación de ramas de Git: combinación y creación de ramas básicas](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Wiki de Project Kudu](https://github.com/projectkudu/kudu/wiki)
