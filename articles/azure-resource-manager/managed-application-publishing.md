---
title: "Creación y publicación de una aplicación administrada del catálogo de servicios de Azure | Microsoft Docs"
description: "Se explica cómo crear una aplicación administrada de Azure diseñada para los miembros de su organización."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="1b8c4-103">Publicación de una aplicación administrada para consumo interno</span><span class="sxs-lookup"><span data-stu-id="1b8c4-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="1b8c4-104">Puede crear y publicar [aplicaciones administradas](managed-application-overview.md) de Azure que están diseñadas para los miembros de su organización.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="1b8c4-105">Por ejemplo, un departamento de TI puede publicar aplicaciones administradas que garantizan el cumplimiento de los estándares de la organización.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="1b8c4-106">Estas aplicaciones administradas están disponibles a través del catálogo de servicios y no en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="1b8c4-107">Para publicar una aplicación administrada en el catálogo de servicios:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="1b8c4-108">Cree un paquete .zip que contenga los tres archivos de plantilla necesarios.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="1b8c4-109">Decida qué usuario, grupo o aplicación necesita acceder al grupo de recursos en la suscripción del usuario.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="1b8c4-110">Cree la definición de aplicación administrada que apunta al paquete .zip y solicita acceso para la identidad.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="1b8c4-111">Creación de un paquete de aplicación administrada</span><span class="sxs-lookup"><span data-stu-id="1b8c4-111">Create a managed application package</span></span>

<span data-ttu-id="1b8c4-112">El primer paso es crear los tres archivos de plantilla necesarios.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="1b8c4-113">Empaquete los tres archivos en un archivo ZIP y cárguelo en una ubicación accesible, como una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="1b8c4-114">Pase un vínculo a este archivo ZIP al crear la definición de aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="1b8c4-115">**applianceMainTemplate.json**: este archivo define los recursos de Azure que se aprovisionan como parte de la aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="1b8c4-116">La plantilla no difiere de una plantilla habitual de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="1b8c4-117">Por ejemplo, para crear una cuenta de almacenamiento con una aplicación administrada, el archivo applianceMainTemplate.json contiene:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="1b8c4-118">**mainTemplate.json**: los usuarios implementan esta plantilla al crear la aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="1b8c4-119">Define el recurso de la aplicación administrada, que es un tipo de recurso Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="1b8c4-120">Este archivo contiene todos los parámetros que necesita para los recursos en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="1b8c4-121">Establezca dos propiedades importantes en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-121">You set two important properties in this template.</span></span> <span data-ttu-id="1b8c4-122">En primer lugar, la propiedad **applianceDefinitionId** es el identificador de la definición de aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="1b8c4-123">Cree la definición más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-123">You create the definition later in this topic.</span></span> <span data-ttu-id="1b8c4-124">Al configurar este valor, debe decidir qué suscripción y grupo de recursos usar para almacenar las definiciones de aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="1b8c4-125">Además, debe decidir un nombre para la definición.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="1b8c4-126">El identificador tiene el formato:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="1b8c4-127">En segundo lugar, la propiedad **managedResourceGroupId** es el identificador del grupo de recursos donde se crean los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="1b8c4-128">Puede asignar un valor para este nombre de grupo de recursos o dejar que el usuario facilite un nombre.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="1b8c4-129">El formato del identificador es:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-129">The format of the ID is:</span></span>

  <span data-ttu-id="1b8c4-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="1b8c4-131">En el ejemplo siguiente se muestra un archivo mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="1b8c4-132">Especifica un grupo de recursos para los recursos implementados.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="1b8c4-133">El identificador de la definición está establecido para usar una definición con nombre **storageApp** en un grupo de recursos denominado **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="1b8c4-134">Puede cambiar estos valores para usar nombres distintos.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-134">You can change these values to use different names.</span></span> <span data-ttu-id="1b8c4-135">Proporcione su propio identificador de suscripción en el identificador de definición.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-135">Provide your own subscription ID in the definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="1b8c4-136">**applianceCreateUiDefinition.json**: Azure Portal usa este archivo para generar la interfaz de usuario para los usuarios que crean la aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="1b8c4-137">Defina cómo los usuarios proporcionan la entrad de cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="1b8c4-138">Puede usar opciones como una lista desplegable, un cuadro de texto, un cuadro de contraseña y otras herramientas de entrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="1b8c4-139">Para aprender a crear un archivo de definición de interfaz de usuario para una aplicación administrada, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="1b8c4-140">En el ejemplo siguiente se muestra un archivo applianceCreateUiDefinition.json que permite a los usuarios especificar el prefijo del nombre de la cuenta de almacenamiento a través de un cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="1b8c4-141">Después de que todos los archivos necesarios estén listos, empaquételos como un archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="1b8c4-142">Los tres archivos deben estar en el nivel raíz del archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="1b8c4-143">Si los coloca en una carpeta, recibe un error al crear la definición de aplicación administrada que indica que los archivos requeridos no están presentes.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="1b8c4-144">Cargue el paquete en una ubicación accesible desde donde pueda consumirse.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="1b8c4-145">En el resto de este artículo se asume que el archivo ZIP se encuentra en un contenedor de blobs de almacenamiento de acceso público.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="1b8c4-146">Creación de una aplicación o grupo de usuarios de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b8c4-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="1b8c4-147">El segundo paso consiste en seleccionar una aplicación o un grupo de usuarios para administrar los recursos en nombre del cliente.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="1b8c4-148">Este grupo de usuarios o esta aplicación tienen permisos en el grupo de recursos administrado, según el rol asignado.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="1b8c4-149">El rol puede ser cualquier rol de Control de acceso basado en roles (RBAC) integrado como propietario o colaborador.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="1b8c4-150">También puede conceder a un usuario individual permisos para administrar los recursos, pero este permiso se suele asignar a un grupo de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="1b8c4-151">Para crear un grupo de usuarios de Active Directory, consulte [Creación de un grupo y adición de miembros en Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="1b8c4-152">Necesita el identificador de objeto del grupo de usuarios que se usará para administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="1b8c4-153">En el ejemplo siguiente se muestra cómo obtener el identificador de objeto a partir del nombre para mostrar del grupo:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="1b8c4-154">El comando de ejemplo devuelve el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="1b8c4-155">Para recuperar solo el identificador de objeto, use:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="1b8c4-156">Obtención del identificador de definición de rol</span><span class="sxs-lookup"><span data-stu-id="1b8c4-156">Get the role definition ID</span></span>

