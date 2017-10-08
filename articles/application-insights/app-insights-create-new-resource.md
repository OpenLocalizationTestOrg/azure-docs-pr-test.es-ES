---
title: un nuevo recurso de Azure Application Insights aaaCreate | Documentos de Microsoft
description: "Describe la configuración manual de la supervisión de Application Insights para una nueva aplicación activa."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Creación de recursos en Application Insights
Azure Application Insights muestra los datos de la aplicación en un *recurso*de Microsoft Azure. Crear un nuevo recurso, por tanto, forma parte de [configurar Application Insights toomonitor una nueva aplicación][start]. En muchos casos, crear un recurso puede realizarse automáticamente Hola IDE. Pero en algunos casos, se crea un recurso manualmente, por ejemplo, se genera toohave recursos independientes para el desarrollo y producción de la aplicación.

Después de haber creado el recurso de hello, podrá obtener su clave de instrumentación y utilizar ese hello tooconfigure SDK en la aplicación hello. enlaces de clave de recursos de Hola Hola recursos toohello de telemetría.

## <a name="sign-up-toomicrosoft-azure"></a>Suscribirse a Azure tooMicrosoft
Si todavía no dispone de una [cuenta Microsoft, obtenga una ahora](http://live.com). (Si usa servicios como Outlook.com, OneDrive, Windows Phone o XBox Live, ya tiene una cuenta Microsoft).

También necesita una suscripción demasiado[Microsoft Azure](http://azure.com). Si su equipo u organización tiene una suscripción de Azure, propietario de hello puede agregarle tooit, con su Windows Live ID. Solo se le cobrará por lo que use. plan básico de Hello predeterminada permite que una determinada cantidad de uso experimental de forma gratuita.

Si tienes acceso tooa suscripción, inicie sesión en visión tooApplication en [http://portal.azure.com](https://portal.azure.com)y usar su toologin Live ID.

## <a name="create-an-application-insights-resource"></a>Creación de recursos en Application Insights
Hola [portal.azure.com](https://portal.azure.com), agregar un recurso de información de la aplicación:

![Haga clic en Nuevo, Application Insights.](./media/app-insights-create-new-resource/01-new.png)

* **Tipo de aplicación** afecta a lo que ve en la hoja de información general de Hola y Hola propiedades [explorer métrica][metrics]. Si no ve el tipo de aplicación, elija General.
* **suscripción** es su cuenta de pago de Azure.
* **grupo de recursos** resulta práctico para administrar las propiedades, como el control de acceso. Si ya ha creado otros recursos de Azure, puede elegir este recurso nuevo tooput Hola mismo grupo.
* **ubicación** es donde se guardan los datos.
* **PIN toodashboard** coloca un icono de acceso rápido para el recurso en la página principal de Azure. Se recomienda su uso.

Cuando se haya creado la aplicación, se abrirá una nueva hoja. En esta hoja podrá ver datos de uso y rendimiento sobre la aplicación. 

tooget atrás tooit próxima vez que inicie sesión en tooAzure, busque el icono de inicio rápido de la aplicación en hello iniciar Panel (pantalla principal). O haga clic en Examinar toofind lo.

## <a name="copy-hello-instrumentation-key"></a>Copie la clave de instrumentación de Hola
clave de instrumentación de Hello identifica recursos de Hola que ha creado. Necesita toogive toohello SDK.

![Haga clic en Essentials, haga clic en hello clave de instrumentación, CTRL + c.](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Instalar SDK de hello en la aplicación
Instalar Hola Application Insights SDK en la aplicación. Este paso depende en gran medida en el tipo de saludo de la aplicación. 

Usar Hola Instrumental clave tooconfigure [Hola SDK que se instala en la aplicación][start].

Hola SDK incluye módulos estándar que envían telemetría sin necesidad de toowrite cualquier código. las acciones del usuario tootrack o diagnosticar problemas con más detalle, [usar API de hello] [ api] toosend su propio telemetría.

## <a name="monitor"></a>Visualización de los datos de telemetría
Cerrar Hola rápido inicio hoja de aplicaciones de hoja tooreturn tooyour Hola portal de Azure.

Haga clic en toosee de icono de búsqueda de hello [búsqueda diagnóstico][diagnostic], dónde aparecen los primeros eventos de Hola. 

Si espera más datos, haga clic en **Actualizar** después de unos segundos.

## <a name="creating-a-resource-automatically"></a>Creación de un recurso de forma automática
Puede escribir un [script de PowerShell](app-insights-powershell.md) toocreate un recurso automáticamente.

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un panel](app-insights-dashboards.md)
* [Búsqueda de diagnóstico](app-insights-diagnostic-search.md)
* [Exploración de métricas](app-insights-metrics-explorer.md)
* [Escribir consultas de Analytics](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

