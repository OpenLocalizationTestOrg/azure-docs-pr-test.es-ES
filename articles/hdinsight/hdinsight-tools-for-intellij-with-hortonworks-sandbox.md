---
title: Kit de herramientas de Azure para IntelliJ con espacio aislado de Hortonworks aaaUse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ con Hortonworks Sandbox."
keywords: herramientas de hadoop,consulte de hive,intellij,hortonworks sandbox,kit de herramientas de azure para intellij
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox

Obtenga información acerca de cómo toouse HDInsight Tools para aplicaciones de Apache Scala toodevelop IntelliJ y, a continuación, probar Hola aplicaciones en [espacio aislado de Hortonworks](http://hortonworks.com/products/sandbox/) ejecutando en la estación de trabajo. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) es un entorno de desarrollo integrado (IDE) de Java para el desarrollo de software informático. Después de que haya desarrollado y probado las aplicaciones en el espacio aislado de Hortonworks, puede moverlos demasiado[HDInsight de Azure](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar este tutorial, debe contar con lo siguiente:

- Hortonworks Data Platform (HDP) 2.4 en Hortonworks Sandbox ejecutándose en el entorno local. tooconfigure HDP, consulte [empezar a trabajar en el ecosistema de Hadoop de hello con un espacio aislado de Hadoop en una máquina virtual](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Las herramientas de HDInsight para IntelliJ solo se han probado con HDP 2.4. Expanda tooget HDP 2.4, **Archive de espacio aislado de Hortonworks** en hello [sitio de descargas de espacio aislado de Hortonworks](http://hortonworks.com/downloads/#sandbox).

- [Kit de desarrolladores de Java (JDK) versión 1.8 o posterior](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). Hola Kit de herramientas de Azure requiere JDK para IntelliJ.

- [Edición de la Comunidad de IDEA IntelliJ](https://www.jetbrains.com/idea/download) con hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) complemento hello y [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) complemento. Herramientas de HDInsight para IntelliJ está disponible como parte del Kit de herramientas de Azure para IntelliJ Hola. 

  tooinstall Hola complementos, Hola siguientes:

  1. Abra IntelliJ IDEA.
  2. En hello **bienvenida** pantalla, seleccione **configurar**y, a continuación, seleccione **complementos**.
  3. Seleccione **JetBrains instalar complemento** en la esquina inferior izquierda de Hola.
  4. Usar hello toosearch de función de búsqueda para **Scala**y, a continuación, seleccione **instalar**.
  5. Seleccione **reiniciar IntelliJ IDEA** instalación de hello toocomplete.
  6. Hola de Repita el paso 4 y 5 tooinstall **Azure Toolkit for IntelliJ**. Para obtener más información, consulte [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Creación de una aplicación de Scala en Spark

En esta sección, creará un proyecto de Scala de ejemplo con IntelliJ IDEA. En la siguiente sección hello, vincular IDEA IntelliJ toohello Hortonworks espacio aislado (emulador) antes de enviar proyecto Hola.

1. Abra IntelliJ IDEA desde la estación de trabajo. Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:

   a. Seleccione **HDInsight** > **Spark en HDInsight (Scala)**.

   b. Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:

    * **Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala
    * **SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola

   ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Seleccione **Siguiente**.

3. Hola siguiente **nuevo proyecto** diálogo cuadro, Hola siguientes:

    ![Creación de las propiedades del proyecto de Scala en IntelliJ](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Hola **nombre del proyecto** cuadro, escriba un nombre de proyecto.

    b. Hola **ubicación del proyecto** cuadro, escriba una ubicación de proyecto.

    c. Siguiente toohello **proyecto SDK** lista desplegable, seleccione **New**, seleccione **JDK**, y, a continuación, especifique la carpeta Hola de Java JDK versión 1.7 o posterior. Seleccione **Java 1.8** para clúster de hello Spark 2.x, o bien seleccione **Java 1.7** para clúster de hello Spark 1.x. ubicación predeterminada de Hello es C:\Program Files\Java\jdk1.8.x_xxx.

    d. Hola **versión Spark** lista desplegable, el Asistente para crear un proyecto Scala integra con la versión adecuada de Hola de SDK de Spark y Scala SDK. Si la versión de clúster de Spark hello es anterior a la 2.0, seleccione **inspirará 1.x**. De lo contrario, seleccione **Spark 2.x**. Este ejemplo utiliza Spark 1.6.2 (Scala 2.10.5). Asegúrese de que está usando repositorio Hola marcado Scala 2.10.x. No utilice repositorio Hola marcado Scala 2.11.x.

4. Seleccione **Finalizar**.

5. Si hello **proyecto** vista ya no está abierta, presione **Alt + 1** tooopen lo.

6. En **el Explorador de proyectos**, expanda el proyecto de hello y, a continuación, seleccione **src**.

7. Haga clic en **src**, seleccione demasiado**New**y, a continuación, seleccione **Scala clase**.

8. Hola **nombre** cuadro, escriba un nombre en hello **tipo** cuadro, seleccione **objeto**y, a continuación, seleccione **Aceptar**.

    ![ventana de crear una nueva clase de Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. En archivo de .scala de hello, pegue el siguiente código de hello:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. En hello **generar** menú, seleccione **proyecto de compilación**. Asegúrese de que la compilación de Hola se ha completado correctamente.


## <a name="link-toohello-hortonworks-sandbox"></a>Vincular toohello espacio aislado de Hortonworks

Antes de poder enlazar tooa Hortonworks espacio aislado (emulador), debe tener una aplicación de IntelliJ existente.

emulador de tooan toolink, Hola siguientes:

1. Proyecto abierto hello en IntelliJ.

2. En hello **vista** menú, seleccione **herramientas de Windows**y, a continuación, seleccione **explorador Azure**.

3. Expanda **Azure**, haga clic con el botón derecho en **HDInsight** y luego seleccione **Link an Emulator** (Vincular un emulador).

4. Hola **vínculo A nuevo emulador** ventana, escriba la contraseña de Hola que ha configurado para la cuenta raíz de Hola de hello espacio aislado de Hortonworks, escriba toothose similar de valores en la siguiente captura de pantalla de hello y, a continuación, seleccione **Aceptar** . 

   ![ventana de "Vínculo a nuevo emulador" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. emulador de hello tooconfigure, seleccione **Sí**.

Al emulador Hola está conectado correctamente, emulador hello (Hortonworks espacio aislado) se muestra en el nodo de HDInsight de Hola.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Enviar Hola Spark Scala aplicación toohello espacio aislado de Hortonworks

Después de haber vinculado emulador de toohello IntelliJ IDEA, puede enviar el proyecto.

Hola toosubmit un emulador tooan del proyecto, después de:

1. En **el Explorador de proyectos**, haga clic en proyecto de hello y, a continuación, seleccione **enviar Spark aplicación tooHDInsight**.

2. Hola siguientes:

    a. Hola **clúster Spark (solamente para Linux)** lista desplegable, seleccione el espacio aislado de Hortonworks local.

    b. Hola **nombre de la clase principal** cuadro, elija o escriba el nombre de la clase principal de Hola. Para este tutorial, se denomina hello **GroupByTest**.

3. Seleccione **Submit** (Enviar). los registros de envío de trabajos de Hola se muestran en la ventana de herramienta de envío de hello Spark.

## <a name="next-steps"></a>Pasos siguientes

- toolearn cómo ir demasiado toocreate aplicaciones de Spark para HDInsight mediante las herramientas de HDInsight para IntelliJ,[Use herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch un vídeo de herramientas de HDInsight para IntelliJ, vaya demasiado[introducir herramientas de HDInsight para IntelliJ para el desarrollo de Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn cómo las aplicaciones de Spark toodebug mediante Hola Kit de herramientas de forma remota en HDInsight a través de SSH, vaya demasiado[depurar de forma remota aplicaciones Spark en un clúster de HDInsight con el Kit de herramientas de Azure para IntelliJ a través de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn cómo las aplicaciones de Spark toodebug mediante Hola Kit de herramientas de forma remota en HDInsight a través de VPN, vaya demasiado[Use herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toodebug Spark para aplicaciones de forma remota en el clúster de HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- toolearn cómo toouse herramientas de HDInsight para Eclipse toocreate una aplicación Spark, vaya demasiado[Use herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch un vídeo de herramientas de HDInsight para Eclipse, vaya demasiado[usar la herramienta de HDInsight para aplicaciones de Eclipse toocreate Spark](https://mix.office.com/watch/1rau2mopb6fha).
