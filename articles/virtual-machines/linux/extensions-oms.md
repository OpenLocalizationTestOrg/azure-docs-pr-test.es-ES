---
title: "Extensión de máquina virtual de Azure y OMS para Linux | Microsoft Docs"
description: "Implemente el agente de OMS en la máquina virtual Linux con una extensión de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 138fc8c98ea6f409b28407b20851c96ecc618b09
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="4fcee-103">Extensión de máquina virtual de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="4fcee-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="4fcee-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4fcee-104">Overview</span></span>

<span data-ttu-id="4fcee-105">Operations Management Suite (OMS) proporciona funcionalidades de corrección de alertas, supervisión y envío de alertas a todos los recursos locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="4fcee-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="4fcee-106">Microsoft, como editor de la extensión de máquina virtual del agente de OMS para Linux, es quien presta los servicios de soporte técnico para esta solución.</span><span class="sxs-lookup"><span data-stu-id="4fcee-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="4fcee-107">La extensión instala al agente de OMS en máquinas virtuales de Azure e inscribe dichas máquinas virtuales en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="4fcee-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="4fcee-108">En este documento se especifican las plataformas compatibles, configuraciones y opciones de implementación de la extensión de máquina virtual de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4fcee-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fcee-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4fcee-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="4fcee-110">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="4fcee-110">Operating system</span></span>

<span data-ttu-id="4fcee-111">La extensión del agente de OMS puede ejecutarse en estas distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="4fcee-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="4fcee-112">Distribución</span><span class="sxs-lookup"><span data-stu-id="4fcee-112">Distribution</span></span> | <span data-ttu-id="4fcee-113">Versión</span><span class="sxs-lookup"><span data-stu-id="4fcee-113">Version</span></span> |
|---|---|
| <span data-ttu-id="4fcee-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="4fcee-114">CentOS Linux</span></span> | <span data-ttu-id="4fcee-115">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="4fcee-115">5, 6, and 7</span></span> |
| <span data-ttu-id="4fcee-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="4fcee-116">Oracle Linux</span></span> | <span data-ttu-id="4fcee-117">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="4fcee-117">5, 6, and 7</span></span> |
| <span data-ttu-id="4fcee-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="4fcee-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="4fcee-119">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="4fcee-119">5, 6 and 7</span></span> |
| <span data-ttu-id="4fcee-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="4fcee-120">Debian GNU/Linux</span></span> | <span data-ttu-id="4fcee-121">6, 7 y 8</span><span class="sxs-lookup"><span data-stu-id="4fcee-121">6, 7, and 8</span></span> |
| <span data-ttu-id="4fcee-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4fcee-122">Ubuntu</span></span> | <span data-ttu-id="4fcee-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4fcee-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="4fcee-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="4fcee-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="4fcee-125">11 y 12</span><span class="sxs-lookup"><span data-stu-id="4fcee-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="4fcee-126">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="4fcee-126">Internet connectivity</span></span>

<span data-ttu-id="4fcee-127">La extensión del agente de OMS para Linux requiere que la máquina virtual de destino esté conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="4fcee-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="4fcee-128">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="4fcee-128">Extension schema</span></span>

<span data-ttu-id="4fcee-129">El siguiente JSON muestra el esquema para la extensión del agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="4fcee-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="4fcee-130">La extensión requiere el identificador y la clave del área de trabajo de OMS de destino, valores que se pueden encontrar en el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="4fcee-130">The extension requires the workspace ID and workspace key from the target OMS workspace; these values can be found in the OMS portal.</span></span> <span data-ttu-id="4fcee-131">Como la clave del área de trabajo debe tratarse como datos confidenciales, debe almacenarse en una configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="4fcee-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="4fcee-132">Los datos de configuración protegida de la extensión de VM de Azure están cifrados y solo se descifran en la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="4fcee-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="4fcee-133">Tenga en cuenta que **workspaceId** y **workspaceKey** distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4fcee-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="4fcee-134">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="4fcee-134">Property values</span></span>

