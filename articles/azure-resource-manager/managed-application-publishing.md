---
title: "aaaCreate y publicar una aplicación de catálogo que administra el servicio de Azure | Documentos de Microsoft"
description: "Muestra cómo toocreate una Azure administra la aplicación que está destinado a los miembros de su organización."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="82e53-103">Publicación de una aplicación administrada para consumo interno</span><span class="sxs-lookup"><span data-stu-id="82e53-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="82e53-104">Puede crear y publicar [aplicaciones administradas](managed-application-overview.md) de Azure que están diseñadas para los miembros de su organización.</span><span class="sxs-lookup"><span data-stu-id="82e53-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="82e53-105">Por ejemplo, un departamento de TI puede publicar aplicaciones administradas que garantizan el cumplimiento de los estándares de la organización.</span><span class="sxs-lookup"><span data-stu-id="82e53-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="82e53-106">Estas aplicaciones administradas están disponibles a través del catálogo de servicios de hello, no hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="82e53-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="82e53-107">toopublish una aplicación administrada para el catálogo de servicios de hello, debe:</span><span class="sxs-lookup"><span data-stu-id="82e53-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="82e53-108">Crear un paquete .zip que contiene archivos de plantilla requiere tres Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="82e53-109">Decidir qué usuario, grupo o aplicación necesita tener acceso a grupo de recursos de toohello de suscripción de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="82e53-110">Crear definición de la aplicación hello administrado que señala el paquete de extensión .zip toohello y solicita acceso para identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="82e53-111">Creación de un paquete de aplicación administrada</span><span class="sxs-lookup"><span data-stu-id="82e53-111">Create a managed application package</span></span>

