---
title: "Instalación de cuadernos de Jupyter Notebook localmente y conexión a un clúster de Azure HDInsight Spark | Microsoft Docs"
description: "Descubra cómo instalar un cuaderno de Jupyter Notebook en el equipo de forma local y cómo conectarse a un clúster de Apache Spark en Azure HDInsight."
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="2a325-103">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="2a325-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="2a325-104">En este artículo obtendrá información sobre cómo instalar un cuaderno de Jupyter Notebook con PySpark personalizado (para Python) y los kernels de Spark (para Scala) con la Sparkmagic, y conecte el cuaderno a un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a325-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="2a325-105">Puede haber varias razones para instalar Jupyter en el equipo local y también algunos desafíos.</span><span class="sxs-lookup"><span data-stu-id="2a325-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="2a325-106">Para obtener más información sobre esto, consulte la sección [¿Por qué debo instalar Jupyter en mi equipo?](#why-should-i-install-jupyter-on-my-computer) al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2a325-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="2a325-107">Existen tres pasos principales en la instalación de Jupyter y Sparkmagic en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2a325-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="2a325-108">Instalación de cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="2a325-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="2a325-109">Instalación de los kernels de PySpark y Spark con Sparkmagic</span><span class="sxs-lookup"><span data-stu-id="2a325-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="2a325-110">Configuración de Sparkmagic para acceder al clúster de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a325-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="2a325-111">Para más información acerca de los kernels personalizados y Sparkmagic disponibles para cuadernos de Jupyter Notebook con el clúster de HDInsight, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="2a325-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a325-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a325-112">Prerequisites</span></span>
<span data-ttu-id="2a325-113">Los requisitos previos descritos aquí no se aplican a la instalación de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2a325-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="2a325-114">Se facilitan para conectar el cuaderno de Jupyter Notebook con un clúster de HDInsight, una vez instalado el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="2a325-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="2a325-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a325-115">An Azure subscription.</span></span> <span data-ttu-id="2a325-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2a325-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2a325-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a325-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2a325-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2a325-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="2a325-119">Instalación de cuadernos de Jupyter Notebook en el equipo</span><span class="sxs-lookup"><span data-stu-id="2a325-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="2a325-120">Debe instalar Python para poder instalar cuadernos de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="2a325-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="2a325-121">Python y Jupyter están disponibles como parte de la [distribución Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="2a325-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="2a325-122">Al instalar Anaconda, instalará una distribución de Python.</span><span class="sxs-lookup"><span data-stu-id="2a325-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="2a325-123">Una vez se haya instalado Anaconda, agregue la instalación de Jupyter ejecutando comandos adecuados.</span><span class="sxs-lookup"><span data-stu-id="2a325-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="2a325-124">Descargue el [instalador de Anaconda](https://www.continuum.io/downloads) para su plataforma y ejecute el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="2a325-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="2a325-125">Durante la ejecución del Asistente para instalación, asegúrese de seleccionar la opción para agregar Anaconda a la variable PATH.</span><span class="sxs-lookup"><span data-stu-id="2a325-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="2a325-126">Ejecute el siguiente comando para instalar Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2a325-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="2a325-127">Para más información sobre la instalación de Jupyter, consulte [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Instalación de Jupyter con Anaconda).</span><span class="sxs-lookup"><span data-stu-id="2a325-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="2a325-128">Instalación de kernels y Sparkmagic</span><span class="sxs-lookup"><span data-stu-id="2a325-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="2a325-129">Para instrucciones sobre cómo instalar los kernels de PySpark y Spark, además de Sparkmagic, siga las instrucciones de instalación en la [documentación de sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a325-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="2a325-130">El primer paso en la documentación de Sparkmagic es la instalación.</span><span class="sxs-lookup"><span data-stu-id="2a325-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="2a325-131">Reemplace el primer paso del vínculo por los comandos siguientes, dependiendo de la versión del clúster de HDInsight al que se vaya a conectar.</span><span class="sxs-lookup"><span data-stu-id="2a325-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="2a325-132">A continuación, siga los pasos restantes en la documentación de Sparkmagic.</span><span class="sxs-lookup"><span data-stu-id="2a325-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="2a325-133">Si desea instalar kernels diferentes, debe realizar el paso 3 de la sección de instrucciones de instalación de Sparkmagic.</span><span class="sxs-lookup"><span data-stu-id="2a325-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="2a325-134">Para los clústeres 3.4, instale sparkmagic 0.2.3 ejecutando `pip install sparkmagic==0.2.3`.</span><span class="sxs-lookup"><span data-stu-id="2a325-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="2a325-135">Para los clústeres 3.5 y 3.6, instale sparkmagic 0.11.2 ejecutando `pip install sparkmagic==0.11.2`.</span><span class="sxs-lookup"><span data-stu-id="2a325-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="2a325-136">Configuración de Sparkmagic para acceder al clúster de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a325-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="2a325-137">En esta sección, configurará el conjunto de Sparkmagic que instaló anteriormente para conectarse a un clúster de Apache Spark que debe haber creado ya en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a325-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="2a325-138">Normalmente, la información de configuración de Jupyter se almacena en el directorio principal de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="2a325-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="2a325-139">Para localizar el directorio principal en cualquier plataforma de sistema operativo, escriba los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="2a325-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="2a325-140">Inicie el shell de Python.</span><span class="sxs-lookup"><span data-stu-id="2a325-140">Start the Python shell.</span></span> <span data-ttu-id="2a325-141">En una ventana de línea de comandos, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a325-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="2a325-142">En el shell de Python, escriba el siguiente comando para localizar el directorio principal.</span><span class="sxs-lookup"><span data-stu-id="2a325-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="2a325-143">Navegue hasta el directorio principal y cree una carpeta denominada **.sparkmagic** si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="2a325-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="2a325-144">Dentro de la carpeta, cree un archivo llamado **config.json** y agregue el siguiente fragmento de código JSON en él.</span><span class="sxs-lookup"><span data-stu-id="2a325-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="2a325-145">Sustituya **{USERNAME}**, **{CLUSTERDNSNAME}** y **{BASE64ENCODEDPASSWORD}** por los valores que correspondan.</span><span class="sxs-lookup"><span data-stu-id="2a325-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="2a325-146">Puede usar una serie de utilidades en su lenguaje de programación preferido o en línea para generar una contraseña codificada en base64 de su contraseña real.</span><span class="sxs-lookup"><span data-stu-id="2a325-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="2a325-147">Ajuste la configuración de latido adecuada en `config.json`:</span><span class="sxs-lookup"><span data-stu-id="2a325-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="2a325-148">Debe agregar estos parámetros de configuración en el mismo nivel que los fragmentos de código `kernel_python_credentials` y `kernel_scala_credentials` agregados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a325-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="2a325-149">Para ver un ejemplo sobre cómo y dónde agregar la configuración de latido, vea este [archivo config.json de ejemplo](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="2a325-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="2a325-150">Para `sparkmagic 0.2.3` (clústeres 3.4):</span><span class="sxs-lookup"><span data-stu-id="2a325-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="2a325-151">Para `sparkmagic 0.11.2` (clústeres v3.5 y v3.6), incluyen:</span><span class="sxs-lookup"><span data-stu-id="2a325-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="2a325-152">Los latidos se envían para garantizar que no se pierdan sesiones.</span><span class="sxs-lookup"><span data-stu-id="2a325-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="2a325-153">Cuando un equipo entra en modo de suspensión o se apaga, no se enviará el latido, con lo que se la sesión se limpia.</span><span class="sxs-lookup"><span data-stu-id="2a325-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="2a325-154">Para los clústeres 3.4, si desea deshabilitar este comportamiento, puede establecer la configuración de Livio `livy.server.interactive.heartbeat.timeout` a `0` en la interfaz de usuario de Ambari.</span><span class="sxs-lookup"><span data-stu-id="2a325-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="2a325-155">Para los clústeres 3.5, si no establece la configuración de 3.5 anterior, no se eliminará la sesión.</span><span class="sxs-lookup"><span data-stu-id="2a325-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="2a325-156">Reinicie Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2a325-156">Start Jupyter.</span></span> <span data-ttu-id="2a325-157">En la ventana del símbolo del sistema, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="2a325-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="2a325-158">Compruebe que puede conectarse al clúster con el cuaderno de Jupyter Notebook y que puede usar el conjunto Sparkmagic disponible con los kernels.</span><span class="sxs-lookup"><span data-stu-id="2a325-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="2a325-159">Lleve a cabo los siguiente pasos.</span><span class="sxs-lookup"><span data-stu-id="2a325-159">Perform the following steps.</span></span>

    <span data-ttu-id="2a325-160">a.</span><span class="sxs-lookup"><span data-stu-id="2a325-160">a.</span></span> <span data-ttu-id="2a325-161">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="2a325-161">Create a new notebook.</span></span> <span data-ttu-id="2a325-162">En la esquina de la derecha, haga clic en **New**(Nuevo).</span><span class="sxs-lookup"><span data-stu-id="2a325-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="2a325-163">Debería ver el kernel **Python2** predeterminado y los dos nuevos kernels que instaló, **PySpark** y **Spark**.</span><span class="sxs-lookup"><span data-stu-id="2a325-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="2a325-164">Haga clic en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="2a325-164">Click **PySpark**.</span></span>

    <span data-ttu-id="2a325-165">![Kernels de cuadernos de Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels de cuadernos de Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="2a325-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="2a325-166">b.</span><span class="sxs-lookup"><span data-stu-id="2a325-166">b.</span></span> <span data-ttu-id="2a325-167">Ejecute el siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="2a325-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="2a325-168">Si puede recuperar correctamente el resultado, se comprobará la conexión al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a325-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="2a325-169">Si desea actualizar la configuración del cuaderno para conectarse a un clúster distinto, actualice el archivo config.json con el nuevo conjunto de valores como se muestra en el paso 3 anterior.</span><span class="sxs-lookup"><span data-stu-id="2a325-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="2a325-170">¿Por qué debo instalar Jupyter en mi equipo?</span><span class="sxs-lookup"><span data-stu-id="2a325-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="2a325-171">Puede haber varios motivos por los que podría querer instalar Jupyter en el equipo y, a continuación, conectarlo a un clúster de Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a325-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="2a325-172">Aunque los cuadernos de Jupyter Notebook ya están disponibles en el clúster de Spark en HDInsight de Azure, la instalación de Jupyter en el equipo ofrece la opción de crear cuadernos de forma local, probar la aplicación en un clúster en ejecución y cargar los cuadernos en el clúster.</span><span class="sxs-lookup"><span data-stu-id="2a325-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="2a325-173">Para cargar los cuadernos en el clúster, puede hacerlo mediante el cuaderno de Jupyter Notebook en ejecución o el clúster, o bien guardarlos en la carpeta /HdiNotebooks de la cuenta de almacenamiento asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="2a325-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="2a325-174">Para obtener más información sobre cómo se almacenan los cuadernos en el clúster, consulte la sección [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)? (Almacenamiento de los cuadernos de Jupyter Notebook).</span><span class="sxs-lookup"><span data-stu-id="2a325-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="2a325-175">Con los cuadernos disponibles localmente, puede conectarse a diferentes clústeres de Spark según los requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a325-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="2a325-176">Puede usar GitHub para implementar un sistema de control de código fuente y tener el control de las versiones de los cuadernos.</span><span class="sxs-lookup"><span data-stu-id="2a325-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="2a325-177">También puede tener un entorno de colaboración donde varios usuarios pueden trabajar con el mismo cuaderno.</span><span class="sxs-lookup"><span data-stu-id="2a325-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="2a325-178">Puede trabajar con cuadernos localmente sin necesidad de un clúster activo.</span><span class="sxs-lookup"><span data-stu-id="2a325-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="2a325-179">Solo necesita un clúster para probar los cuadernos, no para administrar manualmente los cuadernos o un entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="2a325-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="2a325-180">Puede resultar más fácil configurar su propio entorno de desarrollo local que configurar la instalación de Jupyter en el clúster.</span><span class="sxs-lookup"><span data-stu-id="2a325-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="2a325-181">Puede aprovechar todo el software que haya instalado localmente sin configurar uno o más clústeres remotos.</span><span class="sxs-lookup"><span data-stu-id="2a325-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="2a325-182">Con Jupyter instalado en el equipo local, varios usuarios pueden ejecutar el mismo cuaderno en el mismo clúster de Spark al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="2a325-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="2a325-183">En tal situación, se crean varias sesiones de Livy.</span><span class="sxs-lookup"><span data-stu-id="2a325-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="2a325-184">Si surge un problema y desea depurarlo, es una tarea compleja realizar el seguimiento de a qué sesión de Livy pertenece cada usuario.</span><span class="sxs-lookup"><span data-stu-id="2a325-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="2a325-185"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2a325-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="2a325-186">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="2a325-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="2a325-187">Escenarios</span><span class="sxs-lookup"><span data-stu-id="2a325-187">Scenarios</span></span>
* [<span data-ttu-id="2a325-188">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="2a325-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2a325-189">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="2a325-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2a325-190">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="2a325-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2a325-191">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="2a325-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="2a325-192">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a325-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2a325-193">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2a325-193">Create and run applications</span></span>
* [<span data-ttu-id="2a325-194">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="2a325-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2a325-195">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="2a325-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2a325-196">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="2a325-196">Tools and extensions</span></span>
* [<span data-ttu-id="2a325-197">Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="2a325-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2a325-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="2a325-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2a325-199">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a325-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2a325-200">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a325-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2a325-201">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="2a325-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="2a325-202">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="2a325-202">Manage resources</span></span>
* [<span data-ttu-id="2a325-203">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="2a325-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2a325-204">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="2a325-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