| <span data-ttu-id="4fcee-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="4fcee-135">Name</span></span> | <span data-ttu-id="4fcee-136">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="4fcee-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="4fcee-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4fcee-137">apiVersion</span></span> | <span data-ttu-id="4fcee-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="4fcee-138">2015-06-15</span></span> |
| <span data-ttu-id="4fcee-139">publisher</span><span class="sxs-lookup"><span data-stu-id="4fcee-139">publisher</span></span> | <span data-ttu-id="4fcee-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="4fcee-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="4fcee-141">type</span><span class="sxs-lookup"><span data-stu-id="4fcee-141">type</span></span> | <span data-ttu-id="4fcee-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="4fcee-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="4fcee-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="4fcee-143">typeHandlerVersion</span></span> | <span data-ttu-id="4fcee-144">1.4</span><span class="sxs-lookup"><span data-stu-id="4fcee-144">1.4</span></span> |
| <span data-ttu-id="4fcee-145">workspaceId (p.ej)</span><span class="sxs-lookup"><span data-stu-id="4fcee-145">workspaceId (e.g)</span></span> | <span data-ttu-id="4fcee-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="4fcee-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="4fcee-147">workspaceKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="4fcee-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="4fcee-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="4fcee-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="4fcee-149">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="4fcee-149">Template deployment</span></span>

<span data-ttu-id="4fcee-150">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fcee-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="4fcee-151">Las plantillas resultan ideales al implementar una o varias máquinas virtuales que requieren configurarse tras la implementación, por ejemplo, para incorporarse a OMS.</span><span class="sxs-lookup"><span data-stu-id="4fcee-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="4fcee-152">Puede encontrar una plantilla de Resource Manager de ejemplo que incluye la extensión de VM del agente de OMS en la [Galería de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="4fcee-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="4fcee-153">La configuración JSON de una extensión de máquina virtual puede estar anidada en el recurso de máquina virtual o colocada en la raíz o nivel superior de una plantilla JSON de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fcee-153">The JSON configuration for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="4fcee-154">La colocación de la configuración JSON afecta al valor del nombre y tipo del recurso.</span><span class="sxs-lookup"><span data-stu-id="4fcee-154">The placement of the JSON configuration affects the value of the resource name and type.</span></span> <span data-ttu-id="4fcee-155">Para obtener más información, consulte el artículo sobre cómo [establecer el nombre y el tipo de recursos secundarios](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="4fcee-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="4fcee-156">En el siguiente ejemplo se da por supuesto que la extensión OMS está anidada dentro de los recursos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fcee-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="4fcee-157">Cuando se anidan los recursos de extensión, la plantilla JSON se coloca en el objeto `"resources": []` de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fcee-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="4fcee-158">Al colocar la plantilla JSON de la extensión en la raíz de la plantilla, el nombre de recurso incluye una referencia a la máquina virtual principal, y el tipo refleja la configuración anidada.</span><span class="sxs-lookup"><span data-stu-id="4fcee-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="4fcee-159">Implementación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4fcee-159">Azure CLI deployment</span></span>

<span data-ttu-id="4fcee-160">La CLI de Azure puede utilizarse para implementar la extensión de máquina virtual del agente de OMS en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fcee-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="4fcee-161">Reemplace la clave OMS y el identificador de OMS por los de su área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="4fcee-161">Replace the OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="4fcee-162">Solución de problemas y asistencia</span><span class="sxs-lookup"><span data-stu-id="4fcee-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="4fcee-163">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="4fcee-163">Troubleshoot</span></span>

<span data-ttu-id="4fcee-164">Los datos sobre el estado de las implementaciones de extensiones pueden recuperarse desde Azure Portal y mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fcee-164">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="4fcee-165">Para ver el estado de implementación de las extensiones de una máquina virtual determinada, ejecute el comando siguiente con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fcee-165">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="4fcee-166">El resultado de la ejecución de las extensiones se registra en el archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fcee-166">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="4fcee-167">Códigos de error y su significado</span><span class="sxs-lookup"><span data-stu-id="4fcee-167">Error codes and their meanings</span></span>

