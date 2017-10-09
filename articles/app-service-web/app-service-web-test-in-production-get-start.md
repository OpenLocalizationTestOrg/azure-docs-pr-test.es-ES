---
title: "aaaGet partió de prueba en producción para las aplicaciones Web"
description: "Obtenga información acerca de hello pruebas en función de la producción (TiP) en aplicaciones de Web del servicio de aplicación de Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Introducción a las pruebas en producción para las aplicaciones web
Las pruebas en producción o pruebas en directo de una aplicación web usando el tráfico de clientes, es una estrategia de prueba que los desarrolladores de aplicaciones integran cada vez más en sus metodologías de [desarrollo ágil](https://en.wikipedia.org/wiki/Agile_software_development) . Le permite tootest calidad de Hola de las aplicaciones con el tráfico de usuario en vivo en el entorno de producción, como datos toosynthesized opuestos en un entorno de prueba. Mediante la exposición de los usuarios nuevos de tooreal de aplicación, pueda estar informado sobre los problemas reales de hello que puede enfrentarse a la aplicación una vez que se implementa. Puede comprobar la funcionalidad de hello, el rendimiento y el valor de las actualizaciones de la aplicación en volumen de hello, progreso y variedad de tráfico de usuario real, que no puede aproximar nunca en un entorno de prueba.

## <a name="traffic-routing-in-app-service-web-apps"></a>Enrutamiento de tráfico en las aplicaciones web del Servicio de aplicaciones
Con el enrutamiento de tráfico de hello de características en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714), puede dirigir una parte de tooone de tráfico de usuario en vivo o más [ranuras de implementación](web-sites-staged-publishing.md)y, a continuación, analizar la aplicación con [aplicación de Azure Visión](/services/application-insights/) o [HDInsight de Azure](/services/hdinsight/), o una herramienta de terceros, como [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate el cambio. Por ejemplo, puede implementar Hola con servicio de aplicaciones de los escenarios siguientes:

* Detectar errores funcionales o identificar los cuellos de botella de rendimiento en la implementación de actualizaciones anteriores toosite todo
* Realizar "vuelos de pruebas controlado" de los cambios mediante la medición de las métricas de facilidad de uso en la aplicación de la versión beta de hello
* Optimizar gradualmente tooa nueva actualización y correctamente hacia abajo de la versión actual de toohello si se produce un error 
* Optimizar los resultados empresariales de su aplicación mediante la ejecución de [pruebas A/B](https://en.wikipedia.org/wiki/A/B_testing) o [pruebas sobre múltiples variables](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) en varias ranuras de implementación

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Requisitos para usar el enrutamiento del tráfico en las aplicaciones web
* La aplicación web se debe ejecutar en los niveles **Estándar** o **Premium**, ya que es lo que se requiere cuando hay varias ranuras de implementación.
* En orden toowork correctamente, el enrutamiento de tráfico requiere toobe las cookies habilitada en el Explorador de los usuarios de Hola. Enrutamiento de tráfico usa toopin una ranura de implementación de cliente explorador tooa de cookies de sesión de cliente de Hola Hola vida.
* El enrutamiento de tráfico admite escenarios avanzados de TiP mediante cmdlets de PowerShell de Azure.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Ranura de implementación de ruta tráfico segmento tooa
En el nivel básico de hello en cada escenario de sugerencia, enrutar una porcentaje predefinido de la ranura de implementación de producción no tooa el tráfico en vivo. toodo, a continuación siga los pasos hello:

> [!NOTE]
> Hello estos pasos se da por supuesto que ya tiene un [ranura de implementación no es de producción](web-sites-staged-publishing.md) y ese Hola desea el contenido de las aplicaciones web ya está [implementa](web-sites-deploy.md) tooit.
> 
> 

1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).
2. En la hoja de la aplicación web, haga clic en **Configuración** > **Enrutamiento de tráfico**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Ranura de hello SELECT que desea que el porcentaje de tooroute tráfico tooand Hola de hello total de tráfico que desee y luego haga clic en **guardar**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Hoja de la ranura de implementación de toohello vaya. Ahora debería ver el tráfico en vivo que se va a tooit enrutado.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Una vez configurado el enrutamiento del tráfico, Hola especificados porcentaje de clientes estarán ranura de tooyour aleatoriamente enrutado no sea de producción. Sin embargo, es importante toonote que una vez que un cliente se tooa automáticamente enrutado específico ranura, estará ranura toothat "anclados" para la vida Hola de esa sesión de cliente. Esto se realiza mediante una sesión de usuario de cookie toopin Hola. Si examina las solicitudes HTTP de hello, encontrará un `TipMix` cookie en cada solicitud posterior.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Forzar la ranura específico de tooa de solicitudes de cliente
En suma tooautomatic enrutamiento del tráfico, servicio de aplicaciones es ranura específico de tooroute capaz de solicitudes tooa. Esto es útil cuando desea que su tooopt capaz de usuarios toobe-en o desactivación de la aplicación de la versión beta. toodo, usar hello `x-ms-routing-name` parámetro de consulta.

tooreroute usuarios tooa ranura específico utilizando `x-ms-routing-name`, debe asegurarse de que esa ranura Hola ya se ha agregado toohello lista de enrutamiento del tráfico. Debido a que desea tooroute tooa ranura explícitamente, no importa el porcentaje de enrutamiento real Hola establece. Si lo desea, puede crear un "vínculo beta" que los usuarios puedan seleccionar tooaccess Hola aplicación beta.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Exclusión voluntaria de la aplicación beta para los usuarios
toolet a los usuarios que no formen parte de la aplicación de la versión beta, por ejemplo, se puede colocar este vínculo en la página web:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Hola cadena `x-ms-routing-name=self` especifica la zona de producción de hello. Una vez hello vínculo de Hola de acceso de explorador de cliente, no solo se redirige toohello ranura de producción, pero todas las solicitudes subsiguientes contendrá hello `x-ms-routing-name=self` cookie que ancla ranura de producción de hello sesión toohello.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Participación de los usuarios de aplicación toobeta
toolet a los usuarios participar en aplicaciones de la versión beta de tooyour, conjunto Hola misma consulta toohello nombre del parámetro de la ranura de no producción de hello, por ejemplo:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Más recursos
* [Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-staged-publishing.md)
* [Implementación predecible de una aplicación compleja en Azure](app-service-deploy-complex-application-predictably.md)
* [Agile Software Development con el Servicio de aplicaciones de Azure](app-service-agile-software-development.md)
* [Uso eficaz de entornos DevOps para las aplicaciones web](app-service-web-staged-publishing-realworld-scenarios.md)

