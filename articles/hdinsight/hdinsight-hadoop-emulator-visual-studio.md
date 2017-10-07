---
title: herramientas de aaaData Lake para Visual Studio con el espacio aislado de Hortonworks - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola herramientas de Azure Data Lake para Visual Studio con el espacio aislado de Hortonworks Hola ejecuta en una máquina virtual local. Con estas herramientas, puede crear y ejecutar trabajos de Hive y Pig en espacio aislado de hello y ver la salida de trabajo y el historial."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Usar herramientas de Azure Data Lake de Hola para Visual Studio con hello espacio aislado de Hortonworks

Azure Data Lake incluye herramientas para trabajar con clústeres de Hadoop genéricos. Este documento proporciona los pasos de hello necesitan las herramientas de Data Lake con toouse Hola Hola espacio aislado de Hortonworks que se ejecuta en una máquina virtual local.

Usar Hola espacio aislado de Hortonworks, podrá toowork con Hadoop localmente en el entorno de desarrollo. Una vez que ha desarrollado una solución y desea toodeploy lo a escala, a continuación, puede mover clúster de HDInsight tooan.

## <a name="prerequisites"></a>Requisitos previos

* Hola espacio aislado de Hortonworks, ejecutándose en una máquina virtual en el entorno de desarrollo. Este documento se ha escrito y probado con espacio aislado de Hola que se ejecuta en Oracle VirtualBox. Para obtener información sobre cómo configurar el espacio aislado de hello, vea hello [empezar a trabajar con el espacio aislado de Hortonworks Hola.](hdinsight-hadoop-emulator-get-started.md) .

* Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (cualquier edición).

