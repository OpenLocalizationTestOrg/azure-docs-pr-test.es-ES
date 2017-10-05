---
title: "Información general del Proveedor de recursos de red | Microsoft Docs"
description: "Más información sobre el nuevo Proveedor de recursos de red del Administrador de recursos de Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="0b9d6-103">Proveedor de recursos de red</span><span class="sxs-lookup"><span data-stu-id="0b9d6-103">Network Resource Provider</span></span>
<span data-ttu-id="0b9d6-104">Una necesidad que sustenta el éxito de un negocio hoy en día es la capacidad de crear y administrar aplicaciones compatibles con redes de gran escala de una forma ágil, flexible, segura y repetible.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="0b9d6-105">Azure Resource Manager permite crear tales aplicaciones, como una única colección de recursos en grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="0b9d6-106">Estos recursos se administran a través de diversos proveedores de recursos en Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="0b9d6-107">El Administrador de recursos de Azure utiliza distintos proveedores de recursos para proporcionar acceso a los recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="0b9d6-108">Hay tres proveedores de recursos principales: redes, almacenamiento y proceso.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="0b9d6-109">En este documento, se describen las características y ventajas del proveedor de recursos de red, entre otros:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="0b9d6-110">**Metadatos** : puede agregar información a los recursos mediante etiquetas.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="0b9d6-111">Estas etiquetas pueden utilizarse para realizar el seguimiento de la utilización de recursos en todas las suscripciones y los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="0b9d6-112">**Mayor control de la red** : los recursos de red están acoplados holgadamente y los puede controlar de forma más detallada.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="0b9d6-113">Esto significa que tendrá una mayor flexibilidad en la administración de los recursos de red.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="0b9d6-114">**Configuración más rápida** : dado que los recursos de red están acoplados holgadamente, puede crear y organizar los recursos de red en paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="0b9d6-115">Esto ha reducido drásticamente el tiempo de configuración.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="0b9d6-116">**Control de acceso basado en rol (RBAC)** : RBAC proporciona roles predeterminados, con un  ámbito de seguridad específico, además de permitir la creación de roles personalizados para una administración segura.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="0b9d6-117">**Administración e implementación más sencillas** : resulta más fácil implementar y administrar aplicaciones, ya que puede crear una pila de toda la aplicación como una única colección de recursos en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="0b9d6-118">Y más rápido de implementar, ya que es posible hacerlo con solo proporcionar una carga JSON de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="0b9d6-119">**Personalización rápida** : puede utilizar las plantillas de estilo declarativo para habilitar la personalización repetible y rápida de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="0b9d6-120">**Personalización repetible** : puede utilizar las plantillas de estilo declarativo para habilitar la personalización repetible y rápida de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="0b9d6-121">**Interfaces de administración** : puede utilizar cualquiera de las siguientes interfaces para administrar los recursos:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="0b9d6-122">API basadas en REST</span><span class="sxs-lookup"><span data-stu-id="0b9d6-122">REST based API</span></span>
  * <span data-ttu-id="0b9d6-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b9d6-123">PowerShell</span></span>
  * <span data-ttu-id="0b9d6-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="0b9d6-124">.NET SDK</span></span>
  * <span data-ttu-id="0b9d6-125">SDK de Node.JS</span><span class="sxs-lookup"><span data-stu-id="0b9d6-125">Node.JS SDK</span></span>
  * <span data-ttu-id="0b9d6-126">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="0b9d6-126">Java SDK</span></span>
  * <span data-ttu-id="0b9d6-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b9d6-127">Azure CLI</span></span>
  * <span data-ttu-id="0b9d6-128">Portal de vista previa</span><span class="sxs-lookup"><span data-stu-id="0b9d6-128">Preview Portal</span></span>
  * <span data-ttu-id="0b9d6-129">Idioma de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b9d6-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="0b9d6-130">Recursos de red</span><span class="sxs-lookup"><span data-stu-id="0b9d6-130">Network resources</span></span>
