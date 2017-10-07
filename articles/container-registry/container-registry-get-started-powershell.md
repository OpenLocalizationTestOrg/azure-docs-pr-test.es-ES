---
title: repositorios de registro del contenedor de aaaAzure | Documentos de Microsoft
description: "¿Cómo toouse repositorios de registro de contenedor de Azure para las imágenes de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Crear un registro de contenedor de Docker privado mediante hello Azure PowerShell
Usar comandos de [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate un registro de contenedor y administrar su configuración desde el equipo de Windows. También puede crear y administrar registros de contenedor con hello [portal de Azure](container-registry-get-started-portal.md), hello [CLI de Azure](container-registry-get-started-azure-cli.md), o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* En el fondo y conceptos, vea [Hola información general](container-registry-intro.md)
* Para una lista de los cmdlets compatibles, consulte el artículo sobre los [Cmdlets de administración de Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Requisitos previos
* **Azure PowerShell**: tooinstall y empezar a trabajar con Azure PowerShell, vea hello [las instrucciones de instalación](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Inicie sesión en tooyour suscripción de Azure ejecutando `Login-AzureRMAccount`. Para más información, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente. Asegúrese de que el grupo de recursos de hello está en una ubicación donde hello servicio de registro de contenedor es [disponibles](https://azure.microsoft.com/regions/services/). toocreate un grupo de recursos con PowerShell de Azure, consulte [Hola referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Cuenta de almacenamiento** (opcional): crear un estándar Azure [cuenta de almacenamiento](../storage/common/storage-introduction.md) tooback registro de contenedor de Hola Hola misma ubicación. Si no especifica una cuenta de almacenamiento al crear un registro con `New-AzureRMContainerRegistry`, comando hello crea uno automáticamente. toocreate un almacenamiento de la cuenta con PowerShell, vea [Hola referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Premium Storage no se admite actualmente.
* **Entidad de servicio** (opcional): cuando crea un registro con PowerShell, el acceso a este no está configurado de forma predeterminada. Según sus necesidades, puede asignar un registro de tooa principal de servicio de Azure Active Directory existente o crear y asignar una nueva. Como alternativa, puede habilitar la cuenta de usuario de administrador del registro de hello. Vea las secciones de hello más adelante en este artículo. Para obtener más información acerca del acceso del registro, consulte [autenticar con registro de contenedor de hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Creación de un registro de contenedor
Ejecute hello `New-AzureRMContainerRegistry` comando toocreate un registro de contenedor.

> [!TIP]
> Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números. nombre del registro de Hello en los ejemplos de hello `MyRegistry`, pero sustituir un nombre único de su elección.
>
>

Hola el siguiente comando utiliza Hola del registro de contenedor de parámetros mínimos toocreate `MyRegistry` en grupo de recursos de hello `MyResourceGroup` Hola Ee.uu. Central sur ubicación:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` es opcional. Si no se especifica, se crea una cuenta de almacenamiento con un nombre que consta del nombre del registro de hello y una marca de tiempo en hello especifica el grupo de recursos.

## <a name="assign-a-service-principal"></a>Asignación de una entidad de servicio
Usar comandos de PowerShell tooassign Azure Active Directory [entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registro. Hello entidad de servicio en estos ejemplos se asigna el rol de propietario de hello, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si desea.

### <a name="create-a-service-principal"></a>Creación de una entidad de servicio
En el siguiente comando de hello, se crea una nueva entidad de servicio. Especifique una contraseña segura con hello `-Password` parámetro.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Asignación de una entidad de servicio nueva o existente
Puede asignar un nuevo o por un registro de tooa principal de servicio existente. tooassign el registro de toohello de propietario rol acceso, que se ejecute un toohello similar de comando siguiente ejemplo:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Inicie sesión en el registro de toohello con la entidad de servicio de Hola
Después de asignar el registro de hello servicio toohello principal, puede iniciar sesión con hello siguiente comando:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Administración de las credenciales de administrador
Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada. Hello en los ejemplos siguientes muestran comandos de PowerShell toomanage credenciales de administrador de hello para el registro de contenedor.

### <a name="obtain-admin-user-credentials"></a>Obtención de las credenciales de administrador
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Habilitación del usuario de administrador para un registro existente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Deshabilitación del usuario de administrador para un registro existente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Pasos siguientes
* [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
