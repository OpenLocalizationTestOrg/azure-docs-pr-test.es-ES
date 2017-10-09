---
title: "aaaTroubleshoot los errores comunes de la implementación de Azure | Documentos de Microsoft"
description: "Describe cómo tooresolve errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "error de implementación, implementación de azure, implementar tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Solución de errores comunes de implementación de Azure con Azure Resource Manager
En este tema se describe cómo resolver algunos errores comunes con los que puede encontrarse al realizar una implementación de Azure.

Hola siguientes códigos de error se describe en este tema:

* [AccountNameInvalid](#accountnameinvalid)
* [Error de autorización](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Este código de error indica un error de implementación general, pero no es código de error de Hola que necesita toostart solución de problemas. código de error de Hola que realmente le ayuda a resolver el problema de hello suele ser un nivel por debajo de este error. Por ejemplo, hello siguiente imagen muestra hello **RequestDisallowedByPolicy** código de error que está por debajo del error de implementación de Hola.

![Visualización del código de error](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Al implementar un recurso (normalmente una máquina virtual), puede recibir Hola mensaje de error y de código de error siguiente:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Recibirá este error cuando el recurso de hello SKU que seleccionó (por ejemplo, el tamaño de máquina virtual) no está disponible para la ubicación de Hola que seleccionó. tooresolve este problema, necesita toodetermine que SKU están disponibles en una región. También puede usar PowerShell, portal de Hola o un toofind de operación de resto SKU disponibles.

- Para PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) y filtre por ubicación. Debe tener la versión más reciente de Hola de PowerShell para este comando.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  resultados de Hello incluyen una lista de SKU para la ubicación de Hola y las restricciones para esa SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Hola toouse [portal](https://portal.azure.com), inicie sesión en el portal de toohello y agregue un recurso a través de la interfaz de Hola. Cuando se establecen valores de hello, vea Hola SKU disponibles para ese recurso. No es necesario toocomplete implementación de Hola.

    ![SKU disponibles](./media/resource-manager-common-deployment-errors/view-sku.png)

- Hola toouse API de REST para máquinas virtuales, enviar Hola después de solicitud:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Devuelve disponible SKU y regiones en hello siguiendo el formato:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Si no se puede toofind una SKU adecuada en dicha región o una región alternativa que satisfaga sus necesidades empresariales, enviar un [solicitud SKU](https://aka.ms/skurestriction) tooAzure soporte técnico.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Si recibe este error, usa una suscripción que no está permitido tooaccess los servicios de Azure que no sea de Azure Active Directory. Cuando se necesita el portal clásico de hello tooaccess pero no se permiten toodeploy recursos tendrá este tipo de suscripción. tooresolve este problema, debe usar una suscripción que disponga de permisos de los recursos toodeploy.  

tooview las suscripciones disponibles con PowerShell, use:

```powershell
Get-AzureRmSubscription
```

Y suscripción actual tooset hello, use:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview las suscripciones disponibles con CLI de Azure 2.0, use:

```azurecli
az account list
```

Y suscripción actual tooset hello, use:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Este error puede tener distintos orígenes.

- Error de sintaxis

   Si recibe un mensaje de error que indica la validación de la plantilla no se pudo de hello, puede tener un problema de sintaxis en la plantilla.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Este error es fácil toomake porque las expresiones de plantilla pueden ser complejas. Por ejemplo, hello siguiente asignación de nombre de una cuenta de almacenamiento contiene un conjunto de corchetes, tres funciones, tres conjuntos de paréntesis, un conjunto de comillas simples y una propiedad:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Si no proporciona la sintaxis de coincidencia de hello, plantilla de hello genera un valor que es diferente de su intención.

   Cuando reciba este tipo de error, revise cuidadosamente la sintaxis de expresiones de Hola. Considere la posibilidad de utilizar un editor JSON como [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) o [Visual Studio Code](resource-manager-vs-code.md) que puede avisarlo de los errores de sintaxis.

- Longitudes de segmentos incorrectas

   Cuando el nombre del recurso de hello no está en formato correcto de hello, se produce otro error de plantilla no válido.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Un recurso de nivel de raíz debe tener un segmento de menos en nombre de Hola que en el tipo de recurso de Hola. Cada segmento se distingue por una barra diagonal. En el siguiente ejemplo de Hola, tipo de hello tiene dos segmentos y nombre de hello tiene un segmento, por lo que es un **nombre válido**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Pero es el siguiente ejemplo de Hola **no es un nombre válido** porque tiene Hola tantos segmentos como tipo hello.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Para obtener recursos secundarios, tipo de Hola y el nombre tienen Hola mismo número de segmentos. Este número de segmentos tiene sentido porque el nombre completo de Hola y el tipo secundario Hola incluye el tipo y el nombre del elemento primario de Hola. Por lo tanto, nombre completo de hello aún tiene un segmento de menos de tipo completo de Hola.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Al obtener segmentos Hola derecho pueden ser complicadas con tipos de administrador de recursos que se aplican a través de proveedores de recursos. Por ejemplo, aplicar un sitio web de recurso bloqueo tooa requiere un tipo con cuatro segmentos. Por lo tanto, el nombre de hello es tres segmentos:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Copy index is not expected (Índice de copia no esperado)

   Esto ocurre **InvalidTemplate** error cuando se haya aplicado hello **copia** tooa parte del elemento de plantilla de Hola que no admite este elemento. Sólo puede aplicar el tipo de recurso de hello copiar elemento tooa. No se puede aplicar copia tooa propiedad dentro de un tipo de recurso. Por ejemplo, aplicar copia tooa virtual machine, pero no se puede aplicar toohello OS discos para una máquina virtual. En algunos casos, puede convertir un recurso de primario de secundarios recursos tooa toocreate un bucle de copia. Para más información sobre cómo usar este elemento, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).

- El parámetro no es válido

   Si plantilla Hola especifica los valores permitidos para un parámetro y proporciona un valor que no es uno de esos valores, recibirá un toohello similar de mensaje siguiente error:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Vuelve a revisar Hola valores permitidos en la plantilla de Hola y proporcionar una durante la implementación.

- Se detectó una dependencia circular

   Recibirá este error cuando recursos dependen de ellos de forma que impide la implementación de Hola se inicie. Una combinación de interdependencias hace que dos o más recursos esperen otros recursos que también están esperando. Por ejemplo, resource1 depende de resource3, resource2 depende de resource1 y resource3 depende de resource2. Para resolver este problema, normalmente se eliminan las dependencias innecesarias. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound y ResourceNotFound
Cuando la plantilla incluye nombre Hola de un recurso que no se puede resolver, recibirá un error similar al:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Si estás intentando hello toodeploy falta el recurso de plantilla de hello, compruebe si tiene una dependencia de tooadd. Cuando es posible, Resource Manager optimiza la implementación mediante la creación de recursos en paralelo. Si un recurso se debe implementar después de otro recurso, necesita hello toouse **dependsOn** Hola de elemento en su toocreate plantilla una dependencia en otro recurso. Por ejemplo, al implementar una aplicación web, debe existir Hola plan de servicio de aplicaciones. Si no ha especificado Hola plan de servicio de aplicaciones depende de dicha aplicación Hola, Administrador de recursos crea los recursos en hello mismo tiempo. Recibirá un error que indica que hello no se encuentra el recurso de plan de servicio de aplicaciones, porque no existe todavía al intentar tooset una propiedad en la aplicación web de Hola. Evitar este error estableciendo la dependencia de hello en hello web app.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Para obtener sugerencias sobre cómo solucionar los errores de dependencia, consulte [Comprobación de la secuencia de implementación](#check-deployment-sequence).

También verá este error al recurso de hello existe en otro grupo de recursos que Hola uno está implementando en el. En ese caso, use hello [función resourceId](resource-group-template-functions-resource.md#resourceid) nombre completo de hello tooget del recurso de Hola.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Si intentas hello toouse [referencia](resource-group-template-functions-resource.md#reference) o [listKeys](resource-group-template-functions-resource.md#listkeys) funciones con un recurso que no se puede resolver, recibirá Hola siguiente error:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Busque una expresión que incluya hello **referencia** función. Compruebe que los valores de parámetro hello son correctos.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Cuando un recurso es un recurso de tooanother primario, recurso primario de hello debe existir antes de crear el recurso de hello secundario. Si aún no existe, recibirá Hola siguiente error:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Hola nombre de recurso de hello secundario incluye Hola primario. Por ejemplo, se podría definir una base de datos SQL como:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Sin embargo, si no especifica una dependencia en el recurso primario de hello, pueden obtener implementar recursos secundarios de hello antes que la primaria Hola. tooresolve este error incluyen una dependencia.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists y StorageAccountAlreadyTaken
Las cuentas de almacenamiento, debe proporcionar un nombre para el recurso de Hola que es único en Azure. Si no lo hace, recibirá un error como el siguiente:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Puede crear un nombre único mediante la concatenación de la convención de nomenclatura con el resultado de hello de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (función).

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Si implementa una cuenta de almacenamiento con hello el mismo nombre como una cuenta de almacenamiento existente en su suscripción, pero proporciona una ubicación diferente, recibirá un error en la cuenta de almacenamiento de Hola que indica que ya existe en una ubicación diferente. Elimine la cuenta de almacenamiento existente de hello, o proporcione Hola misma ubicación como Hola cuenta de almacenamiento existente.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Vea hello **AccountNameInvalid** error al intentar toogive un almacenamiento cuenta un nombre que incluya caracteres prohibidos. Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y usar solo números y letras minúsculas. Hola [uniqueString](resource-group-template-functions-string.md#uniquestring) función devuelve 13 caracteres. Si concatenar un prefijo toohello **uniqueString** como resultado, proporcione un prefijo que es de 11 caracteres o menos.

## <a name="badrequest"></a>BadRequest

Puede encontrar un estado BadRequest al proporcionar un valor no válido para una propiedad. Por ejemplo, si proporciona un valor incorrecto de SKU para una cuenta de almacenamiento, se produce un error en implementación Hola. toodetermine los valores válidos para la propiedad, mire hello [API de REST](/rest/api) para tipo de recurso de Hola que va a implementar.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound y MissingSubscriptionRegistration
Al implementar el recurso, puede recibir Hola siguiente código de error y de mensajes:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

O bien, puede recibir un mensaje similar que indica:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Recibirá estos errores por uno de estos tres motivos:

1. no se ha registrado el proveedor de recursos de Hello para la suscripción
2. Versión de API que no se admite para el tipo de recurso de Hola
3. No se admite para el tipo de recurso de Hola de ubicación

mensaje de error de Hello debe proporcionarle sugerencias para ubicaciones de hello compatible y versiones de API. Puede cambiar su tooone plantilla de hello valores sugeridos. Mayoría de los proveedores se registra automáticamente por hello Azure interfaz de línea de comandos de portal o hello usa, pero no todas. Si no ha utilizado un proveedor de recursos determinado antes, deberá tooregister ese proveedor. Puede obtener más información sobre los proveedores de recursos a través de PowerShell o la CLI de Azure.

**Portal**

Puede ver el estado de registro de hello y registrar un espacio de nombres de proveedor de recursos a través del portal de Hola.

1. Para la suscripción, seleccione **Proveedores de recursos**.

   ![seleccionar proveedores de recursos](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Mire Hola lista de proveedores de recursos y, si es necesario, seleccione hello **registrar** proveedor de recursos de vínculo tooregister Hola de tipo hello que estamos toodeploy.

   ![Enumeración de proveedores de recursos](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee el estado de registro, use **AzureRmResourceProvider Get**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister un proveedor, utilice **AzureRmResourceProvider Register** y proporcione el nombre de Hola de proveedor de recursos de hello desea tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

ubicaciones de hello admite tooget para un determinado tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hola tooget admite versiones de API para un determinado tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**CLI de Azure**

toosee si se registra el proveedor de hello, usar hello `azure provider list` comando.

```azurecli
az provider list
```

tooregister un proveedor de recursos, utilice hello `azure provider register` comando y especifique hello *espacio de nombres* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

ubicaciones de hello admite toosee y versiones de API para un tipo de recurso, use:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded y OperationNotAllowed
Podría tener problemas cuando una implementación supera una cuota, lo que podría suceder por grupo de recursos, suscripciones, cuentas y otros ámbitos. Por ejemplo, puede ser su suscripción configurado toolimit Hola número de núcleos de una región. Si intentas toodeploy una máquina virtual con más núcleos que permiten la cantidad de hello, recibirá un error que se superó la cuota de Hola que indica.
Para obtener información completa de las cuotas, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).

tooexamine las cuotas de suscripción para núcleos, puede usar hello `azure vm list-usage` comando hello CLI de Azure. Hola de ejemplo siguiente muestra esa cuota de núcleos de Hola para una cuenta de evaluación gratuita es 4:

```azurecli
az vm list-usage --location "South Central US"
```

Que devuelve:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Si implementa una plantilla que crea más de cuatro núcleos en la región del oeste de Estados Unidos de hello, obtendrá un error de implementación que el siguiente aspecto:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

O bien en PowerShell, puede usar hello **AzureRmVMUsage Get** cmdlet.

```powershell
Get-AzureRmVMUsage
```

Que devuelve:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

En estos casos, debe ir toohello portal y archivo un tooraise de problema de soporte técnico de su cuota de región de hello en el que desea toodeploy.

> [!NOTE]
> Recuerde que para los grupos de recursos, cuota de hello es para cada región individual, no para la suscripción completa de Hola. Si necesita toodeploy 30 núcleos zona horaria del Pacífico occidental, deberá tooask para 30 núcleos de administrador de recursos zona horaria del Pacífico occidental. Si necesita toodeploy 30 núcleos en cualquiera de hello regiones toowhich tiene acceso, deberá solicitar 30 núcleos de administrador de recursos en todas las regiones.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Cuando reciba mensajes de bienvenida del error:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Probablemente ha intentado toolink tooa plantillas anidadas que no está disponible. Vuelve a revisar hello URI proporcionado para plantillas anidadas Hola. Si existe en la plantilla de hello en una cuenta de almacenamiento, asegúrese de hello URI es accesible. Puede que necesite toopass un token de SAS. Para más información, consulte [Uso de plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Recibirá este error cuando la suscripción incluye una directiva de recursos que impide que una acción que está intentando tooperform durante la implementación. En el mensaje de error de hello, busque el identificador de directiva de Hola.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

En **PowerShell**, proporcionar ese identificador de directiva como hello **identificador** detalles del parámetro tooretrieve acerca de la directiva de Hola que bloquea la implementación.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

En **Azure CLI**, proporcione Hola nombre de definición de directiva de hello:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Para obtener más información, vea Hola siguientes artículos:

- [Error RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Usar Directiva toomanage recursos y controlar el acceso](resource-manager-policy.md).

## <a name="authorization-failed"></a>Error de autorización
Puede recibir un error durante la implementación porque hello cuenta o intentar recursos de hello toodeploy entidad de servicio no tiene acceso tooperform esas acciones. Azure Active Directory permite a usted o su toocontrol administrador qué identidades pueden tener acceso a los recursos con un alto grado de precisión. Por ejemplo, si su cuenta se asigna el rol de lector toohello, no está toocreate capaz de recursos. En ese caso, debería ver un mensaje de error que indica que hubo un error de autorización.

Para más información sobre el control de acceso basado en roles, consulte [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de la auditoría de acciones, vea [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).
* toolearn acerca de los errores de hello toodetermine de acciones durante la implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).
