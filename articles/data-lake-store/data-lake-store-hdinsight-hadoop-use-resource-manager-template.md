---
title: "aaaUse toocreate de plantillas de Azure HDInsight y almacén de Data Lake | Documentos de Microsoft"
description: "Utilice toocreate de plantillas de administrador de recursos de Azure y clústeres de HDInsight con el almacén de Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="298d4-103">Creación de un clúster de HDInsight con Data Lake Store mediante las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="298d4-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="298d4-104">Uso del Portal</span><span class="sxs-lookup"><span data-stu-id="298d4-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="298d4-105">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="298d4-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="298d4-106">Uso de PowerShell (para el almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="298d4-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="298d4-107">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="298d4-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="298d4-108">Obtenga información acerca de cómo toouse Azure PowerShell tooconfigure un HDInsight de clúster con el almacén de Azure Data Lake **como almacenamiento adicional**.</span><span class="sxs-lookup"><span data-stu-id="298d4-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="298d4-109">Para los tipos de clúster compatibles, Data Lake Store se puede usar como un almacenamiento predeterminado o una cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="298d4-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="298d4-110">Cuando se utiliza el almacén de Data Lake como almacenamiento adicional, cuenta de almacenamiento predeterminada de Hola para clústeres de hello seguirán estando Blobs de almacenamiento de Azure (WASB) y archivos relacionados con el clúster de hello (por ejemplo, registros, etc.) se escriben todavía almacenamiento predeterminado de toohello, mientras que los datos de Hola que desea tooprocess pueden almacenarse en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="298d4-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="298d4-111">Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecta a rendimiento u Hola capacidad tooread/escritura toohello almacenamiento Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="298d4-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="298d4-112">Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="298d4-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="298d4-113">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="298d4-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="298d4-114">Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento predeterminado está disponible para HDInsight versión 3.5 y 3.6.</span><span class="sxs-lookup"><span data-stu-id="298d4-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="298d4-115">Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento adicional está disponible para las versiones 3.2, 3.4, 3.5 y 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="298d4-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="298d4-116">En este artículo, aprovisionamos un clúster de Hadoop con el Almacén de Data Lake como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="298d4-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="298d4-117">Para obtener instrucciones sobre cómo toocreate un Hadoop de clúster con el almacén de Data Lake como almacenamiento predeterminado, consulte [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="298d4-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="298d4-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="298d4-118">Prerequisites</span></span>
<span data-ttu-id="298d4-119">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="298d4-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="298d4-120">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="298d4-120">**An Azure subscription**.</span></span> <span data-ttu-id="298d4-121">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="298d4-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="298d4-122">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="298d4-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="298d4-123">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="298d4-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="298d4-124">**Entidad de servicio de Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="298d4-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="298d4-125">Pasos de este tutorial proporcionan instrucciones sobre cómo toocreate una entidad de servicio en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="298d4-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="298d4-126">Sin embargo, debe ser un toocreate capaz de Azure AD administrador toobe una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="298d4-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="298d4-127">Si eres un administrador de Azure AD, puede omitir este requisito previo y continuar con tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="298d4-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="298d4-128">**Si no es un administrador de Azure AD**, no será capaz de tooperform Hola pasos necesarios toocreate una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="298d4-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="298d4-129">En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="298d4-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="298d4-130">Además, entidad de servicio de hello debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="298d4-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="298d4-131">Creación de un clúster de HDInsight con Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="298d4-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="298d4-132">plantilla de administrador de recursos de Hola y requisitos previos de Hola para usar la plantilla hello, están disponibles en GitHub en [implementar un clúster de HDInsight Linux con el nuevo almacén de Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="298d4-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="298d4-133">Siga las instrucciones de hello proporcionadas en este vínculo toocreate un clúster de HDInsight con el almacén de Data Lake de Azure como almacenamiento adicional de Hola.</span><span class="sxs-lookup"><span data-stu-id="298d4-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="298d4-134">instrucciones de Hello en el vínculo de hello mencionadas anteriormente requieren PowerShell.</span><span class="sxs-lookup"><span data-stu-id="298d4-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="298d4-135">Antes de empezar con estas instrucciones, asegúrese de que inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="298d4-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="298d4-136">Desde el escritorio, abra una nueva ventana de PowerShell de Azure y escriba Hola siguientes fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="298d4-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="298d4-137">Cuando toolog solicitada, asegúrese de que inicie sesión como una suscripción de hello admininistrators/propietario:</span><span class="sxs-lookup"><span data-stu-id="298d4-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="298d4-138">Cargar el almacén de datos toohello Azure Data Lake de ejemplo</span><span class="sxs-lookup"><span data-stu-id="298d4-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="298d4-139">plantilla de administrador de recursos de Hello crea una nueva cuenta de almacén de Data Lake y lo asocia con clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="298d4-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="298d4-140">Ahora debe cargar algunos toohello de datos de ejemplo almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="298d4-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="298d4-141">Necesitará estos datos más adelante en trabajos de toorun tutorial Hola desde un clúster de HDInsight que tienen acceso a datos en el almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="298d4-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="298d4-142">Para obtener instrucciones sobre cómo ver datos tooupload, [cargar un almacén de Data Lake de archivo tooyour](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="298d4-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="298d4-143">Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="298d4-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="298d4-144">Establecer las ACL relevantes en los datos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="298d4-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="298d4-145">toomake seguro de datos de ejemplo de Hola que cargue están accesibles desde el clúster de HDInsight de hello, debe asegurarse de que la aplicación hello Azure AD identidad tooestablish utilizado entre el clúster de HDInsight de Hola y almacén de Data Lake tiene acceso toohello archivo o carpeta que está intentar tooaccess.</span><span class="sxs-lookup"><span data-stu-id="298d4-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="298d4-146">toodo, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="298d4-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="298d4-147">Encontrar Hola nombre de aplicación de Azure AD que está asociado con el clúster de HDInsight de Hola y Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="298d4-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="298d4-148">Toolook unidireccional para nombre de hello hoja de clúster de HDInsight tooopen Hola que haya creado mediante la plantilla de administrador de recursos de hello, haga clic en hello **identidad de AAD de clúster** y a buscar valor hello **entidad de servicio Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="298d4-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="298d4-149">Ahora, proporcionar acceso toothis aplicación de Azure AD en hello, archivo o carpeta que desea tooaccess de clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="298d4-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="298d4-150">vea tooset Hola ACL de derechos en hello archivo o carpeta en el almacén de Data Lake [proteger los datos en el almacén de Data Lake](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="298d4-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="298d4-151">Ejecutar trabajos de prueba en Hola de toouse de clúster de HDInsight de hello almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="298d4-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="298d4-152">Después de haber configurado un clúster de HDInsight, se puede ejecutar trabajos de prueba en hello clúster tootest ese hello HDInsight clúster puede tener acceso a almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="298d4-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="298d4-153">toodo por lo tanto, se ejecutará un trabajo de Hive de ejemplo que crea una tabla con datos de ejemplo de Hola que cargan almacén de Data Lake de tooyour anteriores.</span><span class="sxs-lookup"><span data-stu-id="298d4-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="298d4-154">En esta sección le SSH en un clúster de HDInsight Linux y ejecución Hola una consulta de Hive de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="298d4-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="298d4-155">Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="298d4-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="298d4-156">Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="298d4-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="298d4-157">Una vez conectado, inicie Hola Hive CLI mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="298d4-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="298d4-158">Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola Hola almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="298d4-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="298d4-159">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="298d4-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="298d4-160">Acceso al Almacén de Data Lake mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="298d4-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="298d4-161">Una vez haya configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar comandos de shell de hello HDFS tooaccess Hola almacén.</span><span class="sxs-lookup"><span data-stu-id="298d4-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="298d4-162">En esta sección le SSH en un clúster de HDInsight Linux y ejecución Hola comandos HDFS.</span><span class="sxs-lookup"><span data-stu-id="298d4-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="298d4-163">Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="298d4-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="298d4-164">Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="298d4-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="298d4-165">Una vez conectado, use Hola siguientes archivos HDFS filesystem comando toolist Hola Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="298d4-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="298d4-166">Esto debería incluir archivo hello que cargan almacén de Data Lake de toohello anteriores.</span><span class="sxs-lookup"><span data-stu-id="298d4-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="298d4-167">También puede usar hello `hdfs dfs -put` comando tooupload algunos toohello archivos del almacén de Data Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="298d4-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="298d4-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="298d4-168">Next steps</span></span>
* [<span data-ttu-id="298d4-169">Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData</span><span class="sxs-lookup"><span data-stu-id="298d4-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
