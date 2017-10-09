---
title: Grupos de recursos de Azure que contienen las extensiones de VM aaaExporting | Documentos de Microsoft
description: "Exportar plantillas de Resource Manager que incluyen extensiones de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="b7d50-103">Exportación de grupos de recursos que contienen extensiones de VM</span><span class="sxs-lookup"><span data-stu-id="b7d50-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="b7d50-104">Los grupos de recursos de Azure se pueden exportar a una nueva plantilla de Resource Manager que, después, se puede volver a implementar.</span><span class="sxs-lookup"><span data-stu-id="b7d50-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="b7d50-105">Hello proceso de exportación interpreta los recursos existentes y crea una plantilla de administrador de recursos que cuando se implementa da como resultado un grupo de recursos similares.</span><span class="sxs-lookup"><span data-stu-id="b7d50-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="b7d50-106">Cuando se usa la opción de exportación de grupo de recursos de hello en un grupo de recursos que contiene las extensiones de máquina Virtual, varios elementos necesidad toobe había considerado como compatibilidad de extensión y protegido configuración.</span><span class="sxs-lookup"><span data-stu-id="b7d50-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="b7d50-107">Este documento se explica cómo funciona la Hola proceso de exportación del grupo de recursos con respecto a las extensiones de máquina virtual, incluida una lista de extensiones admitidas y detalles sobre el control de los datos protegen.</span><span class="sxs-lookup"><span data-stu-id="b7d50-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="b7d50-108">Extensiones de máquina virtual admitidas</span><span class="sxs-lookup"><span data-stu-id="b7d50-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="b7d50-109">Hay muchas extensiones de máquina virtual disponibles.</span><span class="sxs-lookup"><span data-stu-id="b7d50-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="b7d50-110">No todas las extensiones se pueden exportar a una plantilla de administrador de recursos mediante la característica de "Script de automatización" Hola.</span><span class="sxs-lookup"><span data-stu-id="b7d50-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="b7d50-111">Si no se admite una extensión de máquina virtual, debe toobe manualmente vuelve a colocar en plantilla exportada Hola.</span><span class="sxs-lookup"><span data-stu-id="b7d50-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="b7d50-112">Hello siguientes extensiones se pueden exportar con la característica de secuencia de comandos de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7d50-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="b7d50-113">Extensión</span><span class="sxs-lookup"><span data-stu-id="b7d50-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="b7d50-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="b7d50-114">Acronis Backup</span></span> | <span data-ttu-id="b7d50-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="b7d50-115">Datadog Windows Agent</span></span> | <span data-ttu-id="b7d50-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-116">OS Patching For Linux</span></span> | <span data-ttu-id="b7d50-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="b7d50-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-118">Acronis Backup Linux</span></span> | <span data-ttu-id="b7d50-119">Extensión de Docker</span><span class="sxs-lookup"><span data-stu-id="b7d50-119">Docker Extension</span></span> | <span data-ttu-id="b7d50-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="b7d50-120">Puppet Agent</span></span> |
| <span data-ttu-id="b7d50-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="b7d50-121">Bg Info</span></span> | <span data-ttu-id="b7d50-122">Extensión DSC</span><span class="sxs-lookup"><span data-stu-id="b7d50-122">DSC Extension</span></span> | <span data-ttu-id="b7d50-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="b7d50-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="b7d50-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="b7d50-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-125">Dynatrace Linux</span></span> | <span data-ttu-id="b7d50-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="b7d50-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="b7d50-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="b7d50-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="b7d50-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="b7d50-128">Dynatrace Windows</span></span> | <span data-ttu-id="b7d50-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="b7d50-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="b7d50-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="b7d50-130">Chef Client</span></span> | <span data-ttu-id="b7d50-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="b7d50-131">HPE Security Application Defender</span></span> | <span data-ttu-id="b7d50-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="b7d50-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="b7d50-133">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="b7d50-133">Custom Script</span></span> | <span data-ttu-id="b7d50-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="b7d50-134">IaaS Antimalware</span></span> | <span data-ttu-id="b7d50-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="b7d50-136">Extensión Custom Script</span><span class="sxs-lookup"><span data-stu-id="b7d50-136">Custom Script Extension</span></span> | <span data-ttu-id="b7d50-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b7d50-137">IaaS Diagnostics</span></span> | <span data-ttu-id="b7d50-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-138">VM Access For Linux</span></span> |
| <span data-ttu-id="b7d50-139">Script personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-139">Custom Script for Linux</span></span> | <span data-ttu-id="b7d50-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="b7d50-140">Linux Chef Client</span></span> | <span data-ttu-id="b7d50-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="b7d50-141">VM Access For Linux</span></span> |
| <span data-ttu-id="b7d50-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="b7d50-142">Datadog Linux Agent</span></span> | <span data-ttu-id="b7d50-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="b7d50-143">Linux Diagnostic</span></span> | <span data-ttu-id="b7d50-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="b7d50-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="b7d50-145">Exportar Hola grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b7d50-145">Export hello Resource Group</span></span>

