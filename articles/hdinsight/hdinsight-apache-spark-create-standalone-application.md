---
title: "aaaCreate Scala aplicación toorun en clústeres de Spark - HDInsight de Azure | Documentos de Microsoft"
description: "Crear una aplicación de Spark escrita en Scala con Apache Maven como Hola de compilación del sistema y Arquetipo Maven existente para Scala proporcionada por IntelliJ IDEA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Crear un toorun de aplicación Scala Maven en clúster de Apache Spark en HDInsight

Obtenga información acerca de cómo toocreate una aplicación de Spark escrita en Scala con Maven IntelliJ IDEA. artículo Hello usa a Apache Maven cuando Hola sistema de compilación y se inicia con Arquetipo Maven existente por Scala proporcionada por IntelliJ IDEA.  Crear una aplicación Scala en IntelliJ IDEA implica Hola pasos:

* Use Maven como sistema de compilación de Hola.
* Actualizar las dependencias del módulo modelo de objeto de proyecto (POM) archivo tooresolve Spark.
* Escriba la aplicación con Scala.
* Generar un archivo jar que puede ser enviado tooHDInsight Spark clústeres.
* Ejecute la aplicación hello en un clúster de Spark mediante Livio.

> [!NOTE]
> HDInsight también proporciona un proceso de hello IntelliJ IDEA tooease de herramienta de complemento de crear y enviar aplicaciones tooan clúster de HDInsight Spark en Linux. Para obtener más información, consulte [complemento de herramientas de HDInsight de uso para toocreate IntelliJ IDEA y enviar solicitudes de Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de desarrollo de Oracle Java. Se puede instalar desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Un IDE de Java. En este artículo se usa IntelliJ IDEA 15.0.1. Se puede instalar desde [aquí](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Instale el complemento de Scala para IntelliJ IDEA.
Si no una petición no instalación IntelliJ IDEA para habilitar el complemento Scala, inicie IntelliJ IDEA y vaya a través de hello siguiendo los pasos tooinstall Hola complemento:

1. Inicie IntelliJ IDEA y, en la pantalla de bienvenida, haga clic en **Configure** (Configurar) y luego en **Plugins** (Complementos).
   
    ![Habilitar complemento de Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. En la siguiente pantalla de bienvenida, haga clic en **JetBrains instalar complemento** desde la esquina inferior izquierda de Hola. Hola **examinar JetBrains complementos** cuadro de diálogo que se abre, busque Scala y, a continuación, haga clic en **instalar**.
   
    ![Instalar complemento de Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Después de hello complemento se instala correctamente, haga clic en hello **botón de reiniciar la IDEA de IntelliJ** toorestart Hola IDE.

## <a name="create-a-standalone-scala-project"></a>Creación de un proyecto de Scala independiente
1. Inicie IntelliJ IDEA y cree un nuevo proyecto. En el cuadro de diálogo de proyecto nuevo hello, asegúrese de Hola siguientes opciones y, a continuación, haga clic en **siguiente**.
   
    ![Crear proyecto de Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Seleccione **Maven** como tipo de proyecto de Hola.
   * Especifique un **SDK de proyecto**. Haga clic en nuevo y navegue toohello directorio de instalación de Java, normalmente `C:\Program Files\Java\jdk1.8.0_66`.
   * Seleccione hello **crear desde Arquetipo** opción.
   * Seleccionar en lista Hola de archetypes **org.scala tools.archetypes:scala Arquetipo simple**. Esto creará estructura de directorio de Hola y descargar Hola necesario predeterminado dependencias toowrite Scala programa.
2. Proporcione los valores correspondientes para **GroupId**, **ArtifactId** y **Version**. Haga clic en **Siguiente**.
3. En el siguiente cuadro de diálogo hello, donde puede especificar el directorio particular de Maven y otras opciones de usuario, acepte los valores predeterminados de Hola y haga clic en **siguiente**.
4. En el último cuadro de diálogo hello, especifique un nombre de proyecto y una ubicación y, a continuación, haga clic en **finalizar**.
5. Eliminar hello **MySpec.Scala** de archivos en **src\test\scala\com\microsoft\spark\example**. No es necesario para la aplicación hello.
6. Si es necesario, cambie el nombre de archivos de origen y de prueba de hello predeterminados. Desde el panel izquierdo de Hola Hola IntelliJ IDEA, navegue demasiado**src\main\scala\com.microsoft.spark.example**. Haga clic en **App.scala**, haga clic en **refactorizar**, haga clic en cambiar el nombre archivo y en el cuadro de diálogo de hello, especifique el nuevo nombre de hello para la aplicación hello y, a continuación, haga clic en **refactorizar**.
   
    ![Cambiar el nombre de los archivos](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. En pasos posteriores de hello, actualizará hello pom.xml toodefine Hola dependencias Hola Spark Scala aplicación. Para esas dependencias toobe descarga y resuelve automáticamente, que debe configurar a Maven en consecuencia.
   
    ![Configurar Maven para descargas automáticas](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. De hello **archivo** menú, haga clic en **configuración**.
   2. Hola **configuración** diálogo cuadro, vaya demasiado**de compilación, ejecución, implementación** > **herramientas de generación de** > **Maven**  >  **Importar**.
   3. Seleccione la opción de hello demasiado**Maven importar proyectos automáticamente**.
   4. Haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).
8. Actualizar tooinclude del archivo de origen de hello Scala el código de aplicación. Abra y reemplace Hola existente código de ejemplo con el siguiente código de hello y guardar los cambios de Hola. Este código lee los datos de Hola de hello HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la sexta columna de Hola y escribe la salida de hello demasiado**/HVACOut** en almacenamiento de saludo predeterminado contenedor para el clúster de Hola.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Actualizar pom.xml Hola.
   
   1. En `<project>\<properties>` agregue Hola siguientes:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. En `<project>\<dependencies>` agregue Hola siguientes:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Guardar cambios toopom.xml.
10. Crear el archivo .jar Hola. IntelliJ IDEA permite crear JAR como un artefacto de un proyecto. Realizar pasos de Hola.
    
    1. De hello **archivo** menú, haga clic en **estructura del proyecto**.
    2. Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** y, a continuación, haga clic en hello además de símbolos. En el cuadro de diálogo emergente de hello, haga clic en **JAR**y, a continuación, haga clic en **de módulos con dependencias**.
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. Hola **crear JAR de módulos** diálogo cuadro, haga clic en el botón de puntos suspensivos hello (![puntos suspensivos](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) contra Hola **clase principal**.
    4. Hola **seleccionar clase de Main** cuadro de diálogo, clase de hello seleccione aparece de forma predeterminada y, a continuación, haga clic en **Aceptar**.
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. Hola **crear JAR de módulos** diálogo cuadro, asegúrese de que esa opción Hola demasiado**extraer toohello destino JAR** está seleccionada y, a continuación, haga clic en **Aceptar**. Así se crea un archivo JAR único con todas las dependencias.
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. pestaña de diseño de salida de Hello enumera todos los archivos JAR Hola que se incluyen como parte del proyecto de Maven Hola. Puede seleccionar y Hola delete aquellos en los que Hola Scala aplicación no tiene ninguna dependencia directa. Para la aplicación hello vamos a crear a continuación, puede quitar todos menos Hola último (**salida de compilación SparkSimpleApp**). Seleccione toodelete de archivos JAR de hello y, a continuación, haga clic en hello **eliminar** icono.
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Asegúrese de que **compilar en hacer** casilla está activada, lo que garantiza que jar Hola se crea cada vez proyecto Hola se compila o se actualiza. Haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).
    7. En la barra de menús de hello, haga clic en **generar**y, a continuación, haga clic en **proyecto realizar**. También puede hacer clic en **Generar artefactos** jar de hello toocreate. jar de salida Hello se crea una en **\out\artifacts**.
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Ejecutar la aplicación hello en clúster de Spark Hola
aplicación de hello toorun en clúster de hello, debe hacer los siguiente Hola:

* **Blob de almacenamiento de Azure de copia Hola aplicación jar toohello** asociado con el clúster de Hola. Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), por lo que utilidad, toodo un comando de línea. Hay muchos otros clientes, así que puede utilizar datos de tooupload. Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).
* **Usar Livio toosubmit un trabajo de la aplicación de forma remota** toohello clúster de Spark. Clústeres de Spark en HDInsight incluye Livio que expone REST extremos tooremotely enviar trabajos de Spark. Para obtener más información, vea [Envío remoto de trabajos de Spark mediante la utilización de Livy con clústeres Spark en HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Paso siguiente

En este artículo se habrá aprendido cómo toocreate una aplicación de scala Spark. Avance toohello siguiente artículo toolearn cómo toorun esta aplicación en un HDInsight Spark de clúster mediante Livio.

> [!div class="nextstepaction"]
>[Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

