---
title: aaaMonitor un sitio de SharePoint con Application Insights
description: "Inicio de la supervisión de una nueva aplicación con una nueva clave de instrumentación"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Supervisión de un sitio de SharePoint con Application Insights
Azure Hola supervisa la disponibilidad, rendimiento y uso de las aplicaciones de Application Insights. Aquí aprenderá cómo tooset que en un sitio de SharePoint.

## <a name="create-an-application-insights-resource"></a>Creación de recursos en Application Insights
Hola [portal de Azure](https://portal.azure.com), cree un nuevo recurso de Application Insights. Elija ASP.NET como tipo de aplicación Hola.

![Haga clic en Propiedades, seleccione la clave de hello y presione ctrl + C](./media/app-insights-sharepoint/01-new.png)

hoja de Hola que se abre es lugar de Hola donde podrá ver datos de rendimiento y uso sobre su aplicación. tooget atrás tooit próxima vez que inicie sesión tooAzure, debería encontrar un icono para él en la pantalla de inicio de bienvenida. O bien haga clic en Examinar toofind lo.

## <a name="add-our-script-tooyour-web-pages"></a>Agregar nuestras páginas web de tooyour de secuencia de comandos
En Inicio rápido, obtener script de Hola para páginas web:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Insertar el script de Hola justo antes de hello &lt;/head&gt; etiqueta de cada página que desee tootrack. Si su sitio Web tiene una página maestra, puede colocar el script de Hola no existe. Por ejemplo, en un proyecto de ASP.NET MVC, lo colocaría en View\Shared\\_Layout.cshtml.

script de Hola contiene la clave de instrumentación de Hola que dirige el recurso de Application Insights de hello telemetría tooyour.

### <a name="add-hello-code-tooyour-site-pages"></a>Agregar código de hello tooyour páginas de sitio
#### <a name="on-hello-master-page"></a>En la página maestra Hola
Si se puede editar la página principal del sitio de hello, que proporcionarán supervisión para todas las páginas en el sitio de Hola.

Visite la página principal de Hola y modificarlo con SharePoint Designer o cualquier otro editor.

![](./media/app-insights-sharepoint/03-master.png)

Agregar código de hello justo antes de hello </head> etiqueta. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>O, en páginas individuales
toomonitor un conjunto limitado de páginas, agregue el script de Hola por separado tooeach página. 

Insertar un elemento web e insertar el fragmento de código de hello en ella.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Visualización de los datos de la aplicación
Vuelva a implementar la aplicación.

Hoja de aplicaciones tooyour devuelto en hello [portal de Azure](https://portal.azure.com).

eventos primera Hola se definirán en la búsqueda. 

![](./media/app-insights-sharepoint/09-search.png)

Si espera más datos, haga clic en Actualizar después de unos segundos.

En la hoja de información general de hello, haga clic en **análisis de uso** toosee toocharts de usuarios, sesiones y vistas de página:

![](./media/app-insights-sharepoint/06-usage.png)

Haga clic en cualquier toosee gráfico más detalles: por ejemplo vistas de página:

![](./media/app-insights-sharepoint/07-pages.png)

O Usuarios:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Captura del identificador de usuario
fragmento de código de página web estándar de Hello no captura el Id. de usuario de Hola desde SharePoint, pero puede hacerlo con una pequeña modificación.

1. Copie la clave de instrumentación de la aplicación de hello Essentials desplegable en Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Sustituya la clave de instrumentación de Hola para "XXXX" en el siguiente fragmento de Hola. 
2. Incruste scripts de hello en la aplicación de SharePoint en lugar de fragmento de código de hello que obtener del portal de Hola.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Pasos siguientes
* [Pruebas Web](app-insights-monitor-web-app-availability.md) toomonitor disponibilidad de Hola de su sitio.
* [Application Insights](app-insights-overview.md) para otros tipos de aplicación.

<!--Link references-->


