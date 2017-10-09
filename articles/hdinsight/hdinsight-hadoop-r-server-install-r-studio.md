---
title: aaaInstall RStudio con el servidor de R en HDInsight - Azure | Documentos de Microsoft
description: "Cómo tooinstall RStudio con el servidor de R en HDInsight."
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="e2326-103">Instalación de RStudio con R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2326-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="e2326-104">Este artículo describe cómo tooinstall Hola (gratis) versión de comunidad de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) en el nodo de hello borde de un clúster con un script personalizado.</span><span class="sxs-lookup"><span data-stu-id="e2326-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="e2326-105">RStudio Server proporciona un IDE basado en explorador que pueden usar los clientes remotos y se utiliza ampliamente en Linux.</span><span class="sxs-lookup"><span data-stu-id="e2326-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="e2326-106">Hoy en día, hay varios entornos de desarrollo integrados (IDE) disponibles para R, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2326-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="e2326-107">[Herramientas de R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft</span><span class="sxs-lookup"><span data-stu-id="e2326-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="e2326-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="e2326-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="e2326-109">[StatET](http://www.walware.de/goto/statet) basado en Eclipse de Walware.</span><span class="sxs-lookup"><span data-stu-id="e2326-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="e2326-110">ventaja de Hola de instalar servidor de RStudio en el nodo de hello borde de un clúster de HDInsight es que proporciona una experiencia IDE completa para el desarrollo de Hola y ejecutar scripts de R a R Server en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="e2326-111">Esta configuración puede ser mucho más productiva que usan de manera predeterminada de hello consola de R.</span><span class="sxs-lookup"><span data-stu-id="e2326-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="e2326-112">procedimiento de Hello descrito en este artículo solo es pertinente si no ha seleccionado tooinstall edición community de servidor RStudio al aprovisionar el clúster.</span><span class="sxs-lookup"><span data-stu-id="e2326-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="e2326-113">Si se ha agregado durante el aprovisionamiento, a continuación, tooaccess, hacer clic en hello **R Server paneles** mosaico en hello Azure portal entrada para el clúster, a continuación, en hello **R Studio Server** icono.</span><span class="sxs-lookup"><span data-stu-id="e2326-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="e2326-114">Si lo prefiere toouse Hola comercial con licencia Pro versión del servidor de RStudio, debe seguir las instrucciones de instalación de Hola de [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="e2326-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="e2326-115">Si utiliza un clúster de HDInsight para el que se instaló R con hello [acción de secuencia de comandos de R de instalar](hdinsight-hadoop-r-scripts-linux.md), pasos de hello en este documento no funcionarán correctamente tal como requiere que un servidor de R en clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="e2326-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2326-116">Prerequisites</span></span>

* <span data-ttu-id="e2326-117">Un clúster de HDInsight de Azure con servidor de R instalado.</span><span class="sxs-lookup"><span data-stu-id="e2326-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="e2326-118">Para obtener instrucciones, consulte [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md)(Introducción a R Server en clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="e2326-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="e2326-119">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="e2326-119">An SSH client.</span></span> <span data-ttu-id="e2326-120">Para distribuciones de Linux y Unix o Macintosh OS X, Hola `ssh` comando se proporciona con el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="e2326-121">Para Windows, se recomienda [Cygwin](http://www.redhat.com/services/custom/cygwin/) con hello [opción OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), o [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="e2326-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="e2326-122">Instalar RStudio en un clúster de hello mediante un script personalizado</span><span class="sxs-lookup"><span data-stu-id="e2326-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="e2326-123">Estos son los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e2326-123">Here are hello steps:</span></span>

1. <span data-ttu-id="e2326-124">Identificar hello borde nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="e2326-125">Para un clúster de HDInsight con el servidor de R, siguiente es la convención de nomenclatura de hello para el nodo principal y el nodo del borde.</span><span class="sxs-lookup"><span data-stu-id="e2326-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="e2326-126">Nodo principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e2326-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="e2326-127">Nodo perimetral `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e2326-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="e2326-128">SSH en el nodo del borde Hola de clúster hello mediante el patrón de nomenclatura de hello proporcionado en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="e2326-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="e2326-129">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e2326-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e2326-130">Cuando lo haya hecho, se convierten en un usuario raíz en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="e2326-131">En la sesión de SSH de hello, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e2326-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="e2326-132">Descargue tooinstall de secuencia de comandos personalizada hello RStudio.</span><span class="sxs-lookup"><span data-stu-id="e2326-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="e2326-133">Usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e2326-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="e2326-134">Cambiar los permisos de hello en el archivo de script personalizado de hello y ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="e2326-135">Usar hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e2326-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="e2326-136">Si utiliza una contraseña SSH al crear un clúster de HDInsight con el servidor de R, puede omitir este paso y continuar toohello a continuación.</span><span class="sxs-lookup"><span data-stu-id="e2326-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="e2326-137">Si ha usado una clave SSH en su lugar, clúster de hello toocreate, debe establecer una contraseña para el usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="e2326-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="e2326-138">Necesitará esta contraseña cuando se conecte tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="e2326-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="e2326-139">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e2326-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="e2326-140">Cuando se le pida la **contraseña Kerberos actual**, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2326-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="e2326-141">Tenga en cuenta que debe reemplazar `USERNAME` por un usuario SSH de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2326-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="e2326-142">Si la contraseña se ha configurado correctamente, debería ver Hola siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="e2326-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="e2326-143">Salga de sesión SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="e2326-144">Crear un clúster de toohello de túnel SSH asignando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` en hello HDInsight el clúster toohello equipo de cliente.</span><span class="sxs-lookup"><span data-stu-id="e2326-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="e2326-145">Debe crear un túnel SSH antes de abrir una nueva sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="e2326-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="e2326-146">En un cliente Linux o un cliente de Windows con [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra una sesión de terminal y usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e2326-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="e2326-147">Reemplace **nombre de usuario** con un usuario SSH para el clúster de HDInsight y reemplazar **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2326-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="e2326-148">También puede usar una clave SSH en lugar de una contraseña agregando `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="e2326-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="e2326-149">Si usa un cliente de Windows con PuTTY:</span><span class="sxs-lookup"><span data-stu-id="e2326-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="e2326-150">Abra PuTTY y escriba la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="e2326-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="e2326-151">Hola **categoría** toohello de la sección izquierda del cuadro de diálogo de hello, expanda **conexión**, expanda **SSH**y, a continuación, seleccione **túneles**.</span><span class="sxs-lookup"><span data-stu-id="e2326-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="e2326-152">Proporcionar Hola siguiente información en hello **reenvío de puerto de opciones que controlan SSH** formulario:</span><span class="sxs-lookup"><span data-stu-id="e2326-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="e2326-153">**Puerto de origen** -Hola puerto en el cliente de Hola que desea tooforward.</span><span class="sxs-lookup"><span data-stu-id="e2326-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="e2326-154">Por ejemplo, **8787**.</span><span class="sxs-lookup"><span data-stu-id="e2326-154">For example, **8787**.</span></span>
        * <span data-ttu-id="e2326-155">**Destino** : hello destino que se debe asigna toohello equipo de cliente local.</span><span class="sxs-lookup"><span data-stu-id="e2326-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="e2326-156">Por ejemplo, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="e2326-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="e2326-157">![Creación de un túnel de SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Creación de un túnel de SSH")</span><span class="sxs-lookup"><span data-stu-id="e2326-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="e2326-158">Haga clic en **agregar** tooadd Hola configuración y, a continuación, haga clic en **abiertos** tooopen una conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="e2326-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="e2326-159">Cuando se le solicite, inicie sesión en toohello server tooestablish un túnel SSH Hola de sesión y habilitar.</span><span class="sxs-lookup"><span data-stu-id="e2326-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="e2326-160">Abra un explorador web y escriba Hola después de la dirección URL basada en el puerto de Hola que especificó para el túnel de hello:</span><span class="sxs-lookup"><span data-stu-id="e2326-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="e2326-161">Son tooenter solicitadas Hola SSH username y password tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="e2326-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="e2326-162">Si usa una clave SSH al crear el clúster de hello, debe escribir contraseña de Hola que creó en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="e2326-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="e2326-163">![Conectar visita Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "crear un túnel SSH")</span><span class="sxs-lookup"><span data-stu-id="e2326-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="e2326-164">tootest si hello RStudio instalación se realizó correctamente, puede ejecutar un script de prueba que ejecuta trabajos MapReduce y Spark en función de R en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="e2326-165">script de prueba de toodownload hello toorun en RStudio, Atrás toohello SSH consola e introduce Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e2326-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="e2326-166">Si creó un clúster de Hadoop con R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e2326-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="e2326-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="e2326-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="e2326-168">Si creó un clúster de Spark con R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e2326-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="e2326-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="e2326-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="e2326-170">En RStudio, verá Hola descargó el script de prueba.</span><span class="sxs-lookup"><span data-stu-id="e2326-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="e2326-171">Haga doble clic en hello tooopen de archivo, seleccione contenido de hello del archivo hello y, a continuación, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="e2326-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="e2326-172">Debería ver el resultado de hello en hello **consola** panel:</span><span class="sxs-lookup"><span data-stu-id="e2326-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="e2326-173">![Probar la instalación de hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "probar la instalación de Hola")</span><span class="sxs-lookup"><span data-stu-id="e2326-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="e2326-174">Otra opción sería tootype `source(testhdi.r)` o `source(testhdi_spark.r)` tooexecute script de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2326-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2326-175">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e2326-175">See also</span></span>

* [<span data-ttu-id="e2326-176">Opciones de contexto de proceso del servidor de R en HDInsight Premium</span><span class="sxs-lookup"><span data-stu-id="e2326-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="e2326-177">Opciones de Azure Storage para R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2326-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

