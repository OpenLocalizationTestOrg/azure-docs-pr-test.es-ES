---
title: "extensión de máquina virtual de Azure para Linux aaaOMS | Documentos de Microsoft"
description: "Implementar el agente de OMS de hello en máquina virtual de Linux con una extensión de máquina virtual."
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
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="91b59-103">Extensión de máquina virtual de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="91b59-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="91b59-104">Información general</span><span class="sxs-lookup"><span data-stu-id="91b59-104">Overview</span></span>

<span data-ttu-id="91b59-105">Operations Management Suite (OMS) proporciona funcionalidades de corrección de alertas, supervisión y envío de alertas a todos los recursos locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="91b59-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="91b59-106">Hola extensión de máquina virtual de agente de OMS para Linux se publica y compatible con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91b59-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="91b59-107">extensión de Hello instala el agente OMS de hello en máquinas virtuales de Azure e inscribe máquinas virtuales en un área de trabajo OMS existente.</span><span class="sxs-lookup"><span data-stu-id="91b59-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="91b59-108">Este Hola de detalles de documento admite plataformas, configuraciones y opciones de implementación para hello extensión de máquina virtual OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="91b59-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91b59-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91b59-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="91b59-110">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="91b59-110">Operating system</span></span>

<span data-ttu-id="91b59-111">Hola extensión del agente de OMS se pueden ejecutar con las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="91b59-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="91b59-112">Distribución</span><span class="sxs-lookup"><span data-stu-id="91b59-112">Distribution</span></span> | <span data-ttu-id="91b59-113">Versión</span><span class="sxs-lookup"><span data-stu-id="91b59-113">Version</span></span> |
|---|---|
| <span data-ttu-id="91b59-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="91b59-114">CentOS Linux</span></span> | <span data-ttu-id="91b59-115">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="91b59-115">5, 6, and 7</span></span> |
| <span data-ttu-id="91b59-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="91b59-116">Oracle Linux</span></span> | <span data-ttu-id="91b59-117">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="91b59-117">5, 6, and 7</span></span> |
| <span data-ttu-id="91b59-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="91b59-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="91b59-119">5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="91b59-119">5, 6 and 7</span></span> |
| <span data-ttu-id="91b59-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="91b59-120">Debian GNU/Linux</span></span> | <span data-ttu-id="91b59-121">6, 7 y 8</span><span class="sxs-lookup"><span data-stu-id="91b59-121">6, 7, and 8</span></span> |
| <span data-ttu-id="91b59-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="91b59-122">Ubuntu</span></span> | <span data-ttu-id="91b59-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="91b59-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="91b59-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="91b59-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="91b59-125">11 y 12</span><span class="sxs-lookup"><span data-stu-id="91b59-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="91b59-126">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="91b59-126">Internet connectivity</span></span>

<span data-ttu-id="91b59-127">Hola extensión del agente de OMS para Linux requiere esa máquina virtual de destino de hello es toohello conectado internet.</span><span class="sxs-lookup"><span data-stu-id="91b59-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="91b59-128">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="91b59-128">Extension schema</span></span>

<span data-ttu-id="91b59-129">Hello JSON siguiente muestra esquema Hola Hola extensión del agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="91b59-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="91b59-130">extensión de Hello requiere Hola área de trabajo área de trabajo y el identificador de clave de área de trabajo OMS Hola destino; Estos valores se pueden encontrar en el portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="91b59-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="91b59-131">Porque la clave de área de trabajo de hello debe tratarse como datos confidenciales, se deben almacenar en una configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="91b59-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="91b59-132">Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="91b59-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="91b59-133">Tenga en cuenta que **workspaceId** y **workspaceKey** distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="91b59-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="91b59-134">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="91b59-134">Property values</span></span>

| <span data-ttu-id="91b59-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="91b59-135">Name</span></span> | <span data-ttu-id="91b59-136">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="91b59-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="91b59-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="91b59-137">apiVersion</span></span> | <span data-ttu-id="91b59-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="91b59-138">2015-06-15</span></span> |
| <span data-ttu-id="91b59-139">publisher</span><span class="sxs-lookup"><span data-stu-id="91b59-139">publisher</span></span> | <span data-ttu-id="91b59-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="91b59-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="91b59-141">type</span><span class="sxs-lookup"><span data-stu-id="91b59-141">type</span></span> | <span data-ttu-id="91b59-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="91b59-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="91b59-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="91b59-143">typeHandlerVersion</span></span> | <span data-ttu-id="91b59-144">1.4</span><span class="sxs-lookup"><span data-stu-id="91b59-144">1.4</span></span> |
| <span data-ttu-id="91b59-145">workspaceId (p.ej)</span><span class="sxs-lookup"><span data-stu-id="91b59-145">workspaceId (e.g)</span></span> | <span data-ttu-id="91b59-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="91b59-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="91b59-147">workspaceKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="91b59-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="91b59-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="91b59-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="91b59-149">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="91b59-149">Template deployment</span></span>

