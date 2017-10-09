---
title: "aaaAzure herramientas de línea de comandos multiplataforma basada en el Administrador de recursos para la aplicación Web de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola nuevo toomanage basado en Azure Resource Manager herramientas de línea de comandos multiplataforma sus aplicaciones Web de Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Uso de la CLI de XPlat basada en Azure Resource Manager para Azure App Service
> [!div class="op_single_selector"]
> * [CLI de Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Versión de Hola de versión de las herramientas de línea de comandos entre plataformas de Microsoft Azure 0.10.5, se han agregado nuevos comandos. Estos comandos proporcionan Hola usuario Hola capacidad toouse basado en el Administrador de recursos de Azure PowerShell comandos toomanage servicio de aplicaciones.

toolearn acerca de cómo administrar grupos de recursos, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Además, pruebe [CLI de Azure 2.0](https://github.com/Azure/azure-cli), una CLI de próxima generación escrito en Python para el modelo de implementación de administración de recursos de Hola.
>
>

## <a name="managing-app-service-plans"></a>Administración de planes del Servicio de aplicaciones
### <a name="create-an-app-service-plan"></a>Creación de un plan del Servicio de aplicaciones
toocreate un plan de servicio de aplicaciones, usar hello **appserviceplan azure crear** comando.

Siguientes son las descripciones de parámetros diferentes hello:

* **: grupo de recursos**: grupo de recursos que incluye el plan de servicio de aplicación Hola recién creado.
* **--nombre**: nombre del plan de servicio de aplicación Hola.
* **--location**: ubicación del plan de App Service.
* **--sku**: Hola deseado sku precios (Hola opciones son: F1 (Free). D1 (Compartida). B1 (Básico inferior), B2 (Básico medio) y B3 (Básico superior). S1 (Estándar inferior), S2 (Estándar medio) y S3 (Estándar superior). P1 (Premium inferior), P2 (Premium medio) y P3 (Premium superior).)
* **--instancias**: Hola el número de trabajos en el plan de servicio de aplicación Hola (el valor predeterminado es 1).

En el ejemplo se toouse este cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Creación de un plan de App Service de Linux

Usar Hola mismo **appserviceplan azure crear** comando con hello parámetro adicional **--islinux true**. Tenga en cuenta las restricciones de Hola y regiones que se describen en [Introducción tooApp servicio en Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Enumeración de planes del Servicio de aplicaciones existentes
usar planes de servicio de aplicación existente de toolist hello, **appserviceplan azure lista** comando.

toolist todos los planes de servicio de aplicaciones en un grupo de recursos específico, use:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

tooget un plan de servicio de aplicación específica, use **appserviceplan azure mostrar** comando:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configuración de un plan del Servicio de aplicaciones existente
toochange Hola de un plan de servicio de aplicación existente, utilice hello **appserviceplan azure config** comando. Puede cambiar Hola sku y el número de trabajos Hola 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Escalado de un plan del Servicio de aplicaciones
tooscale una existente aplicación Plan del servicio, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Cambiar Hola SKU de un Plan de servicio de aplicaciones
sku de hello toochange una existente aplicación de servicio del Plan de, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Eliminación de un plan del Servicio de aplicaciones
toodelete un plan de servicio de aplicación existente, todas asignadas aplicaciones necesidad toobe movido o eliminado en primer lugar. A continuación, usar Hola **webapp azure eliminar** comando se puede eliminar el plan de servicio de aplicación Hola.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Administración de aplicaciones de App Service
### <a name="create-a-web-app"></a>Creación de una aplicación web
toocreate una aplicación web, utilice hello **crear webapp azure** comando.

Siguientes son las descripciones de parámetros diferentes hello:

* **--nombre**: nombre de la aplicación web de Hola.
* **--plan**: nombre para el plan de servicio Hola utiliza toohost hello web app.
* **: grupo de recursos**: grupo de recursos que hospeda el plan de servicio de aplicación Hola.
* **--ubicación**: Hola ubicación de la aplicación web.

En el ejemplo se toouse este cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Eliminación de una aplicación existente
toodelete una aplicación existente, puede usar hello **webapp azure eliminar** comando. Necesita nombre de hello toospecify de aplicación hello y nombre de grupo de recursos de Hola.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Lista de aplicaciones existentes
toolist hello las aplicaciones existentes, utilice hello **webapp azure lista** comando.

toolist todas las aplicaciones en un grupo de recursos específico, use:

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget una aplicación específica, use hello **webapp azure mostrar** comando.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configuración de una aplicación existente
configuraciones de hello toochange y para una aplicación existente, use hello **conjunto de configuración de aplicación Web de azure** comando.

Ejemplo (1): cambiar versión de php Hola de una aplicación 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Ejemplo (2): Adición o cambio de la configuración de una aplicación

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow se puede cambiar la configuración de otra, use hello **-h de conjunto de configuración de aplicación Web de azure** comando.

### <a name="change-hello-state-of-an-existing-app"></a>Cambio de estado de Hola de una aplicación existente
#### <a name="restart-an-app"></a>Reinicio de una aplicación
toorestart una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Detener una aplicación
toostop una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Inicio de una aplicación
toostart una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Administración de perfiles de publicación de una aplicación
Cada aplicación tiene un perfil de publicación que puede ser toopublish usado el código.

#### <a name="get-publishing-profile"></a>Obtención de un perfil de publicación
tooget Hola de perfil para una aplicación, el uso de publicación:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Este comando devuelve el eco hello línea de comandos de toohello de nombre de usuario y contraseña de perfil de publicación.

### <a name="manage-app-hostnames"></a>Administración de nombres de host de aplicaciones
toomanage enlaces de nombre de host para la aplicación, utilice hello **los nombres de host de configuración de aplicación Web de azure** comando  

#### <a name="list-hostname-bindings"></a>Enumeración de enlaces de nombre de host
enlaces tooget Hola de nombre de host actual para una aplicación, use:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Adición de enlaces de nombre de host
tooadd hostname enlaces tooan a la aplicación, use:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Eliminación de enlaces de nombre de host
enlaces de nombre de host de toodelete, use:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca del soporte técnico de Azure Resource Manager CLI, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn acerca de cómo administrar el servicio de aplicaciones con PowerShell, vea [Using Azure Resource Manager-Based PowerShell tooManage aplicaciones Web de Azure.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn sobre el servicio de aplicaciones de Azure en Linux, consulte [Introducción tooApp servicio en Linux](app-service-linux-intro.md)