<span data-ttu-id="1b8c4-157">A continuación, necesita el identificador de definición de rol para el rol RBAC integrado que desea para conceder acceso al usuario, al grupo de usuarios o a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="1b8c4-158">Por lo general, se usa el rol Propietario, Colaborador o Lector.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="1b8c4-159">El comando siguiente muestra cómo obtener el identificador de definición de rol para el rol Propietario:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="1b8c4-160">El comando devuelve el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="1b8c4-161">Se necesita el valor de la propiedad "name" del ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="1b8c4-162">Puede recuperar solo esa propiedad con:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="1b8c4-163">Creación de la definición de aplicación administrada</span><span class="sxs-lookup"><span data-stu-id="1b8c4-163">Create the managed application definition</span></span>

<span data-ttu-id="1b8c4-164">Si ya no dispone de un grupo de recursos para almacenar la definición de aplicación administrada, créelo ahora:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="1b8c4-165">Ahora, cree el recurso de la definición de aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-165">Now, create the managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="1b8c4-166">Los parámetros que se usan en el ejemplo anterior son:</span><span class="sxs-lookup"><span data-stu-id="1b8c4-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="1b8c4-167">**resource-group**: el nombre del grupo de recursos donde se creó la definición de aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="1b8c4-168">**lock-level**: el tipo de bloqueo aplicado al grupo de recursos administrado.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="1b8c4-169">Impide que el cliente realice operaciones no deseadas en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="1b8c4-170">Actualmente, ReadOnly es el único nivel de bloqueo admitido.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="1b8c4-171">Cuando se especifica ReadOnly, el cliente solo puede leer los recursos presentes en el grupo de recursos administrado.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="1b8c4-172">**authorizations**: describe el identificador de entidad de seguridad y el identificador de definición de rol que se usan para conceder el permiso al grupo de recursos administrado.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="1b8c4-173">Se especifica en el formato `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="1b8c4-174">También se pueden especificar varios valores para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="1b8c4-175">Si se necesitan varios valores, se deben especificar de esta forma `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="1b8c4-176">Los valores van separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="1b8c4-177">**package-file-uri**: la ubicación del paquete de aplicación administrada que contiene los archivos de plantilla, que puede ser una instancia de Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="1b8c4-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b8c4-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b8c4-178">Next steps</span></span>

* <span data-ttu-id="1b8c4-179">Para una introducción a las aplicaciones administradas, consulte [Introducción a las aplicaciones administradas](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1b8c4-180">Para ver ejemplos de los archivos, consulte los [ejemplos de aplicaciones administradas](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="1b8c4-181">Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="1b8c4-182">Para información sobre cómo publicar aplicaciones administradas en Azure Marketplace, consulte [Aplicaciones administradas de Azure en Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="1b8c4-183">Para información sobre cómo usar una aplicación administrada de Marketplace, consulte [Uso de aplicaciones administradas de Azure en Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="1b8c4-184">Para aprender a crear un archivo de definición de interfaz de usuario para una aplicación administrada, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b8c4-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
