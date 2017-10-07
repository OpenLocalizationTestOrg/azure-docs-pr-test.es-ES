---
title: "aaaInstall Jupyter localmente & conectar el clúster de Azure HDInsight Spark tooan | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Jupyter notebook localmente en el equipo y conecte tooan clústeres de Apache Spark en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Instale Jupyter notebook en el equipo y conecte tooApache Spark en HDInsight

En este artículo aprenderá cómo tooinstall Jupyter notebook, con hello PySpark personalizado (para Python) y los kernels de Spark (para Scala) con inspirará magia y conecte el clúster de HDInsight de tooan de hello Bloc de notas. Puede haber una serie de motivos tooinstall Jupyter en el equipo local, y puede haber también algunos desafíos. Para obtener más información sobre esto, vea la sección hello [¿por qué debo instalar Jupyter en mi equipo](#why-should-i-install-jupyter-on-my-computer) final Hola de este artículo.

Hay tres pasos principales implicados en la instalación hello magia Spark y Jupyter en el equipo.

* Instalación de cuadernos de Jupyter Notebook
* Instalar hello PySpark y los kernels de Spark con hello magia Spark
* Configurar Spark mágica tooaccess clúster Spark en HDInsight

Para obtener más información acerca de los kernels personalizada hello y mágico de Spark Hola disponible para equipos portátiles de Jupyter con clúster de HDInsight, vea [clústeres de núcleos disponibles para equipos portátiles Jupyter con Linux de Apache Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Requisitos previos
requisitos previos de Hello descritos aquí no son para la instalación de Jupyter. Se trata de clúster de HDInsight de conexión hello Jupyter notebook tooan una vez instalado el Bloc de notas de Hola.

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Instalación de cuadernos de Jupyter Notebook en el equipo

Debe instalar Python para poder instalar cuadernos de Jupyter Notebook. Python y Jupyter están disponibles como parte del programa Hola a [distribución de Anaconda](https://www.continuum.io/downloads). Al instalar Anaconda, instalará una distribución de Python. Una vez instalado Anaconda, agrega hello Jupyter instalación ejecutando los comandos adecuados.

1. Descargar hello [installer Anaconda](https://www.continuum.io/downloads) para la plataforma y la configuración de ejecución Hola. Mientras el Asistente para instalación de ejecución hello, asegúrese de que seleccionar variable de ruta de acceso de hello opción tooadd Anaconda tooyour.
2. Siguiente ejecución Hola comando tooinstall Jupyter.

        conda install jupyter

    Para más información sobre la instalación de Jupyter, consulte [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Instalación de Jupyter con Anaconda).

## <a name="install-hello-kernels-and-spark-magic"></a>Instalar los kernels de Hola y magia Spark

Para obtener instrucciones sobre cómo mágico de Spark hello tooinstall, hello PySpark y los kernels de Spark, siga las instrucciones de instalación de Hola Hola [sparkmagic documentación](https://github.com/jupyter-incubator/sparkmagic#installation) en GitHub. Hello primer paso en la documentación de hello Spark mágica le pide que tooinstall mágico de Spark. Reemplace ese primer paso en el vínculo de hello con hello siguientes comandos, en función de la versión de Hola Hola del clúster de HDInsight que se va a conectar. Después de eso, siga Hola restantes pasos descritos en la documentación de hello Spark mágica. Si desea que los kernels de diferentes de hello tooinstall, debe realizar paso 3 en la sección de instrucciones de instalación mágica Spark Hola.

* Para los clústeres 3.4, instale sparkmagic 0.2.3 ejecutando `pip install sparkmagic==0.2.3`.

* Para los clústeres 3.5 y 3.6, instale sparkmagic 0.11.2 ejecutando `pip install sparkmagic==0.11.2`.

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Configurar el clúster de Spark tooconnect mágico tooHDInsight Spark

En esta sección, configurará mágico de Spark Hola que instaló anteriormente tooconnect tooan Apache Spark clúster debe haber creado ya en HDInsight de Azure.

1. Hola Jupyter la información de configuración normalmente se almacena en el directorio particular de los usuarios de Hola. comandos de su directorio particular en cualquier plataforma de sistema operativo, Hola tipo después de toolocate.

    Inicie el shell de Python Hola. En una ventana de comandos, escriba Hola siguiente:

        python

    En hello shell de Python, escriba Hola después toofind comando directorio particular de Hola.

        import os
        print(os.path.expanduser('~'))

2. Navegar por el directorio particular de toohello y cree una carpeta denominada **.sparkmagic** si aún no existe.
3. Dentro de la carpeta hello, cree un archivo denominado **config.json** y agregue Hola siguiente fragmento JSON en él.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Sustituya **{USERNAME}**, **{CLUSTERDNSNAME}** y **{BASE64ENCODEDPASSWORD}** por los valores que correspondan. Puede usar un conjunto de utilidades en su lenguaje de programación favoritos o contraseña codificada en línea toogenerate base64 de la contraseña real.

5. Configurar el latido derecho de hello en `config.json`. Debe agregar estos parámetros en el mismo nivel como Hola de hello `kernel_python_credentials` y `kernel_scala_credentials` fragmentos el agregado anteriormente. Para obtener un ejemplo de cómo y dónde tooadd Hola de latido, consulte esta [config.json ejemplo](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Para `sparkmagic 0.2.3` (clústeres 3.4):

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Para `sparkmagic 0.11.2` (clústeres v3.5 y v3.6), incluyen:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Se envían latidos tooensure que no se pierden las sesiones. Cuando un equipo deja de toosleep o se apaga, latido de hello no se envía, lo que resulta en hello sesión que se va a limpia. Para clústeres v3.4, si lo desea toodisable este comportamiento, puede establecer Hola Livio config `livy.server.interactive.heartbeat.timeout` demasiado`0` de hello Ambari UI. Para clústeres v3.5, si no establece la configuración de hello 3.5 anterior, no se eliminarán sesión Hola.

6. Reinicie Jupyter. Usar hello siguiente comando desde el símbolo del sistema Hola.

        jupyter notebook

7. Compruebe que puede conectar el clúster toohello mediante el Bloc de notas de hello Jupyter y que pueden usar mágico de Spark Hola disponible con los kernels de Hola. Realizar pasos de Hola.

    a. Cree un nuevo notebook. En la esquina derecha de hello, haga clic en **nuevo**. Debería ver kernel predeterminada de hello **Python2** y Hola dos kernels nuevos que se instalación, **PySpark** y **Spark**. Haga clic en **PySpark**.

    ![Kernels de cuadernos de Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels de cuadernos de Jupyter Notebook")

    b. Ejecute hello siguiente fragmento de código.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Si puede recuperar correctamente la salida de hello, se probará el clúster de HDInsight de toohello de conexión.

    >[!TIP]
    >Si desea tooupdate Hola Bloc de notas configuración tooconnect tooa otro clúster, actualizar hello config.json con nuevo conjunto de Hola de valores, tal como se muestra en el paso 3 anterior.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>¿Por qué debo instalar Jupyter en mi equipo?
Puede haber varias razones por las que podría desea tooinstall Jupyter en el equipo y, a continuación, conéctelo de clúster tooa Spark en HDInsight.

* Aunque los blocs de notas de Jupyter ya están disponibles en el clúster de hello Spark en HDInsight de Azure, instalar Jupyter en el equipo proporciona Hola toocreate opción localmente los blocs de notas, probar la aplicación en un clúster de ejecución y, a continuación, cargar Hola clúster de toohello blocs de notas. clúster de toohello de tooupload Hola blocs de notas, puede cargar ellos mediante el Bloc de notas de Jupyter de Hola que se está ejecutando o hello clúster, o guardarlos toohello /HdiNotebooks carpeta en la cuenta de almacenamiento de hello asociada con el clúster de Hola. ¿Para obtener más información sobre cómo se almacenan los blocs de notas en clúster de hello, consulte [donde se almacenan los blocs de notas de Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Con blocs de notas de hello disponibles localmente, puede conectarse toodifferent clústeres de Spark en función de sus necesidades de aplicación.
* Puede usar GitHub tooimplement un sistema de control de código fuente y tener control de versiones de los blocs de notas de Hola. También puede tener un entorno de colaboración donde varios usuarios pueden trabajar con hello mismo bloc de notas.
* Puede trabajar con cuadernos localmente sin necesidad de un clúster activo. Solo necesita un clúster tootest los blocs de notas con, no toomanually administrar los blocs de notas o en un entorno de desarrollo.
* Puede ser más fácil tooconfigure su propio entorno de desarrollo local que se trata de tooconfigure hello Jupyter instalación en clúster de Hola.  Puede aprovechar las ventajas de todo el software Hola que haya instalado localmente sin configurar uno o varios clústeres remotos.

> [!WARNING]
> Con Jupyter instalado en el equipo local, varios usuarios pueden ejecutar Hola mismo bloc de notas en hello Spark mismo clúster en hello mismo tiempo. En tal situación, se crean varias sesiones de Livy. Si surge un problema y desea toodebug, que será un tootrack tarea compleja qué sesión Livio pertenece toowhich usuario.
>
>

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
