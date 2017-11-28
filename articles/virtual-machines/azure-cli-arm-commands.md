---
title: comandos de CLI aaaAzure en modo de administrador de recursos | Documentos de Microsoft
description: "Interfaz de línea de comandos (CLI) de Azure comandos toomanage recursos en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="3fee3-103">Comandos de la CLI de Azure en el modo de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3fee3-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="3fee3-104">Este artículo proporciona la sintaxis y opciones de comandos de la interfaz de línea de comandos (CLI) de Azure que lo haría normalmente utilizar toocreate y administración recursos de Azure en el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3fee3-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="3fee3-105">Tener acceso a estos comandos ejecutan Hola CLI en el modo Resource Manager (arm).</span><span class="sxs-lookup"><span data-stu-id="3fee3-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="3fee3-106">Tenga en cuenta que esta no es una referencia completa y que la versión de CLI puede mostrar algunos comandos o parámetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="3fee3-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="3fee3-107">Para obtener una descripción general de los recursos y grupos de recursos de Azure, vea [Información general del grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fee3-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="3fee3-108">Este artículo muestra al administrador de recursos comandos del modo Hola CLI de Azure, que a veces denomina 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fee3-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="3fee3-109">toowork en el modelo de administrador de recursos de hello, también puede intentar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2), nuestro múltiples plataformas próxima generación CLI.</span><span class="sxs-lookup"><span data-stu-id="3fee3-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="3fee3-110">Obtener más información acerca de hello [CLI de Azure antiguos y nuevos](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="3fee3-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="3fee3-111">tooget iniciado, en primer lugar [instalar hello Azure CLI](../cli-install-nodejs.md) y [conectar tooyour suscripción de Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3fee3-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="3fee3-112">Para las opciones en la línea de comandos de hello en el modo de administrador de recursos y la sintaxis de comando actual, escriba `azure help` o toodisplay ayuda para un comando específico, `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="3fee3-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="3fee3-113">También encontrar ejemplos CLI en la documentación de Hola para crear y administrar los servicios de Azure específicos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="3fee3-114">Se muestran parámetros opcionales entre corchetes (por ejemplo, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="3fee3-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="3fee3-115">Los demás parámetros son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="3fee3-115">All other parameters are required.</span></span>

<span data-ttu-id="3fee3-116">En parámetros opcionales de suma toocommand específico documentados en este caso, hay tres parámetros opcionales que pueden ser utilizado toodisplay detallan salida como las opciones de solicitud y códigos de estado.</span><span class="sxs-lookup"><span data-stu-id="3fee3-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="3fee3-117">Hola `-v` parámetro proporciona resultados detallados y hello `-vv` parámetro proporciona incluso más detallada de un resultado detallado.</span><span class="sxs-lookup"><span data-stu-id="3fee3-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="3fee3-118">Hola `--json` opción genera el resultado de hello en formato json sin formato.</span><span class="sxs-lookup"><span data-stu-id="3fee3-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="3fee3-119">Modo de administrador de recursos de configuración Hola</span><span class="sxs-lookup"><span data-stu-id="3fee3-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="3fee3-120">Usar hello después de comandos del modo comando de CLI de Azure Resource Manager tooenable.</span><span class="sxs-lookup"><span data-stu-id="3fee3-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="3fee3-121">modo Azure Resource Manager de CLI de Hola y el modo de administración de servicios de Azure son mutuamente excluyentes.</span><span class="sxs-lookup"><span data-stu-id="3fee3-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="3fee3-122">Es decir, no se pueden administrar recursos creados en un modo de hello otro modo.</span><span class="sxs-lookup"><span data-stu-id="3fee3-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="3fee3-123">cuenta de Azure: administración de la información de la cuenta</span><span class="sxs-lookup"><span data-stu-id="3fee3-123">azure account: Manage your account information</span></span>
<span data-ttu-id="3fee3-124">La información de suscripción de Azure se usa por cuenta de hello herramienta tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="3fee3-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="3fee3-125">**Mostrar las suscripciones de hello importado**</span><span class="sxs-lookup"><span data-stu-id="3fee3-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="3fee3-126">**Mostrar detalles acerca de la suscripción**</span><span class="sxs-lookup"><span data-stu-id="3fee3-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="3fee3-127">**Establecer la suscripción actual de Hola**</span><span class="sxs-lookup"><span data-stu-id="3fee3-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="3fee3-128">**Quitar una suscripción o el entorno o borrar todo del Hola almacena la información de cuenta y entorno**</span><span class="sxs-lookup"><span data-stu-id="3fee3-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="3fee3-129">**Comandos toomanage su entorno de cuenta**</span><span class="sxs-lookup"><span data-stu-id="3fee3-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="3fee3-130">Azure ad: comandos de objetos de Active Directory toodisplay</span><span class="sxs-lookup"><span data-stu-id="3fee3-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="3fee3-131">**Aplicaciones de active directory de toodisplay de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="3fee3-132">**Grupos de active directory de toodisplay de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="3fee3-133">**Comandos tooprovide una información de grupo o miembro de sub de active directory**</span><span class="sxs-lookup"><span data-stu-id="3fee3-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="3fee3-134">**Entidades de servicio de active directory de toodisplay de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="3fee3-135">**Usuarios de active directory de toodisplay de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="3fee3-136">Azure availset: conjuntos de la disponibilidad de toomanage de comandos</span><span class="sxs-lookup"><span data-stu-id="3fee3-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="3fee3-137">**Crea un conjunto de disponibilidad dentro de un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="3fee3-138">**Listas de Hola conjuntos de disponibilidad dentro de un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="3fee3-139">**Obtiene un conjunto de disponibilidad dentro de un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="3fee3-140">**Elimina un conjunto de disponibilidad dentro de un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="3fee3-141">configuración de Azure: comandos toomanage la configuración regional</span><span class="sxs-lookup"><span data-stu-id="3fee3-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="3fee3-142">**Mostrar ajustes de configuración de la CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="3fee3-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="3fee3-143">**Eliminar un valor de configuración**</span><span class="sxs-lookup"><span data-stu-id="3fee3-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="3fee3-144">**Actualizar un valor de configuración**</span><span class="sxs-lookup"><span data-stu-id="3fee3-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="3fee3-145">**Conjuntos de Hola CLI de Azure funciona tooeither modo `arm` o`asm`**</span><span class="sxs-lookup"><span data-stu-id="3fee3-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="3fee3-146">la característica de Azure: características de la cuenta de toomanage de comandos</span><span class="sxs-lookup"><span data-stu-id="3fee3-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="3fee3-147">**Enumera todas las características disponibles para su suscripción**</span><span class="sxs-lookup"><span data-stu-id="3fee3-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="3fee3-148">**Muestra una característica**</span><span class="sxs-lookup"><span data-stu-id="3fee3-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="3fee3-149">**Registra una característica de vista previa de un proveedor de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="3fee3-150">grupo de Azure: comandos toomanage los grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="3fee3-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="3fee3-151">**Crea un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="3fee3-152">**Grupo de recursos de conjunto de etiquetas tooa**</span><span class="sxs-lookup"><span data-stu-id="3fee3-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="3fee3-153">**Elimina un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="3fee3-154">**Enumera los grupos de recursos de hello para la suscripción**</span><span class="sxs-lookup"><span data-stu-id="3fee3-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="3fee3-155">**Muestra un grupo de recursos para la suscripción**</span><span class="sxs-lookup"><span data-stu-id="3fee3-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="3fee3-156">**Registros de grupo de recursos de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="3fee3-157">**Comandos toomanage la implementación en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="3fee3-158">**Comandos toomanage la plantilla de grupo de recursos local o de la Galería**</span><span class="sxs-lookup"><span data-stu-id="3fee3-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="3fee3-159">hdinsight de Azure: comandos toomanage sus clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3fee3-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="3fee3-160">**Comandos toocreate o agregar el archivo de configuración de clúster tooa**</span><span class="sxs-lookup"><span data-stu-id="3fee3-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="3fee3-161">Ejemplo: Crear un archivo de configuración que contiene un toorun de acción de secuencia de comandos al crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="3fee3-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="3fee3-162">**Comando toocreate un clúster en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="3fee3-163">Ejemplo: Crear una clúster de Linux o Storm</span><span class="sxs-lookup"><span data-stu-id="3fee3-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="3fee3-164">Ejemplo: Crear un clúster con una acción de script</span><span class="sxs-lookup"><span data-stu-id="3fee3-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="3fee3-165">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="3fee3-166">**Comando toodelete un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="3fee3-167">**Detalles del comando de clúster tooshow**</span><span class="sxs-lookup"><span data-stu-id="3fee3-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="3fee3-168">**Toolist comando todos los clústeres (en un grupo de recursos específico, si se proporciona)**</span><span class="sxs-lookup"><span data-stu-id="3fee3-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="3fee3-169">**Comando tooresize un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="3fee3-170">**Comando de acceso de tooenable HTTP para un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="3fee3-171">**Comando de acceso de toodisable HTTP para un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="3fee3-172">**Acceso a los comandos tooenable RDP para un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="3fee3-173">**Comando de acceso de toodisable HTTP para un clúster**</span><span class="sxs-lookup"><span data-stu-id="3fee3-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="3fee3-174">visión de Azure: comandos relacionados con la información de toomonitoring (eventos, las reglas de alerta, configuración de escalado automático, las métricas)</span><span class="sxs-lookup"><span data-stu-id="3fee3-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="3fee3-175">**Recuperar registros de operaciones de una suscripción, un correlationId, un grupo de recursos, un recurso o un proveedor de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="3fee3-176">ubicación de Azure: comandos tooget hello las ubicaciones disponibles para todos los tipos de recursos</span><span class="sxs-lookup"><span data-stu-id="3fee3-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="3fee3-177">**Ubicaciones de lista Hola disponibles.**</span><span class="sxs-lookup"><span data-stu-id="3fee3-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="3fee3-178">red de Azure: recursos de red de toomanage de comandos</span><span class="sxs-lookup"><span data-stu-id="3fee3-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="3fee3-179">**Redes virtuales de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="3fee3-180">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="3fee3-180">Creates a virtual network.</span></span> <span data-ttu-id="3fee3-181">Hola siguiente ejemplo se crea una red virtual denominado newvnet para myresourcegroup de grupo de recursos en la región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="3fee3-182">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="3fee3-183">Actualiza una configuración de red virtual dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="3fee3-184">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="3fee3-185">comando de Hello enumera todas las redes virtuales en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="3fee3-186">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="3fee3-187">comando de Hello muestra propiedades de red virtual de hello en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="3fee3-188">comando de Hello quita una red virtual.</span><span class="sxs-lookup"><span data-stu-id="3fee3-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="3fee3-189">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="3fee3-190">**Subredes de red virtual de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="3fee3-191">Agrega otra subred tooan red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="3fee3-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="3fee3-192">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="3fee3-193">Establece una subred de red virtual específica dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="3fee3-194">Enumera todas las subredes de red virtual de Hola para una red virtual específica dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="3fee3-195">Muestra las propiedades de la subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="3fee3-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="3fee3-196">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="3fee3-197">Quita una subred de una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="3fee3-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="3fee3-198">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="3fee3-199">**Equilibradores de carga de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="3fee3-200">Crea un conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="3fee3-201">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="3fee3-202">Enumera los recursos de Equilibrador de carga dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="3fee3-203">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="3fee3-204">Muestra información del equilibrador de un equilibrador de carga específico dentro de un grupo de recursos de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="3fee3-205">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="3fee3-206">Elimina recursos de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="3fee3-207">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="3fee3-208">**Comandos toomanage sondeos de un equilibrador de carga**</span><span class="sxs-lookup"><span data-stu-id="3fee3-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-209">Crear configuración de sondeo de hello para el estado de mantenimiento de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="3fee3-210">Tenga en cuenta toorun este comando, el equilibrador de carga requiere un recurso de ip de front-end (desprotección tooassign un equilibrador de tooload de dirección ip de comando "azure front-end-dirección ip de red").</span><span class="sxs-lookup"><span data-stu-id="3fee3-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="3fee3-211">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-212">Actualiza un sondeo de equilibrador de carga existente con los nuevos valores.</span><span class="sxs-lookup"><span data-stu-id="3fee3-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="3fee3-213">Opciones de parámetro</span><span class="sxs-lookup"><span data-stu-id="3fee3-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="3fee3-214">Propiedades de sondeo de Hola para un conjunto de equilibrador de carga de la lista.</span><span class="sxs-lookup"><span data-stu-id="3fee3-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="3fee3-215">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-216">Quita el sondeo de hello creado para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="3fee3-217">**Configuraciones de ip de front-end de toomanage de comandos de un equilibrador de carga**</span><span class="sxs-lookup"><span data-stu-id="3fee3-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-218">Crea un tooan de configuración de IP de front-end existente conjunto del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-219">Las actualizaciones de una configuración existente de un front-end IP.hello comando siguiente agrega una IP pública denominada mypubip5 tooan existente carga equilibrador IP front-end denominado myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="3fee3-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="3fee3-220">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="3fee3-221">Enumera todos los recursos IP de front-end de hello configurados para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="3fee3-222">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-223">Elimina equilibrador de tooload de objeto asociado de hello front-end IP</span><span class="sxs-lookup"><span data-stu-id="3fee3-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="3fee3-224">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="3fee3-225">**Grupos de direcciones de back-end de toomanage de comandos de un equilibrador de carga**</span><span class="sxs-lookup"><span data-stu-id="3fee3-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-226">Crea un grupo de direcciones de back-end para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="3fee3-227">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="3fee3-228">Enumerar el intervalo de grupo de direcciones IP de backend para un grupo de recursos específicos</span><span class="sxs-lookup"><span data-stu-id="3fee3-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="3fee3-229">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="3fee3-230">grupo de direcciones de red lb eliminar [opciones] < grupo de recursos >< lb-name ><name></span><span class="sxs-lookup"><span data-stu-id="3fee3-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="3fee3-231">Quita el recurso de intervalo de grupo IP de back-end de Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="3fee3-232">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="3fee3-233">**Comandos toomanage reglas del equilibrador de carga**</span><span class="sxs-lookup"><span data-stu-id="3fee3-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-234">Crea reglas de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-234">Create load balancer rules.</span></span>

<span data-ttu-id="3fee3-235">Puede crear una regla de equilibrador de carga configurando punto de conexión de hello front-end de equilibrador de carga de Hola y Hola back-end dirección grupo intervalo tooreceive Hola tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="3fee3-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="3fee3-236">Configuración también incluye puertos hello para el punto de conexión IP de front-end y puertos para el intervalo de grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="3fee3-237">Hello en el ejemplo siguiente se muestra cómo regla toocreate un equilibrador de carga, extremo de front-end de hello escuchando tooport 80 tooport 8080 para el intervalo de grupo de direcciones de back-end de Hola de envío de tráfico de red de TCP y equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-238">Actualiza una regla existente del equilibrador de carga establecida en un grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="3fee3-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="3fee3-239">En el siguiente ejemplo de Hola, hemos cambiado el nombre de la regla de Hola de mylbrule toomynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="3fee3-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="3fee3-240">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="3fee3-241">Enumera todas las reglas configuradas para un equilibrador de carga de un grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="3fee3-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="3fee3-242">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-243">Elimina una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="3fee3-244">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="3fee3-245">**Las reglas NAT de entrada del equilibrador de carga de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-246">Crea una regla NAT de entrada para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="3fee3-247">Hola creamos una regla NAT de la IP de front-end (que se definió anteriormente mediante el comando hello "ip front-end de red de azure") con una entrada de puerto de escucha y el puerto de salida que equilibrador de carga de Hola de ejemplo siguiente utiliza el tráfico de red de toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="3fee3-248">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="3fee3-249">Actualiza una regla NAT de entrada existente.</span><span class="sxs-lookup"><span data-stu-id="3fee3-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="3fee3-250">En el siguiente ejemplo de Hola, hemos cambiado Hola puerto de escucha de too81 80 de entrada.</span><span class="sxs-lookup"><span data-stu-id="3fee3-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="3fee3-251">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="3fee3-252">Enumera todas las reglas NAT de entrada para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3fee3-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="3fee3-253">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="3fee3-254">Elimina la regla NAT para el equilibrador de carga de hello en un grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="3fee3-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="3fee3-255">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="3fee3-256">**Direcciones ip públicas de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="3fee3-257">Crea un recurso de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="3fee3-257">Creates a public ip resource.</span></span> <span data-ttu-id="3fee3-258">Creará recursos de dirección ip pública de Hola y asociar el nombre de dominio tooa.</span><span class="sxs-lookup"><span data-stu-id="3fee3-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="3fee3-259">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="3fee3-260">Actualiza las propiedades de Hola de un recurso de dirección ip pública existente.</span><span class="sxs-lookup"><span data-stu-id="3fee3-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="3fee3-261">En el siguiente ejemplo de Hola hemos cambiado la dirección IP pública Hola de tooStatic dinámica.</span><span class="sxs-lookup"><span data-stu-id="3fee3-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="3fee3-262">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="3fee3-263">network public-ip list [options] &lt;resource-group&gt; Enumera todos los recursos IP públicos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="3fee3-264">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="3fee3-265">red public-ip mostrar [opciones] < grupo de recursos ><name></span><span class="sxs-lookup"><span data-stu-id="3fee3-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="3fee3-266">Muestra las propiedades de la dirección IP pública de un recurso con IP pública dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3fee3-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="3fee3-267">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="3fee3-268">Elimina un recurso de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="3fee3-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="3fee3-269">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="3fee3-270">**Interfaces de red de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="3fee3-271">Crea un recurso denominado interfaz de red (NIC) que puede usarse para equilibradores de carga o asocia tooa Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="3fee3-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="3fee3-272">Opciones de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3fee3-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="3fee3-273">**Grupos de seguridad de red de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="3fee3-274">**Reglas de grupo de seguridad de red de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="3fee3-275">**Perfil del Administrador de tráfico de comandos toomanage**</span><span class="sxs-lookup"><span data-stu-id="3fee3-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="3fee3-276">**Extremos del Administrador de tráfico de comandos toomanage**</span><span class="sxs-lookup"><span data-stu-id="3fee3-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="3fee3-277">**Puertas de enlace de red virtual de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="3fee3-278">el proveedor de Azure: registros de proveedor de recursos de toomanage de comandos</span><span class="sxs-lookup"><span data-stu-id="3fee3-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="3fee3-279">**Enumerar los proveedores registrados actualmente en Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="3fee3-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="3fee3-280">**Mostrar detalles sobre Hola solicitado el espacio de nombres de proveedor**</span><span class="sxs-lookup"><span data-stu-id="3fee3-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="3fee3-281">**Registro del proveedor con la suscripción de Hola**</span><span class="sxs-lookup"><span data-stu-id="3fee3-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="3fee3-282">**Anular el registro del proveedor con la suscripción de Hola**</span><span class="sxs-lookup"><span data-stu-id="3fee3-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="3fee3-283">recursos de Azure: comandos toomanage los recursos</span><span class="sxs-lookup"><span data-stu-id="3fee3-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="3fee3-284">**Crea un recurso en un grupo de recursos.**</span><span class="sxs-lookup"><span data-stu-id="3fee3-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="3fee3-285">**Actualiza un recurso en un grupo de recursos sin parámetros ni plantillas.**</span><span class="sxs-lookup"><span data-stu-id="3fee3-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="3fee3-286">**Recursos de Hola de listas**</span><span class="sxs-lookup"><span data-stu-id="3fee3-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="3fee3-287">**Obtiene un recurso dentro de un grupo de recursos o la suscripción.**</span><span class="sxs-lookup"><span data-stu-id="3fee3-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="3fee3-288">**Elimina un recurso en un grupo de recursos.**</span><span class="sxs-lookup"><span data-stu-id="3fee3-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="3fee3-289">rol de Azure: comandos toomanage los roles de Azure</span><span class="sxs-lookup"><span data-stu-id="3fee3-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="3fee3-290">**Obtener todas las definiciones de rol disponibles**</span><span class="sxs-lookup"><span data-stu-id="3fee3-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="3fee3-291">**Obtener una definición de rol disponible**</span><span class="sxs-lookup"><span data-stu-id="3fee3-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="3fee3-292">**Comandos toomanage su asignación de roles**</span><span class="sxs-lookup"><span data-stu-id="3fee3-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="3fee3-293">almacenamiento de Azure: comandos toomanage los objetos de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3fee3-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="3fee3-294">**Comandos toomanage sus cuentas de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="3fee3-295">**Comandos toomanage las claves de cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="3fee3-296">**Comandos tooshow la cadena de conexión de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="3fee3-297">**Comandos toomanage los contenedores de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="3fee3-298">**Comandos toomanage compartida las firmas de acceso de su contenedor de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="3fee3-299">**Comandos toomanage almacena las directivas de acceso de su contenedor de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="3fee3-300">**Comandos toomanage los blobs de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="3fee3-301">**Comandos toomanage las operaciones de copia de blob**</span><span class="sxs-lookup"><span data-stu-id="3fee3-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="3fee3-302">**Firma de acceso compartido toomanage de comandos de su almacenamiento de blobs**</span><span class="sxs-lookup"><span data-stu-id="3fee3-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="3fee3-303">**Comandos toomanage los recursos compartidos de archivos de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="3fee3-304">**Comandos toomanage los archivos de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="3fee3-305">**Comandos toomanage el directorio de archivos de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="3fee3-306">**Comandos toomanage las colas de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="3fee3-307">**Comandos toomanage compartida las firmas de acceso de la cola de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="3fee3-308">**Comandos toomanage almacena las directivas de acceso de la cola de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="3fee3-309">**Comandos toomanage las propiedades de registro de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="3fee3-310">**Comandos toomanage las propiedades de métricas de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="3fee3-311">**Comandos toomanage las tablas de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="3fee3-312">**Comandos toomanage compartida las firmas de acceso de la tabla de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="3fee3-313">**Comandos toomanage almacena las directivas de acceso de la tabla de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3fee3-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="3fee3-314">etiqueta de Azure: comandos toomanage su etiqueta del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="3fee3-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="3fee3-315">**Agregar una etiqueta**</span><span class="sxs-lookup"><span data-stu-id="3fee3-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="3fee3-316">**Quitar una etiqueta o un valor de etiqueta**</span><span class="sxs-lookup"><span data-stu-id="3fee3-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="3fee3-317">**Muestra información de etiqueta de Hola**</span><span class="sxs-lookup"><span data-stu-id="3fee3-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="3fee3-318">**Obtener una etiqueta**</span><span class="sxs-lookup"><span data-stu-id="3fee3-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="3fee3-319">máquina virtual de Azure: comandos toomanage las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="3fee3-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="3fee3-320">**Crear una máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="3fee3-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="3fee3-321">**Crear una máquina virtual con los recursos predeterminados**</span><span class="sxs-lookup"><span data-stu-id="3fee3-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="3fee3-322">A partir de CLI versión 0.10, puede proporcionar un alias corto como "UbuntuLTS" o "Win2012R2Datacenter" como hello `image-urn` para algunas imágenes de Marketplace populares.</span><span class="sxs-lookup"><span data-stu-id="3fee3-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="3fee3-323">Ejecute `azure help vm quick-create` para ver las opciones.</span><span class="sxs-lookup"><span data-stu-id="3fee3-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="3fee3-324">Además, empezando con la versión 0.10, `azure vm quick-create` usa almacenamiento premium de forma predeterminada, si está disponible en la región seleccionada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fee3-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="3fee3-325">**Enumerar Hola máquinas de virtuales dentro de una cuenta**</span><span class="sxs-lookup"><span data-stu-id="3fee3-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="3fee3-326">**Obtener una máquina virtual en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="3fee3-327">**Eliminar una máquina virtual en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="3fee3-328">**Cerrar una máquina virtual en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="3fee3-329">**Reiniciar una máquina virtual en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="3fee3-330">**Iniciar una máquina virtual en un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="3fee3-331">**Recursos de proceso de cierre una máquina virtual dentro de un saludo de grupo y las versiones de recursos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="3fee3-332">**Enumerar los tamaños disponibles de máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="3fee3-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="3fee3-333">**Capturar Hola VM como imagen del sistema operativo o la imagen de máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="3fee3-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="3fee3-334">**Establecer estado de Hola de hello VM tooGeneralized**</span><span class="sxs-lookup"><span data-stu-id="3fee3-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="3fee3-335">**Obtener la vista de instancia de hello VM**</span><span class="sxs-lookup"><span data-stu-id="3fee3-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="3fee3-336">**Habilitar la configuración de acceso de escritorio remoto o SSH tooreset en una máquina Virtual y la contraseña de hello tooreset de cuenta de hello que tiene administrador o autoridad «sudo»**</span><span class="sxs-lookup"><span data-stu-id="3fee3-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="3fee3-337">**Actualizar la máquina virtual con nuevos datos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="3fee3-338">**Comandos toomanage los discos de datos de máquina Virtual**</span><span class="sxs-lookup"><span data-stu-id="3fee3-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="3fee3-339">**Extensiones de recursos de máquina virtual de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="3fee3-340">**Comandos toomanage la máquina Virtual de Docker**</span><span class="sxs-lookup"><span data-stu-id="3fee3-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="3fee3-341">**Imágenes de máquina virtual de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="3fee3-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