* Hola [Azure SDK para .NET](https://azure.microsoft.com/downloads/) 2.7.1 o una versión posterior.

* Hola [Data Lake de Azure tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Configurar las contraseñas de espacio aislado de Hola

Asegúrese de que ese Hola que espacio aislado de Hortonworks está ejecutando. A continuación, siga los pasos de Hola Hola [empezar a trabajar en hello espacio aislado de Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento. Estos pasos configuran contraseña Hola Hola SSH `root` cuenta y Hola Ambari `admin` cuenta. Estas contraseñas se utilizan cuando se conecta el espacio aislado de toohello desde Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Conectar el espacio aislado de hello herramientas toohello

1. Abra Visual Studio, seleccione **Ver** y, luego, **Explorador de servidores**.

2. De **Explorador de servidores**, contextual hello **HDInsight** entrada y, a continuación, seleccione **conectar tooHDInsight emulador**.

    ![Captura de pantalla del explorador de servidores, con Connect tooHDInsight emulador resaltado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. De hello **conectar tooHDInsight emulador** diálogo cuadro, escriba la contraseña de Hola que ha configurado para Ambari.

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Seleccione **siguiente** toocontinue.

4. Hola de uso **contraseña** contraseña de hello tooenter de campo que configuró para hello `root` cuenta. Deje Hola otros campos en el valor predeterminado de Hola.

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Seleccione **siguiente** toocontinue.

5. Espera para la validación de hello servicios toofinish. En algunos casos, validación puede producirá un error y se le pedirá que configuración de hello tooupdate. Si se produce un error de validación, seleccione **actualización**y esperar a que para la configuración de Hola y comprobación de hello toofinish de servicio.

    ![Captura de pantalla del cuadro de diálogo, con el botón Actualizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > proceso de actualización de Hello usa Ambari toomodify hello toowhat de configuración de espacio aislado de Hortonworks se espera con herramientas de Data Lake Hola para Visual Studio.

6. Después de la validación ha finalizado, seleccione **finalizar** toocomplete configuración.
    ![Captura de pantalla del cuadro de diálogo, con el botón Finalizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Dependiendo de su entorno de desarrollo y Hola cantidad de memoria asignada de la máquina virtual de toohello la velocidad de hello, puede tomar varias tooconfigure minutos y validar los servicios de Hola.

Después de seguir estos pasos, ahora tiene un **clúster local de HDInsight** entrada en el Explorador de servidores, en hello **HDInsight** sección.

## <a name="write-a-hive-query"></a>Escritura de una consulta de Hive

Hive proporciona un lenguaje de consultas de tipo SQL (HiveQL) para trabajar con datos estructurados. Uso Hola siguientes pasos le indican cómo toorun petición consultas en clúster local de Hola de toolearn.

1. En **Explorador de servidores**, haga clic en la entrada de hello para el clúster local de Hola que agregó anteriormente y, a continuación, seleccione **escribir una consulta de Hive**.

    ![Captura de pantalla del Explorador de servidores, con la opción Escribir una consulta de Hive resaltada](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Aparece una nueva ventana de consulta. Aquí puede rápidamente escribir y enviar una consulta toohello local del clúster.

2. En la nueva ventana de consulta hello, escriba Hola siguiente comando:

        select count(*) from sample_08;

    consulta de hello toorun, seleccione **enviar** en parte superior de Hola de ventana hello. Deje Hola otros valores (**lote** y el nombre del servidor) en valores predeterminados de Hola.

    ![Captura de pantalla de ventana de consulta, con el botón de envío de hello resaltado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    También puede utilizar menú desplegable de hello después demasiado**enviar** tooselect **avanzadas**. Opciones avanzadas permiten opciones adicionales de tooprovide cuando se envía el trabajo de Hola.

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Tras enviar consulta hello, aparece el estado del trabajo de Hola. estado del trabajo Hello muestra información sobre trabajo hello cuando se procesa por Hadoop. **Estado del trabajo** muestra el estado de saludo del trabajo de Hola. estado de Hola se actualiza periódicamente, o puede usar Hola actualizar icono toorefresh Hola estado manualmente.

    ![Captura de pantalla del cuadro de diálogo Vista de trabajos, con la opción Estado del trabajo resaltada](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Después de hello **estado del trabajo** cambia demasiado**finalizado**, se muestra un gráfico acíclico dirigido (DAG). Este diagrama describe la ruta de acceso de ejecución de Hola que se determina mediante Tez al procesar la consulta de Hive Hola. Tez es Hola predeterminado motor de ejecución Hive en clúster local de Hola.

    > [!NOTE]
    > Tez también es predeterminado de hello cuando utilizas clústeres de HDInsight basados en Linux. No es predeterminada de hello en HDInsight basados en Windows. toouse no existe, debe agregar la línea hello `set hive.execution.engine = tez;` toohello a partir de la consulta de Hive.

    Hola de uso **salida del trabajo** vincular la salida de hello tooview. En este caso, es 823, número de Hola de filas de tabla de sample_08 Hola. Puede ver información de diagnóstico sobre el trabajo de hello mediante hello **registro de trabajo** y **Descargar registro de YARN** vínculos.

4. También puede ejecutar trabajos de Hive interactivamente cambiando hello **lote** campo demasiado**Interactive**. Luego, seleccione **Ejecutar**.

    ![Captura de pantalla de los botones Interactivo y Ejecutar resaltados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Una consulta interactiva secuencias Hola registro de salida generado durante el procesamiento de toohello **HiveServer2 salida** ventana.

    > [!NOTE]
    > Hello información es Hola igual que está disponible en hello **registro de trabajo** vincular una vez que un trabajo ha finalizado.

    ![Captura de pantalla del registro de salida](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Creación de un proyecto de Hive

También puede crear un proyecto que incluya varios scripts de Hive. Utilizar un proyecto cuando haya relacionados con las secuencias de comandos o desea toostore scripts en un sistema de control de versiones.

1. En Visual Studio, seleccione **Archivo**, **Nuevo** y **Proyecto**.

2. En la lista Hola de proyectos, expanda **plantillas**, expanda **Azure Data Lake**y, a continuación, seleccione **HIVE (HDInsight)**. En la lista Hola de plantillas, seleccione **ejemplo Hive**. Escriba un nombre y una ubicación y, luego, seleccione **Aceptar**.

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, HIVE, Ejemplo de Hive y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Hola **ejemplo Hive** proyecto contiene dos secuencias de comandos, **WebLogAnalysis.hql** y **SensorDataAnalysis.hql**. Puede enviar estas secuencias de comandos mediante el uso de Hola mismo **enviar** situado en la parte superior de Hola de ventana hello.

## <a name="create-a-pig-project"></a>Creación de un proyecto de Pig

Aunque Hive proporciona un lenguaje similar a SQL para trabajar con datos estructurados, Pig funciona mediante la realización de transformaciones de datos. Pig proporciona un idioma (latino Pig) que le permite toodevelop una canalización de transformaciones. toouse Pig con hello local del clúster, siga estos pasos:

1. Abra Visual Studio y seleccione **Archivo**, **Nuevo** y **Proyecto**. En la lista Hola de proyectos, expanda **plantillas**, expanda **Azure Data Lake**y, a continuación, seleccione **Pig (HDInsight)**. En la lista Hola de plantillas, seleccione **aplicación Pig**. Escriba un nombre y una ubicación, y seleccione **Aceptar**.

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, Pig, Aplicación Pig y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Escriba Hola después de texto como contenido de Hola de hello **script.pig** archivo que se creó con este proyecto.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Mientras Pig usa un lenguaje distinto de Hive, cómo ejecutar trabajos de hello es coherente entre ambos lenguajes a través de hello **enviar** botón. Hola de selección desplegable situada junto a **enviar** muestra un cuadro de diálogo Enviar avanzada de Pig.

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. También se muestra la salida y el estado del trabajo de hello, Hola mismo como una consulta de Hive.

    ![Captura de pantalla de un trabajo de Pig finalizado](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Vista de trabajos

Herramientas de Data Lake le permiten ver información acerca de los trabajos que se han ejecutado en Hadoop de tooeasily. Use Hola siguientes pasos le indican los trabajos de hello toosee que se han ejecutado en el clúster local de Hola.

1. De **Explorador de servidores**, haga clic en el clúster local de hello y, a continuación, seleccione **ver trabajos**. Se muestra una lista de trabajos que se han enviado toohello clúster.

    ![Captura de pantalla del Explorador de servidores, con la opción Ver trabajos resaltada](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. En lista de Hola de trabajos, seleccione uno de detalles del trabajo tooview Hola.

    ![Captura de pantalla del explorador trabajo con uno de los trabajos de hello resaltados](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    información de Hola que aparece es similar toowhat que verá después de ejecutar una consulta de Pig o Hive, incluidos vínculos tooview Hola resultados y registro de la información.

3. También puede modificar y volver a enviar el trabajo de Hola desde aquí.

## <a name="view-hive-databases"></a>Vista de bases de datos de Hive

1. En **Explorador de servidores**, expanda hello **clúster local de HDInsight** entrada y, a continuación, expanda **bases de datos de Hive**. Hola **predeterminado** y **xademo** se muestran las bases de datos en clúster local de Hola. Expandir una base de datos muestra tablas Hola dentro de la base de datos de Hola.

    ![Captura de pantalla del Explorador de servidores, con las bases de datos expandidas](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Al expandir una tabla, muestran columnas Hola de dicha tabla. tooquickly ver datos de hello, haga clic en una tabla y seleccione **vista Top 100 Rows**.

    ![Captura de pantalla del Explorador de servidores, con una tabla expandida y la opción Ver las 100 primeras filas seleccionada](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Propiedades de las bases de datos y de las tablas

Puede ver propiedades de Hola de una base de datos o una tabla. Seleccionar **propiedades** muestra los detalles de elemento de hello seleccionado en la ventana de propiedades de Hola. Por ejemplo, ver la información de Hola que se muestra en la siguiente captura de pantalla de hello:

![Captura de pantalla de la ventana Propiedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Creación de una tabla

toocreate una tabla, haga clic en una base de datos y, a continuación, seleccione **Create Table**.

![Captura de pantalla del Explorador de servidores, con la opción Crear tabla resaltada](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

A continuación, puede crear tabla Hola usando un formulario. En parte inferior de Hola de hello siguiente captura de pantalla, puede ver Hola HiveQL sin formato que es usado toocreate Hola tabla.

![Captura de pantalla del formulario de hello usa toocreate una tabla](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Pasos siguientes

* [Cables de Hola de aprendizaje de hello espacio aislado de Hortonworks](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
