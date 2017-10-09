---
title: "clústeres de aaaInstall eso es todo en HDInsight Linux de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall ya está preparado y Airpal en Hadoop de HDInsight basados en Linux clústeres mediante acciones de Script."
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
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="4a4f6-103">Instalación y uso de Presto en clústeres de Hadoop para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a4f6-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="4a4f6-104">En este tema, aprenderá cómo tooinstall eso es todo en Hadoop de HDInsight clústeres mediante la acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="4a4f6-105">También aprenderá cómo tooinstall Airpal en un clúster de HDInsight Presto existente.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a4f6-106">Hello pasos en este documento, es necesario un **clúster de Hadoop de HDInsight 3.5** que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="4a4f6-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4a4f6-108">Para más información, consulte las [versiones de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="4a4f6-109">¿Qué es Presto?</span><span class="sxs-lookup"><span data-stu-id="4a4f6-109">What is Presto?</span></span>
<span data-ttu-id="4a4f6-110">[Presto](https://prestodb.io/overview.html) es un motor de consultas SQL de distribución rápida para macrodatos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="4a4f6-111">Presto es adecuado para las consultas interactivas de petabytes de datos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="4a4f6-112">Para obtener más información sobre componentes de Hola de ya está preparado y cómo funcionan juntos, consulte [conceptos listo](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="4a4f6-113">Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="4a4f6-114">Componentes personalizados, por ejemplo, eso es todo, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="4a4f6-115">Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="4a4f6-116">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="4a4f6-117">Instalación de Presto con una acción de script</span><span class="sxs-lookup"><span data-stu-id="4a4f6-117">Install Presto using script action</span></span>

<span data-ttu-id="4a4f6-118">Esta sección proporciona instrucciones sobre cómo el script de ejemplo de Hola toouse al crear un nuevo clúster mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="4a4f6-119">Iniciar el aprovisionamiento de un clúster mediante el uso de pasos de hello en [clústeres de HDInsight basados en Linux aprovisionar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="4a4f6-120">Asegúrese de crear el clúster hello mediante hello **personalizado** flujo de creación de clúster.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="4a4f6-121">Debe asegurarse de ese clúster Hola que creas cumple Hola según los requisitos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="4a4f6-122">a.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-122">a.</span></span> <span data-ttu-id="4a4f6-123">Tiene que ser un clúster Hadoop con HDInsight versión 3.5.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="4a4f6-124">b.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-124">b.</span></span> <span data-ttu-id="4a4f6-125">Almacenamiento de Azure, debe usar como almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="4a4f6-126">Aún no se admite el uso de Presto en un clúster que utiliza el almacén de Azure Data Lake como opción de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Creación de un clúster de HDInsight usando las opciones personalizadas](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="4a4f6-128">En hello **configuración avanzada** hoja, seleccione **acciones de Script**y proporcionar información de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="4a4f6-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="4a4f6-129">**NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="4a4f6-130">**URI de script de Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="4a4f6-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="4a4f6-131">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="4a4f6-132">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="4a4f6-133">**ZOOKEEPER**: desactive esta casilla</span><span class="sxs-lookup"><span data-stu-id="4a4f6-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="4a4f6-134">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="4a4f6-135">Final de Hola de hello **acciones de Script** hoja, haga clic en hello **seleccione** configuración del botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="4a4f6-136">Por último, haga clic en hello **seleccione** situado en la parte inferior de Hola de hello **configuración avanzada** información de configuración de hoja toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="4a4f6-137">Continuar aprovisionamiento clúster Hola tal y como se describe en [clústeres de HDInsight basados en Linux aprovisionar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a4f6-138">Azure PowerShell, Hola CLI de Azure, hello HDInsight .NET SDK o plantillas del Administrador de recursos de Azure también pueden ser utilizados tooapply acciones de script.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="4a4f6-139">También puede aplicar tooalready de acciones de script clústeres en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="4a4f6-140">Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="4a4f6-141">Uso de Presto con HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a4f6-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="4a4f6-142">Realizar Hola siguiendo los pasos toouse eso es todo en un clúster de HDInsight después de haber instalado mediante pasos de Hola se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="4a4f6-143">Conecte el clúster de HDInsight de toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="4a4f6-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="4a4f6-144">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="4a4f6-145">Inicie Hola shell listo mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="4a4f6-146">Ejecute una consulta en una tabla de ejemplo, **hivesampletable**, que está disponible en todos los clústeres de HDInsight de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="4a4f6-147">De forma predeterminada, los conectores [Hive](https://prestodb.io/docs/current/connector/hive.html) y [TPCH](https://prestodb.io/docs/current/connector/tpch.html) para Presto ya están configurados.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="4a4f6-148">Conector de subárbol es instalación de Hive de toouse configurado Hola instalada de forma predeterminada, por lo que todas las tablas de Hola de subárbol se verán automáticamente en eso es todo.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="4a4f6-149">Para obtener una descripción detallada de cómo puede utilizar Presto, consulte la [documentación de Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="4a4f6-150">Uso de Airpal con Presto</span><span class="sxs-lookup"><span data-stu-id="4a4f6-150">Use Airpal with Presto</span></span>

<span data-ttu-id="4a4f6-151">[Airpal](https://github.com/airbnb/airpal#airpal) es una interfaz de consulta de código abierto basada en web para Presto.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="4a4f6-152">Para más información sobre Airpal, consulte la [documentación de Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="4a4f6-153">En esta sección, veremos los pasos de hello demasiado**instalar Airpal en hello edgenode** de un clúster de Hadoop de HDInsight, que ya tiene eso es todo instalado.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="4a4f6-154">Esto garantiza que esa interfaz de consulta de hello Airpal web está disponible a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="4a4f6-155">Mediante SSH, conecte el nodo principal de toohello Hola del clúster de HDInsight que tenga instalado Presto:</span><span class="sxs-lookup"><span data-stu-id="4a4f6-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="4a4f6-156">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4a4f6-157">Una vez conectado, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="4a4f6-158">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a4f6-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="4a4f6-159">De salida de hello, anote el valor de Hola para hello **valor** propiedad.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="4a4f6-160">Lo necesitará al instalar Airpal en hello edgenode de clúster.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="4a4f6-161">Desde la salida de hello anteriormente, el valor de Hola que necesitará es **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="4a4f6-162">Utilizar una plantilla de hello  **[aquí](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate una HDInsight edgenode de clúster y proporcione los valores de hello tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![Instalación de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="4a4f6-164">Haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="4a4f6-165">Una vez realizados cambios hello toohello aplicada configuración del clúster, puede obtener acceso a interfaz web de hello Airpal utilizando Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="4a4f6-166">a.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-166">a.</span></span> <span data-ttu-id="4a4f6-167">En la hoja de clúster de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-167">From hello cluster blade, click **Applications**.</span></span>

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="4a4f6-169">b.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-169">b.</span></span> <span data-ttu-id="4a4f6-170">De hello **instalado aplicaciones** hoja, haga clic en **Portal** contra airpal.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="4a4f6-172">c.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-172">c.</span></span> <span data-ttu-id="4a4f6-173">Cuando se le solicite, escriba credenciales de administrador de Hola que especificó al crear el clúster de Hadoop de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="4a4f6-174">Personalización de una instalación de Presto en un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a4f6-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="4a4f6-175">Después de haber instalado ya está preparado en un clúster de Hadoop de HDInsight, puede personalizar Hola instalación toomake cambios como la configuración de memoria de actualización, cambiar los conectores, etcetera. Realizar Hola siguiendo los pasos toodo así.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="4a4f6-176">Mediante SSH, conecte el nodo principal de toohello Hola del clúster de HDInsight que tenga instalado Presto:</span><span class="sxs-lookup"><span data-stu-id="4a4f6-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="4a4f6-177">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4a4f6-178">Realice los cambios de configuración en el archivo hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="4a4f6-179">Para más información sobre la configuración de presto, consulte [Presto Configuration Options for YARN-Based Clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Opciones de configuración de Presto para clústeres basados en YARN).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="4a4f6-180">Detener y eliminar la instancia de ejecución actual de Hola de eso es todo.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="4a4f6-181">Inicie una nueva instancia de eso es todo con la personalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="4a4f6-182">Espere toobe de instancia nueva de hello listo y anote la dirección del coordinador listo.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="4a4f6-183">Generación de datos de pruebas comparativas para clústeres de HDInsight que ejecutan Presto</span><span class="sxs-lookup"><span data-stu-id="4a4f6-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="4a4f6-184">TPC-DS es Hola estándar del sector para medir el rendimiento de Hola de muchos sistemas de soporte técnico de decisión, incluidos los sistemas de grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="4a4f6-185">Puede usar Presto en los datos de toogenerate de clústeres de HDInsight y evaluar la manera en que compara con sus propios datos de prueba comparativa de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="4a4f6-186">Para más información, consulte [esta página](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="4a4f6-187">Consulte también</span><span class="sxs-lookup"><span data-stu-id="4a4f6-187">See also</span></span>
* <span data-ttu-id="4a4f6-188">[Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="4a4f6-189">El matiz es una interfaz de usuario que hace más fácil toocreate, ejecute web y guarde los trabajos de Pig y Hive, así como examinar almacenamiento predeterminado de hello para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="4a4f6-190">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="4a4f6-191">Utilice tooinstall de personalización de clúster de clústeres de Giraph en Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="4a4f6-192">Giraph permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="4a4f6-193">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a4f6-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="4a4f6-194">Utilice tooinstall de personalización de clúster de clústeres de Solr en Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="4a4f6-195">Solr permite operaciones de búsqueda eficaces tooperform en los datos almacenados.</span><span class="sxs-lookup"><span data-stu-id="4a4f6-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
