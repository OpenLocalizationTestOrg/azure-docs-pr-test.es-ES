---
title: "análisis de aaaUsage para aplicaciones web con Azure Application Insights | Documentos de Microsoft"
description: "Entender a los usuarios y lo qué hacen con su aplicación web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Análisis de uso de aplicaciones web con Application Insights

¿Qué características de su aplicación web son más populares? ¿Los usuarios logran sus objetivos con la aplicación? ¿Salen de ella en momentos concretos y vuelven más tarde?  [Azure Application Insights](app-insights-overview.md) lo ayudará a obtener información eficaz sobre cómo los usuarios usan su aplicación web. Cada vez que actualice la aplicación, puede evaluar también si funciona bien para los usuarios. Con este conocimiento, puede tomar decisiones basadas en datos sobre los ciclos de desarrollo siguientes.

## <a name="send-telemetry-from-your-app"></a>Envío de telemetría desde la aplicación

mejor experiencia de Hola se obtiene mediante la instalación de Application Insights en el código de servidor de la aplicación y en las páginas web. componentes de cliente y servidor de saludo de la aplicación envían telemetría atrás toohello portal de Azure para su análisis.

1. **Código de servidor:** módulo apropiado de Hola de instalación para su [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), o [otros](app-insights-platforms.md) aplicación.

    * *¿No desea que el código del servidor de tooinstall? Simplemente [cree un recurso de Azure Application Insights](app-insights-create-new-resource.md).*