<span data-ttu-id="0b9d6-131">Ahora puede administrar los recursos de red de forma independiente, en lugar de tener hacerlo a través de un recurso de proceso único (una máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="0b9d6-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="0b9d6-132">Esto garantiza un mayor grado de flexibilidad y agilidad a la hora de componer una infraestructura compleja y de gran escala en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="0b9d6-133">A continuación se presenta una vista conceptual de una implementación de ejemplo que implica una aplicación de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="0b9d6-134">Todos los recursos que vea, por ejemplo, las NIC, las direcciones IP públicas y las máquinas virtuales, pueden administrarse de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modelo de recursos de red](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="0b9d6-136">Cada recurso contiene un conjunto común de propiedades y un conjunto de propiedades individual.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="0b9d6-137">Las propiedades comunes son:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-137">The common properties are:</span></span>

| <span data-ttu-id="0b9d6-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0b9d6-138">Property</span></span> | <span data-ttu-id="0b9d6-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b9d6-139">Description</span></span> | <span data-ttu-id="0b9d6-140">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0b9d6-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b9d6-141">**name**</span><span class="sxs-lookup"><span data-stu-id="0b9d6-141">**name**</span></span> |<span data-ttu-id="0b9d6-142">Nombre de recurso único.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-142">Unique resource name.</span></span> <span data-ttu-id="0b9d6-143">Cada tipo de recurso tiene sus propias restricciones de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="0b9d6-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="0b9d6-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="0b9d6-145">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="0b9d6-145">**location**</span></span> |<span data-ttu-id="0b9d6-146">Región de Azure en la que reside el recurso.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="0b9d6-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="0b9d6-147">westus, eastus</span></span> |
| <span data-ttu-id="0b9d6-148">**id**</span><span class="sxs-lookup"><span data-stu-id="0b9d6-148">**id**</span></span> |<span data-ttu-id="0b9d6-149">URI único basado en la identificación</span><span class="sxs-lookup"><span data-stu-id="0b9d6-149">Unique URI based identification</span></span> |<span data-ttu-id="0b9d6-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="0b9d6-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="0b9d6-151">Puede comprobar las propiedades individuales de los recursos en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-151">You can check the individual properties of resources in the sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="0b9d6-152">Interfaces de administración</span><span class="sxs-lookup"><span data-stu-id="0b9d6-152">Management interfaces</span></span>
<span data-ttu-id="0b9d6-153">Puede administrar los recursos de redes de Azure mediante distintas interfaces.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="0b9d6-154">En este documento, nos centraremos en las interfaces API de REST y las plantillas.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="0b9d6-155">API de REST</span><span class="sxs-lookup"><span data-stu-id="0b9d6-155">REST API</span></span>
<span data-ttu-id="0b9d6-156">Como se mencionó anteriormente, se pueden administrar los recursos de red a través de una variedad de interfaces, incluidas API de REST, .NET SDK, SDK de Node.JS, SDK de Java, PowerShell, CLI, Portal de Azure y plantillas.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="0b9d6-157">Las API de REST se ajustan a la especificación del protocolo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="0b9d6-158">A continuación se presenta la estructura general de URI de la API:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="0b9d6-159">Y los parámetros entre llaves representan los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="0b9d6-160">**subscription-id** : identificador de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="0b9d6-161">**resource-provider-namespace** : espacio de nombres para el proveedor que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="0b9d6-162">El valor para el proveedor de recursos de red es *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="0b9d6-163">**region-name** : el nombre de la región de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="0b9d6-164">Se admiten los siguientes métodos HTTP cuando se realizan llamadas a la API de REST:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="0b9d6-165">**PUT** : se utiliza para crear un recurso de un tipo determinado, modificar una propiedad de recurso o cambiar una asociación entre recursos.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="0b9d6-166">**GET** : se utiliza para recuperar información para un recurso aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="0b9d6-167">**DELETE** : se utiliza para eliminar un recurso existente.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="0b9d6-168">La solicitud y la respuesta se ajustan a un formato de carga JSON.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="0b9d6-169">Para obtener más información, consulte [API de administración de recursos de Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b9d6-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="0b9d6-170">Idioma de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b9d6-170">Resource Manager template language</span></span>
<span data-ttu-id="0b9d6-171">Además de administrar recursos de forma imperativa (a través de API o SDK), también puede utilizar un estilo de programación declarativo para crear y administrar recursos de red mediante el lenguaje de la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="0b9d6-172">A continuación se proporciona una representación de una plantilla de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="0b9d6-173">La plantilla es principalmente una descripción de JSON de los recursos y los valores de instancia insertados a través de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="0b9d6-174">El ejemplo siguiente puede utilizarse para crear una red virtual con dos subredes.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="0b9d6-175">Tiene la opción de proporcionar los valores de los parámetros manualmente cuando se utiliza una plantilla, o bien puede usar un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="0b9d6-176">El ejemplo siguiente muestra un posible conjunto de valores de parámetros para usar con la plantilla anterior:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="0b9d6-177">Las principales ventajas derivadas del uso de plantillas son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="0b9d6-178">Puede crear una infraestructura compleja en un grupo de recursos de estilo declarativo.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="0b9d6-179">La coordinación de la creación de recursos, incluida la administración de dependencias, se controla mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="0b9d6-180">La infraestructura se puede crear de una manera repetible en diferentes regiones y dentro de una misma región cambiando simplemente parámetros.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="0b9d6-181">El estilo declarativo permite reducir el tiempo necesario para generar las plantillas y distribuir la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="0b9d6-182">Para ver plantillas de ejemplo, consulte [Plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="0b9d6-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="0b9d6-183">Para obtener más información sobre el lenguaje de la plantilla de Resource Manager, vea [Idioma de la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0b9d6-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0b9d6-184">La plantilla del ejemplo anterior utiliza la red virtual y los recursos de la subred.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="0b9d6-185">Hay otros recursos de red que se pueden utilizar, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="0b9d6-186">Uso de una plantilla</span><span class="sxs-lookup"><span data-stu-id="0b9d6-186">Using a template</span></span>
<span data-ttu-id="0b9d6-187">Puede implementar servicios en Azure desde una plantilla mediante PowerShell, CLI de Azure o mediante un clic para implementar desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="0b9d6-188">Para implementar servicios de una plantilla en GitHub, ejecute los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0b9d6-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="0b9d6-189">Abra el archivo de plantilla 3 desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="0b9d6-190">Como ejemplo, abra [Red virtual con dos subredes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="0b9d6-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="0b9d6-191">Haga clic en **Implementación en Azure**, y, a continuación, inicie sesión en el Portal de Azure con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="0b9d6-192">Compruebe la plantilla y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="0b9d6-193">Haga clic en **Editar parámetros** y seleccione una ubicación, como *West US*, para la red virtual y las subredes.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="0b9d6-194">Si es necesario, cambie los parámetros **ADDRESSPREFIX** y **SUBNETPREFIX** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="0b9d6-195">Haga clic en **Seleccionar un grupo de recursos** y, a continuación, haga clic en el grupo de recursos al que desea agregar la red virtual y las subredes.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="0b9d6-196">Como alternativa, puede crear un nuevo grupo de recursos haciendo clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="0b9d6-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-197">Click **Create**.</span></span> <span data-ttu-id="0b9d6-198">Observe el icono que muestra **Implementación de plantillas de aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="0b9d6-199">Una vez que se realiza la implementación, verá una pantalla similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="0b9d6-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![Implementación de plantilla de ejemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="0b9d6-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b9d6-201">Next steps</span></span>
[<span data-ttu-id="0b9d6-202">Idioma de la plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="0b9d6-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="0b9d6-203">Redes de Azure: plantillas utilizadas habitualmente</span><span class="sxs-lookup"><span data-stu-id="0b9d6-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="0b9d6-204">Implementación de Azure Resource Manager frente a la implementación clásica</span><span class="sxs-lookup"><span data-stu-id="0b9d6-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="0b9d6-205">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b9d6-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