<span data-ttu-id="b7d50-146">tooexport un grupo de recursos en una plantilla reutilizable, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="b7d50-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="b7d50-147">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b7d50-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="b7d50-148">En el menú del concentrador de hello, haga clic en grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="b7d50-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="b7d50-149">Seleccione el grupo de recursos de destino de hello en lista de Hola</span><span class="sxs-lookup"><span data-stu-id="b7d50-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="b7d50-150">En la hoja de grupo de recursos de hello, haga clic en Script de automatización</span><span class="sxs-lookup"><span data-stu-id="b7d50-150">In hello Resource Group blade, click Automation Script</span></span>

![Exportación de plantilla](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="b7d50-152">Hello secuencia de comandos de Azure Resource Manager automatizaciones genera una plantilla de administrador de recursos, un archivo de parámetros y varias secuencias de comandos de implementación de ejemplo como PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d50-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="b7d50-153">En este momento, se puede descargar plantilla exportada hello mediante el botón de descarga de hello, agrega como una biblioteca de plantillas de toohello plantilla nuevo o volver a implementar mediante Hola botón implementar.</span><span class="sxs-lookup"><span data-stu-id="b7d50-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="b7d50-154">Definición de la configuración protegida</span><span class="sxs-lookup"><span data-stu-id="b7d50-154">Configure protected settings</span></span>

<span data-ttu-id="b7d50-155">Muchas extensiones de máquina virtual de Azure incluyen una configuración protegida, que cifra los datos confidenciales, como credenciales y cadenas de configuración.</span><span class="sxs-lookup"><span data-stu-id="b7d50-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="b7d50-156">Configuración protegida no se exporta con script de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7d50-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="b7d50-157">Si toobe volver a insertar en hello es necesario la configuración protegida, es necesario exporta con plantilla.</span><span class="sxs-lookup"><span data-stu-id="b7d50-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="b7d50-158">Paso 1: Quitar parámetro de plantilla</span><span class="sxs-lookup"><span data-stu-id="b7d50-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="b7d50-159">Cuando Hola que se exporta el grupo de recursos, un parámetro de plantilla solo se crea tooprovide un toohello valor exporta configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="b7d50-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="b7d50-160">Este parámetro se puede quitar.</span><span class="sxs-lookup"><span data-stu-id="b7d50-160">This parameter can be removed.</span></span> <span data-ttu-id="b7d50-161">parámetro de hello tooremove, buscar a través de la lista de parámetros de Hola y eliminar parámetro hello que comprueba el ejemplo JSON toothis similar.</span><span class="sxs-lookup"><span data-stu-id="b7d50-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="b7d50-162">Paso 2: Obtener propiedades de configuración protegida</span><span class="sxs-lookup"><span data-stu-id="b7d50-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="b7d50-163">Dado que cada configuración protegido tiene un conjunto de propiedades necesarias, una lista de estas propiedades necesario toobe recopilada.</span><span class="sxs-lookup"><span data-stu-id="b7d50-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="b7d50-164">Cada parámetro de configuración protegida de hello puede encontrarse en hello [esquema del Administrador de recursos de Azure en GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="b7d50-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="b7d50-165">Este esquema incluye solo los conjuntos de parámetros de Hola para las extensiones de hello indicadas en la sección de información general de Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="b7d50-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="b7d50-166">Desde dentro de repositorio de esquema de hello, busque extensión Hola deseado, en este ejemplo `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="b7d50-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="b7d50-167">Una vez Hola extensiones `protectedSettings` objeto se ha localizado, tome nota de cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="b7d50-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="b7d50-168">En el ejemplo de Hola de hello `IaasDiagnostic` Hola de extensión, requieren parámetros son `storageAccountName`, `storageAccountKey`, y `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="b7d50-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="b7d50-169">Paso 3: volver a crear la configuración de hello protegido</span><span class="sxs-lookup"><span data-stu-id="b7d50-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="b7d50-170">En Hola plantilla exportada, busque `protectedSettings` y reemplazar Hola exportado protegido al establecer un objeto con uno nuevo que incluye parámetros de extensión de hello necesario y un valor para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="b7d50-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="b7d50-171">En el ejemplo de Hola de hello `IaasDiagnostic` extensión, Hola nueva protegido establecer la configuración tendrá el aspecto siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b7d50-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="b7d50-172">recursos de extensión final Hello tiene un aspecto similar toohello siguiente JSON de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b7d50-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="b7d50-173">Si utiliza valores de propiedad de tooprovide de parámetros de plantilla, estos necesitan toobe creado.</span><span class="sxs-lookup"><span data-stu-id="b7d50-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="b7d50-174">Al crear parámetros de plantilla para los valores de configuración protegida, que seguro Hola de toouse `SecureString` tipo de parámetro para que se protegen los valores confidenciales.</span><span class="sxs-lookup"><span data-stu-id="b7d50-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="b7d50-175">Para más información sobre el uso de parámetros, consulte [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md) (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b7d50-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b7d50-176">En el ejemplo de Hola de hello `IaasDiagnostic` extensión, Hola parámetros siguientes se crea en la sección de parámetros de Hola de plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7d50-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="b7d50-177">En este momento, plantilla de hello puede implementarse mediante cualquier método de implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="b7d50-177">At this point, hello template can be deployed using any template deployment method.</span></span>
