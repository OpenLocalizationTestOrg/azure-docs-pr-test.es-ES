---
title: "aaaTroubleshoot análisis de visión de la aplicación de Azure | Documentos de Microsoft"
description: "¿Problemas con Analytics de Application Insights? Comience aquí. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Solución de problemas de Analytics en Application Insights
¿Problemas con [Analytics de Application Insights](app-insights-analytics.md)? Comience aquí. Análisis de es Hola eficaz herramienta de búsqueda de Azure Application Insights.

## <a name="limits"></a>límites
* En la actualidad, resultados de la consulta son toojust limitado durante una semana de datos pasados.
* Exploradores en los que la hemos probado: últimas ediciones de Chrome, Edge e Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Extensiones de explorador incompatibles conocidas
* Ghostery

Deshabilitar la extensión de Hola o use un explorador diferente.

## <a name="e-a"></a> "Error inesperado"
![Pantalla de error inesperado](./media/app-insights-analytics-troubleshooting/010.png)

Error interno durante el tiempo de ejecución del portal: excepción no controlada.

* Limpiar la memoria caché del explorador de Hola. 

## <a name="e-b"></a>403... inténtelo tooreload
![403... inténtelo tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso). portal de Hello no puede tener ninguna manera de recuperar demasiado sin cambiar la configuración del explorador.

* Comprobar [están habilitadas las cookies de terceros](#cookies) en el Explorador de Hola. 

## <a name="authentication"></a>403... compruebe la zona de seguridad
![403... compruebe la zona de seguridad](./media/app-insights-analytics-troubleshooting/030.png)

Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso). portal de Hello no puede tener ninguna manera de recuperar demasiado sin cambiar la configuración del explorador.

1. Comprobar [están habilitadas las cookies de terceros](#cookies) en el Explorador de Hola. 
2. ¿Usó un favorito, marcador o portal de análisis de vínculo guardado tooopen Hola? ¿Se inició sesión con credenciales diferentes a las que utilizó cuando guarda vínculo Hola?
3. Pruebe a usar una ventana de exploración privada o de incógnito (después de cerrar todas estas ventanas). Tendrá tooprovide sus credenciales. 
4. Abra otra ventana del explorador (normal) y vaya demasiado[Azure](https://portal.azure.com). Cierre la sesión. A continuación, abra el vínculo e inicie sesión con las credenciales correctas de Hola.
5. Los usuarios de Edge y de Internet Explorer también pueden recibir este error cuando no se admite la configuración de zona Sitios de confianza.
   
    Comprobar ambos [portal de análisis de](https://analytics.applicationinsights.io) y [portal de Azure Active Directory](https://portal.azure.com) están en hello misma zona de seguridad:
   
   * En Internet Explorer, abra **Opciones de Internet**, **Seguridad**, **Sitios de confianza**, **Sitios**:
     
     ![Cuadro de diálogo Opciones de Internet, si se agrega un sitio tooTrusted sitios](./media/app-insights-analytics-troubleshooting/033.png)
     
     En la lista de sitios Web de hello, si cualquiera de las siguientes direcciones URL de Hola se incluyen, asegúrese de que ese Hola otros también se incluyen:
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Recurso no encontrado
![404 ... recurso no encontrado](./media/app-insights-analytics-troubleshooting/040.png)

Los recursos de la aplicación se eliminaron de Application Insights y ya no están disponibles. Esto puede ocurrir si ha guardado la página de análisis de toohello de dirección URL de Hola.

## <a name="e-e"></a>403 ... Sin autorización
![403 ... no autorizado](./media/app-insights-analytics-troubleshooting/050.png)

No tienes permiso tooopen esta aplicación en el análisis.

* ¿Se obtuvo el vínculo de Hola de otra persona? Pídales que estén en hello toomake [lectores o colaboradores para este grupo de recursos](app-insights-resources-roles-access-control.md).
* ¿Ha guardado vínculo Hola con credenciales diferentes? Abra hello [portal de Azure](https://portal.azure.com), cierre la sesión y, a continuación, inténtelo de nuevo, este vínculo proporcionar las credenciales correctas de Hola.

## <a name="html-storage"></a>403 ... Almacenamiento de HTML5
Nuestro portal utiliza localStorage y sessionStorage de HTML5.

* Chrome: Configuración, Privacidad, Configuración de contenido.
* Internet Explorer: Opciones de Internet, pestaña Opciones avanzadas, Seguridad, Habilitar el almacenamiento DOM

![403... Intente almacenamiento tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Suscripción no encontrada
![404 ... Suscripción no encontrada](./media/app-insights-analytics-troubleshooting/070.png)

Hola URL no es válida. 

* Abra el recurso de aplicación hello en [portal de Application Insights](https://portal.azure.com). A continuación, utilice botón de análisis de Hola.

## <a name="e-h"></a>404... la página no existe
![404 ... La página no existe](./media/app-insights-analytics-troubleshooting/080.png)

Hola URL no es válida.

* Abra el recurso de aplicación hello en [portal de Application Insights](https://portal.azure.com). A continuación, utilice botón de análisis de Hola.

## <a name="cookies"></a>Habilitar cookies de terceros
  Vea [cómo toodisable de terceros cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), pero tenga en cuenta que necesitamos demasiado**habilitar** ellos.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

