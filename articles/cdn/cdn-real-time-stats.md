---
title: "estadísticas de tiempo de aaaReal en la red CDN de Azure | Documentos de Microsoft"
description: "Estadísticas en tiempo real proporciona datos en tiempo real sobre el rendimiento de hello red CDN de Azure para entregar el contenido de los clientes de tooyour contenido."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Estadísticas en tiempo real en la CDN de Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Información general
En este documento se describe la funcionalidad de Estadísticas en tiempo real en la CDN de Microsoft Azure.  Esta funcionalidad proporciona datos en tiempo real, como perfil de ancho de banda, Estados de memoria caché y conexiones simultáneas tooyour CDN para entregar el contenido de los clientes de tooyour contenido. Esto permite la supervisión continua del estado de Hola de su servicio en cualquier momento, incluidos los eventos de puesta en marcha.

Hola siguiendo los gráficos está disponible:

* [Ancho de banda](#bandwidth)
* [Códigos de estado](#status-codes)
* [Estados de la memoria caché](#cache-statuses)
* [Conexiones](#connections)

## <a name="accessing-real-time-stats"></a>Acceso a estadísticas en tiempo real
1. Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
3. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **estadísticas en tiempo real** ventana flotante.  Haga clic en **Objeto grande HTTP**.
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    se muestran gráficos de estadísticas en tiempo real de Hola.

Cada uno de los gráficos de hello muestra estadísticas en tiempo real para intervalo de tiempo de hello seleccionado, se inicien cuando se carga la página de Hola.  gráficos de Hola se actualizan automáticamente cada pocos segundos.  Hola **Actualizar gráfico** botón, si está presente, borrará gráfico hello, tras el cual solo mostrará datos saludo seleccionado.

## <a name="bandwidth"></a>Ancho de banda
![Gráfico Ancho de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

Hola **ancho de banda** gráfico muestra la cantidad de Hola de ancho de banda utilizado para la plataforma actual de hello en el intervalo de tiempo de hello seleccionado. parte sombreado de Hola de gráfico de hello indica el uso de ancho de banda. cantidad exacta de Hola de ancho de banda que se está usando actualmente se muestra directamente por debajo del gráfico de líneas de Hola.

## <a name="status-codes"></a>Códigos de estado
![Gráfico Código de estado](./media/cdn-real-time-stats/cdn-status-codes.png)

Hola **códigos de estado** gráfico indica con qué frecuencia se producen ciertos códigos de respuesta HTTP a través intervalo de tiempo de hello seleccionado.

> [!TIP]
> Para obtener una descripción de cada opción de código de estado de HTTP, consulte [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Códigos de estado HTTP de la red CDN de Azure).
> 
> 

Se muestra una lista de códigos de estado HTTP directamente sobre el gráfico de Hola. Esta lista indica cada código de estado que puede incluirse en el gráfico de líneas de Hola y el número actual de Hola de repeticiones por segundo para ese código de estado. De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado en el gráfico de Hola. Sin embargo, puede elegir tooonly códigos de estado de monitor Hola que tienen un significado especial para la configuración de red CDN. toodo, comprobar los códigos de estado deseado de Hola y desactive todas las demás opciones, haga clic en **Actualizar gráfico**. 

También puede ocultar temporalmente los datos registrados para un determinado código de estado.  En leyenda de hello directamente por debajo del gráfico de hello, haga clic en código de estado de Hola que quiere toohide. código de estado de Hola se ocultará en gráfico de hello inmediatamente. Haga clic de nuevo en ese código de estado provocará que toobe opción volverá a aparecer.

## <a name="cache-statuses"></a>Estados de la memoria caché
![Gráfico Estado de caché](./media/cdn-real-time-stats/cdn-cache-status.png)

Hola **Estados de memoria caché** gráfico indica con qué frecuencia se producen ciertos tipos de Estados de la memoria caché a través intervalo de tiempo de hello seleccionado. 

> [!TIP]
> Para ver una descripción de cada opción de código de estado de caché, consulte [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Códigos de estado de caché de la red CDN de Azure).
> 
> 

Se muestra una lista de códigos de estado de la memoria caché directamente sobre el gráfico de Hola. Esta lista indica cada código de estado que puede incluirse en el gráfico de líneas de Hola y el número actual de Hola de repeticiones por segundo para ese código de estado. De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado en el gráfico de Hola. Sin embargo, puede elegir tooonly códigos de estado de monitor Hola que tienen un significado especial para la configuración de red CDN. toodo, comprobar los códigos de estado deseado de Hola y desactive todas las demás opciones, haga clic en **Actualizar gráfico**. 

También puede ocultar temporalmente los datos registrados para un determinado código de estado.  En leyenda de hello directamente por debajo del gráfico de hello, haga clic en código de estado de Hola que quiere toohide. código de estado de Hola se ocultará en gráfico de hello inmediatamente. Haga clic de nuevo en ese código de estado provocará que toobe opción volverá a aparecer.

## <a name="connections"></a>Conexiones
![Gráfico Conexiones](./media/cdn-real-time-stats/cdn-connections.png)

Este gráfico indica el número de conexiones se han establecido tooyour borde servidores. Cada solicitud de un recurso que pasa por la red CDN genera una conexión.

## <a name="next-steps"></a>Pasos siguientes
* Recibir notificaciones con [alertas en tiempo real en la CDN de Azure](cdn-real-time-alerts.md)
* Profundizar más con [informes de HTTP avanzados](cdn-advanced-http-reports.md)
* Analizar [patrones de uso](cdn-analyze-usage-patterns.md)

