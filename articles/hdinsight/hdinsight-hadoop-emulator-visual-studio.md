---
title: Herramientas de Data Lake para Visual Studio con Sandbox de Hortonworks - Azure HDInsight | Microsoft Docs
description: "Aprenda a usar las herramientas de Azure Data Lake para Visual Studio con Sandbox de Hortonworks en ejecución en una máquina virtual local. Con estas herramientas puede crear y ejecutar trabajos de Hive y Pig en el espacio aislado, así como ver la salida de los trabajos y el historial."
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
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="070e6-104">Uso de las herramientas de Azure Data Lake para Visual Studio con Sandbox de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="070e6-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="070e6-105">Azure Data Lake incluye herramientas para trabajar con clústeres de Hadoop genéricos.</span><span class="sxs-lookup"><span data-stu-id="070e6-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="070e6-106">En este documento se proporcionan los pasos necesarios para usar las herramientas de Data Lake con Sandbox de Hortonworks en una máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="070e6-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="070e6-107">Mediante Sandbox de Hortonworks puede trabajar con Hadoop localmente en su entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="070e6-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="070e6-108">Una vez que haya desarrollado una solución y quiera implementarla a escala, puede desplazarse a un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="070e6-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="070e6-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="070e6-109">Prerequisites</span></span>