<span data-ttu-id="91b59-150">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91b59-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="91b59-151">Las plantillas son ideales al implementar una o varias máquinas virtuales que requieren la configuración de implementación de post como tooOMS de incorporación.</span><span class="sxs-lookup"><span data-stu-id="91b59-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="91b59-152">Una plantilla de administrador de recursos de ejemplo que incluye la extensión de máquina virtual de agente de OMS de hello puede encontrarse en hello [Galería de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="91b59-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="91b59-153">configuración de JSON de Hola para una extensión de máquina virtual puede anidada dentro de recurso de la máquina virtual de hello, o se coloca en la raíz de Hola o de nivel superior de una plantilla JSON del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="91b59-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="91b59-154">colocación de Hola de configuración de JSON de hello afecta al valor de Hola de nombre de recurso de Hola y el tipo.</span><span class="sxs-lookup"><span data-stu-id="91b59-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="91b59-155">Para obtener más información, consulte el artículo sobre cómo [establecer el nombre y el tipo de recursos secundarios](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="91b59-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="91b59-156">Hello en el ejemplo siguiente se supone extensión OMS Hola está anidada dentro de recurso de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="91b59-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="91b59-157">Cuando se anidan los recursos de extensión de hello, Hola JSON se coloca en hello `"resources": []` objeto de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="91b59-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

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

<span data-ttu-id="91b59-158">Al colocar extensión Hola JSON en raíz de Hola de plantilla de hello, el nombre del recurso de hello incluye una máquina virtual de referencia toohello primario, y tipo hello refleja configuración anidados Hola.</span><span class="sxs-lookup"><span data-stu-id="91b59-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

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

## <a name="azure-cli-deployment"></a><span data-ttu-id="91b59-159">Implementación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="91b59-159">Azure CLI deployment</span></span>

<span data-ttu-id="91b59-160">Hola CLI de Azure puede ser usado toodeploy Hola VM de agente de OMS extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="91b59-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="91b59-161">Reemplazar la clave OMS de Hola y el Id. de OMS con los de su área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="91b59-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="91b59-162">Solución de problemas y asistencia</span><span class="sxs-lookup"><span data-stu-id="91b59-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="91b59-163">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="91b59-163">Troubleshoot</span></span>

<span data-ttu-id="91b59-164">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el uso de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="91b59-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="91b59-165">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute hello después de usar el comando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="91b59-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="91b59-166">Ejecución de la extensión de salida se ha iniciado toohello siguiente archivo:</span><span class="sxs-lookup"><span data-stu-id="91b59-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="91b59-167">Códigos de error y su significado</span><span class="sxs-lookup"><span data-stu-id="91b59-167">Error codes and their meanings</span></span>

| <span data-ttu-id="91b59-168">Código de error</span><span class="sxs-lookup"><span data-stu-id="91b59-168">Error Code</span></span> | <span data-ttu-id="91b59-169">Significado</span><span class="sxs-lookup"><span data-stu-id="91b59-169">Meaning</span></span> | <span data-ttu-id="91b59-170">Acción posible</span><span class="sxs-lookup"><span data-stu-id="91b59-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="91b59-171">10</span><span class="sxs-lookup"><span data-stu-id="91b59-171">10</span></span> | <span data-ttu-id="91b59-172">Máquina virtual ya está conectado tooan área de trabajo OMS</span><span class="sxs-lookup"><span data-stu-id="91b59-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="91b59-173">tooconnect Hola VM toohello área de trabajo especificado en el esquema de extensión de hello, establezca stopOnMultipleConnections toofalse en la configuración pública o quite esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="91b59-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="91b59-174">Esta máquina virtual se factura una vez por cada área de trabajo a la que se conecta.</span><span class="sxs-lookup"><span data-stu-id="91b59-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="91b59-175">11</span><span class="sxs-lookup"><span data-stu-id="91b59-175">11</span></span> | <span data-ttu-id="91b59-176">Extensión de configuración no válido proporcionado toohello</span><span class="sxs-lookup"><span data-stu-id="91b59-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="91b59-177">Siga Hola anteriores ejemplos tooset todos los valores de propiedad necesarios para la implementación.</span><span class="sxs-lookup"><span data-stu-id="91b59-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="91b59-178">12</span><span class="sxs-lookup"><span data-stu-id="91b59-178">12</span></span> | <span data-ttu-id="91b59-179">el Administrador de paquetes de saludo dpkg está bloqueado</span><span class="sxs-lookup"><span data-stu-id="91b59-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="91b59-180">Asegúrese de que todas las operaciones de actualización de dpkg en la máquina de hello termine e intente de nuevo.</span><span class="sxs-lookup"><span data-stu-id="91b59-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="91b59-181">20 |</span><span class="sxs-lookup"><span data-stu-id="91b59-181">20</span></span> | <span data-ttu-id="91b59-182">Habilitar llamado antes de tiempo</span><span class="sxs-lookup"><span data-stu-id="91b59-182">Enable called prematurely</span></span> | <span data-ttu-id="91b59-183">[Hola actualización agente Linux de Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello última versión disponible.</span><span class="sxs-lookup"><span data-stu-id="91b59-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="91b59-184">51</span><span class="sxs-lookup"><span data-stu-id="91b59-184">51</span></span> | <span data-ttu-id="91b59-185">Esta extensión no se admite en el sistema operativo de la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="91b59-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="91b59-186">55</span><span class="sxs-lookup"><span data-stu-id="91b59-186">55</span></span> | <span data-ttu-id="91b59-187">No se puede conectar el servicio de Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="91b59-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="91b59-188">Compruebe que Hola sistema disponga de acceso a Internet o que se ha proporcionado un proxy HTTP válido.</span><span class="sxs-lookup"><span data-stu-id="91b59-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="91b59-189">Además, compruebe validez de Hola de hello Id. de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="91b59-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="91b59-190">Información adicional de solución de problemas puede encontrarse en hello [Guía de solución de problemas del agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="91b59-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="91b59-191">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="91b59-191">Support</span></span>

<span data-ttu-id="91b59-192">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="91b59-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="91b59-193">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="91b59-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="91b59-194">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="91b59-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="91b59-195">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="91b59-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
