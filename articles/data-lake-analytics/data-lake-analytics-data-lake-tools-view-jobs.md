---
title: "aaaUse Explorador de trabajo y la vista de trabajos de trabajos de análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Explorador de trabajo y la vista de trabajos de trabajos de análisis de Data Lake de Azure. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Usar el explorador de trabajos y la vista de trabajo para trabajos de Azure Data Lake Analytics
archivos de servicio de análisis de Azure Data Lake Hello envían trabajos en una [almacén de consultas](#query-store). En este artículo, aprenderá cómo toouse Explorador de trabajo y la vista de trabajo en Azure Data Lake Tools para Hola de Visual Studio toofind histórico información del trabajo. 

De forma predeterminada, servicio de análisis de Data Lake Hola archiva trabajos de Hola durante 30 días. período de expiración de Hello puede configurarse en hello portal de Azure mediante la configuración de directiva de expiración de saludo personalizado. No será capaz de tooaccess información sobre el trabajo de los Hola tras la expiración. 

## <a name="prerequisites"></a>Requisitos previos
Vea [Data Lake Tools for Visual Studio prerequisites](data-lake-analytics-data-lake-tools-get-started.md#prerequisites) (Requisitos previos de Data Lake Tools para Visual Studio).

## <a name="open-hello-job-browser"></a>Hola Abrir Explorador de trabajo
Acceso Hola Explorador de trabajo a través de **Explorador de servidores > Azure > análisis de Data Lake > trabajos** en Visual Studio.  Hola Explorador de trabajo puede tener acceso el almacén de consultas Hola de una cuenta de análisis de Data Lake. Explorador de trabajo muestra el almacén de consultas en hello izquierda, que muestra información sobre el trabajo básico y vista de trabajos en mostrando derecho Hola detallada información sobre el trabajo.

## <a name="job-view"></a>Vista de trabajo
Vista de trabajos muestra Hola información detallada de un trabajo. tooopen un trabajo, puede haga doble clic en un trabajo en hello Explorador de trabajo, o abrir el menú de Data Lake Hola haciendo clic en la vista de trabajos. Debería ver un cuadro de diálogo que se rellena con la dirección URL de trabajo de Hola.

![Explorador de trabajos de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

La vista de trabajo contiene:

* Resumen del trabajo
  
    Hola vista de trabajos de actualización toosee Hola información más reciente de trabajos en ejecución.
  
  * Estado del trabajo (gráfico):
    
      Estado del trabajo se describen las fases de trabajo de hello:
    
      ![Estado de las fases del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Preparación: Cargar el script toohello en la nube, compilar y optimizar el script de Hola mediante el servicio de compilación de Hola.
    * En cola: Los trabajos están en cola lactosuero están esperando recursos suficientes o trabajos de hello superan trabajos simultáneos max de Hola por la limitación en la cuenta. valor de prioridad de Hello determina la secuencia de Hola de trabajos en cola - número Hola Hola menor, prioridad Hola Hola.
    * En ejecución: trabajo Hola realmente se está ejecutando en su cuenta de análisis de Data Lake.
    * Finalizando: trabajo Hola completa (por ejemplo, dar por finalizados archivo hello).
      
      trabajo de Hello puede producir un error en cada fase. Por ejemplo, errores de compilación en la fase de preparación de hello, errores de tiempo de espera en la fase de puesta en cola de Hola y errores de ejecución en la fase de ejecución de hello, etcetera.
  * Información básica
    
      Muestra información de trabajo básico de Hello en parte inferior de hello del panel de resumen de trabajos de Hola.
    
      ![Estado de las fases del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Job Result: (Resultado del trabajo) correcto o con error. trabajo de Hello puede producir errores en cada fase.
    * Duración total: tiempo de reloj (duración) entre la hora de envío y la hora de finalización.
    * Tiempo de ejecución total: suma de hello cada vértice de tiempo de ejecución, puede considerar como Hola de tiempo que el trabajo de Hola se ejecuta en solo un vértice. Consulte tooTotal vértices toofind obtener más información acerca de vértices.
    * Hora de enviar/inicio/fin: Hola horario cuando Hola servicio de análisis de Data Lake recibe Hola de trabajo inicia/envío toorun trabajo/finaliza trabajo Hola correctamente o no.
    * Puesta en cola de compilación/ejecución: Dedicado a la hora de reloj durante la fase de puesta en cola/preparación/ejecución Hola.
    * Cuenta: cuenta de análisis de Data Lake Hola usada para ejecutar el trabajo de Hola.
    * Autor: Hola quien envió el trabajo de hello, puede ser una cuenta del sistema o cuenta de una persona real.
    * Prioridad: prioridad de Hola del trabajo de Hola. Hola Hola número inferior, prioridad Hola Hola. Solo afecta a la secuencia de Hola de trabajos de hello en cola de Hola. Al establecer una prioridad mayor no se adelantan trabajos en ejecución.
    * Paralelismo: Hola había solicitado el número máximo de simultáneas Azure Lake Analytics unidades de datos (ADLAUs), también conocido como vértices. Actualmente, un vértice es igual tooone VM con dos núcleo virtual y seis GB de RAM, aunque esto podría actualizarse en el futuro las actualizaciones de análisis de Data Lake.
    * Bytes restante: Bytes que necesitan toobe procesa hasta que se complete el trabajo de Hola.
    * Bytes leídos/escritos: Bytes que han sido leídos/escritos desde el trabajo de hello empezado a ejecutarse.
    * Total de vértices: trabajo Hola se divide en muchos elementos de trabajo, cada parte del trabajo se llama a un vértice. Este valor describe formada por trabajo de Hola de cuántos elementos de trabajo. Un vértice puede considerarse como una unidad de proceso básico, también denominada unidad de Azure Data Lake Analytics (ADLAU), y los vértices se pueden ejecutar en paralelismo. 
    * Completado/ejecución/error: Hola recuento de vértices completado / / no se pudo ejecutar. Vértices pueden producir un error debido a errores de sistema y código de usuario de tooboth, pero no de reintentos de sistema de hello vértices automáticamente varias veces. Si todavía se produce el error de vértices Hola después de reintentarlo, se producirá un error de trabajo entero Hola.
* Gráfico del trabajo
  
    Un script U-SQL representa lógica de Hola de transformación de datos de toooutput de datos de entrada. script de Hola se compila y optimiza el plan de ejecución física tooa en fase de preparación de Hola. Gráfico de trabajo es el plan de ejecución física de hello tooshow.  Hola siguiente diagrama ilustra el proceso de hello:
  
    ![Estado de las fases del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Un trabajo se divide en muchos elementos de trabajo. Cada elemento de trabajo se denomina vértice. vértices Hola se agrupan como Super vértice (también conocida como fase) y visualizar en forma de gráfico de trabajo. paneles de fase verde Hello en el gráfico de trabajo de hello mostrar fases Hola.
  
    Cada vértice en una fase realiza Hola mismo tipo de trabajar con diferentes partes del programa Hola mismos datos. Por ejemplo, si tiene un archivo con un TB de datos y hay cientos de vértices leyendo en ellos, cada uno lee un fragmento. Los vértices se agrupan en hello misma fase y realizar el mismo trabajan en diferentes partes del mismo archivo de entrada.
  
  * <a name="state-information"></a>Información de fase
    
      En una fase determinada, se muestran algunos números en Letrero Hola.
    
      ![Fase del gráfico del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Extraer: nombre de Hola de una fase, denominada mediante un método de operación hello y número.
    * 84 vértices: Hola recuento total de vértices en esta fase. ilustración de Hello indica cuántos elementos de trabajo se divide en esta fase.
    * s/vértices 12,90: Hola vértices promedio tiempo de ejecución para esta fase. La cifra se calcula mediante SUM (tiempo de ejecución de cada vértice)/(recuento total de vértices). Lo que significa que si puede asignar todos los vértices de hello ejecutados en paralelismo, fase todo Hola se completa en 12,90 s. También significa que si todos Hola trabajo en esta fase se realiza en serie, el costo de hello sería #vertices * promedio de tiempo.
    * 850,895 rows written: (850 895 filas escritas) número total de filas escritas en esta fase.
    * Lectura/escritura: cantidad de datos leídos/escritos en esta fase, en bytes.
    * Colores: Se usan los colores en el estado de hello fase tooindicate vértices diferentes.
      
      * Color verde indica vértices hello es correcto.
      * Naranja indica vértices Hola se vuelve a intentar. vértices Hola vuelve a intentar error estaba pero se vuelve a intentar automáticamente y correctamente por sistema de Hola y Hola general fase se completa correctamente. Si vértices Hola reintentaron pero todavía no se pudo, color de hello activa hello y rojo todo error en el trabajo.
      * Color rojo indica un error, lo que significa que un vértice determinado tenía se vuelve a intentar varias veces por el sistema de Hola pero todavía no se pudo. Este mismo escenario provoca Hola trabajo entero toofail.
      * El color azul indica que un vértice determinado está en ejecución.
      * Blanco indica Hola vértices está esperando. vértices Hola pueden toobe espera programado una vez que un ADLAU estará disponible, o puede estar esperando para la entrada ya que sus datos de entrada no sea Listo.
      
      Puede encontrar más detalles para la fase de hello desplazando el cursor del mouse en un estado:
      
      ![Detalles de la fase del gráfico del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Vértices: Describe los detalles de vértices hello, por ejemplo, ¿cuántos vértices en total, el número de vértices se hayan completado, son que no se pudo o todavía/en espera de ejecución, etcetera.
  * Data read cross/intra pod: (Lectura de datos entre pods/dentro del pod) los archivos y datos se almacenan en varios pods en un sistema de archivos distribuido. valor de Hello aquí describe la cantidad de datos se ha leído de hello misma pod o cross pod.
  * Total de tiempo de ejecución: suma de hello cada vértice tiempo de ejecución en la fase de hello, puede considerarlo como tiempo de Hola que se tardaría si todo el trabajo en la fase de Hola se ejecuta en solo un vértice.
  * Datos y escriben y leen filas: indica cuánto datos filas han sido leídos/escritos o necesitan toobe leer.
  * Vertex read failures: (Errores de lectura de vértices) describe cuántos vértices produjeron errores al leer datos.
  * Descartan los vértices duplicados: si un vértice se ejecuta demasiado despacio, sistema de hello puede programar varios vértices toorun Hola misma parte del trabajo. Se descartarán los vértices reductant cuando uno de los vértices de hello completado correctamente. Vértices duplicados descartan el número de registros Hola de vértices que se descartan como duplicados en la fase de Hola.
  * Revocaciones de vértices: vértices Hola se es correcta, pero obtener vuelva a ejecutar más adelante debido a motivos de toosome. Por ejemplo, si los vértices pierden datos intermedios de entrada, pedirá Hola vértices ascendente toorerun.
  * Ejecuciones de programación de vértices: tiempo total de Hola que se hayan programado vértices Hola.
  * Datos de vértice de Media/Min/Max leídos: Hola mínimo/Media/máximo de cada vértice leer los datos.
  * Duración: Hola tiempo de reloj tarda una fase, necesita tooload perfil toosee este valor.
  * Reproducción del trabajo
    
      Análisis de Data Lake ejecuta trabajos y archivos Hola vértices ejecuta información de trabajos de hello, como cuando se inician los vértices de hello, detenido, error y cómo se reintentan, etcetera. Toda información de Hola se registra en el almacén de consultas de Hola y almacenada en su perfil de trabajo automáticamente. Puede descargar Hola perfil de trabajo a través de "Perfil de carga" en la vista de trabajo, y puede ver Hola reproducción de trabajo después de descargar Hola perfil de trabajo.
    
      Reproducción de trabajo es una visualización de representación perfecta de lo que sucedió en clúster de Hola. Permite ver el progreso de la ejecución del trabajo y detectar visualmente los cuellos de botella y las anomalías de rendimiento en muy poco tiempo (normalmente, menos de 30 segundos).
  * Presentación del mapa térmico del trabajo 
    
      Mapa térmico de trabajo se pueden seleccionar a través de la lista desplegable de presentación de hello en el gráfico de trabajo. 
    
      ![Presentación del mapa de montón de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Muestra el mapa de calor de hello E/S, el tiempo y el rendimiento de un trabajo, a través del cual puede buscar donde trabajo Hola emplea la mayor parte del tiempo de hello, o si el trabajo es un trabajo de límites de E/S y así sucesivamente.
    
      ![Ejemplo del mapa de montón de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Curso: Hola progreso de la ejecución de trabajo, vea la información en [fase información](#stage-information).
    * Datos leídos/escritos: mapa térmico de Hola de total de los datos leídos/escritos en cada fase.
    * Tiempo de proceso: mapa térmico de Hola de suma (cada hora de ejecución de vértices), puede considerar esto como la larga tardaría si se ejecuta todo el trabajo en la fase de hello con solo 1 vértices.
    * Tiempo medio de ejecución por nodo: mapa térmico de Hola de suma (cada hora de ejecución de vértices) / (número de vértices). Lo que significa que si puede asignar todos los vértices de hello ejecutados en paralelismo, fase todo Hola se hará en este período de tiempo.
    * Rendimiento de entrada/salida: mapa térmico de Hola de rendimiento de entrada/salida de cada fase, puede confirmar si el trabajo es un trabajo dependiente de E/S a través de este.
* Operaciones de metadatos
  
    Puede realizar algunas operaciones de metadatos en el script U-SQL, como crear una base de datos, eliminar una tabla, etc. Estas operaciones se muestran en la operación de metadatos después de la compilación. Aquí puede encontrar aserciones, crear entidades y eliminar entidades.
  
    ![Operaciones de metadatos de vista de trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Historial de los estados
  
    Hola historial de estado también se visualiza en el resumen de trabajo, pero puede obtener más detalles a continuación. Puede encontrar Hola detallada información como cuando se prepara el trabajo de hello, en cola, empezó a ejecutarse, ha finalizado. También puede encontrar cuántas veces se ha compilado el trabajo de hello (Hola CcsAttempts: 1), cuando es clúster de hello trabajo toohello enviado realmente (Hola detalle: enviar trabajo toocluster), etcetera.
  
    ![Historial de los estados de vista de trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnóstico
  
    herramienta de Hello diagnostica automáticamente la ejecución del trabajo. Recibirá alertas cuando haya errores o problemas de rendimiento en sus trabajos. Tenga en cuenta que debe toodownload perfil tooget toda la información aquí. 
  
    ![Diagnóstico de vista de trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Advertencias: aquí aparece una alerta con una advertencia del compilador. Puede hacer clic en "x problemas" vínculo toohave más detalles cuando aparezca la alerta de Hola.
  * Vertex run too long: (Ejecución de vértice demasiado larga) si algún vértice agota el tiempo (digamos, 5 horas), aquí se encontrarán los problemas.
  * Uso de recursos: si ha asignado más paralelismo del necesario o insuficiente, aquí se encontrarán problemas. También puede haga clic en toosee de uso de recursos más detalles y realizar toofind de escenarios condicionales una mejor asignación de recursos (para obtener más información, consulte esta guía).
  * Comprobación de memoria: si algún vértice utiliza más de 5 GB de memoria, aquí se encontrarán problemas. Puede que el sistema termine la ejecución del trabajo si este usa más memoria que la limitación del sistema.

## <a name="job-detail"></a>Detalles del trabajo
Detalles del trabajo muestra Hola información detallada del trabajo de hello, incluida la secuencia de comandos, los recursos y vista de la ejecución de vértices.

![Detalles del trabajo de Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Hola script U-SQL de trabajo de Hola se almacena en el almacén de consultas Hola. Puede ver el script U-SQL original de Hola y volver a enviarlo si es necesario.
* Recursos
  
    Puede encontrar los resultados de compilación de trabajo Hola almacenados en el almacén de consultas de Hola a través de recursos. Por ejemplo, puede buscar "algebra.xml", que es usado tooshow hello trabajo gráfico, ensamblados de hello registrado, etc. aquí.
* Vista de ejecución de vértices
  
    Muestra detalles de la ejecución de vértices. Hola perfil de trabajo archiva cada registro de ejecución de vértices, como el número total de los datos leídos/escritos, en tiempo de ejecución, estado, etcetera. Mediante esta vista, puede obtener más detalles sobre cómo se ejecutó un trabajo. Para obtener más información, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Pasos siguientes
* información de diagnóstico de toolog, consulte [acceso a registros de diagnóstico para el análisis de Azure Data Lake](data-lake-analytics-diagnostic-logs.md)
* toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* vista de ejecución de vértices toouse, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

