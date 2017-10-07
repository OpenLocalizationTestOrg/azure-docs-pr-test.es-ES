---
title: herramientas de aaaData Lake para Visual Studio con el espacio aislado de Hortonworks - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola herramientas de Azure Data Lake para Visual Studio con el espacio aislado de Hortonworks Hola ejecuta en una máquina virtual local. Con estas herramientas, puede crear y ejecutar trabajos de Hive y Pig en espacio aislado de hello y ver la salida de trabajo y el historial."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="75f01-104">Usar herramientas de Azure Data Lake de Hola para Visual Studio con hello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="75f01-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="75f01-105">Azure Data Lake incluye herramientas para trabajar con clústeres de Hadoop genéricos.</span><span class="sxs-lookup"><span data-stu-id="75f01-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="75f01-106">Este documento proporciona los pasos de hello necesitan las herramientas de Data Lake con toouse Hola Hola espacio aislado de Hortonworks que se ejecuta en una máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="75f01-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="75f01-107">Usar Hola espacio aislado de Hortonworks, podrá toowork con Hadoop localmente en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="75f01-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="75f01-108">Una vez que ha desarrollado una solución y desea toodeploy lo a escala, a continuación, puede mover clúster de HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="75f01-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75f01-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="75f01-109">Prerequisites</span></span>

