---
title: 'aaaUse Tez UI con HDInsight basados en Windows: Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo trabajos toouse hello Tez UI toodebug Tez en HDInsight HDInsight basados en Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Usar hello Tez UI toodebug Tez trabajos de HDInsight basados en Windows
Hola Tez UI es una página web que pueden ser utilizados trabajos toounderstand y depuración que utilizan Tez como motor de ejecución de hello en clústeres de HDInsight basados en Windows. Hola Tez UI permite trabajo de hello toovisualize como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos
* Un clúster de HDInsight basado en Windows Para obtener información sobre cómo crear un clúster, consulte [Introducción al uso de HDInsight basado en Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Hola Tez UI solo está disponible en los clústeres de HDInsight basados en Windows creados después del 8 de febrero de 2016.
  >
  >
* Un cliente de escritorio remoto basado en Windows.

## <a name="understanding-tez"></a>Descripción de Tez
Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce. Para los clústeres de HDInsight basados en Windows, es un motor opcional que puede habilitar para Hive mediante Hola siguiente comando como parte de la consulta de Hive:

    set hive.execution.engine=tez;

Una vez trabajo tooTez enviado, crea un dirigen acíclico gráfico (DAG) que describe el orden de Hola de ejecución de acciones de hello requerido trabajo Hola. Acciones individuales se denominan vértices y ejecutar una parte del programa Hola trabajo completo. ejecución real de Hola de trabajo de hello descrita por un vértice se denomina una tarea y se puede distribuir en varios nodos de clúster de Hola.

### <a name="understanding-hello-tez-ui"></a>Hola descripción Tez UI
Hola Tez UI es que una página web proporciona información sobre los procesos que se ejecutan o tienen previamente se ejecutó con una Tez. Le permite tooview Hola DAG generado por Tez, cómo se distribuyen a través de clústeres, los contadores, como la memoria utilizada por la información de error, las tareas y vértices. Puede ofrecer información útil en hello los escenarios siguientes:

* Supervisión de los procesos de larga ejecución, ver progreso de asignación de Hola y reduzcan las tareas.
* Analizar datos históricos para procesos correctos o con error toolearn cómo se puede mejorar el procesamiento o por qué se produjo un error.

## <a name="generate-a-dag"></a>Generar un DAG
Hola Tez UI solo contendrá datos si un trabajo que utiliza Hola Tez motor se está ejecutando actualmente o se ha quedado en hello anterior. Las consultas de Hive sencillas normalmente se pueden resolver sin usar Tez, pero las consultas más complejas con filtrado, agrupación, ordenación, uniones, etc. suelen requerir Tez.

Usar hello siguiendo los pasos toorun una consulta de Hive que va a ejecutar mediante Tez.

1. En un explorador web, vaya toohttps://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight.
2. En menú de hello al principio de Hola de página de hello, seleccione hello **Editor de Hive**. Se mostrará una página con la siguiente consulta de ejemplo de Hola.

        Select * from hivesampletable

    Borrar la consulta de ejemplo de Hola y reemplazarlo por siguiente Hola.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Seleccione hello **enviar** botón. Hola **sesión de trabajo** sección final Hola de página Hola mostrará el estado de Hola de consulta de Hola. Una vez Hola cambios de estado demasiado**completado**, seleccione hello **ver detalles** vincular tooview Hola resultados. Hola **salida del trabajo** debe ser similar siguiente toohello:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Usar hello Tez UI
> [!NOTE]
> Hola Tez UI solo está disponible en el escritorio de Hola Hola principal de nodos de clúster, por lo que debe usar nodos principales del escritorio remoto tooconnect toohello.
>
>

1. De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight. Desde la parte superior de la hoja de HDInsight de Hola Hola seleccione hello **escritorio remoto** icono. Esto mostrará la hoja de escritorio remoto de Hola

    ![Icono de Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. En la hoja de escritorio remoto de hello, seleccione **conectar** nodo principal del clúster de toohello tooconnect. Cuando se le pida, use Hola clúster usuario nombre y la contraseña tooauthenticate Hola conexión a Escritorio remoto.

    ![Icono de conexión a Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Si no ha habilitado la conectividad de escritorio remoto, proporcione un nombre de usuario, una contraseña y una fecha de expiración, seleccione **habilitar** tooenable escritorio remoto. Una vez que se ha habilitado, utilice hello tooconnect de pasos anteriores.
   >
   >
3. Una vez conectado, abra Internet Explorer en el escritorio remoto hello, icono de engranaje seleccione hello en superior Hola derecha del explorador de hello y, a continuación, seleccione **ver la configuración de compatibilidad**.
4. Desde la parte inferior de Hola de **ver la configuración de compatibilidad**, desactive casilla de verificación de Hola para **mostrar sitios de intranet en la vista de compatibilidad** y **listas de compatibilidad de usar Microsoft**, y, a continuación, seleccione **cerrar**.
5. En Internet Explorer, vaya toohttp://headnodehost:8188/tezui / #/. Esto mostrará hello Tez UI

    ![Interfaz de usuario de Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Cuando se cargue hello Tez UI, verá una lista de grupos dag que se están ejecutando actualmente, o bien haber ejecutado en clúster de Hola. vista predeterminada de Hello incluye Hola Dag Name, Id., remitente, estado, hora de inicio, hora de finalización, duración, Id. de aplicación y cola. Mediante el icono de engranaje de hello en hello derecha de la página de hello, se pueden agregar más columnas.

    Si tiene sólo una entrada, será para consulta de Hola que se ejecutó en la sección anterior de Hola. Si tiene varias entradas, puede buscar mediante la especificación de criterios de búsqueda en los campos de hello anteriormente Hola dag y luego aciertos **ENTRAR**.
6. Seleccione hello **Dag Name** para entrada de DAG de hello más reciente. Se mostrará información acerca de hello DAG, así como toodownload de opción de hello un archivo zip de archivos JSON que contienen información sobre Hola DAG.

    ![Detalles del DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Por encima de hello **DAG detalles** son varios vínculos que pueden ser utilizados toodisplay saber Hola DAG.

   * **Contadores del DAG** muestra información de los contadores de este DAG.
   * **Vista gráfica** muestra una representación gráfica de este DAG.
   * **Todos los vértices** muestra una lista de vértices de hello en este DAG.
   * **Todas las tareas** muestra una lista de tareas de Hola para todos los vértices en este DAG.
   * **Todos los TaskAttempts** muestra información acerca de hello intenta toorun tareas para este DAG.

     > [!NOTE]
     > Si se desplaza la presentación de la columna de Hola de vértices, tareas y TaskAttempts, tenga en cuenta que hay vínculos tooview **contadores** y **ver o descargar los registros de** para cada fila.
     >
     >

     Si se produjo un error en el trabajo de hello, Hola DAG detalles mostrará un estado de error, junto con vínculos tooinformation acerca de la tarea que tuvo el saludo. Información de diagnóstico se mostrará debajo de los detalles de hello DAG.
8. Seleccione **Vista gráfica**. Esto muestra una representación gráfica de hello DAG. Puede colocar mouse Hola sobre cada vértice en hello ver toodisplay información acerca de él.

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Al hacer clic en un vértice cargará hello **detalles de vértices** para ese elemento. Haga clic en hello **mapa 1** detalles de toodisplay de vértices para este elemento. Seleccione **confirmar** navegación de hello tooconfirm.

    ![Detalles del vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Tenga en cuenta que ahora tiene vínculos al principio de Hola de página de Hola que son las tareas y toovertices relacionados.

    > [!NOTE]
    > También puede llegar a esta página volviendo demasiado**DAG detalles**, seleccione **detalles de vértices**y, a continuación, seleccionando hello **mapa 1** vértices.
    >
    >

    * **Contadores del vértice** muestra información de los contadores de este vértice.
    * **Tareas** muestra las tareas de este vértice.
    * **Intentos de tareas** muestra información acerca de las tareas de toorun de intentos para este vértice.
    * **Orígenes y receptores** muestra los orígenes de datos y los receptores de este vértice.

      > [!NOTE]
      > Como con el menú anterior de hello, puede desplazarse a la visualización de columnas de Hola para tareas, los intentos de tarea y orígenes de & Sinks__ toodisplay vincula toomore información para cada elemento.
      >
      >
11. Seleccione **tareas**, y, a continuación, seleccione Hola denominado **00_000000**. De este modo se mostrarán los **Detalles de la tarea** de esta tarea. En esta pantalla, puede ver los **Contadores de tarea** y los **Intentos de tarea**.

    ![Detalles de la tarea](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo ver hello toouse Tez, obtenga más información sobre [utilizando Hive en HDInsight](hdinsight-use-hive.md).

Para obtener más información técnica sobre Tez, consulte hello [Tez página en Hortonworks](http://hortonworks.com/hadoop/tez/).
