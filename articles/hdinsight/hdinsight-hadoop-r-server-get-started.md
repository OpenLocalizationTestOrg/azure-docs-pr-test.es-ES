---
title: aaaGet a trabajar con R Server en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un Apache inspirará en clúster de HDInsight que incluye el servidor de R y enviar un script de R en clúster de Hola."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="14dec-103">Introducción al uso del servidor de R en HDInsight</span><span class="sxs-lookup"><span data-stu-id="14dec-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="14dec-104">HDInsight incluye una toobe de opción R Server integrado en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14dec-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="14dec-105">Esta opción permite a los scripts de R cálculos de toouse Spark y MapReduce toorun distribuida.</span><span class="sxs-lookup"><span data-stu-id="14dec-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="14dec-106">En este documento, aprenderá cómo toocreate un servidor de R en los clústeres de HDInsight y, a continuación, ejecutar una R de archivo de comandos que se muestra el uso de Spark para distribuye los cálculos de R.</span><span class="sxs-lookup"><span data-stu-id="14dec-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="14dec-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="14dec-107">Prerequisites</span></span>

* <span data-ttu-id="14dec-108">**Una suscripción a Azure**: antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="14dec-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="14dec-109">Artículo vaya toohello [evaluación gratuita de Azure de Microsoft obtener](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="14dec-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="14dec-110">**Un cliente de Shell seguro (SSH)**: se usa un SSH cliente tooremotely conectar el clúster de HDInsight toohello y ejecutar comandos directamente en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="14dec-111">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="14dec-112">**Claves SSH (opcionales)**: puede proteger Hola SSH cuenta usada tooconnect toohello clúster con una contraseña o una clave pública.</span><span class="sxs-lookup"><span data-stu-id="14dec-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="14dec-113">Con una contraseña es más fácil y permite tooget se inicia sin necesidad de toocreate un par de claves pública y privada.</span><span class="sxs-lookup"><span data-stu-id="14dec-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="14dec-114">Sin embargo, es más seguro utilizar una clave.</span><span class="sxs-lookup"><span data-stu-id="14dec-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="14dec-115">Hola en este documento da por sentado que está utilizando una contraseña.</span><span class="sxs-lookup"><span data-stu-id="14dec-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="14dec-116">Creación automatizada del clúster</span><span class="sxs-lookup"><span data-stu-id="14dec-116">Automated cluster creation</span></span>

