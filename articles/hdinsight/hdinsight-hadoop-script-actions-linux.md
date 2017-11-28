---
title: "desarrollo de la acción de aaaScript con HDInsight basados en Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Bash scripts toocustomize clústeres de HDInsight basados en Linux. característica de acción de secuencia de comandos de Hola de HDInsight permite las secuencias de comandos de toorun durante o después de la creación del clúster. Las secuencias de comandos pueden ser toochange usa valores de configuración de clúster o instalar software adicional."
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
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="61bd8-105">Desarrollo de la acción de script con HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-105">Script action development with HDInsight</span></span>

<span data-ttu-id="61bd8-106">Obtenga información acerca de cómo su clúster de HDInsight con Bash toocustomize secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="61bd8-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="61bd8-107">Las acciones de script son un toocustomize de manera HDInsight durante o después de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="61bd8-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61bd8-108">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="61bd8-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="61bd8-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="61bd8-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="61bd8-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="61bd8-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="61bd8-111">¿Qué son las acciones de script?</span><span class="sxs-lookup"><span data-stu-id="61bd8-111">What are script actions</span></span>

<span data-ttu-id="61bd8-112">Acciones de script son scripts de Bash que Azure se ejecuta en los cambios de configuración de toomake de nodos de clúster de Hola o instalarán software.</span><span class="sxs-lookup"><span data-stu-id="61bd8-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="61bd8-113">Una acción de secuencia de comandos se ejecuta como raíz y proporciona acceso completo de nodos de clúster de derechos toohello.</span><span class="sxs-lookup"><span data-stu-id="61bd8-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="61bd8-114">Acciones de script se pueden aplicar mediante Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="61bd8-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="61bd8-115">Utilice este tooapply método una secuencia de comandos...</span><span class="sxs-lookup"><span data-stu-id="61bd8-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="61bd8-116">Durante la creación del clúster...</span><span class="sxs-lookup"><span data-stu-id="61bd8-116">During cluster creation...</span></span> | <span data-ttu-id="61bd8-117">En un clúster en ejecución...</span><span class="sxs-lookup"><span data-stu-id="61bd8-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="61bd8-118">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="61bd8-118">Azure portal</span></span> |<span data-ttu-id="61bd8-119">✓ </span><span class="sxs-lookup"><span data-stu-id="61bd8-119">✓</span></span> |<span data-ttu-id="61bd8-120">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-120">✓</span></span> |
| <span data-ttu-id="61bd8-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61bd8-121">Azure PowerShell</span></span> |<span data-ttu-id="61bd8-122">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-122">✓</span></span> |<span data-ttu-id="61bd8-123">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-123">✓</span></span> |
| <span data-ttu-id="61bd8-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="61bd8-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="61bd8-125">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-125">✓</span></span> |
| <span data-ttu-id="61bd8-126">SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="61bd8-127">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-127">✓</span></span> |<span data-ttu-id="61bd8-128">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-128">✓</span></span> |
| <span data-ttu-id="61bd8-129">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61bd8-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="61bd8-130">✓</span><span class="sxs-lookup"><span data-stu-id="61bd8-130">✓</span></span> |&nbsp; |

