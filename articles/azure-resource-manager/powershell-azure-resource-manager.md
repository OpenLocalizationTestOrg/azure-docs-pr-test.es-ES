---
title: aaaManage Azure soluciones con PowerShell | Documentos de Microsoft
description: Usar PowerShell de Azure y el Administrador de recursos toomanage los recursos.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Administración de recursos con Azure PowerShell y Resource Manager
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [CLI de Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API DE REST](resource-manager-rest-api.md)
>
>

En este artículo, aprenderá cómo toomanage sus soluciones con PowerShell de Azure y Azure Resource Manager. Si no está familiarizado con Resource Manager, consulte [Información general de Resource Manager](resource-group-overview.md). Este tema se centra en las tareas de administración. Podrá:

1. Crear un grupo de recursos
2. Agregar un grupo de recursos de toohello de recursos
3. Agregar un recurso de toohello de etiqueta
4. Consulta de recursos según nombres y valores de etiqueta
5. Aplicar y quitar un bloqueo de recurso de Hola
6. Eliminación de un grupo de recursos

En este artículo no se muestra cómo toodeploy una suscripción de tooyour de plantilla de administrador de recursos. Esa información la puede encontrar en [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Introducción a Azure PowerShell

Si no ha instalado Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

Si ha instalado Azure PowerShell Hola anteriores, pero no han actualizado recientemente, considere la posibilidad de instalar la versión más reciente de Hola. Puede actualizar la versión de Hola a través de hello mismo método usado tooinstall lo. Por ejemplo, si ha usado Hola instalador de plataforma Web, inicie de nuevo y busque una actualización.

usar de la versión del módulo de recursos de Azure, hello toocheck Hola siguiente cmdlet:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Este tema se ha actualizado a la versión 3.3.0. Si tiene una versión anterior, la experiencia podría no coincidir con los pasos de hello descritos en este tema. Para obtener documentación sobre los cmdlets de hello en esta versión, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure
Antes de trabajar en la solución, debe iniciar sesión en la cuenta de tooyour.

toolog en tooyour cuenta de Azure, use hello **AzureRmAccount de inicio de sesión** cmdlet.

```powershell
Login-AzureRmAccount
```

Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.

Hola cmdlet devuelve información sobre la toouse de suscripción hello y cuenta para tareas de Hola.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Si tiene más de una suscripción, puede cambiar tooa otra suscripción. En primer lugar, vamos a ver todas las suscripciones de Hola para su cuenta.

```powershell
Get-AzureRmSubscription
```

Se devuelven las suscripciones habilitadas y deshabilitadas.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa otra suscripción, proporcione el nombre de la suscripción de hello con hello **AzureRmContext conjunto** cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Antes de implementar cualquier suscripción de recursos de tooyour, debe crear un grupo de recursos que va a contener recursos de Hola.

toocreate un grupo de recursos, utilice hello **AzureRmResourceGroup New** cmdlet. comando de Hello usa hello **nombre** toospecify parámetro un nombre para el grupo de recursos de Hola y Hola **ubicación** parámetro toospecify su ubicación.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

salida de Hello es Hola siguiendo el formato:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Si necesita tooretrieve grupo de recursos de hello más tarde, utilice Hola siguiente cmdlet:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget todos los grupos de recursos en su suscripción de Hola, no se especifica un nombre:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Agregar grupo de recursos de tooa de recursos
tooadd un grupo de recursos de toohello de recursos, puede usar hello **New-AzureRmResource** cmdlet o un cmdlet que es de tipo toohello específico del recurso que está creando (como **AzureRmStorageAccount New**). Le resultará más fácil toouse un cmdlet que es el tipo de recurso específico tooa porque incluye parámetros para las propiedades de Hola que son necesarios para el nuevo recurso de Hola. toouse **New-AzureRmResource**, debe conocer todos los tooset de propiedades de hello sin que se le solicite para ellos.

Sin embargo, al agregar un recurso a través de los cmdlets podría producir confusión futuras porque el nuevo recurso de hello no existe en una plantilla de administrador de recursos. Microsoft recomienda que se defina la infraestructura de hello para la solución de Azure en una plantilla de administrador de recursos. Las plantillas permiten tooreliably e implementación varias veces la solución. En este tema, creará una cuenta de almacenamiento con un cmdlet de PowerShell, pero más tarde generará una plantilla a partir de su grupo de recursos.

Hola siguiente cmdlet crea una cuenta de almacenamiento. En lugar de usar el nombre de Hola que se muestra en el ejemplo de Hola, proporcione un nombre único para la cuenta de almacenamiento de Hola. nombre de Hello debe tener entre 3 y 24 caracteres de longitud y usar solo números y letras en minúsculas. Si usas nombre Hola que se muestra en el ejemplo de Hola, recibirá un error porque ese nombre ya está en uso.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Si debe tooretrieve este recurso más adelante, utilice Hola siguiente cmdlet:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Agregar una etiqueta

Las etiquetas permiten tooorganize los recursos según las propiedades de toodifferent. Por ejemplo, puede tener varios recursos en distintos grupos de recursos que pertenecen toohello mismo departamento. Puede aplicar un toomark departamento etiqueta y el valor toothose recursos usarlas como pertenecientes toohello misma categoría. O bien, puede marcar si un recurso se usa en un entorno de producción o de prueba. En este tema, aplicar etiquetas tooonly un recurso, pero en su entorno lo más probable es que tiene sentido tooapply etiquetas tooall sus recursos.

Hola siguiente cmdlet aplica la cuenta de almacenamiento de dos etiquetas tooyour:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Las etiquetas se actualizan como un único objeto. en primer lugar, tooadd un recurso de tooa de etiqueta que ya incluye etiquetas, recuperar las etiquetas existentes Hola. Agregar Hola etiqueta toohello objeto nuevo que contiene las etiquetas existentes hello y volver a aplicar todos los recursos de toohello de etiquetas de Hola.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Búsqueda de recursos

Hola de uso **AzureRmResource buscar** cmdlet tooretrieve recursos para las condiciones de búsqueda diferentes.

* tooget un recurso por su nombre, proporcionar hello **ResourceNameContains** parámetro:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget todos los recursos de hello en un grupo de recursos, proporcionar hello **ResourceGroupNameContains** parámetro:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget todos los recursos de hello con un nombre de etiqueta y el valor, proporcionar hello **TagName** y **TagValue** parámetros:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* recursos de hello tooall con un tipo de recurso determinado, proporcionar hello **ResourceType** parámetro:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Bloqueo de un recurso

Cuando necesite toomake seguro de que un recurso crítico no se elimina accidentalmente o modificado, aplicar un recurso de toohello de bloqueo. Puede especificar **CanNotDelete** o **ReadOnly**.

bloqueos de administración toocreate o delete, debe tener acceso demasiado`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` acciones. De las funciones integradas de hello, solo el propietario y el Administrador de acceso de usuario se conceden dichas acciones.

tooapply un bloqueo, utilice Hola siguiente cmdlet:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Hello recurso bloqueado en el anterior ejemplo de Hola no se puede eliminar hasta que se quite el bloqueo de Hola. tooremove un bloqueo, utilice:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Para más información sobre el establecimiento de bloqueos, consulte [Bloqueo de recursos con Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Eliminación de recursos o grupos de recursos
Puede quitar un recurso o un grupo de recursos. Al quitar un grupo de recursos, también quita todos los recursos de hello en ese grupo de recursos.

* un recurso del grupo de recursos de hello, use hello toodelete **Remove-AzureRmResource** cmdlet. Este cmdlet elimina el recurso de hello, pero no elimina el grupo de recursos de Hola.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete un grupo de recursos y todos sus recursos, use hello **Remove-AzureRmResourceGroup** cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Para los cmdlets, deberá tooconfirm que desea tooremove recursos de Hola o grupo de recursos. Si operación Hola elimina correctamente el recurso de Hola o grupo de recursos, devuelve **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Ejecución de scripts de Resource Manager con Azure Automation

Este tema muestra cómo tooperform operaciones básicas en los recursos con PowerShell de Azure. Para escenarios de administración más avanzados, normalmente desea toocreate una secuencia de comandos y volver a utilizar ese script según sea necesario o según una programación. [Automatización de Azure](../automation/automation-intro.md) le proporciona una manera de secuencias de comandos de tooautomate de uso frecuente que administran sus soluciones de Azure.

Hello en los temas siguientes muestran cómo toouse automatización de Azure, el Administrador de recursos y PowerShell tooeffectively realizan tareas de administración:

- Para más información sobre la creación de un Runbook, consulte [Mi primer runbook de PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Para más información sobre cómo trabajar con galerías de scripts, consulte [Galerías de runbooks y módulos para Azure Automation](../automation/automation-runbook-gallery.md).
- Para runbooks que iniciar y detener las máquinas virtuales, consulte [escenario de automatización de Azure: toocreate de etiquetas con formato JSON utilizando una programación para el inicio de la máquina virtual de Azure y cierre](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Para más información sobre Runbooks que iniciar y detienen máquinas virtuales fuera de las horas de trabajo, consulte [Inicio o detención de máquinas virtuales fuera de las horas de trabajo en Automation](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md).
* toolearn sobre la implementación de plantillas, consulte [implementar una aplicación con la plantilla de administrador de recursos de Azure](resource-group-template-deploy.md).
* Puede mover recursos tooa nuevo grupo de recursos existente. Para obtener ejemplos, vea [tooNew recursos Mover grupo de recursos o suscripción](resource-group-move-resources.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