<span data-ttu-id="14dec-117">Puede automatizar la creación de hello de HDInsight R Servers mediante Azure Resource Manager plantillas, Hola SDK y también PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14dec-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="14dec-118">toocreate un servidor de R con una plantilla de administración de recursos de Azure, consulte [implementar un clúster de HDInsight de servidor de R](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="14dec-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="14dec-119">toocreate un servidor de R mediante Hola .NET SDK, vea [crear clústeres basados en Linux en HDInsight con hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="14dec-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="14dec-120">toodeploy R Server con powershell, consulte el artículo de hello en [crear un servidor de R en HDInsight con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="14dec-121">Crear clúster de hello mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="14dec-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="14dec-122">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="14dec-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="14dec-123">Seleccione **NUEVO** -> **Inteligencia y análisis**, -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="14dec-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Imagen de la creación de un nuevo clúster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="14dec-125">Hola **creación rápida** rápida, escriba un nombre para el clúster de Hola Hola **nombre del clúster** campo.</span><span class="sxs-lookup"><span data-stu-id="14dec-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="14dec-126">Si tiene varias suscripciones de Azure, use hello **suscripción** entrada tooselect Hola uno desea toouse.</span><span class="sxs-lookup"><span data-stu-id="14dec-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Opciones de nombre de clúster y suscripción](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="14dec-128">Seleccione **clúster tipo** tooopen hello **configuración de clúster** hoja.</span><span class="sxs-lookup"><span data-stu-id="14dec-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="14dec-129">En hello **configuración de clúster** hoja, seleccione Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="14dec-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="14dec-130">**Tipo de clúster**: R Server</span><span class="sxs-lookup"><span data-stu-id="14dec-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="14dec-131">**Versión**: versión de Hola select de tooinstall R Server en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="14dec-132">versión de Hola actualmente disponible es ***9.1 de servidor de R (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="14dec-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="14dec-133">Notas de la versión para las versiones disponibles de Hola de R Server están disponibles [aquí](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="14dec-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="14dec-134">**Edición de la Comunidad de R Studio para R Server**: esta IDE basadas en el explorador se instala de forma predeterminada en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="14dec-135">Si prefiere toonot instalarla, a continuación, desactive la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="14dec-136">Si elige toohave instalan, dirección URL de hello para tener acceso a Hola inicio de sesión RStudio Server se encuentra en una hoja de aplicación de portal para el clúster, una vez que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="14dec-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="14dec-137">Dejar Hola otras opciones en valores predeterminados de Hola y usar hello **seleccione** toosave Hola clúster tipo de botón.</span><span class="sxs-lookup"><span data-stu-id="14dec-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Captura de pantalla de la hoja del tipo de clúster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="14dec-139">Escriba un **Nombre de usuario de inicio de sesión del clúster** y una **Contraseña de inicio de sesión del clúster**.</span><span class="sxs-lookup"><span data-stu-id="14dec-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="14dec-140">Especifique un **Nombre de usuario de SSH**.</span><span class="sxs-lookup"><span data-stu-id="14dec-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="14dec-141">SSH es tooremotely usado conectarse toohello clúster con un **Shell seguro (SSH)** cliente.</span><span class="sxs-lookup"><span data-stu-id="14dec-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="14dec-142">Puede especificar usuario SSH de hello en este cuadro de diálogo o después de que se haya creado el clúster de hello (en la pestaña de configuración de hello para el clúster de hello).</span><span class="sxs-lookup"><span data-stu-id="14dec-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="14dec-143">R Server está configurado tooexpect una **nombre de usuario SSH** de "remoteuser".</span><span class="sxs-lookup"><span data-stu-id="14dec-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="14dec-144">**Si utiliza un nombre de usuario diferente, debe realizar un paso adicional después de crear el clúster de Hola.**</span><span class="sxs-lookup"><span data-stu-id="14dec-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="14dec-145">Cuadro de hello deje activada para **usar la misma contraseña como inicio de sesión de clúster** toouse **contraseña** como hello tipo de autenticación, a menos que se prefiere el uso de una clave pública.</span><span class="sxs-lookup"><span data-stu-id="14dec-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="14dec-146">Necesita un par de claves pública/privada tooaccess R Server en clúster de Hola a través de un cliente como, por ejemplo, RTV, RStudio u otro IDE de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="14dec-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="14dec-147">Si instala Hola edición community de RStudio Server, debe toochoose una contraseña SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="14dec-148">toocreate y use un par de claves pública y privada, desactive la opción **usar la misma contraseña como inicio de sesión de clúster** y, a continuación, seleccione **clave pública** y haga lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="14dec-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="14dec-149">Estas instrucciones asumen que dispone de Cygwin con ssh-keygen o equivalente instalado.</span><span class="sxs-lookup"><span data-stu-id="14dec-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="14dec-150">Generar un par de claves pública/privada Hola desde línea de comandos en su equipo portátil:</span><span class="sxs-lookup"><span data-stu-id="14dec-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="14dec-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="14dec-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="14dec-152">Siga Hola prompt tooname un archivo de clave y, a continuación, escriba una frase de contraseña para una mayor seguridad.</span><span class="sxs-lookup"><span data-stu-id="14dec-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="14dec-153">La pantalla debe ser similar Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="14dec-153">Your screen should look something like hello following image:</span></span>

        ![Línea de comando SSH en Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="14dec-155">Este comando crea un archivo de clave privada y un archivo de clave público en el nombre < private-key-filename > Hola pub, por ejemplo furiosa y furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="14dec-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="14dec-157">A continuación, especifique el archivo de clave pública de hello (&#42;. pub) al asignar HDI credenciales de clúster y por último, confirme su grupo de recursos y región y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="14dec-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Hoja Credenciales](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="14dec-159">Cambiar los permisos de archivo de clave privada de hello en su equipo portátil:</span><span class="sxs-lookup"><span data-stu-id="14dec-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="14dec-160">chmod 600 <nombreDeArchivoDeClavePrivada></span><span class="sxs-lookup"><span data-stu-id="14dec-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="14dec-161">Use el archivo de clave privada de hello mediante SSH para inicio de sesión remoto:</span><span class="sxs-lookup"><span data-stu-id="14dec-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="14dec-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="14dec-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="14dec-163">O bien, como definiciones de Hola de parte de su Hadoop Spark cálculo para R Server en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="14dec-164">Vea hello **Using Microsoft R Server como un cliente de Hadoop** en la subsección [crear un contexto de proceso para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="14dec-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="14dec-165">Creación rápida de Hello pasa toohello **almacenamiento** cuenta de almacenamiento de hello hoja tooselect toobe de configuración para la ubicación principal de Hola Hola usado por clúster Hola de sistema de archivos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="14dec-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="14dec-166">Seleccione una cuenta de Azure Storage nueva o existente o una cuenta de almacenamiento de Data Lake existente.</span><span class="sxs-lookup"><span data-stu-id="14dec-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="14dec-167">Si selecciona una cuenta de almacenamiento de Azure, se selecciona una cuenta de almacenamiento existente seleccionando **seleccionar una cuenta de almacenamiento** y, a continuación, seleccione cuenta pertinente Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="14dec-168">Crear una nueva cuenta con hello **crear nuevo** vínculo Hola **seleccionar una cuenta de almacenamiento** sección.</span><span class="sxs-lookup"><span data-stu-id="14dec-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="14dec-169">Si selecciona **New** debe especificar un nombre para la nueva cuenta de almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="14dec-170">Una marca de verificación verde aparece si se acepta el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="14dec-171">Hola **contenedor predeterminado** nombre de toohello de los valores predeterminados del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="14dec-172">Deje este valor predeterminado como el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="14dec-173">Si se ha seleccionado una nueva opción de cuenta de almacenamiento un símbolo del sistema tooselect **ubicación** se especificado tooselect qué región toocreate Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="14dec-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Hoja Origen de datos](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="14dec-175">También se estén seleccionando la ubicación de hello para el origen de datos predeterminado de hello establece la ubicación de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14dec-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="14dec-176">Hello clúster y forma predeterminada el origen de datos debe Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="14dec-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="14dec-177">Si desea que toouse un almacén de Data Lake existente, a continuación, seleccione Hola toouse de cuenta de almacenamiento ADLS y agregar clúster hello *agregar* identidad tooyour clúster tooallow toohello en el almacén acceso.</span><span class="sxs-lookup"><span data-stu-id="14dec-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="14dec-178">Para más información sobre este proceso, consulte [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="14dec-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="14dec-179">Hola de uso **seleccione** configuración del origen de datos de botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="14dec-180">Hola **resumen** blade, a continuación, muestra toovalidate toda la configuración.</span><span class="sxs-lookup"><span data-stu-id="14dec-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="14dec-181">Aquí puede cambiar su **tamaño de clúster** toomodify Hola número de servidores en el clúster y hay que especificar ninguno **acciones de Script** desea toorun.</span><span class="sxs-lookup"><span data-stu-id="14dec-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="14dec-182">A menos que sepa que necesita un clúster mayor, deje el número de Hola de nodos de trabajador en el valor predeterminado es hello `4`.</span><span class="sxs-lookup"><span data-stu-id="14dec-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="14dec-183">Hola se calcula el costo de clúster de Hola se muestra en la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![Resumen del clúster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="14dec-185">Si es necesario, puede cambiar el tamaño de su clúster más adelante a través de hello Portal (**clúster** -> **configuración** -> **escala clúster**) tooincrease o reducir el número de Hola de nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="14dec-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="14dec-186">Este cambio de tamaño puede ser útil ralentí hacia abajo de clúster de hello cuando no esté en uso, o para agregar las necesidades de capacidad toomeet Hola de tareas más grandes.</span><span class="sxs-lookup"><span data-stu-id="14dec-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="14dec-187">Algunos tookeep factores en cuenta al asignar el tamaño de su clúster, nodos de datos de Hola y el nodo del borde de hello incluyen:</span><span class="sxs-lookup"><span data-stu-id="14dec-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="14dec-188">rendimiento de Hola de análisis de R Server distribuidos en Spark sea proporcional toohello número de nodos de trabajador cuando hello es grande.</span><span class="sxs-lookup"><span data-stu-id="14dec-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="14dec-189">Hola el rendimiento de análisis de servidor de R es lineal en el tamaño de Hola de los datos que se va a analizar.</span><span class="sxs-lookup"><span data-stu-id="14dec-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="14dec-190">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14dec-190">For example:</span></span>  

     * <span data-ttu-id="14dec-191">Para los datos de toomodest pequeños, rendimiento es mejor cuando se analizan en un contexto de proceso local en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="14dec-192">Para obtener más información sobre los escenarios de hello en la que Hola local y Spark contextos de proceso funcionan mejor, consulte Opciones de contexto de proceso para el servidor de R en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14dec-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="14dec-193">Si debe iniciar sesión en el nodo del borde toohello y ejecuta el script R, a continuación, se ejecutan todos pero hello las funciones ScaleR rx <strong>localmente</strong> en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="14dec-194">Por lo tanto Hola memoria y número de núcleos del nodo de hello borde debe ajustarse según corresponda.</span><span class="sxs-lookup"><span data-stu-id="14dec-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="14dec-195">Hola que esto mismo se aplica si usa R Server en HDI como un contexto de proceso remoto desde su portátil.</span><span class="sxs-lookup"><span data-stu-id="14dec-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Hoja Niveles de precios de nodo](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="14dec-197">Hola de uso **seleccione** nodo del botón toosave Hola precios de configuración.</span><span class="sxs-lookup"><span data-stu-id="14dec-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="14dec-198">Observe que también existe el vínculo **Descargar plantilla y parámetros**.</span><span class="sxs-lookup"><span data-stu-id="14dec-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="14dec-199">Haga clic en este vínculo toodisplay las secuencias de comandos que pueden ser usado tooautomate Hola creación de un clúster con la configuración seleccionada de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="14dec-200">Estas secuencias de comandos también están disponibles en hello Azure entrada portal para el clúster una vez que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="14dec-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="14dec-201">Tarda algún tiempo para hello clúster toobe creado, normalmente alrededor de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="14dec-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="14dec-202">Usar icono hello en el panel de inicio de Hola u Hola **notificaciones** entrada en hello deja de hello página toocheck en proceso de creación de hello.</span><span class="sxs-lookup"><span data-stu-id="14dec-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="14dec-203">Conectar tooRStudio Server</span><span class="sxs-lookup"><span data-stu-id="14dec-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="14dec-204">Si ha elegido tooinclude edición community de RStudio Server en la instalación, puede tener acceso a inicio de sesión de hello RStudio a través de dos métodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="14dec-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="14dec-205">Vaya toohello después de la dirección URL (donde **CLUSTERNAME** es Hola nombre del clúster de Hola que ha creado):</span><span class="sxs-lookup"><span data-stu-id="14dec-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="14dec-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="14dec-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="14dec-207">Abrir entrada de hello para el clúster en hello portal de Azure, seleccione hello **R Server paneles** vínculo rápido y, a continuación, seleccionando hello **R Studio panel**:</span><span class="sxs-lookup"><span data-stu-id="14dec-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Panel de acceso Hola R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Panel de acceso Hola R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="14dec-210">Independientemente del método hello utilizado, hello primera vez que inicie sesión en necesita tooauthenticate dos veces.</span><span class="sxs-lookup"><span data-stu-id="14dec-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="14dec-211">En la primera autenticación hello, proporcionar hello *identificador de usuario de administración de clúster* y *contraseña*.</span><span class="sxs-lookup"><span data-stu-id="14dec-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="14dec-212">En el segundo mensaje Hola, proporcionar hello *SSH userid* y *contraseña*.</span><span class="sxs-lookup"><span data-stu-id="14dec-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="14dec-213">Registros subsiguientes inicios solo requieren hello *contraseña SSH* y *userid*.</span><span class="sxs-lookup"><span data-stu-id="14dec-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="14dec-214">Conectar el nodo del borde toohello R Server</span><span class="sxs-lookup"><span data-stu-id="14dec-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="14dec-215">Conectar visita el nodo del borde de servidor de clúster de HDInsight de hello mediante SSH con el comando hello:</span><span class="sxs-lookup"><span data-stu-id="14dec-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="14dec-216">Puede encontrar Hola `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` dirección Hola portal de Azure, seleccione el clúster, a continuación, **toda la configuración de** -> **aplicaciones** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="14dec-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="14dec-217">Esto muestra información de extremo de SSH para el nodo del borde de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Imagen de hello SSH extremo para el nodo del borde de Hola](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="14dec-219">Si utiliza un toosecure de contraseña de su cuenta de usuario SSH, son tooenter solicitada se.</span><span class="sxs-lookup"><span data-stu-id="14dec-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="14dec-220">Si utiliza una clave pública, puede que tenga hello toouse `-i` toospecify parámetro Hola clave privada correspondiente.</span><span class="sxs-lookup"><span data-stu-id="14dec-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="14dec-221">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14dec-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="14dec-222">Para obtener más información, consulte [conectar tooHDInsight (Hadoop) mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="14dec-223">Una vez conectado, llegan en un símbolo del sistema siguiente toohello similar:</span><span class="sxs-lookup"><span data-stu-id="14dec-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="14dec-224">Habilitación de varios usuarios simultáneos</span><span class="sxs-lookup"><span data-stu-id="14dec-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="14dec-225">Puede habilitar a varios usuarios simultáneos agregando más usuarios para el nodo del borde hello en qué hello RStudio Comunidad se ejecuta la versión.</span><span class="sxs-lookup"><span data-stu-id="14dec-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="14dec-226">Al crear un clúster de HDInsight, es preciso especificar dos usuarios, un usuario HTTP y un usuario SSH:</span><span class="sxs-lookup"><span data-stu-id="14dec-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Usuario simultáneo 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="14dec-228">**Nombre de usuario de inicio de sesión del clúster**: un usuario HTTP para la autenticación a través de la puerta de enlace de HDInsight de Hola que es usado tooprotect hello HDInsight clústeres que ha creado.</span><span class="sxs-lookup"><span data-stu-id="14dec-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="14dec-229">Este usuario HTTP es tooaccess usado hello Ambari UI, interfaz de usuario de YARN, así como otros componentes de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="14dec-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="14dec-230">**El nombre de usuario de Secure Shell (SSH)**: un clúster de hello SSH tooaccess de usuario a través de shell seguro.</span><span class="sxs-lookup"><span data-stu-id="14dec-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="14dec-231">Este usuario es un usuario de hello sistema Linux para todos los nodos principales de hello, nodos de trabajador y nodos de borde.</span><span class="sxs-lookup"><span data-stu-id="14dec-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="14dec-232">Para poder utilizar tooaccess de shell seguro cualquiera de los nodos de hello en un clúster remoto.</span><span class="sxs-lookup"><span data-stu-id="14dec-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="14dec-233">versión de comunidad de R Studio Server de Hello usada en hello Microsoft R Server en clúster de HDInsight tipo acepta únicamente el nombre de usuario de Linux y una contraseña como un mecanismo de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="14dec-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="14dec-234">No admite tokens de paso.</span><span class="sxs-lookup"><span data-stu-id="14dec-234">It does not support passing tokens.</span></span> <span data-ttu-id="14dec-235">Por tanto, si ha creado un nuevo clúster y desea toouse R Studio tooaccess, necesita toolog en dos veces.</span><span class="sxs-lookup"><span data-stu-id="14dec-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="14dec-236">Primero inicie sesión con credenciales de usuario de hello HTTP a través de hello puerta de enlace de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="14dec-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Usuario simultáneo 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="14dec-238">A continuación, usar toolog de credenciales de usuario SSH de hello en tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="14dec-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Usuario simultáneo 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="14dec-240">Actualmente, una cuenta de usuario SSH solo se puede crear al aprovisionar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14dec-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="14dec-241">Para clústeres de varios usuarios tooaccess Microsoft R Server en HDInsight tooenable necesitamos toocreate usuarios adicionales en hello sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="14dec-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="14dec-242">Porque RStudio Comunidad de servidor se ejecuta en el nodo del borde del clúster de hello, hay varios pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="14dec-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="14dec-243">Usar toolog de usuario SSH de hello creado en el nodo del borde toohello</span><span class="sxs-lookup"><span data-stu-id="14dec-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="14dec-244">Agregar más usuarios de Linux al nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="14dec-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="14dec-245">Utilice la versión de comunidad RStudio con creado por el usuario Hola</span><span class="sxs-lookup"><span data-stu-id="14dec-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="14dec-246">Paso 1: Utilizar toolog de usuario SSH de hello creado en el nodo del borde toohello</span><span class="sxs-lookup"><span data-stu-id="14dec-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="14dec-247">Descargar cualquier herramienta SSH (como Putty) y usar hello toolog de usuario SSH existente en.</span><span class="sxs-lookup"><span data-stu-id="14dec-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="14dec-248">A continuación, siga las instrucciones de hello proporcionadas en [conectar tooHDInsight (Hadoop) mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Hola nodo del borde.</span><span class="sxs-lookup"><span data-stu-id="14dec-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="14dec-249">dirección de nodo del borde Hola para R Server en clúster de HDInsight es: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="14dec-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="14dec-250">Paso 2: Adición de más usuarios de Linux al nodo perimetral</span><span class="sxs-lookup"><span data-stu-id="14dec-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="14dec-251">tooadd un nodo del borde usuario toohello, ejecutar comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="14dec-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="14dec-252">Debería ver Hola después de elementos devueltos:</span><span class="sxs-lookup"><span data-stu-id="14dec-252">You should see hello following items returned:</span></span> 

![Usuario simultáneo 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="14dec-254">Cuando se le solicite "contraseña actual de Kerberos:", simplemente presione las teclas **ENTRAR** tooignore lo.</span><span class="sxs-lookup"><span data-stu-id="14dec-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="14dec-255">Hola `-m` opción `useradd` comando indica que el sistema de hello creará una carpeta particular de usuario de hello, que es necesario para la versión de comunidad RStudio.</span><span class="sxs-lookup"><span data-stu-id="14dec-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="14dec-256">Paso 3: Versión Use RStudio Comunidad con creado por el usuario Hola</span><span class="sxs-lookup"><span data-stu-id="14dec-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="14dec-257">Usar Hola creado por el usuario toolog en tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="14dec-257">Use hello user created toolog in tooRStudio:</span></span>

![Usuario simultáneo 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="14dec-259">Observe que RStudio indica que está usando el nuevo usuario de hello (aquí, por ejemplo, *sshuser6*) toolog en clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="14dec-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Usuario simultáneo 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="14dec-261">También puede iniciar sesión con credenciales de hello original (de forma predeterminada, es *sshuser*) simultáneamente en otra ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="14dec-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="14dec-262">Puede enviar un trabajo mediante las funciones de scaleR.</span><span class="sxs-lookup"><span data-stu-id="14dec-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="14dec-263">Este es un ejemplo de Hola comandos usados toorun un trabajo:</span><span class="sxs-lookup"><span data-stu-id="14dec-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="14dec-264">Tenga en cuenta que los trabajos de hello enviados en diferentes nombres de usuario en la interfaz de usuario de YARN:</span><span class="sxs-lookup"><span data-stu-id="14dec-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Usuario simultáneo 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="14dec-266">Tenga en cuenta también que Hola recién agregado usuarios no tienen privilegios de raíz en el sistema Linux, pero ha Hola mismo tener acceso a archivos de Hola de tooall en el almacenamiento remoto de HDFS y WASB Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="14dec-267">Usar la consola de hello R</span><span class="sxs-lookup"><span data-stu-id="14dec-267">Use hello R console</span></span>

1. <span data-ttu-id="14dec-268">Desde la sesión de SSH de hello, use Hola después de la consola de comandos toostart Hola R:</span><span class="sxs-lookup"><span data-stu-id="14dec-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="14dec-269">Debería ver resultados similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="14dec-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="14dec-270">R versión 3.2.2 (2015-08-14)--"Fire Safety" Copyright (C) 2015 hello R Foundation para la plataforma de informática en estadística: x86_64 pc linux-gnu (64 bits)</span><span class="sxs-lookup"><span data-stu-id="14dec-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="14dec-271">R es un software gratuito y NO INCLUYE NINGUNA GARANTÍA.</span><span class="sxs-lookup"><span data-stu-id="14dec-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="14dec-272">Son tooredistribute bienvenida en determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="14dec-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="14dec-273">Escriba 'license()' o 'licence()' para obtener más información de distribución.</span><span class="sxs-lookup"><span data-stu-id="14dec-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="14dec-274">Compatibilidad con lenguaje natural siempre que se ejecute en una configuración regional en inglés</span><span class="sxs-lookup"><span data-stu-id="14dec-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="14dec-275">R es un proyecto de colaboración con muchos colaboradores.</span><span class="sxs-lookup"><span data-stu-id="14dec-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="14dec-276">Escriba 'contributors()' para obtener más información y 'citation()' en cómo toocite R o R paquetes en las publicaciones.</span><span class="sxs-lookup"><span data-stu-id="14dec-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="14dec-277">Escriba 'demo()' para algunos demostraciones, 'help()' para obtener ayuda en línea o 'help.start()' para un toohelp de interfaz de explorador HTML.</span><span class="sxs-lookup"><span data-stu-id="14dec-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="14dec-278">Escriba 'q()' tooquit R.</span><span class="sxs-lookup"><span data-stu-id="14dec-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="14dec-279">Microsoft R Server versión 8.0: una distribución mejorada de los paquetes de Microsoft R Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="14dec-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="14dec-280">Escriba 'readme()' para leer las notas de la versión.</span><span class="sxs-lookup"><span data-stu-id="14dec-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="14dec-281">De hello `>` símbolo del sistema, puede escribir código de R.</span><span class="sxs-lookup"><span data-stu-id="14dec-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="14dec-282">Servidor de R incluye paquetes que le permiten tooeasily interactúan con Hadoop y ejecutar cálculos distribuidos.</span><span class="sxs-lookup"><span data-stu-id="14dec-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="14dec-283">Por ejemplo, usar hello después de raíz de comando tooview Hola Hola predeterminado de sistema de archivos para el clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="14dec-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="14dec-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="14dec-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="14dec-285">También puede usar el direccionamiento de estilo de hello WASB.</span><span class="sxs-lookup"><span data-stu-id="14dec-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="14dec-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="14dec-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="14dec-287">Uso de R Server en HDI desde una instancia remota de Microsoft R Server o Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="14dec-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="14dec-288">Es posible tooset el contexto de proceso de Hadoop Spark de HDI de toohello de acceso desde una instancia remota de Microsoft R Server o Microsoft R cliente que se ejecuta en un escritorio o portátil.</span><span class="sxs-lookup"><span data-stu-id="14dec-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="14dec-289">Vea **Using Microsoft R Server como un cliente de Hadoop** subsección Hola [crear un contexto de proceso para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="14dec-290">toodo por lo tanto, necesita hello toospecify siguientes opciones al definir el contexto de proceso de hello RxSpark en su equipo portátil: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches y sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="14dec-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="14dec-291">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14dec-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="14dec-292">Usar un contexto de proceso</span><span class="sxs-lookup"><span data-stu-id="14dec-292">Use a compute context</span></span>

<span data-ttu-id="14dec-293">Un contexto de proceso le permite toocontrol, si se debe realizar localmente en el nodo del borde de Hola o se distribuyen por los nodos en clúster de HDInsight de Hola Hola cálculo.</span><span class="sxs-lookup"><span data-stu-id="14dec-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="14dec-294">Desde la consola de hello R (en una sesión de SSH) o el servidor de RStudio, usar hello después de datos de ejemplo de código tooload en el almacenamiento de saludo predeterminado de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="14dec-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="14dec-295">A continuación, vamos a crear alguna información de datos y definir dos orígenes de datos de modo que podemos trabajar con datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="14dec-296">Vamos a ejecutar una regresión logística basados en datos de hello mediante el contexto de proceso local Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="14dec-297">Debería ver resultados que termina por toohello similares de las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="14dec-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="14dec-298">A continuación, vamos a ejecutar Hola mismo regresión logística con contexto de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="14dec-299">contexto de Spark Hola distribuye Hola procesar a través de todos los nodos de trabajador de hello en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="14dec-300">También puede utilizar el cálculo de toodistribute MapReduce en nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="14dec-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="14dec-301">Para más información sobre el contexto de proceso, consulte [Opciones de contexto de proceso para R Server en HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="14dec-302">Distribuir los nodos de toomultiple de código de R</span><span class="sxs-lookup"><span data-stu-id="14dec-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="14dec-303">Con el servidor de R, fácilmente puede tomar código existente, R y ejecutar a través de varios nodos de clúster de hello mediante `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="14dec-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="14dec-304">Esta función es útil cuando se realiza un barrido de parámetros o simulaciones.</span><span class="sxs-lookup"><span data-stu-id="14dec-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="14dec-305">Hola código siguiente es un ejemplo de cómo toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="14dec-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="14dec-306">Si todavía utilizas Hola Spark o contexto de MapReduce, este comando devuelve un valor nodename Hola para nodos de trabajador de hello ese código de hello `(Sys.info()["nodename"])` se ejecuta en.</span><span class="sxs-lookup"><span data-stu-id="14dec-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="14dec-307">Por ejemplo, en un clúster de cuatro nodos, se espera tooreceive salida siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="14dec-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="14dec-308">Acceso a datos en Hive y Parquet</span><span class="sxs-lookup"><span data-stu-id="14dec-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="14dec-309">Una característica disponible en R Server 9.1 permite toodata de acceso directo de Hive y Parquet para su uso por las funciones ScaleR en contexto de proceso de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="14dec-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="14dec-310">Estas capacidades están disponibles a través de la nueva ScaleR origen de datos funciona denominados RxHiveData y RxParquetData que funcionan a través del uso de datos de Spark SQL tooload directamente en una trama de datos de Spark para el análisis por ScaleR.</span><span class="sxs-lookup"><span data-stu-id="14dec-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="14dec-311">Hola siguiente código proporciona ejemplos de código en el uso de las nuevas funciones de hello:</span><span class="sxs-lookup"><span data-stu-id="14dec-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="14dec-312">Para obtener más información sobre el uso de estas nuevas funciones, vea Hola ayuda en pantalla de R Server mediante el uso de hello `?RxHivedata` y `?RxParquetData` comandos.</span><span class="sxs-lookup"><span data-stu-id="14dec-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="14dec-313">Instalar paquetes de R adicionales en el nodo del borde de Hola</span><span class="sxs-lookup"><span data-stu-id="14dec-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="14dec-314">Si desea que tooinstall paquetes de R adicionales en el nodo del borde de hello, puede usar `install.packages()` directamente desde Hola consola de R cuando toohello conectado arista nodo a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="14dec-315">Sin embargo, si necesita tooinstall paquetes de R en nodos de trabajador de Hola de clúster de hello, debe usar una acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="14dec-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="14dec-316">Acciones de script son scripts de Bash que usa toomake configuración cambios toohello HDInsight clúster o tooinstall software adicional, como paquetes de R adicionales.</span><span class="sxs-lookup"><span data-stu-id="14dec-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="14dec-317">paquetes adicionales de tooinstall mediante una acción de secuencia de comandos, utilice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="14dec-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14dec-318">Uso de paquetes de R adicionales de acciones de Script tooinstall sólo puede utilizarse una vez creado el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="14dec-319">No utilice este procedimiento durante la creación del clúster, tal y como script de Hola se basa en R Server está completamente instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="14dec-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="14dec-320">De hello [portal de Azure](https://portal.azure.com), seleccione el servidor de R en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14dec-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="14dec-321">De hello **configuración** hoja, seleccione **acciones de Script** y, a continuación, **Enviar nueva** toosubmit una nueva acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="14dec-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Imagen de la hoja Acciones de script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="14dec-323">De hello **acción de secuencia de comandos de envío** hoja, proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="14dec-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="14dec-324">**Nombre**: descriptivo nombre tooidentify esta secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="14dec-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="14dec-325">**URI de script de Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="14dec-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="14dec-326">**Head** (Principal): este elemento debe estar **desactivado**.</span><span class="sxs-lookup"><span data-stu-id="14dec-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="14dec-327">**Worker** (De trabajo): este elemento debe estar **activado**.</span><span class="sxs-lookup"><span data-stu-id="14dec-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="14dec-328">**Edge nodes** (Nodos perimetrales): este elemento debe estar **desactivado**.</span><span class="sxs-lookup"><span data-stu-id="14dec-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="14dec-329">**Zookeeper**: este elemento debe estar **activado**.</span><span class="sxs-lookup"><span data-stu-id="14dec-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="14dec-330">**Parámetros**: Hola R paquetes toobe instalado.</span><span class="sxs-lookup"><span data-stu-id="14dec-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="14dec-331">Por ejemplo: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="14dec-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="14dec-332">**Persist this script...** (Continuar con este script…): debe estar **activado**.</span><span class="sxs-lookup"><span data-stu-id="14dec-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="14dec-333">De forma predeterminada, se instalan todos los paquetes de R desde una instantánea del repositorio de Microsoft MRAN Hola coherente con la versión de Hola de R Server que se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="14dec-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="14dec-334">Si desea que tooinstall las versiones más recientes de los paquetes, no hay algunos riesgos de incompatibilidad.</span><span class="sxs-lookup"><span data-stu-id="14dec-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="14dec-335">Sin embargo este tipo de instalación es posible mediante la especificación de `useCRAN` como Hola primer elemento del paquete de Hola de lista de, por ejemplo `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="14dec-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="14dec-336">Algunos paquetes de R requieren otras bibliotecas de sistema de Linux.</span><span class="sxs-lookup"><span data-stu-id="14dec-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="14dec-337">Para mayor comodidad, nos hemos preinstalado dependencias Hola necesarios Hola top 100 más populares paquetes de R.</span><span class="sxs-lookup"><span data-stu-id="14dec-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="14dec-338">Sin embargo, si paquetes de R de hello que instalar requieren bibliotecas aparte de estos, a continuación, debe descargar el script de base de hello usada aquí y agregar pasos tooinstall Hola sistema bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="14dec-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="14dec-339">Debe a continuación carga Hola modificar script tooa público blob contenedor de almacenamiento de Azure y usar paquetes de hello modificar script tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="14dec-340">Para más información sobre cómo desarrollar acciones de script, consulte [Desarrollo de acciones de script](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="14dec-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Agregar una Acción de script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="14dec-342">Seleccione **crear** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="14dec-343">Una vez completado el script de Hola, paquetes de saludo R están disponibles en todos los nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="14dec-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="14dec-344">Uso de la operacionalización de Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="14dec-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="14dec-345">Una vez completado el modelado de datos, puede poner las predicciones de hello modelo toomake.</span><span class="sxs-lookup"><span data-stu-id="14dec-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="14dec-346">tooconfigure de puesta en marcha Microsoft R Server, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="14dec-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="14dec-347">En primer lugar, ssh en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="14dec-348">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="14dec-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="14dec-349">Después de utilizar ssh, cambie el directorio para la versión pertinente de Hola y sudo Hola dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="14dec-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="14dec-350">Para Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="14dec-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="14dec-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="14dec-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="14dec-352">Para Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="14dec-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="14dec-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="14dec-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="14dec-354">puesta en marcha tooconfigure Microsoft R Server con una configuración de un solo cuadro Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="14dec-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="14dec-355">Seleccione “Configure R Server for Operationalization” (Configurar R Server para operacionalización)</span><span class="sxs-lookup"><span data-stu-id="14dec-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="14dec-356">Seleccione “A.</span><span class="sxs-lookup"><span data-stu-id="14dec-356">Select “A.</span></span> <span data-ttu-id="14dec-357">One-box (web + compute nodes)” [One-box (web y nodos de proceso)]</span><span class="sxs-lookup"><span data-stu-id="14dec-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="14dec-358">Escriba una contraseña para hello **administración** usuario</span><span class="sxs-lookup"><span data-stu-id="14dec-358">Enter a password for hello **admin** user</span></span>

![operacionalización one box](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="14dec-360">Como paso opcional, puede realizar comprobaciones de diagnóstico mediante la ejecución de una prueba de diagnóstico tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="14dec-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="14dec-361">Seleccione “6.</span><span class="sxs-lookup"><span data-stu-id="14dec-361">Select “6.</span></span> <span data-ttu-id="14dec-362">Ejecutar pruebas de diagnóstico”</span><span class="sxs-lookup"><span data-stu-id="14dec-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="14dec-363">Seleccione “A.</span><span class="sxs-lookup"><span data-stu-id="14dec-363">Select “A.</span></span> <span data-ttu-id="14dec-364">Configuración de pruebas”</span><span class="sxs-lookup"><span data-stu-id="14dec-364">Test configuration”</span></span>
3. <span data-ttu-id="14dec-365">Escriba el nombre de usuario = "admin" y la contraseña del paso de configuración anterior</span><span class="sxs-lookup"><span data-stu-id="14dec-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="14dec-366">Confirme el estado general = pass</span><span class="sxs-lookup"><span data-stu-id="14dec-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="14dec-367">Utilidad de administración de Hola de salida</span><span class="sxs-lookup"><span data-stu-id="14dec-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="14dec-368">Salga de SSH</span><span class="sxs-lookup"><span data-stu-id="14dec-368">Exit SSH</span></span>

![Diagnóstico de operacionalización](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="14dec-370">**Retrasos prolongados al consumir el servicio web en Spark**</span><span class="sxs-lookup"><span data-stu-id="14dec-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="14dec-371">Si se producen retrasos prolongados al intentar tooconsume un servicio web creado con las funciones de mrsdeploy en un contexto de proceso Spark, deberá tooadd algunas carpetas que faltan.</span><span class="sxs-lookup"><span data-stu-id="14dec-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="14dec-372">Hola aplicación Spark pertenece el usuario tooa denominado '*rserve2*' cada vez que se invoque desde un servicio web mediante las funciones de mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="14dec-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="14dec-373">toowork resolver este problema:</span><span class="sxs-lookup"><span data-stu-id="14dec-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="14dec-374">En esta fase, la configuración de hello para la puesta en marcha está completa.</span><span class="sxs-lookup"><span data-stu-id="14dec-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="14dec-375">Ahora puede usar hello 'mrsdeploy' en su toohello de tooconnect RClient puesta en marcha en el nodo del borde del paquete y empezar a usar sus características como [la ejecución remota de](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) y [servicios web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="14dec-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="14dec-376">Dependiendo de si el clúster se configura en una red virtual o no, debe tooset de puerto de túnel hacia delante a través de inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="14dec-377">Hello siguientes secciones se explica cómo tooset seguridad este túnel.</span><span class="sxs-lookup"><span data-stu-id="14dec-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="14dec-378">RServer Cluster en una red virtual</span><span class="sxs-lookup"><span data-stu-id="14dec-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="14dec-379">Asegúrese de que permitir el tráfico a través del nodo del puerto 12800 toohello borde.</span><span class="sxs-lookup"><span data-stu-id="14dec-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="14dec-380">De este modo, puede usar la característica de puesta en marcha de hello borde nodo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="14dec-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="14dec-381">Si hello `remoteLogin()` no se puede conectar el nodo del borde toohello, pero puede que el nodo del borde SSH toohello, es necesario tooverify si se ha establecido el tráfico de tooallow de regla de hello en el puerto 12800 correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="14dec-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="14dec-382">Si continúa el problema de hello tooface, puede solucionarlo mediante la configuración de puerto de túnel hacia delante a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="14dec-383">Para obtener instrucciones, consulte Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="14dec-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="14dec-384">RServer Cluster no configurado en una red virtual</span><span class="sxs-lookup"><span data-stu-id="14dec-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="14dec-385">Si el clúster no está configurado en la red virtual o si tiene problemas con la conectividad a través de la red virtual, puede utilizar la tunelización de reenvío del puerto de SSH:</span><span class="sxs-lookup"><span data-stu-id="14dec-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="14dec-386">En Putty, también se puede configurar.</span><span class="sxs-lookup"><span data-stu-id="14dec-386">On Putty, you can set it up as well.</span></span>

![conexión ssh de putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="14dec-388">Una vez que la sesión SSH está activa, el tráfico del puerto de su equipo 12800 Hola se reenvía el puerto del nodo del borde de toohello 12800 a través de la sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="14dec-389">Asegúrese de utilizar `127.0.0.1:12800` en el método `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="14dec-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="14dec-390">Esto se registra en la puesta en marcha del nodo del borde de toohello a través de reenvío de puerto.</span><span class="sxs-lookup"><span data-stu-id="14dec-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="14dec-391">¿Cómo tooscale Microsoft R Server puesta en marcha de proceso nodos en nodos de trabajo de HDInsight</span><span class="sxs-lookup"><span data-stu-id="14dec-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="14dec-392">Retirada de nodos de trabajador de Hola</span><span class="sxs-lookup"><span data-stu-id="14dec-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="14dec-393">Microsoft R Server no se administra actualmente mediante Yarn.</span><span class="sxs-lookup"><span data-stu-id="14dec-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="14dec-394">Si los nodos de trabajador de hello no están dado de baja, hello Yarn el Administrador de recursos no funcionará según lo previsto porque no tendrá constancia de recursos de hello utilizados por el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="14dec-395">En orden tooavoid esta situación, se recomienda retirada nodos de trabajador de hello antes de escalar horizontalmente los nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="14dec-396">Nodos de trabajador de toodecommissioning de pasos:</span><span class="sxs-lookup"><span data-stu-id="14dec-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="14dec-397">Inicie sesión en la consola de Ambari del clúster tooHDI y haga clic en la ficha "hosts"</span><span class="sxs-lookup"><span data-stu-id="14dec-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="14dec-398">Seleccionar nodos de trabajador (toobe dado de baja), haga clic en "Acciones" > "Hosts seleccionado" > "Hosts" > haga clic en "Activar el modo de mantenimiento de ON".</span><span class="sxs-lookup"><span data-stu-id="14dec-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="14dec-399">Por ejemplo, hemos seleccionado toodecommission wn3 y wn4 en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="14dec-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![retirar nodos de trabajo](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="14dec-401">Seleccione **Acciones** > **Hosts seleccionados** > **DataNodes** > haga clic en **Retirar**</span><span class="sxs-lookup"><span data-stu-id="14dec-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="14dec-402">Seleccione **Acciones** > **Hosts seleccionados** > **NodeManagers** > haga clic en **Retirar**</span><span class="sxs-lookup"><span data-stu-id="14dec-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="14dec-403">Seleccione **Acciones** > **Hosts seleccionados** > **DataNodes** > haga clic en **Detener**</span><span class="sxs-lookup"><span data-stu-id="14dec-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="14dec-404">Seleccione **Acciones** > **Hosts seleccionados** > **NodeManagers** > haga clic en **Detener**</span><span class="sxs-lookup"><span data-stu-id="14dec-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="14dec-405">Seleccione **Acciones** > **Hosts seleccionados** > **Hosts** > haga clic en **Detener todos los componentes**</span><span class="sxs-lookup"><span data-stu-id="14dec-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="14dec-406">Anule la selección de nodos de trabajador de Hola y seleccione los nodos principales de Hola</span><span class="sxs-lookup"><span data-stu-id="14dec-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="14dec-407">Seleccione **Acciones** > **Hosts seleccionados** > "**Hosts** > **Reiniciar todos los componentes**</span><span class="sxs-lookup"><span data-stu-id="14dec-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="14dec-408">Configuración de los nodos de proceso en cada nodo de trabajo retirado</span><span class="sxs-lookup"><span data-stu-id="14dec-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="14dec-409">SSH en cada nodo de trabajo retirado.</span><span class="sxs-lookup"><span data-stu-id="14dec-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="14dec-410">Ejecute la utilidad de administración mediante `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="14dec-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="14dec-411">Escriba "1" tooselect opción "Configurar R Server para la puesta en marcha".</span><span class="sxs-lookup"><span data-stu-id="14dec-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="14dec-412">Especifique la opción de "c" tooselect "C."</span><span class="sxs-lookup"><span data-stu-id="14dec-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="14dec-413">Nodo de proceso".</span><span class="sxs-lookup"><span data-stu-id="14dec-413">Compute node".</span></span> <span data-ttu-id="14dec-414">Esto configura el nodo de proceso de Hola en el nodo de trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="14dec-415">Utilidad de administración de hello de salida.</span><span class="sxs-lookup"><span data-stu-id="14dec-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="14dec-416">Incorporación de detalles de nodos de proceso en el nodo web</span><span class="sxs-lookup"><span data-stu-id="14dec-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="14dec-417">Una vez que se han configurado todos los nodos de trabajo retirados toorun nodo de proceso, vuelven a estar en el nodo del borde de Hola y agregar direcciones IP de los nodos de trabajo retirados en configuración del nodo de hello Microsoft R Server web:</span><span class="sxs-lookup"><span data-stu-id="14dec-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="14dec-418">SSH en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="14dec-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="14dec-419">Ejecute `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="14dec-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="14dec-420">Busque la sección "URI" Hola y agregue la IP del nodo de trabajo y los detalles de puerto.</span><span class="sxs-lookup"><span data-stu-id="14dec-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![línea de comandos para retirar nodos de trabajo](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="14dec-422">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="14dec-422">Troubleshoot</span></span>

<span data-ttu-id="14dec-423">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="14dec-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="14dec-424">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14dec-424">Next steps</span></span>

<span data-ttu-id="14dec-425">Ahora debe comprender cómo toocreate un nuevo clúster de HDInsight que incluye los conceptos básicos de hello y R Server Hola del uso Hola consola de R desde una sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="14dec-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="14dec-426">Hello en los temas siguientes se explican otras maneras de administrar y trabajar con R Server en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="14dec-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="14dec-427">Agregar servidor RStudio tooHDInsight (si no se instala durante la creación del clúster)</span><span class="sxs-lookup"><span data-stu-id="14dec-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="14dec-428">Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="14dec-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="14dec-429">Opciones de Azure Storage para R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="14dec-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