* <span data-ttu-id="070e6-110">Sandbox de Hortonworks en ejecución en una máquina virtual en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="070e6-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="070e6-111">Este documento se ha escrito y probado con el espacio aislado ejecutado en Oracle VirtualBox,</span><span class="sxs-lookup"><span data-stu-id="070e6-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="070e6-112">Para información sobre cómo configurar el espacio aislado, consulte el documento de [introducción al espacio aislado de Hortonworks](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="070e6-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="070e6-113">.</span><span class="sxs-lookup"><span data-stu-id="070e6-113">document.</span></span>

* <span data-ttu-id="070e6-114">Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (cualquier edición).</span><span class="sxs-lookup"><span data-stu-id="070e6-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="070e6-115">[Azure SDK para .NET](https://azure.microsoft.com/downloads/) 2.7.1 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="070e6-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="070e6-116">Las [herramientas de Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="070e6-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="070e6-117">Configuración de contraseñas para el espacio aislado</span><span class="sxs-lookup"><span data-stu-id="070e6-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="070e6-118">Asegúrese de que Sandbox de Hortonworks se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="070e6-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="070e6-119">A continuación, siga los pasos descritos en el documento de [introducción al espacio aislado de Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords).</span><span class="sxs-lookup"><span data-stu-id="070e6-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="070e6-120">Estos pasos configuran la contraseña de la cuenta `root` de SSH y de la cuenta `admin` de Ambari.</span><span class="sxs-lookup"><span data-stu-id="070e6-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="070e6-121">Estas contraseñas se usan al conectarse al espacio aislado desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="070e6-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="070e6-122">Conexión de las herramientas al espacio aislado</span><span class="sxs-lookup"><span data-stu-id="070e6-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="070e6-123">Abra Visual Studio, seleccione **Ver** y, luego, **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="070e6-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="070e6-124">En el **Explorador de servidores**, haga clic con el botón derecho en la entrada **HDInsight** y seleccione **Conectar con el emulador de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="070e6-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Captura de pantalla del Explorador de servidores, con la opción Conectar al emulador de HDInsight resaltada](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="070e6-126">En el cuadro de diálogo **Conectar al emulador de HDInsight**, escriba la contraseña que ha configurado para Ambari.</span><span class="sxs-lookup"><span data-stu-id="070e6-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="070e6-128">Seleccione **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="070e6-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="070e6-129">Use el campo **Contraseña** para escribir la contraseña configurada para la cuenta `root`.</span><span class="sxs-lookup"><span data-stu-id="070e6-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="070e6-130">Deje los demás campos con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="070e6-130">Leave the other fields at the default value.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el cuadro de texto de contraseña resaltado](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="070e6-132">Seleccione **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="070e6-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="070e6-133">Espere a que finalice la validación de los servicios.</span><span class="sxs-lookup"><span data-stu-id="070e6-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="070e6-134">En algunos casos, se puede producir un error de validación y se le pedirá que actualice la configuración.</span><span class="sxs-lookup"><span data-stu-id="070e6-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="070e6-135">Si se produce un error de validación, seleccione **Actualizar** y espere a que finalicen la configuración y la comprobación del servicio.</span><span class="sxs-lookup"><span data-stu-id="070e6-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![Captura de pantalla del cuadro de diálogo, con el botón Actualizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="070e6-137">El proceso de actualización usa Ambari para modificar la configuración de Sandbox de Hortonworks en función de lo que esperan las herramientas de Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="070e6-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="070e6-138">Una vez finalizada la validación, seleccione **Finalizar** para concluir la configuración.</span><span class="sxs-lookup"><span data-stu-id="070e6-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="070e6-139">![Captura de pantalla del cuadro de diálogo, con el botón Finalizar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="070e6-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="070e6-140">Según la velocidad del entorno de desarrollo y de la cantidad de memoria asignada a la máquina virtual, la configuración y validación de los servicios puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="070e6-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="070e6-141">Después de seguir estos pasos, tendrá una entrada **Clúster local de HDInsight** en la sección **HDInsight** del Explorador de servidores.</span><span class="sxs-lookup"><span data-stu-id="070e6-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="070e6-142">Escritura de una consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="070e6-142">Write a Hive query</span></span>

<span data-ttu-id="070e6-143">Hive proporciona un lenguaje de consultas de tipo SQL (HiveQL) para trabajar con datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="070e6-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="070e6-144">Use los pasos siguientes para aprender a ejecutar consultas a petición en el clúster local.</span><span class="sxs-lookup"><span data-stu-id="070e6-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="070e6-145">En el **Explorador de servidores**, haga clic con el botón derecho en la entrada del clúster local agregado anteriormente y, luego, seleccione **Escribir una consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="070e6-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Captura de pantalla del Explorador de servidores, con la opción Escribir una consulta de Hive resaltada](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="070e6-147">Aparece una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="070e6-147">A new query window appears.</span></span> <span data-ttu-id="070e6-148">Aquí puede escribir y enviar rápidamente una consulta al clúster local.</span><span class="sxs-lookup"><span data-stu-id="070e6-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="070e6-149">En la nueva ventana de consulta, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="070e6-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="070e6-150">Para ejecutar la consulta, seleccione **Enviar** en la parte superior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="070e6-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="070e6-151">Deje las demás opciones (**Lote** y el nombre del servidor) en los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="070e6-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![Captura de pantalla de la ventana de consulta, con el botón Enviar resaltado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="070e6-153">También puede usar el menú desplegable junto a **Enviar** para seleccionar **Avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="070e6-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="070e6-154">Las opciones avanzadas permiten proporcionar opciones adicionales al enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="070e6-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="070e6-156">Una vez enviada la consulta, aparece el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="070e6-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="070e6-157">El estado del trabajo muestra información sobre el trabajo mientras lo procesa Hadoop.</span><span class="sxs-lookup"><span data-stu-id="070e6-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="070e6-158">En **Estado del trabajo** se proporciona el estado actual del trabajo.</span><span class="sxs-lookup"><span data-stu-id="070e6-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="070e6-159">El estado se actualiza periódicamente, aunque también se puede usar el icono de actualización para actualizarlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="070e6-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![Captura de pantalla del cuadro de diálogo Vista de trabajos, con la opción Estado del trabajo resaltada](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="070e6-161">Cuando el **estado del trabajo** cambie a **Finalizado**, se mostrará un grafo acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="070e6-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="070e6-162">Este diagrama describe la ruta de acceso de ejecución que determina Tez al procesar la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="070e6-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="070e6-163">Tez es el motor de ejecución predeterminado para Hive en el clúster local.</span><span class="sxs-lookup"><span data-stu-id="070e6-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="070e6-164">También es el motor predeterminado cuando se usan clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="070e6-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="070e6-165">No es el motor predeterminado en los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="070e6-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="070e6-166">Para usarlo en Windows, debe agregar la línea `set hive.execution.engine = tez;` al principio de la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="070e6-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="070e6-167">Use el vínculo **Salida de trabajo** para ver la salida.</span><span class="sxs-lookup"><span data-stu-id="070e6-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="070e6-168">En este caso es 823, el número de filas de la tabla sample_08.</span><span class="sxs-lookup"><span data-stu-id="070e6-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="070e6-169">Puede ver información de diagnóstico sobre el trabajo mediante los vínculos **Registro de trabajo** y **Descargar registro YARN**.</span><span class="sxs-lookup"><span data-stu-id="070e6-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="070e6-170">También puede ejecutar trabajos de Hive de forma interactiva cambiando el campo **Lote** a **Interactivo**.</span><span class="sxs-lookup"><span data-stu-id="070e6-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="070e6-171">Luego, seleccione **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="070e6-171">Then select **Execute**.</span></span>

    ![Captura de pantalla de los botones Interactivo y Ejecutar resaltados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="070e6-173">Una consulta interactiva transmite el registro de salida generado durante el procesamiento a la ventana **Salida de HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="070e6-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="070e6-174">Es la misma información que está disponible en el vínculo **Registro de trabajo** una vez concluido un trabajo.</span><span class="sxs-lookup"><span data-stu-id="070e6-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![Captura de pantalla del registro de salida](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="070e6-176">Creación de un proyecto de Hive</span><span class="sxs-lookup"><span data-stu-id="070e6-176">Create a Hive project</span></span>

<span data-ttu-id="070e6-177">También puede crear un proyecto que incluya varios scripts de Hive.</span><span class="sxs-lookup"><span data-stu-id="070e6-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="070e6-178">Cuando tenga scripts relacionados o desee almacenar scripts en un sistema de control de versiones, use un proyecto.</span><span class="sxs-lookup"><span data-stu-id="070e6-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="070e6-179">En Visual Studio, seleccione **Archivo**, **Nuevo** y **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="070e6-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="070e6-180">En la lista de proyectos, expanda **Plantillas** y **Azure Data Lake** y, luego, seleccione **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="070e6-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="070e6-181">En la lista de plantillas, seleccione **Hive Sample**.</span><span class="sxs-lookup"><span data-stu-id="070e6-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="070e6-182">Escriba un nombre y una ubicación y, luego, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="070e6-182">Enter a name and location, and then select **OK**.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, HIVE, Ejemplo de Hive y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="070e6-184">El proyecto **Hive Sample** contiene dos scripts, **WebLogAnalysis.hql** y **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="070e6-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="070e6-185">Puede enviar estos scripts con el mismo botón **Enviar**, situado en la parte superior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="070e6-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="070e6-186">Creación de un proyecto de Pig</span><span class="sxs-lookup"><span data-stu-id="070e6-186">Create a Pig project</span></span>

<span data-ttu-id="070e6-187">Aunque Hive proporciona un lenguaje similar a SQL para trabajar con datos estructurados, Pig funciona mediante la realización de transformaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="070e6-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="070e6-188">Pig proporciona un lenguaje (Pig Latin) que le permite desarrollar una canalización de transformaciones.</span><span class="sxs-lookup"><span data-stu-id="070e6-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="070e6-189">Siga estos pasos para usar Pig con el clúster local:</span><span class="sxs-lookup"><span data-stu-id="070e6-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="070e6-190">Abra Visual Studio y seleccione **Archivo**, **Nuevo** y **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="070e6-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="070e6-191">En la lista de proyectos, expanda **Plantillas** y **Azure Data Lake** y, luego, seleccione **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="070e6-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="070e6-192">En la lista de plantillas, seleccione **Pig Application**.</span><span class="sxs-lookup"><span data-stu-id="070e6-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="070e6-193">Escriba un nombre y una ubicación, y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="070e6-193">Enter a name, location, and then select **OK**.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto, con las opciones Azure Data Lake, Pig, Aplicación Pig y Aceptar resaltadas](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="070e6-195">Escriba el siguiente texto como contenido del archivo **script.pig** que se creó con este proyecto.</span><span class="sxs-lookup"><span data-stu-id="070e6-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="070e6-196">Aunque Pig usa un lenguaje diferente que Hive, la forma de ejecutar los trabajos es la misma en ambos lenguajes mediante el botón **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="070e6-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="070e6-197">La selección de la lista desplegable situada junto a **Enviar** muestra un cuadro de diálogo de envío avanzado para Pig.</span><span class="sxs-lookup"><span data-stu-id="070e6-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="070e6-199">El estado y la salida de trabajo también se muestran del mismo modo que en una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="070e6-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![Captura de pantalla de un trabajo de Pig finalizado](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="070e6-201">Vista de trabajos</span><span class="sxs-lookup"><span data-stu-id="070e6-201">View jobs</span></span>

<span data-ttu-id="070e6-202">Las herramientas de Data Lake también le permiten ver fácilmente la información sobre los trabajos ejecutados en Hadoop.</span><span class="sxs-lookup"><span data-stu-id="070e6-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="070e6-203">Siga estos pasos para ver los trabajos que se han ejecutado en el clúster local.</span><span class="sxs-lookup"><span data-stu-id="070e6-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="070e6-204">En el **Explorador de servidores**, haga clic con el botón derecho en el clúster local y seleccione **Ver trabajos**.</span><span class="sxs-lookup"><span data-stu-id="070e6-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="070e6-205">Se muestra una lista de trabajos que se enviaron al clúster.</span><span class="sxs-lookup"><span data-stu-id="070e6-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![Captura de pantalla del Explorador de servidores, con la opción Ver trabajos resaltada](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="070e6-207">En la lista de trabajos, seleccione uno para ver los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="070e6-207">From the list of jobs, select one to view the job details.</span></span>

    ![Captura de pantalla del Explorador de trabajos, con uno de los trabajos resaltado](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="070e6-209">La información que aparece es similar a la que se ve después de ejecutar una consulta de Hive o Pig, junto con vínculos para ver la información de registro y de salida.</span><span class="sxs-lookup"><span data-stu-id="070e6-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="070e6-210">También puede modificar y volver a enviar el trabajo desde aquí.</span><span class="sxs-lookup"><span data-stu-id="070e6-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="070e6-211">Vista de bases de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="070e6-211">View Hive databases</span></span>

1. <span data-ttu-id="070e6-212">En el **Explorador de servidores**, expanda la entrada **Clúster local de HDInsight** y, luego, **Bases de datos de Hive**.</span><span class="sxs-lookup"><span data-stu-id="070e6-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="070e6-213">Se muestran las bases de datos **Predeterminada** y **xademo** en el clúster local.</span><span class="sxs-lookup"><span data-stu-id="070e6-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="070e6-214">Al expandir una base de datos se muestran las tablas que hay dentro de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="070e6-214">Expanding a database shows the tables within the database.</span></span>

    ![Captura de pantalla del Explorador de servidores, con las bases de datos expandidas](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="070e6-216">La expansión de una tabla muestra las columnas de esa tabla.</span><span class="sxs-lookup"><span data-stu-id="070e6-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="070e6-217">Si quiere ver los datos rápidamente, haga clic con el botón derecho en una tabla y seleccione **Ver las 100 primeras filas**.</span><span class="sxs-lookup"><span data-stu-id="070e6-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Captura de pantalla del Explorador de servidores, con una tabla expandida y la opción Ver las 100 primeras filas seleccionada](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="070e6-219">Propiedades de las bases de datos y de las tablas</span><span class="sxs-lookup"><span data-stu-id="070e6-219">Database and table properties</span></span>

<span data-ttu-id="070e6-220">Puede ver las propiedades de una base de datos o de una tabla.</span><span class="sxs-lookup"><span data-stu-id="070e6-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="070e6-221">Al seleccionar **Propiedades** se muestran los detalles del elemento seleccionado en la ventana de propiedades.</span><span class="sxs-lookup"><span data-stu-id="070e6-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="070e6-222">Por ejemplo, puede ver la información que se muestra en la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="070e6-222">For example, see the information shown in the following screenshot:</span></span>

![Captura de pantalla de la ventana Propiedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="070e6-224">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="070e6-224">Create a table</span></span>

<span data-ttu-id="070e6-225">Para crear una tabla, haga clic con el botón derecho en una base de datos y seleccione **Crear tabla**.</span><span class="sxs-lookup"><span data-stu-id="070e6-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![Captura de pantalla del Explorador de servidores, con la opción Crear tabla resaltada](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="070e6-227">Ya puede crear la tabla usando un formulario.</span><span class="sxs-lookup"><span data-stu-id="070e6-227">You can then create the table using a form.</span></span> <span data-ttu-id="070e6-228">En la parte inferior de la siguiente captura de pantalla puede ver el script HiveQL sin formato que se usa para crear la tabla.</span><span class="sxs-lookup"><span data-stu-id="070e6-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![Captura de pantalla del formulario usado para crear una tabla](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="070e6-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="070e6-230">Next steps</span></span>

* [<span data-ttu-id="070e6-231">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="070e6-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="070e6-232">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="070e6-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
