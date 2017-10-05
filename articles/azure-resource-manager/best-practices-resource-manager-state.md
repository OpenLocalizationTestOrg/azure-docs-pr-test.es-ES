---
title: Paso de valores complejos entre plantillas de Azure | Microsoft Docs
description: Muestra los enfoques recomendados para usar objetos complejos a fin de compartir datos de estado con plantillas vinculadas y plantillas de Azure Resource Manager.
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
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="0b317-103">Uso compartido del estado en y desde las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b317-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="0b317-104">En este tema se muestran los procedimientos recomendados para administrar y compartir el estado en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="0b317-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="0b317-105">Los parámetros y variables que se muestran en este tema son ejemplos del tipo de objetos que puede definir para organizar con facilidad sus requisitos de implementación.</span><span class="sxs-lookup"><span data-stu-id="0b317-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="0b317-106">Desde estos ejemplos, puede implementar sus propios objetos con valores de propiedad que tengan sentido para su entorno.</span><span class="sxs-lookup"><span data-stu-id="0b317-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="0b317-107">Este tema forma parte de un artículo más extenso.</span><span class="sxs-lookup"><span data-stu-id="0b317-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="0b317-108">Para leer el documento completo, descargue [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf) (Consideraciones sobre las plantillas de Resource Manager de talla mundial y prácticas comprobadas).</span><span class="sxs-lookup"><span data-stu-id="0b317-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="0b317-109">Proporcionar opciones de configuración estándar</span><span class="sxs-lookup"><span data-stu-id="0b317-109">Provide standard configuration settings</span></span>
<span data-ttu-id="0b317-110">En lugar de ofrecer una plantilla que proporciona total flexibilidad e infinidad de variaciones, un patrón común es proporcionar una selección de configuraciones conocidas.</span><span class="sxs-lookup"><span data-stu-id="0b317-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="0b317-111">De hecho, los usuarios pueden seleccionar tamaños estándar de camiseta como espacio aislado, pequeño, mediano y grande.</span><span class="sxs-lookup"><span data-stu-id="0b317-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="0b317-112">Otros ejemplos de tamaños de camiseta son ofertas de productos, como edición para la comunidad o edición para impresa.</span><span class="sxs-lookup"><span data-stu-id="0b317-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="0b317-113">En otros casos, pueden ser configuraciones de una tecnología específicas de la carga de trabajo, como MapReduce o NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0b317-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="0b317-114">Con objetos complejos, puede crear las variables que contengan colecciones de datos, a veces conocidas como "contenedores de propiedades" y usar esos datos para dirigir la declaración de recursos de tu plantilla.</span><span class="sxs-lookup"><span data-stu-id="0b317-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="0b317-115">Este enfoque proporciona configuraciones bien conocidas de tamaños variables que están preconfiguradas para los clientes.</span><span class="sxs-lookup"><span data-stu-id="0b317-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="0b317-116">Sin configuraciones conocidas, los usuarios de las plantillas deben determinar el tamaño del clúster por su cuenta, tener en cuenta las restricciones de recursos de plataforma y realizar cálculos matemáticos para identificar el particionamiento resultante de las cuentas de almacenamiento y otros recursos (debido a restricciones en el tamaño del clúster y los recursos).</span><span class="sxs-lookup"><span data-stu-id="0b317-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="0b317-117">Además de crear una experiencia mejor para el cliente, unas cuantas configuraciones conocidas son más fáciles de mantener y puede ayudarle a ofrecer un nivel mayor de densidad.</span><span class="sxs-lookup"><span data-stu-id="0b317-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="0b317-118">En el ejemplo siguiente se muestra cómo definir variables que contienen objetos complejos para representar colecciones de datos.</span><span class="sxs-lookup"><span data-stu-id="0b317-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="0b317-119">Las colecciones definen valores que se usan para el tamaño de la máquina virtual, la configuración de red, la configuración del sistema operativo y la configuración de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0b317-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="0b317-120">Tenga en cuenta que la variable **tshirtSize** concatena el tamaño de la camiseta que proporcionó mediante un parámetro (**Small**, **Medium**, **Large**) en el texto **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="0b317-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="0b317-121">Use esta variable para recuperar la variable asociada del objeto complejo para ese tamaño de camiseta.</span><span class="sxs-lookup"><span data-stu-id="0b317-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="0b317-122">Luego, puede hacer referencia a estas variables más adelante en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="0b317-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="0b317-123">La posibilidad de hacer referencia a variables con nombre y sus propiedades simplifica la sintaxis de la plantilla y facilita la comprensión del contexto.</span><span class="sxs-lookup"><span data-stu-id="0b317-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="0b317-124">En el ejemplo siguiente se define un recurso para implementar mediante los objetos mostrados anteriormente para definir los valores.</span><span class="sxs-lookup"><span data-stu-id="0b317-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="0b317-125">Por ejemplo, el tamaño de VM se establece al recuperar el valor de `variables('tshirtSize').vmSize` mientras que el valor del tamaño del disco se recupera de `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="0b317-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="0b317-126">Además, el URI de una plantilla vinculada se establece con el valor de `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="0b317-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-to-a-template"></a><span data-ttu-id="0b317-127">Pasar el estado a una plantilla</span><span class="sxs-lookup"><span data-stu-id="0b317-127">Pass state to a template</span></span>
<span data-ttu-id="0b317-128">Comparte el estado en una plantilla mediante parámetros que proporciona directamente durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="0b317-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="0b317-129">En la tabla siguiente se enumeran los parámetros usados normalmente en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="0b317-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="0b317-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="0b317-130">Name</span></span> | <span data-ttu-id="0b317-131">Valor</span><span class="sxs-lookup"><span data-stu-id="0b317-131">Value</span></span> | <span data-ttu-id="0b317-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b317-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b317-133">location</span><span class="sxs-lookup"><span data-stu-id="0b317-133">location</span></span> |<span data-ttu-id="0b317-134">Cadena de una lista restringida de regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="0b317-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="0b317-135">La ubicación donde se implementan los recursos.</span><span class="sxs-lookup"><span data-stu-id="0b317-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="0b317-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="0b317-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="0b317-137">Cadena</span><span class="sxs-lookup"><span data-stu-id="0b317-137">String</span></span> |<span data-ttu-id="0b317-138">Nombre DNS único de la cuenta de almacenamiento donde se colocarán los discos de la VM</span><span class="sxs-lookup"><span data-stu-id="0b317-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="0b317-139">domainName</span><span class="sxs-lookup"><span data-stu-id="0b317-139">domainName</span></span> |<span data-ttu-id="0b317-140">String</span><span class="sxs-lookup"><span data-stu-id="0b317-140">String</span></span> |<span data-ttu-id="0b317-141">Nombre de dominio de la VM de JumpBox accesible públicamente en el formato: **{nombreDominio}.{ubicación}.cloudapp.com** Por ejemplo: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="0b317-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="0b317-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="0b317-142">adminUsername</span></span> |<span data-ttu-id="0b317-143">String</span><span class="sxs-lookup"><span data-stu-id="0b317-143">String</span></span> |<span data-ttu-id="0b317-144">Nombre de usuario de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="0b317-144">Username for the VMs</span></span> |
| <span data-ttu-id="0b317-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="0b317-145">adminPassword</span></span> |<span data-ttu-id="0b317-146">String</span><span class="sxs-lookup"><span data-stu-id="0b317-146">String</span></span> |<span data-ttu-id="0b317-147">Contraseña de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="0b317-147">Password for the VMs</span></span> |
| <span data-ttu-id="0b317-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="0b317-148">tshirtSize</span></span> |<span data-ttu-id="0b317-149">Cadena de una lista restringida de tamaños de camiseta ofrecidos</span><span class="sxs-lookup"><span data-stu-id="0b317-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="0b317-150">El tamaño de la unidad de escalado con nombre para aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="0b317-150">The named scale unit size to provision.</span></span> <span data-ttu-id="0b317-151">Por ejemplo, "Pequeña", "Mediana", "Grande"</span><span class="sxs-lookup"><span data-stu-id="0b317-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="0b317-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="0b317-152">virtualNetworkName</span></span> |<span data-ttu-id="0b317-153">String</span><span class="sxs-lookup"><span data-stu-id="0b317-153">String</span></span> |<span data-ttu-id="0b317-154">Nombre de la red virtual que el consumidor desea usar.</span><span class="sxs-lookup"><span data-stu-id="0b317-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="0b317-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="0b317-155">enableJumpbox</span></span> |<span data-ttu-id="0b317-156">Cadena de una lista restringida (habilitada o deshabilitada)</span><span class="sxs-lookup"><span data-stu-id="0b317-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="0b317-157">Parámetro que identifica si se habilitará un JumpBox para el entorno.</span><span class="sxs-lookup"><span data-stu-id="0b317-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="0b317-158">Valores: "habilitado", "deshabilitado"</span><span class="sxs-lookup"><span data-stu-id="0b317-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="0b317-159">El parámetro **tshirtSize** usado en la sección anterior se define como:</span><span class="sxs-lookup"><span data-stu-id="0b317-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

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
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="0b317-160">Pasar el estado a las plantillas vinculadas</span><span class="sxs-lookup"><span data-stu-id="0b317-160">Pass state to linked templates</span></span>
<span data-ttu-id="0b317-161">Al conectarse a plantillas vinculadas, a menudo usa una combinación de variables estáticas y generadas.</span><span class="sxs-lookup"><span data-stu-id="0b317-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="0b317-162">Variables estáticas</span><span class="sxs-lookup"><span data-stu-id="0b317-162">Static variables</span></span>
<span data-ttu-id="0b317-163">Las variables estáticas se suelen usar para proporcionar valores base, como direcciones URL, que se usan en toda la plantilla.</span><span class="sxs-lookup"><span data-stu-id="0b317-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="0b317-164">En el siguiente fragmento de la plantilla, `templateBaseUrl` especifica la ubicación raíz de la plantilla en GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b317-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="0b317-165">La línea siguiente crea una nueva variable `sharedTemplateUrl` que concatena la dirección URL base con el nombre conocido de la plantilla de recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="0b317-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="0b317-166">Debajo de esa línea, una variable de objeto complejo se usa para almacenar un tamaño de camiseta, donde la dirección URL base se concatena a la ubicación de la plantilla de configuración conocida y almacenada en la propiedad `vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="0b317-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="0b317-167">La ventaja de este enfoque es que si cambia la ubicación de la plantilla, solo tendrá que cambiar la variable estática en un lugar, que la pase a todas las plantillas vinculadas.</span><span class="sxs-lookup"><span data-stu-id="0b317-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="0b317-168">Variables generadas</span><span class="sxs-lookup"><span data-stu-id="0b317-168">Generated variables</span></span>
<span data-ttu-id="0b317-169">Además de las variables estáticas, hay varias variables que se generan dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="0b317-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="0b317-170">En esta sección se identifican algunos de los tipos comunes de variables generadas.</span><span class="sxs-lookup"><span data-stu-id="0b317-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="0b317-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="0b317-171">tshirtSize</span></span>
<span data-ttu-id="0b317-172">Está familiarizado con esta variable generada de los ejemplos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0b317-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="0b317-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="0b317-173">networkSettings</span></span>
<span data-ttu-id="0b317-174">En una plantilla de solución de capacidad o con ámbito completo, las plantillas vinculadas suele crean recursos que existen en una red.</span><span class="sxs-lookup"><span data-stu-id="0b317-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="0b317-175">Un enfoque sencillo es usar un objeto complejo para almacenar la configuración de red y pasarla a las plantillas vinculadas.</span><span class="sxs-lookup"><span data-stu-id="0b317-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="0b317-176">A continuación puede verse un ejemplo de comunicación de la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="0b317-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="0b317-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="0b317-177">availabilitySettings</span></span>
<span data-ttu-id="0b317-178">Los recursos creados en las plantillas vinculadas a menudo se colocan en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0b317-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="0b317-179">En el ejemplo siguiente, se especifica el nombre del conjunto de disponibilidad y también el número de dominios de error y dominios de actualización que se van a usar.</span><span class="sxs-lookup"><span data-stu-id="0b317-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="0b317-180">Si necesita varios conjuntos de disponibilidad (por ejemplo, uno para los nodos principales y otro para los nodos de datos), puede usar un nombre como prefijo, especificar varios conjuntos de disponibilidad o seguir el modelo mostrado anteriormente para la creación de una variable para un tamaño de camiseta específico.</span><span class="sxs-lookup"><span data-stu-id="0b317-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="0b317-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="0b317-181">storageSettings</span></span>
<span data-ttu-id="0b317-182">Los detalles de almacenamiento a menudo se comparten con las plantillas vinculadas.</span><span class="sxs-lookup"><span data-stu-id="0b317-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="0b317-183">En el ejemplo siguiente, un objeto *storageSettings* proporciona detalles sobre los nombres del contenedor y la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0b317-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="0b317-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="0b317-184">osSettings</span></span>
<span data-ttu-id="0b317-185">Con las plantillas vinculadas, tendrá que pasar la configuración del sistema operativo a varios tipos de nodos a través de diferentes tipos de configuración conocidos.</span><span class="sxs-lookup"><span data-stu-id="0b317-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="0b317-186">Un objeto complejo es una forma sencilla de almacenar y compartir información del sistema operativo y también facilita la compatibilidad con varias opciones de sistema operativo en la implementación.</span><span class="sxs-lookup"><span data-stu-id="0b317-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="0b317-187">En el ejemplo siguiente se muestra un objeto de *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="0b317-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="0b317-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="0b317-188">machineSettings</span></span>
<span data-ttu-id="0b317-189">Una variable generada, *machineSettings* es un objeto complejo que contiene una combinación de variables principales para crear una VM.</span><span class="sxs-lookup"><span data-stu-id="0b317-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="0b317-190">Las variables incluyen el nombre de usuario y la contraseña de administrador, un prefijo para los nombres de VM y una referencia de imagen del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0b317-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="0b317-191">Tenga en cuenta que *osImageReference* recupera los valores de la variable *osSettings* definida en la plantilla principal.</span><span class="sxs-lookup"><span data-stu-id="0b317-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="0b317-192">Eso significa que puede cambiar fácilmente el sistema operativo de una máquina virtual, por completo, o en función de la preferencia de un consumidor de plantilla.</span><span class="sxs-lookup"><span data-stu-id="0b317-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="0b317-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="0b317-193">vmScripts</span></span>
<span data-ttu-id="0b317-194">El objeto *vmScripts* contiene detalles sobre los scripts que se descargarán y ejecutarán en una instancia de máquina virtual, incluidas las referencias externas e internas.</span><span class="sxs-lookup"><span data-stu-id="0b317-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="0b317-195">Las referencias externas incluyen la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="0b317-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="0b317-196">Las referencias internas incluyen el software instalado y la configuración.</span><span class="sxs-lookup"><span data-stu-id="0b317-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="0b317-197">La propiedad *scriptsToDownload* se usa para mostrar los scripts que se descargarán en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b317-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="0b317-198">Este objeto también contiene referencias a argumentos de línea de comandos para diferentes tipos de acciones.</span><span class="sxs-lookup"><span data-stu-id="0b317-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="0b317-199">Estas acciones incluyen la ejecución de la instalación predeterminada de cada nodo individual, una instalación que se ejecuta después de que se implementan todos los nodos y los scripts adicionales que pueden ser específicos de una plantilla determinada.</span><span class="sxs-lookup"><span data-stu-id="0b317-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="0b317-200">Este ejemplo es de una plantilla que se usa para implementar MongoDB, lo que requiere un árbitro para proporcionar alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0b317-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="0b317-201">*arbiterNodeInstallCommand* se ha agregado a *vmScripts* para instalar el árbitro.</span><span class="sxs-lookup"><span data-stu-id="0b317-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="0b317-202">En la sección de variables es donde encuentra las variables que definen el texto específico para ejecutar el script con los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="0b317-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="0b317-203">Devolver el estado de una plantilla</span><span class="sxs-lookup"><span data-stu-id="0b317-203">Return state from a template</span></span>
<span data-ttu-id="0b317-204">No solo puede pasar datos a una plantilla, también puede compartir datos de nuevo con la plantilla de llamada.</span><span class="sxs-lookup"><span data-stu-id="0b317-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="0b317-205">En la sección **Salidas** de una plantilla vinculada, puede proporcionar pares de clave/valor que pueden usarse en la plantilla de origen.</span><span class="sxs-lookup"><span data-stu-id="0b317-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="0b317-206">En el ejemplo siguiente se muestra cómo pasar la dirección IP privada generada en una plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="0b317-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="0b317-207">Dentro de la plantilla principal, puede usar esos datos con la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b317-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="0b317-208">Puede usar esta expresión en la sección de salidas o en la sección de recursos de la plantilla principal.</span><span class="sxs-lookup"><span data-stu-id="0b317-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="0b317-209">No puede usar la expresión en la sección de variables porque se basa en el estado de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0b317-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="0b317-210">Para devolver este valor desde la plantilla principal, use:</span><span class="sxs-lookup"><span data-stu-id="0b317-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="0b317-211">Para obtener un ejemplo de cómo usar la sección de salidas de una plantilla vinculada para devolver discos de datos para una máquina virtual, consulte [Crear varios discos de datos para una máquina virtual](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0b317-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="0b317-212">Definir la configuración de autenticación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0b317-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="0b317-213">Puede usar el mismo patrón que se mostró anteriormente para las opciones de configuración para especificar la configuración de autenticación de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b317-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="0b317-214">Cree un parámetro para pasarlo en el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0b317-214">You create a parameter for passing in the type of authentication.</span></span>

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

<span data-ttu-id="0b317-215">Agregue variables para los diferentes tipos de autenticación, y una variable para almacenar qué tipo se usa en esta implementación basándose en el valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="0b317-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

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

<span data-ttu-id="0b317-216">Al definir la máquina virtual, establece **osProfile** a la variable que creó.</span><span class="sxs-lookup"><span data-stu-id="0b317-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="0b317-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b317-217">Next steps</span></span>
* <span data-ttu-id="0b317-218">Para obtener información sobre las secciones de la plantilla, consulte [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="0b317-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="0b317-219">Para ver las funciones que están disponibles en una plantilla, consulte [Funciones de plantillas de Azure Resource Manager](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="0b317-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
