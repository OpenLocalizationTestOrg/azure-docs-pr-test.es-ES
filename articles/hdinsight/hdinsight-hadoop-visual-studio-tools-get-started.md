---
title: aaaConnect tooAzure HDInsight con Data Lake Tools para Visual Studio | Documentos de Microsoft
description: "Obtenga información acerca de cómo los clústeres de tooinstall y uso Data Lake Tools para Visual Studio tooconnect tooHadoop en HDInsight de Azure y ejecución de consultas de Hive."
keywords: herramientas hadoop, consulta hive, visual studio, visual studio hadoop
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Conectar tooAzure HDInsight y ejecutar consultas de Hive con Data Lake Tools para Visual Studio

Obtenga información acerca de cómo los clústeres de toouse Data Lake Tools para Visual Studio tooconnect tooHadoop en [HDInsight de Azure](hdinsight-hadoop-introduction.md) y enviar consultas Hive. Para obtener más información sobre el uso de HDInsight, vea [Introducción tooHDInsight](hdinsight-hadoop-introduction.md) y [empezar a trabajar con HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Para obtener más información sobre el clúster de Storm tooa conexión, consulte [C# desarrollar topologías para Apache Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Data Lake Tools para Visual Studio puede ser usado tooaccess análisis de Data Lake y HDInsight.  Para obtener información de hello acerca de Data Lake Tools, vea [Tutorial: desarrollar scripts de SQL U con Data Lake Tools para Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Requisitos previos**

toocomplete Hola Data Lake de este tutorial y el uso de las herramientas en Visual Studio, necesitará Hola siguiente:

* Un clúster de HDInsight de Azure: toocreate un, consulte [Introducción al uso de HDInsight basados en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Una estación de trabajo con hello siguiente software:
  
  * Windows 10, Windows 8.1, Windows 8 o Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Actualmente, Hola Data Lake Tools para Visual Studio sólo se incluyen con la versión en inglés Hola.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Instalación de Data Lake Tools para Visual Studio

Data Lake Tools está instalado de forma predeterminada para Visual Studio de 2017. En las versiones anteriores, puede instalarlo mediante hello [instalador de plataforma Web](https://www.microsoft.com/web/downloads/). Debe elegir Hola uno que coincida con su versión de Visual Studio. Si no tiene instalado Visual Studio, puede instalar Hola Comunidad de Visual Studio y SDK de Azure más recientes mediante hello [instalador de plataforma Web](https://www.microsoft.com/web/downloads/):

![Lago herramientas de datos de instalador de plataforma Web de Visual Studio. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Tooinstall de instalador de plataforma Web de uso Data Lake Tools para Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Conectar tooAzure suscripciones
Data Lake Tools para Visual Studio le permite clústeres de HDInsight de tooconnect tooyour, realizar algunas operaciones básicas de administración y ejecutar consultas de Hive.

> [!NOTE]
> Para obtener información sobre el clúster de Hadoop genérico de tooa de conexión, consulte [escribir y enviar consultas de Hive con Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour suscripción de Azure**

1. Abra Visual Studio.
2. De hello **vista** menú, haga clic en **Explorador de servidores** ventana de explorador de servidores de hello tooopen.
3. Expanda **Azure** y, después, haga lo mismo con **HDInsight**.
   
   > [!NOTE]
   > Hola aviso **lista de tareas de HDInsight** ventana debe estar abierta. Si no lo ve, haga clic en **otras ventanas** de hello **vista** menú y, a continuación, haga clic en **ventana Lista de tareas de HDInsight**.  
   > 
   > 
4. Escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**. Esto solo es necesario si nunca se ha conectado toohello suscripción de Azure desde Visual Studio en esta estación de trabajo.
5. En el Explorador de servidores, se mostrará una lista de los clústeres de HDInsight existentes. Si no dispone de los clústeres, puede crear uno mediante Hola portal de Azure, Azure PowerShell u Hola SDK de HDInsight. Para más información, consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Explorador de servidores de Herramientas de Data Lake para Visual Studio: lista de clústeres](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Explorador de servidores de Herramientas de Data Lake para Visual Studio")
6. Expanda un clúster de HDInsight. Verá las **bases de datos de Hive**, una cuenta de almacenamiento predeterminada, las cuentas de almacenamiento vinculadas y el **registro del servicio Hadoop**. Expandir las entidades de Hola.

Una vez haya conectado tooyour suscripción de Azure, estará siguiente de hello toodo capaz de:

**tooconnect toohello portal de Azure desde Visual Studio**

* En el Explorador de servidores, expanda **Azure** > **HDInsight**, haga clic con el botón derecho en un clúster de HDInsight y, después, haga clic en **Administrar el clúster en Azure Portal**.

**tooask preguntas y proporcionar comentarios de Visual Studio**

* De hello **herramientas** menú, haga clic en **HDInsight**y, a continuación, haga clic en **foro de MSDN** tooask preguntas, o haga clic en **enviar comentarios**.

## <a name="navigate-hello-linked-resources"></a>Navegar por los recursos vinculado de Hola
Desde el Explorador de servidores, puede ver la cuenta de almacenamiento predeterminada de Hola y las cuentas de almacenamiento vinculadas. Si expande la cuenta de almacenamiento predeterminada de hello, puede ver los contenedores de Hola Hola cuenta de almacenamiento. cuenta de almacenamiento predeterminada de Hola y el contenedor predeterminado de hello están marcados. También puede haga clic en cualquier elemento de contenido de hello contenedores tooview Hola.

![Explorador de servidores de Herramientas de Data Lake para Visual Studio: lista de recursos vinculados](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "lista de recursos vinculados")

Después de abrir un contenedor, puede usar Hola después tooupload botones, eliminación y descarga de blobs:

![Explorador de servidores de Herramientas de Data Lake para Visual Studio: operaciones de blob](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "cargar, eliminar y descargar blobs")

## <a name="run-a-hive-query"></a>Ejecución de una consulta de Hive
[Apache Hive](http://hive.apache.org) es una infraestructura de almacenamiento de datos basada en Hadoop para proporcionar resúmenes de datos, consultas y análisis. Data Lake Tools para Visual Studio admite la ejecución de consultas de Hive desde Visual Studio. Para más información sobre Hive, consulte [Uso de Hive con HDInsight](hdinsight-use-hive.md).

Es el script de Hive tootest mucho tiempo en un clúster de HDInsight. Puede tardar varios minutos o más tiempo. Es capaz de validar el script de Hive localmente sin clúster activo de conexión tooa Data Lake Tools para Visual Studio.

Data Lake Tools para Visual Studio también permite a los usuarios toosee lo que está dentro de trabajo de Hive Hola al recopilar y registros YARN Hola de determinados trabajos de Hive así como la exposición.

### <a name="view-hello-hivesampletable"></a>Hola de vista **hivesampletable**
Todos los clústeres de HDInsight incluyen una tabla Hive de ejemplo denominada *hivesampletable*. Usaremos esta tooshow tabla cómo tablas de Hive toolist, vea los esquemas de tabla de Hola y mostrar filas Hola de Hola Hive tabla.

**tablas de Hive toolist y vista de esquema de la tabla de Hive**

1. De **Explorador de servidores**, expanda **Azure** > **HDInsight** > clúster Hola de su elección > **bases de datos de Hive**  >  **Predeterminado** > **hivesampletable** toosee esquema de la tabla de Hola.
2. Haga clic en **hivesampletable**y, a continuación, haga clic en **vista Top 100 Rows** filas de hello toolist. Es hello toorunning equivalente después de consulta de Hive mediante el controlador ODBC de Hive:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Puede personalizar el recuento de filas de Hola.
   
   ![Herramientas de Data Lake para Visual Studio en HDInsight: consulta del esquema de Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Resultados de la consulta de Hive")

### <a name="create-hive-tables"></a>Crear tablas de Hive
Puede usar Hola GUI toocreate una tabla de Hive o utilizar consultas de Hive. Para obtener información acerca del uso de consultas de Hive, consulte [Ejecución de consultas de Hive](#run.queries).

**toocreate una tabla de Hive**

1. En el **Explorador de servidores**, expanda **Azure** > **Clústeres de HDInsight** un clúster de HDInsight > **Bases de datos de Hive**, haga clic con el botón derecho en **Predeterminada** y, finalmente, haga clic en **Crear tabla**.
2. Configurar la tabla de Hola.
3. Haga clic en **Create Table** toosubmit Hola trabajo toocreate Hola nueva tabla de Hive.
   
    ![Herramientas de Data Lake para Visual Studio en HDInsight: creación de tablas de Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Creación de tablas de Hive")

### <a name="run.queries"></a>Validación y ejecución de consultas de Hive
Hay dos maneras toocreate y ejecución de consultas de Hive:

* Crear consultas ad hoc
* Crear una aplicación de Hive

**toocreate, validar y ejecutar consultas ad hoc**

1. En el **Explorador de servidores**, expanda **Azure** y luego expanda **Clústeres de HDInsight**.
2. Menú contextual clúster de Hola donde desea toorun Hola consulta y, a continuación, haga clic en **escribir una consulta de Hive**.
3. Escriba consultas de Hive Hola. Editor de subárboles de aviso hello es compatible con IntelliSense. Data Lake Tools para Visual Studio es compatible con carga Hola metadatos remoto mientras se edita el script de Hive. Por ejemplo, al escribir "SELECT * FROM", Hola IntelliSense enumera todos Hola nombres de tabla sugeridos. Cuando se especifica un nombre de tabla, se enumeran los nombres de columna de Hola por hello IntelliSense. herramientas de Hello admiten casi todas las instrucciones DML Hive, subconsultas y Hola UDF integradas.
   
    ![Herramientas de Data Lake para Visual Studio en HDInsight: IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "IntelliSense en U-SQL")
   
    ![Herramientas de Data Lake para Visual Studio en HDInsight: IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "IntelliSense en U-SQL")
   
   > [!NOTE]
   > Se sugerirá solo Hola metadatos de clústeres de Hola que está seleccionado en la barra de herramientas de HDInsight.
   > 
   > 
4. (Opcional): haga clic en **validar Script** errores de sintaxis de script de Hola toocheck.
   
    ![Herramientas de Data Lake para Visual Studio: validación local](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Validación de scripts")
5. Haga clic en **Enviar** o en **Enviar (avanzado)**. Con hello enviar opción avanzada, configurará **nombre del trabajo**, **argumentos**, **configuraciones adicionales**, y **estado directorio**para script de Hola:
   
    ![Consulta de Hive para Hadoop en HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Envío de consultas")
   
    Después de enviar el trabajo de hello, verá un **resumen del trabajo de Hive** ventana.
   
    ![Resumen de una consulta de Hive para Hadoop en HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Resumen de un trabajo de Hive")
6. Hola de uso **actualizar** botón estado de hello tooupdate hasta que cambie de estado de trabajo de hello demasiado**completado**.
7. Haga clic en vínculos de hello en hello inferior toosee Hola a continuación: **trabajo consulta**, **salida del trabajo**, **registro de trabajo**, o **registro Yarn**.

**toocreate y ejecutar una solución de Hive**

1. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
2. Seleccione **HDInsight** en hello panel izquierdo, seleccione **aplicación Hive** en el panel central de hello, especifique propiedades de hello y, a continuación, haga clic en **Aceptar**.
   
    ![Herramientas de Data Lake para Visual Studio en HDInsight: nuevo proyecto de Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Creación de aplicaciones de Hive desde Visual Studio")
3. De **el Explorador de soluciones**, haga doble clic en **Script.hql** tooopen lo.
4. script de Hive de hello toovalidate, puede hacer clic en hello **validar Script** botón, o haga clic en el script de hello en el editor de Hive de hello y, a continuación, haga clic en **validar Script** desde el menú contextual de Hola.

### <a name="view-hive-jobs"></a>Ver trabajos de Hive
Puede ver consultas de trabajo, salidas de trabajo, registros de trabajo y registros Yarn para trabajos de Hive. Para obtener más información, vea Hola captura de pantalla anterior.

versión más reciente de Hola de herramientas de hello permite toosee lo que está dentro de los trabajos de Hive al recopilar y así como la exposición YARN registros. El registro Yarn puede ayudarle a investigar problemas de rendimiento. Para más información acerca de cómo HDInsight recopila registros YARN, consulte [Acceso a registros de aplicación de HDInsight mediante programación](hdinsight-hadoop-access-yarn-app-logs.md).

**trabajos de Hive tooview**

1. En el **Explorador de servidores**, expanda **Azure** y, después, expanda **HDInsight**.
2. Haga clic con el botón derecho en un clúster de HDInsight y luego haga clic en **Ver trabajos**. Verá una lista de hello Hive trabajos que se ejecutaron en clúster de Hola.
3. Haga clic en un trabajo en tooselect de lista de trabajo de hello y, a continuación, use hello **resumen del trabajo de Hive** ventana tooopen **trabajo consulta**, **salida del trabajo**, **registro de trabajo**, o **registro Yarn**.
   
    ![Herramientas de Data Lake para Visual Studio en HDInsight: visualización de trabajos de Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Visualización de trabajos de Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Ejecución de Hive más rápida mediante HiveServer2
> [!NOTE]
> Este tutorial solo funciona en la versión 3.2 y posteriores del clúster de HDInsight.
> 
> 

Hola Data Lake Tools usa trabajos de Hive toosubmit a través de [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (también conocido como Templeton). Se tardaron un tooreturn mucho tiempo detalles del trabajo y la información de error.
En orden toosolve este problema de rendimiento, Hola ejecuta Data Lake Tools Hive trabajos directamente en el clúster de hello mediante HiveServer2, por lo que omite RDP/SSH.
En el rendimiento de toobetter de suma, los usuarios también pueden ver Hive en los gráficos de Tez y Hola detalles de la tarea.

En el caso del clúster de HDInsight versión 3.2 o posterior, puede ver el botón **Ejecutar mediante HiveServer2**:

![Herramientas de Data Lake para Visual Studio: ejecución con hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Ejecución de consultas de Hive con HiveServer2")

Y puede ver registros de hello modos de transmisión en tiempo real y ver los gráficos de trabajo de hello si se ejecuta la consulta de Hive hello en Tez.

![Herramientas de Data Lake para Visual Studio en HDInsight: ejecución de Hive de ruta de acceso rápida](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Visualización de gráficos de trabajo")

**Diferencia entre la ejecución de consultas a través de HiveServer2 y el envío de consultas a través de WebHCat**

Aunque la ejecución de consultas a través de HiveServer2 ofrece muchas ventajas de rendimiento, tiene varias limitaciones. Algunas de las limitaciones de hello no son adecuados para el uso de producción. Hello tabla siguiente muestran las diferencias de hello:

|  | Ejecución a través de HiveServer2 | Envío a través de WebHCat |
| --- | --- | --- |
| Ejecución de consultas |Elimina la sobrecarga de hello en WebHCat (que inicia un Job de MapReduce con el nombre "TempletonControllerJob"). |Siempre que una consulta se ejecute a través de WebHCat, esta iniciará un trabajo MapReduce que introduce latencia adicional. |
| Registros inversos |Casi en tiempo real. |registros de ejecución del trabajo de Hello solo están disponibles cuando el trabajo de hello ha finalizado. |
| Visualización del historial de trabajos |Si una consulta se ejecuta a través de HiveServer2, no se conserva su historial de trabajos (registro de trabajo, salida de trabajo). aplicación Hello puede verse en la interfaz de usuario de YARN con información limitada. |Si una consulta se ejecuta a través de WebHCat, su historial de trabajos (registro de trabajo, salida de trabajo) se conserva y se puede ver con Visual Studio o HDInsight SDK o PowerShell. |
| Cierre de ventana |Ejecutar a través de HiveServer2 es una manera "sincrónica", por lo que debe mantener Hola ventanas abiertas; Si se cierran windows hello, a continuación, puede cancelar ejecución de la consulta de Hola. |Enviar a través de WebHCat es una manera "asincrónica" para que pueda enviar la consulta de Hola a través de WebHCat y cierre Visual Studio. Puede regresar y ver resultados de Hola en cualquier momento. |

### <a name="tez-hive-job-performance-graph"></a>Gráfico de rendimiento de trabajos de Hive de Tez
soporte técnico de Data Lake Tools Hola que muestra gráficos de rendimiento para hello trabajos de Hive se ejecutó el motor de ejecución de hello Tez. Para más información sobre cómo habilitar Tez, consulte [Uso de Hive en HDInsight](hdinsight-use-hive.md). Después de enviar un subárbol muestra trabajo en Visual Studio, Visual Studio Hola gráfico cuando se completa el trabajo de Hola.  Tendrá que hello tooclick **actualizar** botón estado de trabajo más reciente de tooget Hola.

> [!NOTE]
> Esta característica solo está disponible para las versiones del Clúster de HDInsight posteriores a la 3.2.4.593 y solo puede funcionar con trabajos completados (si ha enviado el trabajo a través de WebHCat; este gráfico se mostrará al ejecutar una consulta a través de HiveServer2). Esto funciona en clústeres de Windows y Linux.
> 
> 

![Gráfico de rendimiento de Tez de Hive para Hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Estado del trabajo")

toohelp comprender el subárbol de consulta mejor, herramientas de hello agregan vista de operador de Hive de hello en esta versión. Basta con toodouble, haga clic en los vértices de Hola Hola del gráfico del trabajo y puede ver todos los operadores de hello dentro de hello vértices. También puede situar en un operador determinado tooview más detalles acerca de este operador.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Vista de ejecución de tareas de Hive en trabajos Tez
Hola vista de ejecución de la tarea de Hive en Tez trabajos se puede utilizar tooget estructurado y visualizar información de los trabajos de Hive y obtener más detalles del trabajo. Cuando hay problemas de rendimiento, puede usar más detalles de hello vista tooget. Por ejemplo, cómo funciona cada tarea así como Hola información detallada sobre cada tarea (lectura/escritura de datos, tiempo de programación/inicio/fin, etc.), por lo que se puede ajustar las configuraciones de trabajo o la arquitectura de sistema en función de hello visualizado información.

![Herramientas de Data Lake para Visual Studio: vista de ejecución](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Vista de ejecución de tareas")

## <a name="run-pig-scripts"></a>Ejecución de scripts de Pig
Data Lake Tools para Visual Studio permite crear y enviar los clústeres de tooHDInsight de scripts de Pig. Los usuarios pueden crear un proyecto de Pig desde plantilla y, a continuación, enviar clústeres de tooHDInsight de script de Hola.

## <a name="feedbacks--known-issues"></a>Comentarios y problemas conocidos
* Actualmente, los resultados de HiveServer2 se muestran en forma de texto puro, un formato que no es el ideal. Estamos trabajando para solucionar ese problema.
* Si los resultados de Hola se inician con valores NULL, actualmente resultados hello no se muestran. Hemos solucionado este problema y si se bloquean en este problema, cree libre toodrop nos un correo electrónico o póngase en contacto con equipo de soporte técnico.
* script de Hola HQL creada por Visual Studio se codifica según la configuración de área local del usuario. Puede no ejecutarse correctamente si el usuario carga Hola script toocluster como binario.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo tooconnect tooHDInsight clústeres desde Visual Studio, con hello Data Lake (HDInsight) el paquete de herramientas y cómo toorun una consulta de Hive. Para más información, consulte:

* [Uso de Hive para Hadoop en HDInsight](hdinsight-use-hive.md)
* [Introducción al uso de Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Envío de trabajos de Hadoop en HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Análisis de datos de Twitter con Hadoop en HDInsight](hdinsight-analyze-twitter-data.md)

