---
title: "clústeres de HDInsight aaaCustomize mediante acciones de script - Azure | Documentos de Microsoft"
description: "Agregar componentes personalizados de que clústeres de HDInsight basados en tooLinux mediante acciones de Script. Acciones de script son scripts de Bash que pueden ser usado toocustomize configuración de clúster de Hola o agregar servicios adicionales y utilidades como el matiz, Solr o R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="3e5b5-104">Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)</span><span class="sxs-lookup"><span data-stu-id="3e5b5-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="3e5b5-105">HDInsight proporciona una opción de configuración denominada **acción de secuencia de comandos** que invoca scripts personalizados que personalizan el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="3e5b5-106">Estas secuencias de comandos son tooinstall usa componentes adicionales y cambiar la configuración.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="3e5b5-107">Las acciones de script pueden usarse durante la creación del clúster o después.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-108">acciones de script de Hola capacidad toouse en un clúster ya se está ejecutando solo está disponible para clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="3e5b5-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e5b5-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="3e5b5-111">Acciones de script también pueden ser publicado toohello Azure Marketplace como una aplicación de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="3e5b5-112">Algunos ejemplos de hello en este documento muestran cómo puede instalar una aplicación de HDInsight mediante comandos de acción de secuencia de comandos de PowerShell y Hola .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="3e5b5-113">Para obtener más información sobre las aplicaciones de HDInsight, vea [HDInsight publicar aplicaciones en Azure Marketplace hello](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="3e5b5-114">Permisos</span><span class="sxs-lookup"><span data-stu-id="3e5b5-114">Permissions</span></span>

<span data-ttu-id="3e5b5-115">Si está usando un clúster de HDInsight Unidos a un dominio, hay dos permisos Ambari que son necesarios para usar acciones de script con el clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="3e5b5-116">**AMBARI. EJECUTAR\_personalizado\_comando**: rol de administrador de Ambari de hello tiene este permiso de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="3e5b5-117">**CLÚSTER. EJECUTAR\_personalizado\_comando**: tanto el Administrador de clústeres de HDInsight de Hola y Ambari Administrador tienen este permiso de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="3e5b5-118">Para más información sobre cómo trabajar con permisos con clústeres de HDInsight unidos a un dominio, consulte [Administrar clústeres de HDInsight unidos a un dominio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="3e5b5-119">Control de acceso</span><span class="sxs-lookup"><span data-stu-id="3e5b5-119">Access control</span></span>

<span data-ttu-id="3e5b5-120">Si no estás Hola administrador o propietario de la suscripción de Azure, la cuenta debe tener al menos **colaborador** grupo de recursos de toohello de acceso que contiene el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="3e5b5-121">Además, si está creando un clúster de HDInsight, alguien que tenga al menos **colaborador** acceso toohello suscripción de Azure debe haber registrado previamente proveedor Hola para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="3e5b5-122">Registro del proveedor se produce cuando un usuario con la suscripción de colaborador acceso toohello crea un recurso de hello primera vez en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="3e5b5-123">También puede realizarse sin crear ningún recurso mediante el [registro de un proveedor con REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="3e5b5-124">Para obtener más información sobre cómo trabajar con la administración de acceso, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="3e5b5-125">Empezar a trabajar con la administración de acceso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="3e5b5-126">Usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="3e5b5-127">Descripción de las acciones de script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-127">Understanding Script Actions</span></span>

<span data-ttu-id="3e5b5-128">Una acción de script es simplemente un script de Bash al que proporciona un URI y para el que proporciona parámetros.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="3e5b5-129">Hola script se ejecuta en nodos de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-130">Hola continuación se indican las características y las características de las acciones de script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="3e5b5-131">Se debe almacenar en un URI que sea accesible desde el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-132">siguiente Hola es ubicaciones de almacenamiento posibles:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="3e5b5-133">Un **almacén de Azure Data Lake** cuenta que sea accesible para el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-134">Para más información sobre el uso de Azure Data Lake Store con HDInsight, consulte [Creación de un clúster de HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="3e5b5-135">Cuando se usa un script almacenado en el almacén de Data Lake, el formato del URI de hello es `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3e5b5-136">Hola servicio principal HDInsight utiliza tooaccess almacén de Data Lake debe tener acceso de lectura toohello script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="3e5b5-137">Un blob en un **cuenta de almacenamiento de Azure** que es cualquier cuenta de almacenamiento principal o adicional de hello para el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-138">HDInsight se concede acceso tooboth de estos tipos de cuentas de almacenamiento durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="3e5b5-139">Un servicio público de uso compartido de archivos, como Azure Blob, GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="3e5b5-140">Por ejemplo, URI, consulte hello [secuencias de comandos de acción de secuencia de comandos de ejemplo](#example-script-action-scripts) sección.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="3e5b5-141">HDInsight solo admite cuentas de Azure Storage de __uso general__.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="3e5b5-142">No es compatible actualmente con hello __almacenamiento de blobs__ tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="3e5b5-143">Pueden estar restringidas demasiado**ejecutar en solo determinados tipos de nodos**, por nodos principales del ejemplo o nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3e5b5-144">Cuando se usa con HDInsight Premium, puede especificar que se debe usar el script de hello en el nodo del borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="3e5b5-145">Puede ser **persistente** o **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="3e5b5-146">**Conserva** scripts son tooworker aplicada con nodos toohello agregado clústeres después de ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="3e5b5-147">Por ejemplo, cuando se escala ascendentemente clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="3e5b5-148">Un script persistente también podría aplicar el tipo de nodo tooanother cambios, por ejemplo, un nodo principal.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3e5b5-149">Las acciones de scripts persistentes deben tener un nombre único.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="3e5b5-150">Los scripts **ad hoc** no son persistentes.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="3e5b5-151">No son clúster toohello agregado de tooworker aplicado nodos después de que se ejecutó el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="3e5b5-152">Posteriormente puede promover una secuencia de comandos ad hoc tooa conservarse script, o puede disminuir el nivel de una secuencia de comandos de script persistentes tooan ad hoc.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3e5b5-153">Las acciones de script usadas durante la creación de un clúster se guardan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="3e5b5-154">Los scripts que dan error no se guardan, aunque indique específicamente que lo hagan.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="3e5b5-155">Puede aceptar **parámetros** que se usan para script de Hola durante la ejecución.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="3e5b5-156">Ejecutar con **privilegios en el nivel de raíz** en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="3e5b5-157">Puede utilizar a través de hello **portal de Azure**, **Azure PowerShell**, **CLI de Azure**, o **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="3e5b5-158">clúster de Hello mantiene un historial de todos los scripts que se ha ejecutado.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="3e5b5-159">historial de Hello es útil cuando necesita Id. de hello toofind de una secuencia de comandos para las operaciones de promoción o degradación.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-160">No hay ningún tooundo de manera automática Hola cambios realizados por una acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="3e5b5-161">O bien manualmente revertir cambios de Hola o proporcionar un script que se invierte.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="3e5b5-162">Acción de secuencia de comandos en el proceso de creación de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="3e5b5-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="3e5b5-163">Las acciones de script usadas durante la creación de un clúster son algo diferentes de las ejecutadas en un clúster existente:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="3e5b5-164">script de Hola es **automáticamente persistente**.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="3e5b5-165">A **error** en hello script puede provocar toofail de proceso de creación de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="3e5b5-166">Hello siguiente diagrama se muestra cuando se ejecuta la acción de secuencia de comandos durante el proceso de creación de hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="3e5b5-167">![Fases y personalización de clústeres de HDInsight durante la creación de clústeres][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="3e5b5-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="3e5b5-168">script de Hola se ejecuta mientras se está configurando HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="3e5b5-169">En esta fase, Hola script se ejecuta en paralelo en todos los Hola nodos especificados en el clúster de Hola y se ejecuta con privilegios de raíz en los nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="3e5b5-170">Como script de Hola se ejecuta con privilegios de nivel de raíz en nodos de clúster de hello, puede realizar operaciones, como detener e iniciar servicios, incluidos los servicios relacionados con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="3e5b5-171">Si se detiene servicios, debe asegurarse de que servicio de Ambari de Hola y otros servicios relacionados con Hadoop están activados y ejecutándose antes de que finaliza la ejecución de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="3e5b5-172">Estos servicios son necesarios toosuccessfully determinar Hola mantenimiento y el estado del clúster de hello mientras se está creando.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="3e5b5-173">Durante la creación del clúster, puede usar varias acciones de script a la vez.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="3e5b5-174">Estas secuencias de comandos se invocan en orden de hello en el que se especificaron.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-175">Las acciones de script se tienen que completar dentro de un periodo de 60 minutos o se superará el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="3e5b5-176">Durante el aprovisionamiento de clústeres, el script de Hola se ejecuta simultáneamente con otros procesos de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="3e5b5-177">La competición por los recursos, como el ancho de banda de red o de tiempo de CPU puede provocar Hola script tootake más toofinish que lo hace en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="3e5b5-178">Hola toominimize tiempo toma toorun Hola script, evitar las tareas como la descarga y la compilación de aplicaciones de origen.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="3e5b5-179">Precompilar las aplicaciones y almacenar binario de hello en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="3e5b5-180">Acción de script en un clúster en ejecución</span><span class="sxs-lookup"><span data-stu-id="3e5b5-180">Script action on a running cluster</span></span>

<span data-ttu-id="3e5b5-181">A diferencia de la secuencia de comandos de acciones que se usan durante la creación del clúster, un error en una secuencia de comandos se ejecutaban en un clúster ya se está ejecutando no provoca automáticamente Hola clúster toochange tooa error de estado.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="3e5b5-182">Una vez completada una secuencia de comandos, el clúster de hello debe devolver tooa "estado" en ejecución.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-183">Aunque el clúster de hello tiene un estado "running", hello errores de secuencia de comandos puede han interrumpido cosas.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="3e5b5-184">Por ejemplo, una secuencia de comandos podría eliminar archivos necesarios para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="3e5b5-185">Acciones de secuencias de comandos se ejecutan con privilegios de raíz, por lo que debe asegurarse de que comprende lo que hace una secuencia de comandos antes de aplicarla tooyour clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="3e5b5-186">Al aplicar un clúster de secuencia de comandos tooa, estado del clúster Hola cambia toofrom **ejecutando** demasiado**aceptado**, a continuación, **configuración de HDInsight**y finalmente, se vuelven demasiado**Ejecuta** para las secuencias de comandos correcta.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="3e5b5-187">estado del script de Hola se registra en el historial de acciones de script de Hola y puede usar esta información toodetermine si el script de Hola se realizó correctamente o no se pudo.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="3e5b5-188">Por ejemplo, hello `Get-AzureRmHDInsightScriptActionHistory` cmdlet de PowerShell puede ser utilizados tooview Hola estado de una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="3e5b5-189">Devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="3e5b5-190">Si ha cambiado la contraseña de usuario (admin) de clúster de Hola después de que se ha creado el clúster de hello, puede producir un error en la secuencia de comandos de acciones que se ejecutaron en este clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="3e5b5-191">Si tiene las acciones de script persistentes que nodos de trabajo de destino, estos scripts producirán errores al escalar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="3e5b5-192">Ejemplo de scripts de acción de script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-192">Example Script Action scripts</span></span>

<span data-ttu-id="3e5b5-193">Pueden utilizar secuencias de comandos de acción de secuencia de comandos mediante Hola siguientes utilidades:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="3e5b5-194">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3e5b5-194">Azure portal</span></span>
* <span data-ttu-id="3e5b5-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e5b5-195">Azure PowerShell</span></span>
* <span data-ttu-id="3e5b5-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3e5b5-196">Azure CLI</span></span>
* <span data-ttu-id="3e5b5-197">SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5b5-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="3e5b5-198">HDInsight proporciona hello tooinstall de secuencias de comandos de los componentes siguientes en clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="3e5b5-199">Nombre</span><span class="sxs-lookup"><span data-stu-id="3e5b5-199">Name</span></span> | <span data-ttu-id="3e5b5-200">Script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="3e5b5-201">**Agregar una cuenta de Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="3e5b5-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Vea [clúster de HDInsight de agregar almacenamiento adicional tooan](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="3e5b5-203">**Instalación de Hue**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-203">**Install Hue**</span></span> |<span data-ttu-id="3e5b5-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Consulte [Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md)</span><span class="sxs-lookup"><span data-stu-id="3e5b5-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="3e5b5-205">**Instalar Presto**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-205">**Install Presto**</span></span> |<span data-ttu-id="3e5b5-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Vea [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md) (Instalación y uso de Presto en clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="3e5b5-207">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-207">**Install Solr**</span></span> |<span data-ttu-id="3e5b5-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="3e5b5-209">**Instalación de Giraph**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-209">**Install Giraph**</span></span> |<span data-ttu-id="3e5b5-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="3e5b5-211">**Carga previa de las bibliotecas de Hive**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="3e5b5-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Vea [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md) (Adición de bibliotecas de Hive en clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="3e5b5-213">**Instalación o actualización de Mono**</span><span class="sxs-lookup"><span data-stu-id="3e5b5-213">**Install or update Mono**</span></span> | <span data-ttu-id="3e5b5-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="3e5b5-215">Vea [Instalación o actualización de Mono en HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="3e5b5-216">Uso de una acción de script durante la creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="3e5b5-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="3e5b5-217">En esta sección se proporciona ejemplos en hello distintas formas que puede usar acciones de script al crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="3e5b5-218">Usar una acción de secuencia de comandos durante la creación del clúster de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="3e5b5-219">Comience a crear un clúster, tal y como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="3e5b5-220">Deténgase cuando llegue a hello __resumen de clúster__ sección.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="3e5b5-221">De hello __resumen de clúster__ sección, seleccione hello __editar__ de vínculos para __configuración avanzada__.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Vínculo Configuración avanzada](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="3e5b5-223">De hello __configuración avanzada__ sección, seleccione __acciones de Script__.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="3e5b5-224">De hello __acciones de Script__ sección, seleccione __+ nuevo envío__</span><span class="sxs-lookup"><span data-stu-id="3e5b5-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Enviar una nueva acción de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="3e5b5-226">Hola de uso __seleccione una secuencia de comandos__ tooselect de entrada una secuencia de comandos elaborado previamente.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="3e5b5-227">toouse una secuencia de comandos personalizada, seleccione __personalizado__ y, a continuación, proporcionar hello __nombre__ y __Bash URI del script__ para la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Agregar un script de Hola select en forma de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="3e5b5-229">Hello en la tabla siguiente describe los elementos de hello en forma de hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="3e5b5-230">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3e5b5-230">Property</span></span> | <span data-ttu-id="3e5b5-231">Valor</span><span class="sxs-lookup"><span data-stu-id="3e5b5-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3e5b5-232">Seleccione un script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-232">Select a script</span></span> | <span data-ttu-id="3e5b5-233">toouse sus propias secuencias de comandos, seleccione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="3e5b5-234">En caso contrario, seleccione una de las secuencias de comandos de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="3e5b5-235">Nombre</span><span class="sxs-lookup"><span data-stu-id="3e5b5-235">Name</span></span> |<span data-ttu-id="3e5b5-236">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="3e5b5-237">URI de script de Bash</span><span class="sxs-lookup"><span data-stu-id="3e5b5-237">Bash script URI</span></span> |<span data-ttu-id="3e5b5-238">Especifique Hola URI toohello script que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="3e5b5-239">Principal, Trabajo o Zookeeper</span><span class="sxs-lookup"><span data-stu-id="3e5b5-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="3e5b5-240">Especifique los nodos de hello (**Head**, **trabajo**, o **ZooKeeper**) en qué personalización Hola se ejecuta el script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="3e5b5-241">parameters</span><span class="sxs-lookup"><span data-stu-id="3e5b5-241">Parameters</span></span> |<span data-ttu-id="3e5b5-242">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="3e5b5-243">Hola de uso __conservar esta acción de secuencia de comandos__ tooensure de entrada que hello secuencia de comandos se aplica durante las operaciones de ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="3e5b5-244">Seleccione __crear__ secuencia de comandos de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="3e5b5-245">A continuación, puede usar __+ Enviar nueva__ tooadd otra secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Varias acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="3e5b5-247">Cuando haya terminado de agregar secuencias de comandos, utilice hello __seleccione__ botón y, a continuación, Hola __siguiente__ botón tooreturn toohello __resumen de clúster__ sección.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="3e5b5-248">clúster de hello toocreate, seleccione __crear__ de hello __resumen de clúster__ selección.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="3e5b5-249">Use una acción de script de las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e5b5-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="3e5b5-250">ejemplos de Hello en esta sección muestra cómo toouse script acciones con plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="3e5b5-251">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3e5b5-251">Before you begin</span></span>

* <span data-ttu-id="3e5b5-252">Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight Powershell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3e5b5-253">Para obtener instrucciones sobre cómo toocreate plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3e5b5-254">Si todavía no ha utilizado Azure PowerShell con el Administrador de recursos, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="3e5b5-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="3e5b5-255">Creación de clústeres mediante acciones de script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="3e5b5-256">Copie Hola después de ubicación de tooa la plantilla en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="3e5b5-257">Esta plantilla instala Giraph en nodos headnodes y de trabajo Hola Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="3e5b5-258">También puede comprobar si la plantilla JSON de hello es válida.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="3e5b5-259">Pegue el contenido de la plantilla en [JSONLint](http://jsonlint.com/), herramienta de validación JSON en línea.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="3e5b5-260">Inicie PowerShell de Azure e inicie sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="3e5b5-261">Después de proporcionar sus credenciales, comando hello devuelve información sobre su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="3e5b5-262">Si tiene varias suscripciones, proporcione el identificador de suscripción de hello desea toouse para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="3e5b5-263">Puede usar `Get-AzureRmSubscription` tooget una lista de todas las suscripciones asociadas con su cuenta, que incluye el Id. de suscripción de Hola para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="3e5b5-264">Si no tiene un grupo de recursos existente, puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="3e5b5-265">Proporcione el nombre de hello del grupo de recursos de Hola y la ubicación que necesite para su solución.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="3e5b5-266">Se devuelve un resumen del nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-266">A summary of hello new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="3e5b5-267">una implementación para el grupo de recursos, ejecute hello toocreate **AzureRmResourceGroupDeployment New** comando y especifique los parámetros necesarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="3e5b5-268">parámetros de Hello incluyen hello datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="3e5b5-269">Un nombre para la implementación</span><span class="sxs-lookup"><span data-stu-id="3e5b5-269">A name for your deployment</span></span>
    * <span data-ttu-id="3e5b5-270">nombre de Hola de su grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3e5b5-270">hello name of your resource group</span></span>
    * <span data-ttu-id="3e5b5-271">ruta de acceso de Hola o plantilla de toohello de dirección URL que ha creado.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="3e5b5-272">Si la plantilla requiere parámetros, tiene que pasar también esos parámetros.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="3e5b5-273">En este caso, hello tooinstall de acción de script R en clúster de hello no requiere ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="3e5b5-274">Son valores tooprovide solicitadas para los parámetros de hello definidos en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="3e5b5-275">Cuando se ha implementado el grupo de recursos de hello, se muestra un resumen de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="3e5b5-276">Si se produce un error en la implementación, puede usar Hola siguiente cmdlets tooget información acerca de los errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="3e5b5-277">Uso de una acción de script durante la creación de un clúster desde Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e5b5-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="3e5b5-278">En esta sección, se utiliza hello [AzureRmHDInsightScriptAction agregar](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts mediante el uso de la acción de secuencia de comandos toocustomize un clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="3e5b5-279">Antes de continuar, asegúrese de que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="3e5b5-280">Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight PowerShell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="3e5b5-281">Hello secuencia de comandos siguiente se muestra cómo tooapply una acción de secuencia de comandos al crear un clúster con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="3e5b5-282">Puede tardar varios minutos antes de que se crea un clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="3e5b5-283">Usar una acción de secuencia de comandos durante la creación del clúster de HDInsight .NET SDK Hola</span><span class="sxs-lookup"><span data-stu-id="3e5b5-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="3e5b5-284">Hola HDInsight .NET SDK proporciona bibliotecas de cliente que resulta más fácil toowork con HDInsight desde una aplicación. NET.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="3e5b5-285">Para obtener un ejemplo de código, vea [basados en Linux crear clústeres de HDInsight utilizando Hola .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="3e5b5-286">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster</span><span class="sxs-lookup"><span data-stu-id="3e5b5-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="3e5b5-287">En esta sección, obtenga información acerca de cómo tooapply script tooa de acciones que se ejecuta el clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="3e5b5-288">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="3e5b5-289">De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="3e5b5-290">En información general del clúster de HDInsight de hello, seleccione hello **acciones de Script** icono.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Icono Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="3e5b5-292">También puede seleccionar **toda la configuración de** y, a continuación, seleccione **acciones de Script** de hello sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="3e5b5-293">Desde la parte superior de la sección de acciones de Script de Hola Hola seleccione **Enviar nueva**.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Agregar un tooa de secuencia de comandos ejecutando el clúster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="3e5b5-295">Hola de uso __seleccione una secuencia de comandos__ tooselect de entrada una secuencia de comandos elaborado previamente.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="3e5b5-296">toouse una secuencia de comandos personalizada, seleccione __personalizado__ y, a continuación, proporcionar hello __nombre__ y __Bash URI del script__ para la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Agregar un script de Hola select en forma de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="3e5b5-298">Hello en la tabla siguiente describe los elementos de hello en forma de hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="3e5b5-299">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3e5b5-299">Property</span></span> | <span data-ttu-id="3e5b5-300">Valor</span><span class="sxs-lookup"><span data-stu-id="3e5b5-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3e5b5-301">Seleccione un script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-301">Select a script</span></span> | <span data-ttu-id="3e5b5-302">toouse sus propias secuencias de comandos, seleccione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="3e5b5-303">En caso contrario, seleccione uno de los que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="3e5b5-304">Nombre</span><span class="sxs-lookup"><span data-stu-id="3e5b5-304">Name</span></span> |<span data-ttu-id="3e5b5-305">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="3e5b5-306">URI de script de Bash</span><span class="sxs-lookup"><span data-stu-id="3e5b5-306">Bash script URI</span></span> |<span data-ttu-id="3e5b5-307">Especifique Hola URI toohello script que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="3e5b5-308">Principal, Trabajo o Zookeeper</span><span class="sxs-lookup"><span data-stu-id="3e5b5-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="3e5b5-309">Especifique los nodos de hello (**Head**, **trabajo**, o **ZooKeeper**) en qué personalización Hola se ejecuta el script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="3e5b5-310">parameters</span><span class="sxs-lookup"><span data-stu-id="3e5b5-310">Parameters</span></span> |<span data-ttu-id="3e5b5-311">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="3e5b5-312">Hola de uso __conservar esta acción de secuencia de comandos__ secuencia de comandos de entrada toomake seguro Hola se aplica durante las operaciones de ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="3e5b5-313">Por último, utilice hello **crear** clúster toohello de botón tooapply hello secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="3e5b5-314">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster en PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="3e5b5-315">Antes de continuar, asegúrese de que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="3e5b5-316">Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight PowerShell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="3e5b5-317">Hello ejemplo siguiente se muestra cómo tooapply un clúster de ejecución de tooa de acción de secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="3e5b5-318">Una vez completada la operación de hello, recibirá información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="3e5b5-319">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="3e5b5-320">Antes de continuar, asegúrese de que ha instalado y configurado Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="3e5b5-321">Para obtener más información, consulte [Install hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="3e5b5-322">tooswitch tooAzure el modo de administrador de recursos, utilice Hola siguiente comando en la línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="3e5b5-323">Usar hello después tooauthenticate tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="3e5b5-324">Usar hello después comando tooapply un tooa de acción de secuencia de comandos ejecutando el clúster</span><span class="sxs-lookup"><span data-stu-id="3e5b5-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="3e5b5-325">Si omite los parámetros de este comando, se le solicitan.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="3e5b5-326">Si Hola script especifica con `-u` acepta parámetros, puede especificar mediante hello `-p` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="3e5b5-327">Los tipos de nodo válidos son `headnode`, `workernode` y `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="3e5b5-328">Si el script de Hola debe estar toomultiple aplicado los tipos de nodo, especificar tipos de hello separados por un ';'.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="3e5b5-329">Por ejemplo: `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="3e5b5-330">toopersist Hola script, agregue hello `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="3e5b5-331">También puede conservar el script de Hola más adelante mediante el uso de `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="3e5b5-332">Cuando se completa el trabajo de hello, recibirá toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="3e5b5-333">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster que usa la API de REST</span><span class="sxs-lookup"><span data-stu-id="3e5b5-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="3e5b5-334">Consulte [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx)(Ejecución de acciones de script en un clúster en ejecución).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="3e5b5-335">Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3e5b5-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="3e5b5-336">Para obtener un ejemplo del uso de clústeres de tooa de hello .NET SDK tooapply secuencias de comandos, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="3e5b5-337">Visualización del historial, promover y disminuir de nivel acciones de script</span><span class="sxs-lookup"><span data-stu-id="3e5b5-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="3e5b5-338">Uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="3e5b5-339">De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="3e5b5-340">En información general del clúster de HDInsight de hello, seleccione hello **acciones de Script** icono.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Icono Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="3e5b5-342">También puede seleccionar **toda la configuración de** y, a continuación, seleccione **acciones de Script** de hello sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="3e5b5-343">Un historial de las secuencias de comandos para este clúster se muestra en la sección de acciones de Script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="3e5b5-344">Esta información incluye una lista de scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="3e5b5-345">En la captura de pantalla de hello siguiente, puede ver que hello Solr ha sido script se ejecutó en este clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="3e5b5-346">captura de pantalla de Hello no muestra las secuencias de comandos persistentes.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Sección Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="3e5b5-348">Seleccionar una secuencia de comandos del historial de hello muestra la sección de propiedades de Hola para esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="3e5b5-349">Desde la parte superior de la pantalla de bienvenida Hola puede volver a ejecutar el script de Hola o promoverlo.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Propiedades de Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="3e5b5-351">También puede usar hello **...**  toohello derecha de las entradas en las acciones tooperform de sección de acciones de Script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Acciones de script... uso](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="3e5b5-353">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e5b5-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="3e5b5-354">Utilice la siguiente de Hola...</span><span class="sxs-lookup"><span data-stu-id="3e5b5-354">Use hello following...</span></span> | <span data-ttu-id="3e5b5-355">demasiado...</span><span class="sxs-lookup"><span data-stu-id="3e5b5-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="3e5b5-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="3e5b5-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="3e5b5-357">Recuperar información sobre acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="3e5b5-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="3e5b5-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="3e5b5-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="3e5b5-359">Recuperar un historial de clústeres de secuencia de comandos acciones aplicadas toohello, o los detalles de una secuencia de comandos específica</span><span class="sxs-lookup"><span data-stu-id="3e5b5-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="3e5b5-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="3e5b5-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="3e5b5-361">Promociona ad hoc tooa de acción de secuencia de comandos conserva la acción de secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="3e5b5-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="3e5b5-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="3e5b5-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="3e5b5-363">Degrada una acción de script persistentes acción tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="3e5b5-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-364">Usar `Remove-AzureRmHDInsightPersistedScriptAction` deshacer las acciones de hello realizadas por una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="3e5b5-365">Este cmdlet quita solo marca persistente Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="3e5b5-366">Hola siguiente secuencia de comandos de ejemplo muestra cómo utilizar Hola cmdlets toopromote, a continuación, disminuir de nivel de una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="3e5b5-367">Uso de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3e5b5-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="3e5b5-368">Utilice la siguiente de Hola...</span><span class="sxs-lookup"><span data-stu-id="3e5b5-368">Use hello following...</span></span> | <span data-ttu-id="3e5b5-369">demasiado...</span><span class="sxs-lookup"><span data-stu-id="3e5b5-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="3e5b5-370">Recuperar una lista de las acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="3e5b5-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="3e5b5-371">Recuperar información sobre una acción de script persistente específica</span><span class="sxs-lookup"><span data-stu-id="3e5b5-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="3e5b5-372">Recuperar un historial de clústeres de secuencia de comandos acciones aplicadas toohello</span><span class="sxs-lookup"><span data-stu-id="3e5b5-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="3e5b5-373">Recuperar información sobre una acción de script específica</span><span class="sxs-lookup"><span data-stu-id="3e5b5-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="3e5b5-374">Promociona ad hoc tooa de acción de secuencia de comandos conserva la acción de secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="3e5b5-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="3e5b5-375">Degrada una acción de script persistentes acción tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="3e5b5-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3e5b5-376">Usar `azure hdinsight script-action persisted delete` deshacer las acciones de hello realizadas por una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="3e5b5-377">Este cmdlet quita solo marca persistente Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="3e5b5-378">Uso de hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3e5b5-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="3e5b5-379">Para obtener un ejemplo del uso de historial de script de Hola .NET SDK tooretrieve desde un clúster, promocionar o degradar las secuencias de comandos, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="3e5b5-380">En este ejemplo también muestra cómo tooinstall una aplicación de HDInsight con Hola .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="3e5b5-381">Soporte técnico para el software de código abierto utilizado en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5b5-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="3e5b5-382">Hola servicio HDInsight de Azure de Microsoft usa un ecosistema de tecnologías de código abierto formado alrededor de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="3e5b5-383">Microsoft Azure proporciona un nivel general de soporte técnico para las tecnologías de código abierto.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="3e5b5-384">Para obtener más información, vea hello **compatibilidad con ámbito** sección de hello [sitio Web de preguntas más frecuentes de soporte técnico de Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="3e5b5-385">Hola servicio HDInsight proporciona un nivel adicional de compatibilidad para componentes integrados.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="3e5b5-386">Hay dos tipos de componentes de código abierto que están disponibles en hello servicio HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="3e5b5-387">**Componentes integrados** -estos componentes se instalan previamente en clústeres de HDInsight y proporcionan la funcionalidad básica de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="3e5b5-388">Por ejemplo, ResourceManager hilo, lenguaje de consulta de Hive hello (HiveQL) y biblioteca de Mahout Hola pertenecen toothis categoría.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="3e5b5-389">Una lista completa de componentes del clúster está disponible en [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="3e5b5-390">**Componentes personalizados** -, como un usuario del clúster hello, puede instalar o usar en la carga de trabajo cualquier componente disponible en la Comunidad de Hola o creado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="3e5b5-391">Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="3e5b5-392">Microsoft Support le ayuda a tooisolate y resolver los problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="3e5b5-393">Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="3e5b5-394">Soporte técnico de Microsoft puede ser capaz de tooresolve problema de Hola o pueden pedirle que tooengage los canales disponibles para las tecnologías de código abierto de Hola donde se encuentra la amplia experiencia para que la tecnología.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="3e5b5-395">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="3e5b5-396">Hola servicio HDInsight proporciona varias maneras de componentes personalizados de toouse.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="3e5b5-397">Hola al mismo nivel de compatibilidad se aplica, sin tener en cuenta cómo un componente se utiliza o instalado en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="3e5b5-398">Hello lista siguiente describen los usos más comunes de Hola que se puedan usar componentes personalizados en clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="3e5b5-399">Envío de trabajos - Hadoop u otros tipos de trabajos que se ejecutan o utilizan componentes personalizados pueden clúster toohello enviado.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="3e5b5-400">Personalización de clúster - durante la creación del clúster, puede especificar opciones de configuración adicionales y componentes personalizados que están instalados en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="3e5b5-401">Ejemplos: para componentes personalizados populares, Microsoft y otros elementos pueden proporcionar ejemplos de cómo se pueden usar estos componentes en clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="3e5b5-402">Estas muestras se proporcionan sin soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3e5b5-403">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3e5b5-403">Troubleshooting</span></span>

<span data-ttu-id="3e5b5-404">Puede usar Ambari web UI tooview información registrada por acciones de script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="3e5b5-405">Si se produce un error en el script de Hola durante la creación del clúster, también están disponibles en hello cuenta de almacenamiento predeterminado asociado con el clúster de Hola Hola registros.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="3e5b5-406">En esta sección se proporciona información sobre cómo tooretrieve Hola registros con ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="3e5b5-407">Uso de hello Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="3e5b5-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="3e5b5-408">En el explorador, navegue toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="3e5b5-409">Reemplace CLUSTERNAME por nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="3e5b5-410">Cuando se le solicite, escriba nombre de cuenta de administrador de hello (admin) y la contraseña para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="3e5b5-411">Puede que tenga credenciales de administrador de hello tooreenter en un formulario web Forms.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="3e5b5-412">En barra de hello al principio de Hola de página de hello, seleccione hello **ops** entrada.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="3e5b5-413">Se muestra una lista de las operaciones actuales y anteriores realizadas en clúster de Hola a través de Ambari.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Barra de interfaz de usuario web de Ambari con ops seleccionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="3e5b5-415">Buscar entradas de Hola que tienen **ejecutar\_customscriptaction** en hello **Operations** columna.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="3e5b5-416">Estas entradas se crean al ejecutar las acciones de Script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-416">These entries are created when hello Script Actions run.</span></span>

    ![Captura de pantalla de operaciones](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="3e5b5-418">Hola tooview STDOUT y resultado STDERR, seleccione hello run\customscriptaction entrada y explorar en profundidad los vínculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="3e5b5-419">Esta salida se genera cuando se ejecuta el script de Hola y pueden contener información útil.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="3e5b5-420">Registros de acceso de la cuenta de almacenamiento predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="3e5b5-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="3e5b5-421">Si se produce un error en la creación del clúster Hola debido a error de acción de secuencia de comandos de tooa, Hola registros pueden tener acceso de cuenta de almacenamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="3e5b5-422">Hello registros de almacenamiento están disponibles en `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Captura de pantalla de operaciones](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="3e5b5-424">En este directorio, registros de Hola se organizan por separado para el nodo principal, workernode y zookeeper nodos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="3e5b5-425">A continuación, se indican algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-425">Some examples are:</span></span>

    * <span data-ttu-id="3e5b5-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="3e5b5-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="3e5b5-427">**Nodo de trabajo** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="3e5b5-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="3e5b5-428">**Nodo Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="3e5b5-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="3e5b5-429">Todos los stdout y stderr de host correspondiente Hola está cargado toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="3e5b5-430">Hay un archivo **output-\*.txt** and **errors-\*.txt** para cada acción de script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="3e5b5-431">archivo de salida *.txt Hello contiene información sobre Hola URI del script de Hola que obtuvo ejecutar en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="3e5b5-432">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="3e5b5-433">Es posible crear un clúster de acción de secuencia de comandos repetidamente con hello mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="3e5b5-434">En este caso, puede distinguir los registros pertinentes Hola basados en el nombre de la carpeta de hello fecha.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="3e5b5-435">Por ejemplo, estructura de carpetas de Hola para un clúster (mycluster) creado en diferentes fechas aparece toohello similar siguiendo las entradas del registro:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="3e5b5-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="3e5b5-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="3e5b5-437">Si crea un clúster de acción de secuencia de comandos con hello mismo nombre en hello mismo día, puede usar archivos de registro correspondientes de hello prefijo único tooidentify Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="3e5b5-438">Si crea un clúster cerca de 12:00 A.M. (medianoche), es posible que los archivos de registro de hello abarcan dos días.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="3e5b5-439">En tales casos, verá dos carpetas de otra fecha para hello mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="3e5b5-440">Contenedor de carga registro archivos toohello predeterminado puede tardar hasta too5 minuto (s), especialmente para grandes clústeres.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="3e5b5-441">Por lo tanto, si desea que los registros de hello tooaccess, no debe inmediatamente Eliminar clúster Hola si se produce un error en una acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="3e5b5-442">Guardián Ambari</span><span class="sxs-lookup"><span data-stu-id="3e5b5-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="3e5b5-443">No se cambia la contraseña de Hola de hello Ambari guardián (hdinsightwatchdog) en el clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-444">Cambiar la contraseña para esta cuenta de hello interrumpe acciones nuevo script de Hola capacidad toorun en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="3e5b5-445">No se puede importar el nombre BlobService</span><span class="sxs-lookup"><span data-stu-id="3e5b5-445">Can't import name BlobService</span></span>

<span data-ttu-id="3e5b5-446">__Síntomas__: Hola error en la acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="3e5b5-447">Texto toohello similar siguiente error se muestra cuando ve operación hello en Ambari:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="3e5b5-448">__Causa__: este error se produce si actualiza el cliente de almacenamiento de Azure de Python de Hola que se incluye con clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="3e5b5-449">HDInsight espera el cliente de Azure Storage 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="3e5b5-450">__Resolución__: tooresolve este error, conecte manualmente el nodo de clúster de tooeach con `ssh` y use Hola siguiendo versión de cliente de almacenamiento correcta de comando tooreinstall hello:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="3e5b5-451">Para obtener información sobre la conexión de toohello de clúster mediante SSH, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e5b5-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="3e5b5-452">El historial no muestra los scripts usados durante la creación del clúster</span><span class="sxs-lookup"><span data-stu-id="3e5b5-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="3e5b5-453">Si el clúster se creó antes del 15 de marzo de 2016, puede que no vea una entrada en el historial de acciones de script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="3e5b5-454">Si cambia el tamaño de clúster de hello después del 15 de marzo de 2016, secuencias de comandos de hello mediante durante la creación del clúster aparecen en un historial cuando se aplican toonew nodos de clúster de hello como parte del programa Hola a cambiar el tamaño de operación.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="3e5b5-455">Hay dos excepciones:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-455">There are two exceptions:</span></span>

* <span data-ttu-id="3e5b5-456">Si el clúster se creó antes del 1 de septiembre de 2015.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="3e5b5-457">Esta es la fecha en que se presentaron las acciones de script.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="3e5b5-458">Cualquier clúster creado con anterioridad a esta fecha no ha podido usar acciones de script para su creación.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="3e5b5-459">Si usa varias acciones de Script durante la creación del clúster y lo usó Hola mismo nombre para varias secuencias de comandos, u Hola mismo nombre, mismo URI, pero distintos parámetros de varias secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="3e5b5-460">En estos casos, recibirá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="3e5b5-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="3e5b5-461">Se ejecutó ningún script nuevo las acciones pueden ser en este clúster debido tooconflicting nombres de secuencia de comandos en secuencias de comandos existentes.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="3e5b5-462">Los nombres de script proporcionados en la creación del clúster deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="3e5b5-463">Los scripts existentes se ejecutan con el cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="3e5b5-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e5b5-464">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e5b5-464">Next steps</span></span>

* [<span data-ttu-id="3e5b5-465">Desarrollo de la acción de script con HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5b5-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="3e5b5-466">Instalación y uso de Solr en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5b5-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="3e5b5-467">Instalación y uso de Giraph en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5b5-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="3e5b5-468">Agregar clúster de HDInsight de tooan de almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="3e5b5-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fases durante la creación del clúster"
