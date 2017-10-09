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
# <a name="publish-a-managed-application-for-internal-consumption"></a>Publicación de una aplicación administrada para consumo interno

Puede crear y publicar [aplicaciones administradas](managed-application-overview.md) de Azure que están diseñadas para los miembros de su organización. Por ejemplo, un departamento de TI puede publicar aplicaciones administradas que garantizan el cumplimiento de los estándares de la organización. Estas aplicaciones administradas están disponibles a través del catálogo de servicios de hello, no hello Azure Marketplace.

toopublish una aplicación administrada para el catálogo de servicios de hello, debe:

* Crear un paquete .zip que contiene archivos de plantilla requiere tres Hola.
* Decidir qué usuario, grupo o aplicación necesita tener acceso a grupo de recursos de toohello de suscripción de usuario de Hola.
* Crear definición de la aplicación hello administrado que señala el paquete de extensión .zip toohello y solicita acceso para identidad de Hola.

## <a name="create-a-managed-application-package"></a>Creación de un paquete de aplicación administrada

Hola primer paso es archivos de plantilla requiere tres de toocreate Hola. Los tres archivos de paquete en un archivo .zip y cargarlo ubicación accesible de tooan, por ejemplo, una cuenta de almacenamiento. Pasar un archivo .zip de toothis de vínculo cuando Hola creación administra la definición de la aplicación.

* **applianceMainTemplate.json**: este archivo define hello Azure administran los recursos que se suministran como parte del programa Hola a aplicación. plantilla de Hello es similar a una plantilla de administrador de recursos normal. Por ejemplo, toocreate una cuenta de almacenamiento a través de una aplicación administrada, applianceMainTemplate.json contiene:

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

* **mainTemplate.json**: los usuarios implementan esta plantilla al crear Hola aplicación administrada. Define recursos de aplicación Hola administrado, que es un tipo de recurso Microsoft.Solutions/appliances. Este archivo contiene todos los parámetros de Hola que necesita para recursos de hello en applianceMainTemplate.json.

  Establezca dos propiedades importantes en esta plantilla. En primer lugar, Hola **applianceDefinitionId** propiedad es Id. de Hola de definición de la aplicación hello administrado. Crear definición de hello más adelante en este tema. Al establecer este valor, debe decidir qué suscripción y toouse de grupo de recursos para almacenar Hola definiciones de aplicación administrado. Y debe decidir un nombre para la definición de Hola. Id. de Hello está en formato de hello:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  En segundo lugar, Hola **managedResourceGroupId** propiedad es Id. de Hola Hola del grupo de recursos donde hello recursos de Azure se crean. Puede asignar un valor para este nombre de grupo de recursos o dejar al usuario Hola proporcione un nombre. formato de Hola de Id. de hello es:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Hola de ejemplo siguiente muestra un archivo de mainTemplate.json. Especifica un grupo de recursos para los recursos de hello implementado. Id. de definición Hello es toouse de conjunto con nombre de una definición de **storageApp** en un grupo de recursos denominado **managedApplicationGroup**. Puede cambiar estos nombres diferentes de los valores toouse. Proporcionar su propio Id. de suscripción en la identificación de definición de Hola.

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