2. **Código de la página Web:** Hola abierto [portal de Azure](https://portal.azure.com), abra el recurso de Application Insights de hello para la aplicación y, a continuación, abra **Introducción > supervisar y diagnosticar cliente**. 

    ![Copie el script de Hola en encabezado de hello de la página web principal.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Obtener telemetría:** ejecutar el proyecto en modo de depuración durante unos minutos y, a continuación, compruebe los resultados en la hoja de información general de hello en Application Insights.

    Publique su aplicación toomonitor el rendimiento de la aplicación y averiguar lo que hacen los usuarios con la aplicación.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Inclusión del identificador de usuario y de sesión en la telemetría
tootrack a los usuarios con el tiempo, Application Insights requiere un tooidentify manera ellos. herramienta eventos Hola Hola única herramienta de uso que no requiere un identificador de usuario o un identificador de sesión.

Empiece a enviar estos identificadores [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Exploración de estadísticas y datos demográficos de uso
Descubra cuándo los usuarios utilizan la aplicación, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean. 

informes de usuarios y sesiones de Hello filtrar los datos por páginas o eventos personalizados y segmentación por propiedades tales como la ubicación, el entorno y la página. También puede agregar sus propios filtros.

![Usuarios](./media/app-insights-usage-overview/users.png)  

Visión en hello derecho señalar patrones de interés en el conjunto de Hola de datos.  

* Hola **usuarios** informe cuenta los números de Hola de usuarios únicos que tienen acceso a las páginas dentro de los períodos de tiempo seleccionado. (Los usuarios se cuentan mediante el uso de cookies. Si alguien accede a su sitio con distintos exploradores o equipos cliente, o borra sus cookies, se contabilizarán de más de una vez.)
* Hola **sesiones** informe cuenta el número de Hola de sesiones de usuario que tienen acceso al sitio. Una sesión es un periodo de actividad por parte de un usuario, que finaliza con un periodo de inactividad de más de media hora.

[Más información acerca de las herramientas de los usuarios, sesiones y los eventos de Hola](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Vistas de página

Desde la hoja de uso de hello, click-through Hola vistas de página icono tooget un desglose de las páginas más populares:

![Desde la hoja de información general de hello, haga clic en hello gráfico de vistas de página](./media/app-insights-usage-overview/05-games.png)

ejemplo de Hola anterior es de un sitio web de juegos. De los gráficos de hello, podemos ver al instante:

* Uso no se ha mejorado en hello semana pasada. ¿Quizás debemos pensar en la optimización de motor de búsqueda?
* Tenis es la página de juego más popular de Hola. Este artículo nos centraremos en la página toothis de mejoras aún más.
* En promedio, los usuarios visitar página de tenis de hello aproximadamente tres veces por semana. (Hay unas tres veces más sesiones que usuarios.)
* La mayoría de los usuarios visitan el sitio de Hola durante la semana laboral de hello Estados Unidos y en horario laboral. Quizás que deberíamos proporcionarle un botón "Ocultar rápido" en la página web de Hola.
* Hola [anotaciones](app-insights-annotations.md) en el gráfico de hello aparecerán cuando se implementaron las nuevas versiones del sitio Web de Hola. Ninguna de las implementaciones de hello recientes tenía un efecto notable en uso.

¿Qué ocurre si desea sitio de tooyour tooinvestigate Hola tráfico con más detalle, como la división de una propiedad personalizada, que el sitio envía en su telemetría de vista de página?

1. Abra hello **eventos** herramienta en el menú de recursos de Application Insights Hola. Esta herramienta permite analizar el número de eventos personalizados y vistas de página que se enviaron desde su aplicación, en función de una variedad de opciones de filtrado, cohorte y segmentación.
2. En la lista desplegable "Que usa" Hola, seleccione "Vista de página Any".
3. En la lista desplegable de "División por" Hola, seleccione una propiedad por qué toosplit la página Ver telemetría.

## <a name="retention---how-many-users-come-back"></a>Retención : ¿cuántos usuarios regresan?

Retención le ayudará a comprender la frecuencia con los usuarios devuelven toouse su aplicación, en función de las cohortes de usuarios que realizan alguna acción empresarial durante un depósito de tiempo determinado. 

- Comprender qué características específicas hacer que los usuarios toocome back más que otras personas 
- Formular hipótesis basadas en datos de usuarios reales 
- Determinar si la retención es un problema del producto 

![Retención](./media/app-insights-usage-overview/retention.png) 

los controles de retención de Hello en la parte superior permiten toodefine eventos específicos y la conservación de toocalculate de intervalo de tiempo. gráfico situado en medio de Hola Hola proporciona una representación visual de hello porcentaje total de retención por hello intervalo de tiempo especificado. gráfico de Hello en la parte inferior de hello representa retención individual en un período de tiempo determinado. Este nivel de detalle permite toounderstand hacen qué los usuarios y qué pueden afectar a devolver a los usuarios con una granularidad más detallada.  

[Más información acerca de la herramienta de retención de Hola](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Eventos de negocio personalizados

tooget una idea clara de lo que los usuarios hacer con la aplicación web, resulta útil tooinsert líneas de eventos personalizados de código toolog. Estos eventos pueden realizar un seguimiento de nada de las acciones del usuario detallada como hacer clic en botones específicos, toomore los eventos significativos para el negocio, como realizar una compra o ganar una partida. 

Aunque, en algunos casos, las vistas de página pueden representar eventos útiles, en general, no es así. Un usuario puede abrir una página del producto sin necesidad de adquirir el producto de Hola. 

Con los eventos específicos del negocio, puede realizar un gráfico del progreso de los usuarios en su sitio. Puede averiguar sus preferencias para diferentes opciones y en qué partes salen o tienen dificultades. Con este conocimiento, puedan tomar decisiones fundamentadas sobre prioridades de hello en el trabajo pendiente de desarrollo.

Eventos se pueden registrar en la página web de hello:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

O en el lado del servidor hello de aplicación web de hello:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Puede asociar eventos de toothese de valores de propiedad, de forma que puede filtrar o dividir los eventos de hello al examinar en el portal de Hola. Además, un conjunto estándar de propiedades es evento tooeach adjunta, como Id. de usuario anónimo, lo que permite la secuencia de hello tootrace de actividades de un usuario individual.

Obtenga más información sobre los [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) y las [propiedades](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Eventos de segmentación y desglose

En herramientas de los usuarios, sesiones y los eventos de hello, puede segmentar y reorganizar los eventos personalizados por usuario, nombre del evento y propiedades.
![Usuarios](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Diseño Hola telemetría con la aplicación hello

Al diseñar cada característica de la aplicación, tenga en cuenta cómo va toomeasure su éxito con los usuarios. Decidir qué eventos de negocios que necesita toorecord y el código Hola llamadas para los eventos de seguimiento en la aplicación de Hola se inicia.

## <a name="a--b-testing"></a>Prueba A | B
Si no sabe qué variante de una característica tendrá más éxito, liberar ambos, hacer que los usuarios toodifferent accesible. Medir el éxito de Hola de cada uno y, a continuación, mover tooa unificada versión.

Para que esta técnica, debe adjuntar telemetría Hola de tooall de valores de propiedad distintiva que se envía con cada versión de la aplicación. Puede hacerlo mediante la definición de propiedades en hello TelemetryContext active. Estas propiedades predeterminadas se agregan envía el mensaje de telemetría tooevery que Hola aplicación - no solo los mensajes personalizados, pero también telemetría estándar de Hola.

En el portal de Application Insights hello, filtrar y dividir los datos en los valores de propiedad hello, así como versiones diferentes de toocompare Hola.

toodo, [configurar un inicializador de telemetría](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

En el inicializador de aplicación de hello web como Global.asax.cs:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

TelemetryClients nuevo todos los agrega automáticamente el valor de propiedad de Hola que especifique. Eventos de telemetría individual pueden invalidar los valores predeterminados de Hola.

## <a name="next-steps"></a>Pasos siguientes
   - [Usuarios, sesiones, eventos](app-insights-usage-segmentation.md)
   - [Embudos](usage-funnels.md)
   - [Retención](app-insights-usage-retention.md)
   - [Flujos de usuario](app-insights-usage-flows.md)
   - [Libros](app-insights-usage-workbooks.md)
   - [Adición de contexto de usuario](app-insights-usage-send-user-context.md)
