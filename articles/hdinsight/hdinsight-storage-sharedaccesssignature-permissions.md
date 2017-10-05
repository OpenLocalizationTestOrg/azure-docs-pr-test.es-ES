---
title: "Restricción del acceso mediante firmas de acceso compartido - Azure HDInsight | Microsoft Docs"
description: "Obtener información acerca de cómo usar firmas de acceso compartido para restringir el acceso de HDInsight a datos almacenados en blobs de Almacenamiento de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 2e4b1a307fae06c0639d93b9804c6f0f703d5900
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-in-hdinsight"></a><span data-ttu-id="af300-103">Uso de firmas de acceso compartido de Azure Storage para restringir el acceso a datos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-103">Use Azure Storage Shared Access Signatures to restrict access to data in HDInsight</span></span>

<span data-ttu-id="af300-104">HDInsight tiene acceso total a los datos de las cuentas de Azure Storage asociadas con el clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-104">HDInsight has full access to data in the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="af300-105">Puede usar firmas de acceso compartido en el contenedor de blobs para restringir el acceso a los datos.</span><span class="sxs-lookup"><span data-stu-id="af300-105">You can use Shared Access Signatures on the blob container to restrict access to the data.</span></span> <span data-ttu-id="af300-106">Por ejemplo, para proporcionar acceso de solo lectura a los datos.</span><span class="sxs-lookup"><span data-stu-id="af300-106">For example, to provide read-only access to the data.</span></span> <span data-ttu-id="af300-107">Las firmas de acceso compartido (SAS) son una característica de las cuentas de Almacenamiento de Azure que permite limitar el acceso a los datos.</span><span class="sxs-lookup"><span data-stu-id="af300-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="af300-108">Por ejemplo, al proporcionar acceso de solo lectura a los datos.</span><span class="sxs-lookup"><span data-stu-id="af300-108">For example, providing read-only access to data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af300-109">Para una solución con Apache Ranger, considere la posibilidad de usar HDInsight unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="af300-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="af300-110">Para más información, consulte el documento [Configuración de clústeres de HDInsight unidos a un dominio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="af300-110">For more information, see the [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="af300-111">HDInsight debe tener acceso total al almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-111">HDInsight must have full access to the default storage for the cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="af300-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="af300-112">Requirements</span></span>

* <span data-ttu-id="af300-113">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="af300-113">An Azure subscription</span></span>
* <span data-ttu-id="af300-114">C# o Python.</span><span class="sxs-lookup"><span data-stu-id="af300-114">C# or Python.</span></span> <span data-ttu-id="af300-115">El código de ejemplo de C# se proporciona como una solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af300-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="af300-116">Se debe usar la versión de Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="af300-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="af300-117">Se debe usar la versión de Python 2.7 o superior.</span><span class="sxs-lookup"><span data-stu-id="af300-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="af300-118">Un clúster de HDInsight basado en Linux o [Azure PowerShell][powershell]: si ya tiene un clúster basado en Linux, puede usar Ambari para agregar una firma de acceso compartido al clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="af300-119">Si no es así, puede usar Azure PowerShell para crear un clúster y agregar una firma de acceso compartido durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-119">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="af300-120">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="af300-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="af300-121">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="af300-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="af300-122">Los archivos de ejemplo de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="af300-122">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="af300-123">Este repositorio contiene los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="af300-123">This repository contains the following items:</span></span>

  * <span data-ttu-id="af300-124">Un proyecto de Visual Studio que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="af300-125">Un script de Python que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="af300-126">Un script de PowerShell que puede crear un clúster de HDInsight y configurarlo para que use la SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-126">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="af300-127">Las firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="af300-127">Shared Access Signatures</span></span>

<span data-ttu-id="af300-128">Hay dos formas de firmas de acceso compartido:</span><span class="sxs-lookup"><span data-stu-id="af300-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="af300-129">Ad hoc: la hora de inicio, la hora de expiración y los permisos para la firma de acceso compartido se especifican en el URI de esta.</span><span class="sxs-lookup"><span data-stu-id="af300-129">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span>

* <span data-ttu-id="af300-130">Directiva de acceso almacenada: se define una directiva de acceso almacenada en un contenedor de recursos, como un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="af300-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="af300-131">Una directiva puede usarse para administrar las restricciones de una o varias firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="af300-131">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="af300-132">Cuando asocia una SAS a una directiva de acceso almacenada, la SAS hereda las restricciones (hora de inicio, hora de expiración y permisos) definidas para la directiva de acceso almacenada.</span><span class="sxs-lookup"><span data-stu-id="af300-132">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="af300-133">La diferencia entre las dos formas es importante para un escenario principal: revocación.</span><span class="sxs-lookup"><span data-stu-id="af300-133">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="af300-134">Una SAS es una dirección URL, por lo que cualquier persona que obtenga la SAS puede usarla, independientemente de quién la solicitó para comenzar.</span><span class="sxs-lookup"><span data-stu-id="af300-134">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="af300-135">Si una SAS se encuentra disponible públicamente, cualquier persona del mundo puede usarla.</span><span class="sxs-lookup"><span data-stu-id="af300-135">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="af300-136">Una SAS distribuida es válida hasta que se produzca una de las cuatro situaciones:</span><span class="sxs-lookup"><span data-stu-id="af300-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="af300-137">Se alcanza el tiempo de expiración especificado en la SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-137">The expiry time specified on the SAS is reached.</span></span>

2. <span data-ttu-id="af300-138">Se alcanza la hora de expiración especificada en la directiva de acceso almacenada a la que hace referencia la SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-138">The expiry time specified on the stored access policy referenced by the SAS is reached.</span></span> <span data-ttu-id="af300-139">Los escenarios siguientes hacen que se alcance la hora de expiración:</span><span class="sxs-lookup"><span data-stu-id="af300-139">The following scenarios cause the expiry time to be reached:</span></span>

    * <span data-ttu-id="af300-140">Ha transcurrido el intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="af300-140">The time interval has elapsed.</span></span>
    * <span data-ttu-id="af300-141">La directiva de acceso almacenada se ha modificado para que la hora de expiración haya pasado.</span><span class="sxs-lookup"><span data-stu-id="af300-141">The stored access policy is modified to have an expiry time in the past.</span></span> <span data-ttu-id="af300-142">Cambiar la hora de expiración es una manera de revocar la firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="af300-142">Changing the expiry time is one way to revoke the SAS.</span></span>

3. <span data-ttu-id="af300-143">Se elimina la directiva de acceso almacenada a la que hace referencia la SAS, que es otra forma de revocar la SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-143">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="af300-144">Si se vuelve a crear la directiva de acceso almacenada con el mismo nombre, todos los tokens de SAS de la directiva anterior son válidos (si la SAS no ha caducado).</span><span class="sxs-lookup"><span data-stu-id="af300-144">If you recreate the stored access policy with the same name, all  SAS tokens for the previous policy are valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="af300-145">Si prevé revocar la SAS, asegúrese de usar un nombre distinto si vuelve a crear la directiva de acceso con una hora de expiración futura.</span><span class="sxs-lookup"><span data-stu-id="af300-145">If you intend to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>

4. <span data-ttu-id="af300-146">Se vuelve a generar la clave de cuenta que se usó para crear la SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-146">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="af300-147">Regenerar la clave hace que todas las aplicaciones que usan la clave anterior no se puedan autenticar.</span><span class="sxs-lookup"><span data-stu-id="af300-147">Regenerating the key causes all applications that use the previous key to fail authentication.</span></span> <span data-ttu-id="af300-148">Actualice todos los componentes con la nueva clave.</span><span class="sxs-lookup"><span data-stu-id="af300-148">Update all components to the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af300-149">Los URI de firma de acceso compartido están asociados a la clave de la cuenta que se utiliza para crear la firma y a la directiva de acceso almacenada correspondiente (en su caso).</span><span class="sxs-lookup"><span data-stu-id="af300-149">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="af300-150">Si no se especifica una directiva de acceso almacenada, la única forma de revocar una firma de acceso compartido es cambiar la clave de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="af300-150">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

<span data-ttu-id="af300-151">Se recomienda usar siempre las directivas de acceso almacenadas.</span><span class="sxs-lookup"><span data-stu-id="af300-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="af300-152">Al utilizar las directivas almacenadas, puede revocar las firmas o ampliar la fecha de expiración según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="af300-152">When using stored policies, you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="af300-153">Los pasos descritos en este documento utilizan directivas de acceso almacenadas para generar las SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-153">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="af300-154">Para más información sobre firmas de acceso compartido, consulte [Firmas de acceso compartido, Parte 1: Descripción del modelo de firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="af300-154">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="af300-155">Creación de una directiva almacenada y una SAS mediante C\#</span><span class="sxs-lookup"><span data-stu-id="af300-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="af300-156">Abra la solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af300-156">Open the solution in Visual Studio.</span></span>

2. <span data-ttu-id="af300-157">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SASToke**n y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="af300-157">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="af300-158">Seleccione **Configuración** y agregue valores para las siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="af300-158">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="af300-159">StorageConnectionString: la cadena de conexión de la cuenta de almacenamiento para la que desea crear una directiva almacenada y una SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-159">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="af300-160">El formato debe ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` donde `myaccount` es el nombre de la cuenta de almacenamiento y `mykey` es la clave para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af300-160">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>

   * <span data-ttu-id="af300-161">ContainerName: el contenedor de la cuenta de almacenamiento a la que desea restringir el acceso.</span><span class="sxs-lookup"><span data-stu-id="af300-161">ContainerName: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="af300-162">SASPolicyName: el nombre que se usará para la directiva almacenada que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="af300-162">SASPolicyName: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="af300-163">FileToUpload: la ruta de acceso a un archivo que se carga en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="af300-163">FileToUpload: The path to a file that is uploaded to the container.</span></span>

4. <span data-ttu-id="af300-164">Ejecute el proyecto.</span><span class="sxs-lookup"><span data-stu-id="af300-164">Run the project.</span></span> <span data-ttu-id="af300-165">Una vez generada la firma de acceso compartido, se mostrará información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="af300-165">Information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="af300-166">Guarde el token de directiva de SAS, el nombre de la cuenta de almacenamiento y el nombre del contenedor.</span><span class="sxs-lookup"><span data-stu-id="af300-166">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="af300-167">Estos valores se usan al asociar la cuenta de almacenamiento con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-167">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="af300-168">Creación de una directiva almacenada y una SAS mediante Python</span><span class="sxs-lookup"><span data-stu-id="af300-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="af300-169">Abra el archivo SASToken.py y cambie los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="af300-169">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="af300-170">policy\_name: el nombre que se usará para la directiva almacenada que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="af300-170">policy\_name: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="af300-171">storage\_account\_name: el nombre de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af300-171">storage\_account\_name: The name of your storage account.</span></span>

   * <span data-ttu-id="af300-172">storage\_account\_key: la clave de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af300-172">storage\_account\_key: The key for the storage account.</span></span>

   * <span data-ttu-id="af300-173">storage\_container\_name: el contenedor de la cuenta de almacenamiento al que desea restringir el acceso.</span><span class="sxs-lookup"><span data-stu-id="af300-173">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="af300-174">example\_file\_path: la ruta de acceso a un archivo que se carga en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="af300-174">example\_file\_path: The path to a file that is uploaded to the container.</span></span>

2. <span data-ttu-id="af300-175">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="af300-175">Run the script.</span></span> <span data-ttu-id="af300-176">Cuando finalice el script, muestra un token de SAS similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="af300-176">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="af300-177">Guarde el token de directiva de SAS, el nombre de la cuenta de almacenamiento y el nombre del contenedor.</span><span class="sxs-lookup"><span data-stu-id="af300-177">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="af300-178">Estos valores se usan al asociar la cuenta de almacenamiento con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-178">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="af300-179">Uso de las SAS con HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-179">Use the SAS with HDInsight</span></span>

<span data-ttu-id="af300-180">Al crear un clúster de HDInsight, debe especificar una cuenta de almacenamiento principal y puede especificar, opcionalmente, cuentas de almacenamiento adicionales.</span><span class="sxs-lookup"><span data-stu-id="af300-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="af300-181">Estos dos métodos para agregar almacenamiento requieren tener un acceso total a las cuentas de almacenamiento y los contenedores que se utilizan.</span><span class="sxs-lookup"><span data-stu-id="af300-181">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="af300-182">Para usar una firma de acceso compartido a fin de limitar el acceso a un contenedor, agregue una entrada personalizada a la configuración **core-site** para el clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-182">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="af300-183">Para clústeres de HDInsight **basados en Windows** o **basados en Linux**, puede agregar la entrada durante la creación del clúster mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af300-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="af300-184">Para clústeres de HDInsight **basados en Linux**, cambie la configuración después de crear el clúster con Ambari.</span><span class="sxs-lookup"><span data-stu-id="af300-184">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="af300-185">Crear un clúster que usa la SAS</span><span class="sxs-lookup"><span data-stu-id="af300-185">Create a cluster that uses the SAS</span></span>

<span data-ttu-id="af300-186">Se incluye un ejemplo de creación de un clúster de HDInsight que usa la SAS en el directorio `CreateCluster` del repositorio.</span><span class="sxs-lookup"><span data-stu-id="af300-186">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="af300-187">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="af300-187">To use it, use the following steps:</span></span>

1. <span data-ttu-id="af300-188">Abra el archivo `CreateCluster\HDInsightSAS.ps1` en un editor de texto y modifique los valores siguientes al principio del documento.</span><span class="sxs-lookup"><span data-stu-id="af300-188">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

    ```powershell
    # Replace 'mycluster' with the name of the cluster to be created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with the name of the group to be created
    $resourceGroupName = 'myresourcegroup'
    # Replace with the Azure data center you want to the cluster to live in
    $location = 'North Europe'
    # Replace with the name of the default storage account to be created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with the name of the SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with the name of the SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with the SAS token generated earlier
    $SASToken = 'sastoken'
    # Set the number of worker nodes in the cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="af300-189">Por ejemplo, cambie `'mycluster'` por el nombre del clúster que desea crear.</span><span class="sxs-lookup"><span data-stu-id="af300-189">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="af300-190">Los valores de SAS deben coincidir con los valores de los pasos anteriores al crear una cuenta de almacenamiento y el token de SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-190">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="af300-191">Una vez que haya cambiado los valores, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="af300-191">Once you have changed the values, save the file.</span></span>

2. <span data-ttu-id="af300-192">Abra un nuevo símbolo del sistema de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af300-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="af300-193">Si no está familiarizado con Azure PowerShell, o si no lo ha instalado, consulte [Cómo instalar y configurar Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="af300-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="af300-194">En el símbolo del sistema, use el siguiente comando para autenticarse en la suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="af300-194">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="af300-195">Cuando se le solicite, inicie sesión con la cuenta de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="af300-195">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="af300-196">Si la cuenta está asociada a varias suscripciones de Azure, puede que tenga que usar `Select-AzureRmSubscription` para seleccionar la suscripción que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="af300-196">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>

4. <span data-ttu-id="af300-197">En el símbolo del sistema, cambie los directorios al directorio `CreateCluster` que contiene el archivo HDInsightSAS.ps1.</span><span class="sxs-lookup"><span data-stu-id="af300-197">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="af300-198">Después, use el siguiente comando para ejecutar el script</span><span class="sxs-lookup"><span data-stu-id="af300-198">Then use the following command to run the script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="af300-199">Mientras se ejecuta el script, registra la salida en el símbolo del sistema de PowerShell mientras crea las cuentas de grupo de recursos y de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af300-199">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="af300-200">Se le pedirá que escriba el usuario HTTP para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-200">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="af300-201">Esta cuenta se usa para proteger el acceso HTTP/s al clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-201">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="af300-202">Si está creando un clúster basado en Linux, se le solicitará un nombre de cuenta de usuario SSH y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="af300-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="af300-203">Esta cuenta se usa para el inicio de sesión remoto al clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-203">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="af300-204">Cuando se le pida el nombre de usuario SSH o HTTP/s y la contraseña, debe proporcionar una contraseña que cumpla los criterios siguientes:</span><span class="sxs-lookup"><span data-stu-id="af300-204">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="af300-205">Debe tener como mínimo 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="af300-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="af300-206">Debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="af300-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="af300-207">Debe incluir al menos un carácter no alfanumérico.</span><span class="sxs-lookup"><span data-stu-id="af300-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="af300-208">Debe contener al menos una mayúscula o una minúscula.</span><span class="sxs-lookup"><span data-stu-id="af300-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="af300-209">Este script tarda un tiempo en completarse, normalmente unos 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="af300-209">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="af300-210">Una vez finalizado el script sin errores, se creará el clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-210">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="af300-211">Usar la SAS con un clúster existente</span><span class="sxs-lookup"><span data-stu-id="af300-211">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="af300-212">Si tiene un clúster existente basado en Linux, puede agregar las SAS para la configuración **core-site** mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="af300-212">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="af300-213">Abra la interfaz de usuario web Ambari del clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-213">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="af300-214">La dirección de esta página es https://NOMBREDESUCLÚSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="af300-214">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="af300-215">Cuando se le solicite, autentíquese en el clúster con el nombre de administrador (admin) y la contraseña que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-215">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>

2. <span data-ttu-id="af300-216">En el lado izquierdo de la interfaz de usuario web Ambari, seleccione **HDFS** y, a continuación, seleccione la pestaña **Configs** (Configuraciones) en el centro de la página.</span><span class="sxs-lookup"><span data-stu-id="af300-216">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>

3. <span data-ttu-id="af300-217">Seleccione la pestaña **Advanced** (Avanzadas) y, a continuación, desplácese hasta encontrar la sección **Custom core-site** (Sitio principal personalizado).</span><span class="sxs-lookup"><span data-stu-id="af300-217">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>

4. <span data-ttu-id="af300-218">Expanda la sección **Custom core-site** (Sitio principal personalizado), desplácese hasta el final y seleccione el vínculo **Add property...** (Agregar propiedad...).</span><span class="sxs-lookup"><span data-stu-id="af300-218">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="af300-219">Utilice los siguientes valores para los campos **Key** (Clave) y **Value** (Valor):</span><span class="sxs-lookup"><span data-stu-id="af300-219">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="af300-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="af300-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="af300-221">**Value**: la SAS devuelta por la aplicación de C# o Python ejecutada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af300-221">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="af300-222">Reemplace **CONTAINERNAME** por el nombre del contenedor utilizado con la aplicación de C# o de SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-222">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="af300-223">Reemplace **STORAGEACCOUNTNAME** por el nombre de la cuenta de almacenamiento utilizada.</span><span class="sxs-lookup"><span data-stu-id="af300-223">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>

5. <span data-ttu-id="af300-224">Haga clic en el botón **Add** (Agregar) para guardar esta clave y este valor y, a continuación, haga clic en el botón **Save** (Guardar) para guardar los cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="af300-224">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="af300-225">Cuando se le solicite, agregue una descripción del cambio ("Agregar acceso de almacenamiento de SAS", por ejemplo) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="af300-225">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="af300-226">Haga clic en **OK** (Aceptar) cuando se hayan completado los cambios.</span><span class="sxs-lookup"><span data-stu-id="af300-226">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="af300-227">Debe reiniciar varios servicios para que el cambio surta efecto.</span><span class="sxs-lookup"><span data-stu-id="af300-227">You must restart several services before the change takes effect.</span></span>

6. <span data-ttu-id="af300-228">En la interfaz de usuario web Ambari, seleccione **HDFS** en la lista de la izquierda y, a continuación, seleccione **Restart All** (Reiniciar todos) en la lista desplegable **Service Actions** (Acciones del servicio) de la derecha.</span><span class="sxs-lookup"><span data-stu-id="af300-228">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="af300-229">Cuando se le solicite, seleccione **Turn on maintenance mode** (Activar modo de mantenimiento) y, a continuación, "Confirm Restart All" ("Confirmar reiniciar todo").</span><span class="sxs-lookup"><span data-stu-id="af300-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="af300-230">Repita este proceso para MapReduce2 y YARN.</span><span class="sxs-lookup"><span data-stu-id="af300-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="af300-231">Una vez reiniciados los servicios, seleccione cada uno de ellos y deshabilite el modo de mantenimiento en la lista desplegable **Service Actions** (Acciones del servicio).</span><span class="sxs-lookup"><span data-stu-id="af300-231">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="af300-232">Prueba de acceso restringido</span><span class="sxs-lookup"><span data-stu-id="af300-232">Test restricted access</span></span>

<span data-ttu-id="af300-233">Para comprobar que tiene el acceso restringido, utilice los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="af300-233">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="af300-234">Para clústeres de HDInsight **basados en Windows** , use el Escritorio remoto para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-234">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="af300-235">Para más información, vea [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp) (Conectarse a HDInsight mediante RDP).</span><span class="sxs-lookup"><span data-stu-id="af300-235">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="af300-236">Una vez conectado, use el icono de **línea de comandos de Hadoop** en el escritorio para abrir un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="af300-236">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>

* <span data-ttu-id="af300-237">Para clústeres de HDInsight **basados en Linux** , use SSH para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="af300-237">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="af300-238">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="af300-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="af300-239">Una vez conectado al clúster, siga estos pasos para comprobar que solo puede leer y listar elementos en la cuenta de almacenamiento de SAS:</span><span class="sxs-lookup"><span data-stu-id="af300-239">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="af300-240">Para mostrar el contenido del contenedor, utilice el siguiente comando desde el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="af300-240">To list the contents of the container, use the following command from the prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="af300-241">Reemplace **SASCONTAINER** por el nombre del contenedor creado para la cuenta de almacenamiento de SAS.</span><span class="sxs-lookup"><span data-stu-id="af300-241">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="af300-242">Reemplace **SASACCOUNTNAME** por el nombre de la cuenta de almacenamiento utilizada para la firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="af300-242">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS.</span></span>

    <span data-ttu-id="af300-243">La lista incluye el archivo que se cargó al crear el contenedor y la firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="af300-243">The list includes the file uploaded when the container and SAS were created.</span></span>

2. <span data-ttu-id="af300-244">Use el siguiente comando para comprobar que puede leer el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="af300-244">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="af300-245">Reemplace **SASCONTAINER** y **SASACCOUNTNAME** tal como lo ha hecho en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="af300-245">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="af300-246">Reemplace **FILENAME** por el nombre de archivo que aparece en el comando anterior:</span><span class="sxs-lookup"><span data-stu-id="af300-246">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="af300-247">Este comando muestra el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="af300-247">This command lists the contents of the file.</span></span>

3. <span data-ttu-id="af300-248">Use el siguiente comando para descargar el archivo en el sistema de archivos local:</span><span class="sxs-lookup"><span data-stu-id="af300-248">Use the following command to download the file to the local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="af300-249">Este comando descarga el archivo en un archivo local denominado **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="af300-249">This command downloads the file to a local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="af300-250">Use el siguiente comando para cargar el archivo local en un nuevo archivo denominado **testupload.txt** en el almacenamiento de SAS:</span><span class="sxs-lookup"><span data-stu-id="af300-250">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="af300-251">Recibirá un mensaje similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="af300-251">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="af300-252">Este error se produce porque la ubicación de almacenamiento es solo de lectura y lista.</span><span class="sxs-lookup"><span data-stu-id="af300-252">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="af300-253">Use el siguiente comando para colocar los datos en el almacenamiento predeterminado para el clúster, que tiene permiso de escritura:</span><span class="sxs-lookup"><span data-stu-id="af300-253">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="af300-254">Esta vez, la operación debe completarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="af300-254">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="af300-255">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="af300-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="af300-256">Se ha cancelado una tarea</span><span class="sxs-lookup"><span data-stu-id="af300-256">A task was canceled</span></span>

<span data-ttu-id="af300-257">**Síntomas**: al crear un clúster mediante el script de PowerShell, puede recibir el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="af300-257">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="af300-258">**Causa**: este error se puede producir si usa una contraseña para el usuario administrador/HTTP del clúster o, en clústeres basados en Linux, el usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="af300-258">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="af300-259">**Solución**: utilice una contraseña que cumpla los criterios siguientes:</span><span class="sxs-lookup"><span data-stu-id="af300-259">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="af300-260">Debe tener como mínimo 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="af300-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="af300-261">Debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="af300-261">Must contain at least one digit</span></span>
* <span data-ttu-id="af300-262">Debe incluir al menos un carácter no alfanumérico.</span><span class="sxs-lookup"><span data-stu-id="af300-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="af300-263">Debe contener al menos una mayúscula o una minúscula.</span><span class="sxs-lookup"><span data-stu-id="af300-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="af300-264">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af300-264">Next steps</span></span>

<span data-ttu-id="af300-265">Ahora que ha aprendido a agregar almacenamiento de acceso limitado al clúster de HDInsight, obtenga información acerca de otras maneras de trabajar con datos en el clúster:</span><span class="sxs-lookup"><span data-stu-id="af300-265">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="af300-266">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="af300-267">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="af300-268">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