<span data-ttu-id="82e53-112">Hola primer paso es archivos de plantilla requiere tres de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="82e53-113">Los tres archivos de paquete en un archivo .zip y cargarlo ubicación accesible de tooan, por ejemplo, una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="82e53-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="82e53-114">Pasar un archivo .zip de toothis de vínculo cuando Hola creación administra la definición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82e53-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="82e53-115">**applianceMainTemplate.json**: este archivo define hello Azure administran los recursos que se suministran como parte del programa Hola a aplicación.</span><span class="sxs-lookup"><span data-stu-id="82e53-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="82e53-116">plantilla de Hello es similar a una plantilla de administrador de recursos normal.</span><span class="sxs-lookup"><span data-stu-id="82e53-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="82e53-117">Por ejemplo, toocreate una cuenta de almacenamiento a través de una aplicación administrada, applianceMainTemplate.json contiene:</span><span class="sxs-lookup"><span data-stu-id="82e53-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="82e53-118">**mainTemplate.json**: los usuarios implementan esta plantilla al crear Hola aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="82e53-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="82e53-119">Define recursos de aplicación Hola administrado, que es un tipo de recurso Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="82e53-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="82e53-120">Este archivo contiene todos los parámetros de Hola que necesita para recursos de hello en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="82e53-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="82e53-121">Establezca dos propiedades importantes en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="82e53-121">You set two important properties in this template.</span></span> <span data-ttu-id="82e53-122">En primer lugar, Hola **applianceDefinitionId** propiedad es Id. de Hola de definición de la aplicación hello administrado.</span><span class="sxs-lookup"><span data-stu-id="82e53-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="82e53-123">Crear definición de hello más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="82e53-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="82e53-124">Al establecer este valor, debe decidir qué suscripción y toouse de grupo de recursos para almacenar Hola definiciones de aplicación administrado.</span><span class="sxs-lookup"><span data-stu-id="82e53-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="82e53-125">Y debe decidir un nombre para la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="82e53-126">Id. de Hello está en formato de hello:</span><span class="sxs-lookup"><span data-stu-id="82e53-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="82e53-127">En segundo lugar, Hola **managedResourceGroupId** propiedad es Id. de Hola Hola del grupo de recursos donde hello recursos de Azure se crean.</span><span class="sxs-lookup"><span data-stu-id="82e53-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="82e53-128">Puede asignar un valor para este nombre de grupo de recursos o dejar al usuario Hola proporcione un nombre.</span><span class="sxs-lookup"><span data-stu-id="82e53-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="82e53-129">formato de Hola de Id. de hello es:</span><span class="sxs-lookup"><span data-stu-id="82e53-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="82e53-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="82e53-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="82e53-131">Hola de ejemplo siguiente muestra un archivo de mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="82e53-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="82e53-132">Especifica un grupo de recursos para los recursos de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="82e53-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="82e53-133">Id. de definición Hello es toouse de conjunto con nombre de una definición de **storageApp** en un grupo de recursos denominado **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="82e53-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="82e53-134">Puede cambiar estos nombres diferentes de los valores toouse.</span><span class="sxs-lookup"><span data-stu-id="82e53-134">You can change these values toouse different names.</span></span> <span data-ttu-id="82e53-135">Proporcionar su propio Id. de suscripción en la identificación de definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="82e53-136">**applianceCreateUiDefinition.json**: hello portal de Azure usa este archivo toogenerate Hola interfaz de usuario para los usuarios que creen Hola aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="82e53-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="82e53-137">Defina cómo los usuarios proporcionan la entrad de cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="82e53-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="82e53-138">Puede usar opciones como una lista desplegable, un cuadro de texto, un cuadro de contraseña y otras herramientas de entrada.</span><span class="sxs-lookup"><span data-stu-id="82e53-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="82e53-139">toolearn toocreate un archivo de definición de interfaz de usuario para una aplicación administrada, vea [empezar a trabajar con CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="82e53-140">Hello en el ejemplo siguiente se muestra un archivo applianceCreateUiDefinition.json que permite el prefijo del nombre de cuenta de usuarios toospecify Hola almacenamiento a través de un cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="82e53-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
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

<span data-ttu-id="82e53-141">Después de que todos los archivos necesitado de hello están listos, empaquetar como un archivo zip.</span><span class="sxs-lookup"><span data-stu-id="82e53-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="82e53-142">Hola tres archivos deben en nivel de raíz de hello del archivo .zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="82e53-143">Si los coloca en una carpeta, recibirá un error al crear Hola administra la definición de la aplicación que indica Hola requiere archivos no están presentes.</span><span class="sxs-lookup"><span data-stu-id="82e53-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="82e53-144">Cargar tooan de ubicación accesible desde donde pueden utilizarse para la paquete Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="82e53-145">resto Hola de este artículo se da por supuesto que existe el archivo .zip de hello en un contenedor de blobs de almacenamiento accesibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="82e53-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="82e53-146">Creación de una aplicación o grupo de usuarios de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82e53-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="82e53-147">Hola segundo paso es tooselect un grupo de usuarios o una aplicación para la administración de recursos de hello en nombre de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="82e53-148">Este grupo de usuarios o la aplicación tiene permisos en hello recurso administrado correspondiente toohello función de grupo que se asigna.</span><span class="sxs-lookup"><span data-stu-id="82e53-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="82e53-149">rol de Hello puede ser cualquier rol de Control de acceso basado en roles (RBAC) integrado como propietario o colaborador.</span><span class="sxs-lookup"><span data-stu-id="82e53-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="82e53-150">También puede dar a un usuario individual recursos de permiso toomanage hello, pero suele asignar a este grupo de usuarios de tooa de permiso.</span><span class="sxs-lookup"><span data-stu-id="82e53-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="82e53-151">toocreate un nuevo grupo de usuarios de Active Directory, vea [crear un grupo y agregar miembros en Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="82e53-152">Necesita Id. de objeto de Hola de hello usuario grupo toouse para administrar recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="82e53-153">Hola de ejemplo siguiente muestra cómo tooget Hola Id. de objeto de nombre para mostrar del grupo de hello:</span><span class="sxs-lookup"><span data-stu-id="82e53-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="82e53-154">comando de ejemplo de Hola devuelve Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="82e53-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="82e53-155">Identificador de objeto de hello simplemente tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="82e53-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="82e53-156">Obtener Id. de definición de rol de Hola</span><span class="sxs-lookup"><span data-stu-id="82e53-156">Get hello role definition ID</span></span>

<span data-ttu-id="82e53-157">A continuación, deberá Hola Id. de definición de rol de hello función integrada de RBAC desea toogrant acceso toohello usuario, grupo de usuarios o aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82e53-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="82e53-158">Normalmente, se utiliza Hola propietario o el rol de colaborador o lector.</span><span class="sxs-lookup"><span data-stu-id="82e53-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="82e53-159">Hola siguiente comando muestra cómo tooget Hola Id. de definición de rol para el rol de propietario de hello:</span><span class="sxs-lookup"><span data-stu-id="82e53-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="82e53-160">Este comando devuelve Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="82e53-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
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

<span data-ttu-id="82e53-161">Se necesita el valor de Hola de propiedad de "nombre" Hola desde el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="82e53-162">Puede recuperar solo esa propiedad con:</span><span class="sxs-lookup"><span data-stu-id="82e53-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="82e53-163">Crear definición de la aplicación hello administrado</span><span class="sxs-lookup"><span data-stu-id="82e53-163">Create hello managed application definition</span></span>

<span data-ttu-id="82e53-164">Si ya no dispone de un grupo de recursos para almacenar la definición de aplicación administrada, créelo ahora:</span><span class="sxs-lookup"><span data-stu-id="82e53-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="82e53-165">Ahora, crear recursos de definición de aplicación Hola administrado.</span><span class="sxs-lookup"><span data-stu-id="82e53-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="82e53-166">parámetros de Hello utilizados en el anterior ejemplo de Hola son:</span><span class="sxs-lookup"><span data-stu-id="82e53-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="82e53-167">**grupo de recursos**: nombre de Hola Hola del grupo de recursos donde hello administra la definición de la aplicación se crea.</span><span class="sxs-lookup"><span data-stu-id="82e53-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="82e53-168">**nivel de bloqueo**: tipo de Hola de bloqueo se coloca en el grupo de recursos administrados de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="82e53-169">Impide que el cliente de hello realizar operaciones no deseadas en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="82e53-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="82e53-170">Actualmente, solo lectura es Hola solo admite el nivel de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="82e53-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="82e53-171">Cuando se especifica ReadOnly, cliente hello sólo puede leer recursos Hola presentes en el grupo de recursos administrados de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e53-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="82e53-172">**autorizaciones**: describe Id. principal de Hola y Hola identificador de definición de rol que son el grupo de recursos administrados de toohello de permiso de toogrant usado.</span><span class="sxs-lookup"><span data-stu-id="82e53-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="82e53-173">Se especifica en formato de Hola de `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="82e53-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="82e53-174">También se pueden especificar varios valores para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="82e53-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="82e53-175">Si se necesitan varios valores, se debe especificar en forma de hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="82e53-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="82e53-176">Los valores van separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="82e53-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="82e53-177">**uri de archivo de paquete**: Hola ubicación del paquete de aplicación administrada de Hola que contiene los archivos de plantilla de hello, que pueden ser un blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="82e53-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e53-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82e53-178">Next steps</span></span>

* <span data-ttu-id="82e53-179">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="82e53-180">Para obtener ejemplos de archivos de hello, consulte [administrado ejemplos de aplicaciones](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="82e53-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="82e53-181">Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="82e53-182">Para obtener información acerca de la publicación de aplicaciones administradas de toohello Azure Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="82e53-183">Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="82e53-184">toolearn toocreate un archivo de definición de interfaz de usuario para una aplicación administrada, vea [empezar a trabajar con CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82e53-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
