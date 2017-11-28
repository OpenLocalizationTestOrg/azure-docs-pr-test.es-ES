---
title: acceso de aaaRestrict mediante firmas de acceso compartido - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse firmas de acceso compartido toorestrict HDInsight acceso toodata almacenado en blobs de almacenamiento de Azure."
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
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="0ee23-103">Usar firmas de acceso compartido de almacenamiento de Azure toorestrict acceso toodata en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee23-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="0ee23-104">HDInsight tiene acceso completo toodata en cuentas de almacenamiento de Azure de hello asociadas Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="0ee23-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="0ee23-105">Puede usar firmas de acceso compartido en los datos de hello blob contenedor toorestrict acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="0ee23-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="0ee23-106">Por ejemplo, tooprovide acceso de solo lectura toohello los datos.</span><span class="sxs-lookup"><span data-stu-id="0ee23-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="0ee23-107">Las firmas de acceso compartido (SAS) son una característica de cuentas de almacenamiento de Azure que le permite toolimit acceso toodata.</span><span class="sxs-lookup"><span data-stu-id="0ee23-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="0ee23-108">Por ejemplo, proporcionar toodata de acceso de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="0ee23-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ee23-109">Para una solución con Apache Ranger, considere la posibilidad de usar HDInsight unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="0ee23-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="0ee23-110">Para obtener más información, vea hello [configurar Unidos al dominio HDInsight](hdinsight-domain-joined-configure.md) documento.</span><span class="sxs-lookup"><span data-stu-id="0ee23-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="0ee23-111">HDInsight debe tener el almacenamiento de acceso completo toohello predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="0ee23-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0ee23-112">Requirements</span></span>

* <span data-ttu-id="0ee23-113">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="0ee23-113">An Azure subscription</span></span>
* <span data-ttu-id="0ee23-114">C# o Python.</span><span class="sxs-lookup"><span data-stu-id="0ee23-114">C# or Python.</span></span> <span data-ttu-id="0ee23-115">El código de ejemplo de C# se proporciona como una solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ee23-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="0ee23-116">Se debe usar la versión de Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="0ee23-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="0ee23-117">Se debe usar la versión de Python 2.7 o superior.</span><span class="sxs-lookup"><span data-stu-id="0ee23-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="0ee23-118">Un clúster de HDInsight basados en Linux o [Azure PowerShell] [ powershell] -si tiene un clúster existente basada en Linux, puede usar Ambari tooadd un clúster de toohello de firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="0ee23-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="0ee23-119">Si no es así, puede usar Azure PowerShell toocreate un clúster y agregar una firma de acceso compartido durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="0ee23-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0ee23-120">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="0ee23-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0ee23-121">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0ee23-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0ee23-122">Hola archivos de ejemplo de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="0ee23-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="0ee23-123">Este repositorio incluye Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0ee23-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="0ee23-124">Un proyecto de Visual Studio que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee23-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="0ee23-125">Un script de Python que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee23-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="0ee23-126">Un script de PowerShell que puede crear un HDInsight de clúster y configurar toouse Hola SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="0ee23-127">Las firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="0ee23-127">Shared Access Signatures</span></span>