<span data-ttu-id="61bd8-131">Para obtener más información sobre el uso de estas acciones de secuencia de comandos de tooapply de métodos, vea [HDInsight personalizar clústeres mediante acciones de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61bd8-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="61bd8-132"><a name="bestPracticeScripting"></a>Prácticas recomendadas para el desarrollo de scripts</span><span class="sxs-lookup"><span data-stu-id="61bd8-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="61bd8-133">Al desarrollar un script personalizado para un clúster de HDInsight, hay varios tookeep prácticas recomendadas en cuenta:</span><span class="sxs-lookup"><span data-stu-id="61bd8-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="61bd8-134">Versión de Hadoop de Hola de destino</span><span class="sxs-lookup"><span data-stu-id="61bd8-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="61bd8-135">Hola versión del sistema operativo de destino</span><span class="sxs-lookup"><span data-stu-id="61bd8-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="61bd8-136">Proporcionar estable vincula tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="61bd8-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="61bd8-137">Usar recursos compilados previamente</span><span class="sxs-lookup"><span data-stu-id="61bd8-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="61bd8-138">Asegúrese de que el script de personalización de clúster de hello es idempotente</span><span class="sxs-lookup"><span data-stu-id="61bd8-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="61bd8-139">Asegurar la alta disponibilidad de la arquitectura de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="61bd8-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="61bd8-140">Configurar el almacenamiento de blobs de Azure de hello componentes personalizados toouse</span><span class="sxs-lookup"><span data-stu-id="61bd8-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="61bd8-141">Escribir información tooSTDOUT y STDERR</span><span class="sxs-lookup"><span data-stu-id="61bd8-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="61bd8-142">Guardar los archivos como ASCII con el fin de línea LF</span><span class="sxs-lookup"><span data-stu-id="61bd8-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="61bd8-143">Usar toorecover de lógica de reintento de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="61bd8-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="61bd8-144">Acciones de script deben completarse dentro de 60 minutos o se produce un error en el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="61bd8-145">Durante el aprovisionamiento de nodo, el script de Hola se ejecuta simultáneamente con otros procesos de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="61bd8-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="61bd8-146">La competición por los recursos, como el ancho de banda de red o de tiempo de CPU puede provocar Hola script tootake más toofinish que lo hace en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="61bd8-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="61bd8-147"><a name="bPS1"></a>Versión de Hadoop de Hola de destino</span><span class="sxs-lookup"><span data-stu-id="61bd8-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="61bd8-148">Las distintas versiones de HDInsight tienen distintas versiones de componentes y servicios de Hadoop instalados.</span><span class="sxs-lookup"><span data-stu-id="61bd8-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="61bd8-149">Si la secuencia de comandos espera una versión específica de un servicio o componente, solo debería usar script de Hola con la versión de Hola de HDInsight que incluye componentes de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="61bd8-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="61bd8-150">Puede encontrar información sobre las versiones del componente incluido con HDInsight con hello [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="61bd8-151"><a name="bps10"></a>Versión de Hola SO de destino</span><span class="sxs-lookup"><span data-stu-id="61bd8-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="61bd8-152">HDInsight basados en Linux se basa en hello distribución Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="61bd8-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="61bd8-153">Las distintas versiones de HDInsight se basan en diferentes versiones de Ubuntu, que podrían cambiar el funcionamiento del script.</span><span class="sxs-lookup"><span data-stu-id="61bd8-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="61bd8-154">Por ejemplo, HDInsight 3.4 y versiones anteriores se basan en versiones de Ubuntu que emplean Upstart.</span><span class="sxs-lookup"><span data-stu-id="61bd8-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="61bd8-155">La versión 3.5 se basa en Ubuntu 16.04, que utiliza Systemd.</span><span class="sxs-lookup"><span data-stu-id="61bd8-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="61bd8-156">Systemd y advenedizo utilizan comandos diferentes, por lo que se debe escribir el script toowork con ambos.</span><span class="sxs-lookup"><span data-stu-id="61bd8-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="61bd8-157">Otra diferencia importante entre HDInsight 3.4 y 3.5 es que `JAVA_HOME` señale tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="61bd8-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="61bd8-158">Puede comprobar versión Hola SO mediante `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="61bd8-159">Hello código siguiente muestra cómo toodetermine si hello secuencia de comandos se ejecuta en Ubuntu 14 o 16:</span><span class="sxs-lookup"><span data-stu-id="61bd8-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="61bd8-160">Puede encontrar el script completo de Hola que contiene estos fragmentos de código en https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="61bd8-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="61bd8-161">Para versión de Hola de Ubuntu que usa HDInsight, vea hello [HDInsight la versión del componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="61bd8-162">vea las diferencias de hello toounderstand entre Systemd y advenedizo, [Systemd para los usuarios de advenedizo](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="61bd8-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="61bd8-163"><a name="bPS2"></a>Proporcionar estable vincula tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="61bd8-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="61bd8-164">Hello secuencia de comandos y los recursos asociados deben permanecer disponibles durante toda la duración de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="61bd8-165">Estos recursos son necesarios si se agregan nuevos nodos de clúster toohello durante las operaciones de ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="61bd8-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="61bd8-166">procedimiento recomendado de Hello es toodownload y archivar todo el contenido de una cuenta de almacenamiento de Azure en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="61bd8-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61bd8-167">cuenta de almacenamiento de Hello utilizada debe ser cuenta de almacenamiento del predeterminada Hola para clúster de Hola o un contenedor público, de solo lectura en ninguna otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="61bd8-168">Por ejemplo, ejemplos de hello proporcionados por Microsoft se almacenan en hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="61bd8-169">Se trata de un contenedor público, de solo lectura mantenido por el equipo de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="61bd8-170"><a name="bPS4"></a>Usar recursos compilados previamente</span><span class="sxs-lookup"><span data-stu-id="61bd8-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="61bd8-171">Hola tooreduce tiempo toma toorun Hola script, evitar las operaciones que se compilan los recursos desde el código fuente.</span><span class="sxs-lookup"><span data-stu-id="61bd8-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="61bd8-172">Por ejemplo, la compilación previa de recursos y almacenarlos en un blob de la cuenta de almacenamiento de Azure en hello mismo centro de datos como HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd8-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="61bd8-173"><a name="bPS3"></a>Asegúrese de que el script de personalización de clúster de hello es idempotente</span><span class="sxs-lookup"><span data-stu-id="61bd8-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="61bd8-174">Los scripts deben ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="61bd8-174">Scripts must be idempotent.</span></span> <span data-ttu-id="61bd8-175">Si se ejecuta el script de Hola varias veces, debería devolver Hola toohello clúster mismo estado cada vez.</span><span class="sxs-lookup"><span data-stu-id="61bd8-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="61bd8-176">Por ejemplo, un script que modifique los archivos de configuración no debería agregar entradas duplicadas si se ejecuta varias veces.</span><span class="sxs-lookup"><span data-stu-id="61bd8-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="61bd8-177"><a name="bPS5"></a>Asegurar la alta disponibilidad de la arquitectura de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="61bd8-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="61bd8-178">Los clústeres de HDInsight basados en Linux proporcionan dos nodos principales que están activos en el clúster de Hola y acciones de secuencia de comandos se ejecutan en ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="61bd8-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="61bd8-179">Si instala los componentes Hola esperan sólo un nodo principal, no instale componentes de hello en ambos nodos principales.</span><span class="sxs-lookup"><span data-stu-id="61bd8-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61bd8-180">Servicios proporcionados como parte de HDInsight son toofail diseñada sobre entre dos nodos principales del Hola según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="61bd8-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="61bd8-181">Esta funcionalidad no se amplía toocustom que se instalen a través de acciones de script.</span><span class="sxs-lookup"><span data-stu-id="61bd8-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="61bd8-182">Si necesita una disponibilidad elevada en componentes personalizados, deberá implementar su propio mecanismo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="61bd8-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="61bd8-183"><a name="bPS6"></a>Configurar el almacenamiento de blobs de Azure de hello componentes personalizados toouse</span><span class="sxs-lookup"><span data-stu-id="61bd8-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="61bd8-184">Componentes que se instalan en el clúster de hello podrían tener una configuración predeterminada que utiliza el almacenamiento de sistema de archivos distribuido de Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="61bd8-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="61bd8-185">HDInsight usa el almacenamiento de Azure o el almacén de Data Lake como almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="61bd8-186">Ambos proporcionan un sistema de archivos compatibles de HDFS que conserva los datos incluso si se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="61bd8-187">Puede que tenga los componentes de tooconfigure instalar toouse WASB o ADL en lugar de HDFS.</span><span class="sxs-lookup"><span data-stu-id="61bd8-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="61bd8-188">Para la mayoría de las operaciones, no es necesario toospecify sistema de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="61bd8-189">Por ejemplo, siguiente Hola copia archivo del archivo giraph-examples.jar hello de almacenamiento de toocluster del sistema de archivos local de hello:</span><span class="sxs-lookup"><span data-stu-id="61bd8-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="61bd8-190">En este ejemplo, Hola `hdfs` comando usa forma transparente el almacenamiento de clúster predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="61bd8-191">Para algunas operaciones, puede que necesite toospecify Hola URI.</span><span class="sxs-lookup"><span data-stu-id="61bd8-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="61bd8-192">Por ejemplo, `adl:///example/jars` para Data Lake Store o `wasb:///example/jars` para Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="61bd8-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="61bd8-193"><a name="bPS7"></a>Escribir información tooSTDOUT y STDERR</span><span class="sxs-lookup"><span data-stu-id="61bd8-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="61bd8-194">HDInsight registra el resultado de script que está escrito tooSTDOUT y STDERR.</span><span class="sxs-lookup"><span data-stu-id="61bd8-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="61bd8-195">Puede ver esta información mediante la interfaz de usuario de web de hello Ambari.</span><span class="sxs-lookup"><span data-stu-id="61bd8-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="61bd8-196">Ambari solo está disponible si Hola clúster se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="61bd8-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="61bd8-197">Si usa una acción de secuencia de comandos durante la creación del clúster y se produce un error de creación, consulte sección de solución de problemas de hello [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para conocer otras maneras de obtener acceso a información registrada.</span><span class="sxs-lookup"><span data-stu-id="61bd8-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="61bd8-198">Mayoría de las utilidades y los paquetes de instalación ya escriben información tooSTDOUT y STDERR, sin embargo, puede que desee tooadd inicio de sesión adicional.</span><span class="sxs-lookup"><span data-stu-id="61bd8-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="61bd8-199">texto toosend tooSTDOUT, use `echo`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="61bd8-200">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61bd8-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="61bd8-201">De forma predeterminada, `echo` envía Hola tooSTDOUT de cadena.</span><span class="sxs-lookup"><span data-stu-id="61bd8-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="61bd8-202">toodirect, tooSTDERR, agregue `>&2` antes de `echo`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="61bd8-203">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61bd8-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="61bd8-204">Esto redirige la información escrita tooSTDOUT tooSTDERR (2) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="61bd8-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="61bd8-205">Para obtener más información sobre la redirección de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="61bd8-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="61bd8-206">Para obtener más información sobre la visualización de información registrada por las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="61bd8-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="61bd8-207"><a name="bps8"></a> Guardar los archivos como ASCII con el fin de línea LF</span><span class="sxs-lookup"><span data-stu-id="61bd8-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="61bd8-208">Los scripts de Bash deben almacenarse con formato ASCII, con líneas terminadas con LF.</span><span class="sxs-lookup"><span data-stu-id="61bd8-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="61bd8-209">Se pueden producir archivos que se almacenan como UTF-8, o usan CRLF como final de la línea de Hola Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="61bd8-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="61bd8-210"><a name="bps9"></a>Usar toorecover de lógica de reintento de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="61bd8-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="61bd8-211">Al descargar archivos, instalar paquetes mediante get apt u otras acciones que transmiten datos a través de Hola internet, acción de hello puede producirse errores debido a errores de red tootransient.</span><span class="sxs-lookup"><span data-stu-id="61bd8-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="61bd8-212">Por ejemplo, recurso remoto de Hola que se está comunicando con puede estar en proceso de Hola de errores sobre el nodo de copia de seguridad de tooa.</span><span class="sxs-lookup"><span data-stu-id="61bd8-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="61bd8-213">toomake los errores de tootransient resistente a errores de secuencia de comandos, puede implementar la lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="61bd8-214">Hola siguiente función muestra cómo tooimplement lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="61bd8-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="61bd8-215">Vuelve a intentar la operación de hello tres veces antes de desistir.</span><span class="sxs-lookup"><span data-stu-id="61bd8-215">It retries hello operation three times before failing.</span></span>

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

<span data-ttu-id="61bd8-216">Hello en los ejemplos siguientes se muestran cómo toouse esta función.</span><span class="sxs-lookup"><span data-stu-id="61bd8-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="61bd8-217"><a name="helpermethods"></a>Métodos auxiliares para scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="61bd8-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="61bd8-218">Los métodos auxiliares de la acción de script son utilidades que puede usar al escribir scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="61bd8-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="61bd8-219">Estos métodos se encuentran en el script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="61bd8-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="61bd8-220">Usar hello después toodownload y usarlas como parte de la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="61bd8-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="61bd8-221">Hola después Ayudantes disponibles para su uso en la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="61bd8-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="61bd8-222">Uso de la aplicación auxiliar</span><span class="sxs-lookup"><span data-stu-id="61bd8-222">Helper usage</span></span> | <span data-ttu-id="61bd8-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="61bd8-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="61bd8-224">Descarga un archivo de hello origen URI toohello ruta de acceso especificada.</span><span class="sxs-lookup"><span data-stu-id="61bd8-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="61bd8-225">De forma predeterminada, no sobrescribirá un archivo existente.</span><span class="sxs-lookup"><span data-stu-id="61bd8-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="61bd8-226">Extrae un archivo tar (mediante `-xf`) toohello directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="61bd8-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="61bd8-227">Si se ejecutaba en un nodo principal del clúster, devuelve 1. En caso contrario, devuelve 0.</span><span class="sxs-lookup"><span data-stu-id="61bd8-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="61bd8-228">Si el nodo actual de hello es un nodo de datos (trabajo), devuelve un 1; en caso contrario, es 0.</span><span class="sxs-lookup"><span data-stu-id="61bd8-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="61bd8-229">Si el nodo actual de hello es datos primera hello (trabajo) nodo (con nombre workernode0) devuelve un 1; en caso contrario, es 0.</span><span class="sxs-lookup"><span data-stu-id="61bd8-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="61bd8-230">Devuelve el nombre de dominio completo de Hola de hello headnodes de clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="61bd8-231">Los nombres están delimitados por comas.</span><span class="sxs-lookup"><span data-stu-id="61bd8-231">Names are comma delimited.</span></span> <span data-ttu-id="61bd8-232">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="61bd8-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="61bd8-233">Obtiene el nombre de dominio completo de Hola de nodo principal de hello principal.</span><span class="sxs-lookup"><span data-stu-id="61bd8-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="61bd8-234">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="61bd8-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="61bd8-235">Obtiene el nombre de dominio completo de Hola de nodo principal de hello secundaria.</span><span class="sxs-lookup"><span data-stu-id="61bd8-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="61bd8-236">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="61bd8-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="61bd8-237">Obtiene el sufijo numérico de Hola de nodo principal primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="61bd8-238">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="61bd8-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="61bd8-239">Obtiene el sufijo numérico de Hola de nodo principal secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="61bd8-240">En caso de error, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="61bd8-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="61bd8-241"><a name="commonusage"></a>Patrones de uso común</span><span class="sxs-lookup"><span data-stu-id="61bd8-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="61bd8-242">Esta sección proporciona instrucciones sobre cómo implementar algunos Hola patrones de uso comunes que pueden surgir al escribir sus propios scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="61bd8-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="61bd8-243">Pasar parámetros de script tooa</span><span class="sxs-lookup"><span data-stu-id="61bd8-243">Passing parameters tooa script</span></span>

<span data-ttu-id="61bd8-244">En algunos casos, un script puede requerir parámetros.</span><span class="sxs-lookup"><span data-stu-id="61bd8-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="61bd8-245">Por ejemplo, puede necesitar contraseña de administrador de Hola para clúster hello cuando se usa la API de REST de Ambari Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="61bd8-246">Se denominan parámetros pasados script toohello *parámetros posicionales*y se asignan demasiado`$1` para el primer parámetro hello, `$2` para hello segundo y por lo que la sesión.</span><span class="sxs-lookup"><span data-stu-id="61bd8-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="61bd8-247">`$0`contiene el nombre de hello del propio script de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="61bd8-248">Valores pasados toohello script como parámetros deberían estar entre comillas simples (').</span><span class="sxs-lookup"><span data-stu-id="61bd8-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="61bd8-249">Este modo se asegura que Hola pasado el valor se trata como un literal.</span><span class="sxs-lookup"><span data-stu-id="61bd8-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="61bd8-250">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="61bd8-250">Setting environment variables</span></span>

<span data-ttu-id="61bd8-251">Establecer una variable de entorno se realiza por hello siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="61bd8-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="61bd8-252">Donde VARIABLENAME es nombre Hola de variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="61bd8-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="61bd8-253">uso de variables, tooaccess hello `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="61bd8-254">Por ejemplo, tooassign un valor proporcionado por un parámetro posicional como una variable de entorno denominada contraseña, usaría Hola siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="61bd8-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="61bd8-255">A continuación, podría utilizar la información de acceso subsiguiente toohello `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="61bd8-256">Las variables de entorno que se establece en el script de Hola solo existen en ámbito de Hola de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="61bd8-257">En algunos casos, deberá variables de entorno de todo el sistema de tooadd que se conservarán cuando finalice el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="61bd8-258">variables de entorno de todo el sistema de tooadd, Agregar variable Hola demasiado`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="61bd8-259">Por ejemplo, hello siguiente instrucción agrega `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="61bd8-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="61bd8-260">Toolocations de acceso donde se almacenan los scripts personalizados de Hola</span><span class="sxs-lookup"><span data-stu-id="61bd8-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="61bd8-261">Toocustomize de secuencias de comandos que se utiliza un clúster debe toobe almacenado en una de las siguientes ubicaciones de Hola:</span><span class="sxs-lookup"><span data-stu-id="61bd8-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="61bd8-262">Un __cuenta de almacenamiento de Azure__ que está asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="61bd8-263">Un __cuenta de almacenamiento adicional__ asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="61bd8-264">Un __URI legible públicamente__.</span><span class="sxs-lookup"><span data-stu-id="61bd8-264">A __publicly readable URI__.</span></span> <span data-ttu-id="61bd8-265">Por ejemplo, un toodata de dirección URL almacenado en OneDrive, Dropbox o en otro archivo de servicio de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="61bd8-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="61bd8-266">Un __cuenta de almacén de Azure Data Lake__ que está asociado con el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="61bd8-267">Para más información sobre el uso de Azure Data Lake Store con HDInsight, consulte [Creación de un clúster de HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61bd8-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="61bd8-268">Hola servicio principal HDInsight utiliza tooaccess almacén de Data Lake debe tener acceso de lectura toohello script.</span><span class="sxs-lookup"><span data-stu-id="61bd8-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="61bd8-269">Recursos utilizados por el script de Hola también deben estar disponibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="61bd8-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="61bd8-270">Almacenar archivos de hello en una cuenta de almacenamiento de Azure o un almacén de Data Lake de Azure proporciona un acceso rápido, como en hello red de Azure.</span><span class="sxs-lookup"><span data-stu-id="61bd8-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="61bd8-271">Hola URI formato usado tooreference Hola script depende de servicio Hola usándola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="61bd8-272">Para las cuentas de almacenamiento asociadas con el clúster de HDInsight de hello, use `wasb://` o `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="61bd8-273">Para los URI legibles públicamente, use `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="61bd8-274">Para Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="61bd8-275">Comprobación de la versión de sistema operativo de Hola</span><span class="sxs-lookup"><span data-stu-id="61bd8-275">Checking hello operating system version</span></span>

<span data-ttu-id="61bd8-276">Las distintas versiones de HDInsight se basan en versiones específicas de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="61bd8-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="61bd8-277">Puede haber diferencias entre las versiones del sistema operativo que debe comprobar en el script.</span><span class="sxs-lookup"><span data-stu-id="61bd8-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="61bd8-278">Por ejemplo, puede que necesite tooinstall un archivo binario que está enlazada toohello versión de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="61bd8-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="61bd8-279">versión de Hola OS toocheck, use `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="61bd8-280">Por ejemplo, hello siguiente secuencia de comandos muestra cómo tooreference una tar específico de archivos según Hola versión del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="61bd8-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

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

## <span data-ttu-id="61bd8-281"><a name="deployScript"></a>Lista de comprobación para implementar una acción de script</span><span class="sxs-lookup"><span data-stu-id="61bd8-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="61bd8-282">Estos son los pasos de Hola que se llevaron a cabo al preparar toodeploy estas secuencias de comandos:</span><span class="sxs-lookup"><span data-stu-id="61bd8-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="61bd8-283">Coloque los archivos de Hola que contienen scripts personalizados de hello en un lugar que sea accesible para nodos de clúster de Hola durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="61bd8-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="61bd8-284">Por ejemplo, hello almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="61bd8-285">Los archivos también se pueden almacenar en servicios de hospedaje visibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="61bd8-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="61bd8-286">Compruebe que el script de Hola es impotent.</span><span class="sxs-lookup"><span data-stu-id="61bd8-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="61bd8-287">Esto permite que toobe de script de Hola ejecuta varias veces en hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="61bd8-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="61bd8-288">Use un hello tookeep de archivo temporal directorio/tmp descargan archivos utilizados por las secuencias de comandos de hello y, a continuación, limpiarlas después de que se han ejecutado las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="61bd8-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="61bd8-289">Si se cambian los valores de configuración de nivel de sistema operativo o archivos de configuración de servicio de Hadoop, puede que desee toorestart HDInsight servicios.</span><span class="sxs-lookup"><span data-stu-id="61bd8-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="61bd8-290"><a name="runScriptAction"></a>¿Cómo toorun una acción de secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="61bd8-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="61bd8-291">Puede utilizar clústeres de HDInsight de toocustomize script acciones con hello siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="61bd8-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="61bd8-292">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61bd8-292">Azure portal</span></span>
* <span data-ttu-id="61bd8-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61bd8-293">Azure PowerShell</span></span>
* <span data-ttu-id="61bd8-294">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61bd8-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="61bd8-295">Hola HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="61bd8-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="61bd8-296">Para obtener más información sobre el uso de cada método, consulte [cómo toouse script acción](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61bd8-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="61bd8-297"><a name="sampleScripts"></a>Ejemplos de scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="61bd8-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="61bd8-298">Microsoft proporciona secuencias de comandos de ejemplo tooinstall componentes en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd8-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="61bd8-299">Vea los siguientes vínculos para ver más acciones de script de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="61bd8-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="61bd8-300">Instalación y uso de Hue en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="61bd8-301">Instalación y uso de Solr en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="61bd8-302">Instalación y uso de Giraph en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="61bd8-303">Instalación o actualización de Mono en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="61bd8-304">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="61bd8-304">Troubleshooting</span></span>

<span data-ttu-id="61bd8-305">siguiente Hola es errores que pueden producirse al utilizar secuencias de comandos que se han desarrollado:</span><span class="sxs-lookup"><span data-stu-id="61bd8-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="61bd8-306">**Error**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="61bd8-307">A veces seguido de `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="61bd8-308">*Causa*: este error se produce cuando las líneas de hello en una secuencia de comandos se terminan con CRLF.</span><span class="sxs-lookup"><span data-stu-id="61bd8-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="61bd8-309">Los sistemas UNIX esperan sólo LF como final de la línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="61bd8-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="61bd8-310">Este problema suele producirse cuando se ha creado en un entorno de Windows, el script de Hola CRLF sea una línea común final para muchos editores de texto en Windows.</span><span class="sxs-lookup"><span data-stu-id="61bd8-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="61bd8-311">*Resolución*: si es una opción en el editor de texto, seleccione formato Unix o LF final de la línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="61bd8-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="61bd8-312">También puede usar Hola siguientes comandos en un tooan de Unix sistema toochange Hola CRLF LF:</span><span class="sxs-lookup"><span data-stu-id="61bd8-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="61bd8-313">Hello siguientes comandos son aproximadamente equivalentes en que deben cambiar Hola CRLF línea finales tooLF.</span><span class="sxs-lookup"><span data-stu-id="61bd8-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="61bd8-314">Seleccione una basada en utilidades de hello disponibles en el sistema.</span><span class="sxs-lookup"><span data-stu-id="61bd8-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="61bd8-315">Comando</span><span class="sxs-lookup"><span data-stu-id="61bd8-315">Command</span></span> | <span data-ttu-id="61bd8-316">Notas</span><span class="sxs-lookup"><span data-stu-id="61bd8-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="61bd8-317">archivo original de Hello está respaldado por una. Extensión BAK</span><span class="sxs-lookup"><span data-stu-id="61bd8-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="61bd8-318">OUTFILE contendrá una versión con finales de línea solo LF</span><span class="sxs-lookup"><span data-stu-id="61bd8-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="61bd8-319">Modifica el archivo hello directamente</span><span class="sxs-lookup"><span data-stu-id="61bd8-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="61bd8-320">OUTFILE contendrá una versión con finales de línea solo LF.</span><span class="sxs-lookup"><span data-stu-id="61bd8-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="61bd8-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="61bd8-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="61bd8-322">*Causa*: este error se produce cuando hello script se guarda como UTF-8 con una marca de orden de bytes (BOM).</span><span class="sxs-lookup"><span data-stu-id="61bd8-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="61bd8-323">*Resolución*: guardar el archivo hello como ASCII o UTF-8 sin una marca BOM.</span><span class="sxs-lookup"><span data-stu-id="61bd8-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="61bd8-324">También puede usar el siguiente comando en un sistema Linux o Unix toocreate un archivo sin Hola BOM de hello:</span><span class="sxs-lookup"><span data-stu-id="61bd8-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="61bd8-325">Reemplace `INFILE` con archivo hello que contiene Hola BOM.</span><span class="sxs-lookup"><span data-stu-id="61bd8-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="61bd8-326">`OUTFILE`debe ser un nuevo nombre de archivo que contiene el script de Hola sin Hola BOM.</span><span class="sxs-lookup"><span data-stu-id="61bd8-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="61bd8-327"><a name="seeAlso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61bd8-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="61bd8-328">Obtenga información acerca de cómo demasiado[clústeres de HDInsight personalizar mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="61bd8-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="61bd8-329">Hola de uso [referencia de SDK de HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx) toolearn más acerca de cómo crear aplicaciones .NET que administración HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd8-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="61bd8-330">Hola de uso [API de REST de HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn cómo clústeres acciones de administración de toouse REST tooperform en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd8-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
