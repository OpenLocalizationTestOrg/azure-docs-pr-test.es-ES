---
title: "información general de proveedor de recursos aaaNetwork | Documentos de Microsoft"
description: "Obtenga información acerca de hello nuevo proveedor de recursos de red en el Administrador de recursos de Azure"
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
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="01ce2-103">Proveedor de recursos de red</span><span class="sxs-lookup"><span data-stu-id="01ce2-103">Network Resource Provider</span></span>
<span data-ttu-id="01ce2-104">Una necesidad de respaldo de éxito del negocio de hoy en día, es Hola toobuild de capacidad y administrar aplicaciones de red de gran escala de una manera ágil, flexible, segura y repetible.</span><span class="sxs-lookup"><span data-stu-id="01ce2-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="01ce2-105">Administrador de recursos de Azure permite toocreate aplicaciones, como una sola colección de recursos de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="01ce2-106">Estos recursos se administran a través de diversos proveedores de recursos en Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01ce2-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="01ce2-107">Administrador de recursos de Azure se basa en distintos proveedores tooprovide acceso tooyour de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="01ce2-108">Hay tres proveedores de recursos principales: redes, almacenamiento y proceso.</span><span class="sxs-lookup"><span data-stu-id="01ce2-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="01ce2-109">Este documento describen las características de Hola y las ventajas de hello proveedor de recursos de red, incluidos:</span><span class="sxs-lookup"><span data-stu-id="01ce2-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="01ce2-110">**Metadatos** : puede agregar tooresources información mediante etiquetas.</span><span class="sxs-lookup"><span data-stu-id="01ce2-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="01ce2-111">Estas etiquetas pueden tener usado tootrack utilización de recursos entre suscripciones y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="01ce2-112">**Mayor control de la red** : los recursos de red están acoplados holgadamente y los puede controlar de forma más detallada.</span><span class="sxs-lookup"><span data-stu-id="01ce2-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="01ce2-113">Esto significa que tiene más flexibilidad para administrar recursos de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="01ce2-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="01ce2-114">**Configuración más rápida** : dado que los recursos de red están acoplados holgadamente, puede crear y organizar los recursos de red en paralelo.</span><span class="sxs-lookup"><span data-stu-id="01ce2-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="01ce2-115">Esto ha reducido drásticamente el tiempo de configuración.</span><span class="sxs-lookup"><span data-stu-id="01ce2-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="01ce2-116">**Control de acceso basado en roles** -RBAC proporciona roles de forma predeterminada, con ámbito de seguridad específicos, en la creación de hello tooallowing de adición de roles personalizados para una administración segura.</span><span class="sxs-lookup"><span data-stu-id="01ce2-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="01ce2-117">**La implementación y administración más fácil** -es más fácil toodeploy y administrar las aplicaciones, ya que puede crear una pila de toda la aplicación como una sola colección de recursos en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="01ce2-118">Y toodeploy más rápido, ya que puede implementar simplemente proporcionando una carga JSON de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="01ce2-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="01ce2-119">**Personalización rápida** -puede usar plantillas de estilo declarativo tooenable repetible y rápida personalización de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="01ce2-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="01ce2-120">**Personalización repetible** -puede usar plantillas de estilo declarativo tooenable repetible y rápida personalización de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="01ce2-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="01ce2-121">**Interfaces de administración** -se pueden usar cualquiera de hello siguientes interfaces toomanage los recursos:</span><span class="sxs-lookup"><span data-stu-id="01ce2-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="01ce2-122">API basadas en REST</span><span class="sxs-lookup"><span data-stu-id="01ce2-122">REST based API</span></span>
  * <span data-ttu-id="01ce2-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01ce2-123">PowerShell</span></span>
  * <span data-ttu-id="01ce2-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="01ce2-124">.NET SDK</span></span>
  * <span data-ttu-id="01ce2-125">SDK de Node.JS</span><span class="sxs-lookup"><span data-stu-id="01ce2-125">Node.JS SDK</span></span>
  * <span data-ttu-id="01ce2-126">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="01ce2-126">Java SDK</span></span>
  * <span data-ttu-id="01ce2-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01ce2-127">Azure CLI</span></span>
  * <span data-ttu-id="01ce2-128">Portal de vista previa</span><span class="sxs-lookup"><span data-stu-id="01ce2-128">Preview Portal</span></span>
  * <span data-ttu-id="01ce2-129">Idioma de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01ce2-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="01ce2-130">Recursos de red</span><span class="sxs-lookup"><span data-stu-id="01ce2-130">Network resources</span></span>
