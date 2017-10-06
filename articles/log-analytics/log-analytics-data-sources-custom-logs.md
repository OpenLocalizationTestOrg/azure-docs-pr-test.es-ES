---
title: "aaaCollect personalizado que se registra en el análisis de registros de OMS | Documentos de Microsoft"
description: "Log Analytics puede recopilar eventos de archivos de texto en equipos Windows y Linux.  Este artículo describe cómo toodefine un nuevo registro personalizado y detalles de los registros de hello crean en el repositorio de OMS Hola."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Registros personalizados de Log Analytics
origen de datos de los registros personalizados de Hello en análisis de registros permite toocollect eventos de los archivos de texto en los equipos Windows y Linux. Archivos de tootext de información en lugar de los servicios de registro estándar como el registro de eventos de Windows o Syslog de registro de muchas aplicaciones.  Una vez recopilados, puede analizar cada registro de registro de hello en campos de tooindividual mediante hello [campos personalizados](log-analytics-custom-fields.md) característica de análisis de registros.

![Recopilación de registros personalizados](media/log-analytics-data-sources-custom-logs/overview.png)

toobe de archivos de registro de Hello recopilan debe coincidir con hello siguiendo criterios.

- registro de Hello debe tener una única entrada por línea o bien un marca de tiempo que coincida con uno de los siguientes Hola dé formato al principio de Hola de cada entrada.

    AAAA-MM-DD HH:MM:SS <br>M/D/AAAA HH:MM:SS AM/PM <br>Lun DD,AAAA HH:MM:SS

- archivo de registro de Hello no debe permitir actualizaciones circulares donde se sobrescribe el archivo hello con las nuevas entradas.
- archivo de registro de Hello debe utilizar la codificación ASCII o UTF-8.  No se admiten otros formatos, como UTF-16.

>[!NOTE]
>Si hay entradas duplicadas en el archivo de registro de hello, análisis de registros recopilará ellos.  Sin embargo, los resultados de búsqueda de hello serán incoherentes donde resultados del filtro Hola mostrar de recuento de resultados de hello más eventos.  Será importante que se pueden valida Hola registro toodetermine si la aplicación hello que crea está causando este comportamiento y solucionarlo si es posible antes de crear la definición de la colección de hello registro personalizado.  
>
  
## <a name="defining-a-custom-log"></a>Definición de un registro personalizado
Usar hello siguiendo el procedimiento toodefine un archivo de registro personalizado.  Desplazamiento final de toohello de este artículo para ver un tutorial de un ejemplo de cómo agregar un registro personalizado.

### <a name="step-1-open-hello-custom-log-wizard"></a>Paso 1. Abra Hola Asistente de registro personalizado
Hola Asistente de registro personalizado se ejecuta en el portal de OMS de Hola y permite toodefine un nuevo toocollect de registro personalizado.

1. En el portal de OMS de hello, vaya demasiado**configuración**.
2. Haga clic en **Datos** y en **Registros personalizados**.
3. De forma predeterminada, todos los cambios de configuración se insertan automáticamente agentes tooall.  Para los agentes de Linux, un archivo de configuración se envía el recopilador de datos de toohello Fluentd.  Si desea que este archivo manualmente en cada agente de Linux toomodify, a continuación, desactive la casilla de hello *aplicar la siguiente máquinas de Linux de configuración toomy*.
4. Haga clic en **agregar +** tooopen Hola Asistente de registro personalizado.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Paso 2: Carga y análisis de un registro de ejemplo
Primero debe cargar una muestra de registro personalizado de Hola.  Asistente de Hello analizar y mostrar las entradas de hello en este archivo para toovalidate.  Análisis de registros usará delimitador Hola especificar tooidentify cada registro.

**Nueva línea** es el delimitador predeterminado de Hola y se usa para archivos de registro que tienen una sola entrada por línea.  Si la línea hello comienza con una fecha y hora en uno de los formatos disponibles hello, entonces puede especificar un **Timestamp** delimitador que admite las entradas que abarcan más de una línea.

Si se usa un delimitador de marca de tiempo, propiedad TimeGenerated de Hola de cada registro almacenado en OMS se rellenará con hello, fecha y hora especificada para esa entrada en el archivo de registro de hello.  Si se usa un delimitador de línea nueva, TimeGenerated se rellena con la fecha y hora en que el análisis de registros recopila entrada Hola.

> [!NOTE]
> Análisis de registros actualmente trata Hola fecha y hora procedentes de un registro utilizando un delimitador de marca de tiempo como hora UTC.  Zona de horaria de hello toouse modificada en el agente de hello será pronto.
>
>

