---
title: anotaciones de aaaRelease para Application Insights | Documentos de Microsoft
description: "Agregar implementación o crear marcadores gráficos de explorador de métricas de tooyour en Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Anotaciones sobre gráficos de métricas en Application Insights
En las anotaciones sobre gráficos del [Explorador de métricas](app-insights-metrics-explorer.md) se muestra donde ha implementado una nueva compilación u otros eventos importantes. Hacen fácil toosee si los cambios tenían ningún efecto en el rendimiento de la aplicación. Se pueden crear automáticamente por hello [sistema de compilación de Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). También puede crear anotaciones tooflag cualquier evento que desee por [crearlos desde PowerShell](#create-annotations-from-powershell).

![Ejemplo de anotaciones con correlación visible con el tiempo de respuesta del servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Publicar anotaciones con una compilación de VSTS

Anotaciones de versión son una característica de generación de hello en la nube y la versión de servicio de Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Instalar extensión de anotaciones de hello (una vez)
toobe toocreate capaz de versión anotaciones, necesitará tooinstall uno de hello muchas extensiones de servicio de equipo disponibles en Hola Visual Studio Marketplace.

1. Inicie sesión en tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) proyecto.
2. En Visual Studio Marketplace, [obtener extensión de anotaciones de la versión de Hola](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)y agregar cuenta de Team Services tooyour.

![En la parte superior derecha de página web de Team Services, abra Marketplace. Seleccione Visual Studio Team Services y después, en Generar y versión, elija Ver más.](./media/app-insights-annotations/10.png)

Solo necesita toodo esta vez para la cuenta de Visual Studio Team Services. Las anotaciones de versión se pueden configurar ahora para cualquier proyecto de su cuenta. 

### <a name="configure-release-annotations"></a>Configurar anotaciones de versión

Se necesita la clave de tooget una API diferente para cada plantilla de versión VSTS.

1. Inicie sesión en toohello [Portal de Microsoft Azure](https://portal.azure.com) y abra el recurso de Application Insights de Hola que supervisa su aplicación. (O bien, [cree uno ahora](app-insights-overview.md), si aún no lo ha hecho).
2. Abra **Acceso a la API**, **Id. de Application Insights**.
   
    ![En portal.azure.com, abra el recurso de Application Insights y elija Configuración. Abra el Acceso a la API. Copiar Hola Id. de aplicación](./media/app-insights-annotations/20.png)

4. En otra ventana del explorador, abra (o cree) plantilla de versión de Hola que administra las implementaciones de Visual Studio Team Services. 
   
    Agregue una tarea y seleccione una tarea de anotación de versión de información de aplicación de Hola de menú de Hola.
   
    Hola pegar **identificador de la aplicación** que copió de hello hoja de acceso de la API.
   
    ![En Visual Studio Team Services, abra Versión, seleccione una definición de versión y elija Editar. Haga clic en Agregar tarea y seleccione Anotación de versión de Application Insights. Hola pegar información de Id. de aplicaciones.](./media/app-insights-annotations/30.png)
4. Conjunto hello **APIKey** variable del campo de tooa `$(ApiKey)`.

5. En hello ventana de Azure, cree una nueva clave de API y realizar una copia de él.
   
    ![Hola hoja de acceso de API en hello Azure ventana, haga clic en crear clave de API. Proporcione un comentario, compruebe las anotaciones de escritura y haga clic en Generar clave. Copie Hola nueva clave.](./media/app-insights-annotations/40.png)

6. Abra la ficha de configuración de Hola de plantilla de versión de Hola.
   
    Cree una definición de variable para `ApiKey`.
   
    Pegue la definición de variable ApiKey de toohello clave de API.
   
    ![En la ventana de Team Services hello, seleccione la ficha de configuración de Hola y haga clic en Agregar Variable. Establecer Hola nombre tooApiKey y en valor hello, pegue clave Hola que acaba de generar y haga clic en el icono de candado de Hola.](./media/app-insights-annotations/50.png)
7. Por último, **guardar** Hola definición de versión.


## <a name="view-annotations"></a>Ver anotaciones
Ahora, siempre que se use Hola versión plantilla toodeploy una nueva versión, se enviará a una anotación tooApplication visión. anotaciones de Hello aparecerán en los gráficos en el Explorador de métricas.

Haga clic en los detalles de tooopen de marcador de anotación sobre versión hello, así como solicitante, bifurcación de control de código fuente, definición de versión, entorno y mucho más.

![Haga clic en cualquier marcador de anotación de la versión.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Crear anotaciones personalizadas desde PowerShell
También puede crear anotaciones desde cualquier proceso que desee (sin usar VS Team System). 


1. Hacer una copia local de hello [secuencia de comandos de Powershell desde GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Obtener Id. de aplicación Hola y crear una clave de API de hello hoja de acceso de la API.

3. Llamar al script de Hola similar al siguiente:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Es script de Hola toomodify fácil, por ejemplo toocreate anotaciones para hello anterior.

## <a name="next-steps"></a>Pasos siguientes

* [Crear elementos de trabajo](app-insights-diagnostic-search.md#create-work-item)
* [Automation con PowerShell](app-insights-powershell.md)
