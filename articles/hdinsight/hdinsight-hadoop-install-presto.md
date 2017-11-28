---
title: "Instalación de Presto en clústeres de Azure HDInsight basados en Linux | Microsoft Docs"
description: "Aprenda a instalar Presto y Airpal en clústeres de Hadoop para HDInsight basados en Linux mediante acciones de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="78c87-103">Instalación y uso de Presto en clústeres de Hadoop para HDInsight</span><span class="sxs-lookup"><span data-stu-id="78c87-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="78c87-104">En este tema aprenderá a instalar Presto en clústeres de Hadoop para HDInsight con la acción de script.</span><span class="sxs-lookup"><span data-stu-id="78c87-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="78c87-105">También aprenderá a instalar Airpal en un clúster de HDInsight Presto existente.</span><span class="sxs-lookup"><span data-stu-id="78c87-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78c87-106">Los pasos descritos en este documento requieren un **clúster de Hadoop para HDInsight 3.5** que use Linux.</span><span class="sxs-lookup"><span data-stu-id="78c87-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="78c87-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="78c87-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78c87-108">Para más información, consulte las [versiones de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="78c87-109">¿Qué es Presto?</span><span class="sxs-lookup"><span data-stu-id="78c87-109">What is Presto?</span></span>
<span data-ttu-id="78c87-110">[Presto](https://prestodb.io/overview.html) es un motor de consultas SQL de distribución rápida para macrodatos.</span><span class="sxs-lookup"><span data-stu-id="78c87-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="78c87-111">Presto es adecuado para las consultas interactivas de petabytes de datos.</span><span class="sxs-lookup"><span data-stu-id="78c87-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="78c87-112">Para más información sobre los componentes de Presto y cómo funcionan en conjunto, consulte [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst) (Conceptos de Presto).</span><span class="sxs-lookup"><span data-stu-id="78c87-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="78c87-113">Los componentes ofrecidos con HDInsight son totalmente compatibles. Además, el soporte técnico de Microsoft le ayudará a aislar y resolver problemas relacionados con estos componentes.</span><span class="sxs-lookup"><span data-stu-id="78c87-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="78c87-114">Los componentes personalizados, como Presto, reciben un soporte técnico comercialmente razonable para ayudarle a solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="78c87-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="78c87-115">Esto podría resolver el problema o pedirle que forme parte de los canales disponibles para las tecnologías de código abierto donde se encuentra la más amplia experiencia para esa tecnología.</span><span class="sxs-lookup"><span data-stu-id="78c87-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="78c87-116">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="78c87-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="78c87-117">Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="78c87-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="78c87-118">Instalación de Presto con una acción de script</span><span class="sxs-lookup"><span data-stu-id="78c87-118">Install Presto using script action</span></span>

<span data-ttu-id="78c87-119">En esta sección se proporcionan instrucciones sobre cómo usar el script de ejemplo al crear un nuevo clúster mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="78c87-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="78c87-120">Inicie el aprovisionamiento de un clúster siguiendo los pasos que se describen en [Aprovisionamiento de clústeres de HDInsight basados en Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="78c87-121">Asegúrese de crear el clúster con el flujo de creación de clúster **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="78c87-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="78c87-122">Tiene que asegurarse de que el clúster que crea cumple los requisitos siguientes.</span><span class="sxs-lookup"><span data-stu-id="78c87-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="78c87-123">a.</span><span class="sxs-lookup"><span data-stu-id="78c87-123">a.</span></span> <span data-ttu-id="78c87-124">Tiene que ser un clúster Hadoop con HDInsight versión 3.5.</span><span class="sxs-lookup"><span data-stu-id="78c87-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="78c87-125">b.</span><span class="sxs-lookup"><span data-stu-id="78c87-125">b.</span></span> <span data-ttu-id="78c87-126">Tiene que usar Azure Storage como almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="78c87-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="78c87-127">El uso de Presto en un clúster que utiliza Azure Data Lake Store como opción de almacenamiento aún no se admite.</span><span class="sxs-lookup"><span data-stu-id="78c87-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Creación de un clúster de HDInsight usando las opciones personalizadas](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="78c87-129">En la hoja **Configuración opcional**, seleccione **Acciones de script** y proporcione la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="78c87-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="78c87-130">**NOMBRE**: escriba un nombre descriptivo para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="78c87-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="78c87-131">**URI de script de Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="78c87-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="78c87-132">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="78c87-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="78c87-133">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="78c87-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="78c87-134">**ZOOKEEPER**: desactive esta casilla</span><span class="sxs-lookup"><span data-stu-id="78c87-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="78c87-135">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="78c87-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="78c87-136">En la parte inferior de la hoja **Acciones de script**, haga clic en el botón **Seleccionar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="78c87-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="78c87-137">Por último, haga clic en el botón **Seleccionar** situado en la parte inferior de la hoja **Configuración avanzada** para guardar la información de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="78c87-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="78c87-138">Siga aprovisionando el clúster como se describe en [Aprovisionamiento de clústeres de HDInsight basados en Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="78c87-139">También se puede utilizar Azure PowerShell, la CLI de Azure, el SDK de .NET de HDInsight o las plantillas de Azure Resource Manager para aplicar las acciones de script.</span><span class="sxs-lookup"><span data-stu-id="78c87-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="78c87-140">También puede aplicar acciones de script a clústeres que ya se estén ejecutando.</span><span class="sxs-lookup"><span data-stu-id="78c87-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="78c87-141">Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="78c87-142">Uso de Presto con HDInsight</span><span class="sxs-lookup"><span data-stu-id="78c87-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="78c87-143">Realice los pasos siguientes para usar Presto en un clúster de HDInsight después de instalarlo mediante los pasos descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="78c87-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="78c87-144">Conéctese al clúster de HDInsight con SSH:</span><span class="sxs-lookup"><span data-stu-id="78c87-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="78c87-145">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="78c87-146">Inicie el shell de Presto con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="78c87-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="78c87-147">Ejecute una consulta en una tabla de ejemplo, **hivesampletable**, que está disponible en todos los clústeres de HDInsight de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="78c87-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="78c87-148">De forma predeterminada, los conectores [Hive](https://prestodb.io/docs/current/connector/hive.html) y [TPCH](https://prestodb.io/docs/current/connector/tpch.html) para Presto ya están configurados.</span><span class="sxs-lookup"><span data-stu-id="78c87-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="78c87-149">El conector de Hive está configurado para usar la instalación de Hive que se instala de forma predeterminada, de modo que todas las tablas de Hive estarán visibles automáticamente en Presto.</span><span class="sxs-lookup"><span data-stu-id="78c87-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="78c87-150">Para obtener una descripción detallada de cómo puede utilizar Presto, consulte la [documentación de Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="78c87-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="78c87-151">Uso de Airpal con Presto</span><span class="sxs-lookup"><span data-stu-id="78c87-151">Use Airpal with Presto</span></span>

<span data-ttu-id="78c87-152">[Airpal](https://github.com/airbnb/airpal#airpal) es una interfaz de consulta de código abierto basada en web para Presto.</span><span class="sxs-lookup"><span data-stu-id="78c87-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="78c87-153">Para más información sobre Airpal, consulte la [documentación de Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="78c87-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="78c87-154">En esta sección, veremos cómo **instalar Airpal en el nodo perimetral** de un clúster de Hadoop para HDInsight que ya tiene Presto instalado.</span><span class="sxs-lookup"><span data-stu-id="78c87-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="78c87-155">Esto garantiza que la interfaz de consulta web de Airpal está disponible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="78c87-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="78c87-156">Mediante SSH, conéctese al nodo principal del clúster de HDInsight en el que instaló Presto:</span><span class="sxs-lookup"><span data-stu-id="78c87-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="78c87-157">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="78c87-158">Una vez que esté conectado, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="78c87-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="78c87-159">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78c87-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="78c87-160">De esta salida, anote el valor de la propiedad **value**.</span><span class="sxs-lookup"><span data-stu-id="78c87-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="78c87-161">Va a necesitar este valor durante la instalación de Airpal en el nodo perimetral del clúster.</span><span class="sxs-lookup"><span data-stu-id="78c87-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="78c87-162">En la salida anterior, el valor que necesita es **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="78c87-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="78c87-163">Utilice la plantilla **[aquí](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** para crear un modo perimetral del clúster de HDInsight y proporcionar los valores como se muestran en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="78c87-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![Instalación de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="78c87-165">Haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="78c87-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="78c87-166">Una vez que los cambios se aplican a la configuración del clúster, puede tener acceso a la interfaz de web de Airpal siguiendo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="78c87-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="78c87-167">a.</span><span class="sxs-lookup"><span data-stu-id="78c87-167">a.</span></span> <span data-ttu-id="78c87-168">En la hoja del clúster, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78c87-168">From the cluster blade, click **Applications**.</span></span>

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="78c87-170">b.</span><span class="sxs-lookup"><span data-stu-id="78c87-170">b.</span></span> <span data-ttu-id="78c87-171">Desde la hoja **Aplicaciones instaladas**, haga clic en **Portal** en Airpal.</span><span class="sxs-lookup"><span data-stu-id="78c87-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="78c87-173">c.</span><span class="sxs-lookup"><span data-stu-id="78c87-173">c.</span></span> <span data-ttu-id="78c87-174">Cuando se le solicite, escriba las credenciales de administrador que especificó al crear el clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78c87-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="78c87-175">Personalización de una instalación de Presto en un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="78c87-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="78c87-176">Una vez haya instalado Presto en un clúster de Hadoop en HDInsight, puede personalizar la instalación para realizar cambios, como actualizar la configuración de memoria, cambiar los conectores, etc. Para ello, siga los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="78c87-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="78c87-177">Mediante SSH, conéctese al nodo principal del clúster de HDInsight en el que instaló Presto:</span><span class="sxs-lookup"><span data-stu-id="78c87-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="78c87-178">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="78c87-179">Realice los cambios de configuración en el archivo `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="78c87-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="78c87-180">Para más información sobre la configuración de presto, consulte [Presto Configuration Options for YARN-Based Clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Opciones de configuración de Presto para clústeres basados en YARN).</span><span class="sxs-lookup"><span data-stu-id="78c87-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="78c87-181">Detenga y termine la instancia de ejecución actual de presto.</span><span class="sxs-lookup"><span data-stu-id="78c87-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="78c87-182">Inicie una nueva instancia de Presto con la personalización.</span><span class="sxs-lookup"><span data-stu-id="78c87-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="78c87-183">Espere a que la nueva instancia esté lista y anote la dirección del coordinador de Presto.</span><span class="sxs-lookup"><span data-stu-id="78c87-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="78c87-184">Generación de datos de pruebas comparativas para clústeres de HDInsight que ejecutan Presto</span><span class="sxs-lookup"><span data-stu-id="78c87-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="78c87-185">TPC-DS es el estándar del sector para medir el rendimiento de muchos sistemas de ayuda a la toma de decisiones, incluidos los sistemas de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="78c87-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="78c87-186">Puede usar Presto en clústeres de HDInsight para generar datos y evaluar cómo se compara con sus propios datos de prueba comparativa de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78c87-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="78c87-187">Para más información, consulte [esta página](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="78c87-188">Consulte también</span><span class="sxs-lookup"><span data-stu-id="78c87-188">See also</span></span>
* <span data-ttu-id="78c87-189">[Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="78c87-190">Hue es una interfaz de usuario web que simplifica la creación, la ejecución y el guardado de trabajos de Pig y Hive, así como el examen del almacenamiento predeterminado de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78c87-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="78c87-191">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="78c87-192">Use la personalización del clúster para instalar Giraph en clústeres de Hadoop para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78c87-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="78c87-193">Giraph permite realizar un procesamiento gráfico mediante Hadoop, y se puede usar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="78c87-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="78c87-194">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="78c87-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="78c87-195">Use la personalización del clúster para instalar Solr en clústeres de Hadoop para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78c87-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="78c87-196">Solr le permite realizar potentes operaciones de búsqueda en los datos almacenados.</span><span class="sxs-lookup"><span data-stu-id="78c87-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
