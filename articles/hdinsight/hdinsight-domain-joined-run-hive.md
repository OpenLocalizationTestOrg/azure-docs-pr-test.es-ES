---
title: aaaConfigure directivas de Hive en HDInsight Unidos a un dominio - Azure | Documentos de Microsoft
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
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="b2e74-103">Configuración de directivas de Hive en HDInsight unido a un dominio (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b2e74-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="b2e74-104">Obtenga información acerca de cómo las directivas de Apache Cazador tooconfigure de Hive.</span><span class="sxs-lookup"><span data-stu-id="b2e74-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="b2e74-105">En este artículo, cree dos Cazador directivas toorestrict acceso toohello hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="b2e74-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="b2e74-106">Hola hivesampletable viene con clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2e74-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="b2e74-107">Después de haber configurado las directivas de hello, use Excel y ODBC driver tooconnect tooHive las tablas de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2e74-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2e74-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b2e74-108">Prerequisites</span></span>
* <span data-ttu-id="b2e74-109">Un clúster de HDInsight unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="b2e74-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="b2e74-110">Consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="b2e74-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b2e74-111">Un equipo con Office 2016, Office 2013 Professional Plus, Office 2013 Pro Plus, Excel 365 Standalone u Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="b2e74-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="b2e74-112">Conectar tooApache interfaz de usuario de administrador de Cazador</span><span class="sxs-lookup"><span data-stu-id="b2e74-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="b2e74-113">**tooconnect tooRanger administrador UI**</span><span class="sxs-lookup"><span data-stu-id="b2e74-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="b2e74-114">En un explorador, conéctese tooRanger administrador UI.</span><span class="sxs-lookup"><span data-stu-id="b2e74-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="b2e74-115">Hola URL es https://&lt;ClusterName >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="b2e74-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b2e74-116">Ranger usa credenciales diferentes de clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b2e74-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="b2e74-117">exploradores tooprevent utilizando credenciales almacenadas en caché de Hadoop, utilice nuevo navegador inprivate ventana tooconnect toohello interfaz de usuario de administrador de Cazador.</span><span class="sxs-lookup"><span data-stu-id="b2e74-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="b2e74-118">Inicie sesión con la contraseña y nombre de usuario de dominio de administrador de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="b2e74-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Página principal de Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="b2e74-120">Actualmente, Ranger solo funciona con Yarn y Hive.</span><span class="sxs-lookup"><span data-stu-id="b2e74-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="b2e74-121">Creación de usuarios del dominio</span><span class="sxs-lookup"><span data-stu-id="b2e74-121">Create Domain users</span></span>
<span data-ttu-id="b2e74-122">En [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio), ha creado hiveruser1 y hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="b2e74-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="b2e74-123">Se usará la cuenta de usuario de dos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b2e74-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="b2e74-124">Creación de directivas de Ranger</span><span class="sxs-lookup"><span data-stu-id="b2e74-124">Create Ranger policies</span></span>
<span data-ttu-id="b2e74-125">En esta sección creará dos directivas Ranger para acceder a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="b2e74-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="b2e74-126">Se concede el permiso select en un conjunto diferente de columnas.</span><span class="sxs-lookup"><span data-stu-id="b2e74-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="b2e74-127">Ambos usuarios se crearon en [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="b2e74-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="b2e74-128">En la siguiente sección hello, probará dos directivas de hello en Excel.</span><span class="sxs-lookup"><span data-stu-id="b2e74-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="b2e74-129">**directivas de Cazador toocreate**</span><span class="sxs-lookup"><span data-stu-id="b2e74-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="b2e74-130">Abra la interfaz de usuario administrador de Ranger.</span><span class="sxs-lookup"><span data-stu-id="b2e74-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="b2e74-131">Vea [conectar tooApache interfaz de usuario de administrador de Cazador](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="b2e74-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="b2e74-132">Haga clic en **&lt;nombreDeClúster>_hive**, en **Hive**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="b2e74-133">Deben aparecer dos directivas preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="b2e74-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="b2e74-134">Haga clic en **agregar nueva directiva**y, a continuación, escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="b2e74-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="b2e74-135">Nombre de directiva: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="b2e74-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="b2e74-136">Base de datos de Hive: default</span><span class="sxs-lookup"><span data-stu-id="b2e74-136">Hive Database: default</span></span>
   * <span data-ttu-id="b2e74-137">tabla: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b2e74-137">table: hivesampletable</span></span>
   * <span data-ttu-id="b2e74-138">Columna de Hive: *</span><span class="sxs-lookup"><span data-stu-id="b2e74-138">Hive column: *</span></span>
   * <span data-ttu-id="b2e74-139">Seleccionar usuario: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="b2e74-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="b2e74-140">Permisos: select</span><span class="sxs-lookup"><span data-stu-id="b2e74-140">Permissions: select</span></span>

     ![Configuración de políticas de Hive para Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="b2e74-142">.</span><span class="sxs-lookup"><span data-stu-id="b2e74-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b2e74-143">Si un usuario de dominio no se rellena en Seleccionar usuarios, espere unos minutos para Cazador toosync con AAD.</span><span class="sxs-lookup"><span data-stu-id="b2e74-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="b2e74-144">Haga clic en **agregar** toosave directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2e74-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="b2e74-145">Repita Hola dos últimos pasos toocreate otra directiva con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="b2e74-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="b2e74-146">Nombre de directiva: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="b2e74-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="b2e74-147">Base de datos de Hive: default</span><span class="sxs-lookup"><span data-stu-id="b2e74-147">Hive Database: default</span></span>
   * <span data-ttu-id="b2e74-148">tabla: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b2e74-148">table: hivesampletable</span></span>
   * <span data-ttu-id="b2e74-149">Columna de Hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="b2e74-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="b2e74-150">Seleccionar usuario: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="b2e74-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="b2e74-151">Permisos: select</span><span class="sxs-lookup"><span data-stu-id="b2e74-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="b2e74-152">Creación de un origen de datos de Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="b2e74-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="b2e74-153">Encontrará instrucciones de Hello en [origen de datos ODBC de Hive crear](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="b2e74-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="b2e74-154">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b2e74-154">Property</span></span>|<span data-ttu-id="b2e74-155">Description</span><span class="sxs-lookup"><span data-stu-id="b2e74-155">Description</span></span>
    ---|---
    <span data-ttu-id="b2e74-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="b2e74-156">Data Source Name</span></span>|<span data-ttu-id="b2e74-157">Proporcionar a un origen de datos de nombre tooyour</span><span class="sxs-lookup"><span data-stu-id="b2e74-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="b2e74-158">Host</span><span class="sxs-lookup"><span data-stu-id="b2e74-158">Host</span></span>|<span data-ttu-id="b2e74-159">Escriba &lt;NombreClústerHDInsight>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="b2e74-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="b2e74-160">Por ejemplo, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="b2e74-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="b2e74-161">Port</span><span class="sxs-lookup"><span data-stu-id="b2e74-161">Port</span></span>|<span data-ttu-id="b2e74-162">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="b2e74-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="b2e74-163">(Este puerto se ha cambiado de too443 563).</span><span class="sxs-lookup"><span data-stu-id="b2e74-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="b2e74-164">Base de datos</span><span class="sxs-lookup"><span data-stu-id="b2e74-164">Database</span></span>|<span data-ttu-id="b2e74-165">Use el <strong>valor predeterminado</strong></span><span class="sxs-lookup"><span data-stu-id="b2e74-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="b2e74-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="b2e74-166">Hive Server Type</span></span>|<span data-ttu-id="b2e74-167">Seleccione <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="b2e74-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="b2e74-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="b2e74-168">Mechanism</span></span>|<span data-ttu-id="b2e74-169">Seleccione <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="b2e74-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="b2e74-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="b2e74-170">HTTP Path</span></span>|<span data-ttu-id="b2e74-171">Deje este parámetro en blanco.</span><span class="sxs-lookup"><span data-stu-id="b2e74-171">Leave it blank.</span></span>
    <span data-ttu-id="b2e74-172">User Name</span><span class="sxs-lookup"><span data-stu-id="b2e74-172">User Name</span></span>|<span data-ttu-id="b2e74-173">Escriba hiveuser1@contoso158.onmicrosoft.com. Actualizar nombre de dominio de hello si es diferente.</span><span class="sxs-lookup"><span data-stu-id="b2e74-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="b2e74-174">Password</span><span class="sxs-lookup"><span data-stu-id="b2e74-174">Password</span></span>|<span data-ttu-id="b2e74-175">Escriba la contraseña de Hola para hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="b2e74-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="b2e74-176">Asegúrese de que tooclick **prueba** antes de guardar el origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2e74-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="b2e74-177">Importación de datos en Excel desde HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2e74-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="b2e74-178">En la última sección de hello, configurar dos directivas.</span><span class="sxs-lookup"><span data-stu-id="b2e74-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="b2e74-179">hiveuser1 tiene Hola permiso select en todas las columnas de Hola y hiveuser2 tiene Hola permiso select en dos columnas.</span><span class="sxs-lookup"><span data-stu-id="b2e74-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="b2e74-180">En esta sección, se suplantan Hola dos usuarios tooimport los datos en Excel.</span><span class="sxs-lookup"><span data-stu-id="b2e74-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="b2e74-181">Abra un libro de Excel nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="b2e74-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="b2e74-182">De hello **datos** , haga clic en **desde otros orígenes de datos**y, a continuación, haga clic en **desde el Asistente para la conexión de datos** toolaunch hello **Asistente para la conexión de datos**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="b2e74-183">![Abrir el Asistente para la conexión de datos][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="b2e74-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="b2e74-184">Seleccione **DSN de ODBC** como origen de datos de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="b2e74-185">Orígenes de datos ODBC, Hola Seleccione origen de datos nombre que creó en el paso anterior de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="b2e74-186">Volver a escribir contraseña de Hola para clúster hello en el Asistente de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="b2e74-187">Espere hello **Seleccionar base de datos y tabla** tooopen del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2e74-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="b2e74-188">Esta operación puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="b2e74-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="b2e74-189">Seleccione **hivesampletable** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="b2e74-190">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="b2e74-190">Click **Finish**.</span></span>
8. <span data-ttu-id="b2e74-191">Hola **importar datos** cuadro de diálogo, puede cambiar o especificar consultas Hola.</span><span class="sxs-lookup"><span data-stu-id="b2e74-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="b2e74-192">por lo tanto, haga clic en la toodo **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="b2e74-193">Esta operación puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="b2e74-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="b2e74-194">Haga clic en hello **definición** texto del comando ficha hello es:</span><span class="sxs-lookup"><span data-stu-id="b2e74-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="b2e74-195">Directivas de Cazador Hola definiera, hiveuser1 tiene el permiso select en todas las columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2e74-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="b2e74-196">Por lo que esta consulta funciona con las credenciales del hiveuser1, pero no con las credenciales del hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="b2e74-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="b2e74-197">![Propiedades de conexión][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="b2e74-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="b2e74-198">Haga clic en **Aceptar** cuadro de diálogo de propiedades de conexión de Hola de tooclose.</span><span class="sxs-lookup"><span data-stu-id="b2e74-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="b2e74-199">Haga clic en **Aceptar** tooclose hello **importar datos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2e74-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="b2e74-200">Introducir la contraseña de Hola para hiveuser1 y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2e74-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="b2e74-201">Tarda unos segundos antes de que los datos lleguen tooExcel importado.</span><span class="sxs-lookup"><span data-stu-id="b2e74-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="b2e74-202">Cuando termine, verá 11 columnas de datos.</span><span class="sxs-lookup"><span data-stu-id="b2e74-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="b2e74-203">tootest Hola segunda directiva (lectura-hivesampletable-devicemake) que creó en la última sección de Hola</span><span class="sxs-lookup"><span data-stu-id="b2e74-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="b2e74-204">Agregue una nueva hoja de Excel.</span><span class="sxs-lookup"><span data-stu-id="b2e74-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="b2e74-205">Siga Hola último procedimiento tooimport Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="b2e74-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="b2e74-206">deberá tomar único cambio de Hello es credenciales del toouse hiveuser2 en lugar de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="b2e74-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="b2e74-207">Esto se producirá un error porque hiveuser2 sólo tiene dos columnas de toosee de permiso.</span><span class="sxs-lookup"><span data-stu-id="b2e74-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="b2e74-208">Deberá obtener Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="b2e74-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="b2e74-209">Seguimiento Hola mismo datos tooimport de procedimiento.</span><span class="sxs-lookup"><span data-stu-id="b2e74-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="b2e74-210">Esta vez, use las credenciales del hiveuser2 y modificar la instrucción select de Hola desde:</span><span class="sxs-lookup"><span data-stu-id="b2e74-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b2e74-211">a:</span><span class="sxs-lookup"><span data-stu-id="b2e74-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b2e74-212">Cuando termine, verá dos columnas de datos importados.</span><span class="sxs-lookup"><span data-stu-id="b2e74-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e74-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2e74-213">Next steps</span></span>
* <span data-ttu-id="b2e74-214">Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="b2e74-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b2e74-215">Para administrar los clústeres de HDInsight unidos a dominio, consulte [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Administración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="b2e74-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="b2e74-216">Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="b2e74-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="b2e74-217">Para conectarse de Hive mediante Hive JDBC, consulte [conectar tooHive en HDInsight de Azure con controlador de JDBC Hive Hola](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b2e74-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="b2e74-218">Para conectar tooHadoop de Excel con ODBC Hive, consulte [tooHadoop Excel conectarse con hello unidad Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b2e74-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="b2e74-219">Para conectar tooHadoop de Excel con Power Query, consulte [tooHadoop Excel conectarse mediante Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="b2e74-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
