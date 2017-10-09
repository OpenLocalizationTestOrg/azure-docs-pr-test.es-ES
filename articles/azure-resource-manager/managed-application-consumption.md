---
title: "aplicación administrada de aaaConsume un Azure | Documentos de Microsoft"
description: "Describe cómo crear una aplicación administrada de Azure a partir de archivos publicados."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Uso de una aplicación administrada interna

Puede usar [aplicaciones administradas](managed-application-overview.md) de Azure que están diseñadas para los miembros de su organización. Por ejemplo, puede seleccionar aplicaciones administradas desde el departamento de TI que garantizan el cumplimiento normativo de los estándares de la organización. Estas aplicaciones administradas están disponibles a través de hello catálogo de servicios, no hello Azure Marketplace.

Antes de continuar con este artículo, debe tener una aplicación administrada disponible en el catálogo de servicios de Hola para su suscripción. Si nadie de la organización ha creado todavía una aplicación administrada, consulte [Publicación de una aplicación administrada para uso interno](managed-application-publishing.md).

Actualmente, se puede utilizar la CLI de Azure o hello tooconsume portal Azure una aplicación administrada.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Crear aplicación hello administrado mediante el portal de Hola

toodeploy una aplicación administrada a través del portal de hello, siga estos pasos:

1. Vaya toohello portal de Azure. Búsqueda de una **aplicación administrada del catálogo de servicios**.

   ![Aplicación administrada del catálogo de servicios](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Hola seleccione administra aplicación desea toocreate de lista de Hola de las soluciones disponibles. Seleccione **Crear**.

   ![Selección de aplicaciones administradas](./media/managed-application-consumption/select-offer.png)

1. Proporcionar valores para parámetros de Hola que sean necesarios tooprovision Hola recursos. Seleccione **Centro occidental de EE. UU.** como ubicación. Seleccione **Aceptar**.

   ![Parámetros de aplicaciones administradas](./media/managed-application-consumption/input-parameters.png)

1. plantilla de Hola valida valores de hello que proporcionó. Si la validación es correcta, seleccione **Aceptar** implementación de hello toostart.

   ![Validación de aplicaciones administradas](./media/managed-application-consumption/validation.png)

Una vez finalizada la implementación de hello, los recursos adecuados de hello definidos en la plantilla de Hola se aprovisionan en grupo de recursos administrados de hello proporcionada.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Crear aplicación hello administrado mediante la CLI de Azure

Hay dos toocreate formas una aplicación administrada mediante Azure CLI:

* Use el comando de hello para la creación de aplicaciones administradas.
* Use el comando de implementación de plantilla Normal Hola.

### <a name="use-hello-template-deployment-command"></a>Use el comando de implementación de plantilla Hola

Implementar archivo applianceMainTemplate.json Hola Hola proveedor creado.

Después, cree dos grupos de recursos. Hello primer grupo de recursos es donde hello recursos de la aplicación administrada que se crea: Microsoft.Solutions/appliances. segundo grupo de recursos de Hello contiene todos los recursos de hello definidos en mainTemplate.json. Hola ISV administra este grupo de recursos.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Use `westcentralus` como ubicación de Hola Hola del grupo de recursos.
>

toodeploy applianceMainTemplate.json en mainResourceGroup, Hola de uso siguiente comando:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Después de hello anterior se ejecuta de la plantilla, le pedirá Hola valores de parámetros de Hola que se definen en la plantilla de Hola. Además toohello parámetros que necesitan recursos tooprovision en una plantilla, es necesario que dos valores de parámetro de clave:

- **managedResourceGroupId**: Hola identificador hello de recursos de grupo contenedor Hola recursos definidos en applianceMainTemplate.json. Id. de Hello tiene el formato de hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. En el anterior ejemplo de Hola, lo del Id. de Hola de `managedResourceGroup`.
- **applianceDefinitionId**: Id. de Hola de hello administra recursos de la definición de aplicación. Este valor se proporciona por hello ISV.

> [!NOTE]
> publicador de Hello debe conceder el grupo de recursos de toohello de acceso que contiene la definición de la aplicación hello administrado. se crea el recurso de la definición de Hello en la suscripción del publicador de Hola. Por lo tanto, un usuario, el grupo de usuarios o la aplicación en el inquilino de cliente hello necesita acceso de lectura toothis recursos.

Cuando finaliza correctamente la implementación de hello, vea Hola administrado aplicación se crea en mainResourceGroup. se crea el recurso de storageAccount de Hello en managedResourceGroup.

### <a name="use-hello-create-command"></a>Hola use create, comando

Puede usar hello `az managedapp create` comando toocreate una aplicación administrada de hello administra la definición de la aplicación.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Id. de definición de dispositivo**: definición de aplicación creado en hello anterior paso administrada por Id. de recurso de Hola de hello. tooobtain este identificador, ejecute el siguiente comando de hello:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Este comando devuelve la definición de la aplicación hello administrado. Se necesita el valor de Hola de propiedad de Id. de Hola.

* **Identificador administrado rg**: nombre de Hola Hola de recursos de grupo contenedor Hola recursos definidos en applianceMainTemplate.json. Este grupo de recursos es el grupo de recursos administrados de Hola. Está administrado por el publicador de Hola. Si no existe, se crea.
* **grupo de recursos**: se crea el grupo de recursos de Hola donde hello administra el recurso de la aplicación. Hola Microsoft.Solutions/appliance recursos vive en este grupo de recursos.
* **parámetros**: Hola parámetros que son necesarios para los recursos de hello definidos en applianceMainTemplate.json.

## <a name="known-issues"></a>Problemas conocidos

Esta versión de vista previa incluye Hola problemas siguientes:

* Aparece un error de servidor interno 500 durante la creación de hello de aplicación hello administrado. Si experimenta este problema, es probable que toobe intermitente. Vuelva a intentar la operación de Hola.
* Se necesita un nuevo grupo de recursos para el grupo de recursos administrados de Hola. Si utiliza un grupo de recursos existente, se produce un error en la implementación de Hola.
* Hello grupo de recursos que contiene el recurso de hello Microsoft.Solutions/appliances debe crearse en hello **westcentralus** ubicación.

## <a name="next-steps"></a>Pasos siguientes

* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).
* Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).
* Para obtener información acerca de la publicación de aplicaciones administradas de toohello Azure Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).
* Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).
