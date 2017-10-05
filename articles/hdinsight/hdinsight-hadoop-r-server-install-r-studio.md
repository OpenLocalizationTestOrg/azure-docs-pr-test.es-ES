---
title: "Instalación de RStudio con R Server en HDInsight: Azure | Microsoft Docs"
description: "Cómo instalar RStudio con R Server en HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="b088d-103">Instalación de RStudio con R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b088d-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="b088d-104">En este artículo se describe cómo instalar la versión de la comunidad (gratuita) de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) en el nodo perimetral de un clúster mediante un script personalizado.</span><span class="sxs-lookup"><span data-stu-id="b088d-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="b088d-105">RStudio Server proporciona un IDE basado en explorador que pueden usar los clientes remotos y se utiliza ampliamente en Linux.</span><span class="sxs-lookup"><span data-stu-id="b088d-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="b088d-106">Hoy en día, hay varios entornos de desarrollo integrados (IDE) disponibles para R, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b088d-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="b088d-107">[Herramientas de R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft</span><span class="sxs-lookup"><span data-stu-id="b088d-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="b088d-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="b088d-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="b088d-109">[StatET](http://www.walware.de/goto/statet) basado en Eclipse de Walware.</span><span class="sxs-lookup"><span data-stu-id="b088d-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="b088d-110">La ventaja de instalar RStudio Server en el nodo perimetral de un clúster de HDInsight es que ofrece una experiencia de IDE completa para desarrollar y ejecutar scripts de R con R Server en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="b088d-111">Esta configuración puede ser mucho más productiva que el uso predeterminado de la consola de R.</span><span class="sxs-lookup"><span data-stu-id="b088d-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="b088d-112">El procedimiento descrito en este artículo solo es pertinente si no seleccionó instalar la edición community de RStudio Server al aprovisionar el clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="b088d-113">Si la agregó durante el aprovisionamiento, puede acceder a ella haciendo clic en el icono **Paneles de R Server** en la entrada de Azure Portal para el clúster y luego en el icono **R Studio Server**.</span><span class="sxs-lookup"><span data-stu-id="b088d-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="b088d-114">Si prefiere utilizar la versión Pro con licencia comercial de RStudio Server, debe seguir las instrucciones de instalación de [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="b088d-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="b088d-115">Si está usando un clúster de HDInsight para el que R se instaló mediante la [acción de script de instalación de R](hdinsight-hadoop-r-scripts-linux.md), los pasos de este documento no funcionarán correctamente, ya que requieren R Server en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b088d-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="b088d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b088d-116">Prerequisites</span></span>

* <span data-ttu-id="b088d-117">Un clúster de HDInsight de Azure con servidor de R instalado.</span><span class="sxs-lookup"><span data-stu-id="b088d-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="b088d-118">Para obtener instrucciones, consulte [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md)(Introducción a R Server en clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="b088d-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="b088d-119">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="b088d-119">An SSH client.</span></span> <span data-ttu-id="b088d-120">Para las distribuciones de Linux y Unix o Macintosh OS X, el comando `ssh` se proporciona con el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b088d-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="b088d-121">En Windows, se recomienda [Cygwin](http://www.redhat.com/services/custom/cygwin/) con la [opción OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU) o [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="b088d-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="b088d-122">Instalación de RStudio en el clúster mediante un script personalizado</span><span class="sxs-lookup"><span data-stu-id="b088d-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="b088d-123">Estos son los pasos que se deben seguir:</span><span class="sxs-lookup"><span data-stu-id="b088d-123">Here are the steps:</span></span>

1. <span data-ttu-id="b088d-124">Identifique el nodo perimetral del clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="b088d-125">Para un clúster de HDInsight con servidor de R, la siguiente es la convención de nomenclatura para el nodo principal y el nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="b088d-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="b088d-126">Nodo principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="b088d-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="b088d-127">Nodo perimetral `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="b088d-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="b088d-128">SSH en el nodo perimetral del clúster mediante el patrón de nomenclatura proporcionado en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="b088d-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="b088d-129">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b088d-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="b088d-130">Una vez conectado, se convierte en un usuario raíz en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="b088d-131">En la sesión SSH, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b088d-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="b088d-132">Descargue el script personalizado para instalar RStudio.</span><span class="sxs-lookup"><span data-stu-id="b088d-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="b088d-133">Use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b088d-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="b088d-134">Cambie los permisos en el archivo de script personalizado y ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="b088d-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="b088d-135">Use los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b088d-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="b088d-136">Si utiliza una contraseña SSH al crear un clúster de HDInsight con el servidor de R, puede omitir este paso y continuar en el siguiente.</span><span class="sxs-lookup"><span data-stu-id="b088d-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="b088d-137">Si en su lugar utiliza una clave SSH para crear el clúster, debe establecer una contraseña para el usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="b088d-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="b088d-138">Necesita esta contraseña para conectarse a RStudio.</span><span class="sxs-lookup"><span data-stu-id="b088d-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="b088d-139">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b088d-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="b088d-140">Cuando se le pida la **contraseña Kerberos actual**, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b088d-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="b088d-141">Tenga en cuenta que debe reemplazar `USERNAME` por un usuario SSH de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b088d-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="b088d-142">Si la contraseña se estableció correctamente, verá el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="b088d-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="b088d-143">Salga de la sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="b088d-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="b088d-144">Cree un túnel SSH al clúster asignando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` en el clúster de HDInsight al equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="b088d-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="b088d-145">Debe crear un túnel SSH antes de abrir una nueva sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="b088d-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="b088d-146">En un cliente de Linux o de Windows con [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra una sesión de terminal y use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b088d-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="b088d-147">Reemplace **USERNAME** por un usuario SSH para su clúster de HDInsight y reemplace **CLUSTERNAME** por el nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b088d-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="b088d-148">También puede usar una clave SSH en lugar de una contraseña agregando `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="b088d-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="b088d-149">Si usa un cliente de Windows con PuTTY:</span><span class="sxs-lookup"><span data-stu-id="b088d-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="b088d-150">Abra PuTTY y escriba la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="b088d-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="b088d-151">En la sección **Category** (Categoría) a la izquierda del cuadro de diálogo, expanda **Connection** (Conexión), **SSH** y, a continuación, seleccione **Tunnels** (Túneles).</span><span class="sxs-lookup"><span data-stu-id="b088d-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="b088d-152">Proporcione la siguiente información en el formulario **Options controlling SSH port forwarding** (Opciones que controlan el desvío de puertos SSH):</span><span class="sxs-lookup"><span data-stu-id="b088d-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="b088d-153">**Source port** : el puerto en el cliente que desea desviar.</span><span class="sxs-lookup"><span data-stu-id="b088d-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="b088d-154">Por ejemplo, **8787**.</span><span class="sxs-lookup"><span data-stu-id="b088d-154">For example, **8787**.</span></span>
        * <span data-ttu-id="b088d-155">**Destino** : el destino que debe asignarse al equipo cliente local.</span><span class="sxs-lookup"><span data-stu-id="b088d-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="b088d-156">Por ejemplo, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="b088d-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="b088d-157">![Creación de un túnel de SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Creación de un túnel de SSH")</span><span class="sxs-lookup"><span data-stu-id="b088d-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="b088d-158">Haga clic en **Add** (Agregar) para agregar la configuración y, a continuación, en **Open** (Abrir) para abrir una conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="b088d-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="b088d-159">Cuando se le solicite, inicie sesión en el servidor para establecer una sesión de SSH y habilite el túnel.</span><span class="sxs-lookup"><span data-stu-id="b088d-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="b088d-160">Abra un explorador web y escriba la siguiente dirección URL basada en el puerto especificado para el túnel:</span><span class="sxs-lookup"><span data-stu-id="b088d-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="b088d-161">Se le pedirá que escriba el nombre de usuario SSH y la contraseña para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="b088d-162">Si usó una clave SSH al crear el clúster, debe escribir la contraseña que creó en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="b088d-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="b088d-163">![Conexión a R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Creación de un túnel de SSH")</span><span class="sxs-lookup"><span data-stu-id="b088d-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="b088d-164">Para probar si la instalación de RStudio fue correcta, puede ejecutar un script de prueba que ejecute trabajos MapReduce y Spark basados en R en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b088d-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="b088d-165">Para descargar el script de prueba para su ejecución en RStudio, vuelva a la consola SSH y escriba los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b088d-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="b088d-166">Si creó un clúster de Hadoop con R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="b088d-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="b088d-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="b088d-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="b088d-168">Si creó un clúster de Spark con R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="b088d-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="b088d-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="b088d-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="b088d-170">En RStudio, verá el script de prueba que descargó.</span><span class="sxs-lookup"><span data-stu-id="b088d-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="b088d-171">Haga doble clic en el archivo para abrirlo, seleccione el contenido del archivo y haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="b088d-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="b088d-172">Debería ver la salida en el panel **Consola**:</span><span class="sxs-lookup"><span data-stu-id="b088d-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="b088d-173">![Prueba de la instalación](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Prueba de la instalación")</span><span class="sxs-lookup"><span data-stu-id="b088d-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="b088d-174">Otra opción sería escribir `source(testhdi.r)` o `source(testhdi_spark.r)` para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="b088d-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="b088d-175">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b088d-175">See also</span></span>

* [<span data-ttu-id="b088d-176">Opciones de contexto de proceso del servidor de R en HDInsight Premium</span><span class="sxs-lookup"><span data-stu-id="b088d-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="b088d-177">Opciones de Azure Storage para R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b088d-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

