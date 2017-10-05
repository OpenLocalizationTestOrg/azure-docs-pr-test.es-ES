---
title: Desarrollo de acciones de script con HDInsight basado en Linux (Azure) | Microsoft Docs
description: "Obtenga información sobre cómo usar scripts de Bash para personalizar clústeres de HDInsight basado en Linux. La característica de acción de script de HDInsight le permite ejecutar scripts durante o después de la creación del clúster. Los scripts se pueden usar para cambiar la configuración de clúster o instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="560a1-105">Desarrollo de la acción de script con HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-105">Script action development with HDInsight</span></span>

<span data-ttu-id="560a1-106">Obtenga información sobre cómo personalizar su clúster de HDInsight mediante scripts de Bash.</span><span class="sxs-lookup"><span data-stu-id="560a1-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="560a1-107">Las acciones de script son una forma de personalizar HDInsight durante la creación del clúster o después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="560a1-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="560a1-108">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="560a1-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="560a1-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="560a1-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="560a1-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="560a1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="560a1-111">¿Qué son las acciones de script?</span><span class="sxs-lookup"><span data-stu-id="560a1-111">What are script actions</span></span>

<span data-ttu-id="560a1-112">Las acciones de script son scripts de Bash que Azure ejecuta en los nodos del clúster para realizar cambios de configuración o instalar software.</span><span class="sxs-lookup"><span data-stu-id="560a1-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="560a1-113">Una acción de script se ejecuta como raíz y proporciona derechos de acceso completo a los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="560a1-114">Se puede aplicar una acción de script a través de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="560a1-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="560a1-115">Use este método para aplicar un script...</span><span class="sxs-lookup"><span data-stu-id="560a1-115">Use this method to apply a script...</span></span> | <span data-ttu-id="560a1-116">Durante la creación del clúster...</span><span class="sxs-lookup"><span data-stu-id="560a1-116">During cluster creation...</span></span> | <span data-ttu-id="560a1-117">En un clúster en ejecución...</span><span class="sxs-lookup"><span data-stu-id="560a1-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="560a1-118">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="560a1-118">Azure portal</span></span> |<span data-ttu-id="560a1-119">✓ </span><span class="sxs-lookup"><span data-stu-id="560a1-119">✓</span></span> |<span data-ttu-id="560a1-120">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-120">✓</span></span> |
| <span data-ttu-id="560a1-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="560a1-121">Azure PowerShell</span></span> |<span data-ttu-id="560a1-122">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-122">✓</span></span> |<span data-ttu-id="560a1-123">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-123">✓</span></span> |
| <span data-ttu-id="560a1-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="560a1-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="560a1-125">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-125">✓</span></span> |
| <span data-ttu-id="560a1-126">SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="560a1-127">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-127">✓</span></span> |<span data-ttu-id="560a1-128">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-128">✓</span></span> |
| <span data-ttu-id="560a1-129">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="560a1-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="560a1-130">✓</span><span class="sxs-lookup"><span data-stu-id="560a1-130">✓</span></span> |&nbsp; |

