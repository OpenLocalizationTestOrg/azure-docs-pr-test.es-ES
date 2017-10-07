---
title: "campos de aaaCustom de análisis de registros | Documentos de Microsoft"
description: "característica de campos personalizados de Hola de análisis de registros permite toocreate sus propios campos de búsqueda de datos de OMS que agregar toohello propiedades de un registro recopilado.  Este artículo describe el proceso de hello toocreate un campo personalizado y ofrece un tutorial detallado con un evento de muestreo."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Campos personalizados de Log Analytics
Hola **campos personalizados** característica de análisis de registros permite tooextend los registros existentes en el repositorio OMS Hola agregando sus propios campos de búsqueda.  Campos personalizados se rellenan automáticamente con los datos extraídos de otras propiedades Hola mismo registro.

![Introducción a los campos personalizados](media/log-analytics-custom-fields/overview.png)

Por ejemplo, el registro de ejemplo de Hola siguiente tiene datos útiles ocultos en la descripción del evento Hola.  Si estos datos se extraen en diferentes propiedades, estarán disponibles para ciertas acciones, como la ordenación y el filtrado.

![Botón Log Search (Búsqueda de registros)](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> En vista previa de hello, son campos personalizados de too100 limitado en el área de trabajo.  Este límite se ampliará cuando esta característica esté disponible con carácter general.
> 
> 

## <a name="creating-a-custom-field"></a>Creación de un campo personalizado
Cuando se crea un campo personalizado, análisis de registros debe comprender qué toopopulate de toouse datos su valor.  Usa una tecnología de Microsoft Research denominada FlashExtract tooquickly identificar estos datos.  En lugar de requerir tooprovide instrucciones explícitas, análisis de registros obtiene información acerca de los datos de hello desea tooextract de ejemplos que proporciona.

Hola las secciones siguientes proporciona procedimiento hello para la creación de un campo personalizado.  En hello final de este artículo es un tutorial de una extracción de ejemplo.

> [!NOTE]
> campo personalizado de Hola se rellena como registros Hola coincidente especifica los criterios se agregan toohello almacén de datos OMS, por lo que sólo aparecerá en los registros recopilados después de crea el campo personalizado de Hola.  campo personalizado de Hello no agregará toorecords que ya están en el almacén de datos de hello cuando se crea.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Paso 1: identificar los registros que tendrán Hola de campo personalizado
Hola primer paso es registros de hello tooidentify que obtendrán Hola de campo personalizado.  Comience con un [búsqueda de registros estándar](log-analytics-log-searches.md) y, a continuación, seleccione un tooact de registro como modelo de Hola que análisis de registros obtendrá información.  Cuando se especifica que se van tooextract datos en un campo personalizado, Hola **Asistente para la extracción de campos** se abre en validar y refinar los criterios de Hola.

1. Vaya demasiado**Log Search** y usar un [consultar los registros de hello tooretrieve](log-analytics-log-searches.md) que tendrán el campo personalizado de Hola.
2. Seleccione un registro que análisis de registros usará tooact como un modelo para extraer campos de datos toopopulate Hola personalizados.  Deberá identificar Hola datos que desee tooextract de este registro y análisis de registros usará esta información toodetermine Hola lógica toopopulate Hola campo personalizado para todos los registros similares.
3. Haga clic en hello botón toohello izquierda de cualquier propiedad de texto del programa Hola a registros y seleccione **extraer campos de**.
4. Hola **se abre el Asistente para la extracción de campos**, y registro de hello seleccionado se muestra en hello **Main Example** columna.  campo personalizado de Hola se definirá para aquellos registros con hello mismo valores de propiedades de Hola que están seleccionados.  
5. Si la selección de hello no es exactamente lo que desea, seleccione los criterios de hello toonarrow campos adicionales.  Orden toochange Hola valores de campo para los criterios de hello, debe cancelar y seleccionar un registro diferente que cumpla los criterios de Hola que desee.

### <a name="step-2---perform-initial-extract"></a>Paso 2: Ejecución de la extracción inicial.
Después de identificar los registros de Hola que tendrán el campo personalizado de hello, debe identificar los datos de Hola que desea tooextract.  Análisis de registros usará esta patrones similares para tooidentify información en los registros similares.  En el paso de hello después de esto se puede toovalidate Hola que los resultados sean y proporcionar más detalles para toouse de análisis de registros en su análisis.

1. Resaltar texto hello en el registro de ejemplo de Hola que desea que el campo personalizado de toopopulate Hola.  A continuación, aparecerá con un tooprovide del cuadro de diálogo un nombre para hello campo y tooperform Hola extracción inicial.  Hola caracteres  **\_CF** automáticamente se anexará.
2. Haga clic en **extraer** tooperform un análisis de registros recopilados.  
3. Hola **resumen** y **resultados de la búsqueda** secciones muestran resultados de Hola de extracción de hello, por lo que puede inspeccionar su precisión.  **Resumen** muestra hello criterios usados tooidentify registros y un recuento para cada uno de los valores de datos de hello identificados.  **Resultados de la búsqueda** proporciona una lista detallada de los registros que coincidan con los criterios de Hola.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Paso 3: comprobar la exactitud de extracción de Hola y crear el campo personalizado
Una vez que ha llevado a cabo la extracción inicial hello, análisis de registros mostrará sus resultados en función de los datos que ya se han recopilado.  Si los resultados de hello ser precisos puede crear campos personalizados de hello sin ningún trabajo adicional.  Si no es así, puede refinar los resultados de Hola para que análisis de registros pueda mejorar su lógica.

1. Si los valores de extracción inicial de hello no están correctos, a continuación, haga clic en hello **editar** tooan siguiente inexactos registro de icono y seleccione **modificar este resaltado** de selección de orden toomodify Hola.
2. entrada Hello es copiada toohello **ejemplos adicionales** sección debajo hello **Main Example**.  Puede ajustar Hola resaltado aquí toohelp análisis de registros entender selección Hola debería haber realizado.
3. Haga clic en **extraer** toouse registra este tooevaluate información nueva todos Hola existente.  se pueden modificar los resultados de Hola para los registros que no sea de hello uno que acaba de modificar basándose en esta nueva inteligencia.
4. Continuar tooadd correcciones hasta que todos los registros de hello extraer correctamente identifican Hola datos toopopulate Hola nuevo campo personalizado.
5. Haga clic en **Save Extract** cuando esté satisfecho con los resultados de Hola.  campo personalizado de Hello ya está definido, pero no se agregará tooany registros todavía.
6. Espera para los nuevos registros coincidentes Hola especifica criterios toobe recopila y, a continuación, ejecute de nuevo la búsqueda de registros de Hola. Nuevos registros deben tener el campo personalizado de Hola.
7. Usar Hola campo personalizado como cualquier otra propiedad del registro.  Puede usar tooaggregate y agrupar datos y usarlo incluso tooproduce nuevos puntos de vista.

## <a name="viewing-custom-fields"></a>Presentación de los de campos personalizados
Puede ver una lista de todos los campos personalizados en el grupo de administración de hello **configuración** icono de panel de OMS Hola.  Seleccione **Datos** y después **Campos personalizados** para obtener una lista de todos los campos personalizados del área de trabajo.  

![Custom Fields](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Eliminación de un campo personalizado
Hay dos tooremove de formas de un campo personalizado.  Hola primero es hello **quitar** opción para cada campo al ver la lista completa de hello como se describió anteriormente.  Hola otro método es tooretrieve que un toohello de botón de Hola de registro y haga clic en izquierda del campo de Hola.  menú de Hello tendrá un campo personalizado de opción tooremove Hola.

## <a name="sample-walkthrough"></a>Tutorial de ejemplo
Hello siguiente sección le guía a través de un ejemplo completo de cómo crear un campo personalizado.  En este ejemplo extrae el nombre del servicio hello en los eventos de Windows que indican un cambio de estado de servicio.  Esto se basa en los eventos creados por el Administrador de Control de servicios en registro del sistema hello en los equipos de Windows.  Si desea toofollow en este ejemplo, debe ser [recopilar eventos de información de registro del sistema hello](log-analytics-data-sources-windows-events.md).

Escribimos Hola después tooreturn consulta todos los eventos del servicio Administrador de Control que tiene un identificador de evento 7036 que es el evento de Hola que indica que un servicio, iniciar o detener.

![Consultar](media/log-analytics-custom-fields/query.png)

A continuación, seleccionamos cualquier registro con el identificador de evento 7036.

![Registro de origen](media/log-analytics-custom-fields/source-record.png)

Queremos que el nombre de servicio de Hola que aparece en hello **RenderedDescription** propiedades y seleccione Hola botón siguiente toothis.

![Extraer campos](media/log-analytics-custom-fields/extract-fields.png)

Hola **Asistente para la extracción de campos** se abre y Hola **EventLog** y **EventID** campos están seleccionados en hello **Main Example** columna.  Esto indica que ese campo personalizado Hola se definirá para los eventos del registro del sistema Hola con un identificador de evento 7036.  Esto es suficiente, por lo que no es necesario tooselect cualquier otro campo.

![Main Example](media/log-analytics-custom-fields/main-example.png)

Se resalte el nombre de hello del servicio de Hola Hola **RenderedDescription** propiedad y use **servicio** nombre del servicio tooidentify Hola.  campo personalizado de Hola se denominará **Service_CF**.

![Título del campo](media/log-analytics-custom-fields/field-title.png)

Vemos que el nombre servicio Hola se identifica correctamente para algunos registros, pero no para otros.   Hola **resultados de la búsqueda** muestran que parte del nombre de Hola para hello **WMI Performance Adapter** no estaba seleccionado.  Hola **resumen** muestra que cuatro registros con **DPRMA** servicio incluía incorrectamente una palabra de más y dos registros identificados **Modules Installer** en lugar de **Windows Modules Installer**.  

![Search Results](media/log-analytics-custom-fields/search-results-01.png)

Empezaremos con hello **WMI Performance Adapter** registro.  Hacemos clic en el icono de edición y luego en **Modify this highlight**(Modificar texto resaltado).  

![Modificar texto resaltado](media/log-analytics-custom-fields/modify-highlight.png)

Ampliamos palabra Hola de hello resaltado tooinclude **WMI** y, a continuación, vuelva a ejecutar Hola extracción.  

![Ejemplo adicional](media/log-analytics-custom-fields/additional-example-01.png)

Podemos ver que hello las entradas de **WMI Performance Adapter** están corregidas y análisis de registros usó esa información toocorrect registra de Hola para **Windows Module Installer**.  Podemos ver Hola **resumen** sección que **DPMRA** se sigue sin identificarse correctamente.

![Search Results](media/log-analytics-custom-fields/search-results-02.png)

Estamos desplácese registro tooa con hello servicio DPMRA y utilizar Hola mismo proceso toocorrect que el registro.

![Ejemplo adicional](media/log-analytics-custom-fields/additional-example-02.png)

 Al ejecutar Hola extracción, podemos ver que todos nuestros resultados son ahora precisos.

![Search Results](media/log-analytics-custom-fields/search-results-03.png)

Podemos ver que **Service_CF** se crea pero no se agregó todavía tooany registros.

![Recuento inicial](media/log-analytics-custom-fields/initial-count.png)

Una vez transcurrido un tiempo por lo que new los eventos se recopilan, podemos ver que Hola **Service_CF** campo se agrega toorecords que coincide con nuestros criterios.

![Resultados finales](media/log-analytics-custom-fields/final-results.png)

Ahora podemos usar campos personalizados de hello como cualquier otra propiedad de registro.  tooillustrate esto, creamos una consulta que agrupa por hello nueva **Service_CF** tooinspect campo los servicios que están más activo Hola.

![Agrupar por consulta](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) consultas toobuild con campos personalizados para los criterios.
* Supervise los [archivos de registro personalizados](log-analytics-data-sources-custom-logs.md) que se analizan con campos personalizados.

