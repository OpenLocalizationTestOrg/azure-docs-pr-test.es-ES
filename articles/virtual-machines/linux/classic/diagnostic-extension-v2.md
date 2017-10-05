---
title: "Supervisión de una máquina virtual de Linux con una extensión de máquina virtual | Microsoft Docs"
description: "Obtenga información sobre cómo usar la extensión de diagnóstico de Linux para supervisar los datos de rendimiento y diagnóstico de una máquina virtual Linux de Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="48ce7-103">Uso de la extensión de diagnóstico de Linux para supervisar los datos de rendimiento y diagnóstico de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="48ce7-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="48ce7-104">En este documento se describe la versión 2.3 de la extensión Diagnostics de Linux.</span><span class="sxs-lookup"><span data-stu-id="48ce7-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48ce7-105">Esta versión está en desuso y puede eliminarse en cualquier momento a partir del 30 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="48ce7-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="48ce7-106">La sustituye la versión 3.0.</span><span class="sxs-lookup"><span data-stu-id="48ce7-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="48ce7-107">Para obtener más información, consulte los [documentos de la versión 3.0 de la extensión Diagnostics de Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="48ce7-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="48ce7-108">Introducción</span><span class="sxs-lookup"><span data-stu-id="48ce7-108">Introduction</span></span>

<span data-ttu-id="48ce7-109">(**Nota**: La extensión de diagnóstico de Linux se ofrece como código abierto en [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic), donde se publica primero la información más actualizada sobre la extensión.</span><span class="sxs-lookup"><span data-stu-id="48ce7-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="48ce7-110">Es posible que quiera comprobar antes la [página de GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)).</span><span class="sxs-lookup"><span data-stu-id="48ce7-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="48ce7-111">La extensión de diagnóstico de Linux ayuda a los usuarios a supervisar las máquinas virtuales Linux que se ejecutan en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="48ce7-112">Ofrece la siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="48ce7-112">It has the following capabilities:</span></span>

* <span data-ttu-id="48ce7-113">Recopila y carga la información de rendimiento del sistema de la máquina virtual Linux en la tabla de almacenamiento del usuario, incluidos los datos de diagnóstico y Syslog.</span><span class="sxs-lookup"><span data-stu-id="48ce7-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="48ce7-114">Permite a los usuarios personalizar las métricas de datos que se recopilan y se cargan.</span><span class="sxs-lookup"><span data-stu-id="48ce7-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="48ce7-115">Permite a los usuarios cargar los archivos de registro especificados en la tabla de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="48ce7-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="48ce7-116">En la versión 2.3 actual, los datos incluyen la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="48ce7-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="48ce7-117">Todos los registros de Linux Rsyslog, incluidos los relacionados con el sistema, la seguridad y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48ce7-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="48ce7-118">Todos los datos del sistema que se especifican en el [sitio de soluciones multiplataforma de System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="48ce7-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="48ce7-119">Archivos de registro especificados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="48ce7-119">User-specified log files.</span></span>

<span data-ttu-id="48ce7-120">Esta extensión funciona tanto con el modelo de implementación clásico como con el de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48ce7-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="48ce7-121">La versión actual de la extensión y el desuso de las versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="48ce7-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="48ce7-122">La versión más reciente de la extensión es la **2.3** y **cualquier versión anterior (2.0, 2.1 y 2.2) quedará en desuso y se retirará a finales de este año (2017)**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="48ce7-123">Si ha instalado la extensión de diagnóstico de Linux con la actualización automática de versión secundaria deshabilitada, es muy recomendable que la desinstale y la vuelva a instalar con la actualización automática de versión secundaria habilitada.</span><span class="sxs-lookup"><span data-stu-id="48ce7-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="48ce7-124">En máquinas virtuales clásicas (ASM), puede hacerlo especificando '2.*' como versión, si va a instalar la extensión mediante la CLI XPLAT de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48ce7-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="48ce7-125">En máquinas virtuales de ARM, puede realizarlo mediante la inclusión de ' "autoUpgradeMinorVersion": true' en la plantilla de implementación de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="48ce7-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="48ce7-126">Además, cualquier instalación nueva de la extensión debe tener la opción de actualización automática de versión secundaria activada.</span><span class="sxs-lookup"><span data-stu-id="48ce7-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="48ce7-127">Habilitación de la extensión</span><span class="sxs-lookup"><span data-stu-id="48ce7-127">Enable the extension</span></span>

<span data-ttu-id="48ce7-128">Puede habilitar esta extensión a través del [Portal de Azure](https://portal.azure.com/#), Azure PowerShell o scripts de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="48ce7-129">Para ver y configurar los datos de rendimiento y el sistema directamente desde Azure Portal, siga [estos pasos del blog de Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="48ce7-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="48ce7-130">En este artículo nos centramos en cómo habilitar y configurar la extensión mediante comandos de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="48ce7-131">De esta forma, podrá leer y ver los datos directamente desde la tabla de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="48ce7-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="48ce7-132">Tenga en cuenta que los métodos de configuración que se describen a continuación no funcionarán en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="48ce7-133">Para ver y configurar los datos de rendimiento y del sistema directamente desde el Portal de Azure, se debe habilitar esta extensión a través de dicho portal.</span><span class="sxs-lookup"><span data-stu-id="48ce7-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48ce7-134">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48ce7-134">Prerequisites</span></span>

* <span data-ttu-id="48ce7-135">**Versión 2.0.6 o posterior del agente Linux de Azure**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="48ce7-136">Tenga en cuenta que la mayoría de las imágenes de la galería de máquina virtual Linux de Azure incluyen la versión 2.0.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="48ce7-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="48ce7-137">Puede ejecutar **WAAgent -version** para confirmar la versión instalada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="48ce7-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="48ce7-138">Si la máquina virtual está ejecutando una versión anterior a la 2.0.6, puede seguir [estas instrucciones de GitHub](https://github.com/Azure/WALinuxAgent "instrucciones") para actualizarla.</span><span class="sxs-lookup"><span data-stu-id="48ce7-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="48ce7-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-139">**Azure CLI**.</span></span> <span data-ttu-id="48ce7-140">Siga [esta guía de instalación de la CLI](../../../cli-install-nodejs.md) para configurar el entorno de la CLI de Azure en su máquina.</span><span class="sxs-lookup"><span data-stu-id="48ce7-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="48ce7-141">Cuando se haya instalado la CLI de Azure, puede usar el comando **azure** desde la interfaz de la línea de comandos (Bash, Terminal o símbolo del sistema) para obtener acceso a los comandos de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="48ce7-142">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48ce7-142">For example:</span></span>

  * <span data-ttu-id="48ce7-143">Ejecute **azure vm extension set --help** para obtener información de ayuda detallada.</span><span class="sxs-lookup"><span data-stu-id="48ce7-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="48ce7-144">Ejecute **azure login** para iniciar sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="48ce7-145">Ejecute **azure vm list** para enumerar todas las máquinas virtuales que tiene en Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="48ce7-146">Una cuenta de almacenamiento para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="48ce7-146">A storage account to store the data.</span></span> <span data-ttu-id="48ce7-147">Necesitará que el nombre de la cuenta de almacenamiento se haya creado anteriormente, además de una clave de acceso para cargar los datos en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="48ce7-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="48ce7-148">Uso del comando de la CLI de Azure para habilitar la extensión de diagnóstico de Linux</span><span class="sxs-lookup"><span data-stu-id="48ce7-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="48ce7-149">Escenario 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-149">Scenario 1.</span></span> <span data-ttu-id="48ce7-150">Habilitación de la extensión con el conjunto de datos predeterminado</span><span class="sxs-lookup"><span data-stu-id="48ce7-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="48ce7-151">En la versión 2.3 o posterior, los datos predeterminados que se recopilarán incluyen la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="48ce7-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="48ce7-152">Todas la información de Rsyslog, incluidos los registros del sistema, seguridad y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48ce7-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="48ce7-153">Un conjunto de datos del sistema base.</span><span class="sxs-lookup"><span data-stu-id="48ce7-153">A core set of basis system data.</span></span> <span data-ttu-id="48ce7-154">Tenga en cuenta que el conjunto de datos completo aparece descrito en el [sitio de soluciones multiplataforma de System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="48ce7-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="48ce7-155">Si desea habilitar más datos, continúe con los pasos que figuran en los escenarios 2 y 3.</span><span class="sxs-lookup"><span data-stu-id="48ce7-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="48ce7-156">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-156">Step 1.</span></span> <span data-ttu-id="48ce7-157">Cree un archivo llamado "PrivateConfig.json" con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="48ce7-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="48ce7-158">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="48ce7-158">Step 2.</span></span> <span data-ttu-id="48ce7-159">Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="48ce7-160">Escenario 2.</span><span class="sxs-lookup"><span data-stu-id="48ce7-160">Scenario 2.</span></span> <span data-ttu-id="48ce7-161">Personalización de las métricas del monitor de rendimiento</span><span class="sxs-lookup"><span data-stu-id="48ce7-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="48ce7-162">En esta sección se describe cómo personalizar la tabla de datos de rendimiento y diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="48ce7-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="48ce7-163">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-163">Step 1.</span></span> <span data-ttu-id="48ce7-164">Cree un archivo denominado "PrivateConfig.json" con el contenido descrito en el escenario 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="48ce7-165">Cree también un archivo llamado "PublicConfig.json".</span><span class="sxs-lookup"><span data-stu-id="48ce7-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="48ce7-166">Especificar los datos concretos que quiere recopilar.</span><span class="sxs-lookup"><span data-stu-id="48ce7-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="48ce7-167">Para ver todos los proveedores y variables que se admiten, visite el [sitio de soluciones multiplataforma de System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="48ce7-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="48ce7-168">Puede tener varias consultas y almacenarlas en varias tablas anexando más consultas al script.</span><span class="sxs-lookup"><span data-stu-id="48ce7-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="48ce7-169">De forma predeterminada, siempre se recopilan los datos de Rsyslog.</span><span class="sxs-lookup"><span data-stu-id="48ce7-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="48ce7-170">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="48ce7-170">Step 2.</span></span> <span data-ttu-id="48ce7-171">Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="48ce7-172">Escenario 3.</span><span class="sxs-lookup"><span data-stu-id="48ce7-172">Scenario 3.</span></span> <span data-ttu-id="48ce7-173">Carga de sus propios archivos de registro</span><span class="sxs-lookup"><span data-stu-id="48ce7-173">Upload your own log files</span></span>

<span data-ttu-id="48ce7-174">En esta sección se describe cómo recopilar y cargar archivos de registro concretos en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="48ce7-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="48ce7-175">Deberá especificar la ruta de acceso al archivo de registro y el nombre de la tabla en la que se almacenará el registro.</span><span class="sxs-lookup"><span data-stu-id="48ce7-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="48ce7-176">Para tener varios archivos de registro puede agregar varias entradas de archivo o tabla al script.</span><span class="sxs-lookup"><span data-stu-id="48ce7-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="48ce7-177">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-177">Step 1.</span></span> <span data-ttu-id="48ce7-178">Cree un archivo denominado "PrivateConfig.json" con el contenido descrito en el escenario 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="48ce7-179">Luego, cree otro archivo llamado "PublicConfig.json" con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="48ce7-179">Then create another file named PublicConfig.json with the following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="48ce7-180">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="48ce7-180">Step 2.</span></span> <span data-ttu-id="48ce7-181">Ejecute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="48ce7-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="48ce7-182">Tenga en cuenta que, con esta configuración de las versiones de extensión anteriores a 2.3, todos los registros que se escriban en `/var/log/mysql.err` también podrían duplicarse en `/var/log/syslog` (o `/var/log/messages` según la distribución de Linux).</span><span class="sxs-lookup"><span data-stu-id="48ce7-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="48ce7-183">Si desea evitar este registro duplicado, puede excluir el registro de los registros de instalación `local6` en la configuración de rsyslog.</span><span class="sxs-lookup"><span data-stu-id="48ce7-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="48ce7-184">Depende de la distribución de Linux pero en un sistema Ubuntu 14.04 el archivo que se debe modificar es `/etc/rsyslog.d/50-default.conf` y puede reemplazar la línea `*.*;auth,authpriv.none -/var/log/syslog` por `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="48ce7-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="48ce7-185">Este problema se ha corregido en la versión de revisión de 2.3 (2.3.9007) más reciente, de modo que si tiene la versión de extensión 2.3, no debería producirse más.</span><span class="sxs-lookup"><span data-stu-id="48ce7-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="48ce7-186">Si sigue produciéndose incluso después de reiniciar la máquina virtual, póngase en contacto con nosotros y ayúdenos a averiguar por qué la versión de revisión más reciente no se ha instalado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="48ce7-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="48ce7-187">Escenario 4.</span><span class="sxs-lookup"><span data-stu-id="48ce7-187">Scenario 4.</span></span> <span data-ttu-id="48ce7-188">Detención del proceso de recopilación de registros por parte de la extensión</span><span class="sxs-lookup"><span data-stu-id="48ce7-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="48ce7-189">En esta sección se describe cómo hacer que la extensión deje de recopilar registros.</span><span class="sxs-lookup"><span data-stu-id="48ce7-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="48ce7-190">Tenga en cuenta que el proceso del agente de supervisión seguirá activo y en ejecución incluso con esta reconfiguración.</span><span class="sxs-lookup"><span data-stu-id="48ce7-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="48ce7-191">Si desea detener completamente el proceso de agente de supervisión, puede hacerlo deshabilitando la extensión.</span><span class="sxs-lookup"><span data-stu-id="48ce7-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="48ce7-192">El comando para deshabilitar la extensión es `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="48ce7-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="48ce7-193">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-193">Step 1.</span></span> <span data-ttu-id="48ce7-194">Cree un archivo denominado "PrivateConfig.json" con el contenido descrito en el escenario 1.</span><span class="sxs-lookup"><span data-stu-id="48ce7-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="48ce7-195">Cree otro archivo llamado "PublicConfig.json" con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="48ce7-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="48ce7-196">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="48ce7-196">Step 2.</span></span> <span data-ttu-id="48ce7-197">Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="48ce7-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="48ce7-198">Revisión de los datos</span><span class="sxs-lookup"><span data-stu-id="48ce7-198">Review your data</span></span>

<span data-ttu-id="48ce7-199">Los datos de diagnóstico y rendimiento y se almacenan en una tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="48ce7-200">Consulte [Uso del Almacenamiento de tablas de Azure con Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) para obtener información sobre cómo acceder a los datos de la tabla de almacenamiento utilizando scripts de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="48ce7-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="48ce7-201">Además, puede utilizar las siguientes herramientas de la interfaz de usuario para tener acceso a los datos:</span><span class="sxs-lookup"><span data-stu-id="48ce7-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="48ce7-202">Explorador de servidores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48ce7-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="48ce7-203">Vaya a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="48ce7-203">Go to your storage account.</span></span> <span data-ttu-id="48ce7-204">Cuando la máquina virtual se ejecute aproximadamente durante 5 minutos, debe ver las cuatro tablas predeterminadas: "LinuxCpu", "LinuxDisk", "LinuxMemory" y "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="48ce7-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="48ce7-205">Haga doble clic en el nombre de la tabla para ver los datos.</span><span class="sxs-lookup"><span data-stu-id="48ce7-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="48ce7-206">[Explorador de almacenamiento de Azure](https://azurestorageexplorer.codeplex.com/ "Explorador de almacenamiento de Azure").</span><span class="sxs-lookup"><span data-stu-id="48ce7-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![imagen](./media/diagnostic-extension/no1.png)

<span data-ttu-id="48ce7-208">Si ha habilitado el archivo fileCfg o perfCfg (tal y como se describe en los escenarios 2 y 3), podrá utilizar el Explorador de servidores de Visual Studio y el Explorador de almacenamiento de Azure para ver los datos no predeterminados.</span><span class="sxs-lookup"><span data-stu-id="48ce7-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="48ce7-209">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="48ce7-209">Known issues</span></span>

* <span data-ttu-id="48ce7-210">Solo puede accederse a la información de Rsyslog y el archivo de registro del cliente especificado a través de scripts.</span><span class="sxs-lookup"><span data-stu-id="48ce7-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>