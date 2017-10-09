---
title: aaaPass valores complejos entre plantillas de Azure | Documentos de Microsoft
description: Muestra recomienda enfoques para utilizar datos de estado de objetos complejos tooshare con plantillas del Administrador de recursos de Azure y plantillas vinculadas.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="18acd-103">Tooand de estado de recurso compartido de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="18acd-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="18acd-104">En este tema se muestran los procedimientos recomendados para administrar y compartir el estado en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="18acd-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="18acd-105">Hello parámetros y variables que se muestran en este tema son ejemplos de tipo hello de objetos se pueden definir tooconveniently organizar los requisitos de implementación.</span><span class="sxs-lookup"><span data-stu-id="18acd-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="18acd-106">Desde estos ejemplos, puede implementar sus propios objetos con valores de propiedad que tengan sentido para su entorno.</span><span class="sxs-lookup"><span data-stu-id="18acd-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="18acd-107">Este tema forma parte de un artículo más extenso.</span><span class="sxs-lookup"><span data-stu-id="18acd-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="18acd-108">Hola tooread completa papel, descargue [clase recursos el Administrador de plantillas de consideraciones y prácticas comprobadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="18acd-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="18acd-109">Proporcionar opciones de configuración estándar</span><span class="sxs-lookup"><span data-stu-id="18acd-109">Provide standard configuration settings</span></span>
<span data-ttu-id="18acd-110">En lugar de ofrecer una plantilla que proporciona total flexibilidad y muchas variaciones, un patrón común es tooprovide una selección de configuraciones conocidas.</span><span class="sxs-lookup"><span data-stu-id="18acd-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="18acd-111">De hecho, los usuarios pueden seleccionar tamaños estándar de camiseta como espacio aislado, pequeño, mediano y grande.</span><span class="sxs-lookup"><span data-stu-id="18acd-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="18acd-112">Otros ejemplos de tamaños de camiseta son ofertas de productos, como edición para la comunidad o edición para impresa.</span><span class="sxs-lookup"><span data-stu-id="18acd-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="18acd-113">En otros casos, pueden ser configuraciones de una tecnología específicas de la carga de trabajo, como MapReduce o NoSQL.</span><span class="sxs-lookup"><span data-stu-id="18acd-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="18acd-114">Con objetos complejos, puede crear variables que contienen colecciones de datos, a veces conocidos como "los contenedores de propiedades" y usar esa declaración de recurso de datos toodrive hello en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="18acd-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="18acd-115">Este enfoque proporciona configuraciones bien conocidas de tamaños variables que están preconfiguradas para los clientes.</span><span class="sxs-lookup"><span data-stu-id="18acd-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="18acd-116">Sin configuraciones conocidas, los usuarios de la plantilla de hello deben determinar el tamaño de clúster en función de su propios, factor en las restricciones de recursos de plataforma y hacer matemáticas tooidentify Hola resultante particiones de las cuentas de almacenamiento y otros recursos (debido a tamaño toocluster y restricciones de recursos).</span><span class="sxs-lookup"><span data-stu-id="18acd-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="18acd-117">Además toomaking una mejor experiencia de cliente hello, algunas configuraciones conocidas son toosupport más fácil y pueden ayudarle a ofrecer un mayor nivel de densidad.</span><span class="sxs-lookup"><span data-stu-id="18acd-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="18acd-118">Hola siguiente ejemplo se muestra cómo las variables de toodefine que contienen objetos complejos para representar las colecciones de datos.</span><span class="sxs-lookup"><span data-stu-id="18acd-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="18acd-119">colecciones de Hello definen los valores que se usan para el tamaño de la máquina virtual, configuración de red, configuración del sistema operativo y configuración de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="18acd-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="18acd-120">Tenga en cuenta que hello **tshirtSize** variable concatena el tamaño de la camiseta de hello proporcionan a través de un parámetro (**pequeño**, **medio**, **grande**) texto toohello **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="18acd-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="18acd-121">Utilice esta variable de objeto complejo asociado tooretrieve variable Hola para ese tamaño camiseta.</span><span class="sxs-lookup"><span data-stu-id="18acd-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="18acd-122">A continuación, puede hacer referencia a estas variables más adelante en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="18acd-123">capacidad de Hello tooreference denominado-variables y sus propiedades simplifica la sintaxis de la plantilla de Hola y resulta fácil toounderstand contexto.</span><span class="sxs-lookup"><span data-stu-id="18acd-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="18acd-124">Hola siguiente ejemplo define un recurso toodeploy mediante objetos de Hola se ha mostrado anteriormente tooset valores.</span><span class="sxs-lookup"><span data-stu-id="18acd-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="18acd-125">Por ejemplo, hello tamaño de máquina virtual se establece mediante la recuperación de valor de hello para `variables('tshirtSize').vmSize` mientras el valor de hello para el tamaño del disco de Hola se recupera de `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="18acd-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="18acd-126">Además, Hola URI para una plantilla vinculada se establece con el valor de Hola para `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="18acd-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a><span data-ttu-id="18acd-127">Pase la plantilla de tooa de estado</span><span class="sxs-lookup"><span data-stu-id="18acd-127">Pass state tooa template</span></span>
<span data-ttu-id="18acd-128">Comparte el estado en una plantilla mediante parámetros que proporciona directamente durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="18acd-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="18acd-129">Hola tabla listas usadas parámetros en las plantillas siguientes.</span><span class="sxs-lookup"><span data-stu-id="18acd-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="18acd-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="18acd-130">Name</span></span> | <span data-ttu-id="18acd-131">Valor</span><span class="sxs-lookup"><span data-stu-id="18acd-131">Value</span></span> | <span data-ttu-id="18acd-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="18acd-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18acd-133">location</span><span class="sxs-lookup"><span data-stu-id="18acd-133">location</span></span> |<span data-ttu-id="18acd-134">Cadena de una lista restringida de regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="18acd-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="18acd-135">ubicación de Hola donde se implementan los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="18acd-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="18acd-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="18acd-137">String</span><span class="sxs-lookup"><span data-stu-id="18acd-137">String</span></span> |<span data-ttu-id="18acd-138">Nombre DNS único para la cuenta de almacenamiento donde se colocan los discos de la máquina virtual de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="18acd-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="18acd-139">domainName</span><span class="sxs-lookup"><span data-stu-id="18acd-139">domainName</span></span> |<span data-ttu-id="18acd-140">String</span><span class="sxs-lookup"><span data-stu-id="18acd-140">String</span></span> |<span data-ttu-id="18acd-141">Nombre de dominio de hello accesible públicamente jumpbox VM en formato de hello: **{domainName}. {} ubicación}.cloudapp.com** por ejemplo: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="18acd-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="18acd-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="18acd-142">adminUsername</span></span> |<span data-ttu-id="18acd-143">String</span><span class="sxs-lookup"><span data-stu-id="18acd-143">String</span></span> |<span data-ttu-id="18acd-144">Nombre de usuario para hello las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="18acd-144">Username for hello VMs</span></span> |
| <span data-ttu-id="18acd-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="18acd-145">adminPassword</span></span> |<span data-ttu-id="18acd-146">String</span><span class="sxs-lookup"><span data-stu-id="18acd-146">String</span></span> |<span data-ttu-id="18acd-147">Contraseña de hello las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="18acd-147">Password for hello VMs</span></span> |
| <span data-ttu-id="18acd-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="18acd-148">tshirtSize</span></span> |<span data-ttu-id="18acd-149">Cadena de una lista restringida de tamaños de camiseta ofrecidos</span><span class="sxs-lookup"><span data-stu-id="18acd-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="18acd-150">Hola denominado tooprovision de tamaño de unidad de escala.</span><span class="sxs-lookup"><span data-stu-id="18acd-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="18acd-151">Por ejemplo, "Pequeña", "Mediana", "Grande"</span><span class="sxs-lookup"><span data-stu-id="18acd-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="18acd-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="18acd-152">virtualNetworkName</span></span> |<span data-ttu-id="18acd-153">String</span><span class="sxs-lookup"><span data-stu-id="18acd-153">String</span></span> |<span data-ttu-id="18acd-154">Nombre de red virtual de Hola que Hola consumidor desea toouse.</span><span class="sxs-lookup"><span data-stu-id="18acd-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="18acd-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="18acd-155">enableJumpbox</span></span> |<span data-ttu-id="18acd-156">Cadena de una lista restringida (habilitada o deshabilitada)</span><span class="sxs-lookup"><span data-stu-id="18acd-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="18acd-157">Parámetro que identifica si tooenable un jumpbox para entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="18acd-158">Valores: "habilitado", "deshabilitado"</span><span class="sxs-lookup"><span data-stu-id="18acd-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="18acd-159">Hola **tshirtSize** parámetro usado en la sección anterior de Hola se define como:</span><span class="sxs-lookup"><span data-stu-id="18acd-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="18acd-160">Pasar plantillas toolinked de estado</span><span class="sxs-lookup"><span data-stu-id="18acd-160">Pass state toolinked templates</span></span>
<span data-ttu-id="18acd-161">Cuando se conecte toolinked plantillas, a menudo utilizar una combinación de estático y genera las variables.</span><span class="sxs-lookup"><span data-stu-id="18acd-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="18acd-162">Variables estáticas</span><span class="sxs-lookup"><span data-stu-id="18acd-162">Static variables</span></span>
<span data-ttu-id="18acd-163">Variables estáticas a menudo son los valores de base de tooprovide usado, como las direcciones URL, que se utilizan a lo largo de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="18acd-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="18acd-164">Hola siguiente extracto de plantilla, `templateBaseUrl` especifica la ubicación de raíz de hello para la plantilla de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="18acd-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="18acd-165">línea siguiente de Hello crea una nueva variable `sharedTemplateUrl` que concatena Hola dirección URL base con el nombre conocido de Hola de plantilla de recursos compartidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="18acd-166">Por debajo de esa línea, una variable de objeto complejo es toostore usa un tamaño de la camiseta, donde URL base hello es toohello concatenado conoce la ubicación de la plantilla de configuración y se almacenan en hello `vmTemplate` propiedad.</span><span class="sxs-lookup"><span data-stu-id="18acd-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="18acd-167">ventaja de Hola de este enfoque es que si cambia la ubicación de la plantilla de hello, solo necesita la variable estática de hello toochange en un solo lugar, que pasa a lo largo de plantillas de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="18acd-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="18acd-168">Variables generadas</span><span class="sxs-lookup"><span data-stu-id="18acd-168">Generated variables</span></span>
<span data-ttu-id="18acd-169">En variables de toostatic de adición, varias variables se generan dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="18acd-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="18acd-170">En esta sección se identifica algunos de los tipos comunes de Hola de variables generados.</span><span class="sxs-lookup"><span data-stu-id="18acd-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="18acd-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="18acd-171">tshirtSize</span></span>
<span data-ttu-id="18acd-172">Está familiarizado con esta variable generada de ejemplos de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="18acd-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="18acd-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="18acd-173">networkSettings</span></span>
<span data-ttu-id="18acd-174">En un Hola de capacidad, funcionalidad o plantilla de solución de ámbito de extremo a extremo, plantillas vinculadas normalmente crean recursos que existen en una red.</span><span class="sxs-lookup"><span data-stu-id="18acd-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="18acd-175">Un enfoque sencillo es toouse una configuración de red de toostore de objeto complejo y pasarlas toolinked plantillas.</span><span class="sxs-lookup"><span data-stu-id="18acd-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="18acd-176">A continuación puede verse un ejemplo de comunicación de la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="18acd-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="18acd-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="18acd-177">availabilitySettings</span></span>
<span data-ttu-id="18acd-178">Los recursos creados en las plantillas vinculadas a menudo se colocan en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="18acd-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="18acd-179">En el siguiente ejemplo de Hola, nombre del conjunto de disponibilidad de Hola se especifica también Hola dominio de error y actualice toouse de recuento de dominio.</span><span class="sxs-lookup"><span data-stu-id="18acd-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="18acd-180">Si tiene varios conjuntos de disponibilidad (por ejemplo, uno para los nodos principales) y otro para los nodos de datos, puede utilizar un nombre como prefijo, especifique varios conjuntos de disponibilidad o seguir modelo Hola mostrado anteriormente para crear una variable para un tamaño específico de la camiseta.</span><span class="sxs-lookup"><span data-stu-id="18acd-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="18acd-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="18acd-181">storageSettings</span></span>
<span data-ttu-id="18acd-182">Los detalles de almacenamiento a menudo se comparten con las plantillas vinculadas.</span><span class="sxs-lookup"><span data-stu-id="18acd-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="18acd-183">En el ejemplo de Hola siguiente, un *storageSettings* objeto proporciona detalles acerca de hello nombres de cuenta y el contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18acd-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="18acd-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="18acd-184">osSettings</span></span>
<span data-ttu-id="18acd-185">Con las plantillas vinculadas, puede que tenga tipos de nodos de toovarious de configuración de sistema operativo de toopass entre los tipos de configuración conocido diferente.</span><span class="sxs-lookup"><span data-stu-id="18acd-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="18acd-186">Un objeto complejo es una información del sistema operativo toostore y compartir fácilmente y también resulta más fácil toosupport múltiples opciones de sistema operativo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="18acd-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="18acd-187">Hello en el ejemplo siguiente se muestra un objeto para *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="18acd-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="18acd-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="18acd-188">machineSettings</span></span>
<span data-ttu-id="18acd-189">Una variable generada, *machineSettings* es un objeto complejo que contiene una combinación de variables principales para crear una VM.</span><span class="sxs-lookup"><span data-stu-id="18acd-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="18acd-190">variables de Hello incluyen el nombre de usuario de administrador y contraseña, un prefijo para los nombres de máquina virtual de Hola y referencia de una imagen de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="18acd-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="18acd-191">Tenga en cuenta que *osImageReference* recupera Hola valores de hello *osSettings* variable definida en la plantilla principal Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="18acd-192">Esto significa que puede cambiar fácilmente el sistema operativo de Hola para una máquina virtual: completamente o basado en la preferencia de Hola de un consumidor de plantilla.</span><span class="sxs-lookup"><span data-stu-id="18acd-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="18acd-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="18acd-193">vmScripts</span></span>
<span data-ttu-id="18acd-194">Hola *vmScripts* objeto contiene los detalles sobre toodownload de secuencias de comandos de Hola y ejecutar en una instancia de máquina virtual, incluidas las referencias exterior e interior.</span><span class="sxs-lookup"><span data-stu-id="18acd-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="18acd-195">Fuera de las referencias incluyen infraestructura Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="18acd-196">Las referencias de interior incluyen configuración y software de hello instalado instalado.</span><span class="sxs-lookup"><span data-stu-id="18acd-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="18acd-197">Usar hello *scriptsToDownload* Hola de propiedad toolist scripts toodownload toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18acd-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="18acd-198">Este objeto también contiene los argumentos de línea de toocommand de referencias para diferentes tipos de acciones.</span><span class="sxs-lookup"><span data-stu-id="18acd-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="18acd-199">Estas acciones incluyen la ejecución de la instalación predeterminada de Hola para cada nodo individual, una instalación que se ejecuta después de que se implementan todos los nodos y scripts adicionales que pueden ser tooa específico que proporciona la plantilla.</span><span class="sxs-lookup"><span data-stu-id="18acd-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="18acd-200">Este ejemplo es de un toodeploy de plantilla que se usa MongoDB, que requiere un árbitro toodeliver alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="18acd-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="18acd-201">Hola *arbiterNodeInstallCommand* se ha agregado demasiado*vmScripts* tooinstall árbitro de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="18acd-202">sección de variables de Hello es dónde encontrar las variables de Hola que definen la secuencia de comandos de hello texto específico tooexecute Hola con los valores adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="18acd-203">Devolver el estado de una plantilla</span><span class="sxs-lookup"><span data-stu-id="18acd-203">Return state from a template</span></span>
<span data-ttu-id="18acd-204">No solo puede pasar datos en una plantilla, también puede plantilla que realiza la llamada de recurso compartido de datos back-toohello.</span><span class="sxs-lookup"><span data-stu-id="18acd-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="18acd-205">Hola **genera** sección de una plantilla vinculada, puede proporcionar los pares clave/valor que se pueden usar en la plantilla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="18acd-206">Hello en el ejemplo siguiente se muestra cómo toopass Hola dirección IP privada generada en una plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="18acd-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="18acd-207">Dentro de la plantilla principal de hello, puede usar esos datos con la sintaxis de hello:</span><span class="sxs-lookup"><span data-stu-id="18acd-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="18acd-208">Puede utilizar esta expresión en la sección de salidas de Hola o sección de recursos de hello de la plantilla principal Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="18acd-209">No puede usar expresión de hello en la sección de variables de hello porque se basa en el estado de tiempo de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="18acd-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="18acd-210">tooreturn este valor de la plantilla principal de hello, utilice:</span><span class="sxs-lookup"><span data-stu-id="18acd-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="18acd-211">Para un ejemplo del uso de hello genera sección una plantilla vinculada tooreturn de discos de datos para una máquina virtual, consulte [crear varios discos de datos para una máquina Virtual](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="18acd-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="18acd-212">Definir la configuración de autenticación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="18acd-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="18acd-213">Puede usar hello mismo patrón que se ha mostrado anteriormente para la configuración de autenticación de configuración configuración toospecify Hola para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18acd-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="18acd-214">Cree un parámetro para pasarlo en tipo hello de autenticación.</span><span class="sxs-lookup"><span data-stu-id="18acd-214">You create a parameter for passing in hello type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="18acd-215">Agregue las variables para hello diferentes tipos de autenticación y una variable toostore qué tipo se usa para esta implementación en función del valor Hola de parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="18acd-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="18acd-216">Al definir la máquina virtual de hello, establecer hello **osProfile** variable toohello que creó.</span><span class="sxs-lookup"><span data-stu-id="18acd-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="18acd-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18acd-217">Next steps</span></span>
* <span data-ttu-id="18acd-218">toolearn acerca de las secciones de Hola de plantilla de hello, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="18acd-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="18acd-219">toosee Hola funciones que están disponibles en una plantilla, vea [funciones de plantilla de administrador de recursos de Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="18acd-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