<span data-ttu-id="560a1-131">Para más información sobre el uso de estos métodos para aplicar acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="560a1-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="560a1-132"><a name="bestPracticeScripting"></a>Prácticas recomendadas para el desarrollo de scripts</span><span class="sxs-lookup"><span data-stu-id="560a1-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="560a1-133">Al desarrollar un script personalizado para un clúster de HDInsight, hay varios procedimientos recomendados que hay que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="560a1-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="560a1-134">Concentrarse en la versión de Hadoop</span><span class="sxs-lookup"><span data-stu-id="560a1-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="560a1-135">Concentrarse en el sistema operativo</span><span class="sxs-lookup"><span data-stu-id="560a1-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="560a1-136">Proporcionar vínculos estables a los recursos de script</span><span class="sxs-lookup"><span data-stu-id="560a1-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="560a1-137">Usar recursos compilados previamente</span><span class="sxs-lookup"><span data-stu-id="560a1-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="560a1-138">Asegurarse de que el script de personalización del clúster es idempotente</span><span class="sxs-lookup"><span data-stu-id="560a1-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="560a1-139">Asegurar una alta disponibilidad de la arquitectura de clúster</span><span class="sxs-lookup"><span data-stu-id="560a1-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="560a1-140">Configurar los componentes personalizados para usar el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="560a1-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="560a1-141">Escribir información en STDOUT y STDERR</span><span class="sxs-lookup"><span data-stu-id="560a1-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="560a1-142">Guardar los archivos como ASCII con el fin de línea LF</span><span class="sxs-lookup"><span data-stu-id="560a1-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="560a1-143">Utilizar la lógica de reintento para recuperarse de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="560a1-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="560a1-144">Las acciones de script se tienen que completar dentro de un período de sesenta minutos o se producirá un error en el proceso.</span><span class="sxs-lookup"><span data-stu-id="560a1-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="560a1-145">Durante el aprovisionamiento del nodo, el script se ejecuta simultáneamente con otros procesos de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="560a1-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="560a1-146">La competición por los recursos, como el ancho de banda de red o el tiempo de CPU puede ocasionar que el script tarde más en terminar que en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="560a1-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="560a1-147"><a name="bPS1"></a>Concentrarse en la versión de Hadoop</span><span class="sxs-lookup"><span data-stu-id="560a1-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="560a1-148">Las distintas versiones de HDInsight tienen distintas versiones de componentes y servicios de Hadoop instalados.</span><span class="sxs-lookup"><span data-stu-id="560a1-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="560a1-149">Si su script espera una versión específica de un servicio o componente, debe usar solamente el script con la versión de HDInsight que incluye los componentes necesarios.</span><span class="sxs-lookup"><span data-stu-id="560a1-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="560a1-150">Puede encontrar información sobre las versiones de los componentes incluidos con HDInsight mediante el documento [Versiones de HDInsight y componentes](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="560a1-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="560a1-151"><a name="bps10"></a> Concentrarse en el sistema operativo</span><span class="sxs-lookup"><span data-stu-id="560a1-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="560a1-152">HDInsight basado en Linux utiliza como cimientos la distribución de Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="560a1-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="560a1-153">Las distintas versiones de HDInsight se basan en diferentes versiones de Ubuntu, que podrían cambiar el funcionamiento del script.</span><span class="sxs-lookup"><span data-stu-id="560a1-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="560a1-154">Por ejemplo, HDInsight 3.4 y versiones anteriores se basan en versiones de Ubuntu que emplean Upstart.</span><span class="sxs-lookup"><span data-stu-id="560a1-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="560a1-155">La versión 3.5 se basa en Ubuntu 16.04, que utiliza Systemd.</span><span class="sxs-lookup"><span data-stu-id="560a1-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="560a1-156">Systemd y Upstart se basan en comandos diferentes, por lo que debe escribirse el script para usar los dos.</span><span class="sxs-lookup"><span data-stu-id="560a1-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="560a1-157">Otra diferencia importante entre HDInsight 3.4 y 3.5 es que `JAVA_HOME` ahora apunta a Java 8.</span><span class="sxs-lookup"><span data-stu-id="560a1-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="560a1-158">Puede comprobar la versión del sistema operativo mediante `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="560a1-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="560a1-159">El código siguiente demuestra cómo determinar si el script se ejecuta en Ubuntu 14 o 16:</span><span class="sxs-lookup"><span data-stu-id="560a1-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="560a1-160">Puede encontrar el script completo que contiene estos fragmentos de código en https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="560a1-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="560a1-161">Para la versión de Ubuntu que usa HDInsight, lea el documento sobre la [versión del componente de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="560a1-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="560a1-162">Para entender las diferencias entre Systemd y Upstart, consulte el artículo sobre [Systemd para usuarios de Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="560a1-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="560a1-163"><a name="bPS2"></a>Proporcionar vínculos estables a los recursos de script</span><span class="sxs-lookup"><span data-stu-id="560a1-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="560a1-164">El script y los recursos asociados deben permanecer disponibles durante la vigencia del clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="560a1-165">Estos recursos son necesarios si se agregan nodos nuevos al clúster durante operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="560a1-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="560a1-166">La práctica recomendada es descargar y archivar todo el contenido de una cuenta de Azure Storage en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="560a1-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="560a1-167">La cuenta de almacenamiento usada tiene que ser la cuenta de almacenamiento predeterminada del clúster o un contenedor público de solo lectura en cualquier otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="560a1-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="560a1-168">Por ejemplo, los ejemplos proporcionados por Microsoft se almacenan en la cuenta de almacenamiento [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="560a1-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="560a1-169">Este es un contenedor público de solo lectura mantenido por el equipo de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="560a1-170"><a name="bPS4"></a>Usar recursos compilados previamente</span><span class="sxs-lookup"><span data-stu-id="560a1-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="560a1-171">Para minimizar el tiempo necesario para ejecutar el script, evite las operaciones que compilan recursos a partir del código fuente.</span><span class="sxs-lookup"><span data-stu-id="560a1-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="560a1-172">Por ejemplo, compile previamente los recursos y almacénelos en un blob de cuenta de Azure Storage en el mismo centro de datos en que está HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="560a1-173"><a name="bPS3"></a>Asegurarse de que el script de personalización del clúster es idempotente</span><span class="sxs-lookup"><span data-stu-id="560a1-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="560a1-174">Los scripts deben ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="560a1-174">Scripts must be idempotent.</span></span> <span data-ttu-id="560a1-175">Si el script se ejecuta varias veces, debe devolver el clúster al mismo estado cada vez.</span><span class="sxs-lookup"><span data-stu-id="560a1-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="560a1-176">Por ejemplo, un script que modifique los archivos de configuración no debería agregar entradas duplicadas si se ejecuta varias veces.</span><span class="sxs-lookup"><span data-stu-id="560a1-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="560a1-177"><a name="bPS5"></a>Asegurar una alta disponibilidad de la arquitectura de clúster</span><span class="sxs-lookup"><span data-stu-id="560a1-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="560a1-178">Los clústeres de HDInsight basados en Linux proporcionan dos nodos principales que están activos dentro del clúster, y las acciones de script se ejecutan en ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="560a1-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="560a1-179">Si los componentes instalados esperan únicamente un nodo principal, no instale los componentes en ambos nodos principales.</span><span class="sxs-lookup"><span data-stu-id="560a1-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="560a1-180">Los servicios proporcionados como parte de HDInsight están diseñados para conmutar por error entre los dos nodos principales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="560a1-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="560a1-181">Esta funcionalidad no se extiende a componentes personalizados instalados mediante acciones de script.</span><span class="sxs-lookup"><span data-stu-id="560a1-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="560a1-182">Si necesita una disponibilidad elevada en componentes personalizados, deberá implementar su propio mecanismo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="560a1-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="560a1-183"><a name="bPS6"></a>Configurar los componentes personalizados para usar el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="560a1-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="560a1-184">Los componentes que instaló en el clúster podrían tener una configuración predeterminada que usa el almacenamiento Sistema de archivos distribuido de Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="560a1-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="560a1-185">HDInsight usa Azure Storage o Data Lake Store como almacén predeterminado.</span><span class="sxs-lookup"><span data-stu-id="560a1-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="560a1-186">Ambas soluciones proporcionan un sistema de archivos compatible con HDFS que conserva los datos incluso si se elimina el clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="560a1-187">Podría tener que configurar los componentes instalados para que usen WASB o ADL en lugar de HDFS.</span><span class="sxs-lookup"><span data-stu-id="560a1-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="560a1-188">En la mayoría de las operaciones, no es necesario especificar el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="560a1-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="560a1-189">Por ejemplo, lo siguiente copia el archivo giraph-examples.jar del sistema de archivos local a un almacenamiento de clúster:</span><span class="sxs-lookup"><span data-stu-id="560a1-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="560a1-190">En este ejemplo, el comando `hdfs` usa de forma transparente el almacenamiento de clúster predeterminado.</span><span class="sxs-lookup"><span data-stu-id="560a1-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="560a1-191">En algunas operaciones debe especificar el URI.</span><span class="sxs-lookup"><span data-stu-id="560a1-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="560a1-192">Por ejemplo, `adl:///example/jars` para Data Lake Store o `wasb:///example/jars` para Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="560a1-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="560a1-193"><a name="bPS7"></a>Escribir información en STDOUT y STDERR</span><span class="sxs-lookup"><span data-stu-id="560a1-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="560a1-194">HDInsight registra el resultado del script que se escribe en STDOUT y STDERR.</span><span class="sxs-lookup"><span data-stu-id="560a1-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="560a1-195">Puede ver esta información mediante la interfaz de usuario de Ambari web.</span><span class="sxs-lookup"><span data-stu-id="560a1-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="560a1-196">Ambari solo estará disponible si el clúster se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="560a1-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="560a1-197">Si usa una acción de script durante la creación del clúster y se produce un error, consulte la sección de solución de problemas [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para conocer otras formas de acceder a la información registrada.</span><span class="sxs-lookup"><span data-stu-id="560a1-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="560a1-198">La mayoría de las utilidades y paquetes de instalación escriben información en STDOUT y STDERR, pero puede que desee agregar un registro adicional.</span><span class="sxs-lookup"><span data-stu-id="560a1-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="560a1-199">Para enviar texto a STDOUT, use `echo`.</span><span class="sxs-lookup"><span data-stu-id="560a1-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="560a1-200">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="560a1-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="560a1-201">De forma predeterminada, `echo` enviará la cadena a STDOUT.</span><span class="sxs-lookup"><span data-stu-id="560a1-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="560a1-202">Para dirigirla a STDERR, agregue `>&2` antes de `echo`.</span><span class="sxs-lookup"><span data-stu-id="560a1-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="560a1-203">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="560a1-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="560a1-204">Esto redirige la información escrita en STDOUT a STDERR (2).</span><span class="sxs-lookup"><span data-stu-id="560a1-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="560a1-205">Para obtener más información sobre la redirección de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="560a1-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="560a1-206">Para obtener más información sobre la visualización de información registrada por las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="560a1-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="560a1-207"><a name="bps8"></a> Guardar los archivos como ASCII con el fin de línea LF</span><span class="sxs-lookup"><span data-stu-id="560a1-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="560a1-208">Los scripts de Bash deben almacenarse con formato ASCII, con líneas terminadas con LF.</span><span class="sxs-lookup"><span data-stu-id="560a1-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="560a1-209">Los archivos que se almacenan como UTF-8 o usan CRLF como el final de línea pueden generar el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="560a1-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="560a1-210"><a name="bps9"></a> Utilizar la lógica de reintento para recuperarse de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="560a1-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="560a1-211">Al descargar archivos, instalar paquetes mediante apt-get o realizar otras acciones que transmiten datos por Internet, se puede producir un error en la acción debido a errores de red transitorios.</span><span class="sxs-lookup"><span data-stu-id="560a1-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="560a1-212">Por ejemplo, puede suceder que el recurso remoto con el que se está comunicando esté a punto de conmutar por error a un nodo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="560a1-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="560a1-213">Para que el script sea resistente a los errores transitorios, puede implementar la lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="560a1-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="560a1-214">La siguiente función muestra cómo implementar la lógica de reintentos.</span><span class="sxs-lookup"><span data-stu-id="560a1-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="560a1-215">Vuelve a intentar la operación tres veces antes de desistir.</span><span class="sxs-lookup"><span data-stu-id="560a1-215">It retries the operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="560a1-216">En los ejemplos siguientes se muestra cómo utilizar esta función.</span><span class="sxs-lookup"><span data-stu-id="560a1-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="560a1-217"><a name="helpermethods"></a>Métodos auxiliares para scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="560a1-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="560a1-218">Los métodos auxiliares de la acción de script son utilidades que puede usar al escribir scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="560a1-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="560a1-219">Estos métodos se encuentran en el script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="560a1-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="560a1-220">Para descargar y usarlos como parte de su script:</span><span class="sxs-lookup"><span data-stu-id="560a1-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="560a1-221">Las siguientes aplicaciones auxiliares estén disponibles para su uso en el script:</span><span class="sxs-lookup"><span data-stu-id="560a1-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="560a1-222">Uso de la aplicación auxiliar</span><span class="sxs-lookup"><span data-stu-id="560a1-222">Helper usage</span></span> | <span data-ttu-id="560a1-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="560a1-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="560a1-224">Descarga un archivo del URI de origen en la ruta de acceso de archivo especificada.</span><span class="sxs-lookup"><span data-stu-id="560a1-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="560a1-225">De forma predeterminada, no sobrescribirá un archivo existente.</span><span class="sxs-lookup"><span data-stu-id="560a1-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="560a1-226">Extrae un archivo tar (mediante `-xf`) en el directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="560a1-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="560a1-227">Si se ejecutaba en un nodo principal del clúster, devuelve 1. En caso contrario, devuelve 0.</span><span class="sxs-lookup"><span data-stu-id="560a1-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="560a1-228">Si el nodo actual es un nodo de datos (trabajo), devuelve 1. En caso contrario, devuelve 0.</span><span class="sxs-lookup"><span data-stu-id="560a1-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="560a1-229">Si el nodo actual es el primer nodo (trabajo) de datos (llamado workernode0), devuelve 1. En caso contrario, devuelve 0.</span><span class="sxs-lookup"><span data-stu-id="560a1-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="560a1-230">Devuelve el nombre de dominio completo de los nodos principales del clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="560a1-231">Los nombres están delimitados por comas.</span><span class="sxs-lookup"><span data-stu-id="560a1-231">Names are comma delimited.</span></span> <span data-ttu-id="560a1-232">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="560a1-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="560a1-233">Obtiene el nombre de dominio completo del nodo principal primario.</span><span class="sxs-lookup"><span data-stu-id="560a1-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="560a1-234">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="560a1-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="560a1-235">Obtiene el nombre de dominio completo del nodo principal secundario.</span><span class="sxs-lookup"><span data-stu-id="560a1-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="560a1-236">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="560a1-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="560a1-237">Obtiene el sufijo numérico del nodo principal primario.</span><span class="sxs-lookup"><span data-stu-id="560a1-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="560a1-238">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="560a1-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="560a1-239">Obtiene el sufijo numérico del nodo principal secundario.</span><span class="sxs-lookup"><span data-stu-id="560a1-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="560a1-240">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="560a1-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="560a1-241"><a name="commonusage"></a>Patrones de uso común</span><span class="sxs-lookup"><span data-stu-id="560a1-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="560a1-242">Esta sección proporciona instrucciones sobre cómo implementar algunos de los patrones de uso común que podría encontrar mientras escribe su propio script personalizado.</span><span class="sxs-lookup"><span data-stu-id="560a1-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="560a1-243">Paso de parámetros a un script</span><span class="sxs-lookup"><span data-stu-id="560a1-243">Passing parameters to a script</span></span>

<span data-ttu-id="560a1-244">En algunos casos, un script puede requerir parámetros.</span><span class="sxs-lookup"><span data-stu-id="560a1-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="560a1-245">Por ejemplo, puede que necesite la contraseña de administrador para el clúster si utiliza la API REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="560a1-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="560a1-246">Los parámetros que se pasan al script se conocen como *parámetros posicionales*, y se asignan a `$1` para el primer parámetro, `$2` para el segundo y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="560a1-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="560a1-247">`$0` contiene el nombre del script.</span><span class="sxs-lookup"><span data-stu-id="560a1-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="560a1-248">Los valores se pasan al script como parámetros deben estar rodeados de comillas simples (').</span><span class="sxs-lookup"><span data-stu-id="560a1-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="560a1-249">De este modo, se garantiza que el valor pasado se trate literalmente.</span><span class="sxs-lookup"><span data-stu-id="560a1-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="560a1-250">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="560a1-250">Setting environment variables</span></span>

<span data-ttu-id="560a1-251">La instrucción siguiente establece una variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="560a1-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="560a1-252">Donde VARIABLENAME es el nombre de la variable.</span><span class="sxs-lookup"><span data-stu-id="560a1-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="560a1-253">Para obtener acceso a la variable, use `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="560a1-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="560a1-254">Por ejemplo, para asignar un valor proporcionado por un parámetro posicional como una variable de entorno denominada PASSWORD, use esta instrucción:</span><span class="sxs-lookup"><span data-stu-id="560a1-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="560a1-255">Para el acceso posterior a la información puede usar `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="560a1-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="560a1-256">Las variables de entorno establecidas dentro del script solo existen en el ámbito del script.</span><span class="sxs-lookup"><span data-stu-id="560a1-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="560a1-257">En algunos casos, puede que necesite agregar variables de entorno de todo el sistema que se conserven una vez finalizado el script.</span><span class="sxs-lookup"><span data-stu-id="560a1-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="560a1-258">Para agregar variables de entorno de todo el sistema, agregue la variable a `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="560a1-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="560a1-259">Por ejemplo, la instrucción siguiente agrega `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="560a1-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="560a1-260">Acceso a ubicaciones donde se almacenan los scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="560a1-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="560a1-261">Los scripts usados para personalizar un clúster deben almacenarse en una de las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="560a1-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="560a1-262">Una __cuenta de Azure Storage__ asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="560a1-263">Una __cuenta de almacenamiento adicional__ asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="560a1-264">Un __URI legible públicamente__.</span><span class="sxs-lookup"><span data-stu-id="560a1-264">A __publicly readable URI__.</span></span> <span data-ttu-id="560a1-265">Por ejemplo, una dirección URL a los datos almacenados en OneDrive, Dropbox u otro servicio de hospedaje de archivo.</span><span class="sxs-lookup"><span data-stu-id="560a1-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="560a1-266">Una __cuenta de Azure Data Lake Store__ que esté asociada con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="560a1-267">Para más información sobre el uso de Azure Data Lake Store con HDInsight, consulte [Creación de un clúster de HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="560a1-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="560a1-268">La entidad de servicio que HDInsight usa para acceder a Data Lake Store debe tener acceso de lectura al script.</span><span class="sxs-lookup"><span data-stu-id="560a1-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="560a1-269">Los recursos utilizados por el script también deben estar disponibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="560a1-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="560a1-270">Almacenar los archivos en una cuenta de Azure Storage o Azure Data Lake Store proporciona un acceso rápido, ya que ambas soluciones están dentro de la red de Azure.</span><span class="sxs-lookup"><span data-stu-id="560a1-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="560a1-271">El formato de URI que se use para hacer referencia al script difiere en función del servicio que se utilice.</span><span class="sxs-lookup"><span data-stu-id="560a1-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="560a1-272">Para las cuentas de almacenamiento asociadas con el clúster de HDInsight, use `wasb://` o `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="560a1-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="560a1-273">Para los URI legibles públicamente, use `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="560a1-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="560a1-274">Para Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="560a1-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="560a1-275">Comprobación de la versión del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="560a1-275">Checking the operating system version</span></span>

<span data-ttu-id="560a1-276">Las distintas versiones de HDInsight se basan en versiones específicas de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="560a1-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="560a1-277">Puede haber diferencias entre las versiones del sistema operativo que debe comprobar en el script.</span><span class="sxs-lookup"><span data-stu-id="560a1-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="560a1-278">Por ejemplo, debe instalar un archivo binario que esté asociado a la versión de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="560a1-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="560a1-279">Para comprobar la versión del sistema operativo, use `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="560a1-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="560a1-280">Por ejemplo, el script siguiente muestra cómo hacer referencia a un archivo tar específico en función de la versión del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="560a1-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="560a1-281"><a name="deployScript"></a>Lista de comprobación para implementar una acción de script</span><span class="sxs-lookup"><span data-stu-id="560a1-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="560a1-282">Estos son los pasos que se llevaron a cabo al prepararse para implementar estos scripts:</span><span class="sxs-lookup"><span data-stu-id="560a1-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="560a1-283">Coloque los archivos que contengan los scripts personalizados en un lugar que sea accesible por los nodos del clúster durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="560a1-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="560a1-284">Por ejemplo, el almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="560a1-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="560a1-285">Los archivos también se pueden almacenar en servicios de hospedaje visibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="560a1-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="560a1-286">Compruebe que el script sea idempotente.</span><span class="sxs-lookup"><span data-stu-id="560a1-286">Verify that the script is impotent.</span></span> <span data-ttu-id="560a1-287">De ese modo, se permite el script que se ejecute varias veces en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="560a1-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="560a1-288">Use un directorio de archivo temporal /tmp para conservar los archivos descargados que usan los scripts y, a continuación, y realice una limpieza una vez que se ejecuten los scripts.</span><span class="sxs-lookup"><span data-stu-id="560a1-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="560a1-289">Si se cambia la configuración del nivel de sistema operativo o los archivos de configuración de servicio de Hadoop, debería reiniciar los servicios de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="560a1-290"><a name="runScriptAction"></a>Ejecución de una acción de script</span><span class="sxs-lookup"><span data-stu-id="560a1-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="560a1-291">Puede usar acciones de script para personalizar los clústeres de HDInsight con los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="560a1-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="560a1-292">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="560a1-292">Azure portal</span></span>
* <span data-ttu-id="560a1-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="560a1-293">Azure PowerShell</span></span>
* <span data-ttu-id="560a1-294">Plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="560a1-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="560a1-295">El SDK de .NET para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="560a1-296">Para obtener más información sobre el uso de cada método, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="560a1-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="560a1-297"><a name="sampleScripts"></a>Ejemplos de scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="560a1-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="560a1-298">Microsoft proporciona scripts de ejemplo para instalar los componentes en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="560a1-299">Consulte los vínculos siguientes para ver más acciones de script de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="560a1-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="560a1-300">Instalación y uso de Hue en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="560a1-301">Instalación y uso de Solr en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="560a1-302">Instalación y uso de Giraph en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="560a1-303">Instalación o actualización de Mono en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a1-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="560a1-304">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="560a1-304">Troubleshooting</span></span>

<span data-ttu-id="560a1-305">Estos son errores que pueden producirse al usar los scripts desarrollados:</span><span class="sxs-lookup"><span data-stu-id="560a1-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="560a1-306">**Error**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="560a1-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="560a1-307">A veces seguido de `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="560a1-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="560a1-308">*Causa*: este error se produce si las líneas en un script terminan con CRLF.</span><span class="sxs-lookup"><span data-stu-id="560a1-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="560a1-309">Los sistemas UNIX esperan solo LF como final de la línea.</span><span class="sxs-lookup"><span data-stu-id="560a1-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="560a1-310">Este problema suele producirse cuando se crea el script en un entorno Windows, ya que CRLF es una línea común final para muchos editores de texto en Windows.</span><span class="sxs-lookup"><span data-stu-id="560a1-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="560a1-311">*Resolución*: si es una opción en el editor de texto, seleccione formato UNIX o LF para el final de la línea.</span><span class="sxs-lookup"><span data-stu-id="560a1-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="560a1-312">También puede usar los siguientes comandos en un sistema UNIX para cambiar un CRLF por un LF:</span><span class="sxs-lookup"><span data-stu-id="560a1-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="560a1-313">Los siguientes comandos son aproximadamente equivalentes en que deben cambiar los finales de línea CRLF a LF.</span><span class="sxs-lookup"><span data-stu-id="560a1-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="560a1-314">Seleccione uno en función de las utilidades disponibles en el sistema.</span><span class="sxs-lookup"><span data-stu-id="560a1-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="560a1-315">Comando</span><span class="sxs-lookup"><span data-stu-id="560a1-315">Command</span></span> | <span data-ttu-id="560a1-316">Notas</span><span class="sxs-lookup"><span data-stu-id="560a1-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="560a1-317">Se realizará una copia de seguridad del archivo original con una extensión .BAK</span><span class="sxs-lookup"><span data-stu-id="560a1-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="560a1-318">OUTFILE contendrá una versión con finales de línea solo LF</span><span class="sxs-lookup"><span data-stu-id="560a1-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="560a1-319">Modifica el archivo directamente</span><span class="sxs-lookup"><span data-stu-id="560a1-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="560a1-320">OUTFILE contendrá una versión con finales de línea solo LF.</span><span class="sxs-lookup"><span data-stu-id="560a1-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="560a1-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="560a1-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="560a1-322">*Causa*: este error se produce cuando el script se guarda como UTF-8 con una marca de orden de bytes (BOM).</span><span class="sxs-lookup"><span data-stu-id="560a1-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="560a1-323">*Resolución*: guarde el archivo como ASCII o UTF-8 sin una marca BOM.</span><span class="sxs-lookup"><span data-stu-id="560a1-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="560a1-324">También puede usar el siguiente comando en un sistema Linux o UNIX para crear un archivo sin marca BOM:</span><span class="sxs-lookup"><span data-stu-id="560a1-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="560a1-325">Reemplace `INFILE` con el archivo que contiene la marca BOM.</span><span class="sxs-lookup"><span data-stu-id="560a1-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="560a1-326">`OUTFILE` debe ser un nombre de archivo nuevo, que contendrá el script sin la marca BOM.</span><span class="sxs-lookup"><span data-stu-id="560a1-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="560a1-327"><a name="seeAlso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="560a1-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="560a1-328">Obtenga información sobre cómo [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="560a1-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="560a1-329">Use la [referencia del SDK de .NET de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) para obtener más información sobre la creación de aplicaciones .NET que administran HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="560a1-330">Use la [API de REST de HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) para obtener información sobre cómo usar REST para realizar acciones de administración en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a1-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
