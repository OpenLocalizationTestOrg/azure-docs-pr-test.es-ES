---
title: "Configuración de directivas de Hive en HDInsight unido a un dominio - Azure | Microsoft Docs"
description: Aprenda a...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="cb97d-103">Configuración de directivas de Hive en HDInsight unido a un dominio (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="cb97d-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="cb97d-104">Aprenda a configurar las directivas de Apache Ranger para Hive.</span><span class="sxs-lookup"><span data-stu-id="cb97d-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="cb97d-105">En este artículo, cree dos directivas Ranger para restringir el acceso a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="cb97d-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="cb97d-106">hivesampletable viene con los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb97d-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="cb97d-107">Una vez configuradas las directivas, utilice Excel y el controlador ODBC para conectarse a las tablas de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb97d-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb97d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb97d-108">Prerequisites</span></span>
* <span data-ttu-id="cb97d-109">Un clúster de HDInsight unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="cb97d-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="cb97d-110">Consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="cb97d-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="cb97d-111">Un equipo con Office 2016, Office 2013 Professional Plus, Office 2013 Pro Plus, Excel 365 Standalone u Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="cb97d-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="cb97d-112">Conexión a la interfaz de usuario administrador de Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="cb97d-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="cb97d-113">**Para conectarse a la interfaz de usuario administrador de Apache Ranger**</span><span class="sxs-lookup"><span data-stu-id="cb97d-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="cb97d-114">En un explorador, conéctese a la interfaz de usuario administrador de Ranger.</span><span class="sxs-lookup"><span data-stu-id="cb97d-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="cb97d-115">La dirección URL es https://&lt;nombreDeClúster>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="cb97d-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb97d-116">Ranger usa credenciales diferentes de clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cb97d-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="cb97d-117">Para evitar que los exploradores usen credenciales almacenadas en caché de Hadoop, use nueva ventana del explorador inprivate para conectarse a la interfaz de usuario administrador de Ranger.</span><span class="sxs-lookup"><span data-stu-id="cb97d-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="cb97d-118">Inicie sesión con el nombre de usuario y la contraseña del dominio del administrador de clúster:</span><span class="sxs-lookup"><span data-stu-id="cb97d-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Página principal de Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="cb97d-120">Actualmente, Ranger solo funciona con Yarn y Hive.</span><span class="sxs-lookup"><span data-stu-id="cb97d-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="cb97d-121">Creación de usuarios del dominio</span><span class="sxs-lookup"><span data-stu-id="cb97d-121">Create Domain users</span></span>
<span data-ttu-id="cb97d-122">En [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio), ha creado hiveruser1 y hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="cb97d-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="cb97d-123">Para este tutorial utilizará las dos cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="cb97d-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="cb97d-124">Creación de directivas de Ranger</span><span class="sxs-lookup"><span data-stu-id="cb97d-124">Create Ranger policies</span></span>
<span data-ttu-id="cb97d-125">En esta sección creará dos directivas Ranger para acceder a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="cb97d-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="cb97d-126">Se concede el permiso select en un conjunto diferente de columnas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="cb97d-127">Ambos usuarios se crearon en [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="cb97d-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="cb97d-128">En la siguiente sección probará las dos directivas en Excel.</span><span class="sxs-lookup"><span data-stu-id="cb97d-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="cb97d-129">**Para crear directivas de Ranger**</span><span class="sxs-lookup"><span data-stu-id="cb97d-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="cb97d-130">Abra la interfaz de usuario administrador de Ranger.</span><span class="sxs-lookup"><span data-stu-id="cb97d-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="cb97d-131">Consulte el artículo sobre la [conexión a la interfaz de usuario administrador de Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="cb97d-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="cb97d-132">Haga clic en **&lt;nombreDeClúster>_hive**, en **Hive**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="cb97d-133">Deben aparecer dos directivas preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="cb97d-134">Haga clic en **Agregar nueva directiva**, y escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="cb97d-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="cb97d-135">Nombre de directiva: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="cb97d-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="cb97d-136">Base de datos de Hive: default</span><span class="sxs-lookup"><span data-stu-id="cb97d-136">Hive Database: default</span></span>
   * <span data-ttu-id="cb97d-137">tabla: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="cb97d-137">table: hivesampletable</span></span>
   * <span data-ttu-id="cb97d-138">Columna de Hive: *</span><span class="sxs-lookup"><span data-stu-id="cb97d-138">Hive column: *</span></span>
   * <span data-ttu-id="cb97d-139">Seleccionar usuario: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="cb97d-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="cb97d-140">Permisos: select</span><span class="sxs-lookup"><span data-stu-id="cb97d-140">Permissions: select</span></span>

     ![Configuración de políticas de Hive para Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="cb97d-142">.</span><span class="sxs-lookup"><span data-stu-id="cb97d-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cb97d-143">Si un usuario de dominio no se rellena en Seleccionar usuario, espere unos instantes para que Ranger se sincronice con AAD.</span><span class="sxs-lookup"><span data-stu-id="cb97d-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="cb97d-144">Haga clic en **Agregar** para guardar la directiva.</span><span class="sxs-lookup"><span data-stu-id="cb97d-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="cb97d-145">Repita los dos últimos pasos para crear otra directiva con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="cb97d-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="cb97d-146">Nombre de directiva: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="cb97d-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="cb97d-147">Base de datos de Hive: default</span><span class="sxs-lookup"><span data-stu-id="cb97d-147">Hive Database: default</span></span>
   * <span data-ttu-id="cb97d-148">tabla: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="cb97d-148">table: hivesampletable</span></span>
   * <span data-ttu-id="cb97d-149">Columna de Hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="cb97d-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="cb97d-150">Seleccionar usuario: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="cb97d-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="cb97d-151">Permisos: select</span><span class="sxs-lookup"><span data-stu-id="cb97d-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="cb97d-152">Creación de un origen de datos de Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="cb97d-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="cb97d-153">Las instrucciones se pueden encontrar en el artículo sobre la [creación de origen de datos ODBC en Hive](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="cb97d-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="cb97d-154">Propiedad</span><span class="sxs-lookup"><span data-stu-id="cb97d-154">Property</span></span>|<span data-ttu-id="cb97d-155">Description</span><span class="sxs-lookup"><span data-stu-id="cb97d-155">Description</span></span>
    ---|---
    <span data-ttu-id="cb97d-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="cb97d-156">Data Source Name</span></span>|<span data-ttu-id="cb97d-157">Asigne un nombre al origen de datos</span><span class="sxs-lookup"><span data-stu-id="cb97d-157">Give a name to your data source</span></span>
    <span data-ttu-id="cb97d-158">Host</span><span class="sxs-lookup"><span data-stu-id="cb97d-158">Host</span></span>|<span data-ttu-id="cb97d-159">Escriba &lt;NombreClústerHDInsight>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="cb97d-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="cb97d-160">Por ejemplo, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="cb97d-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="cb97d-161">Port</span><span class="sxs-lookup"><span data-stu-id="cb97d-161">Port</span></span>|<span data-ttu-id="cb97d-162">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="cb97d-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="cb97d-163">(Este puerto se ha cambiado de 563 a 443).</span><span class="sxs-lookup"><span data-stu-id="cb97d-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="cb97d-164">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb97d-164">Database</span></span>|<span data-ttu-id="cb97d-165">Use el <strong>valor predeterminado</strong></span><span class="sxs-lookup"><span data-stu-id="cb97d-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="cb97d-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="cb97d-166">Hive Server Type</span></span>|<span data-ttu-id="cb97d-167">Seleccione <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="cb97d-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="cb97d-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="cb97d-168">Mechanism</span></span>|<span data-ttu-id="cb97d-169">Seleccione <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="cb97d-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="cb97d-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="cb97d-170">HTTP Path</span></span>|<span data-ttu-id="cb97d-171">Deje este parámetro en blanco.</span><span class="sxs-lookup"><span data-stu-id="cb97d-171">Leave it blank.</span></span>
    <span data-ttu-id="cb97d-172">User Name</span><span class="sxs-lookup"><span data-stu-id="cb97d-172">User Name</span></span>|<span data-ttu-id="cb97d-173">Escriba hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cb97d-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="cb97d-174">Actualice el nombre de dominio si es diferente.</span><span class="sxs-lookup"><span data-stu-id="cb97d-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="cb97d-175">Password</span><span class="sxs-lookup"><span data-stu-id="cb97d-175">Password</span></span>|<span data-ttu-id="cb97d-176">Escriba la contraseña de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="cb97d-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="cb97d-177">Haga clic **Prueba** antes de guardar el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="cb97d-178">Importación de datos en Excel desde HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb97d-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="cb97d-179">En la última sección ha configurado dos directivas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="cb97d-180">hiveuser1 tiene el permiso select en todas las columnas y hiveuser2, en dos columnas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="cb97d-181">En esta sección se suplanta a los dos usuarios para importar datos a Excel.</span><span class="sxs-lookup"><span data-stu-id="cb97d-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="cb97d-182">Abra un libro de Excel nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="cb97d-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="cb97d-183">En la pestaña **Datos**, haga clic en **From Other Data Sources** (Desde otros orígenes de datos) y en **Desde el Asistente para la conexión de datos** para iniciar el **Asistente para la conexión de datos**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="cb97d-184">![Abrir el Asistente para la conexión de datos][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="cb97d-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="cb97d-185">Seleccione **DSN ODBC** como origen de datos y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="cb97d-186">En los orígenes de datos ODBC, seleccione el nombre del origen de datos creado en el paso anterior y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="cb97d-187">Vuelva a escribir la contraseña para el clúster en el asistente y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="cb97d-188">Espere a que se abra el cuadro de diálogo **Seleccionar base de datos y tabla** .</span><span class="sxs-lookup"><span data-stu-id="cb97d-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="cb97d-189">Esta operación puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="cb97d-190">Seleccione **hivesampletable** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="cb97d-191">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cb97d-191">Click **Finish**.</span></span>
8. <span data-ttu-id="cb97d-192">En el cuadro de diálogo **Importar datos** , puede cambiar o especificar la consulta.</span><span class="sxs-lookup"><span data-stu-id="cb97d-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="cb97d-193">Para ello, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-193">To do so, click **Properties**.</span></span> <span data-ttu-id="cb97d-194">Esta operación puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="cb97d-195">Haga clic en la pestaña **Definición**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-195">Click the **Definition** tab.</span></span> <span data-ttu-id="cb97d-196">El texto del comando es:</span><span class="sxs-lookup"><span data-stu-id="cb97d-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="cb97d-197">Según las directivas de Ranger definidas, hiveuser1 tiene el permiso select en todas las columnas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="cb97d-198">Por lo que esta consulta funciona con las credenciales del hiveuser1, pero no con las credenciales del hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="cb97d-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="cb97d-199">![Propiedades de conexión][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="cb97d-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="cb97d-200">Haga clic en **Aceptar** para cerrar el cuadro de diálogo Propiedades de conexión.</span><span class="sxs-lookup"><span data-stu-id="cb97d-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="cb97d-201">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Importar datos**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="cb97d-202">Vuelva a escribir la contraseña de hiveuser1 y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cb97d-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="cb97d-203">La importación de los datos a Excel tarda algunos segundos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="cb97d-204">Cuando termine, verá 11 columnas de datos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="cb97d-205">Para probar la segunda directiva (read-hivesampletable-devicemake) que creó en la última sección</span><span class="sxs-lookup"><span data-stu-id="cb97d-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="cb97d-206">Agregue una nueva hoja de Excel.</span><span class="sxs-lookup"><span data-stu-id="cb97d-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="cb97d-207">Siga el último procedimiento para importar los datos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="cb97d-208">El único cambio que deberá hacer es usar las credenciales de hiveuser2 en lugar de las de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="cb97d-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="cb97d-209">Esto generará un error, ya que hiveuser2 solo tiene permiso para ver dos columnas.</span><span class="sxs-lookup"><span data-stu-id="cb97d-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="cb97d-210">Se producirá el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb97d-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="cb97d-211">Siga el mismo procedimiento para importar los datos.</span><span class="sxs-lookup"><span data-stu-id="cb97d-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="cb97d-212">Esta vez, utilice las credenciales de hiveuser2 y modifique la instrucción select de:</span><span class="sxs-lookup"><span data-stu-id="cb97d-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="cb97d-213">a:</span><span class="sxs-lookup"><span data-stu-id="cb97d-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="cb97d-214">Cuando termine, verá dos columnas de datos importados.</span><span class="sxs-lookup"><span data-stu-id="cb97d-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb97d-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb97d-215">Next steps</span></span>
* <span data-ttu-id="cb97d-216">Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="cb97d-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="cb97d-217">Para administrar los clústeres de HDInsight unidos a dominio, consulte [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Administración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="cb97d-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="cb97d-218">Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="cb97d-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="cb97d-219">Para conectar Hive mediante Hive JDBC, consulte [Conexión a Hive en HDInsight de Azure con el controlador JDBC de Hive](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="cb97d-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="cb97d-220">Para conectar Excel a Hadoop con Hive ODBC, consulte [Conexión de Excel a Hadoop con el controlador ODBC de Microsoft Hive](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="cb97d-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="cb97d-221">Para conectar Excel a Hadoop con Power Query, consulte [Conexión de Excel a Hadoop con Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="cb97d-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
