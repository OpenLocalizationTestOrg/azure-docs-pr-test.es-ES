---
title: "creación - Azure de clústeres de bibliotecas de Hive aaaAdd durante HDInsight | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd Hive bibliotecas (archivos jar), tooan HDInsight clúster durante la creación del clúster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="fc80e-103">Incorporación de bibliotecas personalizadas de Hive al crear el clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="fc80e-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="fc80e-104">Si dispone de las bibliotecas que utilizan con frecuencia con Hive en HDInsight, este documento contiene información sobre el uso de una biblioteca de acción de secuencia de comandos toopre carga Hola durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fc80e-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="fc80e-105">Las bibliotecas que se agregan mediante los pasos de hello en este documento están disponibles globalmente en el subárbol: no hay ninguna necesidad de toouse [agregar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload ellos.</span><span class="sxs-lookup"><span data-stu-id="fc80e-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fc80e-106">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="fc80e-106">How it works</span></span>

<span data-ttu-id="fc80e-107">Al crear un clúster, también puede especificar una acción de secuencia de comandos que se ejecuta una secuencia de comandos en nodos de clúster de hello mientras se crea.</span><span class="sxs-lookup"><span data-stu-id="fc80e-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="fc80e-108">script de Hola en este documento acepta un único parámetro, que es una ubicación de WASB que contenga Hola bibliotecas (almacenadas como archivos jar) toobe previamente cargado.</span><span class="sxs-lookup"><span data-stu-id="fc80e-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="fc80e-109">Durante la creación del clúster, script de Hola enumera los archivos de hello, copiarlos en toohello `/usr/lib/customhivelibs/` directorio en los nodos principal y de trabajo, a continuación, agrega toohello `hive.aux.jars.path` propiedad Hola `core-site.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="fc80e-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="fc80e-110">En los clústeres basados en Linux, también actualiza hello `hive-env.sh` archivo con la ubicación Hola archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="fc80e-111">Con las acciones de script de Hola en este artículo incluye bibliotecas de hello en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc80e-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="fc80e-112">**HDInsight basados en Linux** : al usar Hola un cliente de Hive, **WebHCat**, y **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="fc80e-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="fc80e-113">**HDInsight basados en Windows** : cuando se usa el cliente de Hive de Hola y **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="fc80e-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="fc80e-114">script de Hola</span><span class="sxs-lookup"><span data-stu-id="fc80e-114">hello script</span></span>

<span data-ttu-id="fc80e-115">**Ubicación del script**</span><span class="sxs-lookup"><span data-stu-id="fc80e-115">**Script location**</span></span>

<span data-ttu-id="fc80e-116">En los **clústeres basados en Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="fc80e-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="fc80e-117">En los **clústeres basados en Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="fc80e-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc80e-118">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="fc80e-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fc80e-119">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fc80e-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="fc80e-120">**Requisitos**</span><span class="sxs-lookup"><span data-stu-id="fc80e-120">**Requirements**</span></span>

* <span data-ttu-id="fc80e-121">scripts de Hello deben ser aplicado tooboth Hola **Head nodos** y **nodos de trabajador**.</span><span class="sxs-lookup"><span data-stu-id="fc80e-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="fc80e-122">Hola JAR desea tooinstall deben estar almacenados en almacenamiento de blobs de Azure en un **único contenedor**.</span><span class="sxs-lookup"><span data-stu-id="fc80e-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="fc80e-123">cuenta de almacenamiento de Hola que contiene la biblioteca de Hola de archivos jar **debe** ser toohello vinculado HDInsight clúster durante la creación.</span><span class="sxs-lookup"><span data-stu-id="fc80e-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="fc80e-124">Debe ser cuenta de almacenamiento predeterminada de Hola o agrega una cuenta a través de __configuración opcional__.</span><span class="sxs-lookup"><span data-stu-id="fc80e-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="fc80e-125">contenedor de toohello de ruta de acceso de Hello WASB debe especificarse como una acción de secuencia de comandos de toohello de parámetro.</span><span class="sxs-lookup"><span data-stu-id="fc80e-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="fc80e-126">Por ejemplo, si hello archivos JAR se almacena en un contenedor denominado **bibliotecas** en una cuenta de almacenamiento denominada **mystorage**, sería el parámetro hello  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="fc80e-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fc80e-127">Este documento se supone que ya ha crear una cuenta de almacenamiento, contenedor de blobs y tooit de archivos cargados Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="fc80e-128">Si no ha creado una cuenta de almacenamiento, puede hacerlo a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc80e-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fc80e-129">A continuación, puede usar una utilidad como [Azure Storage Explorer](http://storageexplorer.com/) toocreate un contenedor en la cuenta de hello y carga archivos tooit.</span><span class="sxs-lookup"><span data-stu-id="fc80e-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="fc80e-130">Crear un clúster mediante el script de Hola</span><span class="sxs-lookup"><span data-stu-id="fc80e-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="fc80e-131">Hola pasos crea un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="fc80e-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fc80e-132">Seleccione un clúster basado en Windows, toocreate **Windows** como Hola clúster SO al crear el clúster de Hola y utilizar secuencias de comandos de Windows (PowerShell) de hello en lugar de la secuencia de comandos de hello intensiva de errores.</span><span class="sxs-lookup"><span data-stu-id="fc80e-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="fc80e-133">También puede usar PowerShell de Azure o hello HDInsight .NET SDK toocreate un clúster mediante esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="fc80e-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="fc80e-134">Para obtener más información sobre el uso de estos métodos, consulte [Personalización de clústeres de HDInsight mediante acciones de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc80e-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="fc80e-135">Iniciar el aprovisionamiento de un clúster mediante el uso de pasos de hello en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md), pero no complete el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="fc80e-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="fc80e-136">En hello **configuración opcional** hoja, seleccione **acciones de Script**y proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="fc80e-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="fc80e-137">**NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="fc80e-138">**URI DEL SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="fc80e-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="fc80e-139">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="fc80e-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="fc80e-140">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="fc80e-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="fc80e-141">**ZOOKEEPER**: déjelo en blanco.</span><span class="sxs-lookup"><span data-stu-id="fc80e-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="fc80e-142">**PARÁMETROS**: escriba hello WASB toohello contenedor y el almacenamiento cuenta de dirección que contiene archivos JAR Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="fc80e-143">Por ejemplo, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="fc80e-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="fc80e-144">Final de Hola de hello **acciones de Script**, usar hello **seleccione** configuración del botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="fc80e-145">En hello **configuración opcional** hoja, seleccione **cuentas de almacenamiento vinculadas** y seleccione hello **agregar una clave de almacenamiento** vínculo.</span><span class="sxs-lookup"><span data-stu-id="fc80e-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="fc80e-146">Seleccionar cuenta de almacenamiento de Hola que contiene archivos JAR hello y, a continuación, usar hello **seleccione** devuelto hello y configuración de botones toosave **configuración opcional** hoja.</span><span class="sxs-lookup"><span data-stu-id="fc80e-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="fc80e-147">Hola de uso **seleccione** situado en la parte inferior de Hola de hello **configuración opcional** información de configuración opcional de hoja toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="fc80e-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="fc80e-148">Continuar aprovisionamiento clúster Hola tal y como se describe en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fc80e-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="fc80e-149">Una vez finalizada la creación del clúster, es capaz de toouse archivos JAR Hola agregada a través de este script de Hive sin necesidad de hello toouse `ADD JAR` instrucción.</span><span class="sxs-lookup"><span data-stu-id="fc80e-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc80e-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc80e-150">Next steps</span></span>

<span data-ttu-id="fc80e-151">Para obtener más información acerca del trabajo con Hive, consulte [Use Hive with HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="fc80e-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
