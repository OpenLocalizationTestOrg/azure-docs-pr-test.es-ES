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
# <a name="network-resource-provider"></a>Proveedor de recursos de red
Una necesidad de respaldo de éxito del negocio de hoy en día, es Hola toobuild de capacidad y administrar aplicaciones de red de gran escala de una manera ágil, flexible, segura y repetible. Administrador de recursos de Azure permite toocreate aplicaciones, como una sola colección de recursos de grupos de recursos. Estos recursos se administran a través de diversos proveedores de recursos en Resource Manager.

Administrador de recursos de Azure se basa en distintos proveedores tooprovide acceso tooyour de recursos. Hay tres proveedores de recursos principales: redes, almacenamiento y proceso. Este documento describen las características de Hola y las ventajas de hello proveedor de recursos de red, incluidos:

* **Metadatos** : puede agregar tooresources información mediante etiquetas. Estas etiquetas pueden tener usado tootrack utilización de recursos entre suscripciones y grupos de recursos.
* **Mayor control de la red** : los recursos de red están acoplados holgadamente y los puede controlar de forma más detallada. Esto significa que tiene más flexibilidad para administrar recursos de red de Hola.
* **Configuración más rápida** : dado que los recursos de red están acoplados holgadamente, puede crear y organizar los recursos de red en paralelo. Esto ha reducido drásticamente el tiempo de configuración.
* **Control de acceso basado en roles** -RBAC proporciona roles de forma predeterminada, con ámbito de seguridad específicos, en la creación de hello tooallowing de adición de roles personalizados para una administración segura.
* **La implementación y administración más fácil** -es más fácil toodeploy y administrar las aplicaciones, ya que puede crear una pila de toda la aplicación como una sola colección de recursos en un grupo de recursos. Y toodeploy más rápido, ya que puede implementar simplemente proporcionando una carga JSON de la plantilla.
* **Personalización rápida** -puede usar plantillas de estilo declarativo tooenable repetible y rápida personalización de las implementaciones.
* **Personalización repetible** -puede usar plantillas de estilo declarativo tooenable repetible y rápida personalización de las implementaciones.
* **Interfaces de administración** -se pueden usar cualquiera de hello siguientes interfaces toomanage los recursos:
  * API basadas en REST
  * PowerShell
  * .NET SDK
  * SDK de Node.JS
  * SDK de Java
  * Azure CLI
  * Portal de vista previa
  * Idioma de la plantilla de Resource Manager

## <a name="network-resources"></a>Recursos de red
Ahora puede administrar los recursos de red de forma independiente, en lugar de tener hacerlo a través de un recurso de proceso único (una máquina virtual). Esto garantiza un mayor grado de flexibilidad y agilidad a la hora de componer una infraestructura compleja y de gran escala en un grupo de recursos.

A continuación se presenta una vista conceptual de una implementación de ejemplo que implica una aplicación de varios niveles. Todos los recursos que vea, por ejemplo, las NIC, las direcciones IP públicas y las máquinas virtuales, pueden administrarse de forma independiente.

![Modelo de recursos de red](./media/resource-groups-networking/Figure2.png)

Cada recurso contiene un conjunto común de propiedades y un conjunto de propiedades individual. Hola las propiedades comunes son:

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **name** |Nombre de recurso único. Cada tipo de recurso tiene sus propias restricciones de nomenclatura. |PIP01, VM01, NIC01 |
| **ubicación** |Región de Azure en qué Hola reside el recurso |westus, eastus |
| **id** |URI único basado en la identificación |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Puede comprobar las propiedades individuales de recursos de hello las siguientes secciones se Hola.

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

## <a name="management-interfaces"></a>Interfaces de administración
Puede administrar los recursos de redes de Azure mediante distintas interfaces. En este documento, nos centraremos en las interfaces API de REST y las plantillas.

### <a name="rest-api"></a>API de REST
Como se mencionó anteriormente, se pueden administrar los recursos de red a través de una variedad de interfaces, incluidas API de REST, .NET SDK, SDK de Node.JS, SDK de Java, PowerShell, CLI, Portal de Azure y plantillas.

Hola API de Rest se ajustan toohello especificación del protocolo HTTP 1.1. estructura de Hello general URI de hello API se muestra a continuación:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