<span data-ttu-id="01ce2-131">Ahora puede administrar los recursos de red de forma independiente, en lugar de tener hacerlo a través de un recurso de proceso único (una máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="01ce2-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="01ce2-132">Esto garantiza un mayor grado de flexibilidad y agilidad a la hora de componer una infraestructura compleja y de gran escala en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="01ce2-133">A continuación se presenta una vista conceptual de una implementación de ejemplo que implica una aplicación de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="01ce2-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="01ce2-134">Todos los recursos que vea, por ejemplo, las NIC, las direcciones IP públicas y las máquinas virtuales, pueden administrarse de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="01ce2-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modelo de recursos de red](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="01ce2-136">Cada recurso contiene un conjunto común de propiedades y un conjunto de propiedades individual.</span><span class="sxs-lookup"><span data-stu-id="01ce2-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="01ce2-137">Hola las propiedades comunes son:</span><span class="sxs-lookup"><span data-stu-id="01ce2-137">hello common properties are:</span></span>

| <span data-ttu-id="01ce2-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="01ce2-138">Property</span></span> | <span data-ttu-id="01ce2-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="01ce2-139">Description</span></span> | <span data-ttu-id="01ce2-140">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="01ce2-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01ce2-141">**name**</span><span class="sxs-lookup"><span data-stu-id="01ce2-141">**name**</span></span> |<span data-ttu-id="01ce2-142">Nombre de recurso único.</span><span class="sxs-lookup"><span data-stu-id="01ce2-142">Unique resource name.</span></span> <span data-ttu-id="01ce2-143">Cada tipo de recurso tiene sus propias restricciones de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="01ce2-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="01ce2-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="01ce2-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="01ce2-145">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="01ce2-145">**location**</span></span> |<span data-ttu-id="01ce2-146">Región de Azure en qué Hola reside el recurso</span><span class="sxs-lookup"><span data-stu-id="01ce2-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="01ce2-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="01ce2-147">westus, eastus</span></span> |
| <span data-ttu-id="01ce2-148">**id**</span><span class="sxs-lookup"><span data-stu-id="01ce2-148">**id**</span></span> |<span data-ttu-id="01ce2-149">URI único basado en la identificación</span><span class="sxs-lookup"><span data-stu-id="01ce2-149">Unique URI based identification</span></span> |<span data-ttu-id="01ce2-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="01ce2-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="01ce2-151">Puede comprobar las propiedades individuales de recursos de hello las siguientes secciones se Hola.</span><span class="sxs-lookup"><span data-stu-id="01ce2-151">You can check hello individual properties of resources in hello sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="01ce2-152">Interfaces de administración</span><span class="sxs-lookup"><span data-stu-id="01ce2-152">Management interfaces</span></span>
<span data-ttu-id="01ce2-153">Puede administrar los recursos de redes de Azure mediante distintas interfaces.</span><span class="sxs-lookup"><span data-stu-id="01ce2-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="01ce2-154">En este documento, nos centraremos en las interfaces API de REST y las plantillas.</span><span class="sxs-lookup"><span data-stu-id="01ce2-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="01ce2-155">API de REST</span><span class="sxs-lookup"><span data-stu-id="01ce2-155">REST API</span></span>
<span data-ttu-id="01ce2-156">Como se mencionó anteriormente, se pueden administrar los recursos de red a través de una variedad de interfaces, incluidas API de REST, .NET SDK, SDK de Node.JS, SDK de Java, PowerShell, CLI, Portal de Azure y plantillas.</span><span class="sxs-lookup"><span data-stu-id="01ce2-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="01ce2-157">Hola API de Rest se ajustan toohello especificación del protocolo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="01ce2-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="01ce2-158">estructura de Hello general URI de hello API se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="01ce2-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="01ce2-159">Y parámetros de hello entre llaves representan Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="01ce2-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="01ce2-160">**subscription-id** : identificador de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="01ce2-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="01ce2-161">**Resource-provider-namespace** -espacio de nombres de proveedor de Hola que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="01ce2-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="01ce2-162">valor de Hello para el proveedor de recursos de red de hello es *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="01ce2-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="01ce2-163">**nombre de la región** -nombre de la región de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="01ce2-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="01ce2-164">Hello métodos HTTP siguientes se admiten al realizar llamadas toohello API de REST:</span><span class="sxs-lookup"><span data-stu-id="01ce2-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="01ce2-165">**COLOCAR** : se usan toocreate un recurso de un tipo determinado, modificar una propiedad de recurso o cambiar una asociación entre los recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="01ce2-166">**OBTENER** -tooretrieve información que se utiliza para un recurso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="01ce2-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="01ce2-167">**ELIMINAR** -usa toodelete un recurso existente.</span><span class="sxs-lookup"><span data-stu-id="01ce2-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="01ce2-168">Hola solicitud y respuesta ajustan tooa formato de carga JSON.</span><span class="sxs-lookup"><span data-stu-id="01ce2-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="01ce2-169">Para obtener más información, consulte [API de administración de recursos de Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="01ce2-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="01ce2-170">Idioma de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01ce2-170">Resource Manager template language</span></span>
<span data-ttu-id="01ce2-171">En recursos de toomanaging adición imperativamente (a través de las API o SDK), también puede usar un toobuild de estilo de programación declarativa y administrar recursos de red mediante Hola idioma de plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="01ce2-172">A continuación se proporciona una representación de una plantilla de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="01ce2-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="01ce2-173">plantilla de Hello es principalmente una descripción de JSON de recursos de Hola y valores de la instancia de hello insertados a través de parámetros.</span><span class="sxs-lookup"><span data-stu-id="01ce2-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="01ce2-174">ejemplo de Hola siguiente puede ser toocreate usa una red virtual con 2 subredes.</span><span class="sxs-lookup"><span data-stu-id="01ce2-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="01ce2-175">Tiene la opción de Hola de proporcionar valores de parámetro hello manualmente cuando se utiliza una plantilla, o puede usar un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="01ce2-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="01ce2-176">ejemplo de Hola siguiente muestra un posible conjunto de toobe de valores de parámetro utilizado con plantilla Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="01ce2-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

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


<span data-ttu-id="01ce2-177">Hola ventajas principales del uso de plantillas son:</span><span class="sxs-lookup"><span data-stu-id="01ce2-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="01ce2-178">Puede crear una infraestructura compleja en un grupo de recursos de estilo declarativo.</span><span class="sxs-lookup"><span data-stu-id="01ce2-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="01ce2-179">Hola orquestación de creación de recursos de hello, incluida la administración de dependencia, se controla mediante el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="01ce2-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="01ce2-180">infraestructura de Hello puede crearse de forma repetible en diversas regiones y dentro de una región con solo cambiar parámetros.</span><span class="sxs-lookup"><span data-stu-id="01ce2-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="01ce2-181">estilo declarativo Hola conduce tooshorter plazo para generar plantillas de Hola y efectuando infraestructura Hola.</span><span class="sxs-lookup"><span data-stu-id="01ce2-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="01ce2-182">Para ver plantillas de ejemplo, consulte [Plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="01ce2-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="01ce2-183">Para obtener más información sobre Hola idioma de plantilla de administrador de recursos, consulte [idioma de plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01ce2-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="01ce2-184">plantilla de ejemplo de Hola anterior utiliza la red virtual de Hola y recursos de la subred.</span><span class="sxs-lookup"><span data-stu-id="01ce2-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="01ce2-185">Hay otros recursos de red que se pueden utilizar, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="01ce2-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="01ce2-186">Uso de una plantilla</span><span class="sxs-lookup"><span data-stu-id="01ce2-186">Using a template</span></span>
<span data-ttu-id="01ce2-187">Puede implementar servicios tooAzure desde una plantilla mediante el uso de PowerShell, AzureCLI, o bien al realizar una toodeploy haga clic en desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="01ce2-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="01ce2-188">Servicios de toodeploy de una plantilla en GitHub, ejecute Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="01ce2-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="01ce2-189">Abrir archivo de hello template3 desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="01ce2-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="01ce2-190">Como ejemplo, abra [Red virtual con dos subredes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="01ce2-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="01ce2-191">Haga clic en **implementar tooAzure**y, a continuación, inicie sesión en toohello portal de Azure con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="01ce2-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="01ce2-192">Comprobar la plantilla de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="01ce2-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="01ce2-193">Haga clic en **editar parámetros** y seleccione una ubicación, por ejemplo, *oeste de Estados Unidos*, para la red virtual de Hola y subredes.</span><span class="sxs-lookup"><span data-stu-id="01ce2-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="01ce2-194">Si es necesario, cambie hello **ADDRESSPREFIX** y **SUBNETPREFIX** parámetros y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="01ce2-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="01ce2-195">Haga clic en **seleccionar un grupo de recursos** y, a continuación, haga clic en el grupo de recursos de hello desea tooadd Hola virtuales y las subredes a.</span><span class="sxs-lookup"><span data-stu-id="01ce2-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="01ce2-196">Como alternativa, puede crear un nuevo grupo de recursos haciendo clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="01ce2-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="01ce2-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="01ce2-197">Click **Create**.</span></span> <span data-ttu-id="01ce2-198">Tenga en cuenta Hola icono mostrar **implementación de plantilla de aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="01ce2-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="01ce2-199">Una vez que se realice la implementación de hello, verá un tooone similar de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="01ce2-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Implementación de plantilla de ejemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="01ce2-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01ce2-201">Next steps</span></span>
[<span data-ttu-id="01ce2-202">Idioma de la plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="01ce2-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="01ce2-203">Redes de Azure: plantillas utilizadas habitualmente</span><span class="sxs-lookup"><span data-stu-id="01ce2-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="01ce2-204">Implementación de Azure Resource Manager frente a la implementación clásica</span><span class="sxs-lookup"><span data-stu-id="01ce2-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="01ce2-205">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01ce2-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