* **applianceCreateUiDefinition.json**: hello portal de Azure usa este archivo toogenerate Hola interfaz de usuario para los usuarios que creen Hola aplicación administrada. Defina cómo los usuarios proporcionan la entrad de cada parámetro. Puede usar opciones como una lista desplegable, un cuadro de texto, un cuadro de contraseña y otras herramientas de entrada. toolearn toocreate un archivo de definición de interfaz de usuario para una aplicación administrada, vea [empezar a trabajar con CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Hello en el ejemplo siguiente se muestra un archivo applianceCreateUiDefinition.json que permite el prefijo del nombre de cuenta de usuarios toospecify Hola almacenamiento a través de un cuadro de texto.

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

Después de que todos los archivos necesitado de hello están listos, empaquetar como un archivo zip. Hola tres archivos deben en nivel de raíz de hello del archivo .zip de Hola. Si los coloca en una carpeta, recibirá un error al crear Hola administra la definición de la aplicación que indica Hola requiere archivos no están presentes. Cargar tooan de ubicación accesible desde donde pueden utilizarse para la paquete Hola. resto Hola de este artículo se da por supuesto que existe el archivo .zip de hello en un contenedor de blobs de almacenamiento accesibles públicamente.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Creación de una aplicación o grupo de usuarios de Azure Active Directory

Hola segundo paso es tooselect un grupo de usuarios o una aplicación para la administración de recursos de hello en nombre de cliente de Hola. Este grupo de usuarios o la aplicación tiene permisos en hello recurso administrado correspondiente toohello función de grupo que se asigna. rol de Hello puede ser cualquier rol de Control de acceso basado en roles (RBAC) integrado como propietario o colaborador. También puede dar a un usuario individual recursos de permiso toomanage hello, pero suele asignar a este grupo de usuarios de tooa de permiso. toocreate un nuevo grupo de usuarios de Active Directory, vea [crear un grupo y agregar miembros en Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Necesita Id. de objeto de Hola de hello usuario grupo toouse para administrar recursos de Hola. Hola de ejemplo siguiente muestra cómo tooget Hola Id. de objeto de nombre para mostrar del grupo de hello:

```azurecli-interactive
az ad group show --group exampleGroupName
```

comando de ejemplo de Hola devuelve Hola después de salida:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

Identificador de objeto de hello simplemente tooretrieve, use:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Obtener Id. de definición de rol de Hola

A continuación, deberá Hola Id. de definición de rol de hello función integrada de RBAC desea toogrant acceso toohello usuario, grupo de usuarios o aplicaciones. Normalmente, se utiliza Hola propietario o el rol de colaborador o lector. Hola siguiente comando muestra cómo tooget Hola Id. de definición de rol para el rol de propietario de hello:


```azurecli-interactive
az role definition list --name owner
```

Este comando devuelve Hola después de salida:

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

Se necesita el valor de Hola de propiedad de "nombre" Hola desde el anterior ejemplo de Hola. Puede recuperar solo esa propiedad con:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Crear definición de la aplicación hello administrado

Si ya no dispone de un grupo de recursos para almacenar la definición de aplicación administrada, créelo ahora:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Ahora, crear recursos de definición de aplicación Hola administrado.

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

parámetros de Hello utilizados en el anterior ejemplo de Hola son:

* **grupo de recursos**: nombre de Hola Hola del grupo de recursos donde hello administra la definición de la aplicación se crea.
* **nivel de bloqueo**: tipo de Hola de bloqueo se coloca en el grupo de recursos administrados de Hola. Impide que el cliente de hello realizar operaciones no deseadas en este grupo de recursos. Actualmente, solo lectura es Hola solo admite el nivel de bloqueo. Cuando se especifica ReadOnly, cliente hello sólo puede leer recursos Hola presentes en el grupo de recursos administrados de Hola.
* **autorizaciones**: describe Id. principal de Hola y Hola identificador de definición de rol que son el grupo de recursos administrados de toohello de permiso de toogrant usado. Se especifica en formato de Hola de `<principalId>:<roleDefinitionId>`. También se pueden especificar varios valores para esta propiedad. Si se necesitan varios valores, se debe especificar en forma de hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Los valores van separados por un espacio.
* **uri de archivo de paquete**: Hola ubicación del paquete de aplicación administrada de Hola que contiene los archivos de plantilla de hello, que pueden ser un blob de almacenamiento de Azure.

## <a name="next-steps"></a>Pasos siguientes

* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).
* Para obtener ejemplos de archivos de hello, consulte [administrado ejemplos de aplicaciones](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).
* Para obtener información acerca de la publicación de aplicaciones administradas de toohello Azure Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).
* Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).
* toolearn toocreate un archivo de definición de interfaz de usuario para una aplicación administrada, vea [empezar a trabajar con CreateUiDefinition](managed-application-createuidefinition-overview.md).
