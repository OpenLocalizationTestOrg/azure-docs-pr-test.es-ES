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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="dae76-103">Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido</span><span class="sxs-lookup"><span data-stu-id="dae76-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="dae76-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="dae76-104">Introduction</span></span>

<span data-ttu-id="dae76-105">Aprendizaje profundo está afectando al todo, desde servicios de salud tootransportation toomanufacturing y mucho más.</span><span class="sxs-lookup"><span data-stu-id="dae76-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="dae76-106">Las empresas están transformando toodeep aprendizaje toosolve problemas de disco duro, como [clasificación de la imagen](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [el reconocimiento de voz](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), objeto reconocimiento y traducción de la máquina.</span><span class="sxs-lookup"><span data-stu-id="dae76-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="dae76-107">Hay [muchos marcos populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), entre los que se incluyen [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe es uno de hello más famosas marcos no simbólico Red neuronal (imperativo) y se usa ampliamente en muchas áreas, incluidos la visión de equipo.</span><span class="sxs-lookup"><span data-stu-id="dae76-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="dae76-108">Además, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina Caffe con Apache Spark, en cuyo caso el aprendizaje profundo se puede usar fácilmente en un clúster existente de Hadoop junto con las canalizaciones ETL de Spark, lo que reduce la complejidad y latencia del sistema para el aprendizaje de un extremo al otro.</span><span class="sxs-lookup"><span data-stu-id="dae76-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="dae76-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) es hello solo oferta de Hadoop en la nube completamente administrado que proporciona optimizado clústeres de análisis de código abierto para Spark, Hive, MapReduce, HBase, tormenta, Kafka y R Server respaldado por un SLA del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="dae76-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="dae76-110">Cada una de estas tecnologías de macrodatos, así como las aplicaciones de fabricantes de software independientes, se pueden implementar fácilmente como clústeres administrados, con seguridad y supervisión de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="dae76-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="dae76-111">Algunos usuarios se nos pide que acerca de cómo toouse profundo de aprendizaje en HDInsight, que es el producto de PaaS Hadoop de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dae76-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="dae76-112">Tenemos más tooshare Hola futura, pero hoy queremos toosummarize un blog técnico acerca de cómo toouse Caffe en HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="dae76-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="dae76-113">Si ha instalado Caffe con anterioridad, observará que la instalación de este marco es un poco complicada.</span><span class="sxs-lookup"><span data-stu-id="dae76-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="dae76-114">En este blog se se ilustrará cómo tooinstall [Caffe en Spark](https://github.com/yahoo/CaffeOnSpark) para un clúster de HDInsight, a continuación, utilice Hola integrados MNIST demostración toodemostrate cómo toouse aprendizaje profundo distribuidas con HDInsight Spark en las CPU.</span><span class="sxs-lookup"><span data-stu-id="dae76-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="dae76-115">Hay cuatro tooget los pasos principales que funciona en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dae76-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="dae76-116">Instalar las dependencias de hello necesario en todos los nodos de Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="dae76-117">Compilar Caffe en Spark para HDInsight en el nodo principal de Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="dae76-118">Distribuir los nodos de trabajador de hello requerido bibliotecas tooall Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="dae76-119">Componer un modelo de Caffe y ejecutarlo de forma distribuida</span><span class="sxs-lookup"><span data-stu-id="dae76-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="dae76-120">Puesto que HDInsight es una solución de PaaS, ofrece características de la plataforma excelente: por lo que es bastante fácil tooperform algunas tareas.</span><span class="sxs-lookup"><span data-stu-id="dae76-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="dae76-121">Se llama a uno de las características de Hola que utilizamos mucho en esta entrada de blog [acción de secuencia de comandos](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), con lo que puede ejecutar el shell de comandos toocustomize nodos del clúster (nodo principal, el nodo de trabajo o borde).</span><span class="sxs-lookup"><span data-stu-id="dae76-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="dae76-122">Paso 1: Instalar las dependencias de hello necesario en todos los nodos de Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="dae76-123">tooget iniciado, necesitamos dependencias de hello tooinstall que necesitamos.</span><span class="sxs-lookup"><span data-stu-id="dae76-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="dae76-124">sitio de Hello Caffe y [CaffeOnSpark sitio](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) ofrece algunos wiki muy útil para instalar las dependencias de Hola para Spark en modo YARN (que es el modo de Hola para HDInsight Spark), pero necesitamos tooadd unas más dependencias de plataforma de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dae76-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="dae76-125">Se usará la acción de secuencia de comandos de hello siguiente y ejecutarlo en todos los nodos principales de Hola y nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="dae76-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="dae76-126">Esta acción de script tardará aproximadamente 20 minutos en realizarse, ya que dichas dependencias a su vez dependen de otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="dae76-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="dae76-127">Debe colocarla en alguna ubicación que sea accesible tooyour clúster de HDInsight, como una ubicación de GitHub o la cuenta de almacenamiento de blobs de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dae76-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

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


<span data-ttu-id="dae76-128">Hay dos pasos de acción de secuencia de comandos de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="dae76-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="dae76-129">Hola primer paso es tooinstall todos Hola bibliotecas necesarias.</span><span class="sxs-lookup"><span data-stu-id="dae76-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="dae76-130">Dichas bibliotecas incluyen bibliotecas necesarias de Hola para compilar Caffe (por ejemplo, gflags, glog) y ejecuta Caffe (por ejemplo, numpy).</span><span class="sxs-lookup"><span data-stu-id="dae76-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="dae76-131">Estamos usando libatlas para optimizar la CPU, pero siempre puede seguir hello CaffeOnSpark wiki sobre la instalación de otras bibliotecas de optimización, como MKL o CUDA (para GPU).</span><span class="sxs-lookup"><span data-stu-id="dae76-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="dae76-132">Hola segundo paso es toodownload, compilar e instalar protobuf 2.5.0 para Caffe en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dae76-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="dae76-133">Protobuf 2.5.0 [es necesario](https://github.com/yahoo/CaffeOnSpark/issues/87); sin embargo, esta versión no está disponible como un paquete en 16 Ubuntu, por lo que necesitamos toocompile desde el código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="dae76-134">También hay unos pocos recursos en hello Internet acerca de cómo toocompile, como [esto](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="dae76-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="dae76-135">toosimply empezar a trabajar, puede simplemente ejecutar esta acción de secuencia de comandos en el trabajo de clúster tooall Hola nodos nodos y head (para HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="dae76-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="dae76-136">Puede ejecutar acciones de script de Hola para un clúster de ejecución, o también puede ejecutar acciones de script de Hola durante el tiempo de aprovisionamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="dae76-137">Para obtener más información sobre las acciones de script de Hola, consulte la documentación de hello [aquí](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="dae76-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Acciones de script tooInstall dependencias](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="dae76-139">Paso 2: Generar Caffe en Spark para HDInsight en el nodo principal de Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="dae76-140">segundo paso de Hello es toobuild Caffe en el nodo principal de hello y, a continuación, distribuir nodos de trabajador de hello compilado bibliotecas tooall Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="dae76-141">En este paso, deberá demasiado[ssh en el nodo principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), a continuación, basta con que siga hello [CaffeOnSpark el proceso de compilación](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), y a continuación se muestra script de Hola que se puede usar toobuild CaffeOnSpark con unos pocos pasos adicionales.</span><span class="sxs-lookup"><span data-stu-id="dae76-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

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

<span data-ttu-id="dae76-142">Puede que necesite toodo más que indica qué documentación Hola de CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="dae76-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="dae76-143">Hola cambios son:</span><span class="sxs-lookup"><span data-stu-id="dae76-143">hello changes are:</span></span>
- <span data-ttu-id="dae76-144">Cambiar solo tooCPU y usar libatlas para este propósito específico.</span><span class="sxs-lookup"><span data-stu-id="dae76-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="dae76-145">Hola PUT conjuntos de datos toohello almacenamiento de blobs, que es una ubicación compartida accesible tooall nodos de trabajador para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="dae76-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="dae76-146">Hola PUT compila tooBLOB almacenamiento de Caffe bibliotecas, y más adelante copiará los nodos de hello tooall de bibliotecas con el tiempo de compilación adicionales de tooavoid de acciones de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="dae76-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="dae76-147">Solución de problemas: An Ant BuildException has occured: exec returned: 2</span><span class="sxs-lookup"><span data-stu-id="dae76-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="dae76-148">Cuando intente primero toobuild CaffeOnSpark, en ocasiones, lo dirá</span><span class="sxs-lookup"><span data-stu-id="dae76-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="dae76-149">Repositorio de código de hello simplemente limpia por "hacer limpia" y, a continuación, en ejecución "Asegúrese de compilación" resolverá este problema, siempre que tengan dependencias correctas Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="dae76-150">Solución de problemas: se ha superado el tiempo de espera de la conexión con el repositorio de Maven</span><span class="sxs-lookup"><span data-stu-id="dae76-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="dae76-151">A veces maven me da error de tiempo de espera de conexión de hello, toobelow similar:</span><span class="sxs-lookup"><span data-stu-id="dae76-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="dae76-152">Se será correcto después de esperar unos minutos y vuelva a intentar solo código de hello toorebuild, por lo que podría ser experto en algún modo límites Hola tráfico procedente de una dirección IP determinada.</span><span class="sxs-lookup"><span data-stu-id="dae76-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="dae76-153">Solución de problemas: error en las pruebas de Caffe</span><span class="sxs-lookup"><span data-stu-id="dae76-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="dae76-154">Probablemente verá un error de prueba al realizar la comprobación final hello CaffeOnSpark, parecido a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="dae76-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="dae76-155">Esto es prabably relacionada con codificación UTF-8, pero no debería afectar el uso de Hola de Caffe</span><span class="sxs-lookup"><span data-stu-id="dae76-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="dae76-156">Paso 3: Distribuir nodos de trabajador de hello requerido bibliotecas tooall Hola</span><span class="sxs-lookup"><span data-stu-id="dae76-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="dae76-157">Hola siguiente paso es bibliotecas de hello toodistribute (básicamente Hola bibliotecas en CaffeOnSpark/caffe-público/distribuir/lib/y CaffeOnSpark/caffe-puntos de distri/distribuir/lib /) nodos de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="dae76-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="dae76-158">En el paso 2, colocamos esas bibliotecas de almacenamiento de blobs y, en este paso, se usará toocopy de acciones de script tooall Hola nodos principales y trabajo.</span><span class="sxs-lookup"><span data-stu-id="dae76-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="dae76-159">toodo, simple ejecutar una acción de secuencia de comandos siguiente (debe clúster tooyour específico de toopoint toohello ubicación correcta):</span><span class="sxs-lookup"><span data-stu-id="dae76-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="dae76-160">Dado que en el paso 2, se coloca en almacenamiento de blobs que es accesibles tooall Hola Hola, en este paso se simplemente puede copiar nodos de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="dae76-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="dae76-161">Paso 4: Componer un modelo de Caffe y ejecutarlo de forma distribuida</span><span class="sxs-lookup"><span data-stu-id="dae76-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="dae76-162">Después de ejecutar Hola por encima de los pasos, Caffe está ya instalado en el nodo principal de Hola y estamos toogo buena.</span><span class="sxs-lookup"><span data-stu-id="dae76-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="dae76-163">Hola siguiente paso es un modelo de Caffe toowrite.</span><span class="sxs-lookup"><span data-stu-id="dae76-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="dae76-164">Caffe está usando un "expresivo architecture", donde para crear un modelo, que es necesario toodefine un archivo de configuración y sin escribir código en absoluto (en la mayoría de los casos).</span><span class="sxs-lookup"><span data-stu-id="dae76-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="dae76-165">Vamos a examinar dicha arquitectura.</span><span class="sxs-lookup"><span data-stu-id="dae76-165">So let's take a look there.</span></span> 

<span data-ttu-id="dae76-166">modelo de Hola que se entrenará hoy en día es un modelo de ejemplo para el entrenamiento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="dae76-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="dae76-167">base de datos de Hello MNIST de dígitos escritas a mano tiene un conjunto de entrenamiento de 60.000 ejemplos y un conjunto de pruebas de 10.000 ejemplos.</span><span class="sxs-lookup"><span data-stu-id="dae76-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="dae76-168">Es un subconjunto de un conjunto mayor disponible en NIST.</span><span class="sxs-lookup"><span data-stu-id="dae76-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="dae76-169">dígitos Hola han sido tamaño normalizado y centrado en una imagen de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="dae76-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="dae76-170">CaffeOnSpark tiene algún conjunto de datos de secuencias de comandos toodownload hello y convertirla en el formato correcto de saludo.</span><span class="sxs-lookup"><span data-stu-id="dae76-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="dae76-171">CaffeOnSpark proporciona algunos ejemplos de topologías de red para el entrenamiento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="dae76-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="dae76-172">Tiene un diseño "nice" de dividir la arquitectura de red de hello (topología de Hola de hello red) y la optimización.</span><span class="sxs-lookup"><span data-stu-id="dae76-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="dae76-173">En este caso, se requieren dos archivos:</span><span class="sxs-lookup"><span data-stu-id="dae76-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="dae76-174">archivo de "Solver" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) se usa para supervisar optimización hello y generación de actualizaciones de parámetros.</span><span class="sxs-lookup"><span data-stu-id="dae76-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="dae76-175">Por ejemplo, define si CPU o la GPU se usará, ¿cuál es el momento de hello, será el número de iteraciones, etcetera. También define qué topología de red de neurona debe Hola uso de programa (que es el segundo archivo de hello que necesitamos).</span><span class="sxs-lookup"><span data-stu-id="dae76-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="dae76-176">Para obtener más información acerca de Solver, consulte demasiado[Caffe documentación](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="dae76-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="dae76-177">En este ejemplo, puesto que estamos usando CPU en lugar de GPU, debemos cambiamos Hola última línea:</span><span class="sxs-lookup"><span data-stu-id="dae76-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="dae76-179">Puede cambiar otras líneas si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="dae76-179">You can change other lines as needed.</span></span>

<span data-ttu-id="dae76-180">Hola segundo archivo (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define red neurona de hello el aspecto y la entrada pertinente de Hola y el archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="dae76-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="dae76-181">También es necesario ubicación de datos del entrenamiento de Hola de tooupdate Hola archivo tooreflect.</span><span class="sxs-lookup"><span data-stu-id="dae76-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="dae76-182">Hola de cambio después de la parte en lenet_memory_train_test.prototxt (necesita clúster tooyour específico de toopoint toohello ubicación correcta):</span><span class="sxs-lookup"><span data-stu-id="dae76-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="dae76-183">cambiar file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" demasiado "wasb: / / / proyectos/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="dae76-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="dae76-184">Cambie "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" demasiado "wasb: / / / proyectos/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="dae76-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="dae76-186">Para obtener más información sobre cómo toodefine Hola red, compruebe hello [Caffe documentación en el conjunto de datos MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="dae76-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="dae76-187">A fin de Hola de este blog, simplemente usamos este sencillo ejemplo MNIST.</span><span class="sxs-lookup"><span data-stu-id="dae76-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="dae76-188">Debe ejecutar el comando de Hola por debajo del nodo principal de hello:</span><span class="sxs-lookup"><span data-stu-id="dae76-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="dae76-189">Básicamente se distribuye Hola requerido archivos hilados contenedor tooeach (lenet_memory_solver.prototxt y lenet_memory_train_test.prototxt) y también establece Hola ruta de acceso relevante de cada tooLD_LIBRARY_PATH de controlador/ejecutor Spark, que se define en hello anterior fragmento de código y los puntos de toohello ubicación del código que tenga las bibliotecas de CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="dae76-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="dae76-190">Supervisión y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="dae76-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="dae76-191">Puesto que estamos usando el modo de clúster de hilo, en cuyo caso será controlador de Spark Hola contenedor arbitrario tooan programada (y un nodo de trabajo arbitrario) solo verá en la salida de consola Hola un resultado similar:</span><span class="sxs-lookup"><span data-stu-id="dae76-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="dae76-192">Si desea tooknow ¿qué ha ocurrido, suele ser preciso registro del controlador de tooget Hola Spark, que se proporciona más información.</span><span class="sxs-lookup"><span data-stu-id="dae76-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="dae76-193">En este caso, debe toogo toohello YARN toofind Hola relevante YARN registros de IU.</span><span class="sxs-lookup"><span data-stu-id="dae76-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="dae76-194">Puede obtener Hola UI YARN esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="dae76-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![IU de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="dae76-196">Puede echar un vistazo al número de recursos que se asignan a esta aplicación concreta.</span><span class="sxs-lookup"><span data-stu-id="dae76-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="dae76-197">Puede hacer clic en vínculos de "Programador" hello y, a continuación, verá que para esta aplicación, hay 9 contenedores que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="dae76-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="dae76-198">Pedimos YARN tooprovide 8 ejecutor y otro contenedor es para el proceso de controlador.</span><span class="sxs-lookup"><span data-stu-id="dae76-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![Programador de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="dae76-200">Puede que desee toocheck Hola controlador registros o registros de contenedor si hay errores.</span><span class="sxs-lookup"><span data-stu-id="dae76-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="dae76-201">Para los registros del controlador, puede haga clic en el identificador de la aplicación hello en la interfaz de usuario de YARN y luego haga clic en el botón de "Registros" Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="dae76-202">se escriben los registros de controlador de Hello en stderr.</span><span class="sxs-lookup"><span data-stu-id="dae76-202">hello driver logs are written into stderr.</span></span>

![UI de YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="dae76-204">Por ejemplo, podría ver algunos error Hola por debajo de los registros del controlador hello, que indica que asignar demasiados elementos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dae76-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="dae76-205">En ocasiones, puede producirse problema hello en ejecutor en lugar de controladores.</span><span class="sxs-lookup"><span data-stu-id="dae76-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="dae76-206">En este caso, debe toocheck Hola contenedor registros.</span><span class="sxs-lookup"><span data-stu-id="dae76-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="dae76-207">Puede obtener siempre los registros de contenedor de hello y, a continuación, obtener el contenedor errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="dae76-208">Por ejemplo, este error puede aparecer al ejecutar Caffe.</span><span class="sxs-lookup"><span data-stu-id="dae76-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="dae76-209">En este caso, necesita el identificador del contenedor de tooget hello no se pudo (Hola por encima de caso, es container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="dae76-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="dae76-210">A continuación deberá toorun</span><span class="sxs-lookup"><span data-stu-id="dae76-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="dae76-211">desde el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="dae76-211">from hello headnode.</span></span> <span data-ttu-id="dae76-212">Después de comprobar el error del contenedor, se constata que se debe a que se ha usado el modo GPU (que debe usar el modo de CPU en su lugar) en lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="dae76-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="dae76-213">Obtención de resultados</span><span class="sxs-lookup"><span data-stu-id="dae76-213">Getting results</span></span>

<span data-ttu-id="dae76-214">Puesto que se está asignando 8 ejecutor y topología de red de hello es simple, solo debería tardar unos 30 minutos toorun Hola de resultados.</span><span class="sxs-lookup"><span data-stu-id="dae76-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="dae76-215">Desde la línea de comandos de hello, puede ver que se coloca Hola modelo toowasb:///mnist.model y coloque Hola resultados tooa carpeta denominada wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="dae76-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="dae76-216">Puede obtener resultados de hello mediante la ejecución</span><span class="sxs-lookup"><span data-stu-id="dae76-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="dae76-217">y resultado de hello el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="dae76-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="dae76-218">Hola SampleID representa el identificador hello en el conjunto de datos de hello MNIST y etiqueta de hello es el número de Hola Hola modelo identifica.</span><span class="sxs-lookup"><span data-stu-id="dae76-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="dae76-219">Conclusión</span><span class="sxs-lookup"><span data-stu-id="dae76-219">Conclusion</span></span>

<span data-ttu-id="dae76-220">En esta documentación, que se ha intentado tooinstall CaffeOnSpark con ejecutar un ejemplo sencillo.</span><span class="sxs-lookup"><span data-stu-id="dae76-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="dae76-221">HDInsight es una plataforma de proceso distribuido total administrado en la nube y Hola mejor lugar para ejecutar cargas de trabajo de análisis avanzado y aprendizaje automático en el conjunto de datos grande, y para el aprendizaje profundo distribuido, puede usar Caffe en aprendizaje profundo de HDInsight Spark tooperform tareas.</span><span class="sxs-lookup"><span data-stu-id="dae76-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="dae76-222"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="dae76-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="dae76-223">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="dae76-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="dae76-224">Escenarios</span><span class="sxs-lookup"><span data-stu-id="dae76-224">Scenarios</span></span>
* [<span data-ttu-id="dae76-225">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="dae76-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="dae76-226">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="dae76-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="dae76-227">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="dae76-227">Manage resources</span></span>
* [<span data-ttu-id="dae76-228">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="dae76-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