1. Haga clic en **examinar** y busque el archivo de ejemplo tooa.  Tenga en cuenta que este botón puede llamarse **Choose File** (Elegir archivo) en algunos exploradores.
2. Haga clic en **Siguiente**.
3. Hola Asistente de registro personalizado permite cargar archivos y lista registros Hola Hola que lo identifica.
4. Cambiar delimitador de Hola que es usado tooidentify un nuevo registro y el delimitador de hello select que mejor identifique los registros de hello en el archivo de registro.
5. Haga clic en **Siguiente**.

### <a name="step-3-add-log-collection-paths"></a>Paso 3: Incorporación de rutas de recopilación de registros
Debe definir una o más rutas de acceso en agente Hola donde pueda encontrar registro personalizado de Hola.  Se pueden proporcionar una ruta de acceso específica y el nombre de archivo de registro de hello, o puede especificar una ruta de acceso con un carácter comodín para el nombre de Hola.  Esto admite aplicaciones que crean un archivo nuevo cada día o cuando un archivo alcanza un tamaño determinado.  También puede proporcionar varias rutas de acceso para un solo archivo de registro.

Por ejemplo, una aplicación podría crear un archivo de registro cada día con fecha de hello incluido en el nombre de hello como en log20100316.txt. Puede ser un patrón para un registro de este tipo *registro\*.txt* que aplicaría el archivo de registro tooany tras la aplicación hello de nombres del esquema.

Hello tabla siguiente proporciona ejemplos de patrones válidos toospecify diferentes archivos de registro.

| Descripción | Ruta de acceso |
|:--- |:--- |
| Todos los archivos en *C:\Logs* con la extensión .txt en el agente de Windows |C:\Logs\\\*.txt |
| Todos los archivos en *C:\Logs* con un nombre que empieza con "registro" y una extensión .txt en el agente de Windows |C:\Logs\log\*.txt |
| Todos los archivos en */var/log/audit* con la extensión .txt en el agente de Linux |/var/log/audit/*.txt |
| Todos los archivos en */var/log/audit* con un nombre que empieza con "registro" y una extensión .txt en el agente de Linux |/var/log/audit/log\*.txt |

1. Seleccione Windows o Linux toospecify qué formato de ruta de acceso que va a agregar.
2. Escriba la ruta de acceso de Hola y haga clic en hello  **+**  botón.
3. Repita el proceso de Hola para las rutas de acceso adicionales.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Paso 4 Proporcione un nombre y una descripción para el registro de hello
Hello nombre que especifique se usará para el tipo de registro de hello como se describió anteriormente.  Siempre termina con _CL toodistinguish, como un registro personalizado.

1. Escriba un nombre para el registro de hello.  Hola  **\_CL** sufijo se proporciona automáticamente.
2. Agregue una **Descripción**opcional.
3. Haga clic en **siguiente** definición de registro personalizado de toosave Hola.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Paso 5. Validar que se recopilan los registros personalizados de Hola
Puede llevar hasta hora tooan para los datos iniciales de Hola de un tooappear de registro personalizado nuevo en análisis de registros.  Empezará a recopilar entradas de hello registros se encuentran en la ruta de acceso de hello especificado desde el punto de Hola que Hola definido personalizado inicia sesión.  No conservará las entradas de Hola que ha cargado durante la creación del registro personalizadas hello, pero recopilará entradas ya existentes en los archivos de registro de hello que busca.

Una vez que el análisis de registros empieza a recopilar de registro personalizado de hello, sus registros estarán disponibles con una búsqueda de registros.  Usar el nombre de Hola que proporcionó Hola inicio de sesión personalizada como hello **tipo** en la consulta.

> [!NOTE]
> Si no está presente en búsqueda de Hola Hola RawData propiedad, puede necesita tooclose y vuelva a abrir el explorador.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Paso 6. Analizar las entradas del registro personalizadas Hola
entrada de registro completa de Hola se almacenará en una propiedad única denominada **RawData**.  Probablemente le interesará tooseparate Hola datos diferentes en cada entrada en las propiedades individuales almacenados en el registro de hello.  Esto se hace mediante hello [campos personalizados](log-analytics-custom-fields.md) característica de análisis de registros.

Los pasos detallados para analizar la entrada de registro personalizada hello no se muestran a continuación.  Consulte toohello [campos personalizados](log-analytics-custom-fields.md) documentación para obtener esta información.

## <a name="disabling-a-custom-log"></a>Deshabilitación de un registro personalizado
No se puede quitar una definición de registro personalizado una vez que se ha creado, pero se puede deshabilitar mediante la eliminación de todas sus rutas de recopilación.

1. En el portal de OMS de hello, vaya demasiado**configuración**.
2. Haga clic en **Datos** y en **Registros personalizados**.
3. Haga clic en **detalles** toodisable de definición de registro personalizado toohello siguiente.
4. Quite cada una de las rutas de acceso de colección de Hola de definición de registro personalizado de Hola.