| <span data-ttu-id="4fcee-168">Código de error</span><span class="sxs-lookup"><span data-stu-id="4fcee-168">Error Code</span></span> | <span data-ttu-id="4fcee-169">Significado</span><span class="sxs-lookup"><span data-stu-id="4fcee-169">Meaning</span></span> | <span data-ttu-id="4fcee-170">Acción posible</span><span class="sxs-lookup"><span data-stu-id="4fcee-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="4fcee-171">10</span><span class="sxs-lookup"><span data-stu-id="4fcee-171">10</span></span> | <span data-ttu-id="4fcee-172">La máquina virtual ya está conectada a un área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="4fcee-172">VM is already connected to an OMS workspace</span></span> | <span data-ttu-id="4fcee-173">Para conectar la máquina virtual al área de trabajo especificada en el esquema de extensión, establezca stopOnMultipleConnections en false en la configuración pública o quite esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="4fcee-173">To connect the VM to the workspace specified in the extension schema, set stopOnMultipleConnections to false in public settings or remove this property.</span></span> <span data-ttu-id="4fcee-174">Esta máquina virtual se factura una vez por cada área de trabajo a la que se conecta.</span><span class="sxs-lookup"><span data-stu-id="4fcee-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="4fcee-175">11</span><span class="sxs-lookup"><span data-stu-id="4fcee-175">11</span></span> | <span data-ttu-id="4fcee-176">Configuración no válida proporcionada a la extensión</span><span class="sxs-lookup"><span data-stu-id="4fcee-176">Invalid config provided to the extension</span></span> | <span data-ttu-id="4fcee-177">Siga los ejemplos anteriores para configurar todos los valores de propiedad necesarios para la implementación.</span><span class="sxs-lookup"><span data-stu-id="4fcee-177">Follow the preceding examples to set all property values necessary for deployment.</span></span> |
| <span data-ttu-id="4fcee-178">12</span><span class="sxs-lookup"><span data-stu-id="4fcee-178">12</span></span> | <span data-ttu-id="4fcee-179">El administrador de paquetes de dpkg está bloqueado</span><span class="sxs-lookup"><span data-stu-id="4fcee-179">The dpkg package manager is locked</span></span> | <span data-ttu-id="4fcee-180">Asegúrese de que todas las operaciones de actualización de dpkg en el equipo han finalizado e intente de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4fcee-180">Make sure all dpkg update operations on the machine have finished and retry.</span></span> |
| <span data-ttu-id="4fcee-181">20 |</span><span class="sxs-lookup"><span data-stu-id="4fcee-181">20</span></span> | <span data-ttu-id="4fcee-182">Habilitar llamado antes de tiempo</span><span class="sxs-lookup"><span data-stu-id="4fcee-182">Enable called prematurely</span></span> | <span data-ttu-id="4fcee-183">[Actualice el agente de Linux de Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) a la versión más reciente disponible.</span><span class="sxs-lookup"><span data-stu-id="4fcee-183">[Update the Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to the latest available version.</span></span> |
| <span data-ttu-id="4fcee-184">51</span><span class="sxs-lookup"><span data-stu-id="4fcee-184">51</span></span> | <span data-ttu-id="4fcee-185">Esta extensión no se admite en el sistema operativo de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4fcee-185">This extension is not supported on the VM's operation system</span></span> | |
| <span data-ttu-id="4fcee-186">55</span><span class="sxs-lookup"><span data-stu-id="4fcee-186">55</span></span> | <span data-ttu-id="4fcee-187">No se puede conectar con el servicio Microsoft Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="4fcee-187">Cannot connect to the Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="4fcee-188">Compruebe que el sistema tiene acceso a Internet o que se ha proporcionado un servidor proxy HTTP válido.</span><span class="sxs-lookup"><span data-stu-id="4fcee-188">Check that the system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="4fcee-189">Además, compruebe la validez del identificador del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4fcee-189">Additionally, check the correctness of the workspace ID.</span></span> |

<span data-ttu-id="4fcee-190">Puede encontrar información adicional de solución de problemas en la [Guía de solución de problemas del agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="4fcee-190">Additional troubleshooting information can be found on the [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="4fcee-191">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="4fcee-191">Support</span></span>

<span data-ttu-id="4fcee-192">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en los [foros de MSDN Azure o Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="4fcee-192">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="4fcee-193">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fcee-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="4fcee-194">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione Obtener soporte.</span><span class="sxs-lookup"><span data-stu-id="4fcee-194">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="4fcee-195">Para obtener información sobre el uso del soporte técnico, lea las [Preguntas más frecuentes de soporte técnico de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="4fcee-195">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
