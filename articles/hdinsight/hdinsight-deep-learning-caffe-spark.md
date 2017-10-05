---
title: Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido | Microsoft Docs
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
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="4f9c9-103">Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido</span><span class="sxs-lookup"><span data-stu-id="4f9c9-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="4f9c9-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="4f9c9-104">Introduction</span></span>

<span data-ttu-id="4f9c9-105">El aprendizaje profundo afecta a muchos sectores empresariales, desde la atención sanitaria, al transporte o a la fabricación, entre otros.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="4f9c9-106">Las empresas empiezan a usar el aprendizaje profundo para solucionar problemas difíciles, como la [clasificación de imágenes](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), el [reconocimiento de voz](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), el reconocimiento de objetos y la traducción automática.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="4f9c9-107">Hay [muchos marcos populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), entre los que se incluyen [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe es uno de los marcos de redes neuronales no simbólicos más conocidos y se usa ampliamente en muchas áreas, entre las que se incluye la visión de equipos.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="4f9c9-108">Además, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina Caffe con Apache Spark, en cuyo caso el aprendizaje profundo se puede usar fácilmente en un clúster existente de Hadoop junto con las canalizaciones ETL de Spark, lo que reduce la complejidad y latencia del sistema para el aprendizaje de un extremo al otro.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="4f9c9-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) es la única oferta de Hadoop en la nube totalmente administrada que proporciona clústeres de análisis de código abierto optimizados para Spark, Hive, MapReduce, HBase, Storm, Kafka y R Server, con el respaldo de un acuerdo de nivel de servicio del 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="4f9c9-110">Cada una de estas tecnologías de macrodatos, así como las aplicaciones de fabricantes de software independientes, se pueden implementar fácilmente como clústeres administrados, con seguridad y supervisión de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="4f9c9-111">Algunos usuarios preguntan cómo se usa el aprendizaje profundo en HDInsight, que es el producto de PaaS Hadoop de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="4f9c9-112">En el futuro podremos compartir más información, pero ahora queremos resumir un blog técnico sobre cómo usar Caffe en HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="4f9c9-113">Si ha instalado Caffe con anterioridad, observará que la instalación de este marco es un poco complicada.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="4f9c9-114">En este blog, primero se ilustrará cómo instalar [Caffe en Spark](https://github.com/yahoo/CaffeOnSpark) para un clúster de HDInsight y, después, se usará la demostración de MNIST integrada para mostrar cómo utilizar el aprendizaje profundo distribuido mediante HDInsight Spark en las CPU.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="4f9c9-115">Hay cuatro pasos principales para que funcione en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="4f9c9-116">Instalar las dependencias necesarias en todos los nodos</span><span class="sxs-lookup"><span data-stu-id="4f9c9-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="4f9c9-117">Compilar Caffe en Spark para HDInsight en el nodo principal</span><span class="sxs-lookup"><span data-stu-id="4f9c9-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="4f9c9-118">Distribuir las bibliotecas requeridas a todos los nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="4f9c9-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="4f9c9-119">Componer un modelo de Caffe y ejecutarlo de forma distribuida</span><span class="sxs-lookup"><span data-stu-id="4f9c9-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="4f9c9-120">Dado que HDInsight es una solución de PaaS, ofrece unas características de plataforma excelentes (por lo que es bastante fácil realizar algunas tareas).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="4f9c9-121">Una de estas características que se usa mucho en esta entrada de blog se llama [Acción de scripts](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) y con ella puede ejecutar comandos de shell para personalizar nodos de clúster (nodo principal, nodo de trabajo o nodo perimetral).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="4f9c9-122">Paso 1: Instalar las dependencias requeridas en todos los nodos</span><span class="sxs-lookup"><span data-stu-id="4f9c9-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="4f9c9-123">Para empezar, es preciso instalar las dependencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="4f9c9-124">El sitio de Caffe y el [sitio de CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) ofrecen información muy útil para instalar las dependencias para Spark en modo YARN (que es el modo de HDInsight Spark), pero es preciso agregar más dependencias para la plataforma HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="4f9c9-125">Se usará la acción de script como se indica a continuación y se ejecutará en todos los nodos principales y nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="4f9c9-126">Esta acción de script tardará aproximadamente 20 minutos en realizarse, ya que dichas dependencias a su vez dependen de otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="4f9c9-127">Debe colocarla en alguna ubicación a la que pueda acceder el clúster de HDInsight, como una ubicación de GitHub o la cuenta de Blob Storage predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

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


<span data-ttu-id="4f9c9-128">La acción de script anterior tiene dos pasos.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-128">There are two steps in the script action above.</span></span> <span data-ttu-id="4f9c9-129">En el primero se instalan todas las bibliotecas requeridas.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="4f9c9-130">Aquí se incluyen todas las bibliotecas necesarias tanto para compilar Caffe (por ejemplo, gflags, glog) como para ejecuta Caffe (por ejemplo, numpy).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="4f9c9-131">Vamos a usar libatlas para optimizar la CPU, pero puede seguir el wiki de CaffeOnSpark acerca de cómo instalar otras bibliotecas de optimización, como MKL o CUDA (para GPU).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="4f9c9-132">El segundo paso es descargar, compilar e instalar protobuf 2.5.0 para Caffe durante el runtime.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="4f9c9-133">Protobuf 2.5.0 [es obligatorio](https://github.com/yahoo/CaffeOnSpark/issues/87); sin embargo, esta versión no está disponible como paquete en Ubuntu 16, por lo que es preciso compilarlo del código fuente.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="4f9c9-134">En Internet también hay varios recursos que indican cómo compilarlo, como [este](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="4f9c9-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="4f9c9-135">Para empezar, puede ejecutar esta acción de script en el clúster para todos los nodos de trabajo y los nodos principales (para HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="4f9c9-136">Las acciones de script se pueden ejecutar para un clúster en ejecución o durante su tiempo de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="4f9c9-137">Para más información acerca de las acciones de script, consulte la documentación [aquí](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="4f9c9-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Acciones de script para instalar dependencias](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="4f9c9-139">Paso 2: Compilar Caffe en Spark para HDInsight en el nodo principal</span><span class="sxs-lookup"><span data-stu-id="4f9c9-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="4f9c9-140">El segundo paso es compilar Caffe en el nodo principal y, después, distribuir las bibliotecas compiladas a todos los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="4f9c9-141">En este paso, será preciso que use [ssh en el nodo principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y, después, realizar el [proceso de compilación de CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn); a continuación, se muestra el script que puede usar para compilar CaffeOnSpark con varios pasos adicionales.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="4f9c9-142">Es posible que tenga que realizar más operaciones de las que se indican en la documentación de CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="4f9c9-143">Los cambios son:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-143">The changes are:</span></span>
- <span data-ttu-id="4f9c9-144">Cambie a solo la CPU solo y utilice libatlas para este fin concreto.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="4f9c9-145">Coloque los conjuntos de datos en Blob Storage, que es una ubicación compartida a la que pueden acceder todos los nodos de trabajo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="4f9c9-146">Coloque las bibliotecas de Caffe compiladas en Blob Storage. Más adelante copiará dichas bibliotecas a todos los nodos mediante acciones de script para que el tiempo de compilación sea el menor posible.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="4f9c9-147">Solución de problemas: An Ant BuildException has occured: exec returned: 2</span><span class="sxs-lookup"><span data-stu-id="4f9c9-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="4f9c9-148">La primera vez que se intenta realizar la compilación de CaffeOnSpark, a veces puede aparecer el siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="4f9c9-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="4f9c9-149">No tiene más que limpiar el repositorio de código con "make clean" y, después, ejecutar "make build" para resolver este problema, siempre que tenga las dependencias correctas.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="4f9c9-150">Solución de problemas: se ha superado el tiempo de espera de la conexión con el repositorio de Maven</span><span class="sxs-lookup"><span data-stu-id="4f9c9-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="4f9c9-151">A veces Maven genera un error de tiempo de espera de la conexión similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="4f9c9-152">El error se solucionar esperando unos minutos e intentando volver a generar el código, por lo que es posible que Maven limite, en cierto modo, el tráfico de una dirección IP determinada.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="4f9c9-153">Solución de problemas: error en las pruebas de Caffe</span><span class="sxs-lookup"><span data-stu-id="4f9c9-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="4f9c9-154">Al hacer la comprobación final en CaffeOnSpark, es probable que vea un error en la prueba similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="4f9c9-155">Es probable que tenga que ver con la codificación UTF-8, pero no debería afectar al uso de Caffe</span><span class="sxs-lookup"><span data-stu-id="4f9c9-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="4f9c9-156">Paso 3: Distribuir las bibliotecas requeridas a todos los nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="4f9c9-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="4f9c9-157">El paso siguiente consiste en distribuir las bibliotecas (básicamente, las bibliotecas de CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) a todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="4f9c9-158">En el paso 2, dichas bibliotecas se colocaron en Blob Storage y, en este paso, se usarán acciones de script para copiarlas en todos los nodos principales y los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="4f9c9-159">Para ello, ejecute una acción de script como la siguiente (es preciso apuntar a la ubicación específica del clúster):</span><span class="sxs-lookup"><span data-stu-id="4f9c9-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="4f9c9-160">Dado que en el paso 2 se colocaron en Blob Storage, al que pueden acceder todos los nodos, en este paso se simplemente se copian en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="4f9c9-161">Paso 4: Componer un modelo de Caffe y ejecutarlo de forma distribuida</span><span class="sxs-lookup"><span data-stu-id="4f9c9-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="4f9c9-162">Después de ejecutar los pasos anteriores, Caffe ya está instalado en el nodo principal y se puede continuar.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="4f9c9-163">El siguiente paso es escribir un modelo de Caffe.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="4f9c9-164">Caffe usa una "arquitectura expresiva", donde para crear un modelo, solo es preciso definir un archivo de configuración, no hace falta escribir código (en la mayoría de los casos).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="4f9c9-165">Vamos a examinar dicha arquitectura.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-165">So let's take a look there.</span></span> 

<span data-ttu-id="4f9c9-166">El modelo que vamos a entrenar hoy es un modelo de ejemplo para el entrenamiento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="4f9c9-167">La base de datos MNIST de dígitos manuscritos tiene un conjunto de entrenamiento de 60 000 ejemplos y un conjunto de pruebas de 10 000 ejemplos.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="4f9c9-168">Es un subconjunto de un conjunto mayor disponible en NIST.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="4f9c9-169">Los dígitos tienen un tamaño normalizado y están centrados en una imagen de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="4f9c9-170">CaffeOnSpark tiene algunos scripts para descargar el conjunto de datos y convertirlos al formato correcto.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="4f9c9-171">CaffeOnSpark proporciona algunos ejemplos de topologías de red para el entrenamiento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="4f9c9-172">Su diseño divide la arquitectura de red (la topología de la red) y la optimiza.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="4f9c9-173">En este caso, se requieren dos archivos:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="4f9c9-174">el archivo "Solver" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) se usa para supervisar la optimización y generar actualizaciones de parámetros.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="4f9c9-175">Por ejemplo, define si se van a usar la CPU o la GPU, cuál es el momento, cuántas iteraciones habrá, etc. También define qué topología de red neuronal debe utilizar el programa (que es el segundo archivo que se necesita).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="4f9c9-176">Para más información acerca de Solver, consulte la [documentación de Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="4f9c9-177">En este ejemplo, dado que se va a usar la CPU, en lugar de la GPU, es preciso cambiar la última línea a:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="4f9c9-179">Puede cambiar otras líneas si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-179">You can change other lines as needed.</span></span>

<span data-ttu-id="4f9c9-180">El segundo archivo (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define el aspecto de la red neuronal y el archivo de entrada y salida relevante.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="4f9c9-181">También es preciso actualizar el archivo para que refleje la ubicación de los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="4f9c9-182">Cambie la siguiente parte en lenet_memory_train_test.prototxt (es preciso apuntar a la ubicación correcta específica del clúster):</span><span class="sxs-lookup"><span data-stu-id="4f9c9-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="4f9c9-183">cambie "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" a "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="4f9c9-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="4f9c9-184">cambie "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" a "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="4f9c9-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configuración de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="4f9c9-186">Para más información acerca de cómo definir la red, consulte la [documentación de Caffe en el conjunto de datos MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="4f9c9-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="4f9c9-187">En este blog, solo se usará este sencillo ejemplo de MNIST.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="4f9c9-188">Debe ejecutar el comando siguiente desde el nodo principal:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="4f9c9-189">Básicamente distribuye los archivos requeridos (lenet_memory_solver.prototxt y lenet_memory_train_test.prototxt) a cada contenedor YARN y establece la variable PATH de cada controlador o ejecutor de Spark en LD_LIBRARY_PATH, que se define en el fragmento de código anterior y apunta a la ubicación que tenga bibliotecas de CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="4f9c9-190">Supervisión y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="4f9c9-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="4f9c9-191">Dado que usamos el modo de clúster YARN, en cuyo caso el controlador Spark se programará para un contenedor arbitrario (y un nodo de trabajo arbitrario) en la consola solo se debería ver algo como esto:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="4f9c9-192">Si desea saber lo que ha ocurrido, lo habitual es que tenga que acceder al registro del controlador de Spark, que proporciona más información.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="4f9c9-193">En este caso, es preciso que vaya a la interfaz de usuario de YARN para buscar los registros de YARN relevantes.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="4f9c9-194">Para acceder a la interfaz de usuario de YARN, use esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![IU de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="4f9c9-196">Puede echar un vistazo al número de recursos que se asignan a esta aplicación concreta.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="4f9c9-197">Puede hacer clic en el vínculo "Scheduler" (Programador) y vera que en la aplicación hay nueve contenedores en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="4f9c9-198">Pedimos a YARN que proporcione ocho ejecutores, mientras que el otro contenedor es para el proceso del controlador.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![Programador de YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="4f9c9-200">Si aparecen errores, se pueden comprobar los registros del controlador o los registros del contenedor.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="4f9c9-201">En el caso de los registros del controlador, puede haga clic en el identificador de la aplicación en la interfaz de usuario de YARN y, después, hacer clic en el botón "Logs" (Registros).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="4f9c9-202">Los registros de controlador se escriben en stderr.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-202">The driver logs are written into stderr.</span></span>

![UI de YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="4f9c9-204">Por ejemplo, a continuación puede ver una parte del error de los registros de controlador, que indica que se asignan demasiados ejecutores.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="4f9c9-205">A veces, el problema puede darse en los ejecutores, en lugar de en los controladores.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="4f9c9-206">En este caso, es preciso comprobar los registros del contenedor.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="4f9c9-207">Siempre puede acceder a los registros del contenedor y, después, al contenedor con el error.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="4f9c9-208">Por ejemplo, este error puede aparecer al ejecutar Caffe.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="4f9c9-209">En ese caso, es preciso obtener el identificador del contenedor con error (en este caso es container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="4f9c9-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="4f9c9-210">Luego, tiene que ejecutar</span><span class="sxs-lookup"><span data-stu-id="4f9c9-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="4f9c9-211">desde el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-211">from the headnode.</span></span> <span data-ttu-id="4f9c9-212">Después de comprobar el error del contenedor, se constata que se debe a que se ha usado el modo GPU (que debe usar el modo de CPU en su lugar) en lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="4f9c9-213">Obtención de resultados</span><span class="sxs-lookup"><span data-stu-id="4f9c9-213">Getting results</span></span>

<span data-ttu-id="4f9c9-214">Dado que se asignan ocho ejecutores y que la topología de red es sencilla, el resultado no debería tardar más de 30 minutos en aparecer.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="4f9c9-215">En la línea de comandos, puede ver que el modelo se ha colocado en wasb:///mnist.model y los resultados en una carpeta llamada wasb: ///mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="4f9c9-216">Para obtener los resultados, ejecute</span><span class="sxs-lookup"><span data-stu-id="4f9c9-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="4f9c9-217">y obtendrá un resultado como este:</span><span class="sxs-lookup"><span data-stu-id="4f9c9-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="4f9c9-218">SampleID representa el identificador del conjunto de datos de MNIST y "label" es el número que identifica el modelo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="4f9c9-219">Conclusión</span><span class="sxs-lookup"><span data-stu-id="4f9c9-219">Conclusion</span></span>

<span data-ttu-id="4f9c9-220">En esta documentación, se ha intentado instalar CaffeOnSpark mediante la ejecución de un ejemplo sencillo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="4f9c9-221">HDInsight es una plataforma de proceso distribuido en la nube totalmente administrada y es el mejor lugar para ejecutar cargas de trabajo de análisis avanzado y aprendizaje automático en conjuntos de datos grandes, mientras que para el aprendizaje profundo distribuido puede usar Caffe en HDInsight Spark para realizar tareas de aprendizaje profundo.</span><span class="sxs-lookup"><span data-stu-id="4f9c9-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="4f9c9-222"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4f9c9-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4f9c9-223">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4f9c9-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4f9c9-224">Escenarios</span><span class="sxs-lookup"><span data-stu-id="4f9c9-224">Scenarios</span></span>
* [<span data-ttu-id="4f9c9-225">Spark con Aprendizaje automático: uso de Spark en HDInsight para analizar la temperatura de edificios con los de datos del sistema de acondicionamiento de aire</span><span class="sxs-lookup"><span data-stu-id="4f9c9-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4f9c9-226">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="4f9c9-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="4f9c9-227">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="4f9c9-227">Manage resources</span></span>
* [<span data-ttu-id="4f9c9-228">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4f9c9-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

