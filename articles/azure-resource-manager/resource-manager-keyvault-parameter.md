---
title: "secreto del almacén de aaaKey con plantilla del Administrador de recursos | Documentos de Microsoft"
description: "Muestra cómo toopass un secreto de una clave del almacén como un parámetro durante la implementación."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Utilizar el valor de parámetro secure toopass de almacén de claves durante la implementación

Cuando necesite toopass un valor seguro (por ejemplo, una contraseña) como un parámetro durante la implementación, se puede recuperar el valor de Hola desde una [el almacén de claves de Azure](../key-vault/key-vault-whatis.md). Recupera el valor de hello haciendo referencia a almacén de claves de Hola y el secreto en el archivo de parámetros. valor de Hello nunca se expone como solo hace referencia a su identificador de almacén de claves. No es necesario toomanually escriba valor Hola de secreto de hello cada vez que implemente recursos Hola. almacén de claves de Hello puede existir en otra suscripción que va a implementar en el grupo de recursos de Hola. Al hacer referencia a almacén de claves de hello, incluir Hola Id. de suscripción.

Al crear el almacén de claves de hello, establezca hello *enabledForTemplateDeployment* propiedad demasiado*true*. Al establecer este valor tootrue, permite el acceso desde plantillas de administrador de recursos durante la implementación.  

## <a name="deploy-a-key-vault-and-secret"></a>Implementación de un almacén de claves y un secreto

toocreate un almacén de claves y el secreto, utilice Azure CLI o PowerShell. Tenga en cuenta que ese almacén de claves de hello está habilitado para la implementación de plantilla. 

Para la CLI de Azure, utilice:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Para PowerShell, use:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Habilitar el secreto de toohello de acceso

Si usas un almacén de claves nuevo o uno ya existente, asegúrese de ese usuario Hola implementar plantilla Hola puede tener acceso secreto Hola. implementación de una plantilla que hace referencia a un secreto de usuario de Hello debe tener hello `Microsoft.KeyVault/vaults/deploy/action` permiso para el almacén de claves de Hola. Hola [propietario](../active-directory/role-based-access-built-in-roles.md#owner) y [colaborador](../active-directory/role-based-access-built-in-roles.md#contributor) roles ambos conceden este acceso. También puede crear un [roles personalizados](../active-directory/role-based-access-control-custom-roles.md) que concede este permiso y agregar rol de hello usuario toothat. Para obtener información acerca de cómo agregar un rol de usuario tooa, consulte [asignar roles de tooadministrator en Azure Active Directory de un usuario](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Referencia a un secreto con identificador estático

plantilla de Hola que recibe un secreto de almacén de claves es como cualquier otra plantilla. Esto es así porque **hace referencia a almacén de claves de Hola Hola archivo de parámetros, no la plantilla de Hola.** Por ejemplo, hello sigue template implementa una base de datos SQL que incluye una contraseña de administrador. el parámetro de contraseña Hola se establece la cadena segura tooa. Sin embargo, plantilla hello no especifica dónde procede ese valor.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Ahora, cree un archivo de parámetro para hello anterior plantilla. En el archivo de parámetros de hello, especificar un parámetro que coincida con hello nombre del parámetro de hello en plantilla Hola. Valor de parámetro hello, hacer referencia a Hola secreto del almacén de claves de Hola. Hacer referencia a secreto Hola pasando el identificador de recurso de Hola de almacén de claves de Hola y el nombre de Hola de secreto de Hola. En el siguiente ejemplo de Hola, ya debe existir el secreto del almacén de claves de Hola y proporcionar un valor estático para su identificador de recurso.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Referencia a un secreto con identificador dinámico

sección anterior de Hola se ha explicado cómo toopass un identificador de recurso estático para la clave de hello almacén secreto. Sin embargo, en algunos escenarios, debe tooreference un secreto de almacén de claves que varía en función de la implementación actual de Hola. En ese caso, no se puede codificar Hola Id. de recurso en el archivo de parámetros de hello. Lamentablemente, no se puede generar dinámicamente Id. de recurso de hello en el archivo de parámetros de hello porque no se permiten expresiones de plantilla en el archivo de parámetros de hello.

toodynamically generar Id. de recurso de Hola para un secreto de almacén de claves, debe mover los recursos de Hola que necesita el secreto de hello en una plantilla anidada. En la plantilla principal, puede agregar plantillas anidadas de Hola y pasa un parámetro que contiene el identificador de recurso de hello generada dinámicamente.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información general sobre almacenes de claves, consulte el artículo de [introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).
* Para obtener ejemplos completos de secretos de clave de referencia, consulte [Ejemplos del Almacén de claves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