Y parámetros de hello entre llaves representan Hola siguientes elementos:

* **subscription-id** : identificador de su suscripción a Azure.
* **Resource-provider-namespace** -espacio de nombres de proveedor de Hola que se utiliza. valor de Hello para el proveedor de recursos de red de hello es *Microsoft.Network*.
* **nombre de la región** -nombre de la región de Azure de Hola

Hello métodos HTTP siguientes se admiten al realizar llamadas toohello API de REST:

* **COLOCAR** : se usan toocreate un recurso de un tipo determinado, modificar una propiedad de recurso o cambiar una asociación entre los recursos.
* **OBTENER** -tooretrieve información que se utiliza para un recurso de aprovisionamiento.
* **ELIMINAR** -usa toodelete un recurso existente.

Hola solicitud y respuesta ajustan tooa formato de carga JSON. Para obtener más información, consulte [API de administración de recursos de Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Idioma de la plantilla de Resource Manager
En recursos de toomanaging adición imperativamente (a través de las API o SDK), también puede usar un toobuild de estilo de programación declarativa y administrar recursos de red mediante Hola idioma de plantilla de administrador de recursos.

A continuación se proporciona una representación de una plantilla de ejemplo:

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

plantilla de Hello es principalmente una descripción de JSON de recursos de Hola y valores de la instancia de hello insertados a través de parámetros. ejemplo de Hola siguiente puede ser toocreate usa una red virtual con 2 subredes.

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

Tiene la opción de Hola de proporcionar valores de parámetro hello manualmente cuando se utiliza una plantilla, o puede usar un archivo de parámetros. ejemplo de Hola siguiente muestra un posible conjunto de toobe de valores de parámetro utilizado con plantilla Hola anterior:

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


Hola ventajas principales del uso de plantillas son:

* Puede crear una infraestructura compleja en un grupo de recursos de estilo declarativo. Hola orquestación de creación de recursos de hello, incluida la administración de dependencia, se controla mediante el Administrador de recursos.
* infraestructura de Hello puede crearse de forma repetible en diversas regiones y dentro de una región con solo cambiar parámetros.
* estilo declarativo Hola conduce tooshorter plazo para generar plantillas de Hola y efectuando infraestructura Hola.

Para ver plantillas de ejemplo, consulte [Plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).

Para obtener más información sobre Hola idioma de plantilla de administrador de recursos, consulte [idioma de plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

plantilla de ejemplo de Hola anterior utiliza la red virtual de Hola y recursos de la subred. Hay otros recursos de red que se pueden utilizar, como se muestra a continuación:

### <a name="using-a-template"></a>Uso de una plantilla
Puede implementar servicios tooAzure desde una plantilla mediante el uso de PowerShell, AzureCLI, o bien al realizar una toodeploy haga clic en desde GitHub. Servicios de toodeploy de una plantilla en GitHub, ejecute Hola pasos:

1. Abrir archivo de hello template3 desde GitHub. Como ejemplo, abra [Red virtual con dos subredes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Haga clic en **implementar tooAzure**y, a continuación, inicie sesión en toohello portal de Azure con sus credenciales.
3. Comprobar la plantilla de hello y, a continuación, haga clic en **guardar**.
4. Haga clic en **editar parámetros** y seleccione una ubicación, por ejemplo, *oeste de Estados Unidos*, para la red virtual de Hola y subredes.
5. Si es necesario, cambie hello **ADDRESSPREFIX** y **SUBNETPREFIX** parámetros y, a continuación, haga clic en **Aceptar**.
6. Haga clic en **seleccionar un grupo de recursos** y, a continuación, haga clic en el grupo de recursos de hello desea tooadd Hola virtuales y las subredes a. Como alternativa, puede crear un nuevo grupo de recursos haciendo clic en **Crear nuevo**.
7. Haga clic en **Crear**. Tenga en cuenta Hola icono mostrar **implementación de plantilla de aprovisionamiento**. Una vez que se realice la implementación de hello, verá un tooone similar de pantalla siguiente.

![Implementación de plantilla de ejemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Pasos siguientes
[Idioma de la plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Redes de Azure: plantillas utilizadas habitualmente](https://github.com/Azure/azure-quickstart-templates)

[Implementación de Azure Resource Manager frente a la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md)

[Información general sobre Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

