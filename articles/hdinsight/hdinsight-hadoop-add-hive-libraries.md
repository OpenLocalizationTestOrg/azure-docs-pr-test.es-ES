---
title: "Incorporación de bibliotecas de Hive durante la creación de clústeres de HDInsight - Azure | Microsoft Docs"
description: "Aprenda a agregar bibliotecas de Hive (archivos JAR) a un clúster de HDInsight durante la creación del clúster."
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
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="c39a4-103">Incorporación de bibliotecas personalizadas de Hive al crear el clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c39a4-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="c39a4-104">Este documento contiene información sobre el uso de una acción de script para cargar previamente bibliotecas durante la creación de un clúster, por lo que puede resultarle interesante si dispone de bibliotecas que utiliza con frecuencia con Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c39a4-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="c39a4-105">Las bibliotecas que se agregan mediante los pasos de este documento están disponibles globalmente en Hive: no hace falta usar [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) para cargarlos.</span><span class="sxs-lookup"><span data-stu-id="c39a4-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c39a4-106">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="c39a4-106">How it works</span></span>

<span data-ttu-id="c39a4-107">Cuando cree un clúster, también tiene la posibilidad de especificar opcionalmente una acción de script que ejecute un script en los nodos del clúster mientras estos se crean.</span><span class="sxs-lookup"><span data-stu-id="c39a4-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="c39a4-108">El script de este documento acepta un único parámetro, que es una ubicación de WASB que contiene las bibliotecas (almacenadas como archivos JAR) que se cargarán previamente.</span><span class="sxs-lookup"><span data-stu-id="c39a4-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="c39a4-109">Durante la creación del clúster, el script enumera los archivos, los copia en el directorio `/usr/lib/customhivelibs/` de los nodos principal y de trabajo y luego los agrega a la propiedad `hive.aux.jars.path` en el archivo `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="c39a4-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="c39a4-110">En los clústeres basados en Linux, también actualiza el archivo `hive-env.sh` con la ubicación de los archivos.</span><span class="sxs-lookup"><span data-stu-id="c39a4-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="c39a4-111">El uso de las acciones de script de este artículo permite que las bibliotecas estén disponibles en las situaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c39a4-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="c39a4-112">**HDInsight basado en Linux**: cuando se usa un cliente de Hive, **WebHCat** y **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="c39a4-113">**HDInsight basado en Windows**: cuando se usa el cliente de Hive y **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="c39a4-114">La secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="c39a4-114">The script</span></span>

<span data-ttu-id="c39a4-115">**Ubicación del script**</span><span class="sxs-lookup"><span data-stu-id="c39a4-115">**Script location**</span></span>

<span data-ttu-id="c39a4-116">En los **clústeres basados en Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="c39a4-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="c39a4-117">En los **clústeres basados en Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="c39a4-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c39a4-118">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="c39a4-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c39a4-119">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c39a4-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c39a4-120">**Requisitos**</span><span class="sxs-lookup"><span data-stu-id="c39a4-120">**Requirements**</span></span>

* <span data-ttu-id="c39a4-121">Las scripts deben aplicarse tanto a los **nodos principales** como a los **nodos de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="c39a4-122">Los archivos JAR que se van a instalar deben almacenarse en Azure Blob Storage en un **único contenedor**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="c39a4-123">La cuenta de almacenamiento que contiene la biblioteca de archivos JAR **debe** vincularse al clúster de HDInsight durante la creación.</span><span class="sxs-lookup"><span data-stu-id="c39a4-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="c39a4-124">Debe ser la cuenta de almacenamiento predeterminada o una agregada a través de la __configuración opcional__.</span><span class="sxs-lookup"><span data-stu-id="c39a4-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="c39a4-125">La ruta de acceso de WASB al contenedor debe especificarse como un parámetro para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="c39a4-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="c39a4-126">Por ejemplo, si los archivos JAR se almacenan en un contenedor llamado **libs** en una cuenta de almacenamiento llamada **mystorage**, el parámetro sería **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c39a4-127">En este documento se supone que ha creado ya una cuenta de almacenamiento, contenedora de blobs, y ha cargado los archivos en ella.</span><span class="sxs-lookup"><span data-stu-id="c39a4-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="c39a4-128">Si no ha creado una cuenta de almacenamiento, puede hacerlo a través de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c39a4-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c39a4-129">Después, puede usar una utilidad como el [Explorador de almacenamiento de Azure](http://storageexplorer.com/) para crear un contenedor en la cuenta y cargar archivos en él.</span><span class="sxs-lookup"><span data-stu-id="c39a4-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="c39a4-130">Creación de un clúster mediante el script</span><span class="sxs-lookup"><span data-stu-id="c39a4-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="c39a4-131">Al seguir estos pasos, se crea un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="c39a4-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c39a4-132">Para crear un clúster basado en Windows, seleccione **Windows** como sistema operativo del clúster en el momento de su creación y use el script de Windows (PowerShell) en lugar del script de Bash.</span><span class="sxs-lookup"><span data-stu-id="c39a4-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="c39a4-133">También puede usar Azure PowerShell o el SDK de .NET para HDInsight para crear un clúster mediante este script.</span><span class="sxs-lookup"><span data-stu-id="c39a4-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="c39a4-134">Para obtener más información sobre el uso de estos métodos, consulte [Personalización de clústeres de HDInsight mediante acciones de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c39a4-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="c39a4-135">Inicie el aprovisionamiento de un clúster siguiendo los pasos que se describen en [Aprovisionamiento de clústeres de HDInsight en Linux](hdinsight-hadoop-provision-linux-clusters.md), pero no complete la operación.</span><span class="sxs-lookup"><span data-stu-id="c39a4-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="c39a4-136">En la hoja **Configuración opcional**, seleccione **Acciones de script** y proporcione la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="c39a4-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="c39a4-137">**NOMBRE**: escriba un nombre descriptivo para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="c39a4-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="c39a4-138">**URI DEL SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="c39a4-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="c39a4-139">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="c39a4-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="c39a4-140">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="c39a4-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="c39a4-141">**ZOOKEEPER**: déjelo en blanco.</span><span class="sxs-lookup"><span data-stu-id="c39a4-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="c39a4-142">**PARÁMETROS**: escriba la dirección WASB que dirige al contenedor y la cuenta de almacenamiento que contiene los archivos JAR.</span><span class="sxs-lookup"><span data-stu-id="c39a4-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="c39a4-143">Por ejemplo, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="c39a4-144">En la parte inferior de **Acciones de scripts**, use el botón **Seleccionar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="c39a4-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="c39a4-145">En la hoja **Configuración opcional**, seleccione **Cuentas de almacenamiento vinculadas** y luego el vínculo **Agregar una clave de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="c39a4-146">Seleccione la cuenta de almacenamiento que contiene los archivos JAR y, después, use los botones de **selección** para guardar la configuración y volver a la hoja **Configuración opcional**.</span><span class="sxs-lookup"><span data-stu-id="c39a4-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="c39a4-147">Use el botón **Seleccionar** situado en la parte inferior de la hoja **Configuración opcional** para guardar la información de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="c39a4-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="c39a4-148">Continúe aprovisionando el clúster tal como se describe en [Aprovisionamiento de clústeres de HDInsight en Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c39a4-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="c39a4-149">Una vez finalizada la creación del clúster, podrá utilizar los archivos JAR agregados a través de este script desde Hive sin tener que utilizar la instrucción `ADD JAR`.</span><span class="sxs-lookup"><span data-stu-id="c39a4-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c39a4-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c39a4-150">Next steps</span></span>

<span data-ttu-id="c39a4-151">Para obtener más información acerca del trabajo con Hive, consulte [Use Hive with HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="c39a4-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
