---
title: aaaInstall o actualizar Mono en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse una versión específica de Mono con clúster de HDInsight. Mono es toorun usa .NET applications en clústeres de HDInsight basados en Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="f522b-104">Instalación o actualización de Mono en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f522b-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="f522b-105">Obtenga información acerca de cómo tooinstall una versión específica de [Mono](https://www.mono-project.com) en HDInsight 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="f522b-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="f522b-106">Mono se instala en HDInsight 3.4 y versiones posteriores y es toorun usa .NET applications.</span><span class="sxs-lookup"><span data-stu-id="f522b-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="f522b-107">Para obtener información sobre la versión de Hola de Mono que se incluyen con cada versión de HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f522b-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f522b-108">tooinstall una versión diferente en el clúster, la acción de secuencia de comandos de uso hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="f522b-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="f522b-109">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="f522b-109">How it works</span></span>

<span data-ttu-id="f522b-110">Esta secuencia de comandos acepta Hola después de parámetro:</span><span class="sxs-lookup"><span data-stu-id="f522b-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="f522b-111">__Número de versión mono__: versión de Hola de tooinstall Mono.</span><span class="sxs-lookup"><span data-stu-id="f522b-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="f522b-112">versión de Hola debe estar disponible desde [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="f522b-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="f522b-113">script de Hola instala Hola siguientes Mono paquetes:</span><span class="sxs-lookup"><span data-stu-id="f522b-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="f522b-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="f522b-114">__mono-complete__</span></span>

* <span data-ttu-id="f522b-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="f522b-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="f522b-116">script de Hola</span><span class="sxs-lookup"><span data-stu-id="f522b-116">hello script</span></span>

<span data-ttu-id="f522b-117">__Ubicación de script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="f522b-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="f522b-118">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="f522b-118">__Requirements__:</span></span>

* <span data-ttu-id="f522b-119">se debe aplicar el script de Hola en hello __head nodos__ y __nodos de trabajador__.</span><span class="sxs-lookup"><span data-stu-id="f522b-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="f522b-120">script de Hola toouse</span><span class="sxs-lookup"><span data-stu-id="f522b-120">toouse hello script</span></span>

<span data-ttu-id="f522b-121">Para obtener información sobre cómo toouse esta secuencia de comandos con HDInsight, vea hello [mediante la acción de secuencia de comandos de clústeres de HDInsight basados en Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="f522b-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="f522b-122">Puede usar el script de Hola Hola portal de Azure, Azure PowerShell, u Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f522b-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="f522b-123">Mientras siguiente hello documento de la acción de secuencia de comandos, utilice Hola siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="f522b-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="f522b-124">Al configurar HDInsight con este script, marque el script de Hola como __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="f522b-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="f522b-125">Esta configuración permite HDInsight tooapply nodos de hello script tooworker agregados a través de las operaciones de ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="f522b-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f522b-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f522b-126">Next steps</span></span>

<span data-ttu-id="f522b-127">Ha aprendido cómo tooupgrade o instale una versión específica de Mono en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f522b-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="f522b-128">Para obtener más información sobre el uso de aplicaciones .NET con Mono en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="f522b-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f522b-129">Uso de .NET con el streaming de MapReduce en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f522b-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="f522b-130">Uso de .NET con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f522b-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="f522b-131">Desarrollo de topologías de C# para Apache Storm en HDInsight con herramientas de Hadoop para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f522b-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="f522b-132">Migrar soluciones de .NET basada en tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="f522b-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="f522b-133">Para más información sobre el uso de las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f522b-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>