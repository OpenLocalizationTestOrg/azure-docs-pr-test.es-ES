---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - solicitud de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de solicitudes"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Telemetría de solicitudes: modelo de datos de Application Insights

Un elemento de telemetría de solicitud (en [Application Insights](app-insights-overview.md)) representa hello secuencia lógica de ejecución desencadenada por una aplicación de tooyour solicitudes externas. Único identifica cada ejecución de la solicitud `ID` y `url` que contiene todos los parámetros de ejecución de Hola. Puede agrupar las solicitudes por lógica `name` y definir hello `source` de esta solicitud. La ejecución de código puede ser `success` o `fail`, y tiene una `duration` determinada. Tanto las ejecuciones correctas como las erróneas se pueden seguir agrupando por `resultCode`. Hora de inicio de telemetría de solicitud de hello definido en el nivel de la envoltura de Hola.

Solicitud de telemetría es compatible con el modelo de extensibilidad estándar de hello mediante personalizado `properties` y `measurements`.

## <a name="name"></a>Nombre

Nombre de solicitud de hello representa la solicitud de Hola de tooprocess de ruta de acceso de código. Valor de cardinalidad baja tooallow mejor agrupación de solicitudes. Para las solicitudes HTTP representa Hola método HTTP y la plantilla de ruta de acceso de dirección URL como `GET /values/{id}` sin Hola real `id` valor.

Web de visión de aplicación SDK envía el nombre de la solicitud "tal cual" con lo que respecta tooletter caso. Agrupación de interfaz de usuario distingue mayúsculas de minúsculas para `GET /Home/Index` se cuentan por separado desde `GET /home/INDEX` , aunque a menudo dan lugar a Hola misma ejecución de acción y controlador. Hello motivo de esto es que las direcciones URL en general son [entre mayúsculas y minúsculas](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). Puede que desee toosee si todos los `404` realizado en las direcciones URL de hello escritas en mayúsculas. Puede leer en más solicitud la colección de nombre mediante ASP.Net Web SDK en hello [entrada de blog](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Longitud máxima: 1024 caracteres

## <a name="id"></a>ID

Identificador de una instancia de llamada de solicitud. Se utiliza para la correlación entre la solicitud y otros elementos de telemetría. El identificador debe ser único en todo el mundo. Para obtener más información, vea la página de [correlación](application-insights-correlation.md).

Longitud máxima: 128 caracteres

## <a name="url"></a>URL

URL de solicitud con todos los parámetros de la cadena de consulta.

Longitud máxima: 2048 caracteres

## <a name="source"></a>Origen

Origen de solicitud de saludo. Algunos ejemplos son la clave de instrumentación de hello del autor de llamada de Hola o la dirección de ip de hello del autor de llamada de Hola. Para obtener más información, vea la página de [correlación](application-insights-correlation.md).

Longitud máxima: 1024 caracteres

## <a name="duration"></a>Duración

Duración de la solicitud en formato: `DD.HH:MM:SS.MMMMMM`. Debe ser positiva y tener menos de `1000` días. Este campo es obligatorio, como solicitud telemetría representa la operación de hello con hello principio y al final de Hola.

## <a name="response-code"></a>Response code

Resultado de una ejecución de solicitudes. Código de estado de HTTP para solicitudes HTTP. Puede ser un valor `HRESULT` o un tipo de excepción para otros tipos de solicitudes.

Longitud máxima: 1024 caracteres

## <a name="success"></a>Correcto

Indicación de si la llamada es correcta o no. Este campo es obligatorio. Cuando no se establece explícitamente demasiado`false` -solicitud considera toobe correcto. Establezca este valor demasiado`false` si la operación se ha interrumpido por excepción o devolvió el código de resultado de error.

Para las aplicaciones web de hello, Application Insights definir solicitudes como erróneo cuando el código de respuesta de hello tiene menos hello `400` o igual a demasiado`401`. Sin embargo, hay casos en esta asignación predeterminada no coincide con la semántica de la aplicación hello Hola. El código de respuesta `404` puede indicar que "no hay registros", lo cual puede formar parte de un flujo regular. También puede indicar que un vínculo está roto. Para hello vínculos rotos, incluso se pueden implementar la lógica más avanzada. Puede marcar vínculos rotos como errores sólo cuando esos vínculos se encuentran en hello mediante el análisis de origen de referencia de dirección url del mismo sitio. O bien, márquelos como errores cuando se tiene acceso desde aplicaciones móviles de la compañía de Hola. De igual forma `301` y `302` indica un error cuando se tiene acceso de cliente de Hola que no admite la redirección.

El contenido aceptado parcialmente `206` puede indicar un error de una solicitud general. Por ejemplo, el punto de conexión de Application Insights recibe un lote de elementos de telemetría como una solicitud única. Devuelve `206` cuando algunos elementos de lote de hello no se procesaron correctamente. Tasa creciente de `206` indica un problema que necesita toobe investigar. Esta misma lógica se aplica demasiado`207` varios Estados que puede ser correcto de Hola Hola peor de los códigos de respuesta independiente.

Puede leer más resultados de solicitud de código y el código de estado de hello [entrada de blog](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Propiedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Pasos siguientes

- [Escritura de telemetría de solicitud personalizada](app-insights-api-custom-events-metrics.md#trackrequest)
- Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.
- Obtenga información acerca de cómo demasiado[configurar ASP.NET Core](app-insights-asp-net.md) aplicación con Application Insights.
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
