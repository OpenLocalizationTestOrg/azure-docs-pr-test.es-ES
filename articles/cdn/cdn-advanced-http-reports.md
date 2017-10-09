---
title: "informes de HTTP de avanzados de estadísticas de uso de aaaAnalyze con CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate había avanzada informes HTTP en la red CDN de Microsoft Azure. Estos informes proporcionan información detallada sobre la actividad de la red CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Análisis de estadísticas de uso con los informes de HTTP avanzados de la red CDN de Azure
## <a name="overview"></a>Información general
En este documento se explican los informes de HTTP avanzados en la red CDN de Microsoft Azure. Estos informes proporcionan información detallada sobre la actividad de la red CDN.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Acceso a los informes de HTTP avanzados
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **informes avanzados de HTTP** ventana flotante.  Haga clic en **Plataforma grande HTTP**.
   
    ![Portal de administración de la red CDN: menú Informes avanzados](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Se muestran las opciones de informe.

## <a name="geography-reports-map-based"></a>Informes de geografía (basados en mapas)
Hay cinco informes que aprovechan las ventajas de un mapa tooindicate regiones Hola desde el que se solicita el contenido. Estos informes son World Map, United States Map, Canada Map, Europe Map y Asia Pacific Map.

Cada informe basada en mapas clasifica entidades geográficas (es decir, países, Estados y provincias) según toohello porcentaje de aciertos que se originó en dicha región. Además, un mapa es siempre toohelp, ver ubicaciones Hola desde el que se solicita el contenido. Es capaz de toodo para mediante la codificación de colores de cada región según la cantidad de toohello de petición consiguió en dicha región. Las regiones más claras indican una demanda menor de contenido y las más oscuras indican mayores niveles de petición de contenido.

Se proporciona información detallada de tráfico y ancho de banda para cada región directamente debajo de la asignación de Hola. Esto le permite número total de hello tooview de aciertos, el porcentaje de Hola de aciertos, la cantidad total de Hola de datos transferidos (en gigabytes) y porcentaje de Hola de datos transferidos para cada región. Consulte una descripción de cada una de estas métricas. Por último, cuando mantenga el mouse sobre una región (es decir, país, estado o provincia), nombre de Hola y el porcentaje de Hola de aciertos de que se ha producido en la región de Hola se mostrará como una información sobre herramientas.

Se proporciona más abajo una descripción breve de cada tipo de informe de geografía basado en mapas.

| Nombre del informe | Descripción |
| --- | --- |
| World Map |Este informe permite petición en todo el mundo de hello tooview contenido de la red CDN. Cada país está codificada por colores en hello world mapa tooindicate Hola porcentaje de aciertos que se originó en dicha región. |
| United States Map |Este informe permite tooview demanda de hello para el contenido CDN Hola Estados Unidos. Cada estado con código de color en este porcentaje de mapa tooindicate Hola de aciertos que se originó en dicha región. |
| Canada Map |Este informe permite tooview demanda de hello para el contenido CDN en Canadá. Cada provincia con código de color en este porcentaje de mapa tooindicate Hola de aciertos que se originó en dicha región. |
| Europe Map |Este informe permite tooview demanda de hello para el contenido CDN en Europa. Cada país con código de color en este porcentaje de mapa tooindicate Hola de aciertos que se originó en dicha región. |
| Asia Pacific Map |Este informe permite tooview demanda de hello para el contenido CDN en Asia. Cada país con código de color en este porcentaje de mapa tooindicate Hola de aciertos que se originó en dicha región. |

## <a name="geography-reports-bar-charts"></a>Informes de geografía (gráficos de barras)
Hay dos informes adicionales que proporcionan información estadística según toogeography, que son ciudades de la parte superior y países de la parte superior. Estos informes clasifican ciudades y países, respectivamente, según el número de toohello de aciertos que se originó en esas regiones. Tras generar este tipo de informe, un gráfico de barras se indicará top 10 ciudades de Hola o países que solicitó contenido a través de una plataforma específica. Este gráfico de barras permite tooquickly evaluar las regiones de Hola que generan Hola mayor número de solicitudes para su contenido.

lado izquierdo de Hola de gráfico de hello (eje y) indica la cantidad de hits ha producido en la región especificada de Hola. Directamente debajo de gráfico de hello (eje x), encontrará una etiqueta para cada una de hello top 10 regiones.

### <a name="using-hello-bar-charts"></a>Usar gráficos de barras Hola
* Si mantiene el mouse sobre una barra, nombre de Hola y Hola el número total de aciertos de que se ha producido en la región de Hola se mostrará como una información sobre herramientas.
* información sobre herramientas de Hola Hola informes de ciudades de la parte superior identifica una ciudad por su nombre, el estado o provincia y la abreviatura del país.
* Si no se pudo determinar la ciudad de Hola o región (es decir, estado o provincia) desde el que se originó una solicitud, se indicará que es desconocidos. Si el país de hello es desconocido, dos signos de interrogación (es decir,??), se mostrará.
* Un informe puede incluir las métricas para "Europe" o hello "Asia-Pacífico/región". Los elementos no están diseñados tooprovide información estadística relativa a todas las direcciones IP en esas regiones. En su lugar, solo se aplican toorequests que se originan de direcciones IP que se expanden horizontalmente en Europa y Asia/Pacífico en lugar de tooa determinada ciudad o país.

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará el número total de Hola de aciertos, porcentaje de Hola de aciertos, cantidad de Hola de datos transferidos (en gigabytes), y porcentaje de Hola de datos transferidos para Hola 250 regiones superiores. Consulte una descripción de cada una de estas métricas.

A continuación se proporciona una breve descripción para ambos tipos de informes.

| Nombre del informe | Descripción |
| --- | --- |
| Top Cities |Este informe clasifica según el número de toohello de aciertos que se originó en dicha región de ciudades. |
| Top Countries |Este informe clasifica países según el número de toohello de aciertos que se originó en dicha región. |

## <a name="daily-summary"></a>Daily Summary
Hola informe de resumen diaria permite a número total de hello tooview de aciertos y los datos transferidos a través de una plataforma concreta a diario. Esta información puede utilizarse tooquickly discernir los patrones de actividad de red CDN. Por ejemplo, este informe puede ayudar a detectar qué días han tenido un tráfico mayor o menor que el previsto.

Tras generar este tipo de informe, un gráfico de barras proporcionará una indicación visual como toohello cantidad de demanda específica de la plataforma con experiencia a diario en hello período de tiempo cubierto por el informe de Hola. Lo hará, mostrando una barra para cada día en el informe de Hola. Por ejemplo, al seleccionar Hola período de tiempo denominado "Última semana" generará un gráfico de barras con siete barras. Cada barra indicará el número total de Hola de aciertos que se ha producido ese día.

Hello lado izquierdo del gráfico de hello (eje y) indica la cantidad de hits ha ocurrido en hello especificado fecha. Directamente debajo de gráfico de hello (eje x), encontrará una etiqueta que indica la fecha de hello (formato: aaaa-MM-DD) para cada día que se incluyen en el informe de Hola.

> [!TIP]
> Si mantiene el mouse sobre una barra, número total de Hola de aciertos ocurridos en esa fecha se mostrará como una información sobre herramientas.
> 
> 

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará número total de Hola de aciertos y cantidad de Hola de datos transferidos (en gigabytes) para cada día abarcado por el informe de Hola.

## <a name="by-hour"></a>By Hour
Hola informes por hora permite a número total de hello tooview de aciertos y los datos transferidos a través de una plataforma concreta cada hora. Esta información puede utilizarse tooquickly discernir los patrones de actividad de red CDN. Por ejemplo, este informe puede ayudarle a detectar Hola períodos de tiempo durante el día de Hola que experimentar superior o inferior al tráfico previsto.

Tras generar este tipo de informe, un gráfico de barras proporcionará una indicación visual como toohello cantidad de demanda específica de la plataforma que se ha producido en cada hora sobre Hola período de tiempo cubierto por el informe de Hola. Lo hará, mostrando una barra para cada hora abarcado por el informe de Hola. Por ejemplo, si se selecciona un período de tiempo de 24 horas, se generará un gráfico de barras con veinticuatro barras. Cada barra indicará el número total de Hola de aciertos que se ha producido durante esa hora.

lado izquierdo de Hola de gráfico de hello (eje y) indica la cantidad de hits ha ocurrido en hora indicada Hola. Directamente debajo de gráfico de hello (eje x), encontrará una etiqueta que indica la fecha y hora de hello (formato: aaaa-MM-DD hh: mm) para cada hora incluido en el informe de Hola. Notifique el tiempo con el formato de 24 horas y se especifica utilizando la zona horaria de hello UTC/GMT.

> [!TIP]
> Si mantiene el mouse sobre una barra, se mostrará el número total de Hola de aciertos ocurridos durante esa hora como una información sobre herramientas.
> 
> 

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará número total de Hola de aciertos y cantidad de Hola de datos transferidos (en gigabytes) para cada hora abarcado por el informe de Hola.

## <a name="by-file"></a>By File
Hola por archivo de informe permite tooview Hola cantidad de tráfico de hello y petición generada a través de una plataforma concreta para hello más solicitado activos. Tras generar este tipo de informe, se generará un gráfico de barras en hello top 10 más solicitados los activos sobre Hola período de tiempo especificado.

> [!NOTE]
> Para fines de Hola de este informe, las direcciones URL de borde CNAME son direcciones URL CDN equivalentes tootheir convertido. Esto permite que un recuento preciso para el número total de Hola de aciertos asociados a un activo sin tener en cuenta CDN Hola o toorequest de dirección URL de CNAME utilizada de borde.
> 
> 

lado izquierdo de Hola de gráfico de hello (eje y) indica número Hola de solicitudes para cada activo sobre Hola período de tiempo especificado. Directamente debajo de gráfico de hello (eje x), se encuentra en una etiqueta que indica el nombre de archivo de Hola para cada uno de hello top 10 solicitado activos.

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará la siguiente información para cada uno de los activos solicitados 250 superior Hola de hello: ruta de acceso relativa, el número total de Hola de aciertos, el porcentaje de Hola de aciertos, la cantidad de Hola de datos transferidos (en gigabytes) y el porcentaje de Hola de datos transferidos.

## <a name="by-file-detail"></a>By File Detail
Hola informe de detalle por archivo permite tooview cantidad de Hola de hello y petición tráfico que se incurre en una plataforma concreta para un activo específico. En hello parte superior de este informe es Hola detalles de archivo para la opción. Esta opción proporciona una lista de los activos más solicitados en la plataforma seleccionada Hola. En orden toogenerate un informe de detalles por archivo, será necesario tooselect Hola deseado activo Hola detalles de archivo para la opción. Transcurrido ese período, un gráfico de barras se indicará la cantidad de Hola de demanda diaria que genera durante Hola período de tiempo especificado.

lado izquierdo de Hola de gráfico de hello (eje y) indica el número total de Hola de solicitudes que ha tenido un activo en un día determinado. Directamente debajo de gráfico de hello (eje x), encontrará una etiqueta que indica la fecha de hello (formato: aaaa-MM-DD) para que informe a petición CDN para Hola se notificó activo.

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará número total de Hola de aciertos y cantidad de Hola de datos transferidos (en gigabytes) para cada día abarcado por el informe de Hola.

## <a name="by-file-type"></a>By File Type
Hola informes por tipo de archivo permite tooview Hola cantidad de tráfico de petición y Hola producido por el tipo de archivo. Tras generar este tipo de informe, un gráfico de anillos indicará porcentaje Hola de las correspondencias generadas por los primeros tipos de archivo 10 Hola.

> [!TIP]
> Si mantiene el mouse sobre un segmento de gráfico de anillos hello, tipo de medio de Internet de Hola de que el tipo de archivo se mostrará como una información sobre herramientas.
> 
> 

pueden verse datos Hola gráfico de anillos de hello toogenerate usado por debajo de él. Allí encontrará Hola nombre de archivo tipo de medio de extensión/Internet, número total de Hola de aciertos, porcentaje de Hola de aciertos de, cantidad Hola de datos transferidos (en gigabytes) y porcentaje de datos transferidos para cada uno de Hola Hola principales 250 tipos de archivo.

## <a name="by-directory"></a>By Directory
informe de directorio por Hello permite tooview cantidad de Hola de hello y petición tráfico que se incurre en una plataforma concreta para el contenido desde un directorio específico. Tras generar este tipo de informe, un gráfico de barras se indicará el número total de Hola de las correspondencias generadas por el contenido de los principales 10 directorios de Hola.

### <a name="using-hello-bar-chart"></a>Usar el gráfico de barras de Hola
* Mantenga el mouse sobre una barra de directorio correspondiente del toohello tooview Hola ruta de acceso relativa.
* El contenido almacenado en una subcarpeta de un directorio no cuenta al calcular la demanda por directorio. Este cálculo se basa exclusivamente en número Hola de solicitudes generadas para el contenido almacenado en el directorio real de Hola.
* Para fines de Hola de este informe, las direcciones URL de borde CNAME son direcciones URL CDN equivalentes tootheir convertido. Esto permite que un recuento preciso para todas las estadísticas asociadas a un activo sin tener en cuenta CDN Hola o toorequest de dirección URL de CNAME utilizada de borde.

Hello lado izquierdo del gráfico de hello (eje y) indica Hola número total de solicitudes de contenido de hello almacenados en los 10 directorios principales. Cada barra en el gráfico de hello representa un directorio. Hola usar códigos de colores esquema toomatch una barra tooa directorio aparece en la sección superior 250 completa directorios de Hola.

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará Hola siguiente información para cada uno de los directorios de la parte superior a 250 de hello: ruta de acceso relativa, el número total de Hola de aciertos, el porcentaje de Hola de aciertos, la cantidad de Hola de datos transferidos (en gigabytes) y el porcentaje de Hola de datos transferidos.

## <a name="by-browser"></a>By Browser
Hola informes por explorador permite tooview qué exploradores estaban usado toorequest contenido. Tras generar este tipo de informe, un gráfico circular indicará el porcentaje de Hola de solicitudes administradas por hello top 10 de los exploradores.

### <a name="using-hello-pie-chart"></a>Uso de gráfico circular de Hola
* Mantenga el mouse sobre un segmento de hello gráfico circular tooview nombre del explorador y la versión.
* Para fines de Hola de este informe, cada combinación única/versión del explorador se considera un explorador diferente.
* sector de Hello denominado "Otros" indica porcentaje Hola de solicitudes administradas por todos los otros exploradores y versiones.

se pueden ver datos Hola Hola toogenerate usa un gráfico circular por debajo de él. Allí encontrará Hola explorador tipo/número de versión número total de Hola de aciertos y porcentaje de Hola de resultados para cada uno de los exploradores de 250 superior Hola.

## <a name="by-referrer"></a>By Referrer
Hola informes por referencia permite tooview Hola remitentes principales toocontent en la plataforma seleccionada Hola. Un origen de referencia indica hostname Hola desde el que se generó una solicitud. Tras generar este tipo de informe, un gráfico de barras indicará cantidad Hola de demanda (es decir, aciertos) generado por remitentes de 10 principales Hola.

lado izquierdo de Hola de gráfico de hello (eje y) indica el número total de Hola de solicitudes que ha tenido un activo para cada origen de referencia. Cada barra en el gráfico de hello representa un origen de referencia. Hola usar códigos de colores esquema toomatch una barra tooa referrer enumerados en la sección superior 250 Referrer de Hola.

datos de Hola que era el gráfico de barras de hello toogenerate utilizadas se pueden ver por debajo de él. Allí encontrará dirección URL de hello, número total de Hola de aciertos y porcentaje de Hola de aciertos generados a partir de cada uno de los remitentes de 250 principales Hola.

## <a name="by-download"></a>By Download
Hola por descargar informe permite tooanalyze patrones de descarga para el contenido más solicitado. parte superior de Hola de informe de hello contiene un gráfico de barras que compara intenta realizar descargas con descargas completadas para hello top 10 activos solicitados. Cada barra con código de color según toowhether es un intento de descarga (azul) o una descarga completada (verde).

> [!NOTE]
> Para fines de Hola de este informe, las direcciones URL de borde CNAME son direcciones URL CDN equivalentes tootheir convertido. Esto permite que un recuento preciso para todas las estadísticas asociadas a un activo sin tener en cuenta CDN Hola o toorequest de dirección URL de CNAME utilizada de borde.
> 
> 

lado izquierdo de Hola de gráfico de hello (eje y) indica el nombre de archivo de Hola para cada uno de hello top 10 solicitado activos. Directamente debajo de gráfico de hello (eje x), se encuentra en las etiquetas que indican el número total de Hola de descargas ha intentado/finalizada.

Directamente por debajo del gráfico de barras de hello, Hola siguiente información se mostrará en activos solicitados 250 superior hello: ruta de acceso relativa (nombre de archivo incluido), el número de Hola de veces que se encontraba toocompletion descargado, Hola número de veces que se solicitó y Hola porcentaje de solicitudes que dan como resultado una descarga completa.

> [!TIP]
> Un cliente HTTP (es decir, un explorador) no notificará a la red CDN cuando un activo se ha descargado completamente. Como resultado, tenemos toocalculate si un recurso se ha descargado completamente correspondiente códigos toostatus y solicitudes de intervalo de bytes. Hello lo primero que se buscan al realizar este cálculo es si produce un código de 200 estado Aceptar una solicitud de Hola. Si es así, a continuación, veremos tooensure de las solicitudes de intervalo de bytes que cubren activo completo Hola. Por último, se compare cantidad Hola transferidos toohello del tamaño de datos del recurso solicitado Hola. Si se transfieren datos de hello es mayor que el tamaño del archivo de hello tooor igual y las solicitudes de intervalo de bytes de hello son adecuadas para ese recurso, Hola aciertos se contarán como una descarga completa.
> 
> Pagar toohello naturaleza interpretada de este informe, debe mantener en hello cuenta después de puntos que pueden modificar la coherencia de Hola y la precisión de este informe.
> 
> * Los patrones de tráfico no se puede predecir con precisión cuando los agentes de usuario se comportan de manera diferente. Esto puede producir resultados de descarga completada que son superiores al 100 %.
> * Los activos que usan la descarga progresiva de HTTP no se pueden representar con precisión en este informe. Esto es debido a toousers búsqueda toodifferent posiciones en un vídeo.
> 
> 

## <a name="by-404-errors"></a>By 404 Errors
Hola informes de errores por 404 permite a tipo de hello tooidentify de contenido que genera hello más número de códigos de estado 404 no encontrado. parte superior de Hola de informe de hello contiene un gráfico de barras para los activos de 10 mejores hello para el que se devolvió un código de estado 404 no encontrado. Este gráfico de barras compara el número total de Hola de solicitudes con las solicitudes que dan como resultado un código de estado no se encuentra 404 de esos recursos. Cada barra está codificada en colores. Se usa una barra amarilla tooindicate que Hola solicitud dio como resultado un código de estado 404 no encontrado. Se usa una barra roja número total de hello tooindicate de solicitudes de los activos de Hola.

> [!NOTE]
> Para fines de Hola de este informe, tenga en cuenta Hola siguiente:
> 
> * Una visita representa cualquier solicitud de un activo, con independencia del código de estado.
> * Las direcciones URL de borde CNAME son direcciones URL CDN equivalentes tootheir convertido. Esto permite que un recuento preciso para todas las estadísticas asociadas a un activo sin tener en cuenta CDN Hola o toorequest de dirección URL de CNAME utilizada de borde.
> 
> 

lado izquierdo de Hola de gráfico de hello (eje y) indica el nombre de archivo de Hola para cada uno de hello top 10 activos solicitados que dan como resultado un código de estado 404 no encontrado. Directamente debajo de gráfico de hello (eje x), se encuentra en las etiquetas que indican el número total de Hola de solicitudes y número de Hola de solicitudes que dan como resultado un código de estado 404 no encontrado.

Directamente por debajo del gráfico de barras de hello, Hola siguiente información se mostrará en activos solicitados 250 superior hello: ruta de acceso relativa (nombre de archivo incluido), número de Hola de solicitudes que dan como resultado un 404 no encontrado código de estado, número total de Hola de veces que Hola asset era solicitado y Hola porcentaje de solicitudes que dan como resultado un código de estado 404 no encontrado.

## <a name="see-also"></a>Otras referencias
* [Información general de la red CDN de Azure](cdn-overview.md)
* [Estadísticas en tiempo real en CDN de Microsoft Azure](cdn-real-time-stats.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
* [Análisis del rendimiento perimetral](cdn-edge-performance.md)

