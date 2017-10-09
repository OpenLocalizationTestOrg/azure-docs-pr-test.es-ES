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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="a1d08-103">Utilizar el valor de parámetro secure toopass de almacén de claves durante la implementación</span><span class="sxs-lookup"><span data-stu-id="a1d08-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="a1d08-104">Cuando necesite toopass un valor seguro (por ejemplo, una contraseña) como un parámetro durante la implementación, se puede recuperar el valor de Hola desde una [el almacén de claves de Azure](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1d08-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="a1d08-105">Recupera el valor de hello haciendo referencia a almacén de claves de Hola y el secreto en el archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="a1d08-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="a1d08-106">valor de Hello nunca se expone como solo hace referencia a su identificador de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a1d08-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="a1d08-107">No es necesario toomanually escriba valor Hola de secreto de hello cada vez que implemente recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="a1d08-108">almacén de claves de Hello puede existir en otra suscripción que va a implementar en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="a1d08-109">Al hacer referencia a almacén de claves de hello, incluir Hola Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="a1d08-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="a1d08-110">Al crear el almacén de claves de hello, establezca hello *enabledForTemplateDeployment* propiedad demasiado*true*.</span><span class="sxs-lookup"><span data-stu-id="a1d08-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="a1d08-111">Al establecer este valor tootrue, permite el acceso desde plantillas de administrador de recursos durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a1d08-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="a1d08-112">Implementación de un almacén de claves y un secreto</span><span class="sxs-lookup"><span data-stu-id="a1d08-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="a1d08-113">toocreate un almacén de claves y el secreto, utilice Azure CLI o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1d08-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="a1d08-114">Tenga en cuenta que ese almacén de claves de hello está habilitado para la implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="a1d08-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="a1d08-115">Para la CLI de Azure, utilice:</span><span class="sxs-lookup"><span data-stu-id="a1d08-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="a1d08-116">Para PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="a1d08-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="a1d08-117">Habilitar el secreto de toohello de acceso</span><span class="sxs-lookup"><span data-stu-id="a1d08-117">Enable access toohello secret</span></span>

<span data-ttu-id="a1d08-118">Si usas un almacén de claves nuevo o uno ya existente, asegúrese de ese usuario Hola implementar plantilla Hola puede tener acceso secreto Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="a1d08-119">implementación de una plantilla que hace referencia a un secreto de usuario de Hello debe tener hello `Microsoft.KeyVault/vaults/deploy/action` permiso para el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="a1d08-120">Hola [propietario](../active-directory/role-based-access-built-in-roles.md#owner) y [colaborador](../active-directory/role-based-access-built-in-roles.md#contributor) roles ambos conceden este acceso.</span><span class="sxs-lookup"><span data-stu-id="a1d08-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="a1d08-121">También puede crear un [roles personalizados](../active-directory/role-based-access-control-custom-roles.md) que concede este permiso y agregar rol de hello usuario toothat.</span><span class="sxs-lookup"><span data-stu-id="a1d08-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="a1d08-122">Para obtener información acerca de cómo agregar un rol de usuario tooa, consulte [asignar roles de tooadministrator en Azure Active Directory de un usuario](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1d08-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="a1d08-123">Referencia a un secreto con identificador estático</span><span class="sxs-lookup"><span data-stu-id="a1d08-123">Reference a secret with static ID</span></span>

<span data-ttu-id="a1d08-124">plantilla de Hola que recibe un secreto de almacén de claves es como cualquier otra plantilla.</span><span class="sxs-lookup"><span data-stu-id="a1d08-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="a1d08-125">Esto es así porque **hace referencia a almacén de claves de Hola Hola archivo de parámetros, no la plantilla de Hola.**</span><span class="sxs-lookup"><span data-stu-id="a1d08-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="a1d08-126">Por ejemplo, hello sigue template implementa una base de datos SQL que incluye una contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="a1d08-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="a1d08-127">el parámetro de contraseña Hola se establece la cadena segura tooa.</span><span class="sxs-lookup"><span data-stu-id="a1d08-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="a1d08-128">Sin embargo, plantilla hello no especifica dónde procede ese valor.</span><span class="sxs-lookup"><span data-stu-id="a1d08-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="a1d08-129">Ahora, cree un archivo de parámetro para hello anterior plantilla.</span><span class="sxs-lookup"><span data-stu-id="a1d08-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="a1d08-130">En el archivo de parámetros de hello, especificar un parámetro que coincida con hello nombre del parámetro de hello en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="a1d08-131">Valor de parámetro hello, hacer referencia a Hola secreto del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="a1d08-132">Hacer referencia a secreto Hola pasando el identificador de recurso de Hola de almacén de claves de Hola y el nombre de Hola de secreto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="a1d08-133">En el siguiente ejemplo de Hola, ya debe existir el secreto del almacén de claves de Hola y proporcionar un valor estático para su identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="a1d08-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="a1d08-134">Referencia a un secreto con identificador dinámico</span><span class="sxs-lookup"><span data-stu-id="a1d08-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="a1d08-135">sección anterior de Hola se ha explicado cómo toopass un identificador de recurso estático para la clave de hello almacén secreto.</span><span class="sxs-lookup"><span data-stu-id="a1d08-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="a1d08-136">Sin embargo, en algunos escenarios, debe tooreference un secreto de almacén de claves que varía en función de la implementación actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1d08-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="a1d08-137">En ese caso, no se puede codificar Hola Id. de recurso en el archivo de parámetros de hello.</span><span class="sxs-lookup"><span data-stu-id="a1d08-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="a1d08-138">Lamentablemente, no se puede generar dinámicamente Id. de recurso de hello en el archivo de parámetros de hello porque no se permiten expresiones de plantilla en el archivo de parámetros de hello.</span><span class="sxs-lookup"><span data-stu-id="a1d08-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="a1d08-139">toodynamically generar Id. de recurso de Hola para un secreto de almacén de claves, debe mover los recursos de Hola que necesita el secreto de hello en una plantilla anidada.</span><span class="sxs-lookup"><span data-stu-id="a1d08-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="a1d08-140">En la plantilla principal, puede agregar plantillas anidadas de Hola y pasa un parámetro que contiene el identificador de recurso de hello generada dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="a1d08-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1d08-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1d08-141">Next steps</span></span>
* <span data-ttu-id="a1d08-142">Para obtener información general sobre almacenes de claves, consulte el artículo de [introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a1d08-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="a1d08-143">Para obtener ejemplos completos de secretos de clave de referencia, consulte [Ejemplos del Almacén de claves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="a1d08-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

