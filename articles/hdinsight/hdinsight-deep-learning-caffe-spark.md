---
title: aaaUse Caffe en Azure HDInsight Spark para aprendizaje profundo distribuida | Documentos de Microsoft
description: Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido


## <a name="introduction"></a>Introducción

Aprendizaje profundo está afectando al todo, desde servicios de salud tootransportation toomanufacturing y mucho más. Las empresas están transformando toodeep aprendizaje toosolve problemas de disco duro, como [clasificación de la imagen](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [el reconocimiento de voz](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), objeto reconocimiento y traducción de la máquina. 

Hay [muchos marcos populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), entre los que se incluyen [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe es uno de hello más famosas marcos no simbólico Red neuronal (imperativo) y se usa ampliamente en muchas áreas, incluidos la visión de equipo. Además, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina Caffe con Apache Spark, en cuyo caso el aprendizaje profundo se puede usar fácilmente en un clúster existente de Hadoop junto con las canalizaciones ETL de Spark, lo que reduce la complejidad y latencia del sistema para el aprendizaje de un extremo al otro.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) es hello solo oferta de Hadoop en la nube completamente administrado que proporciona optimizado clústeres de análisis de código abierto para Spark, Hive, MapReduce, HBase, tormenta, Kafka y R Server respaldado por un SLA del 99,9%. Cada una de estas tecnologías de macrodatos, así como las aplicaciones de fabricantes de software independientes, se pueden implementar fácilmente como clústeres administrados, con seguridad y supervisión de nivel empresarial.

Algunos usuarios se nos pide que acerca de cómo toouse profundo de aprendizaje en HDInsight, que es el producto de PaaS Hadoop de Microsoft. Tenemos más tooshare Hola futura, pero hoy queremos toosummarize un blog técnico acerca de cómo toouse Caffe en HDInsight Spark.

Si ha instalado Caffe con anterioridad, observará que la instalación de este marco es un poco complicada. En este blog se se ilustrará cómo tooinstall [Caffe en Spark](https://github.com/yahoo/CaffeOnSpark) para un clúster de HDInsight, a continuación, utilice Hola integrados MNIST demostración toodemostrate cómo toouse aprendizaje profundo distribuidas con HDInsight Spark en las CPU.

Hay cuatro tooget los pasos principales que funciona en HDInsight.

1. Instalar las dependencias de hello necesario en todos los nodos de Hola
2. Compilar Caffe en Spark para HDInsight en el nodo principal de Hola
3. Distribuir los nodos de trabajador de hello requerido bibliotecas tooall Hola
4. Componer un modelo de Caffe y ejecutarlo de forma distribuida

Puesto que HDInsight es una solución de PaaS, ofrece características de la plataforma excelente: por lo que es bastante fácil tooperform algunas tareas. Se llama a uno de las características de Hola que utilizamos mucho en esta entrada de blog [acción de secuencia de comandos](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), con lo que puede ejecutar el shell de comandos toocustomize nodos del clúster (nodo principal, el nodo de trabajo o borde).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Paso 1: Instalar las dependencias de hello necesario en todos los nodos de Hola

tooget iniciado, necesitamos dependencias de hello tooinstall que necesitamos. sitio de Hello Caffe y [CaffeOnSpark sitio](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) ofrece algunos wiki muy útil para instalar las dependencias de Hola para Spark en modo YARN (que es el modo de Hola para HDInsight Spark), pero necesitamos tooadd unas más dependencias de plataforma de HDInsight. Se usará la acción de secuencia de comandos de hello siguiente y ejecutarlo en todos los nodos principales de Hola y nodos de trabajador. Esta acción de script tardará aproximadamente 20 minutos en realizarse, ya que dichas dependencias a su vez dependen de otros paquetes. Debe colocarla en alguna ubicación que sea accesible tooyour clúster de HDInsight, como una ubicación de GitHub o la cuenta de almacenamiento de blobs de hello predeterminada.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Hay dos pasos de acción de secuencia de comandos de hello anterior. Hola primer paso es tooinstall todos Hola bibliotecas necesarias. Dichas bibliotecas incluyen bibliotecas necesarias de Hola para compilar Caffe (por ejemplo, gflags, glog) y ejecuta Caffe (por ejemplo, numpy). Estamos usando libatlas para optimizar la CPU, pero siempre puede seguir hello CaffeOnSpark wiki sobre la instalación de otras bibliotecas de optimización, como MKL o CUDA (para GPU).

Hola segundo paso es toodownload, compilar e instalar protobuf 2.5.0 para Caffe en tiempo de ejecución. Protobuf 2.5.0 [es necesario](https://github.com/yahoo/CaffeOnSpark/issues/87); sin embargo, esta versión no está disponible como un paquete en 16 Ubuntu, por lo que necesitamos toocompile desde el código fuente de Hola. También hay unos pocos recursos en hello Internet acerca de cómo toocompile, como [esto](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply empezar a trabajar, puede simplemente ejecutar esta acción de secuencia de comandos en el trabajo de clúster tooall Hola nodos nodos y head (para HDInsight 3.5). Puede ejecutar acciones de script de Hola para un clúster de ejecución, o también puede ejecutar acciones de script de Hola durante el tiempo de aprovisionamiento de clúster de Hola. Para obtener más información sobre las acciones de script de Hola, consulte la documentación de hello [aquí](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Acciones de script tooInstall dependencias](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Paso 2: Generar Caffe en Spark para HDInsight en el nodo principal de Hola

segundo paso de Hello es toobuild Caffe en el nodo principal de hello y, a continuación, distribuir nodos de trabajador de hello compilado bibliotecas tooall Hola. En este paso, deberá demasiado[ssh en el nodo principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), a continuación, basta con que siga hello [CaffeOnSpark el proceso de compilación](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), y a continuación se muestra script de Hola que se puede usar toobuild CaffeOnSpark con unos pocos pasos adicionales. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Puede que necesite toodo más que indica qué documentación Hola de CaffeOnSpark. Hola cambios son:
- Cambiar solo tooCPU y usar libatlas para este propósito específico.
- Hola PUT conjuntos de datos toohello almacenamiento de blobs, que es una ubicación compartida accesible tooall nodos de trabajador para su uso posterior.
- Hola PUT compila tooBLOB almacenamiento de Caffe bibliotecas, y más adelante copiará los nodos de hello tooall de bibliotecas con el tiempo de compilación adicionales de tooavoid de acciones de secuencias de comandos.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Solución de problemas: An Ant BuildException has occured: exec returned: 2

Cuando intente primero toobuild CaffeOnSpark, en ocasiones, lo dirá

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Repositorio de código de hello simplemente limpia por "hacer limpia" y, a continuación, en ejecución "Asegúrese de compilación" resolverá este problema, siempre que tengan dependencias correctas Hola.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Solución de problemas: se ha superado el tiempo de espera de la conexión con el repositorio de Maven

A veces maven me da error de tiempo de espera de conexión de hello, toobelow similar:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Se será correcto después de esperar unos minutos y vuelva a intentar solo código de hello toorebuild, por lo que podría ser experto en algún modo límites Hola tráfico procedente de una dirección IP determinada.


### <a name="troubleshooting-test-failure-for-caffe"></a>Solución de problemas: error en las pruebas de Caffe

Probablemente verá un error de prueba al realizar la comprobación final hello CaffeOnSpark, parecido a la siguiente. Esto es prabably relacionada con codificación UTF-8, pero no debería afectar el uso de Hola de Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Paso 3: Distribuir nodos de trabajador de hello requerido bibliotecas tooall Hola

Hola siguiente paso es bibliotecas de hello toodistribute (básicamente Hola bibliotecas en CaffeOnSpark/caffe-público/distribuir/lib/y CaffeOnSpark/caffe-puntos de distri/distribuir/lib /) nodos de hello tooall. En el paso 2, colocamos esas bibliotecas de almacenamiento de blobs y, en este paso, se usará toocopy de acciones de script tooall Hola nodos principales y trabajo.

toodo, simple ejecutar una acción de secuencia de comandos siguiente (debe clúster tooyour específico de toopoint toohello ubicación correcta):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Dado que en el paso 2, se coloca en almacenamiento de blobs que es accesibles tooall Hola Hola, en este paso se simplemente puede copiar nodos de hello tooall.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Paso 4: Componer un modelo de Caffe y ejecutarlo de forma distribuida

Después de ejecutar Hola por encima de los pasos, Caffe está ya instalado en el nodo principal de Hola y estamos toogo buena. Hola siguiente paso es un modelo de Caffe toowrite. 

Caffe está usando un "expresivo architecture", donde para crear un modelo, que es necesario toodefine un archivo de configuración y sin escribir código en absoluto (en la mayoría de los casos). Vamos a examinar dicha arquitectura. 

modelo de Hola que se entrenará hoy en día es un modelo de ejemplo para el entrenamiento de MNIST. base de datos de Hello MNIST de dígitos escritas a mano tiene un conjunto de entrenamiento de 60.000 ejemplos y un conjunto de pruebas de 10.000 ejemplos. Es un subconjunto de un conjunto mayor disponible en NIST. dígitos Hola han sido tamaño normalizado y centrado en una imagen de tamaño fijo. CaffeOnSpark tiene algún conjunto de datos de secuencias de comandos toodownload hello y convertirla en el formato correcto de saludo.

CaffeOnSpark proporciona algunos ejemplos de topologías de red para el entrenamiento de MNIST. Tiene un diseño "nice" de dividir la arquitectura de red de hello (topología de Hola de hello red) y la optimización. En este caso, se requieren dos archivos: 

archivo de "Solver" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) se usa para supervisar optimización hello y generación de actualizaciones de parámetros. Por ejemplo, define si CPU o la GPU se usará, ¿cuál es el momento de hello, será el número de iteraciones, etcetera. También define qué topología de red de neurona debe Hola uso de programa (que es el segundo archivo de hello que necesitamos). Para obtener más información acerca de Solver, consulte demasiado[Caffe documentación](http://caffe.berkeleyvision.org/tutorial/solver.html).

En este ejemplo, puesto que estamos usando CPU en lugar de GPU, debemos cambiamos Hola última línea:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

Puede cambiar otras líneas si fuera necesario.

Hola segundo archivo (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define red neurona de hello el aspecto y la entrada pertinente de Hola y el archivo de salida. También es necesario ubicación de datos del entrenamiento de Hola de tooupdate Hola archivo tooreflect. Hola de cambio después de la parte en lenet_memory_train_test.prototxt (necesita clúster tooyour específico de toopoint toohello ubicación correcta):

- cambiar file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" demasiado "wasb: / / / proyectos/machine_learning/image_dataset/mnist_train_lmdb"
- Cambie "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" demasiado "wasb: / / / proyectos/machine_learning/image_dataset/mnist_test_lmdb"

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Para obtener más información sobre cómo toodefine Hola red, compruebe hello [Caffe documentación en el conjunto de datos MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

A fin de Hola de este blog, simplemente usamos este sencillo ejemplo MNIST. Debe ejecutar el comando de Hola por debajo del nodo principal de hello:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

Básicamente se distribuye Hola requerido archivos hilados contenedor tooeach (lenet_memory_solver.prototxt y lenet_memory_train_test.prototxt) y también establece Hola ruta de acceso relevante de cada tooLD_LIBRARY_PATH de controlador/ejecutor Spark, que se define en hello anterior fragmento de código y los puntos de toohello ubicación del código que tenga las bibliotecas de CaffeOnSpark. 

## <a name="monitoring-and-troubleshooting"></a>Supervisión y solución de problemas

Puesto que estamos usando el modo de clúster de hilo, en cuyo caso será controlador de Spark Hola contenedor arbitrario tooan programada (y un nodo de trabajo arbitrario) solo verá en la salida de consola Hola un resultado similar:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Si desea tooknow ¿qué ha ocurrido, suele ser preciso registro del controlador de tooget Hola Spark, que se proporciona más información. En este caso, debe toogo toohello YARN toofind Hola relevante YARN registros de IU. Puede obtener Hola UI YARN esta dirección URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![IU de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Puede echar un vistazo al número de recursos que se asignan a esta aplicación concreta. Puede hacer clic en vínculos de "Programador" hello y, a continuación, verá que para esta aplicación, hay 9 contenedores que se ejecutan. Pedimos YARN tooprovide 8 ejecutor y otro contenedor es para el proceso de controlador. 

![Programador de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Puede que desee toocheck Hola controlador registros o registros de contenedor si hay errores. Para los registros del controlador, puede haga clic en el identificador de la aplicación hello en la interfaz de usuario de YARN y luego haga clic en el botón de "Registros" Hola. se escriben los registros de controlador de Hello en stderr.

![UI de YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Por ejemplo, podría ver algunos error Hola por debajo de los registros del controlador hello, que indica que asignar demasiados elementos de ejecución.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

En ocasiones, puede producirse problema hello en ejecutor en lugar de controladores. En este caso, debe toocheck Hola contenedor registros. Puede obtener siempre los registros de contenedor de hello y, a continuación, obtener el contenedor errores de Hola. Por ejemplo, este error puede aparecer al ejecutar Caffe.

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

En este caso, necesita el identificador del contenedor de tooget hello no se pudo (Hola por encima de caso, es container_1485916338528_0008_05_000005). A continuación deberá toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

desde el nodo principal de Hola. Después de comprobar el error del contenedor, se constata que se debe a que se ha usado el modo GPU (que debe usar el modo de CPU en su lugar) en lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Obtención de resultados

Puesto que se está asignando 8 ejecutor y topología de red de hello es simple, solo debería tardar unos 30 minutos toorun Hola de resultados. Desde la línea de comandos de hello, puede ver que se coloca Hola modelo toowasb:///mnist.model y coloque Hola resultados tooa carpeta denominada wasb: / / / mnist_features_result.

Puede obtener resultados de hello mediante la ejecución

    hadoop fs -cat hdfs:///mnist_features_result/*

y resultado de hello el siguiente aspecto:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Hola SampleID representa el identificador hello en el conjunto de datos de hello MNIST y etiqueta de hello es el número de Hola Hola modelo identifica.


## <a name="conclusion"></a>Conclusión

En esta documentación, que se ha intentado tooinstall CaffeOnSpark con ejecutar un ejemplo sencillo. HDInsight es una plataforma de proceso distribuido total administrado en la nube y Hola mejor lugar para ejecutar cargas de trabajo de análisis avanzado y aprendizaje automático en el conjunto de datos grande, y para el aprendizaje profundo distribuido, puede usar Caffe en aprendizaje profundo de HDInsight Spark tooperform tareas.


## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)

