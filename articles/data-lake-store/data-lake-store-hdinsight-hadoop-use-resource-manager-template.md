---
title: Uso de plantillas de Azure para crear Azure HDInsight y Data Lake Store | Microsoft Docs
description: "Uso de las plantillas de Azure Resource Manager para crear y usar clústeres de HDInsight con Azure Data Lake Store"
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="bdfec-103">Creación de un clúster de HDInsight con Data Lake Store mediante las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bdfec-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdfec-104">Uso del Portal</span><span class="sxs-lookup"><span data-stu-id="bdfec-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="bdfec-105">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="bdfec-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="bdfec-106">Uso de PowerShell (para el almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="bdfec-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="bdfec-107">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bdfec-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="bdfec-108">Aprenda a usar Azure PowerShell para configurar un clúster de HDInsight con Azure Data Lake Store **como almacenamiento adicional**.</span><span class="sxs-lookup"><span data-stu-id="bdfec-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="bdfec-109">Para los tipos de clúster compatibles, Data Lake Store se puede usar como un almacenamiento predeterminado o una cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="bdfec-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="bdfec-110">Cuando Data Lake Store se usa como almacenamiento adicional, la cuenta de almacenamiento predeterminada para los clústeres seguirá siendo Azure Storage Blobs (WASB) y los archivos relacionados con clústeres (como registros, etc.) seguirán escribiéndose en el almacenamiento predeterminado, mientras que los datos que quiere procesar pueden almacenarse en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bdfec-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="bdfec-111">Utilizar el Almacén de Data Lake como una cuenta de almacenamiento adicional no afecta al rendimiento o la capacidad de lectura y escritura en el almacenamiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="bdfec-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="bdfec-112">Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdfec-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="bdfec-113">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="bdfec-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="bdfec-114">La opción para crear clústeres de HDInsight con acceso a Data Lake Store como almacenamiento predeterminado está disponible para las versiones 3.5 y 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdfec-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="bdfec-115">La opción para crear clústeres de HDInsight con acceso a Data Lake Store como almacenamiento está disponible para las versiones 3.2, 3.4, 3.5 y 3.6. de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdfec-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="bdfec-116">En este artículo, aprovisionamos un clúster de Hadoop con el Almacén de Data Lake como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="bdfec-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="bdfec-117">Para instrucciones sobre cómo crear un clúster de Hadoop con Data Lake Store como almacenamiento predeterminado, consulte [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bdfec-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdfec-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bdfec-118">Prerequisites</span></span>
<span data-ttu-id="bdfec-119">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bdfec-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="bdfec-120">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="bdfec-120">**An Azure subscription**.</span></span> <span data-ttu-id="bdfec-121">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdfec-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bdfec-122">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="bdfec-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="bdfec-123">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bdfec-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="bdfec-124">**Entidad de servicio de Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="bdfec-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="bdfec-125">En los pasos de este tutorial se proporcionan instrucciones sobre cómo crear entidades de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdfec-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="bdfec-126">Sin embargo, debe ser administrador de Azure AD para poder crearlas.</span><span class="sxs-lookup"><span data-stu-id="bdfec-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="bdfec-127">Si ya lo es, puede hacer caso omiso a este requisito previo y continuar con el tutorial.</span><span class="sxs-lookup"><span data-stu-id="bdfec-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="bdfec-128">**Si no lo es**, no podrá realizar los pasos necesarios para crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="bdfec-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="bdfec-129">En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bdfec-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="bdfec-130">Además, la entidad de servicio debe crearse con un certificado, tal y como se describe en [Creación de una entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="bdfec-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="bdfec-131">Creación de un clúster de HDInsight con Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bdfec-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="bdfec-132">Las plantillas de Resource Manager y los requisitos previos para usarla están disponibles en GitHub: [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage) (Implementación de un clúster Linux de HDInsight con la nueva versión de Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="bdfec-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="bdfec-133">Siga las instrucciones de este vínculo para crear un clúster de HDInsight con Azure Data Lake Store como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="bdfec-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="bdfec-134">Estas instrucciones requieren el uso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdfec-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="bdfec-135">Antes de comenzar con las instrucciones, asegúrese de iniciar sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfec-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="bdfec-136">En el escritorio, abra una nueva ventana de Azure PowerShell y escriba los siguientes fragmentos.</span><span class="sxs-lookup"><span data-stu-id="bdfec-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="bdfec-137">Cuando se le solicite iniciar sesión, asegúrese de iniciarla como uno de los administradores o propietario de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="bdfec-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="bdfec-138">Carga de datos de ejemplo en Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bdfec-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="bdfec-139">Las plantilla de Resource Manager crean una cuenta de Data Lake Store y la asocian con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdfec-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="bdfec-140">Ahora, debe cargar algunos datos de ejemplo en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bdfec-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="bdfec-141">Necesitará estos datos más adelante en el tutorial para ejecutar trabajos desde un clúster de HDInsight que accedan a datos en el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bdfec-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="bdfec-142">Para ver las instrucciones sobre cómo cargar datos, consulte el artículo de [carga de archivos en Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="bdfec-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="bdfec-143">Si busca datos de ejemplo para cargar, puede obtener la carpeta **Ambulance Data** en el [repositorio Git de Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="bdfec-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="bdfec-144">Establecimiento de listas ACL pertinentes en los datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bdfec-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="bdfec-145">Para confirmar que los datos de ejemplo que carga están accesibles desde el clúster de HDInsight, debe asegurarse de que la aplicación de Azure AD que utiliza para establecer la identidad entre el clúster de HDInsight y Data Lake Store tiene acceso al archivo o a la carpeta deseados.</span><span class="sxs-lookup"><span data-stu-id="bdfec-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="bdfec-146">Para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="bdfec-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="bdfec-147">Busque el nombre de la aplicación de Azure AD asociada al clúster de HDInsight y a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bdfec-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="bdfec-148">Una manera de buscar el nombre es abrir la hoja de clúster de HDInsight que creó mediante la plantilla de Resource Manager, hacer clic en la pestaña **Identidad de AAD del clúster** y buscar el valor del **nombre para mostrar de la entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="bdfec-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="bdfec-149">Ahora, proporcione acceso a esta aplicación de Azure AD en el archivo o la carpeta a los quiera acceder desde el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdfec-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="bdfec-150">Para establecer las listas ACL adecuadas en el archivo o carpeta de Data Lake Store, consulte el artículo sobre cómo [proteger los datos de Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="bdfec-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="bdfec-151">Ejecución de trabajos de prueba en el clúster de HDInsight para usar el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="bdfec-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="bdfec-152">Después de configurar un clúster de HDInsight, puede ejecutar trabajos de prueba en el clúster para probar que el clúster de HDInsight pueda acceder al Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bdfec-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="bdfec-153">Para hacerlo, ejecutaremos un trabajo de Hive de ejemplo que crea una tabla con los datos de ejemplo que cargó antes en el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bdfec-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="bdfec-154">En esta sección, aprenderá a usar SSH en el clúster de Linux en HDInsight y ejecutará una consulta de Hive de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bdfec-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="bdfec-155">Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="bdfec-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="bdfec-156">Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="bdfec-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="bdfec-157">Una vez conectado, inicie la CLI de Hive con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bdfec-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="bdfec-158">Mediante la CLI, especifique las siguientes instrucciones para crear una tabla nueva denominada **vehicles** con los datos de ejemplo del Almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="bdfec-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="bdfec-159">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bdfec-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="bdfec-160">Acceso al Almacén de Data Lake mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="bdfec-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="bdfec-161">Una vez que configure el clúster de HDInsight para que use el Almacén de Data Lake, puede usar los comandos de shell de HDFS para acceder al almacén.</span><span class="sxs-lookup"><span data-stu-id="bdfec-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="bdfec-162">En esta sección, aprenderá a usar SSH en un clúster de Linux en HDInsight y ejecutará los comandos HDFS.</span><span class="sxs-lookup"><span data-stu-id="bdfec-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="bdfec-163">Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="bdfec-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="bdfec-164">Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="bdfec-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="bdfec-165">Una vez conectado, utilice el siguiente comando del sistema de archivos HDFS para enumerar los archivos del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bdfec-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="bdfec-166">Se debería incluir el archivo que cargó antes en el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bdfec-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="bdfec-167">También puede usar el comando `hdfs dfs -put` para cargar algunos archivos en el almacén de Data Lake y después usar `hdfs dfs -ls` para comprobar si los archivos se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="bdfec-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bdfec-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bdfec-168">Next steps</span></span>
* [<span data-ttu-id="bdfec-169">Copia de datos de blobs de Azure Storage en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bdfec-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
