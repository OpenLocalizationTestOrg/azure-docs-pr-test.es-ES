---
title: "aaaApplication telemetría visión en CodeLens de Visual Studio | Documentos de Microsoft"
description: "Acceda rápidamente a la telemetría de sus solicitudes y excepciones de Application Insights con CodeLens en Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Telemetría de Application Insights en CodeLens de Visual Studio
Métodos en el código de hello de la aplicación web se pueden anotar con la telemetría sobre las excepciones de tiempo de ejecución y tiempos de respuesta de solicitud. Si instala [Azure Application Insights](app-insights-overview.md) en su aplicación, telemetría Hola aparece en Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -Hola notas en la parte superior de Hola de cada función que está acostumbrado tooseeing útil información como el número de Hola de función de hello lugares Hola última persona que editó, o haga referencia.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights en CodeLens está disponible en Visual Studio 2015 Update 3 y posteriores o con la versión más reciente de Hola de [extensión Developer Analytics Tools](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens está disponible en hello ediciones Enterprise y Professional de Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Donde toofind datos de Application Insights
Busque la telemetría de Application Insights en los indicadores de CodeLens Hola de métodos de solicitud pública hello de la aplicación web. Los indicadores de CodeLens se muestran encima del método y de otras declaraciones en el código de C# y Visual Basic. Si hay datos de Application Insights disponibles para un método, verá indicadores de solicitudes y excepciones como "100 solicitudes, 1 % con error" o "10 excepciones". Para más detalles, haga clic en un indicador de CodeLens. 

> [!TIP]
> Application Insights solicitar e indicadores de la excepción pueden tardar unos segundos adicionales tooload después de que aparezcan otros indicadores de CodeLens.
> 
> 

## <a name="exceptions-in-codelens"></a>Excepciones en CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

indicador de CodeLens de excepción de Hello muestra hello de excepciones que se han producido en hello las últimas 24 horas de hello 15 mayoría de las excepciones que ocurren con frecuencia en la aplicación durante ese período, al procesar la solicitud de hello atendida por método hello.

toosee más detalles, haga clic en indicador de CodeLens de hello excepciones:

* cambio de porcentaje de Hello en número de excepciones de hello últimas 24 horas relativa toohello antes de 24 horas
* Elija **vaya toocode** toonavigate toohello de código para la función hello producir excepción Hola
* Elija **búsqueda** tooquery Hola de todas las instancias de esta excepción que se han producido en las últimas 24 horas
* Elija **tendencia** tooview una visualización de tendencia para las repeticiones de esta excepción en hello las últimas 24 horas
* Elija **ver todas las excepciones de esta aplicación** tooquery Hola de todas las excepciones que se han producido en las últimas 24 horas
* Elija **explorar las tendencias de excepción** tooview una visualización de tendencia para todas las excepciones que se han producido en hello las últimas 24 horas. 

> [!TIP]
> Si consulta "0 excepciones" en CodeLens pero sabrá que debería haber excepciones, compruebe que esté seleccionado el recurso de Application Insights derecho Hola en CodeLens toomake. tooselect otro recurso, haga doble clic en el proyecto en el Explorador de soluciones de Hola y elija **Application Insights > Elegir origen de telemetría**. CodeLens solo se muestre para hello 15 mayoría de las excepciones que ocurren con frecuencia en la aplicación en hello las últimas 24 horas, por tanto, si una excepción se Hola con frecuencia más 16 o menos, verá "0 excepciones." Excepciones de vistas ASP.NET no pueden aparecer en los métodos de controlador de Hola que las vistas generan.
> 
> [!TIP]
> Si ve "? las excepciones"en CodeLens, deberá tooassociate que su cuenta de Azure con Visual Studio o sus credenciales de cuenta de Azure puede haber expirado. En ambos casos, haga clic en "? excepciones"y elija **agregar una cuenta...**  tooenter sus credenciales.
> 
> 

## <a name="requests-in-codelens"></a>Solicitudes en CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hello muestra del indicador de CodeLens Hola número de HTTP de solicitud solicita que sido atendidas por un método de hello más allá de 24 horas, además de porcentaje de Hola de esas solicitudes erróneas.

toosee más detalles, haga clic en hello solicita indicador de CodeLens:

* Hola cambios absoluto y el porcentaje en número de solicitudes, solicitudes con error y tiempos de respuesta promedio sobre hello más allá de 24 horas en comparación con toohello anterior 24 horas
* confiabilidad de Hello del método hello, calculado como porcentaje de Hola de solicitudes que no produjo un error en hello las últimas 24 horas
* Elija **búsqueda** solicitudes o tooquery de solicitudes con error todos Hola solicitudes (errores) que se produjeron en hello las últimas 24 horas
* Elija **tendencia** tooview una visualización de tendencia para las solicitudes, las solicitudes con error o medio de respuesta el tiempo de espera en hello las últimas 24 horas.
* Elija el nombre de Hola de hello recursos de Application Insights en hello izquierdo superior de la vista de detalles de hello CodeLens toochange el recurso que es el origen de Hola para los datos de CodeLens.

## <a name="next"></a>Pasos siguientes
|  |  |
| --- | --- |
| **[Trabajo con Application Insights en Visual Studio](app-insights-visual-studio.md)**<br/>Busque la telemetría, consulte los datos de CodeLens y configure Application Insights. Todos desde Visual Studio. |![Haga clic en proyecto de Hola y elija Application Insights, búsqueda](./media/app-insights-visual-studio-codelens/34.png) |
| **[Incorporación de datos adicionales](app-insights-asp-net-more.md)**<br/>Supervise el uso, la disponibilidad, las dependencias y las excepciones. Integrar seguimientos de marcos de registro. Escribir telemetría personalizada. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Trabajar con el portal de Application Insights Hola](app-insights-dashboards.md)**<br/>Paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y exportación de la telemetría. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

