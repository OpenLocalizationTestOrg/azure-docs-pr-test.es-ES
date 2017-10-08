---
title: "exportación de aaaContinuous de telemetría de Application Insights | Documentos de Microsoft"
description: "Exportar toostorage de datos de diagnóstico y uso de Microsoft Azure y descargarla desde allí."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Exportación de telemetría desde Application Insights
¿Desea tookeep la telemetría durante más tiempo que el período de retención estándar de hello? ¿O quiere procesarla de algún modo especializado? La exportación continua es lo más conveniente para ello. eventos de Hola que se ven en el portal de Application Insights Hola pueden ser exportado toostorage en Microsoft Azure en formato JSON. Desde allí se puede descargar los datos y escribir cualquier código que se necesita tooprocess lo.  

El uso de la exportación continua puede conllevar un cargo adicional. Consulte su [modelo de fijación de precios](http://azure.microsoft.com/pricing/details/application-insights/).

Antes de configurar la exportación continua, hay algunas alternativas que puede querer tooconsider:

* botón de exportación de Hello en parte superior de Hola de una hoja de métricas o buscar permite transferir spreadsheet de Excel tooan de tablas y gráficos.

* [Analytics](app-insights-analytics.md) proporciona un lenguaje de consulta eficaz para telemetría. También puede exportar los resultados.
* Si está pensando demasiado[explorar los datos en Power BI](app-insights-export-power-bi.md), puede hacerlo sin usar exportar continua.
* Hola [API de REST de acceso a datos](https://dev.applicationinsights.io/) le permite tener acceso mediante programación a la telemetría.

Después de exportar continua copia su toostorage de datos (donde puede permanecer siempre como sea necesario), está todavía disponible en Application Insights para saludo habitual [período de retención](app-insights-data-retention-privacy.md).

## <a name="setup"></a>Creación de una exportación continua.
1. En hello recurso de Application Insights para su aplicación, abra exportar continua y elija **agregar**:

    ![Desplácese hacia abajo y haga clic en Exportación continua.](./media/app-insights-export-telemetry/01-export.png)

2. Elegir tipos de datos de telemetría de hello desea tooexport.

3. Cree o seleccione un [cuenta de almacenamiento de Azure](../storage/common/storage-introduction.md) donde desea toostore Hola datos.

    > [!Warning]
    > De forma predeterminada, la ubicación de almacenamiento de Hola se establecerá toohello misma región geográfica que el recurso de Application Insights. Si los almacena en una región diferente, puede conllevar gastos de transferencia.

    ![Haga clic en Agregar, Destino de exportación, Cuenta de almacenamiento y cree un nuevo almacén o elija uno almacén.](./media/app-insights-export-telemetry/02-add.png)

4. Cree o seleccione un contenedor de almacenamiento de hello:

    ![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/create-container.png)

Una vez que ha creado la exportación, comienza el proceso. Solo obtiene los datos que llegan después de crear la exportación de Hola.

Puede haber un retraso de aproximadamente una hora antes de que los datos aparecen en el almacenamiento de Hola.

### <a name="tooedit-continuous-export"></a>exportación de tooedit continua

Si desea que los tipos de evento de hello toochange más tarde, edite exportación hello:

![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>exportación de toostop continua

exportación de hello toostop, haga clic en deshabilitar. Al hacer clic en habilitar de nuevo, se reiniciará exportación Hola con nuevos datos. No obtendrá datos Hola que han llegado en el portal de hello mientras estaba deshabilitada la exportación.

exportación de hello toostop, eliminarlo de forma permanente. Al realizar esta acción no se eliminan los datos del almacenamiento.

### <a name="cant-add-or-change-an-export"></a>¿No puede agregar o cambiar una exportación?
* exportaciones de tooadd o cambiar, necesita derechos de acceso de propietario, Colaborador o colaborador de la información de aplicación. [Más información sobre los roles][roles].

## <a name="analyze"></a> ¿Qué eventos obtiene?
Hello datos exportados están telemetría sin procesar de Hola que recibimos desde su aplicación, salvo que se agregue datos de ubicación que se calculan Hola dirección IP de cliente.

Datos que se ha descartado por [muestreo](app-insights-sampling.md) no se incluye en hello exportan datos.

No se incluyen otras métricas calculadas. Por ejemplo, no Exportamos uso promedio de la CPU, pero Exportamos telemetría de hello sin formato desde el que se calcula la media de Hola.

Hello datos también incluyen los resultados de Hola de cualquier [disponibilidad las pruebas web](app-insights-monitor-web-app-availability.md) que ha configurado.

> [!NOTE]
> **Muestreo.** Si la aplicación envía una gran cantidad de datos, característica de muestreo de Hola puede operar y enviar sólo una fracción de telemetría de hello generado. [Aprenda más sobre el muestreo.](app-insights-sampling.md)
>
>

## <a name="get"></a>Inspeccionar los datos de Hola
Puede inspeccionar almacenamiento Hola directamente en el portal de Hola. Haga clic en **Examinar**, seleccione la cuenta de almacenamiento y abra **Contenedores**.

tooinspect almacenamiento de Azure en Visual Studio, abra **vista**, **nube explorador**. (Si no tiene ese comando de menú, necesita tooinstall hello Azure SDK: Hola abierto **nuevo proyecto** cuadro de diálogo, expanda Visual C# y de la nube y elija **obtener Microsoft Azure SDK para .NET**.)

Al abrir el almacén de blobs, verá un contenedor con un conjunto de archivos blob. Hola URI de cada archivo que se deriva de su nombre de recurso de Application Insights, su clave de instrumentación, telemetría-tipo, fecha y hora. (nombre de recurso de hello está en minúsculas y clave de instrumentación de hello omite guiones).

![Inspeccionar Hola el almacén de blobs con una herramienta apropiada](./media/app-insights-export-telemetry/04-data.png)

Hola fecha y hora son UTC y cuando telemetría Hola se deposita en almacén de hello: tiempo de presentación no se generó. Por lo que si se escribe código toodownload Hola dato, puede mover a través de los datos de Hola linealmente.

A continuación aparece el formulario de Hola de ruta de acceso de hello:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`es hora blob se creó en hello interno de almacenamiento provisional almacenamiento
* `blobDeliveryTimeUtc`es el momento de hello cuando está copiada toohello exportación destino almacenamiento blob

## <a name="format"></a> Formato de datos
* Cada blob es un archivo de texto que contiene varias filas separadas por' \n'. Contiene telemetría Hola procesado durante un período de tiempo de aproximadamente la mitad de un minuto.
* Cada fila representa un punto de datos de telemetría, como una vista de página o una solicitud.
* Cada fila es un documento JSON sin formato. Si desea toosit y te quedas mirando en él, ábralo en Visual Studio y elija Editar, avanzadas, archivo de formato:

![Vista Hola telemetría con una herramienta apropiada](./media/app-insights-export-telemetry/06-json.png)

Las duraciones de tiempo son tics, donde 10 000 tics = 1 ms. Por ejemplo, estos valores muestran un tiempo de 1 ms toosend una solicitud de explorador hello, 3ms tooreceive y 1.8s tooprocess Hola página en el Explorador de hello:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Procesamiento de datos de Hola
En una escala pequeña, puede escribir algunas toopull código alejados de los datos, leer en una hoja de cálculo y así sucesivamente. Por ejemplo:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

Para obtener un ejemplo de código más grande, consulte el [uso de un rol de trabajo][exportasa].

## <a name="delete"></a>Eliminación de los datos antiguos
Tenga en cuenta que usted es responsable de administrar la capacidad de almacenamiento y eliminar datos antiguos de hello si es necesario.

## <a name="if-you-regenerate-your-storage-key"></a>Si vuelve a generar la clave de almacenamiento...
Si cambia el almacenamiento de claves tooyour hello, exportación continua dejará de funcionar. Verá una notificación en su cuenta de Azure.

Abra hoja exportar continua de Hola y edite la exportación. Editar Hola exportar destino, pero deje Hola mismo almacenamiento seleccionado. Haga clic en Aceptar tooconfirm.

![Editar Hola continua exportar, abra y cierre tres destino de exportación.](./media/app-insights-export-telemetry/07-resetstore.png)

exportación continua Hola se reiniciará.

## <a name="export-samples"></a>Ejemplos de exportación

* [Exportar tooSQL mediante el análisis de transmisiones][exportasa]
* [Ejemplo 2 de Stream Analytics](app-insights-export-stream-analytics.md)

En escalas más grandes, considere la posibilidad de [HDInsight](https://azure.microsoft.com/services/hdinsight/) -clústeres de Hadoop en la nube de Hola. HDInsight proporciona una variedad de tecnologías para administrar y analizar grandes cantidades de datos y podría utilizar tooprocess datos que se han exportado desde Application Insights.

## <a name="q--a"></a>Preguntas y respuestas
* *Lo único que quiero es una descarga única de un gráfico.*  

    Sí, puede hacerlo. En la parte superior de Hola de hoja de hello, haga clic en **exportar datos**.
* *Configuro una exportación, pero no hay ningún dato en el almacén.*

    ¿Application Insights recibió cualquier telemetría de la aplicación desde que ha configurado la exportación de hello? Solo recibirá datos nuevos.
* *Intentó tooset de una exportación, pero se denegó el acceso*

    Si cuenta Hola pertenece a su organización, deberá toobe un miembro de los grupos de los propietarios o colaboradores de Hola.
* *¿Se pueden exportar un almacén local propio toomy recta?*

    Lamentablemente, no. Nuestro motor de exportación actualmente solo funciona con el almacenamiento de Azure.  
* *¿Hay cualquier cantidad de toohello límite de datos que pone en el almacén my?*

    No. Le mantenemos datos hasta que se elimina la exportación de Hola. Se detendrá si encontramos límites hello para el almacenamiento de blobs, pero esto es bastante grande. Es una tooyou toocontrol cuánto almacenamiento usa.  
* *¿Blobs cuántos debo ver en el almacenamiento de hello?*

  * Para el tipo de datos de cada tooexport seleccionada, un nuevo blob se crea cada minuto (si los datos están disponibles).
  * Además, para las aplicaciones con mucho tráfico, se asignan unidades de partición adicionales. En este caso, cada unidad crea un blob cada minuto.
* *Volver a generar almacenamiento de claves toomy de Hola o ha cambiado el nombre de Hola de contenedor de Hola y ahora no funciona la exportación de Hola.*

    Editar exportación hello y abra la hoja de destino de exportación de Hola. Dejar Hola mismo almacenamiento seleccionado como antes y haga clic en Aceptar tooconfirm. La exportación se reiniciará. Si cambió de hello en hello pocos días pasados, no perderá los datos.
* *¿Puedo hacer una pausa de exportación de hello?*

    Sí. Haga clic en Deshabilitar.

## <a name="code-samples"></a>Ejemplos de código

* [Ejemplo de Stream Analytics](app-insights-export-stream-analytics.md)
* [Exportar tooSQL mediante el análisis de transmisiones][exportasa]
* [Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