<span data-ttu-id="0ee23-128">Hay dos formas de firmas de acceso compartido:</span><span class="sxs-lookup"><span data-stu-id="0ee23-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="0ee23-129">Ad hoc: Hola hora de inicio, la hora de expiración y permisos para hello SAS se especifican en hello URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="0ee23-130">Directiva de acceso almacenada: se define una directiva de acceso almacenada en un contenedor de recursos, como un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="0ee23-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="0ee23-131">Una directiva puede tener restricciones toomanage usado para una o varias firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="0ee23-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="0ee23-132">Al asociar una SAS con una directiva de acceso almacenada, Hola SAS hereda las restricciones de hello: Hola hora de inicio, la hora de expiración y permisos - definidos para la directiva de acceso de hello almacenado.</span><span class="sxs-lookup"><span data-stu-id="0ee23-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="0ee23-133">Hello diferencia entre Hola dos formatos es importante para un escenario clave: revocación.</span><span class="sxs-lookup"><span data-stu-id="0ee23-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="0ee23-134">Una SAS es una dirección URL, por lo que cualquier persona que obtiene Hola SAS puede utilizar, independientemente de quién lo ha solicitado toobegin con.</span><span class="sxs-lookup"><span data-stu-id="0ee23-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="0ee23-135">Si una SAS se publica públicamente, se puede utilizar cualquier usuario de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="0ee23-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="0ee23-136">Una SAS distribuida es válida hasta que se produzca una de las cuatro situaciones:</span><span class="sxs-lookup"><span data-stu-id="0ee23-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="0ee23-137">hora de expiración de Hello especificado en hello que SAS se alcanza.</span><span class="sxs-lookup"><span data-stu-id="0ee23-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="0ee23-138">hora de expiración de Hello especificado en la directiva de acceso de hello almacenado al que hace referencia Hola que SAS se alcanza.</span><span class="sxs-lookup"><span data-stu-id="0ee23-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="0ee23-139">los escenarios siguientes Hello causa un tiempo de expiración hello toobe alcanzado:</span><span class="sxs-lookup"><span data-stu-id="0ee23-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="0ee23-140">ha transcurrido el intervalo de tiempo de saludo.</span><span class="sxs-lookup"><span data-stu-id="0ee23-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="0ee23-141">Directiva de acceso de Hello almacenado es toohave modificado una hora de expiración en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="0ee23-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="0ee23-142">Al cambiar la hora de expiración de hello es una manera de toorevoke Hola SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="0ee23-143">Hola almacenado al que hace referencia Hola que SAS se elimina, que es hello de toorevoke de otra manera SAS de directiva de acceso.</span><span class="sxs-lookup"><span data-stu-id="0ee23-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="0ee23-144">Si vuelve a crear la directiva de acceso Hola almacenado con hello mismo nombre, todos los tokens SAS de directiva anterior Hola son válidos (si no ha superado la hora de expiración de hello en hello SAS).</span><span class="sxs-lookup"><span data-stu-id="0ee23-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="0ee23-145">Si piensa toorevoke Hola SAS, ser seguro toouse un nombre diferente si vuelve a crear la directiva de acceso Hola con una hora de expiración en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="0ee23-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="0ee23-146">clave de la cuenta de Hello que estaba toocreate usado Hola SAS se vuelve a generar.</span><span class="sxs-lookup"><span data-stu-id="0ee23-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="0ee23-147">Regenerando la clave de hello hace que todas las aplicaciones que usan la autenticación de clave toofail anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="0ee23-148">Actualizar todos los componentes toohello nueva clave.</span><span class="sxs-lookup"><span data-stu-id="0ee23-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ee23-149">Un URI de firma de acceso compartido está asociado a la firma de hello cuenta clave toocreate usado Hola y Hola asociados directiva de acceso almacenada (si existe).</span><span class="sxs-lookup"><span data-stu-id="0ee23-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="0ee23-150">Si no se especifica ninguna directiva de acceso almacenada, hello toorevoke de manera sólo firma de acceso compartido es toochange Hola cuenta clave.</span><span class="sxs-lookup"><span data-stu-id="0ee23-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="0ee23-151">Se recomienda usar siempre las directivas de acceso almacenadas.</span><span class="sxs-lookup"><span data-stu-id="0ee23-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="0ee23-152">Al utilizar las directivas almacenadas, puede revocar las firmas o ampliar la fecha de expiración de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0ee23-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="0ee23-153">pasos de Hello en este documento utiliza toogenerate de directivas de acceso almacenada SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="0ee23-154">Para obtener más información sobre firmas de acceso compartido, consulte [modelo SAS de descripción hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="0ee23-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="0ee23-155">Creación de una directiva almacenada y una SAS mediante C\#</span><span class="sxs-lookup"><span data-stu-id="0ee23-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="0ee23-156">Abra la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ee23-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="0ee23-157">En el Explorador de soluciones, haga doble clic en hello **SASToken** de proyecto y seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ee23-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="0ee23-158">Seleccione **configuración** y agregue los valores de hello siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="0ee23-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="0ee23-159">StorageConnectionString: Hola cadena de conexión de cuenta de almacenamiento de Hola que desea que toocreate una directiva almacenada y la SAS para.</span><span class="sxs-lookup"><span data-stu-id="0ee23-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="0ee23-160">Hola formato debe ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` donde `myaccount` es Hola nombre de la cuenta de almacenamiento y `mykey` es clave Hola Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee23-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="0ee23-161">ContainerName: contenedor de hello de cuenta de almacenamiento de Hola que desee tener acceso toorestrict a.</span><span class="sxs-lookup"><span data-stu-id="0ee23-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="0ee23-162">SASPolicyName: Hola nombre toouse para hello almacena toocreate de directiva.</span><span class="sxs-lookup"><span data-stu-id="0ee23-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="0ee23-163">FileToUpload: ruta de acceso tooa archivo hello que es cargado toohello contenedor.</span><span class="sxs-lookup"><span data-stu-id="0ee23-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="0ee23-164">Ejecute el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-164">Run hello project.</span></span> <span data-ttu-id="0ee23-165">Información toohello similar después de texto se muestra una vez que se ha generado Hola SAS:</span><span class="sxs-lookup"><span data-stu-id="0ee23-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="0ee23-166">Guarde el token de directiva SAS de hello, el nombre de la cuenta de almacenamiento y el nombre del contenedor.</span><span class="sxs-lookup"><span data-stu-id="0ee23-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="0ee23-167">Estos valores se utilizan al asociar la cuenta de almacenamiento de Hola a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee23-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="0ee23-168">Creación de una directiva almacenada y una SAS mediante Python</span><span class="sxs-lookup"><span data-stu-id="0ee23-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="0ee23-169">Abrir archivo SASToken.py de hello y cambiar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0ee23-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="0ee23-170">directiva\_nombre: Hola nombre toouse para hello almacenado toocreate de directiva.</span><span class="sxs-lookup"><span data-stu-id="0ee23-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="0ee23-171">almacenamiento\_cuenta\_nombre: nombre de hello de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee23-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="0ee23-172">almacenamiento\_cuenta\_clave: Hola clave Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee23-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="0ee23-173">almacenamiento\_contenedor\_nombre: contenedor Hola de cuenta de almacenamiento de Hola que desee tener acceso toorestrict a.</span><span class="sxs-lookup"><span data-stu-id="0ee23-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="0ee23-174">en el ejemplo se\_archivo\_ruta de acceso: Hola ruta tooa archivo que es cargado toohello contenedor.</span><span class="sxs-lookup"><span data-stu-id="0ee23-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="0ee23-175">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-175">Run hello script.</span></span> <span data-ttu-id="0ee23-176">Muestra hello SAS token similar toohello después de texto cuando se completa el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="0ee23-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="0ee23-177">Guarde el token de directiva SAS de hello, el nombre de la cuenta de almacenamiento y el nombre del contenedor.</span><span class="sxs-lookup"><span data-stu-id="0ee23-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="0ee23-178">Estos valores se utilizan al asociar la cuenta de almacenamiento de Hola a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee23-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="0ee23-179">Usar SAS Hola con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee23-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="0ee23-180">Al crear un clúster de HDInsight, debe especificar una cuenta de almacenamiento principal y puede especificar, opcionalmente, cuentas de almacenamiento adicionales.</span><span class="sxs-lookup"><span data-stu-id="0ee23-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="0ee23-181">Ambos métodos de adición de almacenamiento requieren cuentas de almacenamiento de toohello de acceso completo y contenedores que se utilizan.</span><span class="sxs-lookup"><span data-stu-id="0ee23-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="0ee23-182">toouse un contenedor tooa de acceso de toolimit de firma de acceso compartido, agregar una entrada personalizada toohello **core sitio** configuración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="0ee23-183">Para **basados en Windows** o **basados en Linux** clústeres de HDInsight, puede agregar la entrada de Hola durante su creación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ee23-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="0ee23-184">Para **basados en Linux** clústeres de HDInsight, cambiar la configuración de hello después de la creación de clúster con Ambari.</span><span class="sxs-lookup"><span data-stu-id="0ee23-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="0ee23-185">Crear un clúster que usa Hola SAS</span><span class="sxs-lookup"><span data-stu-id="0ee23-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="0ee23-186">Un ejemplo de creación de un clúster de HDInsight que hello usa SAS se incluye en hello `CreateCluster` directorio del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="0ee23-187">toouse, Hola de uso después avanza:</span><span class="sxs-lookup"><span data-stu-id="0ee23-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="0ee23-188">Abra hello `CreateCluster\HDInsightSAS.ps1` archivo en un editor de texto y modifique Hola siguiente valores al principio de saludo del documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="0ee23-189">Por ejemplo, cambiar `'mycluster'` toohello nombre del clúster de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="0ee23-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="0ee23-190">valores de Hello SAS deben coincidir con valores de hello de los pasos anteriores de hello al crear una cuenta de almacenamiento y el token de SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="0ee23-191">Una vez que han cambiado los valores de hello, guarde el archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="0ee23-192">Abra un nuevo símbolo del sistema de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ee23-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="0ee23-193">Si no está familiarizado con Azure PowerShell, o si no lo ha instalado, consulte [Cómo instalar y configurar Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="0ee23-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="0ee23-194">Desde el símbolo del sistema de hello, utilice Hola después comando tooauthenticate tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="0ee23-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="0ee23-195">Cuando se le solicite, inicie sesión con la cuenta de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee23-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="0ee23-196">Si su cuenta está asociada a varias suscripciones de Azure, puede que necesite toouse `Select-AzureRmSubscription` suscripción de hello tooselect desea toouse.</span><span class="sxs-lookup"><span data-stu-id="0ee23-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="0ee23-197">Desde el símbolo del sistema de hello, cambiar directorios toohello `CreateCluster` directorio que contiene el archivo de hello HDInsightSAS.ps1.</span><span class="sxs-lookup"><span data-stu-id="0ee23-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="0ee23-198">A continuación, usar hello sigue la secuencia de comandos de hello toorun</span><span class="sxs-lookup"><span data-stu-id="0ee23-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="0ee23-199">Durante la ejecución de secuencias de comandos hello, registra el símbolo del sistema de salida toohello PowerShell mientras crea recursos Hola cuentas de grupo y de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee23-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="0ee23-200">Eres usuario de hello HTTP tooenter solicitadas para hello clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee23-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="0ee23-201">Esta cuenta es el clúster de toohello de acceso HTTP/s toosecure usado.</span><span class="sxs-lookup"><span data-stu-id="0ee23-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="0ee23-202">Si está creando un clúster basado en Linux, se le solicitará un nombre de cuenta de usuario SSH y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="0ee23-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="0ee23-203">Esta cuenta es registro tooremotely usado en clúster toohello.</span><span class="sxs-lookup"><span data-stu-id="0ee23-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0ee23-204">Cuando se le solicite Hola HTTP/s o SSH nombre de usuario y contraseña, debe proporcionar una contraseña que cumpla Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="0ee23-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="0ee23-205">Debe tener como mínimo 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0ee23-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="0ee23-206">Debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="0ee23-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="0ee23-207">Debe incluir al menos un carácter no alfanumérico.</span><span class="sxs-lookup"><span data-stu-id="0ee23-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="0ee23-208">Debe contener al menos una mayúscula o una minúscula.</span><span class="sxs-lookup"><span data-stu-id="0ee23-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="0ee23-209">Se tarda un tiempo para este toocomplete de secuencia de comandos, normalmente unos 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="0ee23-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="0ee23-210">Cuando se completa en el script de Hola sin errores, se ha creado el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="0ee23-211">Usar SAS Hola con un clúster existente</span><span class="sxs-lookup"><span data-stu-id="0ee23-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="0ee23-212">Si tiene un clúster existente basada en Linux, puede agregar Hola SAS toohello **core sitio** configuración mediante el uso de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="0ee23-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="0ee23-213">Abra hello Ambari web interfaz de usuario para el clúster.</span><span class="sxs-lookup"><span data-stu-id="0ee23-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="0ee23-214">Hola una dirección de esta página es https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0ee23-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0ee23-215">Cuando se le solicite, autenticar clúster toohello con nombre de administrador de hello (admin) y contraseña que ha utilizado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="0ee23-216">En hello parte izquierda de la interfaz de usuario de web de Ambari hello, seleccione **HDFS** y, a continuación, seleccione hello **configuraciones** ficha en medio de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="0ee23-217">Seleccione hello **avanzadas** ficha y, a continuación, desplácese hasta que encuentre hello **personalizado core-sitio** sección.</span><span class="sxs-lookup"><span data-stu-id="0ee23-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="0ee23-218">Expanda hello **personalizado core-sitio** sección, a continuación, final de desplazamiento toohello y seleccione hello **Agregar propiedad... ** vínculo.</span><span class="sxs-lookup"><span data-stu-id="0ee23-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="0ee23-219">Los valores siguientes de Hola de uso para hello **clave** y **valor** campos:</span><span class="sxs-lookup"><span data-stu-id="0ee23-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="0ee23-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="0ee23-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="0ee23-221">**Valor**: Hola SAS devolviendo Hola aplicación de C# o Python haya ejecutado anteriormente</span><span class="sxs-lookup"><span data-stu-id="0ee23-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="0ee23-222">Reemplace **CONTAINERNAME** con el nombre del contenedor de Hola usó con la aplicación de C# o SAS de hello.</span><span class="sxs-lookup"><span data-stu-id="0ee23-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="0ee23-223">Reemplace **STORAGEACCOUNTNAME** con nombre de la cuenta de almacenamiento Hola ha usado.</span><span class="sxs-lookup"><span data-stu-id="0ee23-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="0ee23-224">Haga clic en hello **agregar** toosave esta clave y valor, a continuación, haga clic en hello **guardar** botón cambios de configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="0ee23-225">Cuando se le pida, agregue una descripción de cambio de hello ("Agregar acceso de almacenamiento SAS" por ejemplo) y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ee23-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="0ee23-226">Haga clic en **Aceptar** cuando se hayan completado los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0ee23-227">Debe reiniciar varios servicios para que hello cambio surta efecto.</span><span class="sxs-lookup"><span data-stu-id="0ee23-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="0ee23-228">En la interfaz de usuario del web Ambari hello, seleccione **HDFS** en lista de Hola Hola izquierda y, a continuación, seleccione **reiniciar todos los** de hello **acciones de servicio** lista desplegable lista de hello derecho.</span><span class="sxs-lookup"><span data-stu-id="0ee23-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="0ee23-229">Cuando se le solicite, seleccione **Turn on maintenance mode** (Activar modo de mantenimiento) y, a continuación, "Confirm Restart All" ("Confirmar reiniciar todo").</span><span class="sxs-lookup"><span data-stu-id="0ee23-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="0ee23-230">Repita este proceso para MapReduce2 y YARN.</span><span class="sxs-lookup"><span data-stu-id="0ee23-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="0ee23-231">Una vez que se hayan reiniciado los servicios de hello, seleccione cada uno de ellos y deshabilitar el modo de mantenimiento de hello **acciones de servicio** de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0ee23-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="0ee23-232">Prueba de acceso restringido</span><span class="sxs-lookup"><span data-stu-id="0ee23-232">Test restricted access</span></span>

<span data-ttu-id="0ee23-233">tooverify que ha restringido el acceso, Hola de uso siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="0ee23-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="0ee23-234">Para **basados en Windows** clústeres de HDInsight, use el clúster de toohello tooconnect de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="0ee23-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="0ee23-235">Para obtener más información, consulte [conectar tooHDInsight mediante RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="0ee23-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="0ee23-236">Una vez conectado, usar hello **Hadoop de línea de comandos** icono en hello escritorio tooopen un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0ee23-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="0ee23-237">Para **basados en Linux** clústeres de HDInsight, utilizar SSH tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="0ee23-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="0ee23-238">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0ee23-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="0ee23-239">Una vez conectado toohello clúster, use Hola después tooverify pasos que sólo se pueden leer y mostrar elementos en la cuenta de almacenamiento SAS hello:</span><span class="sxs-lookup"><span data-stu-id="0ee23-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="0ee23-240">contenido de hello toolist del contenedor de hello, utilice Hola siguiente comando desde el símbolo del sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="0ee23-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="0ee23-241">Reemplace **SASCONTAINER** con nombre hello del contenedor de hello creado para la cuenta de almacenamiento SAS Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="0ee23-242">Reemplace **SASACCOUNTNAME** con el nombre de Hola de cuenta de almacenamiento de hello usada para hello SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="0ee23-243">lista de Hello incluye archivo hello cargado cuando se creó el contenedor de Hola y SAS.</span><span class="sxs-lookup"><span data-stu-id="0ee23-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="0ee23-244">Usar hello después tooverify de comando que se puede leer el contenido de hello del archivo hello.</span><span class="sxs-lookup"><span data-stu-id="0ee23-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="0ee23-245">Reemplace hello **SASCONTAINER** y **SASACCOUNTNAME** como en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="0ee23-246">Reemplace **FILENAME** con nombre de hello del archivo de hello muestra en el comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="0ee23-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="0ee23-247">Este comando muestra el contenido de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="0ee23-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="0ee23-248">Usar hello después de sistema de archivos local de comando toodownload Hola archivo toohello:</span><span class="sxs-lookup"><span data-stu-id="0ee23-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="0ee23-249">Este comando descargas Hola tooa archivo local denominado **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="0ee23-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="0ee23-250">Siguiente Hola de uso del comando tooupload Hola archivo local tooa nuevo archivo denominado **testupload.txt** en hello almacenamiento SAS:</span><span class="sxs-lookup"><span data-stu-id="0ee23-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="0ee23-251">Recibirá un toohello similar de mensaje siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0ee23-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="0ee23-252">Este error se produce debido a la ubicación de almacenamiento de hello lectura + lista solo.</span><span class="sxs-lookup"><span data-stu-id="0ee23-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="0ee23-253">Usar hello siguiente datos de hello tooput de comando de almacenamiento predeterminado de hello para el clúster hello, que se puede escribir:</span><span class="sxs-lookup"><span data-stu-id="0ee23-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="0ee23-254">En esta ocasión, operación Hola debe completarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="0ee23-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0ee23-255">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="0ee23-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="0ee23-256">Se ha cancelado una tarea</span><span class="sxs-lookup"><span data-stu-id="0ee23-256">A task was canceled</span></span>

<span data-ttu-id="0ee23-257">**Síntomas**: al crear un clúster con la secuencia de comandos de PowerShell de hello, es posible que reciba Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ee23-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="0ee23-258">**Causa**: este error puede producirse si usa una contraseña de usuario de administrador/HTTP hello para el clúster de Hola o (para los clústeres basados en Linux) usuario SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee23-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="0ee23-259">**Resolución**: usar una contraseña que cumpla Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="0ee23-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="0ee23-260">Debe tener como mínimo 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0ee23-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="0ee23-261">Debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="0ee23-261">Must contain at least one digit</span></span>
* <span data-ttu-id="0ee23-262">Debe incluir al menos un carácter no alfanumérico.</span><span class="sxs-lookup"><span data-stu-id="0ee23-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="0ee23-263">Debe contener al menos una mayúscula o una minúscula.</span><span class="sxs-lookup"><span data-stu-id="0ee23-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ee23-264">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ee23-264">Next steps</span></span>

<span data-ttu-id="0ee23-265">Ahora que ha aprendido cómo tooadd almacenamiento limitado con acceso tooyour clúster de HDInsight, obtenga información acerca de otro toowork formas con datos en el clúster:</span><span class="sxs-lookup"><span data-stu-id="0ee23-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="0ee23-266">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee23-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0ee23-267">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee23-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0ee23-268">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee23-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
