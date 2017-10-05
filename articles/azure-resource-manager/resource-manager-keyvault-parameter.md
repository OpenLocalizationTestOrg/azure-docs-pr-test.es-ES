---
title: Secreto de Key Vault con la plantilla de Resource Manager | Microsoft Docs
description: "Muestra cómo pasar un secreto de un almacén de claves como un parámetro durante la implementación."
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
ms.openlocfilehash: 1ca72599e67e79d42a3d430dbb13e89ea7265334
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="386a1-103">Uso de Key Vault para pasar el valor de parámetro seguro durante la implementación</span><span class="sxs-lookup"><span data-stu-id="386a1-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="386a1-104">Cuando tiene que pasar un valor seguro (por ejemplo, una contraseña) como un parámetro durante la implementación, puede recuperar el valor de [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="386a1-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="386a1-105">El valor se recupera haciendo referencia a Key Vault y al secreto del archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="386a1-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="386a1-106">El valor nunca se expone debido a que solo hace referencia a su identificador de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="386a1-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="386a1-107">No es necesario especificar manualmente el valor del secreto cada vez que implementan los recursos.</span><span class="sxs-lookup"><span data-stu-id="386a1-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="386a1-108">Key Vault puede existir en una suscripción diferente en la que está implementando el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="386a1-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="386a1-109">Cuando hace referencia a Key Vault, incluye el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="386a1-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="386a1-110">Al crear el almacén de claves, establezca la propiedad *enabledForTemplateDeployment* en *true*.</span><span class="sxs-lookup"><span data-stu-id="386a1-110">When creating the key vault, set the *enabledForTemplateDeployment* property to *true*.</span></span> <span data-ttu-id="386a1-111">Al establecer este valor en true, permite el acceso desde las plantillas de Resource Manager durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="386a1-111">By setting this value to true, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="386a1-112">Implementación de un almacén de claves y un secreto</span><span class="sxs-lookup"><span data-stu-id="386a1-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="386a1-113">Para crear un almacén de claves y un secreto, use la CLI de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="386a1-113">To create a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="386a1-114">Tenga en cuenta que el almacén de claves está habilitado para la implementación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="386a1-114">Notice that the key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="386a1-115">Para la CLI de Azure, utilice:</span><span class="sxs-lookup"><span data-stu-id="386a1-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="386a1-116">Para PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="386a1-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="386a1-117">Habilitación del acceso al secreto</span><span class="sxs-lookup"><span data-stu-id="386a1-117">Enable access to the secret</span></span>

<span data-ttu-id="386a1-118">Si usa un nuevo Key Vault o uno ya existente, asegúrese de que el usuario que implementa la plantilla puede acceder al secreto.</span><span class="sxs-lookup"><span data-stu-id="386a1-118">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="386a1-119">El usuario que implementa una plantilla que hace referencia a un secreto debe tener el permiso `Microsoft.KeyVault/vaults/deploy/action` para Key Vault.</span><span class="sxs-lookup"><span data-stu-id="386a1-119">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="386a1-120">Los roles [Propietario](../active-directory/role-based-access-built-in-roles.md#owner) y [Colaborador](../active-directory/role-based-access-built-in-roles.md#contributor) conceden este acceso.</span><span class="sxs-lookup"><span data-stu-id="386a1-120">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="386a1-121">También puede crear un [rol personalizado](../active-directory/role-based-access-control-custom-roles.md) que concede este permiso y agrega el usuario a ese rol.</span><span class="sxs-lookup"><span data-stu-id="386a1-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="386a1-122">Para más información sobre cómo agregar un usuario a un rol, vea [Asignación de un usuario a roles de administrador en Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="386a1-122">For information about adding a user to a role, see [Assign a user to administrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="386a1-123">Referencia a un secreto con identificador estático</span><span class="sxs-lookup"><span data-stu-id="386a1-123">Reference a secret with static ID</span></span>

<span data-ttu-id="386a1-124">La plantilla que recibe un secreto de Key Vault es como cualquier otra plantilla.</span><span class="sxs-lookup"><span data-stu-id="386a1-124">The template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="386a1-125">Esto se debe a que **se hace referencia al almacén de claves del archivo de parámetros, no de la plantilla**.</span><span class="sxs-lookup"><span data-stu-id="386a1-125">That's because **you reference the key vault in the parameter file, not the template.**</span></span> <span data-ttu-id="386a1-126">Por ejemplo, la siguiente plantilla implementa una base de datos SQL que incluye una contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="386a1-126">For example, the following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="386a1-127">El parámetro de contraseña se establece en una cadena segura.</span><span class="sxs-lookup"><span data-stu-id="386a1-127">The password parameter is set to a secure string.</span></span> <span data-ttu-id="386a1-128">Pero la plantilla no especifica de dónde procede ese valor.</span><span class="sxs-lookup"><span data-stu-id="386a1-128">But, the template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="386a1-129">Ahora, cree un archivo de parámetros para la plantilla anterior.</span><span class="sxs-lookup"><span data-stu-id="386a1-129">Now, create a parameter file for the preceding template.</span></span> <span data-ttu-id="386a1-130">En el archivo de parámetros, especifique un parámetro que coincida con el nombre del parámetro de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="386a1-130">In the parameter file, specify a parameter that matches the name of the parameter in the template.</span></span> <span data-ttu-id="386a1-131">Para el valor del parámetro, haga referencia al secreto del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="386a1-131">For the parameter value, reference the secret from the key vault.</span></span> <span data-ttu-id="386a1-132">Se hace referencia al secreto pasando el identificador de recurso de almacén de claves y el nombre del secreto.</span><span class="sxs-lookup"><span data-stu-id="386a1-132">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="386a1-133">En este ejemplo, ya debe existir el secreto del almacén de claves y se utiliza un valor estático para el mismo identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="386a1-133">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="386a1-134">Referencia a un secreto con identificador dinámico</span><span class="sxs-lookup"><span data-stu-id="386a1-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="386a1-135">En la sección anterior se mostró cómo pasar un identificador de recurso estático para el secreto del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="386a1-135">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="386a1-136">Sin embargo, en algunos escenarios, debe hacer referencia a un secreto del Almacén de claves que varía en función de la implementación actual.</span><span class="sxs-lookup"><span data-stu-id="386a1-136">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="386a1-137">En ese caso, no se puede codificar el identificador de recurso en el archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="386a1-137">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="386a1-138">Desafortunadamente, no se puede generar dinámicamente el identificador de recurso en el archivo de parámetros, ya que no se permiten expresiones de plantilla en este tipo de archivos.</span><span class="sxs-lookup"><span data-stu-id="386a1-138">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="386a1-139">Para generar dinámicamente el identificador de recurso de un secreto del almacén de claves, debe mover los recursos que necesite el secreto a una plantilla anidada.</span><span class="sxs-lookup"><span data-stu-id="386a1-139">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="386a1-140">En la plantilla principal, agregue la plantilla anidada y pase un parámetro que contenga el identificador de recurso generado dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="386a1-140">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="386a1-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="386a1-141">Next steps</span></span>
* <span data-ttu-id="386a1-142">Para obtener información general sobre almacenes de claves, consulte el artículo de [introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="386a1-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="386a1-143">Para obtener ejemplos completos de secretos de clave de referencia, consulte [Ejemplos del Almacén de claves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="386a1-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

