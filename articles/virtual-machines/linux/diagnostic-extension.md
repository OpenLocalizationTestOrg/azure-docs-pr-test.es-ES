---
title: "Azure Compute: extensión Diagnostics de Linux | Microsoft Docs"
description: "Instrucciones de configuración de la extensión Diagnostics de Linux (LAD) de Azure para recopilar métricas y registrar eventos de máquinas virtuales Linux que se ejecuten en Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="4ff79-103">Uso de la extensión Diagnostics de Linux para supervisar métricas y registros</span><span class="sxs-lookup"><span data-stu-id="4ff79-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="4ff79-104">En este documento se describen las versiones 3.0 y posteriores de la extensión Diagnostics de Linux.</span><span class="sxs-lookup"><span data-stu-id="4ff79-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ff79-105">Para obtener información sobre las versiones 2.3 y anteriores, consulte [este documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="4ff79-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="4ff79-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="4ff79-106">Introduction</span></span>

<span data-ttu-id="4ff79-107">La extensión Diagnostics de Linux ayuda a los usuarios a supervisar el mantenimiento de máquinas virtuales Linux que se ejecuten en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="4ff79-108">Ofrece la siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="4ff79-108">It has the following capabilities:</span></span>

* <span data-ttu-id="4ff79-109">Recopila métricas de rendimiento del sistema de la máquina virtual y las almacena en una tabla específica de una cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="4ff79-110">Recupera eventos de registro de syslog y los almacena en una tabla específica de la cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="4ff79-111">Permite a los usuarios personalizar las métricas de datos que se recopilan y se cargan.</span><span class="sxs-lookup"><span data-stu-id="4ff79-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="4ff79-112">Permite a los usuarios personalizar las utilidades de syslog y los niveles de gravedad de los eventos que se recopilan y se cargan.</span><span class="sxs-lookup"><span data-stu-id="4ff79-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="4ff79-113">Permite a los usuarios cargar los archivos de registro especificados en la tabla de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="4ff79-114">Admite el envío de métricas y eventos de registro a puntos de conexión arbitrarios de EventHub y blobs con formato JSON en la cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="4ff79-115">Esta extensión funciona con los dos modelos de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="4ff79-116">Instalación de la extensión en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4ff79-116">Installing the extension in your VM</span></span>

<span data-ttu-id="4ff79-117">Puede habilitar esta extensión mediante cmdlets de Azure PowerShell, scripts de CLI de Azure o plantillas de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="4ff79-118">Para obtener más información, consulte [Funciones de la extensión](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="4ff79-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="4ff79-119">No se puede usar Azure portal para habilitar LAD 3.0 ni configurarlo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="4ff79-120">En su lugar, instala versión 2.3 y la configura.</span><span class="sxs-lookup"><span data-stu-id="4ff79-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="4ff79-121">Los grafos y las alertas de Azure Portal funcionan con datos procedentes de ambas versiones de la extensión.</span><span class="sxs-lookup"><span data-stu-id="4ff79-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="4ff79-122">Mediante estas instrucciones de instalación y una [configuración de ejemplo descargable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) se configura LAD 3.0 para:</span><span class="sxs-lookup"><span data-stu-id="4ff79-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="4ff79-123">capturar las mismas métricas que las proporcionadas por LAD 2.3 y almacenarlas,</span><span class="sxs-lookup"><span data-stu-id="4ff79-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="4ff79-124">capturar un conjunto útil de métricas del sistema de archivos (función nueva de LAD 3.0),</span><span class="sxs-lookup"><span data-stu-id="4ff79-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="4ff79-125">capturar la recopilación predeterminada de syslog habilitada por LAD 2.3, y</span><span class="sxs-lookup"><span data-stu-id="4ff79-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="4ff79-126">habilitar la experiencia de Azure Portal para la creación de gráficos y desencadenamiento de alertas en métricas de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4ff79-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="4ff79-127">La configuración que se puede descargar es solo un ejemplo; modifíquela como corresponda para adaptarla a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="4ff79-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4ff79-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ff79-128">Prerequisites</span></span>

* <span data-ttu-id="4ff79-129">**Versión 2.2.0 o posterior del agente Linux de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ff79-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="4ff79-130">La mayoría de las imágenes de la galería de máquina virtual Linux de Azure incluyen la versión 2.2.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4ff79-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="4ff79-131">Ejecute `/usr/sbin/waagent -version` para confirmar la versión instalada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ff79-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="4ff79-132">Si la máquina virtual está ejecutando una versión anterior del agente invitado, siga [estas instrucciones](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) para actualizarla.</span><span class="sxs-lookup"><span data-stu-id="4ff79-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="4ff79-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="4ff79-133">**Azure CLI**.</span></span> <span data-ttu-id="4ff79-134">[Instale el entorno de CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) en la máquina.</span><span class="sxs-lookup"><span data-stu-id="4ff79-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="4ff79-135">El comando wget, si aún no lo tiene: ejecute `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="4ff79-136">Una suscripción a Azure existente con una cuenta de almacenamiento para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="4ff79-137">Instalación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4ff79-137">Sample installation</span></span>

<span data-ttu-id="4ff79-138">Rellene las tres primeras líneas con los parámetros correctos y, a continuación, ejecute este script a modo de raíz:</span><span class="sxs-lookup"><span data-stu-id="4ff79-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="4ff79-139">La URL de la configuración de muestreo y su contenido están sujetos a cambios.</span><span class="sxs-lookup"><span data-stu-id="4ff79-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="4ff79-140">Descargue una copia del archivo JSON de configuración del portal y personalícelo en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="4ff79-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="4ff79-141">Cualquier plantilla o automatización que genere deberían usar su propia copia en lugar de descargar dicha URL cada vez.</span><span class="sxs-lookup"><span data-stu-id="4ff79-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="4ff79-142">Actualización de la configuración de la extensión</span><span class="sxs-lookup"><span data-stu-id="4ff79-142">Updating the extension settings</span></span>

<span data-ttu-id="4ff79-143">Después de cambiar la Configuración pública o protegida, ejecute el mismo comando para implementarla en la VM.</span><span class="sxs-lookup"><span data-stu-id="4ff79-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="4ff79-144">Si se ha realizado cualquier modificación en la configuración, la configuración actualizada se envía a la extensión.</span><span class="sxs-lookup"><span data-stu-id="4ff79-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="4ff79-145">LAD recarga la configuración y se reinicia automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="4ff79-146">Migración desde versiones anteriores de la extensión</span><span class="sxs-lookup"><span data-stu-id="4ff79-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="4ff79-147">La versión más reciente de la extensión es la **3.0**.</span><span class="sxs-lookup"><span data-stu-id="4ff79-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="4ff79-148">**Todas las versiones anteriores (2.x) están en desuso y pueden retirarse a partir del 31 de julio de 2018**.</span><span class="sxs-lookup"><span data-stu-id="4ff79-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ff79-149">En esta extensión se introducen importantes cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="4ff79-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="4ff79-150">La finalidad de uno de estos cambios era aumentar la seguridad de la extensión; por tanto, no se pudo conservar la compatibilidad con las versiones 2.x anteriores.</span><span class="sxs-lookup"><span data-stu-id="4ff79-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="4ff79-151">Además, el publicador de esta extensión es diferente del de las versiones 2.x.</span><span class="sxs-lookup"><span data-stu-id="4ff79-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="4ff79-152">Para migrar a esta nueva versión de la extensión desde versiones 2.x, debe desinstalar la antigua (con el nombre de publicador anterior) y, a continuación, instalar la versión 3.</span><span class="sxs-lookup"><span data-stu-id="4ff79-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="4ff79-153">Recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4ff79-153">Recommendations:</span></span>

* <span data-ttu-id="4ff79-154">Instale la extensión con la actualización de versión secundaria automática habilitada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="4ff79-155">En máquinas virtuales con el modelo de implementación clásica, especifique "3.*" como versión si va a instalar la extensión mediante la CLI xPLAT de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ff79-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="4ff79-156">En las máquinas virtuales del modelo de implementación de Azure Resource Manager, incluya ""autoUpgradeMinorVersion": true" en la plantilla de implementación de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ff79-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="4ff79-157">Use una cuenta de almacenamiento nueva o diferente para LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="4ff79-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="4ff79-158">Hay varias pequeñas incompatibilidades entre LAD 2.3 y LAD 3.0 que hacen que compartir una cuenta sea problemático:</span><span class="sxs-lookup"><span data-stu-id="4ff79-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="4ff79-159">LAD 3.0 almacena los eventos de syslog en una tabla con un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="4ff79-160">Las cadenas de counterSpecifier para las métricas de `builtin` son diferentes en LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="4ff79-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="4ff79-161">Configuración protegida</span><span class="sxs-lookup"><span data-stu-id="4ff79-161">Protected settings</span></span>

<span data-ttu-id="4ff79-162">Este conjunto de información de configuración contiene información confidencial que debería protegerse de la vista pública, por ejemplo, las credenciales de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4ff79-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="4ff79-163">Esta configuración se transmite la extensión y es almacenada por esta de forma cifrada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="4ff79-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="4ff79-164">Name</span></span> | <span data-ttu-id="4ff79-165">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-165">Value</span></span>
---- | -----
<span data-ttu-id="4ff79-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="4ff79-166">storageAccountName</span></span> | <span data-ttu-id="4ff79-167">Es el nombre de la cuenta de almacenamiento en la que la extensión escribe los datos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="4ff79-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="4ff79-168">storageAccountEndPoint</span></span> | <span data-ttu-id="4ff79-169">(Opcional) es el punto de conexión que identifica la nube en la que existe la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4ff79-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="4ff79-170">Si no hubiera configuración, LAD selecciona la nube pública de Azure (`https://core.windows.net`) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4ff79-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="4ff79-171">Para usar una cuenta de almacenamiento en Azure Alemania, Azure Government o Azure China, establezca este valor como corresponda.</span><span class="sxs-lookup"><span data-stu-id="4ff79-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="4ff79-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="4ff79-172">storageAccountSasToken</span></span> | <span data-ttu-id="4ff79-173">Es un [token de SAS de cuenta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para blob services y table services (`ss='bt'`) aplicable a contenedores y objetos (`srt='co'`), que otorga permisos, los crea, los enumera, los actualiza y los escribe (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="4ff79-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="4ff79-174">*No* incluya el signo de interrogación principal (?).</span><span class="sxs-lookup"><span data-stu-id="4ff79-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="4ff79-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="4ff79-175">mdsdHttpProxy</span></span> | <span data-ttu-id="4ff79-176">(Opcional) es información del proxy HTTP necesaria para habilitar la extensión para conectarse a la cuenta de almacenamiento y el punto de conexión especificados.</span><span class="sxs-lookup"><span data-stu-id="4ff79-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="4ff79-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="4ff79-177">sinksConfig</span></span> | <span data-ttu-id="4ff79-178">(Opcional) es información sobre destinos alternativos a los que pueden enviarse métricas y eventos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="4ff79-179">La información específica de cada receptor de datos admitido por la extensión se trata en las siguientes secciones.</span><span class="sxs-lookup"><span data-stu-id="4ff79-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="4ff79-180">Es posible construir el token de SAS necesario de forma muy sencilla mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4ff79-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="4ff79-181">Seleccione la cuenta de almacenamiento de uso general en la que quiere que escriba la extensión.</span><span class="sxs-lookup"><span data-stu-id="4ff79-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="4ff79-182">Seleccione "Firma de acceso compartido" de la sección Configuración del menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="4ff79-183">Cree las secciones pertinentes, conforme a lo descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="4ff79-184">Haga clic en el botón "Generar SAS".</span><span class="sxs-lookup"><span data-stu-id="4ff79-184">Click the "Generate SAS" button.</span></span>

![imagen](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="4ff79-186">Copie la SAS generada en el campo storageAccountSasToken. Elimine el signo de interrogación principal ("?").</span><span class="sxs-lookup"><span data-stu-id="4ff79-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="4ff79-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="4ff79-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="4ff79-188">En esta sección opcional se definen destinos adicionales a los que la extensión envía la información que recopila.</span><span class="sxs-lookup"><span data-stu-id="4ff79-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="4ff79-189">La matriz "sink" contiene un objeto para cada receptor de datos adicional.</span><span class="sxs-lookup"><span data-stu-id="4ff79-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="4ff79-190">El atributo "type" determina los demás atributos del objeto.</span><span class="sxs-lookup"><span data-stu-id="4ff79-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="4ff79-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-191">Element</span></span> | <span data-ttu-id="4ff79-192">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-192">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-193">name</span><span class="sxs-lookup"><span data-stu-id="4ff79-193">name</span></span> | <span data-ttu-id="4ff79-194">Una cadena usada para hacer referencia a este receptor en cualquier otra parte de la configuración de la extensión.</span><span class="sxs-lookup"><span data-stu-id="4ff79-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="4ff79-195">type</span><span class="sxs-lookup"><span data-stu-id="4ff79-195">type</span></span> | <span data-ttu-id="4ff79-196">Es el tipo de receptor que se va a definir.</span><span class="sxs-lookup"><span data-stu-id="4ff79-196">The type of sink being defined.</span></span> <span data-ttu-id="4ff79-197">Determina los demás valores (si los hubiera) en instancias de este tipo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="4ff79-198">La versión 3.0 de la extensión Diagnostics de Linux admite dos tipos de receptores: de EventHub y Json BLOB.</span><span class="sxs-lookup"><span data-stu-id="4ff79-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="4ff79-199">El receptor de EventHub</span><span class="sxs-lookup"><span data-stu-id="4ff79-199">The EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="4ff79-200">La entrada "sasURL" contiene la URL completa, incluido el token SAS, para la instancia de EventHub en la que deberían publicarse los datos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="4ff79-201">LAD necesita una directiva de denominación de SAS que habilite la notificación Send.</span><span class="sxs-lookup"><span data-stu-id="4ff79-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="4ff79-202">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4ff79-202">An example:</span></span>

* <span data-ttu-id="4ff79-203">Cree un espacio de nombres de Event Hubs llamado `contosohub`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="4ff79-204">Cree un Event Hub en el espacio de nombres llamado `syslogmsgs`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="4ff79-205">Cree una directiva de acceso compartido en el Event Hub llamada `writer` que habilite la notificación Send.</span><span class="sxs-lookup"><span data-stu-id="4ff79-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="4ff79-206">Si creó una SAS válida hasta la medianoche en horario UTC del 1 de enero de 2018, el valor de sasURL podría ser:</span><span class="sxs-lookup"><span data-stu-id="4ff79-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="4ff79-207">Para obtener más información sobre la generación de tokens de SAS para Event Hubs, consulte [esta página web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ff79-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="4ff79-208">El receptor de Json BLOB</span><span class="sxs-lookup"><span data-stu-id="4ff79-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="4ff79-209">Los datos dirigidos a un receptor de Json BLOB se almacenan en blobs en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ff79-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="4ff79-210">Cada instancia de LAD crea un blob cada hora para cada nombre de receptor.</span><span class="sxs-lookup"><span data-stu-id="4ff79-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="4ff79-211">Todos los blobs siempre contienen una matriz de objeto JSON válida sintácticamente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="4ff79-212">Se agregan nuevas entradas a la matriz automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="4ff79-213">Los blobs se almacenan en un contenedor con el mismo nombre que el receptor.</span><span class="sxs-lookup"><span data-stu-id="4ff79-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="4ff79-214">Las reglas de Azure Storage para los nombres de contenedores de blobs se aplican a los nombres de los receptores de Json BLOB: entre 3 y 63 caracteres alfanuméricos ASCII o guiones.</span><span class="sxs-lookup"><span data-stu-id="4ff79-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="4ff79-215">Configuración pública</span><span class="sxs-lookup"><span data-stu-id="4ff79-215">Public settings</span></span>

<span data-ttu-id="4ff79-216">Esta estructura contiene varios bloques de valores de configuración que controlan la información recopilada por la extensión.</span><span class="sxs-lookup"><span data-stu-id="4ff79-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="4ff79-217">Cada valor de configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="4ff79-217">Each setting is optional.</span></span> <span data-ttu-id="4ff79-218">Si especifica `ladCfg`, también debe especificar `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="4ff79-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-219">Element</span></span> | <span data-ttu-id="4ff79-220">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-220">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="4ff79-221">StorageAccount</span></span> | <span data-ttu-id="4ff79-222">Es el nombre de la cuenta de almacenamiento en la que la extensión escribe los datos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="4ff79-223">Debe ser el mismo nombre que se especifique en la [Configuración protegida](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="4ff79-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="4ff79-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="4ff79-224">mdsdHttpProxy</span></span> | <span data-ttu-id="4ff79-225">(Opcional) es el mismo que en la [Configuración protegida](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="4ff79-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="4ff79-226">El valor público reemplaza al privado, en caso de estar establecido.</span><span class="sxs-lookup"><span data-stu-id="4ff79-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="4ff79-227">Coloque elementos de configuración de proxy que contengan un secreto, como una contraseña, en la [Configuración protegida](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="4ff79-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="4ff79-228">El resto de los elementos se describen con más detalle en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="4ff79-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="4ff79-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="4ff79-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="4ff79-230">Esta estructura opcional controla la recopilación de métricas y registros para enviarlos al servicio de Métricas de Azure y otros receptores de datos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="4ff79-231">Debe especificar `performanceCounters`, `syslogEvents` o ambos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="4ff79-232">Debe especificar la estructura de `metrics`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="4ff79-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-233">Element</span></span> | <span data-ttu-id="4ff79-234">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-234">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="4ff79-235">eventVolume</span></span> | <span data-ttu-id="4ff79-236">(Opcional) controla el número de particiones creadas en la tabla de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4ff79-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="4ff79-237">Debe ser uno de los siguientes valores: `"Large"`, `"Medium"` o `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="4ff79-238">Si no se especifica, el valor predeterminado es `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="4ff79-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="4ff79-239">sampleRateInSeconds</span></span> | <span data-ttu-id="4ff79-240">(Opcional) es el intervalo predeterminado entre la recopilación de métricas sin procesar (sin agregar).</span><span class="sxs-lookup"><span data-stu-id="4ff79-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="4ff79-241">La frecuencia de muestreo más pequeña admitida es de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="4ff79-242">Si no se especifica, el valor predeterminado es `15`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="4ff79-243">Métricas</span><span class="sxs-lookup"><span data-stu-id="4ff79-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="4ff79-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-244">Element</span></span> | <span data-ttu-id="4ff79-245">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-245">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="4ff79-246">resourceId</span></span> | <span data-ttu-id="4ff79-247">El identificador de recurso de Azure Resource Manager de la VM o del conjunto de escalado de máquinas virtuales al que pertenezca la VM.</span><span class="sxs-lookup"><span data-stu-id="4ff79-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="4ff79-248">Esta configuración también debe especificarse en caso de usar cualquier receptor de Json BLOB en la configuración.</span><span class="sxs-lookup"><span data-stu-id="4ff79-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="4ff79-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="4ff79-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="4ff79-250">La frecuencia con la que se computarán métricas agregadas y se transferirán a Métricas de Azure, expresadas en forma de intervalo de tiempo ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="4ff79-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="4ff79-251">El período de transferencia mínimo es de 60 segundos, es decir, PT1M.</span><span class="sxs-lookup"><span data-stu-id="4ff79-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="4ff79-252">Debe especificar al menos un elemento scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="4ff79-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="4ff79-253">Se recopilan muestras de las métricas especificadas en la sección performanceCounters cada 15 segundos o a la frecuencia de muestreo definida para el contador de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="4ff79-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="4ff79-254">Si aparecen varias frecuencias de scheduledTransferPeriod (como en el ejemplo), cada agregación se computa de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="4ff79-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="4ff79-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="4ff79-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="4ff79-256">Esta sección opcional controla la recopilación de métricas.</span><span class="sxs-lookup"><span data-stu-id="4ff79-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="4ff79-257">Se agregan muestras sin procesar para cada elemento [scheduledTransferPeriod](#metrics) a fin de generar estos valores:</span><span class="sxs-lookup"><span data-stu-id="4ff79-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="4ff79-258">mean</span><span class="sxs-lookup"><span data-stu-id="4ff79-258">mean</span></span>
* <span data-ttu-id="4ff79-259">minimum</span><span class="sxs-lookup"><span data-stu-id="4ff79-259">minimum</span></span>
* <span data-ttu-id="4ff79-260">maximum</span><span class="sxs-lookup"><span data-stu-id="4ff79-260">maximum</span></span>
* <span data-ttu-id="4ff79-261">last-collected value</span><span class="sxs-lookup"><span data-stu-id="4ff79-261">last-collected value</span></span>
* <span data-ttu-id="4ff79-262">Número de muestras sin procesar usadas para computar el agregado</span><span class="sxs-lookup"><span data-stu-id="4ff79-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="4ff79-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-263">Element</span></span> | <span data-ttu-id="4ff79-264">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-264">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-265">sinks</span><span class="sxs-lookup"><span data-stu-id="4ff79-265">sinks</span></span> | <span data-ttu-id="4ff79-266">(Opcional) es una lista separada por comas de nombres de receptores a los que LAD envía los resultados de las métricas agregadas.</span><span class="sxs-lookup"><span data-stu-id="4ff79-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="4ff79-267">Todas las métricas agregadas se publican en cada receptor indicado.</span><span class="sxs-lookup"><span data-stu-id="4ff79-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="4ff79-268">Consulte [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="4ff79-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="4ff79-269">Ejemplo: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="4ff79-270">type</span><span class="sxs-lookup"><span data-stu-id="4ff79-270">type</span></span> | <span data-ttu-id="4ff79-271">Identifica el proveedor real de la métrica.</span><span class="sxs-lookup"><span data-stu-id="4ff79-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="4ff79-272">class</span><span class="sxs-lookup"><span data-stu-id="4ff79-272">class</span></span> | <span data-ttu-id="4ff79-273">Junto con "counter", identifica la métrica específica en el espacio de nombres del proveedor.</span><span class="sxs-lookup"><span data-stu-id="4ff79-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="4ff79-274">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-274">counter</span></span> | <span data-ttu-id="4ff79-275">Junto con "class", identifica la métrica específica en el espacio de nombres del proveedor.</span><span class="sxs-lookup"><span data-stu-id="4ff79-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="4ff79-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="4ff79-276">counterSpecifier</span></span> | <span data-ttu-id="4ff79-277">Identifica la métrica específica en el espacio de nombres de Métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="4ff79-278">condition</span><span class="sxs-lookup"><span data-stu-id="4ff79-278">condition</span></span> | <span data-ttu-id="4ff79-279">(Opcional) selecciona una instancia específica del objeto al que se aplica la métrica o selecciona la agregación en todas las instancias de este objeto.</span><span class="sxs-lookup"><span data-stu-id="4ff79-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="4ff79-280">Para obtener más información, consulte las [definiciones de las métricas](#metrics-supported-by-builtin) de `builtin`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="4ff79-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="4ff79-281">sampleRate</span></span> | <span data-ttu-id="4ff79-282">Intervalo de ISO 8601 que establece la frecuencia de recopilación de muestras sin procesar de esta métrica.</span><span class="sxs-lookup"><span data-stu-id="4ff79-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="4ff79-283">Si no se establece, el intervalo de recopilación se establece a partir del valor de [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="4ff79-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="4ff79-284">La frecuencia de muestreo más corta admitida es de 15 segundos (PT15S).</span><span class="sxs-lookup"><span data-stu-id="4ff79-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="4ff79-285">unit</span><span class="sxs-lookup"><span data-stu-id="4ff79-285">unit</span></span> | <span data-ttu-id="4ff79-286">Debería ser una de estas cadenas: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond" o "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="4ff79-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="4ff79-287">Define la unidad para la métrica.</span><span class="sxs-lookup"><span data-stu-id="4ff79-287">Defines the unit for the metric.</span></span> <span data-ttu-id="4ff79-288">Los consumidores de los datos recopilados esperan que los valores de los datos recopilados coincidan con esta unidad.</span><span class="sxs-lookup"><span data-stu-id="4ff79-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="4ff79-289">LAD omite este campo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-289">LAD ignores this field.</span></span>
<span data-ttu-id="4ff79-290">DisplayName</span><span class="sxs-lookup"><span data-stu-id="4ff79-290">displayName</span></span> | <span data-ttu-id="4ff79-291">La etiqueta (en el idioma especificado por la configuración regional correspondiente) que va a adjuntarse a estos datos en el servicio de Métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="4ff79-292">LAD omite este campo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-292">LAD ignores this field.</span></span>

<span data-ttu-id="4ff79-293">El elemento counterSpecifier es un identificador arbitrario.</span><span class="sxs-lookup"><span data-stu-id="4ff79-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="4ff79-294">Los consumidores de métricas, como la característica de creación de grafos y desencadenamiento alertas de Azure Portal, usan counterSpecifier como "clave" para identificar una métrica o instancia de una métrica.</span><span class="sxs-lookup"><span data-stu-id="4ff79-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="4ff79-295">Para las métricas de `builtin`, se recomienda usar valores counterSpecifier que empiecen por `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="4ff79-296">Si va a recopilar una instancia específica de una métrica, se recomienda adjuntar el identificador de la instancia al valor de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="4ff79-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="4ff79-297">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="4ff79-297">Some examples:</span></span>

* <span data-ttu-id="4ff79-298">`/builtin/Processor/PercentIdleTime`: tiempo de inactividad promediado en todos los núcleos</span><span class="sxs-lookup"><span data-stu-id="4ff79-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="4ff79-299">`/builtin/Disk/FreeSpace(/mnt)`: espacio libre para el elemento /mnt filesystem</span><span class="sxs-lookup"><span data-stu-id="4ff79-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="4ff79-300">`/builtin/Disk/FreeSpace`: espacio libre promediado entre todos los elementos filesystem montados</span><span class="sxs-lookup"><span data-stu-id="4ff79-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="4ff79-301">Ni LAD ni Azure Portal esperan que el valor de counterSpecifier concuerde con ningún patrón.</span><span class="sxs-lookup"><span data-stu-id="4ff79-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="4ff79-302">Sea coherente en el modo de construcción de valores counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="4ff79-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="4ff79-303">Si especifica `performanceCounters`, LAD siempre escribe datos en una tabla en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ff79-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="4ff79-304">Puede hacer que se escriban los mismos datos a blobs JSON o Event Hubs, pero no puede deshabilitar el almacenamiento de datos en una tabla.</span><span class="sxs-lookup"><span data-stu-id="4ff79-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="4ff79-305">Todas las instancias de la extensión de diagnóstico configuradas para usar el mismo nombre de cuenta de almacenamiento y el mismo punto de conexión agregan sus métricas y registros a la misma tabla.</span><span class="sxs-lookup"><span data-stu-id="4ff79-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="4ff79-306">Si hay demasiadas máquinas virtuales escribiendo en la misma partición de tabla, Azure puede limitar las escrituras a dicha partición.</span><span class="sxs-lookup"><span data-stu-id="4ff79-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="4ff79-307">El valor eventVolume hace que las entradas se repartan entre 1 (Small), 10 (Medium) o 100 (Large) particiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="4ff79-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="4ff79-308">Por lo general, un valor "Medium" es suficiente para asegurarse de que el tráfico no se vea limitado.</span><span class="sxs-lookup"><span data-stu-id="4ff79-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="4ff79-309">La característica de las métricas de Azure de Azure Portal usa los datos de esta tabla para crear gráficos o desencadenar alertas.</span><span class="sxs-lookup"><span data-stu-id="4ff79-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="4ff79-310">El nombre de tabla es la concatenación de las siguientes cadenas:</span><span class="sxs-lookup"><span data-stu-id="4ff79-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="4ff79-311">El elemento "scheduledTransferPeriod" para los valores agregados almacenados en la tabla</span><span class="sxs-lookup"><span data-stu-id="4ff79-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="4ff79-312">Una fecha en formato "AAAAMMDD", que cambia cada 10 días</span><span class="sxs-lookup"><span data-stu-id="4ff79-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="4ff79-313">Algunos ejemplos son `WADMetricsPT1HP10DV2S20170410` y `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="4ff79-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="4ff79-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="4ff79-315">Esta sección opcional controla la recopilación de eventos de registro de syslog.</span><span class="sxs-lookup"><span data-stu-id="4ff79-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="4ff79-316">Si se omite la sección, no se captura ningún evento de syslog.</span><span class="sxs-lookup"><span data-stu-id="4ff79-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="4ff79-317">La recopilación de syslogEventConfiguration tiene una entrada para cada recurso de syslog de interés.</span><span class="sxs-lookup"><span data-stu-id="4ff79-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="4ff79-318">Si el valor de minSeverity es "NONE" para un recurso en particular, o si el recurso no aparece en el elemento, no se captura ningún evento de dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="4ff79-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="4ff79-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-319">Element</span></span> | <span data-ttu-id="4ff79-320">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-320">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-321">sinks</span><span class="sxs-lookup"><span data-stu-id="4ff79-321">sinks</span></span> | <span data-ttu-id="4ff79-322">Es una lista separada por comas de nombres de receptores en los que se publican los eventos de registros individuales.</span><span class="sxs-lookup"><span data-stu-id="4ff79-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="4ff79-323">Todos los eventos de registro que coincidan con las restricciones de syslogEventConfiguration se publican en cada receptor indicado.</span><span class="sxs-lookup"><span data-stu-id="4ff79-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="4ff79-324">Por ejemplo, "EHforsyslog".</span><span class="sxs-lookup"><span data-stu-id="4ff79-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="4ff79-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="4ff79-325">facilityName</span></span> | <span data-ttu-id="4ff79-326">Es un nombre de recurso de syslog (como "LOG\_USER" o "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="4ff79-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="4ff79-327">Consulte la sección "facility" de la [página man de syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obtener la lista completa.</span><span class="sxs-lookup"><span data-stu-id="4ff79-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="4ff79-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="4ff79-328">minSeverity</span></span> | <span data-ttu-id="4ff79-329">Es un nivel de gravedad de syslog (como "LOG\_ERR" o "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="4ff79-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="4ff79-330">Consulte la sección "level" de la [página man de syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obtener la lista completa.</span><span class="sxs-lookup"><span data-stu-id="4ff79-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="4ff79-331">La extensión captura eventos enviados al recurso al nivel especificado o uno superior.</span><span class="sxs-lookup"><span data-stu-id="4ff79-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="4ff79-332">Si especifica `syslogEvents`, LAD siempre escribe datos en una tabla en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ff79-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="4ff79-333">Puede hacer que se escriban los mismos datos a blobs JSON o Event Hubs, pero no puede deshabilitar el almacenamiento de datos en una tabla.</span><span class="sxs-lookup"><span data-stu-id="4ff79-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="4ff79-334">El compartimiento de la creación de particiones para esta tabla es el mismo descrito para `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="4ff79-335">El nombre de tabla es la concatenación de las siguientes cadenas:</span><span class="sxs-lookup"><span data-stu-id="4ff79-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="4ff79-336">Una fecha en formato "AAAAMMDD", que cambia cada 10 días</span><span class="sxs-lookup"><span data-stu-id="4ff79-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="4ff79-337">Algunos ejemplos son `LinuxSyslog20170410` y `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="4ff79-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="4ff79-338">perfCfg</span></span>

<span data-ttu-id="4ff79-339">Esta sección opcional controla la exclusión de consultas [OMI](https://github.com/Microsoft/omi) arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="4ff79-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="4ff79-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-340">Element</span></span> | <span data-ttu-id="4ff79-341">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-341">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-342">espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="4ff79-342">namespace</span></span> | <span data-ttu-id="4ff79-343">(Opcional) es el espacio de nombres OMI en el que la consulta debería ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4ff79-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="4ff79-344">Si no se especifica, el valor predeterminado es "root/scx", implementado por los [proveedores multiplataforma de System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="4ff79-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="4ff79-345">query</span><span class="sxs-lookup"><span data-stu-id="4ff79-345">query</span></span> | <span data-ttu-id="4ff79-346">Es la consulta de OMI que va a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4ff79-346">The OMI query to be executed.</span></span>
<span data-ttu-id="4ff79-347">table</span><span class="sxs-lookup"><span data-stu-id="4ff79-347">table</span></span> | <span data-ttu-id="4ff79-348">(Opcional) es la tabla de almacenamiento de Azure, en la cuenta de almacenamiento designada (consulte [Configuración protegida](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="4ff79-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="4ff79-349">frequency</span><span class="sxs-lookup"><span data-stu-id="4ff79-349">frequency</span></span> | <span data-ttu-id="4ff79-350">(Opcional) es el número de segundos entre la ejecución de la consulta.</span><span class="sxs-lookup"><span data-stu-id="4ff79-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="4ff79-351">El valor predeterminado es de 300 (5 minutos) y el mínimo es de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="4ff79-352">sinks</span><span class="sxs-lookup"><span data-stu-id="4ff79-352">sinks</span></span> | <span data-ttu-id="4ff79-353">(Opcional) es una lista separada por comas de nombres de receptores adicionales en los que deberían publicarse los resultados de las métricas de muestra sin procesar.</span><span class="sxs-lookup"><span data-stu-id="4ff79-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="4ff79-354">Ni la extensión ni Métricas de Azure computan ninguna agregación de estos ejemplos sin procesar.</span><span class="sxs-lookup"><span data-stu-id="4ff79-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="4ff79-355">Deben especificarse "table", "sinks" o ambos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="4ff79-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="4ff79-356">fileLogs</span></span>

<span data-ttu-id="4ff79-357">Controla la captura de los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="4ff79-357">Controls the capture of log files.</span></span> <span data-ttu-id="4ff79-358">LAD captura nuevas líneas de texto a medida que se escriben en el archivo y las escribe en filas de tabla o en cualquier receptor especificado (de JsonBlob o EventHub).</span><span class="sxs-lookup"><span data-stu-id="4ff79-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="4ff79-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="4ff79-359">Element</span></span> | <span data-ttu-id="4ff79-360">Valor</span><span class="sxs-lookup"><span data-stu-id="4ff79-360">Value</span></span>
------- | -----
<span data-ttu-id="4ff79-361">file</span><span class="sxs-lookup"><span data-stu-id="4ff79-361">file</span></span> | <span data-ttu-id="4ff79-362">Es la ruta de acceso completa del archivo de registro que va a inspeccionarse y capturarse.</span><span class="sxs-lookup"><span data-stu-id="4ff79-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="4ff79-363">La ruta de acceso debe denominar un único archivo. No puede denominar un directorio ni contener caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="4ff79-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="4ff79-364">table</span><span class="sxs-lookup"><span data-stu-id="4ff79-364">table</span></span> | <span data-ttu-id="4ff79-365">(Opcional) es la tabla de Azure Storage en la cuenta de almacenamiento designada (especificada en la configuración protegida) en la que se escriben nuevas líneas de la "cola" del archivo.</span><span class="sxs-lookup"><span data-stu-id="4ff79-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="4ff79-366">sinks</span><span class="sxs-lookup"><span data-stu-id="4ff79-366">sinks</span></span> | <span data-ttu-id="4ff79-367">(Opcional) es una lista separada por combas de nombres de receptores adicionales a la que se envían líneas de registro.</span><span class="sxs-lookup"><span data-stu-id="4ff79-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="4ff79-368">Deben especificarse "table", "sinks" o ambos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="4ff79-369">Métricas admitidas por el proveedor de builtin</span><span class="sxs-lookup"><span data-stu-id="4ff79-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="4ff79-370">El proveedor de métricas builtin es una fuente de métricas del máximo interés para una gran cantidad de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4ff79-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="4ff79-371">Estas métricas se dividen en cinco clases amplias:</span><span class="sxs-lookup"><span data-stu-id="4ff79-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="4ff79-372">Procesador</span><span class="sxs-lookup"><span data-stu-id="4ff79-372">Processor</span></span>
* <span data-ttu-id="4ff79-373">Memoria</span><span class="sxs-lookup"><span data-stu-id="4ff79-373">Memory</span></span>
* <span data-ttu-id="4ff79-374">Red</span><span class="sxs-lookup"><span data-stu-id="4ff79-374">Network</span></span>
* <span data-ttu-id="4ff79-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="4ff79-375">Filesystem</span></span>
* <span data-ttu-id="4ff79-376">Disco</span><span class="sxs-lookup"><span data-stu-id="4ff79-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="4ff79-377">Métricas builtin para la clase Processor</span><span class="sxs-lookup"><span data-stu-id="4ff79-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="4ff79-378">La clase de métricas Processor proporciona información sobre el uso del procesador en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ff79-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="4ff79-379">Al agregar porcentajes, el resultado es el promedio de todas las CPU.</span><span class="sxs-lookup"><span data-stu-id="4ff79-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="4ff79-380">En una máquina virtual de dos núcleos, si uno de ellos estaba activo al 100 % y el otro, inactivo al 100 %, el valor de PercentIdleTime sería de 50.</span><span class="sxs-lookup"><span data-stu-id="4ff79-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="4ff79-381">Si la actividad de cada núcleo era del 50 % durante el mismo período, el resultado indicado sería de 50.</span><span class="sxs-lookup"><span data-stu-id="4ff79-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="4ff79-382">En una máquina virtual de cuatro núcleos, si uno de ellos estaba activo al 100 % y todos los demás, inactivos, el valor de PercentIdleTime sería de 75.</span><span class="sxs-lookup"><span data-stu-id="4ff79-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="4ff79-383">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-383">counter</span></span> | <span data-ttu-id="4ff79-384">Significado</span><span class="sxs-lookup"><span data-stu-id="4ff79-384">Meaning</span></span>
------- | -------
<span data-ttu-id="4ff79-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-385">PercentIdleTime</span></span> | <span data-ttu-id="4ff79-386">Porcentaje de tiempo del período de agregación durante el que los procesadores ejecutaban el bucle de inactividad del kernel</span><span class="sxs-lookup"><span data-stu-id="4ff79-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="4ff79-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-387">PercentProcessorTime</span></span> | <span data-ttu-id="4ff79-388">Porcentaje de tiempo de ejecución de un subproceso no inactivo</span><span class="sxs-lookup"><span data-stu-id="4ff79-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="4ff79-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-389">PercentIOWaitTime</span></span> | <span data-ttu-id="4ff79-390">Porcentaje de tiempo de espera para la finalización de operaciones de E/S</span><span class="sxs-lookup"><span data-stu-id="4ff79-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="4ff79-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-391">PercentInterruptTime</span></span> | <span data-ttu-id="4ff79-392">Porcentaje de tiempo de ejecución de interrupciones de hardware o software y DPC (llamadas a procedimiento aplazadas)</span><span class="sxs-lookup"><span data-stu-id="4ff79-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="4ff79-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-393">PercentUserTime</span></span> | <span data-ttu-id="4ff79-394">Del tiempo no inactivo durante el período de agregación, el porcentaje empleado en modo de usuario en prioridad normal</span><span class="sxs-lookup"><span data-stu-id="4ff79-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="4ff79-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-395">PercentNiceTime</span></span> | <span data-ttu-id="4ff79-396">Del tiempo no inactivo, el porcentaje empleado en prioridad disminuida (nice)</span><span class="sxs-lookup"><span data-stu-id="4ff79-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="4ff79-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="4ff79-398">Del tiempo no inactivo, el porcentaje empleado en modo privilegiado (kernel)</span><span class="sxs-lookup"><span data-stu-id="4ff79-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="4ff79-399">Los cuatro primeros contadores deberían sumar un 100 %.</span><span class="sxs-lookup"><span data-stu-id="4ff79-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="4ff79-400">Los tres últimos contadores también suman 100 %. Subdividen la suma de PercentProcessorTime, PercentIOWaitTime y PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="4ff79-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="4ff79-401">Para obtener un único agregado de métricas de todos los procesadores, establezca `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="4ff79-402">Para obtener una métrica para un procesador específico, como el segundo procesador lógico de una máquina virtual de cuatro núcleos, establezca `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="4ff79-403">Los números de procesador lógico se encuentran en el rango `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="4ff79-404">Métricas builtin para la clase Memory</span><span class="sxs-lookup"><span data-stu-id="4ff79-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="4ff79-405">La clase de métricas Memory proporciona información sobre utilización, paginación e intercambio de memoria.</span><span class="sxs-lookup"><span data-stu-id="4ff79-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="4ff79-406">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-406">counter</span></span> | <span data-ttu-id="4ff79-407">Significado</span><span class="sxs-lookup"><span data-stu-id="4ff79-407">Meaning</span></span>
------- | -------
<span data-ttu-id="4ff79-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4ff79-408">AvailableMemory</span></span> | <span data-ttu-id="4ff79-409">Memoria física disponible en MiB</span><span class="sxs-lookup"><span data-stu-id="4ff79-409">Available physical memory in MiB</span></span>
<span data-ttu-id="4ff79-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4ff79-410">PercentAvailableMemory</span></span> | <span data-ttu-id="4ff79-411">Memoria física disponible en forma de porcentaje del total de memoria</span><span class="sxs-lookup"><span data-stu-id="4ff79-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="4ff79-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="4ff79-412">UsedMemory</span></span> | <span data-ttu-id="4ff79-413">Memoria física en uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="4ff79-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="4ff79-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="4ff79-414">PercentUsedMemory</span></span> | <span data-ttu-id="4ff79-415">Memoria física en uso en forma de porcentaje del total de memoria</span><span class="sxs-lookup"><span data-stu-id="4ff79-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="4ff79-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="4ff79-416">PagesPerSec</span></span> | <span data-ttu-id="4ff79-417">Paginación total (lectura y escritura)</span><span class="sxs-lookup"><span data-stu-id="4ff79-417">Total paging (read/write)</span></span>
<span data-ttu-id="4ff79-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="4ff79-418">PagesReadPerSec</span></span> | <span data-ttu-id="4ff79-419">Páginas leídas desde la memoria auxiliar (archivo de intercambio, archivo de programa, archivo asignado, etc.)</span><span class="sxs-lookup"><span data-stu-id="4ff79-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="4ff79-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="4ff79-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="4ff79-421">Páginas escritas en la memoria auxiliar (archivo de intercambio, archivo asignado, etc.)</span><span class="sxs-lookup"><span data-stu-id="4ff79-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="4ff79-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4ff79-422">AvailableSwap</span></span> | <span data-ttu-id="4ff79-423">Espacio de intercambio sin usar (MiB)</span><span class="sxs-lookup"><span data-stu-id="4ff79-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="4ff79-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4ff79-424">PercentAvailableSwap</span></span> | <span data-ttu-id="4ff79-425">Espacio de intercambio sin usar en forma de porcentaje del total de intercambio</span><span class="sxs-lookup"><span data-stu-id="4ff79-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="4ff79-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="4ff79-426">UsedSwap</span></span> | <span data-ttu-id="4ff79-427">Espacio de intercambio (MiB) en uso</span><span class="sxs-lookup"><span data-stu-id="4ff79-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="4ff79-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="4ff79-428">PercentUsedSwap</span></span> | <span data-ttu-id="4ff79-429">Espacio de intercambio en uso en forma de porcentaje del total de intercambio</span><span class="sxs-lookup"><span data-stu-id="4ff79-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="4ff79-430">Esta clase de métricas tiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="4ff79-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="4ff79-431">El atributo "condition" no tiene valores de configuración útiles y debería omitirse.</span><span class="sxs-lookup"><span data-stu-id="4ff79-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="4ff79-432">Métricas builtin para la clase Network</span><span class="sxs-lookup"><span data-stu-id="4ff79-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="4ff79-433">La clase de métricas Network proporciona información sobre la actividad de red de una interfaz de red concreta desde el arranque.</span><span class="sxs-lookup"><span data-stu-id="4ff79-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="4ff79-434">LAD no expone las métricas de ancho de banda, las cuales pueden recuperarse a partir de métricas de host.</span><span class="sxs-lookup"><span data-stu-id="4ff79-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="4ff79-435">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-435">counter</span></span> | <span data-ttu-id="4ff79-436">Significado</span><span class="sxs-lookup"><span data-stu-id="4ff79-436">Meaning</span></span>
------- | -------
<span data-ttu-id="4ff79-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="4ff79-437">BytesTransmitted</span></span> | <span data-ttu-id="4ff79-438">Total de bytes enviados desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-438">Total bytes sent since boot</span></span>
<span data-ttu-id="4ff79-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="4ff79-439">BytesReceived</span></span> | <span data-ttu-id="4ff79-440">Total de bytes recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-440">Total bytes received since boot</span></span>
<span data-ttu-id="4ff79-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="4ff79-441">BytesTotal</span></span> | <span data-ttu-id="4ff79-442">Total de bytes enviados o recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="4ff79-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="4ff79-443">PacketsTransmitted</span></span> | <span data-ttu-id="4ff79-444">Total de paquetes enviados desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-444">Total packets sent since boot</span></span>
<span data-ttu-id="4ff79-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="4ff79-445">PacketsReceived</span></span> | <span data-ttu-id="4ff79-446">Total de paquetes recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-446">Total packets received since boot</span></span>
<span data-ttu-id="4ff79-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="4ff79-447">TotalRxErrors</span></span> | <span data-ttu-id="4ff79-448">Número de errores de recepción desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-448">Number of receive errors since boot</span></span>
<span data-ttu-id="4ff79-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="4ff79-449">TotalTxErrors</span></span> | <span data-ttu-id="4ff79-450">Número de errores de transmisión desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="4ff79-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="4ff79-451">TotalCollisions</span></span> | <span data-ttu-id="4ff79-452">Número de colisiones notificadas por los puertos de red desde el arranque</span><span class="sxs-lookup"><span data-stu-id="4ff79-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="4ff79-453">Aunque esta clase está instanciada, LAD no admite la captura de agregados de métricas Network de todos los dispositivos de red.</span><span class="sxs-lookup"><span data-stu-id="4ff79-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="4ff79-454">Para obtener las métricas de una interfaz instanciada, como eth0, establezca `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="4ff79-455">Métricas builtin para la clase Filesystem</span><span class="sxs-lookup"><span data-stu-id="4ff79-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="4ff79-456">La clase de métricas Filesystem proporciona información sobre el uso del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="4ff79-457">Los valores absolutos y porcentuales se notifican como se hubieran mostrado a un usuario normal (no raíz).</span><span class="sxs-lookup"><span data-stu-id="4ff79-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="4ff79-458">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-458">counter</span></span> | <span data-ttu-id="4ff79-459">Significado</span><span class="sxs-lookup"><span data-stu-id="4ff79-459">Meaning</span></span>
------- | -------
<span data-ttu-id="4ff79-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="4ff79-460">FreeSpace</span></span> | <span data-ttu-id="4ff79-461">Espacio disponible en disco en bytes</span><span class="sxs-lookup"><span data-stu-id="4ff79-461">Available disk space in bytes</span></span>
<span data-ttu-id="4ff79-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="4ff79-462">UsedSpace</span></span> | <span data-ttu-id="4ff79-463">Espacio usado en disco en bytes</span><span class="sxs-lookup"><span data-stu-id="4ff79-463">Used disk space in bytes</span></span>
<span data-ttu-id="4ff79-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="4ff79-464">PercentFreeSpace</span></span> | <span data-ttu-id="4ff79-465">Porcentaje de espacio libre</span><span class="sxs-lookup"><span data-stu-id="4ff79-465">Percentage free space</span></span>
<span data-ttu-id="4ff79-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="4ff79-466">PercentUsedSpace</span></span> | <span data-ttu-id="4ff79-467">Porcentaje de espacio usado</span><span class="sxs-lookup"><span data-stu-id="4ff79-467">Percentage used space</span></span>
<span data-ttu-id="4ff79-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="4ff79-468">PercentFreeInodes</span></span> | <span data-ttu-id="4ff79-469">Porcentaje de inodes sin usar</span><span class="sxs-lookup"><span data-stu-id="4ff79-469">Percentage of unused inodes</span></span>
<span data-ttu-id="4ff79-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="4ff79-470">PercentUsedInodes</span></span> | <span data-ttu-id="4ff79-471">Porcentaje de inodes asignados (en uso) sumado de todos los sistemas de archivos</span><span class="sxs-lookup"><span data-stu-id="4ff79-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="4ff79-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-472">BytesReadPerSecond</span></span> | <span data-ttu-id="4ff79-473">Bytes leídos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-473">Bytes read per second</span></span>
<span data-ttu-id="4ff79-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="4ff79-475">Bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-475">Bytes written per second</span></span>
<span data-ttu-id="4ff79-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-476">BytesPerSecond</span></span> | <span data-ttu-id="4ff79-477">Bytes leídos o escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-477">Bytes read or written per second</span></span>
<span data-ttu-id="4ff79-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-478">ReadsPerSecond</span></span> | <span data-ttu-id="4ff79-479">Operaciones de lectura por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-479">Read operations per second</span></span>
<span data-ttu-id="4ff79-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-480">WritesPerSecond</span></span> | <span data-ttu-id="4ff79-481">Operaciones de escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-481">Write operations per second</span></span>
<span data-ttu-id="4ff79-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-482">TransfersPerSecond</span></span> | <span data-ttu-id="4ff79-483">Operaciones de lectura o escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-483">Read or write operations per second</span></span>

<span data-ttu-id="4ff79-484">Los valores agregados de todos los archivos del sistema pueden obtenerse estableciendo `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="4ff79-485">Los valores para un sistema de archivos montado específico, como "/mnt", pueden obtenerse estableciendo `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="4ff79-486">Métricas builtin para la clase Disk</span><span class="sxs-lookup"><span data-stu-id="4ff79-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="4ff79-487">La clase de métricas Disk proporciona información sobre el uso de dispositivos de disco.</span><span class="sxs-lookup"><span data-stu-id="4ff79-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="4ff79-488">Estas estadísticas se aplican a toda la unidad.</span><span class="sxs-lookup"><span data-stu-id="4ff79-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="4ff79-489">Si hay varios sistemas de archivos en un dispositivo, los contadores para dicho dispositivo están, de hecho, agregados en todos ellos.</span><span class="sxs-lookup"><span data-stu-id="4ff79-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="4ff79-490">counter</span><span class="sxs-lookup"><span data-stu-id="4ff79-490">counter</span></span> | <span data-ttu-id="4ff79-491">Significado</span><span class="sxs-lookup"><span data-stu-id="4ff79-491">Meaning</span></span>
------- | -------
<span data-ttu-id="4ff79-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-492">ReadsPerSecond</span></span> | <span data-ttu-id="4ff79-493">Operaciones de lectura por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-493">Read operations per second</span></span>
<span data-ttu-id="4ff79-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-494">WritesPerSecond</span></span> | <span data-ttu-id="4ff79-495">Operaciones de escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-495">Write operations per second</span></span>
<span data-ttu-id="4ff79-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-496">TransfersPerSecond</span></span> | <span data-ttu-id="4ff79-497">Total de operaciones por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-497">Total operations per second</span></span>
<span data-ttu-id="4ff79-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-498">AverageReadTime</span></span> | <span data-ttu-id="4ff79-499">Promedio de segundos por operación de lectura</span><span class="sxs-lookup"><span data-stu-id="4ff79-499">Average seconds per read operation</span></span>
<span data-ttu-id="4ff79-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-500">AverageWriteTime</span></span> | <span data-ttu-id="4ff79-501">Promedio de segundos por operación de escritura</span><span class="sxs-lookup"><span data-stu-id="4ff79-501">Average seconds per write operation</span></span>
<span data-ttu-id="4ff79-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="4ff79-502">AverageTransferTime</span></span> | <span data-ttu-id="4ff79-503">Promedio de segundos por operación</span><span class="sxs-lookup"><span data-stu-id="4ff79-503">Average seconds per operation</span></span>
<span data-ttu-id="4ff79-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="4ff79-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="4ff79-505">Promedio de operaciones de disco en cola</span><span class="sxs-lookup"><span data-stu-id="4ff79-505">Average number of queued disk operations</span></span>
<span data-ttu-id="4ff79-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="4ff79-507">Número de bytes leídos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-507">Number of bytes read per second</span></span>
<span data-ttu-id="4ff79-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="4ff79-509">Número de bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-509">Number of bytes written per second</span></span>
<span data-ttu-id="4ff79-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ff79-510">BytesPerSecond</span></span> | <span data-ttu-id="4ff79-511">Número de bytes leídos o escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="4ff79-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="4ff79-512">Los valores agregados de todos los discos pueden obtenerse estableciendo `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="4ff79-513">Para obtener información para un dispositivo en concreto (por ejemplo, /dev/sdf1), establezca `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="4ff79-514">Instalación y configuración de LAD 3.0 a través de CLI</span><span class="sxs-lookup"><span data-stu-id="4ff79-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="4ff79-515">Si suponemos que la configuración protegida se encuentra en el archivo PrivateConfig.json y que la información de configuración pública está en PublicConfig.json, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="4ff79-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="4ff79-516">El comando supone que se está usando el modo de Administración de recursos de Azure (ARM) de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff79-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="4ff79-517">Para configura LAD para máquinas virtuales con el modelo de implementación clásica (ASM), cambie al modo "asm" (`azure config mode asm`) y omita el nombre del grupo de recursos en el comando.</span><span class="sxs-lookup"><span data-stu-id="4ff79-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="4ff79-518">Para obtener más información, consulte la [documentación de la CLI multiplataforma](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="4ff79-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="4ff79-519">Una configuración de LAD 3.0 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4ff79-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="4ff79-520">Conforme a las anteriores definiciones, a continuación hay un ejemplo de configuración de extensión de LAD 3.0 con una explicación.</span><span class="sxs-lookup"><span data-stu-id="4ff79-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="4ff79-521">Para aplicar este ejemplo a su caso, debería usar su propio nombre de cuenta de almacenamiento, token de SAS de cuenta y tokens de SAS de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4ff79-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="4ff79-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="4ff79-522">PrivateConfig.json</span></span>

<span data-ttu-id="4ff79-523">Estos valores privados configuran lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ff79-523">These private settings configure:</span></span>

* <span data-ttu-id="4ff79-524">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4ff79-524">a storage account</span></span>
* <span data-ttu-id="4ff79-525">Un token de SAS de cuenta que coincida</span><span class="sxs-lookup"><span data-stu-id="4ff79-525">a matching account SAS token</span></span>
* <span data-ttu-id="4ff79-526">Varios receptores (Json BLOB o Event Hubs con tokens SAS)</span><span class="sxs-lookup"><span data-stu-id="4ff79-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="4ff79-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="4ff79-527">PublicConfig.json</span></span>

<span data-ttu-id="4ff79-528">Estos valores públicos hacen que LAD:</span><span class="sxs-lookup"><span data-stu-id="4ff79-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="4ff79-529">Cargue métricas de porcentaje de tiempo de procesador y espacio usado en disco en la tabla `WADMetrics*`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="4ff79-530">Cargue mensajes del recurso de syslog "user" y la gravedad "info" en la tabla `LinuxSyslog*`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="4ff79-531">Cargue resultados sin formato de consultas OMI (PercentProcessorTime y PercentIdleTime) en la tabla llamada `LinuxCPU`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="4ff79-532">Cargue líneas anexadas en el archivo `/var/log/myladtestlog` en la tabla `MyLadTestLog`.</span><span class="sxs-lookup"><span data-stu-id="4ff79-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="4ff79-533">En cualquier caso, también se cargan datos en:</span><span class="sxs-lookup"><span data-stu-id="4ff79-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="4ff79-534">Azure Blob Storage (el nombre del contenedor es el definido en el receptor de JSON Blob)</span><span class="sxs-lookup"><span data-stu-id="4ff79-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="4ff79-535">El punto de conexión de Event Hubs (especificado en el receptor de Event Hubs)</span><span class="sxs-lookup"><span data-stu-id="4ff79-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="4ff79-536">El elemento `resourceId` de la configuración debe coincidir con el de la VM o el del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4ff79-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="4ff79-537">La característica de creación de gráficos y desencadenamiento de alertas de métricas de la plataforma de Azure conoce el elemento resourceId de la máquina virtual en la que se esté trabajando.</span><span class="sxs-lookup"><span data-stu-id="4ff79-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="4ff79-538">Espera encontrar los datos de la máquina virtual mediante el elemento resourceId de la clave de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4ff79-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="4ff79-539">Si usa el escalado automático de Azure, el elemento resourceId de la configuración del escalado automático debe coincidir con el usado por LAD.</span><span class="sxs-lookup"><span data-stu-id="4ff79-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="4ff79-540">El elemento resourceId se compila en los nombres de instancias de JSON Blob escritas por LAD.</span><span class="sxs-lookup"><span data-stu-id="4ff79-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="4ff79-541">Consulta de los datos</span><span class="sxs-lookup"><span data-stu-id="4ff79-541">View your data</span></span>

<span data-ttu-id="4ff79-542">Use Azure Portal para consultar datos de rendimiento o establecer alertas:</span><span class="sxs-lookup"><span data-stu-id="4ff79-542">Use the Azure portal to view performance data or set alerts:</span></span>

![imagen](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="4ff79-544">Los datos de `performanceCounters` se almacenan en una tabla de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ff79-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="4ff79-545">Las API de Azure Storage están disponibles para múltiples lenguajes y plataformas.</span><span class="sxs-lookup"><span data-stu-id="4ff79-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="4ff79-546">Los datos enviados a receptores de Json BLOB se almacenan en blobs de la cuenta de almacenamiento a los que se dio nombre en la [Configuración protegida](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="4ff79-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="4ff79-547">Puede consumir los datos de blob con cualquier API de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4ff79-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="4ff79-548">Además, puede usar las siguientes herramientas de la interfaz de usuario para acceder a los datos de Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="4ff79-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="4ff79-549">Explorador de servidores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ff79-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="4ff79-550">[Explorador de Microsoft Azure Storage](https://azurestorageexplorer.codeplex.com/ "Explorador de Azure Storage").</span><span class="sxs-lookup"><span data-stu-id="4ff79-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="4ff79-551">Esta instantánea de una sesión del Explorador de Microsoft Azure Storage muestra las tablas y los contenedores de Azure Storage generados a partir de una extensión de LAD 3.0 configurada correctamente en una máquina virtual de prueba.</span><span class="sxs-lookup"><span data-stu-id="4ff79-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="4ff79-552">La imagen no coincide exactamente con la [configuración de ejemplo de LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="4ff79-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![imagen](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="4ff79-554">Consulte los [documentos de EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) pertinentes para obtener información sobre cómo consumir mensajes publicados en un punto de conexión de EventHubs.</span><span class="sxs-lookup"><span data-stu-id="4ff79-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ff79-555">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ff79-555">Next steps</span></span>

* <span data-ttu-id="4ff79-556">Cree alertas de métricas de [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para las métricas que recopile.</span><span class="sxs-lookup"><span data-stu-id="4ff79-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="4ff79-557">Cree [gráficos de supervisión](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para las métricas.</span><span class="sxs-lookup"><span data-stu-id="4ff79-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="4ff79-558">Obtenga información sobre cómo [crear un conjunto de escalado de máquinas virtuales](/azure/virtual-machines/linux/tutorial-create-vmss) con sus propias métricas para controlar el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4ff79-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
