---
title: "Proceso de aaaAzure - extensión de diagnóstico de Linux | Documentos de Microsoft"
description: "Cómo tooconfigure Hola métricas de toocollect de extensión de diagnóstico Linux (LAD) de Azure y registrar los eventos de máquinas virtuales de Linux que se ejecutan en Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="89e10-103">Usar registros y las métricas de toomonitor de extensión de diagnóstico de Linux</span><span class="sxs-lookup"><span data-stu-id="89e10-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="89e10-104">Este documento describe la versión 3.0 y versiones más reciente de hello extensión de diagnóstico de Linux.</span><span class="sxs-lookup"><span data-stu-id="89e10-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89e10-105">Para obtener información sobre las versiones 2.3 y anteriores, consulte [este documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="89e10-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="89e10-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="89e10-106">Introduction</span></span>

<span data-ttu-id="89e10-107">Hola extensión de diagnóstico de Linux ayuda a un usuario monitor Hola el estado de una VM de Linux que se ejecutan en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="89e10-108">Tiene Hola siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="89e10-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="89e10-109">Recopila las métricas de rendimiento del sistema de hello VM y los almacena en una tabla específica en una cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="89e10-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="89e10-110">Recupera el registro de sucesos de syslog y almacenarlos en una tabla específica en hello designado de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89e10-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="89e10-111">Permite a los usuarios toocustomize hello las métricas de datos que se recopilan y cargan.</span><span class="sxs-lookup"><span data-stu-id="89e10-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="89e10-112">Permite los recursos de syslog de usuarios toocustomize hello y niveles de gravedad de los eventos que se recopilan y cargan.</span><span class="sxs-lookup"><span data-stu-id="89e10-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="89e10-113">Permite que los usuarios tooupload registro especificado archivos tooa almacenamiento designadas tabla.</span><span class="sxs-lookup"><span data-stu-id="89e10-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="89e10-114">Admite el envío de las métricas y registro de eventos tooarbitrary EventHub los puntos de conexión y los blobs con formato JSON en hello designado cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89e10-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="89e10-115">Esta extensión funciona con los dos modelos de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="89e10-116">Instalando la extensión de Hola la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="89e10-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="89e10-117">Puede habilitar esta extensión mediante cmdlets de PowerShell de Azure de hello, secuencias de comandos de CLI de Azure o las plantillas de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="89e10-118">Para obtener más información, consulte [Funciones de la extensión](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="89e10-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="89e10-119">Hola portal de Azure no puede ser usado tooenable o configurar LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="89e10-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="89e10-120">En su lugar, instala versión 2.3 y la configura.</span><span class="sxs-lookup"><span data-stu-id="89e10-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="89e10-121">Alertas y gráficos de portal de azure trabajan con datos de ambas versiones de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="89e10-122">Mediante estas instrucciones de instalación y una [configuración de ejemplo descargable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) se configura LAD 3.0 para:</span><span class="sxs-lookup"><span data-stu-id="89e10-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="89e10-123">Capture y almacene Hola mismas métricas como proporcionadas por LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="89e10-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="89e10-124">capturar un conjunto útil de las métricas del sistema de archivo, nuevo tooLAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="89e10-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="89e10-125">captura de la colección de syslog predeterminada Hola habilitada por LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="89e10-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="89e10-126">Habilitar hello Azure experiencia del portal para gráficos y las alertas relacionadas con las métricas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89e10-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="89e10-127">configuración descargable Hello es simplemente un ejemplo; modificar toosuit sus propias necesidades.</span><span class="sxs-lookup"><span data-stu-id="89e10-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="89e10-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="89e10-128">Prerequisites</span></span>

* <span data-ttu-id="89e10-129">**Versión 2.2.0 o posterior del agente Linux de Azure**.</span><span class="sxs-lookup"><span data-stu-id="89e10-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="89e10-130">La mayoría de las imágenes de la galería de máquina virtual Linux de Azure incluyen la versión 2.2.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="89e10-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="89e10-131">Ejecutar `/usr/sbin/waagent -version` versión de hello tooconfirm instalada en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89e10-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="89e10-132">Si Hola VM está ejecutando una versión anterior del agente de invitado de Hola, siga [estas instrucciones](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate lo.</span><span class="sxs-lookup"><span data-stu-id="89e10-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="89e10-133">**CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="89e10-133">**Azure CLI**.</span></span> <span data-ttu-id="89e10-134">[Configurar hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) entorno en su equipo.</span><span class="sxs-lookup"><span data-stu-id="89e10-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="89e10-135">Hola wget comando, si aún no lo tiene: ejecutar `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="89e10-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="89e10-136">Cuenta de una suscripción de Azure y un almacenamiento existente dentro de él toostore datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="89e10-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="89e10-137">Instalación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89e10-137">Sample installation</span></span>

<span data-ttu-id="89e10-138">Rellenar parámetros correctos de hello en hello tres primeras líneas y, a continuación, ejecutar este script como raíz:</span><span class="sxs-lookup"><span data-stu-id="89e10-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="89e10-139">dirección URL de Hello para la configuración de ejemplo de Hola y su contenido es toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="89e10-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="89e10-140">Descargue una copia del archivo JSON de la configuración del portal de Hola y personalizarla en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="89e10-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="89e10-141">Cualquier plantilla o automatización que genere deberían usar su propia copia en lugar de descargar dicha URL cada vez.</span><span class="sxs-lookup"><span data-stu-id="89e10-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="89e10-142">Actualizando la configuración de la extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="89e10-142">Updating hello extension settings</span></span>

<span data-ttu-id="89e10-143">Después de cambiar la configuración pública o protegido, implementarlas toohello VM mediante la ejecución de Hola mismo comando.</span><span class="sxs-lookup"><span data-stu-id="89e10-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="89e10-144">Si nada cambia en la configuración de hello, configuraciones de hello actualizado se envían toohello extensión.</span><span class="sxs-lookup"><span data-stu-id="89e10-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="89e10-145">LAD vuelve a cargar la configuración de Hola y se reinicia.</span><span class="sxs-lookup"><span data-stu-id="89e10-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="89e10-146">Migración desde versiones anteriores de extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="89e10-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="89e10-147">Hola la versión más reciente de extensión de hello es **3.0**.</span><span class="sxs-lookup"><span data-stu-id="89e10-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="89e10-148">**Todas las versiones anteriores (2.x) están en desuso y pueden retirarse a partir del 31 de julio de 2018**.</span><span class="sxs-lookup"><span data-stu-id="89e10-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89e10-149">Esta extensión introduce la separación de la configuración de toohello de cambios de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="89e10-150">Uno de estos cambios se realizó la seguridad de hello tooimprove de extensión de hello; como resultado, con las versiones anteriores compatibilidad con 2.x no se pudo mantener.</span><span class="sxs-lookup"><span data-stu-id="89e10-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="89e10-151">Además, Hola publicador de extensión para esta extensión es diferente de publicador Hola para las versiones 2.x Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="89e10-152">toomigrate de 2.x toothis nueva versión de extensión de hello, debe desinstalar la extensión anterior de hello (con nombre de publicador antiguo de hello) y, a continuación, instalar la versión 3 de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="89e10-153">Recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="89e10-153">Recommendations:</span></span>

* <span data-ttu-id="89e10-154">Instalar extensión de hello con la actualización de versión secundaria automática habilitada.</span><span class="sxs-lookup"><span data-stu-id="89e10-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="89e10-155">En el modelo de implementación clásica máquinas virtuales, especificar '3.*' como versión de Hola si va a instalar la extensión de Hola a través de Azure XPLAT CLI o Powershell.</span><span class="sxs-lookup"><span data-stu-id="89e10-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="89e10-156">En la implementación de Azure Resource Manager del modelo de las máquinas virtuales, incluir ' "autoUpgradeMinorVersion": true' en la plantilla de implementación de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="89e10-157">Use una cuenta de almacenamiento nueva o diferente para LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="89e10-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="89e10-158">Hay varias pequeñas incompatibilidades entre LAD 2.3 y LAD 3.0 que hacen que compartir una cuenta sea problemático:</span><span class="sxs-lookup"><span data-stu-id="89e10-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="89e10-159">LAD 3.0 almacena los eventos de syslog en una tabla con un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="89e10-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="89e10-160">counterSpecifier Hola cadenas para `builtin` métricas difieren en LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="89e10-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="89e10-161">Configuración protegida</span><span class="sxs-lookup"><span data-stu-id="89e10-161">Protected settings</span></span>

<span data-ttu-id="89e10-162">Este conjunto de información de configuración contiene información confidencial que debería protegerse de la vista pública, por ejemplo, las credenciales de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89e10-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="89e10-163">Estos valores son transmitido tooand almacenado por la extensión de hello en formato cifrado.</span><span class="sxs-lookup"><span data-stu-id="89e10-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="89e10-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="89e10-164">Name</span></span> | <span data-ttu-id="89e10-165">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-165">Value</span></span>
---- | -----
<span data-ttu-id="89e10-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="89e10-166">storageAccountName</span></span> | <span data-ttu-id="89e10-167">Hola el nombre de cuenta de almacenamiento de hello en el que los datos se escriben por extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="89e10-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="89e10-168">storageAccountEndPoint</span></span> | <span data-ttu-id="89e10-169">identificar en qué Hola existe la cuenta de almacenamiento en la nube Hola el extremo de hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="89e10-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="89e10-170">Si este valor está ausente, LAD predeterminado toohello nube pública de Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="89e10-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="89e10-171">toouse una cuenta de almacenamiento de Azure en Alemania, Azure Government o Azure China, establezca este valor en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="89e10-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="89e10-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="89e10-172">storageAccountSasToken</span></span> | <span data-ttu-id="89e10-173">Un [token de SAS de cuenta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para los servicios Blob y tabla (`ss='bt'`), toocontainers aplicables y los objetos (`srt='co'`), que concede agrega, crear, enumerar, actualizar y permisos de escritura (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="89e10-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="89e10-174">Hacer *no* incluyen hello inicial interrogación (?).</span><span class="sxs-lookup"><span data-stu-id="89e10-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="89e10-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="89e10-175">mdsdHttpProxy</span></span> | <span data-ttu-id="89e10-176">(opcional) La información necesaria de proxy HTTP tooenable Hola extensión tooconnect toohello especifica cuenta de almacenamiento y del extremo.</span><span class="sxs-lookup"><span data-stu-id="89e10-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="89e10-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="89e10-177">sinksConfig</span></span> | <span data-ttu-id="89e10-178">(opcional) Detalles de las métricas de toowhich destinos alternativos y eventos se pueden entregar.</span><span class="sxs-lookup"><span data-stu-id="89e10-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="89e10-179">detalles específicos de Hola de cada receptor de datos compatibles con la extensión de Hola se tratan en secciones de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="89e10-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="89e10-180">Puede construir fácilmente Hola requerido el token de SAS a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="89e10-181">Seleccione toowhich de cuenta de almacenamiento general Hola desea Hola extensión toowrite</span><span class="sxs-lookup"><span data-stu-id="89e10-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="89e10-182">Seleccione "Firma de acceso compartido" de parte de la configuración de hello del menú izquierdo Hola</span><span class="sxs-lookup"><span data-stu-id="89e10-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="89e10-183">Asegúrese de secciones correspondientes de hello como se describió anteriormente</span><span class="sxs-lookup"><span data-stu-id="89e10-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="89e10-184">Haga clic en el botón de "Generar SAS" Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-184">Click hello "Generate SAS" button.</span></span>

![imagen](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="89e10-186">Hola copia genera SAS en el campo de hello storageAccountSasToken; quitar Hola inicial de interrogación ("?").</span><span class="sxs-lookup"><span data-stu-id="89e10-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="89e10-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="89e10-187">sinksConfig</span></span>

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

<span data-ttu-id="89e10-188">Esta sección opcional define otros destinos de extensión de hello toowhich envía información de hello recopila.</span><span class="sxs-lookup"><span data-stu-id="89e10-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="89e10-189">matriz de "receptor" Hello contiene un objeto para cada receptor de datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="89e10-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="89e10-190">Hola determina el atributo "type" Hola otros atributos de objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="89e10-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-191">Element</span></span> | <span data-ttu-id="89e10-192">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-192">Value</span></span>
------- | -----
<span data-ttu-id="89e10-193">name</span><span class="sxs-lookup"><span data-stu-id="89e10-193">name</span></span> | <span data-ttu-id="89e10-194">Receptor de toothis toorefer en otra parte de la configuración de la extensión de hello usa una cadena.</span><span class="sxs-lookup"><span data-stu-id="89e10-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="89e10-195">type</span><span class="sxs-lookup"><span data-stu-id="89e10-195">type</span></span> | <span data-ttu-id="89e10-196">tipo de Hello del receptor que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="89e10-196">hello type of sink being defined.</span></span> <span data-ttu-id="89e10-197">Hola otros valores (si existe) se determina en instancias de este tipo.</span><span class="sxs-lookup"><span data-stu-id="89e10-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="89e10-198">La versión 3.0 de hello extensión de diagnóstico de Linux admite dos tipos de receptor: EventHub y JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="89e10-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="89e10-199">receptor de EventHub Hola</span><span class="sxs-lookup"><span data-stu-id="89e10-199">hello EventHub sink</span></span>

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

<span data-ttu-id="89e10-200">entrada de "sasURL" Hello contiene Hola debe publicarse la dirección URL completa, incluido el token SAS, para hello datos toowhich de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="89e10-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="89e10-201">LAD requiere una SAS una directiva que habilita la notificación de envío de Hola de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="89e10-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="89e10-202">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="89e10-202">An example:</span></span>

* <span data-ttu-id="89e10-203">Cree un espacio de nombres de Event Hubs llamado `contosohub`.</span><span class="sxs-lookup"><span data-stu-id="89e10-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="89e10-204">Crear un concentrador de eventos en el espacio de nombres de hello denominado`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="89e10-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="89e10-205">Crear una directiva de acceso compartido en hello concentrador de eventos denominado `writer` que permite Hola notificación de envío</span><span class="sxs-lookup"><span data-stu-id="89e10-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="89e10-206">Si ha creado una SAS buena hasta medianoche UTC en el 1 de enero de 2018, el valor de sasURL de hello podría ser:</span><span class="sxs-lookup"><span data-stu-id="89e10-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="89e10-207">Para obtener más información sobre la generación de tokens de SAS para Event Hubs, consulte [esta página web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89e10-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="89e10-208">receptor de Hello JsonBlob</span><span class="sxs-lookup"><span data-stu-id="89e10-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="89e10-209">Los datos de dirigir tooa JsonBlob receptor se almacena en blobs en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="89e10-210">Cada instancia de LAD crea un blob cada hora para cada nombre de receptor.</span><span class="sxs-lookup"><span data-stu-id="89e10-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="89e10-211">Todos los blobs siempre contienen una matriz de objeto JSON válida sintácticamente.</span><span class="sxs-lookup"><span data-stu-id="89e10-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="89e10-212">Las nuevas entradas se agregan atómicamente toohello matriz.</span><span class="sxs-lookup"><span data-stu-id="89e10-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="89e10-213">BLOB se almacenan en un contenedor con el mismo nombre como receptor de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="89e10-214">Hola reglas de almacenamiento de Azure para los nombres de contenedor de blob aplican nombres toohello de receptores JsonBlob: entre 3 y 63 caracteres ASCII alfanuméricos en minúsculas o guiones.</span><span class="sxs-lookup"><span data-stu-id="89e10-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="89e10-215">Configuración pública</span><span class="sxs-lookup"><span data-stu-id="89e10-215">Public settings</span></span>

<span data-ttu-id="89e10-216">Esta estructura contiene varios bloques de configuración que controla la información de hello recopilada por extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="89e10-217">Cada valor de configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="89e10-217">Each setting is optional.</span></span> <span data-ttu-id="89e10-218">Si especifica `ladCfg`, también debe especificar `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="89e10-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="89e10-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-219">Element</span></span> | <span data-ttu-id="89e10-220">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-220">Value</span></span>
------- | -----
<span data-ttu-id="89e10-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="89e10-221">StorageAccount</span></span> | <span data-ttu-id="89e10-222">Hola el nombre de cuenta de almacenamiento de hello en el que los datos se escriben por extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="89e10-223">Debe ser Hola mismo nombre tal y como se especifica en hello [protegido configuración](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="89e10-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="89e10-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="89e10-224">mdsdHttpProxy</span></span> | <span data-ttu-id="89e10-225">(opcional) Igual que hello [protegido configuración](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="89e10-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="89e10-226">Hola pública valor se sustituye por valor privada de hello, si establece.</span><span class="sxs-lookup"><span data-stu-id="89e10-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="89e10-227">Colocar valores de proxy que contienen un secreto, como una contraseña, en hello [protegido configuración](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="89e10-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="89e10-228">los elementos restantes de Hola se describen en detalle en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="89e10-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="89e10-229">ladCfg</span></span>

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

<span data-ttu-id="89e10-230">Los receptores de esta recopilación de Hola de controles de estructura opcional de las métricas y los registros para entrega toohello datos de servicio y tooother de métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="89e10-231">Debe especificar `performanceCounters`, `syslogEvents` o ambos.</span><span class="sxs-lookup"><span data-stu-id="89e10-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="89e10-232">Debe especificar hello `metrics` estructura.</span><span class="sxs-lookup"><span data-stu-id="89e10-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="89e10-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-233">Element</span></span> | <span data-ttu-id="89e10-234">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-234">Value</span></span>
------- | -----
<span data-ttu-id="89e10-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="89e10-235">eventVolume</span></span> | <span data-ttu-id="89e10-236">(opcional) Número de particiones creadas dentro de la tabla de almacenamiento de Hola Hola a controles.</span><span class="sxs-lookup"><span data-stu-id="89e10-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="89e10-237">Debe ser uno de los siguientes valores: `"Large"`, `"Medium"` o `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="89e10-238">Si no se especifica, el valor predeterminado de hello es `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="89e10-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="89e10-239">sampleRateInSeconds</span></span> | <span data-ttu-id="89e10-240">intervalo predeterminado de hello (opcional) entre la colección de métricas (prolongadas) sin formato.</span><span class="sxs-lookup"><span data-stu-id="89e10-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="89e10-241">velocidad de muestra de Hola menor admitida es de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="89e10-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="89e10-242">Si no se especifica, el valor predeterminado de hello es `15`.</span><span class="sxs-lookup"><span data-stu-id="89e10-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="89e10-243">Métricas</span><span class="sxs-lookup"><span data-stu-id="89e10-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="89e10-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-244">Element</span></span> | <span data-ttu-id="89e10-245">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-245">Value</span></span>
------- | -----
<span data-ttu-id="89e10-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="89e10-246">resourceId</span></span> | <span data-ttu-id="89e10-247">Identificador de recurso de Azure Resource Manager Hola de hello VM o de escala de máquinas virtuales de hello establece hello toowhich que pertenece la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89e10-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="89e10-248">Este valor debe ser también especifica si se utiliza cualquier receptor JsonBlob en configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="89e10-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="89e10-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="89e10-250">frecuencia de Hello en el que métricas agregadas son toobe se calcula y transfiere tooAzure métricas, expresado como un intervalo de tiempo es 8601.</span><span class="sxs-lookup"><span data-stu-id="89e10-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="89e10-251">período de transferencia más pequeño de Hello es 60 segundos, es decir, PT1M.</span><span class="sxs-lookup"><span data-stu-id="89e10-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="89e10-252">Debe especificar al menos un elemento scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="89e10-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="89e10-253">Ejemplos de hello métricas especificadas en la sección de performanceCounters de Hola se recopilan cada 15 segundos o en la velocidad de muestra de Hola definida explícitamente para el contador de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="89e10-254">Si aparecen varias frecuencias de scheduledTransferPeriod (como en el ejemplo de Hola), cada agregación se calcula de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="89e10-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="89e10-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="89e10-255">performanceCounters</span></span>

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

<span data-ttu-id="89e10-256">Colección de Hola de métricas de controles de esta sección opcional.</span><span class="sxs-lookup"><span data-stu-id="89e10-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="89e10-257">Ejemplos sin formato se agregan para cada [scheduledTransferPeriod](#metrics) tooproduce estos valores:</span><span class="sxs-lookup"><span data-stu-id="89e10-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="89e10-258">mean</span><span class="sxs-lookup"><span data-stu-id="89e10-258">mean</span></span>
* <span data-ttu-id="89e10-259">minimum</span><span class="sxs-lookup"><span data-stu-id="89e10-259">minimum</span></span>
* <span data-ttu-id="89e10-260">maximum</span><span class="sxs-lookup"><span data-stu-id="89e10-260">maximum</span></span>
* <span data-ttu-id="89e10-261">last-collected value</span><span class="sxs-lookup"><span data-stu-id="89e10-261">last-collected value</span></span>
* <span data-ttu-id="89e10-262">recuento de muestras sin formato utiliza el agregado de hello toocompute</span><span class="sxs-lookup"><span data-stu-id="89e10-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="89e10-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-263">Element</span></span> | <span data-ttu-id="89e10-264">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-264">Value</span></span>
------- | -----
<span data-ttu-id="89e10-265">sinks</span><span class="sxs-lookup"><span data-stu-id="89e10-265">sinks</span></span> | <span data-ttu-id="89e10-266">(opcional) Una lista separada por comas de nombres de los receptores toowhich que LAD envía los resultados de métrica agregado.</span><span class="sxs-lookup"><span data-stu-id="89e10-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="89e10-267">Todas las métricas agregadas son tooeach publicado aparece receptor.</span><span class="sxs-lookup"><span data-stu-id="89e10-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="89e10-268">Consulte [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="89e10-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="89e10-269">Ejemplo: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="89e10-270">type</span><span class="sxs-lookup"><span data-stu-id="89e10-270">type</span></span> | <span data-ttu-id="89e10-271">Identifica Hola proveedor real de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="89e10-272">class</span><span class="sxs-lookup"><span data-stu-id="89e10-272">class</span></span> | <span data-ttu-id="89e10-273">Junto con "counter" identifica métrica específica de hello en el espacio de nombres del proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="89e10-274">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-274">counter</span></span> | <span data-ttu-id="89e10-275">Junto con "clase", identifica métrica específica de hello en el espacio de nombres del proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="89e10-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="89e10-276">counterSpecifier</span></span> | <span data-ttu-id="89e10-277">Identifica la métrica específica de hello en el espacio de nombres de hello las métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="89e10-278">condition</span><span class="sxs-lookup"><span data-stu-id="89e10-278">condition</span></span> | <span data-ttu-id="89e10-279">(opcional) Selecciona una instancia específica de la métrica de hello objeto toowhich Hola se aplica o selecciona Hola agregación en todas las instancias de ese objeto.</span><span class="sxs-lookup"><span data-stu-id="89e10-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="89e10-280">Para obtener más información, vea hello [ `builtin` definiciones de métrica](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="89e10-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="89e10-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="89e10-281">sampleRate</span></span> | <span data-ttu-id="89e10-282">ES el intervalo de 8601 que establece la tasa de hello en el que se recopilaron las muestras sin procesar para esta métrica.</span><span class="sxs-lookup"><span data-stu-id="89e10-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="89e10-283">Si no se establece, el intervalo de recopilación de Hola se establece por valor de Hola de [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="89e10-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="89e10-284">velocidad de muestreo admitida más corta de Hello es 15 segundos (PT15S).</span><span class="sxs-lookup"><span data-stu-id="89e10-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="89e10-285">unit</span><span class="sxs-lookup"><span data-stu-id="89e10-285">unit</span></span> | <span data-ttu-id="89e10-286">Debería ser una de estas cadenas: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond" o "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="89e10-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="89e10-287">Define la unidad de Hola de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="89e10-288">Los consumidores de hello recopilan datos esperar Hola recopila datos valores toomatch esta unidad.</span><span class="sxs-lookup"><span data-stu-id="89e10-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="89e10-289">LAD omite este campo.</span><span class="sxs-lookup"><span data-stu-id="89e10-289">LAD ignores this field.</span></span>
<span data-ttu-id="89e10-290">DisplayName</span><span class="sxs-lookup"><span data-stu-id="89e10-290">displayName</span></span> | <span data-ttu-id="89e10-291">Hola etiqueta (en el lenguaje de hello especificado por la configuración regional asociada de hello establecer) toobe adjunta toothis datos de métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="89e10-292">LAD omite este campo.</span><span class="sxs-lookup"><span data-stu-id="89e10-292">LAD ignores this field.</span></span>

<span data-ttu-id="89e10-293">counterSpecifier Hello es un identificador arbitrario.</span><span class="sxs-lookup"><span data-stu-id="89e10-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="89e10-294">Los consumidores de métricas, como Hola diagramación de portal de Azure y las alertas de característica, usan counterSpecifier como Hola "clave" que identifica una métrica o una instancia de una métrica.</span><span class="sxs-lookup"><span data-stu-id="89e10-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="89e10-295">Para las métricas de `builtin`, se recomienda usar valores counterSpecifier que empiecen por `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="89e10-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="89e10-296">Si va a recopilar una instancia específica de una métrica, se recomienda que asociar identificador hello de valor de hello instancia toohello counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="89e10-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="89e10-297">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="89e10-297">Some examples:</span></span>

* <span data-ttu-id="89e10-298">`/builtin/Processor/PercentIdleTime`: tiempo de inactividad promediado en todos los núcleos</span><span class="sxs-lookup"><span data-stu-id="89e10-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="89e10-299">`/builtin/Disk/FreeSpace(/mnt)`-Espacio para el sistema de archivos de Hola/mnt</span><span class="sxs-lookup"><span data-stu-id="89e10-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="89e10-300">`/builtin/Disk/FreeSpace`: espacio libre promediado entre todos los elementos filesystem montados</span><span class="sxs-lookup"><span data-stu-id="89e10-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="89e10-301">LAD ni Hola portal de Azure espera hello counterSpecifier valor toomatch cualquier patrón.</span><span class="sxs-lookup"><span data-stu-id="89e10-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="89e10-302">Sea coherente en el modo de construcción de valores counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="89e10-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="89e10-303">Cuando se especifica `performanceCounters`, LAD siempre escribe tooa tabla de datos en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="89e10-304">Se puede haber Hola mismo datos escritos tooJSON blobs o centros de eventos, pero no se puede deshabilitar la tabla de tooa de almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="89e10-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="89e10-305">Todas las instancias de hello configurada de diagnóstico extensión toouse Hola misma cuenta de almacenamiento, nombre y el extremo agregan su toohello registros y las métricas misma tabla.</span><span class="sxs-lookup"><span data-stu-id="89e10-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="89e10-306">Si hay demasiadas máquinas virtuales son escribir toohello puede limitar la misma partición de tabla, Azure escribe toothat partición.</span><span class="sxs-lookup"><span data-stu-id="89e10-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="89e10-307">eventVolume Hola establecer causas entradas toobe se reparten entre 1 (pequeño), 10 (medio) o 100 particiones diferentes (grande).</span><span class="sxs-lookup"><span data-stu-id="89e10-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="89e10-308">Por lo general, "Medio" es suficiente tooensure tráfico no está limitado.</span><span class="sxs-lookup"><span data-stu-id="89e10-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="89e10-309">característica de las métricas de Azure Hola de hello portal de Azure usa datos de hello en este gráficos tooproduce de tabla o tootrigger alertas.</span><span class="sxs-lookup"><span data-stu-id="89e10-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="89e10-310">nombre de la tabla de Hello es la concatenación de Hola de estas cadenas:</span><span class="sxs-lookup"><span data-stu-id="89e10-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="89e10-311">Hola "scheduledTransferPeriod" para hello agrega valores almacenados en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="89e10-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="89e10-312">Una fecha, en forma de Hola "AAAAMMDD", que cambia cada 10 días</span><span class="sxs-lookup"><span data-stu-id="89e10-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="89e10-313">Algunos ejemplos son `WADMetricsPT1HP10DV2S20170410` y `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="89e10-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="89e10-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="89e10-314">syslogEvents</span></span>

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

<span data-ttu-id="89e10-315">Esta sección opcional controla la recolección de Hola de registrar eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="89e10-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="89e10-316">Si se omite la sección de hello, eventos de syslog no se capturan en absoluto.</span><span class="sxs-lookup"><span data-stu-id="89e10-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="89e10-317">colección de Hello syslogEventConfiguration tiene una entrada para cada utilidad syslog de interés.</span><span class="sxs-lookup"><span data-stu-id="89e10-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="89e10-318">Si minSeverity es "NONE" para un servicio determinado, o si dicha instalación no aparece en el elemento de hello en absoluto, no se captura ningún evento de dicha instalación.</span><span class="sxs-lookup"><span data-stu-id="89e10-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="89e10-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-319">Element</span></span> | <span data-ttu-id="89e10-320">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-320">Value</span></span>
------- | -----
<span data-ttu-id="89e10-321">sinks</span><span class="sxs-lookup"><span data-stu-id="89e10-321">sinks</span></span> | <span data-ttu-id="89e10-322">Una lista separada por comas de nombres de los receptores de registro individuales toowhich los eventos se publican.</span><span class="sxs-lookup"><span data-stu-id="89e10-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="89e10-323">Todos los eventos de registro que coinciden con las restricciones de hello en syslogEventConfiguration son tooeach publicado aparece receptor.</span><span class="sxs-lookup"><span data-stu-id="89e10-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="89e10-324">Por ejemplo, "EHforsyslog".</span><span class="sxs-lookup"><span data-stu-id="89e10-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="89e10-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="89e10-325">facilityName</span></span> | <span data-ttu-id="89e10-326">Es un nombre de recurso de syslog (como "LOG\_USER" o "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="89e10-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="89e10-327">Consulte la sección de "instalación de" hello de hello [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para la lista completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="89e10-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="89e10-328">minSeverity</span></span> | <span data-ttu-id="89e10-329">Es un nivel de gravedad de syslog (como "LOG\_ERR" o "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="89e10-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="89e10-330">Consulte la sección de "nivel" hello de hello [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para la lista completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="89e10-331">extensión de Hello captura eventos enviados toohello instalaciones en o por encima de hello especifica el nivel.</span><span class="sxs-lookup"><span data-stu-id="89e10-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="89e10-332">Cuando se especifica `syslogEvents`, LAD siempre escribe tooa tabla de datos en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="89e10-333">Se puede haber Hola mismo datos escritos tooJSON blobs o centros de eventos, pero no se puede deshabilitar la tabla de tooa de almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="89e10-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="89e10-334">Hola comportamiento para esta tabla de la partición es Hola igual al descrito en `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="89e10-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="89e10-335">nombre de la tabla de Hello es la concatenación de Hola de estas cadenas:</span><span class="sxs-lookup"><span data-stu-id="89e10-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="89e10-336">Una fecha, en forma de Hola "AAAAMMDD", que cambia cada 10 días</span><span class="sxs-lookup"><span data-stu-id="89e10-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="89e10-337">Algunos ejemplos son `LinuxSyslog20170410` y `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="89e10-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="89e10-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="89e10-338">perfCfg</span></span>

<span data-ttu-id="89e10-339">Esta sección opcional controla la exclusión de consultas [OMI](https://github.com/Microsoft/omi) arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="89e10-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="89e10-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-340">Element</span></span> | <span data-ttu-id="89e10-341">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-341">Value</span></span>
------- | -----
<span data-ttu-id="89e10-342">espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="89e10-342">namespace</span></span> | <span data-ttu-id="89e10-343">(opcional) Hola OMI espacio de nombres dentro de qué Hola se debe ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="89e10-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="89e10-344">Si no se especifica, el valor de predeterminado de hello es "root/scx", implementada por hello [System Center multiplataforma proveedores](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="89e10-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="89e10-345">query</span><span class="sxs-lookup"><span data-stu-id="89e10-345">query</span></span> | <span data-ttu-id="89e10-346">Hola OMI toobe de consulta ejecutado.</span><span class="sxs-lookup"><span data-stu-id="89e10-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="89e10-347">table</span><span class="sxs-lookup"><span data-stu-id="89e10-347">table</span></span> | <span data-ttu-id="89e10-348">tabla de almacenamiento de Azure de hello (opcional), en hello designado de la cuenta de almacenamiento (vea [protegido configuración](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="89e10-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="89e10-349">frequency</span><span class="sxs-lookup"><span data-stu-id="89e10-349">frequency</span></span> | <span data-ttu-id="89e10-350">número de hello (opcional) de segundos entre ejecuciones de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="89e10-351">El valor predeterminado es de 300 (5 minutos) y el mínimo es de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="89e10-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="89e10-352">sinks</span><span class="sxs-lookup"><span data-stu-id="89e10-352">sinks</span></span> | <span data-ttu-id="89e10-353">(opcional) Debe publicarse una lista separada por comas de nombres de los resultados de métrica de receptores adicionales toowhich ejemplo sin formato.</span><span class="sxs-lookup"><span data-stu-id="89e10-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="89e10-354">Ninguna agregación de estos ejemplos sin procesar se calcula por la extensión de Hola o las métricas de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="89e10-355">Deben especificarse "table", "sinks" o ambos.</span><span class="sxs-lookup"><span data-stu-id="89e10-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="89e10-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="89e10-356">fileLogs</span></span>

<span data-ttu-id="89e10-357">Hola de controles de captura de los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="89e10-357">Controls hello capture of log files.</span></span> <span data-ttu-id="89e10-358">LAD captura nuevas líneas de texto, tal y como se escriben toohello archivo y los escribe filas tootable o los receptores especificados (JsonBlob o EventHub).</span><span class="sxs-lookup"><span data-stu-id="89e10-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="89e10-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="89e10-359">Element</span></span> | <span data-ttu-id="89e10-360">Valor</span><span class="sxs-lookup"><span data-stu-id="89e10-360">Value</span></span>
------- | -----
<span data-ttu-id="89e10-361">file</span><span class="sxs-lookup"><span data-stu-id="89e10-361">file</span></span> | <span data-ttu-id="89e10-362">ruta de acceso completa de Hola de toobe de archivo de registro de hello visto y capturado.</span><span class="sxs-lookup"><span data-stu-id="89e10-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="89e10-363">ruta de acceso de Hello debe asignar un nombre único de un archivo, no puede nombrar un directorio o contiene caracteres comodines.</span><span class="sxs-lookup"><span data-stu-id="89e10-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="89e10-364">table</span><span class="sxs-lookup"><span data-stu-id="89e10-364">table</span></span> | <span data-ttu-id="89e10-365">tabla de almacenamiento de Azure de hello (opcional), en el almacenamiento de hello designado de la cuenta (tal y como se especifica en la configuración de hello protegido), en las nuevas líneas de Hola "cola" del archivo hello se escribe.</span><span class="sxs-lookup"><span data-stu-id="89e10-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="89e10-366">sinks</span><span class="sxs-lookup"><span data-stu-id="89e10-366">sinks</span></span> | <span data-ttu-id="89e10-367">(opcional) Envía una lista separada por comas de nombres de las líneas de registro de toowhich de receptores adicionales.</span><span class="sxs-lookup"><span data-stu-id="89e10-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="89e10-368">Deben especificarse "table", "sinks" o ambos.</span><span class="sxs-lookup"><span data-stu-id="89e10-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="89e10-369">Métricas de hello builtin proveedor admitidas</span><span class="sxs-lookup"><span data-stu-id="89e10-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="89e10-370">proveedor de Hello builtin métrica es un origen de métricas más interesantes tooa amplio conjunto de usuarios.</span><span class="sxs-lookup"><span data-stu-id="89e10-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="89e10-371">Estas métricas se dividen en cinco clases amplias:</span><span class="sxs-lookup"><span data-stu-id="89e10-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="89e10-372">Procesador</span><span class="sxs-lookup"><span data-stu-id="89e10-372">Processor</span></span>
* <span data-ttu-id="89e10-373">Memoria</span><span class="sxs-lookup"><span data-stu-id="89e10-373">Memory</span></span>
* <span data-ttu-id="89e10-374">Red</span><span class="sxs-lookup"><span data-stu-id="89e10-374">Network</span></span>
* <span data-ttu-id="89e10-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="89e10-375">Filesystem</span></span>
* <span data-ttu-id="89e10-376">Disco</span><span class="sxs-lookup"><span data-stu-id="89e10-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="89e10-377">métricas de Builtin para hello clase de procesador</span><span class="sxs-lookup"><span data-stu-id="89e10-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="89e10-378">Hola clase de procesador de métricas proporciona información sobre el uso de procesador en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89e10-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="89e10-379">Al agregar porcentajes, resultado de hello es promedio de hello en todas las CPU.</span><span class="sxs-lookup"><span data-stu-id="89e10-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="89e10-380">En una máquina virtual de dos núcleos, si un núcleo era ocupados al 100% y Hola otro era 100% inactivo, Hola informa que percentidletime sería 50.</span><span class="sxs-lookup"><span data-stu-id="89e10-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="89e10-381">Si cada núcleo es 50% ocupado para Hola mismo período, Hola notifica el resultado también sería 50.</span><span class="sxs-lookup"><span data-stu-id="89e10-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="89e10-382">En una de máquina virtual, de cuatro núcleos con un núcleo ocupados al 100% y Hola otros inactivo, Hola indicados que percentidletime sería 75.</span><span class="sxs-lookup"><span data-stu-id="89e10-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="89e10-383">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-383">counter</span></span> | <span data-ttu-id="89e10-384">Significado</span><span class="sxs-lookup"><span data-stu-id="89e10-384">Meaning</span></span>
------- | -------
<span data-ttu-id="89e10-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="89e10-385">PercentIdleTime</span></span> | <span data-ttu-id="89e10-386">Porcentaje de tiempo durante la ventana de la agregación de Hola que procesadores estaban ejecutando bucle inactivo de hello kernel</span><span class="sxs-lookup"><span data-stu-id="89e10-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="89e10-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="89e10-387">PercentProcessorTime</span></span> | <span data-ttu-id="89e10-388">Porcentaje de tiempo de ejecución de un subproceso no inactivo</span><span class="sxs-lookup"><span data-stu-id="89e10-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="89e10-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="89e10-389">PercentIOWaitTime</span></span> | <span data-ttu-id="89e10-390">Porcentaje de tiempo de espera para toocomplete de las operaciones de E/S</span><span class="sxs-lookup"><span data-stu-id="89e10-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="89e10-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="89e10-391">PercentInterruptTime</span></span> | <span data-ttu-id="89e10-392">Porcentaje de tiempo de ejecución de interrupciones de hardware o software y DPC (llamadas a procedimiento aplazadas)</span><span class="sxs-lookup"><span data-stu-id="89e10-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="89e10-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="89e10-393">PercentUserTime</span></span> | <span data-ttu-id="89e10-394">Tiempo no está inactivo durante la ventana de la agregación de hello, porcentaje de Hola de tiempo invertido en usuario más con prioridad normal</span><span class="sxs-lookup"><span data-stu-id="89e10-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="89e10-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="89e10-395">PercentNiceTime</span></span> | <span data-ttu-id="89e10-396">Tiempo no está inactivo, porcentaje de hello dedicado con menor prioridad ("nice")</span><span class="sxs-lookup"><span data-stu-id="89e10-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="89e10-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="89e10-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="89e10-398">De momento no está inactivo, Hola porcentaje empleado en modo privilegiado (kernel)</span><span class="sxs-lookup"><span data-stu-id="89e10-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="89e10-399">Hello primero cuatro contadores deberían sumar too100%.</span><span class="sxs-lookup"><span data-stu-id="89e10-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="89e10-400">Hello última tres contadores también suma too100%; subdivide suma Hola de PercentProcessorTime, PercentIOWaitTime y PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="89e10-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="89e10-401">tooobtain una sola métrica se agrega a lo largo de todos los procesadores, establezca `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="89e10-402">tooobtain una métrica para un procesador específico, como el segundo procesador lógico Hola de un cuatro principales de máquina virtual, establece `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="89e10-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="89e10-403">Números de procesador lógico están en el intervalo de hello `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="89e10-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="89e10-404">métricas de Builtin para hello Memory (clase)</span><span class="sxs-lookup"><span data-stu-id="89e10-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="89e10-405">Hola Memory (clase) de métricas proporciona información acerca del uso de memoria, la paginación y el intercambio.</span><span class="sxs-lookup"><span data-stu-id="89e10-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="89e10-406">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-406">counter</span></span> | <span data-ttu-id="89e10-407">Significado</span><span class="sxs-lookup"><span data-stu-id="89e10-407">Meaning</span></span>
------- | -------
<span data-ttu-id="89e10-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="89e10-408">AvailableMemory</span></span> | <span data-ttu-id="89e10-409">Memoria física disponible en MiB</span><span class="sxs-lookup"><span data-stu-id="89e10-409">Available physical memory in MiB</span></span>
<span data-ttu-id="89e10-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="89e10-410">PercentAvailableMemory</span></span> | <span data-ttu-id="89e10-411">Memoria física disponible en forma de porcentaje del total de memoria</span><span class="sxs-lookup"><span data-stu-id="89e10-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="89e10-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="89e10-412">UsedMemory</span></span> | <span data-ttu-id="89e10-413">Memoria física en uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="89e10-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="89e10-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="89e10-414">PercentUsedMemory</span></span> | <span data-ttu-id="89e10-415">Memoria física en uso en forma de porcentaje del total de memoria</span><span class="sxs-lookup"><span data-stu-id="89e10-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="89e10-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="89e10-416">PagesPerSec</span></span> | <span data-ttu-id="89e10-417">Paginación total (lectura y escritura)</span><span class="sxs-lookup"><span data-stu-id="89e10-417">Total paging (read/write)</span></span>
<span data-ttu-id="89e10-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="89e10-418">PagesReadPerSec</span></span> | <span data-ttu-id="89e10-419">Páginas leídas desde la memoria auxiliar (archivo de intercambio, archivo de programa, archivo asignado, etc.)</span><span class="sxs-lookup"><span data-stu-id="89e10-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="89e10-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="89e10-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="89e10-421">Páginas escritas toobacking almacenan (archivo de intercambio, archivo asignado, etcetera.)</span><span class="sxs-lookup"><span data-stu-id="89e10-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="89e10-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="89e10-422">AvailableSwap</span></span> | <span data-ttu-id="89e10-423">Espacio de intercambio sin usar (MiB)</span><span class="sxs-lookup"><span data-stu-id="89e10-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="89e10-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="89e10-424">PercentAvailableSwap</span></span> | <span data-ttu-id="89e10-425">Espacio de intercambio sin usar en forma de porcentaje del total de intercambio</span><span class="sxs-lookup"><span data-stu-id="89e10-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="89e10-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="89e10-426">UsedSwap</span></span> | <span data-ttu-id="89e10-427">Espacio de intercambio (MiB) en uso</span><span class="sxs-lookup"><span data-stu-id="89e10-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="89e10-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="89e10-428">PercentUsedSwap</span></span> | <span data-ttu-id="89e10-429">Espacio de intercambio en uso en forma de porcentaje del total de intercambio</span><span class="sxs-lookup"><span data-stu-id="89e10-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="89e10-430">Esta clase de métricas tiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="89e10-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="89e10-431">atributo de "condición" Hello no tiene ningún valor útil y debe omitirse.</span><span class="sxs-lookup"><span data-stu-id="89e10-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="89e10-432">métricas de Builtin para hello clase de red</span><span class="sxs-lookup"><span data-stu-id="89e10-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="89e10-433">Hola clase red de métricas proporciona información acerca de la actividad de red en interfaces de red individuales de una desde el inicio.</span><span class="sxs-lookup"><span data-stu-id="89e10-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="89e10-434">LAD no expone las métricas de ancho de banda, las cuales pueden recuperarse a partir de métricas de host.</span><span class="sxs-lookup"><span data-stu-id="89e10-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="89e10-435">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-435">counter</span></span> | <span data-ttu-id="89e10-436">Significado</span><span class="sxs-lookup"><span data-stu-id="89e10-436">Meaning</span></span>
------- | -------
<span data-ttu-id="89e10-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="89e10-437">BytesTransmitted</span></span> | <span data-ttu-id="89e10-438">Total de bytes enviados desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-438">Total bytes sent since boot</span></span>
<span data-ttu-id="89e10-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="89e10-439">BytesReceived</span></span> | <span data-ttu-id="89e10-440">Total de bytes recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-440">Total bytes received since boot</span></span>
<span data-ttu-id="89e10-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="89e10-441">BytesTotal</span></span> | <span data-ttu-id="89e10-442">Total de bytes enviados o recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="89e10-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="89e10-443">PacketsTransmitted</span></span> | <span data-ttu-id="89e10-444">Total de paquetes enviados desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-444">Total packets sent since boot</span></span>
<span data-ttu-id="89e10-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="89e10-445">PacketsReceived</span></span> | <span data-ttu-id="89e10-446">Total de paquetes recibidos desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-446">Total packets received since boot</span></span>
<span data-ttu-id="89e10-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="89e10-447">TotalRxErrors</span></span> | <span data-ttu-id="89e10-448">Número de errores de recepción desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-448">Number of receive errors since boot</span></span>
<span data-ttu-id="89e10-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="89e10-449">TotalTxErrors</span></span> | <span data-ttu-id="89e10-450">Número de errores de transmisión desde el arranque</span><span class="sxs-lookup"><span data-stu-id="89e10-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="89e10-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="89e10-451">TotalCollisions</span></span> | <span data-ttu-id="89e10-452">Número de conflictos notificados por los puertos de red de Hola desde el inicio</span><span class="sxs-lookup"><span data-stu-id="89e10-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="89e10-453">Aunque esta clase está instanciada, LAD no admite la captura de agregados de métricas Network de todos los dispositivos de red.</span><span class="sxs-lookup"><span data-stu-id="89e10-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="89e10-454">conjunto de métricas de hello tooobtain para una interfaz específica, como eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="89e10-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="89e10-455">métricas de Builtin para hello Filesystem (clase)</span><span class="sxs-lookup"><span data-stu-id="89e10-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="89e10-456">Hola clase Filesystem de métricas proporciona información sobre el uso del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="89e10-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="89e10-457">Valores absolutos y el porcentaje se notifican como se haría usuario ordinaria tooan mostrado (no raíz).</span><span class="sxs-lookup"><span data-stu-id="89e10-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="89e10-458">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-458">counter</span></span> | <span data-ttu-id="89e10-459">Significado</span><span class="sxs-lookup"><span data-stu-id="89e10-459">Meaning</span></span>
------- | -------
<span data-ttu-id="89e10-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="89e10-460">FreeSpace</span></span> | <span data-ttu-id="89e10-461">Espacio disponible en disco en bytes</span><span class="sxs-lookup"><span data-stu-id="89e10-461">Available disk space in bytes</span></span>
<span data-ttu-id="89e10-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="89e10-462">UsedSpace</span></span> | <span data-ttu-id="89e10-463">Espacio usado en disco en bytes</span><span class="sxs-lookup"><span data-stu-id="89e10-463">Used disk space in bytes</span></span>
<span data-ttu-id="89e10-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="89e10-464">PercentFreeSpace</span></span> | <span data-ttu-id="89e10-465">Porcentaje de espacio libre</span><span class="sxs-lookup"><span data-stu-id="89e10-465">Percentage free space</span></span>
<span data-ttu-id="89e10-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="89e10-466">PercentUsedSpace</span></span> | <span data-ttu-id="89e10-467">Porcentaje de espacio usado</span><span class="sxs-lookup"><span data-stu-id="89e10-467">Percentage used space</span></span>
<span data-ttu-id="89e10-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="89e10-468">PercentFreeInodes</span></span> | <span data-ttu-id="89e10-469">Porcentaje de inodes sin usar</span><span class="sxs-lookup"><span data-stu-id="89e10-469">Percentage of unused inodes</span></span>
<span data-ttu-id="89e10-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="89e10-470">PercentUsedInodes</span></span> | <span data-ttu-id="89e10-471">Porcentaje de inodes asignados (en uso) sumado de todos los sistemas de archivos</span><span class="sxs-lookup"><span data-stu-id="89e10-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="89e10-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-472">BytesReadPerSecond</span></span> | <span data-ttu-id="89e10-473">Bytes leídos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-473">Bytes read per second</span></span>
<span data-ttu-id="89e10-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="89e10-475">Bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-475">Bytes written per second</span></span>
<span data-ttu-id="89e10-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-476">BytesPerSecond</span></span> | <span data-ttu-id="89e10-477">Bytes leídos o escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-477">Bytes read or written per second</span></span>
<span data-ttu-id="89e10-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-478">ReadsPerSecond</span></span> | <span data-ttu-id="89e10-479">Operaciones de lectura por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-479">Read operations per second</span></span>
<span data-ttu-id="89e10-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-480">WritesPerSecond</span></span> | <span data-ttu-id="89e10-481">Operaciones de escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-481">Write operations per second</span></span>
<span data-ttu-id="89e10-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-482">TransfersPerSecond</span></span> | <span data-ttu-id="89e10-483">Operaciones de lectura o escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-483">Read or write operations per second</span></span>

<span data-ttu-id="89e10-484">Los valores agregados de todos los archivos del sistema pueden obtenerse estableciendo `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="89e10-485">Los valores para un sistema de archivos montado específico, como "/mnt", pueden obtenerse estableciendo `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="89e10-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="89e10-486">métricas de Builtin para hello clase de disco</span><span class="sxs-lookup"><span data-stu-id="89e10-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="89e10-487">Hola, clase de disco de las métricas de proporciona información sobre el uso de dispositivos de disco.</span><span class="sxs-lookup"><span data-stu-id="89e10-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="89e10-488">Estas estadísticas aplican toohello toda la unidad.</span><span class="sxs-lookup"><span data-stu-id="89e10-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="89e10-489">Si hay varios sistemas de archivos en un dispositivo, contadores de Hola para dicho dispositivo son, de hecho, agregan a lo largo de todas ellas.</span><span class="sxs-lookup"><span data-stu-id="89e10-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="89e10-490">counter</span><span class="sxs-lookup"><span data-stu-id="89e10-490">counter</span></span> | <span data-ttu-id="89e10-491">Significado</span><span class="sxs-lookup"><span data-stu-id="89e10-491">Meaning</span></span>
------- | -------
<span data-ttu-id="89e10-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-492">ReadsPerSecond</span></span> | <span data-ttu-id="89e10-493">Operaciones de lectura por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-493">Read operations per second</span></span>
<span data-ttu-id="89e10-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-494">WritesPerSecond</span></span> | <span data-ttu-id="89e10-495">Operaciones de escritura por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-495">Write operations per second</span></span>
<span data-ttu-id="89e10-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-496">TransfersPerSecond</span></span> | <span data-ttu-id="89e10-497">Total de operaciones por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-497">Total operations per second</span></span>
<span data-ttu-id="89e10-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="89e10-498">AverageReadTime</span></span> | <span data-ttu-id="89e10-499">Promedio de segundos por operación de lectura</span><span class="sxs-lookup"><span data-stu-id="89e10-499">Average seconds per read operation</span></span>
<span data-ttu-id="89e10-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="89e10-500">AverageWriteTime</span></span> | <span data-ttu-id="89e10-501">Promedio de segundos por operación de escritura</span><span class="sxs-lookup"><span data-stu-id="89e10-501">Average seconds per write operation</span></span>
<span data-ttu-id="89e10-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="89e10-502">AverageTransferTime</span></span> | <span data-ttu-id="89e10-503">Promedio de segundos por operación</span><span class="sxs-lookup"><span data-stu-id="89e10-503">Average seconds per operation</span></span>
<span data-ttu-id="89e10-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="89e10-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="89e10-505">Promedio de operaciones de disco en cola</span><span class="sxs-lookup"><span data-stu-id="89e10-505">Average number of queued disk operations</span></span>
<span data-ttu-id="89e10-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="89e10-507">Número de bytes leídos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-507">Number of bytes read per second</span></span>
<span data-ttu-id="89e10-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="89e10-509">Número de bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-509">Number of bytes written per second</span></span>
<span data-ttu-id="89e10-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="89e10-510">BytesPerSecond</span></span> | <span data-ttu-id="89e10-511">Número de bytes leídos o escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="89e10-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="89e10-512">Los valores agregados de todos los discos pueden obtenerse estableciendo `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="89e10-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="89e10-513">conjunto de información de tooget para un dispositivo específico (por ejemplo, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="89e10-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="89e10-514">Instalación y configuración de LAD 3.0 a través de CLI</span><span class="sxs-lookup"><span data-stu-id="89e10-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="89e10-515">Suponiendo que es la configuración protegida en el archivo hello PrivateConfig.json y la información de configuración pública está en PublicConfig.json, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="89e10-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="89e10-516">comando de Hola se da por supuesto que se usa el modo de administración de recursos de Azure de hello (arm) de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="89e10-517">tooconfigure LAD para implementación clásica del modelo de máquinas virtuales (ASM), cambiar demasiado el modo "asm" (`azure config mode asm`) y se omite el nombre del grupo de recursos de hello en comando Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="89e10-518">Para obtener más información, vea hello [documentación de CLI multiplataforma](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="89e10-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="89e10-519">Una configuración de LAD 3.0 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89e10-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="89e10-520">Se basa en hello anteriores definiciones, aquí un ejemplo de configuración de extensión de LAD 3.0 con algunas explicaciones.</span><span class="sxs-lookup"><span data-stu-id="89e10-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="89e10-521">tooapply este ejemplo tooyour caso, debe usar su propio nombre de cuenta de almacenamiento, la cuenta de token de SAS y tokens EventHubs SAS.</span><span class="sxs-lookup"><span data-stu-id="89e10-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="89e10-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="89e10-522">PrivateConfig.json</span></span>

<span data-ttu-id="89e10-523">Estos valores privados configuran lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="89e10-523">These private settings configure:</span></span>

* <span data-ttu-id="89e10-524">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="89e10-524">a storage account</span></span>
* <span data-ttu-id="89e10-525">Un token de SAS de cuenta que coincida</span><span class="sxs-lookup"><span data-stu-id="89e10-525">a matching account SAS token</span></span>
* <span data-ttu-id="89e10-526">Varios receptores (Json BLOB o Event Hubs con tokens SAS)</span><span class="sxs-lookup"><span data-stu-id="89e10-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="89e10-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="89e10-527">PublicConfig.json</span></span>

<span data-ttu-id="89e10-528">Estos valores públicos hacen que LAD:</span><span class="sxs-lookup"><span data-stu-id="89e10-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="89e10-529">Cargar las métricas de porcentaje de tiempo de procesador y espacio en disco utilizado toohello `WADMetrics*` tabla</span><span class="sxs-lookup"><span data-stu-id="89e10-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="89e10-530">Cargar mensajes de syslog facility "usuario" y la gravedad "información" toohello `LinuxSyslog*` tabla</span><span class="sxs-lookup"><span data-stu-id="89e10-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="89e10-531">Cargar sin formato OMI consulta resultados (PercentProcessorTime y PercentIdleTime) toohello denominado `LinuxCPU` tabla</span><span class="sxs-lookup"><span data-stu-id="89e10-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="89e10-532">Cargar anexadas líneas en el archivo `/var/log/myladtestlog` toohello `MyLadTestLog` tabla</span><span class="sxs-lookup"><span data-stu-id="89e10-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="89e10-533">En cualquier caso, también se cargan datos en:</span><span class="sxs-lookup"><span data-stu-id="89e10-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="89e10-534">Almacenamiento de blobs de Azure (nombre del contenedor es tal como se define en el receptor de hello JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="89e10-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="89e10-535">Punto de conexión EventHubs (según lo especificado en el receptor de hello EventHubs)</span><span class="sxs-lookup"><span data-stu-id="89e10-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

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

<span data-ttu-id="89e10-536">Hola `resourceId` Hola configuración debe coincidir con que de escalas de máquina virtual VM u Hola Hola establecido.</span><span class="sxs-lookup"><span data-stu-id="89e10-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="89e10-537">Métricas de la plataforma Windows Azure gráficos y las alertas sabe Hola resourceId de hello VM que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="89e10-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="89e10-538">Espera datos de hello toofind para la máquina virtual con la clave de búsqueda de hello resourceId Hola.</span><span class="sxs-lookup"><span data-stu-id="89e10-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="89e10-539">Si usa el escalado automático de Azure, resourceId hello en la configuración de escalado automático de hello debe coincidir con resourceId hello usa LAD.</span><span class="sxs-lookup"><span data-stu-id="89e10-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="89e10-540">Hola resourceId se integra en nombres de Hola de JsonBlobs escrito LAD.</span><span class="sxs-lookup"><span data-stu-id="89e10-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="89e10-541">Consulta de los datos</span><span class="sxs-lookup"><span data-stu-id="89e10-541">View your data</span></span>

<span data-ttu-id="89e10-542">Usar datos de rendimiento de tooview portal Azure de Hola o establecer alertas:</span><span class="sxs-lookup"><span data-stu-id="89e10-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![imagen](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="89e10-544">Hola `performanceCounters` datos siempre se almacenan en una tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="89e10-545">Las API de Azure Storage están disponibles para múltiples lenguajes y plataformas.</span><span class="sxs-lookup"><span data-stu-id="89e10-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="89e10-546">Datos que se envían los receptores tooJsonBlob se almacenan en blobs en la cuenta de almacenamiento de hello denominada Hola [protegido configuración](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="89e10-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="89e10-547">Puede consumir datos de blob de hello mediante las API de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e10-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="89e10-548">Además, puede usar estos datos de Hola de tooaccess de herramientas de interfaz de usuario en el almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="89e10-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="89e10-549">Explorador de servidores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89e10-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="89e10-550">[Explorador de Microsoft Azure Storage](https://azurestorageexplorer.codeplex.com/ "Explorador de Azure Storage").</span><span class="sxs-lookup"><span data-stu-id="89e10-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="89e10-551">Esta instantánea de una sesión de Microsoft Azure Storage Explorer muestra hello genera tablas de almacenamiento de Azure y contenedores desde una extensión de LAD 3.0 configurada correctamente en una máquina virtual de prueba.</span><span class="sxs-lookup"><span data-stu-id="89e10-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="89e10-552">imagen de Hello no coincide exactamente con hello [configuración del ejemplo LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="89e10-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![imagen](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="89e10-554">Vea Hola relevante [EventHubs documentación](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn cómo tooconsume mensajes publican tooan EventHubs extremo.</span><span class="sxs-lookup"><span data-stu-id="89e10-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89e10-555">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89e10-555">Next steps</span></span>

* <span data-ttu-id="89e10-556">Crear alertas métricas en [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para las métricas de Hola que recopila.</span><span class="sxs-lookup"><span data-stu-id="89e10-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="89e10-557">Cree [gráficos de supervisión](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para las métricas.</span><span class="sxs-lookup"><span data-stu-id="89e10-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="89e10-558">Obtenga información acerca de cómo demasiado[crear un conjunto de escalas de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) mediante el escalado automático toocontrol de métricas.</span><span class="sxs-lookup"><span data-stu-id="89e10-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
