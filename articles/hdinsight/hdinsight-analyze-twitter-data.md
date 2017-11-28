---
title: aaaAnalyze datos de Twitter con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hive tooanalyze Twitter datos en Hadoop en HDInsight toofind Hola frecuencia de uso de una palabra determinada."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="6dd48-103">Análisis de datos de Twitter con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd48-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="6dd48-104">Sitios Web sociales es una de las fuerzas principales de conducción hello para la adopción de grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="6dd48-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="6dd48-105">Las API públicas proporcionadas por sitios como Twitter constituyen un origen de datos muy útil para analizar y comprender las tendencias populares.</span><span class="sxs-lookup"><span data-stu-id="6dd48-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="6dd48-106">En este tutorial, se obtendrá tweets mediante el uso de una API de transmisión por secuencias de Twitter y, a continuación, usar Apache Hive en HDInsight de Azure tooget una lista de usuarios de Twitter que envían Hola tweets mayoría que contenía una palabra determinada.</span><span class="sxs-lookup"><span data-stu-id="6dd48-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dd48-107">Hello pasos de este documento requieren un clúster de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="6dd48-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="6dd48-108">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="6dd48-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6dd48-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6dd48-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6dd48-110">Para clúster pasos tooa específicos basados en Linux, consulte [Twitter analizar datos con Hive en HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6dd48-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dd48-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6dd48-111">Prerequisites</span></span>
<span data-ttu-id="6dd48-112">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6dd48-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="6dd48-113">**Una estación de trabajo** con Powershell de Azure instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="6dd48-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="6dd48-114">tooexecute secuencias de comandos de Windows PowerShell, debe ejecutar Azure PowerShell como administrador y establecer la directiva de ejecución de hello demasiado*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="6dd48-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="6dd48-115">Consulte [Ejecución de scripts de Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="6dd48-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="6dd48-116">Antes de ejecutar scripts de Windows PowerShell, asegúrese de que están conectado tooyour suscripción de Azure mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6dd48-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="6dd48-117">Si tiene varias suscripciones de Azure, use Hola después de la suscripción actual de cmdlet tooset hello:</span><span class="sxs-lookup"><span data-stu-id="6dd48-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="6dd48-118">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="6dd48-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="6dd48-119">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd48-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="6dd48-120">Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd48-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="6dd48-121">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="6dd48-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="6dd48-122">**Un clúster de HDInsight de Azure**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="6dd48-123">Para obtener instrucciones sobre el aprovisionamiento del clúster, consulte [Introducción al uso de HDInsight][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="6dd48-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="6dd48-124">Necesitará el nombre de clúster de hello más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="6dd48-125">Hello siguiente tabla enumeran Hola archivos utilizados en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="6dd48-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="6dd48-126">Archivos</span><span class="sxs-lookup"><span data-stu-id="6dd48-126">Files</span></span> | <span data-ttu-id="6dd48-127">Description</span><span class="sxs-lookup"><span data-stu-id="6dd48-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6dd48-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="6dd48-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="6dd48-129">datos de origen de Hello para el trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="6dd48-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="6dd48-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="6dd48-131">carpeta de salida de Hello de trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="6dd48-132">Hola nombre de archivo de salida de trabajo de Hive de predeterminada es **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="6dd48-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="6dd48-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="6dd48-134">archivo de script de HiveQL Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="6dd48-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="6dd48-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="6dd48-136">Hola estado del trabajo de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6dd48-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="6dd48-137">Obtención de una fuente de Twitter</span><span class="sxs-lookup"><span data-stu-id="6dd48-137">Get Twitter feed</span></span>
<span data-ttu-id="6dd48-138">En este tutorial, utilizará hello [API de transmisión por secuencias de Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="6dd48-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="6dd48-139">Hola específico Twitter streaming API que se va a usar es [Estados/filtro][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="6dd48-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="6dd48-140">Un archivo que contiene 10.000 tweets y archivo de script de Hive hello (que se describe en la sección siguiente Hola) se han cargado en un contenedor de Blob público.</span><span class="sxs-lookup"><span data-stu-id="6dd48-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="6dd48-141">Puede omitir esta sección si desea toouse Hola cargar archivos.</span><span class="sxs-lookup"><span data-stu-id="6dd48-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="6dd48-142">[TWEETS datos](https://dev.twitter.com/docs/platform-objects/tweets) se almacena en formato JavaScript Object Notation (JSON) de Hola que contiene una estructura anidada compleja.</span><span class="sxs-lookup"><span data-stu-id="6dd48-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="6dd48-143">En lugar de escribir varias líneas de código con un lenguaje de programación convencional, puede transformar esta estructura anidada en una tabla de Hive para que se puedan realizar consultas a través de un lenguaje similar al Lenguaje de consulta estructurado (SQL) llamado HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6dd48-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="6dd48-144">Twitter usa OAuth tooprovide autorizado acceso tooits API.</span><span class="sxs-lookup"><span data-stu-id="6dd48-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="6dd48-145">OAuth es un protocolo de autenticación que permite a los usuarios tooapprove aplicaciones tooact en su nombre sin compartir su contraseña.</span><span class="sxs-lookup"><span data-stu-id="6dd48-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="6dd48-146">Puede encontrar más información en [oauth.net](http://oauth.net/) u Hola excelente [tooOAuth de guía para principiantes](http://hueniverse.com/oauth/) desde Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="6dd48-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="6dd48-147">Hola primer paso toouse OAuth es una nueva aplicación en el sitio para desarrolladores de Twitter hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6dd48-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="6dd48-148">**toocreate una aplicación de Twitter**</span><span class="sxs-lookup"><span data-stu-id="6dd48-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="6dd48-149">Inicie sesión en demasiado[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="6dd48-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="6dd48-150">Haga clic en hello **Regístrese ahora** vincular si no tienes una cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="6dd48-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="6dd48-151">Haga clic en **Crear nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="6dd48-152">Especifique los campos **Name** (Nombre), **Description** (Descripción), **Website** (Sitio web).</span><span class="sxs-lookup"><span data-stu-id="6dd48-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="6dd48-153">Se pueden realizar hasta una dirección URL para hello **sitio Web** campo.</span><span class="sxs-lookup"><span data-stu-id="6dd48-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="6dd48-154">Hello en la tabla siguiente muestra algunos toouse de valores de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6dd48-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="6dd48-155">Campo</span><span class="sxs-lookup"><span data-stu-id="6dd48-155">Field</span></span> | <span data-ttu-id="6dd48-156">Valor</span><span class="sxs-lookup"><span data-stu-id="6dd48-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="6dd48-157">Nombre</span><span class="sxs-lookup"><span data-stu-id="6dd48-157">Name</span></span> |<span data-ttu-id="6dd48-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="6dd48-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="6dd48-159">Description</span><span class="sxs-lookup"><span data-stu-id="6dd48-159">Description</span></span> |<span data-ttu-id="6dd48-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="6dd48-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="6dd48-161">Website</span><span class="sxs-lookup"><span data-stu-id="6dd48-161">Website</span></span> |<span data-ttu-id="6dd48-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="6dd48-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="6dd48-163">Active **Yes, I agree** (Acepto) y, a continuación, haga clic en **Create your Twitter application** (Crear la aplicación de Twitter).</span><span class="sxs-lookup"><span data-stu-id="6dd48-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="6dd48-164">Haga clic en hello **permisos** permiso predeterminado de pestaña hello es **de sólo lectura**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="6dd48-165">Esto es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6dd48-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="6dd48-166">Haga clic en hello **claves y Tokens de acceso** ficha.</span><span class="sxs-lookup"><span data-stu-id="6dd48-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="6dd48-167">Haga clic en **Create my access token**(Crear mi token de acceso).</span><span class="sxs-lookup"><span data-stu-id="6dd48-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="6dd48-168">Haga clic en **prueba OAuth** en la esquina superior derecha de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="6dd48-169">Rellene los campos **consumer key** (clave del consumidor), **Consumer secret** (Secreto del consumidor), **Access token** (Token de acceso) y **Access token secret** (Secreto del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="6dd48-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="6dd48-170">Necesitará los valores de hello más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="6dd48-171">En este tutorial, utilizará llamada de servicio web de Windows PowerShell toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="6dd48-172">Para obtener un ejemplo de .NET C#, consulte [Análisis de opinión en Twitter en tiempo real con HBase en HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="6dd48-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="6dd48-173">Hola otras llamadas a servicios web populares herramienta toomake es [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="6dd48-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="6dd48-174">Puede descargar Curl [aquí][curl-download].</span><span class="sxs-lookup"><span data-stu-id="6dd48-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="6dd48-175">Cuando utiliza el comando de curl Hola de Windows, use comillas dobles en lugar de comillas simples para los valores de opción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="6dd48-176">**tooget tweets**</span><span class="sxs-lookup"><span data-stu-id="6dd48-176">**tooget tweets**</span></span>

1. <span data-ttu-id="6dd48-177">Hola abrir Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="6dd48-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="6dd48-178">(En la pantalla de inicio de Windows 8 de bienvenida, escriba **PowerShell_ISE** y, a continuación, haga clic en **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="6dd48-179">Consulte [Inicio de Windows PowerShell en Windows 8 y Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="6dd48-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="6dd48-180">Copie Hola siguiente secuencia de comandos en el panel de scripts de hello:</span><span class="sxs-lookup"><span data-stu-id="6dd48-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="6dd48-181">Establecer variables de tooeight cinco primeros de hello en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="6dd48-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="6dd48-182">Variable</span><span class="sxs-lookup"><span data-stu-id="6dd48-182">Variable</span></span>|<span data-ttu-id="6dd48-183">Description</span><span class="sxs-lookup"><span data-stu-id="6dd48-183">Description</span></span>
    ---|---
    <span data-ttu-id="6dd48-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="6dd48-184">$clusterName</span></span>|<span data-ttu-id="6dd48-185">Este es el nombre de Hola Hola del clúster de HDInsight donde desea que la aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="6dd48-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="6dd48-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="6dd48-186">$oauth_consumer_key</span></span>|<span data-ttu-id="6dd48-187">Se trata de aplicación de Twitter de hello **clave de consumidor** anotó anteriormente cuando se creó la aplicación de Twitter de hello.</span><span class="sxs-lookup"><span data-stu-id="6dd48-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="6dd48-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="6dd48-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="6dd48-189">Se trata de aplicación de Twitter de hello **secreto de consumidor** anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6dd48-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="6dd48-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="6dd48-190">$oauth_token</span></span>|<span data-ttu-id="6dd48-191">Se trata de aplicación de Twitter de hello **token de acceso** anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6dd48-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="6dd48-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="6dd48-192">$oauth_token_secret</span></span>|<span data-ttu-id="6dd48-193">Se trata de aplicación de Twitter de hello **secreto del token de acceso** anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6dd48-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="6dd48-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="6dd48-194">$destBlobName</span></span>|<span data-ttu-id="6dd48-195">Este es el nombre de blob de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6dd48-195">This is hello output blob name.</span></span> <span data-ttu-id="6dd48-196">es el valor predeterminado de Hello **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="6dd48-197">Si cambia el valor predeterminado de hello, necesitará tooupdate scripts de Windows PowerShell de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="6dd48-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="6dd48-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="6dd48-198">$trackString</span></span>|<span data-ttu-id="6dd48-199">servicio web de Hello devolverá palabras clave de tweets toothese relacionados.</span><span class="sxs-lookup"><span data-stu-id="6dd48-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="6dd48-200">es el valor predeterminado de Hello **HDInsight de Azure, en la nube,**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="6dd48-201">Si cambia el valor predeterminado de hello, actualizará los scripts de Windows PowerShell de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="6dd48-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="6dd48-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="6dd48-202">$lineMax</span></span>|<span data-ttu-id="6dd48-203">valor de Hello determina cuántos script de Hola tweets va a leer.</span><span class="sxs-lookup"><span data-stu-id="6dd48-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="6dd48-204">Tarda aproximadamente tres minutos tooread 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="6dd48-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="6dd48-205">Puede establecer un número mayor, pero se tardará más toodownload de tiempo.</span><span class="sxs-lookup"><span data-stu-id="6dd48-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="6dd48-206">Presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="6dd48-207">Si experimenta problemas, como alternativa, seleccione todas las líneas de Hola y, a continuación, presione **F8**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="6dd48-208">Verá un mensaje de que se ha completado la tarea</span><span class="sxs-lookup"><span data-stu-id="6dd48-208">You shall see "Complete!"</span></span> <span data-ttu-id="6dd48-209">al final de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6dd48-209">at hello end of hello output.</span></span> <span data-ttu-id="6dd48-210">Los posibles mensajes de error aparecerán en rojo.</span><span class="sxs-lookup"><span data-stu-id="6dd48-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="6dd48-211">Como procedimiento de validación, puede comprobar el archivo de salida de hello, **/tutorials/twitter/data/tweets.txt**, en el almacenamiento de blobs de Azure mediante un explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dd48-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="6dd48-212">Para obtener un script de ejemplo de Windows PowerShell de todos los archivos enumerados, consulte [Uso de Blob Storage con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="6dd48-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="6dd48-213">Creación de un script de HiveQL</span><span class="sxs-lookup"><span data-stu-id="6dd48-213">Create HiveQL script</span></span>
<span data-ttu-id="6dd48-214">Uso de PowerShell de Azure, puede ejecutar varias instrucciones de HiveQL uno a una hora u Hola paquete HiveQL instrucción en un archivo de script.</span><span class="sxs-lookup"><span data-stu-id="6dd48-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="6dd48-215">En este tutorial, creará un script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6dd48-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="6dd48-216">archivo de script de Hola debe ser tooAzure cargado el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="6dd48-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="6dd48-217">En la siguiente sección hello, se ejecutará el archivo de script de Hola mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dd48-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="6dd48-218">archivo de script de Hive Hello y un archivo que contiene 10.000 tweets se han cargado en un contenedor de Blob público.</span><span class="sxs-lookup"><span data-stu-id="6dd48-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="6dd48-219">Puede omitir esta sección si desea toouse Hola cargar archivos.</span><span class="sxs-lookup"><span data-stu-id="6dd48-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="6dd48-220">Hola script de HiveQL llevará a cabo siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6dd48-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="6dd48-221">**Quitar tabla de hello tweets_raw** en caso de hello tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="6dd48-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="6dd48-222">**Crear tabla de Hive de hello tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="6dd48-223">Esta sección temporal estructurado tabla contiene más datos de Hola para extraer, transformar y cargar el procesamiento de (datos ETL).</span><span class="sxs-lookup"><span data-stu-id="6dd48-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="6dd48-224">Para obtener información sobre las particiones, consulte el [tutorial de Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="6dd48-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="6dd48-225">**Cargar datos** desde la carpeta de origen hello /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="6dd48-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="6dd48-226">conjunto de datos de Hello tweets grande en formato JSON anidado ahora se ha transformado en una estructura de tabla temporal de Hive.</span><span class="sxs-lookup"><span data-stu-id="6dd48-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="6dd48-227">**Colocar Hola tweets tabla** en caso de hello tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="6dd48-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="6dd48-228">**Crear tabla de tweets de hello**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-228">**Create hello tweets table**.</span></span> <span data-ttu-id="6dd48-229">Antes de poder realizar consultas en el conjunto de datos de hello tweets mediante el uso de Hive, debe toorun otro proceso ETL.</span><span class="sxs-lookup"><span data-stu-id="6dd48-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="6dd48-230">Este proceso ETL define un esquema de tabla más detallado para los datos de hello almacenada en la tabla de "twitter_raw" Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="6dd48-231">**Insertar tabla de sobrescritura**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-231">**Insert overwrite table**.</span></span> <span data-ttu-id="6dd48-232">Este script de Hive complejo se lanzará un conjunto de trabajos MapReduce largos por clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="6dd48-233">Según el tamaño de hello y conjunto de datos del clúster, puede tardar unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="6dd48-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="6dd48-234">**Insertar directorio de sobrescritura**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="6dd48-235">Ejecutar un archivo de tooa de un conjunto de datos de hello consulta y de salida.</span><span class="sxs-lookup"><span data-stu-id="6dd48-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="6dd48-236">Esta consulta devolverá una lista de usuarios de Twitter que envían tweets mayoría que contenía la palabra Hola "Azure".</span><span class="sxs-lookup"><span data-stu-id="6dd48-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="6dd48-237">**toocreate un subárbol de scripts y cargar tooAzure**</span><span class="sxs-lookup"><span data-stu-id="6dd48-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="6dd48-238">Abra Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6dd48-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="6dd48-239">Copie Hola siguiente secuencia de comandos en el panel de scripts de hello:</span><span class="sxs-lookup"><span data-stu-id="6dd48-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="6dd48-240">Establecer primero dos variables de hello en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="6dd48-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="6dd48-241">Variable</span><span class="sxs-lookup"><span data-stu-id="6dd48-241">Variable</span></span> | <span data-ttu-id="6dd48-242">Description</span><span class="sxs-lookup"><span data-stu-id="6dd48-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="6dd48-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="6dd48-243">$clusterName</span></span> |<span data-ttu-id="6dd48-244">Escriba nombre de clúster de HDInsight de Hola donde desea que la aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="6dd48-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="6dd48-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="6dd48-245">$subscriptionID</span></span> |<span data-ttu-id="6dd48-246">Especifique el identificador de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd48-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="6dd48-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="6dd48-247">$sourceDataPath</span></span> |<span data-ttu-id="6dd48-248">Hola donde las consultas de Hive Hola leerá los datos de Hola desde la ubicación de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd48-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="6dd48-249">No es necesario toochange esta variable.</span><span class="sxs-lookup"><span data-stu-id="6dd48-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="6dd48-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="6dd48-250">$outputPath</span></span> |<span data-ttu-id="6dd48-251">ubicación de almacenamiento de blobs de Azure donde las consultas de Hive Hola generará resultados Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="6dd48-252">No es necesario toochange esta variable.</span><span class="sxs-lookup"><span data-stu-id="6dd48-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="6dd48-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="6dd48-253">$hqlScriptFile</span></span> |<span data-ttu-id="6dd48-254">ubicación de Hola y el nombre del archivo de script de HiveQL de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="6dd48-255">No es necesario toochange esta variable.</span><span class="sxs-lookup"><span data-stu-id="6dd48-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="6dd48-256">Presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="6dd48-257">Si experimenta problemas, como alternativa, seleccione todas las líneas de Hola y, a continuación, presione **F8**.</span><span class="sxs-lookup"><span data-stu-id="6dd48-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="6dd48-258">Verá un mensaje de que se ha completado la tarea</span><span class="sxs-lookup"><span data-stu-id="6dd48-258">You shall see "Complete!"</span></span> <span data-ttu-id="6dd48-259">al final de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6dd48-259">at hello end of hello output.</span></span> <span data-ttu-id="6dd48-260">Los posibles mensajes de error aparecerán en rojo.</span><span class="sxs-lookup"><span data-stu-id="6dd48-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="6dd48-261">Como procedimiento de validación, puede comprobar el archivo de salida de hello, **/tutorials/twitter/twitter.hql**, en el almacenamiento de blobs de Azure mediante un explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dd48-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="6dd48-262">Para obtener un script de ejemplo de Windows PowerShell de todos los archivos enumerados, consulte [Uso de Blob Storage con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="6dd48-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="6dd48-263">Procesamiento de datos de Twitter mediante Hive</span><span class="sxs-lookup"><span data-stu-id="6dd48-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="6dd48-264">Ha terminado de todos los trabajos de preparación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="6dd48-265">Ahora, puede invocar el script de Hive de Hola y Hola resultados de la comprobación.</span><span class="sxs-lookup"><span data-stu-id="6dd48-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="6dd48-266">Envío de un trabajo de Hive</span><span class="sxs-lookup"><span data-stu-id="6dd48-266">Submit a Hive job</span></span>
<span data-ttu-id="6dd48-267">Usar hello siguiente secuencia de comandos de Windows PowerShell script toorun Hola Hive.</span><span class="sxs-lookup"><span data-stu-id="6dd48-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="6dd48-268">Necesitará primera variable de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="6dd48-269">Hola toouse tweets y Hola script de HiveQL que cargan en hello las dos últimas secciones, conjunto $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="6dd48-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="6dd48-270">Hola toouse los que se han cargado tooa públicos de blobs para usted, establezca $hqlScriptFile demasiado"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="6dd48-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="6dd48-271">Resultados de comprobación de Hola</span><span class="sxs-lookup"><span data-stu-id="6dd48-271">Check hello results</span></span>
<span data-ttu-id="6dd48-272">Hola de uso después de la salida de trabajo de Windows PowerShell script toocheck Hola Hive.</span><span class="sxs-lookup"><span data-stu-id="6dd48-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="6dd48-273">Deberá primero dos variables de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="6dd48-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabla de Hive Hello usa \001 como Hola delimitador de campo. <span data-ttu-id="6dd48-275">delimitador de Hello no está visible en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6dd48-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="6dd48-276">Después de que los resultados del análisis Hola se han colocado en el almacenamiento de blobs de Azure, puede exportar Hola datos tooan Azure SQL database de SQL server, exportar Hola datos tooExcel mediante Power Query o conectar sus datos de toohello de aplicación mediante el uso de hello Hive el controlador ODBC.</span><span class="sxs-lookup"><span data-stu-id="6dd48-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="6dd48-277">Para obtener más información, consulte [Sqoop de uso con HDInsight][hdinsight-use-sqoop], [analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-delay-data], [ Conectar Excel tooHDInsight con Power Query][hdinsight-power-query], y [tooHDInsight Excel conectarse con hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="6dd48-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd48-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6dd48-278">Next steps</span></span>
<span data-ttu-id="6dd48-279">En este tutorial hemos visto cómo tootransform un conjunto de datos no estructurado de JSON en una estructura tooquery de tabla de Hive, explorar y analizar datos de Twitter mediante el uso de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd48-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="6dd48-280">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="6dd48-280">toolearn more, see:</span></span>

* <span data-ttu-id="6dd48-281">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6dd48-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="6dd48-282">[Análisis de opinión en Twitter en tiempo real con HBase en HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="6dd48-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="6dd48-283">[Análisis de la información de retraso de vuelos con HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="6dd48-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="6dd48-284">[Conectar Excel tooHDInsight con Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="6dd48-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="6dd48-285">[Conectar Excel tooHDInsight con hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="6dd48-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="6dd48-286">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="6dd48-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