## <a name="data-collection"></a>Colección de datos
Log Analytics recopilará nuevas entradas de cada registro personalizado aproximadamente cada 5 minutos.  agente de Hello registrará su lugar en cada archivo de registro que recopila de.  Si agente Hola se queda sin conexión durante un período de tiempo, a continuación, análisis de registros recopilará entradas desde donde se quedó, incluso si se crearon las entradas mientras el agente de hello estaba sin conexión.

contenido completo de Hola Hola de entrada del registro se escribe tooa propiedad única denominada **RawData**.  Se puede analizar en varias propiedades que se pueden analizar y buscar por separado mediante la definición de [campos personalizados](log-analytics-custom-fields.md) después de haber creado el registro de hello personalizadas.

## <a name="custom-log-record-properties"></a>Propiedades de las entradas del registro personalizado
Entradas del registro personalizadas tienen un tipo con el nombre del registro de hello que se proporciona y Hola propiedades en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| TimeGenerated |Fecha y hora en que Hola registro recopiló el inventario por análisis de registros.  Si el registro de hello usa un delimitador basado en tiempo es tiempo Hola recopilado de entrada de Hola. |
| SourceSystem |Tipo de registro del agente de Hola se recopilaron de. <br> OpsManager: agente de Windows, ya sea una conexión directa o System Center Operations Manager <br> Linux: todos los agentes de Linux. |
| RawData |Texto completo de hello recopila entrada. |
| ManagementGroupName |Nombre del grupo de administración de Hola para los agentes de System Center Operations Manage.  En el caso de los otros agentes, es AOI-\<id. de área de trabajo\>. |

## <a name="log-searches-with-custom-log-records"></a>Búsquedas de registros con entradas de registros personalizados
Registros de registros personalizados se almacenan en el repositorio OMS hello como registros de cualquier otro origen de datos.  Tienen un tipo con el mismo nombre de Hola que proporcione al definir el registro de hello, por lo que puede usar la propiedad de tipo hello en los registros de tooretrieve búsqueda recopilados desde un registro específico.

Hello tabla siguiente proporciona diferentes ejemplos de búsquedas de registros que recuperar registros de registros personalizados.

| Consultar | Descripción |
|:--- |:--- |
| Type=MyApp_CL |Todos los eventos de un registro personalizado llamado MyApp_CL. |
| Type=MyApp_CL Severity_CF=error |Todos los eventos de un registro personalizado llamado MyApp_CL con el valor *error* en un campo personalizado llamado *Severity_CF*. |

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.

> | Consultar | Descripción |
|:--- |:--- |
| MyApp_CL |Todos los eventos de un registro personalizado llamado MyApp_CL. |
| MyApp_CL &#124; donde Severity_CF=="error" |Todos los eventos de un registro personalizado llamado MyApp_CL con el valor *error* en un campo personalizado llamado *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Ejemplo de tutorial de agregar un registro personalizado
Hello siguiente sección le guía a través de un ejemplo de cómo crear un registro personalizado.  registro de ejemplo de Hola se recopilan tiene una única entrada en cada línea a partir de una fecha y campos de tiempo y, a continuación, delimitada por comas de código, el estado y el mensaje.  A continuación se muestran varias entradas de ejemplo.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Carga y análisis de un registro de ejemplo
Proporcionamos uno de los archivos de registro de hello y puede ver eventos de Hola que recopilarán.  En este caso, una nueva línea es un delimitador suficiente.  Si una única entrada en el registro de hello podría abarcar varias líneas sin embargo, un delimitador de marca de tiempo tendría toobe usa.

![Carga y análisis de un registro de ejemplo](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Incorporación de rutas de recopilación de registros
archivos de registro de Hello se ubicará en *C:\MyApp\Logs*.  Se creará un nuevo archivo cada día con un nombre que incluye la fecha de hello en patrón de hello *appYYYYMMDD.log*.  Un patrón suficiente para este registro sería *C:\MyApp\Logs\\\*.log*.

![Ruta de recopilación de registros](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Proporcione un nombre y una descripción para el registro de hello
Use el nombre *MyApp_CL* y escriba una descripción en el campo **Descripción**.

![Nombre de registro](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Validar que se recopilan los registros personalizados de Hola
Utilizaremos una consulta de *tipo = MyApp_CL* tooreturn todos los registros de registro recopilados Hola.

![Consulta del registro sin campos personalizados](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Analizar las entradas del registro personalizadas Hola
Usamos Hola de campos personalizados toodefine *EventTime*, *código*, *estado*, y *mensaje* campos y podemos ver la diferencia de Hola Hola registros devueltos por la consulta de Hola.

![Consulta del registro con campos personalizados](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Pasos siguientes
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse entradas de hello en registro personalizado de hello en campos de tooindividual.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.