* <span data-ttu-id="75f01-110">Hola espacio aislado de Hortonworks, ejecutándose en una máquina virtual en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="75f01-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="75f01-111">Este documento se ha escrito y probado con espacio aislado de Hola que se ejecuta en Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="75f01-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="75f01-112">Para obtener información sobre cómo configurar el espacio aislado de hello, vea hello [empezar a trabajar con el espacio aislado de Hortonworks Hola.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="75f01-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="75f01-113">.</span><span class="sxs-lookup"><span data-stu-id="75f01-113">document.</span></span>

* <span data-ttu-id="75f01-114">Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (cualquier edición).</span><span class="sxs-lookup"><span data-stu-id="75f01-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="75f01-115">Hola [Azure SDK para .NET](https://azure.microsoft.com/downloads/) 2.7.1 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="75f01-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="75f01-116">Hola [Data Lake de Azure tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="75f01-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="75f01-117">Configurar las contraseñas de espacio aislado de Hola</span><span class="sxs-lookup"><span data-stu-id="75f01-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="75f01-118">Asegúrese de que ese Hola que espacio aislado de Hortonworks está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="75f01-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="75f01-119">A continuación, siga los pasos de Hola Hola [empezar a trabajar en hello espacio aislado de Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento.</span><span class="sxs-lookup"><span data-stu-id="75f01-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="75f01-120">Estos pasos configuran contraseña Hola Hola SSH `root` cuenta y Hola Ambari `admin` cuenta.</span><span class="sxs-lookup"><span data-stu-id="75f01-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="75f01-121">Estas contraseñas se utilizan cuando se conecta el espacio aislado de toohello desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75f01-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="75f01-122">Conectar el espacio aislado de hello herramientas toohello</span><span class="sxs-lookup"><span data-stu-id="75f01-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="75f01-123">Abra Visual Studio, seleccione **Ver** y, luego, **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="75f01-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="75f01-124">De **Explorador de servidores**, contextual hello **HDInsight** entrada y, a continuación, seleccione **conectar tooHDInsight emulador**.</span><span class="sxs-lookup"><span data-stu-id="75f01-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Captura de pantalla del explorador de servidores, con Connect tooHDInsight emulador resaltado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="75f01-126">De hello **conectar tooHDInsight emulador** diálogo cuadro, escriba la contraseña de Hola que ha configurado para Ambari.</span><span class="sxs-lookup"><span data-stu-id="75f01-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="75f01-128">Seleccione **siguiente** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="75f01-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="75f01-129">Hola de uso **contraseña** contraseña de hello tooenter de campo que configuró para hello `root` cuenta.</span><span class="sxs-lookup"><span data-stu-id="75f01-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="75f01-130">Deje Hola otros campos en el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-130">Leave hello other fields at hello default value.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="75f01-132">Seleccione **siguiente** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="75f01-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="75f01-133">Espera para la validación de hello servicios toofinish.</span><span class="sxs-lookup"><span data-stu-id="75f01-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="75f01-134">En algunos casos, validación puede producirá un error y se le pedirá que configuración de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="75f01-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="75f01-135">Si se produce un error de validación, seleccione **actualización**y esperar a que para la configuración de Hola y comprobación de hello toofinish de servicio.</span><span class="sxs-lookup"><span data-stu-id="75f01-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el botón Actualizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="75f01-137">proceso de actualización de Hello usa Ambari toomodify hello toowhat de configuración de espacio aislado de Hortonworks se espera con herramientas de Data Lake Hola para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75f01-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="75f01-138">Después de la validación ha finalizado, seleccione **finalizar** toocomplete configuración.</span><span class="sxs-lookup"><span data-stu-id="75f01-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="75f01-139">![Captura de pantalla del cuadro de diálogo, con el botón Finalizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="75f01-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="75f01-140">Dependiendo de su entorno de desarrollo y Hola cantidad de memoria asignada de la máquina virtual de toohello la velocidad de hello, puede tomar varias tooconfigure minutos y validar los servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="75f01-141">Después de seguir estos pasos, ahora tiene un **clúster local de HDInsight** entrada en el Explorador de servidores, en hello **HDInsight** sección.</span><span class="sxs-lookup"><span data-stu-id="75f01-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="75f01-142">Escritura de una consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="75f01-142">Write a Hive query</span></span>

<span data-ttu-id="75f01-143">Hive proporciona un lenguaje de consultas de tipo SQL (HiveQL) para trabajar con datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="75f01-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="75f01-144">Uso Hola siguientes pasos le indican cómo toorun petición consultas en clúster local de Hola de toolearn.</span><span class="sxs-lookup"><span data-stu-id="75f01-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="75f01-145">En **Explorador de servidores**, haga clic en la entrada de hello para el clúster local de Hola que agregó anteriormente y, a continuación, seleccione **escribir una consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="75f01-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Captura de pantalla del Explorador de servidores, con la opción Escribir una consulta de Hive resaltada](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="75f01-147">Aparece una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="75f01-147">A new query window appears.</span></span> <span data-ttu-id="75f01-148">Aquí puede rápidamente escribir y enviar una consulta toohello local del clúster.</span><span class="sxs-lookup"><span data-stu-id="75f01-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="75f01-149">En la nueva ventana de consulta hello, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="75f01-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="75f01-150">consulta de hello toorun, seleccione **enviar** en parte superior de Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="75f01-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="75f01-151">Deje Hola otros valores (**lote** y el nombre del servidor) en valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Captura de pantalla de ventana de consulta, con el botón de envío de hello resaltado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="75f01-153">También puede utilizar menú desplegable de hello después demasiado**enviar** tooselect **avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="75f01-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="75f01-154">Opciones avanzadas permiten opciones adicionales de tooprovide cuando se envía el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="75f01-156">Tras enviar consulta hello, aparece el estado del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="75f01-157">estado del trabajo Hello muestra información sobre trabajo hello cuando se procesa por Hadoop.</span><span class="sxs-lookup"><span data-stu-id="75f01-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="75f01-158">**Estado del trabajo** muestra el estado de saludo del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="75f01-159">estado de Hola se actualiza periódicamente, o puede usar Hola actualizar icono toorefresh Hola estado manualmente.</span><span class="sxs-lookup"><span data-stu-id="75f01-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Captura de pantalla del cuadro de diálogo Vista de trabajos, con la opción Estado del trabajo resaltada](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="75f01-161">Después de hello **estado del trabajo** cambia demasiado**finalizado**, se muestra un gráfico acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="75f01-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="75f01-162">Este diagrama describe la ruta de acceso de ejecución de Hola que se determina mediante Tez al procesar la consulta de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="75f01-163">Tez es Hola predeterminado motor de ejecución Hive en clúster local de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75f01-164">Tez también es predeterminado de hello cuando utilizas clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="75f01-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="75f01-165">No es predeterminada de hello en HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="75f01-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="75f01-166">toouse no existe, debe agregar la línea hello `set hive.execution.engine = tez;` toohello a partir de la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="75f01-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="75f01-167">Hola de uso **salida del trabajo** vincular la salida de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="75f01-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="75f01-168">En este caso, es 823, número de Hola de filas de tabla de sample_08 Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="75f01-169">Puede ver información de diagnóstico sobre el trabajo de hello mediante hello **registro de trabajo** y **Descargar registro de YARN** vínculos.</span><span class="sxs-lookup"><span data-stu-id="75f01-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="75f01-170">También puede ejecutar trabajos de Hive interactivamente cambiando hello **lote** campo demasiado**Interactive**.</span><span class="sxs-lookup"><span data-stu-id="75f01-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="75f01-171">Luego, seleccione **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="75f01-171">Then select **Execute**.</span></span>

    ![Captura de pantalla de los botones Interactivo y Ejecutar resaltados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="75f01-173">Una consulta interactiva secuencias Hola registro de salida generado durante el procesamiento de toohello **HiveServer2 salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="75f01-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75f01-174">Hello información es Hola igual que está disponible en hello **registro de trabajo** vincular una vez que un trabajo ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="75f01-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Captura de pantalla del registro de salida](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="75f01-176">Creación de un proyecto de Hive</span><span class="sxs-lookup"><span data-stu-id="75f01-176">Create a Hive project</span></span>

<span data-ttu-id="75f01-177">También puede crear un proyecto que incluya varios scripts de Hive.</span><span class="sxs-lookup"><span data-stu-id="75f01-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="75f01-178">Utilizar un proyecto cuando haya relacionados con las secuencias de comandos o desea toostore scripts en un sistema de control de versiones.</span><span class="sxs-lookup"><span data-stu-id="75f01-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="75f01-179">En Visual Studio, seleccione **Archivo**, **Nuevo** y **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="75f01-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="75f01-180">En la lista Hola de proyectos, expanda **plantillas**, expanda **Azure Data Lake**y, a continuación, seleccione **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="75f01-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="75f01-181">En la lista Hola de plantillas, seleccione **ejemplo Hive**.</span><span class="sxs-lookup"><span data-stu-id="75f01-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="75f01-182">Escriba un nombre y una ubicación y, luego, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="75f01-182">Enter a name and location, and then select **OK**.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, HIVE, Ejemplo de Hive y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="75f01-184">Hola **ejemplo Hive** proyecto contiene dos secuencias de comandos, **WebLogAnalysis.hql** y **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="75f01-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="75f01-185">Puede enviar estas secuencias de comandos mediante el uso de Hola mismo **enviar** situado en la parte superior de Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="75f01-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="75f01-186">Creación de un proyecto de Pig</span><span class="sxs-lookup"><span data-stu-id="75f01-186">Create a Pig project</span></span>

<span data-ttu-id="75f01-187">Aunque Hive proporciona un lenguaje similar a SQL para trabajar con datos estructurados, Pig funciona mediante la realización de transformaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="75f01-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="75f01-188">Pig proporciona un idioma (latino Pig) que le permite toodevelop una canalización de transformaciones.</span><span class="sxs-lookup"><span data-stu-id="75f01-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="75f01-189">toouse Pig con hello local del clúster, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="75f01-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="75f01-190">Abra Visual Studio y seleccione **Archivo**, **Nuevo** y **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="75f01-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="75f01-191">En la lista Hola de proyectos, expanda **plantillas**, expanda **Azure Data Lake**y, a continuación, seleccione **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="75f01-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="75f01-192">En la lista Hola de plantillas, seleccione **aplicación Pig**.</span><span class="sxs-lookup"><span data-stu-id="75f01-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="75f01-193">Escriba un nombre y una ubicación, y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="75f01-193">Enter a name, location, and then select **OK**.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, Pig, Aplicación Pig y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="75f01-195">Escriba Hola después de texto como contenido de Hola de hello **script.pig** archivo que se creó con este proyecto.</span><span class="sxs-lookup"><span data-stu-id="75f01-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="75f01-196">Mientras Pig usa un lenguaje distinto de Hive, cómo ejecutar trabajos de hello es coherente entre ambos lenguajes a través de hello **enviar** botón.</span><span class="sxs-lookup"><span data-stu-id="75f01-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="75f01-197">Hola de selección desplegable situada junto a **enviar** muestra un cuadro de diálogo Enviar avanzada de Pig.</span><span class="sxs-lookup"><span data-stu-id="75f01-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="75f01-199">También se muestra la salida y el estado del trabajo de hello, Hola mismo como una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="75f01-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Captura de pantalla de un trabajo de Pig finalizado](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="75f01-201">Vista de trabajos</span><span class="sxs-lookup"><span data-stu-id="75f01-201">View jobs</span></span>

<span data-ttu-id="75f01-202">Herramientas de Data Lake le permiten ver información acerca de los trabajos que se han ejecutado en Hadoop de tooeasily.</span><span class="sxs-lookup"><span data-stu-id="75f01-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="75f01-203">Use Hola siguientes pasos le indican los trabajos de hello toosee que se han ejecutado en el clúster local de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="75f01-204">De **Explorador de servidores**, haga clic en el clúster local de hello y, a continuación, seleccione **ver trabajos**.</span><span class="sxs-lookup"><span data-stu-id="75f01-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="75f01-205">Se muestra una lista de trabajos que se han enviado toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="75f01-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Captura de pantalla del Explorador de servidores, con la opción Ver trabajos resaltada](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="75f01-207">En lista de Hola de trabajos, seleccione uno de detalles del trabajo tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Captura de pantalla del explorador trabajo con uno de los trabajos de hello resaltados](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="75f01-209">información de Hola que aparece es similar toowhat que verá después de ejecutar una consulta de Pig o Hive, incluidos vínculos tooview Hola resultados y registro de la información.</span><span class="sxs-lookup"><span data-stu-id="75f01-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="75f01-210">También puede modificar y volver a enviar el trabajo de Hola desde aquí.</span><span class="sxs-lookup"><span data-stu-id="75f01-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="75f01-211">Vista de bases de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="75f01-211">View Hive databases</span></span>

1. <span data-ttu-id="75f01-212">En **Explorador de servidores**, expanda hello **clúster local de HDInsight** entrada y, a continuación, expanda **bases de datos de Hive**.</span><span class="sxs-lookup"><span data-stu-id="75f01-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="75f01-213">Hola **predeterminado** y **xademo** se muestran las bases de datos en clúster local de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="75f01-214">Expandir una base de datos muestra tablas Hola dentro de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Captura de pantalla del Explorador de servidores, con las bases de datos expandidas](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="75f01-216">Al expandir una tabla, muestran columnas Hola de dicha tabla.</span><span class="sxs-lookup"><span data-stu-id="75f01-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="75f01-217">tooquickly ver datos de hello, haga clic en una tabla y seleccione **vista Top 100 Rows**.</span><span class="sxs-lookup"><span data-stu-id="75f01-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Captura de pantalla del Explorador de servidores, con una tabla expandida y la opción Ver las 100 primeras filas seleccionada](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="75f01-219">Propiedades de las bases de datos y de las tablas</span><span class="sxs-lookup"><span data-stu-id="75f01-219">Database and table properties</span></span>

<span data-ttu-id="75f01-220">Puede ver propiedades de Hola de una base de datos o una tabla.</span><span class="sxs-lookup"><span data-stu-id="75f01-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="75f01-221">Seleccionar **propiedades** muestra los detalles de elemento de hello seleccionado en la ventana de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="75f01-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="75f01-222">Por ejemplo, ver la información de Hola que se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="75f01-222">For example, see hello information shown in hello following screenshot:</span></span>

![Captura de pantalla de la ventana Propiedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="75f01-224">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="75f01-224">Create a table</span></span>

<span data-ttu-id="75f01-225">toocreate una tabla, haga clic en una base de datos y, a continuación, seleccione **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="75f01-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Captura de pantalla del Explorador de servidores, con la opción Crear tabla resaltada](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="75f01-227">A continuación, puede crear tabla Hola usando un formulario.</span><span class="sxs-lookup"><span data-stu-id="75f01-227">You can then create hello table using a form.</span></span> <span data-ttu-id="75f01-228">En parte inferior de Hola de hello siguiente captura de pantalla, puede ver Hola HiveQL sin formato que es usado toocreate Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="75f01-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Captura de pantalla del formulario de hello usa toocreate una tabla](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="75f01-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75f01-230">Next steps</span></span>

* [<span data-ttu-id="75f01-231">Cables de Hola de aprendizaje de hello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="75f01-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="75f01-232">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="75f01-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
