---
title: aaaManage cuentas de servicios multimedia de Azure con PowerShell
description: "Obtenga información acerca de cómo cuentas toomanage servicios multimedia de Azure con cmdlets de PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Administración de cuentas de Servicios multimedia de Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocreate toobe capaz de una cuenta de servicios multimedia de Azure, debe tener una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Evaluación gratuita de Azure</a>.
> 
> 

## <a name="overview"></a>Información general
Este artículo enumeran los cmdlets de PowerShell de Azure de Hola para servicios de multimedia de Azure (AMS) en el marco de trabajo de hello Azure Resource Manager. Existen cmdlets de Hola Hola **Microsoft.Azure.Commands.Media** espacio de nombres.

## <a name="versions"></a>Versiones
**ApiVersion**:   "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Crea un servicio multimedia.

### <a name="syntax"></a>Sintaxis
Conjunto de parámetros: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Conjunto de parámetros: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Nombre |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

**-Location &lt;String&gt;**

Especifica la ubicación del recurso Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |2 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-StorageAccountId &lt;String&gt;**

Especifica una cuenta de almacenamiento principal asociado con el servicio de medios de Hola.

* Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.
* debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |3 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| Nombre del conjunto de parámetros |StorageAccountIdParamSet |
| ¿Aceptar caracteres comodín? |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Especifica las cuentas de almacenamiento asociado con el servicio de medios de Hola.

* Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.
* debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.
* Solo una cuenta de almacenamiento se puede identificar como principal.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |3 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| Nombre del conjunto de parámetros |StorageAccountsParamSet |
| ¿Aceptar caracteres comodín? |false |

**-Tags &lt;Hashtable&gt;**

Especifica una tabla hash de las etiquetas de Hola que están asociados con el servicio de medios de Hola.

* Ejemplo: @{"tag1"="value1";" tag2 "=: valor2"}

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| ¿Posición? |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Actualiza un servicio multimedia.

### <a name="syntax"></a>Sintaxis
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Nombre |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Especifica las cuentas de almacenamiento asociado con el servicio de medios de Hola.

* Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.
* debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.
* Solo una cuenta de almacenamiento se puede identificar como principal.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| ¿Posición? |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| Nombre del conjunto de parámetros |StorageAccountsParamSet |
| ¿Aceptar caracteres comodín? |false |

**-Tags &lt;Hashtable&gt;**

Especifica una tabla hash de las etiquetas de Hola que están asociados a este servicio de medios.

* etiquetas de Hola que están asociadas con el servicio de medios de Hola se reemplazan con el valor especificado por el cliente de Hola.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| ¿Posición? |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Quita un servicio multimedia.

### <a name="syntax"></a>Sintaxis
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |2 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |False |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Obtiene todos los servicios multimedia de un grupo de recursos o un servicio multimedia con un nombre determinado.

### <a name="syntax"></a>Sintaxis
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| Nombre del conjunto de parámetros |ResourceGroupParameterSet, AccountNameParameterSet |

¿Aceptar caracteres comodín?   false

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| Nombre del conjunto de parámetros |AccountNameParameterSet |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Obtiene las claves de un servicio multimedia.

### <a name="syntax"></a>Sintaxis
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Regenera una clave principal o secundaria de un servicio multimedia.

### <a name="syntax"></a>Sintaxis
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-KeyType &lt;KeyType&gt;**

Especifica el tipo de clave de Hola Hola del servicio de media.

* Principal o secundaria

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |2 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toothe.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Sincroniza las claves de cuenta de almacenamiento para una cuenta de almacenamiento asociada con el servicio de medios de Hola.

### <a name="syntax"></a>Sintaxis
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parámetros
**-ResourceGroupName &lt;String&gt;**

Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |0 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-AccountName &lt;String&gt;**

Especifica el nombre de Hola Hola del servicio de media.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |1 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**-StorageAccountId &lt;String&gt;**

Especifica la cuenta de almacenamiento de hello asociada con el servicio de medios de Hola.

| Alias | Id |
| --- | --- |
| ¿Necesario? |true |
| ¿Posición? |2 |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |true(ByPropertyName) |
| ¿Aceptar caracteres comodín? |false |

**&lt;CommandParameters&gt;**

Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.

### <a name="outputs"></a>Salidas
tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.

## <a name="next-step"></a>Paso siguiente
Revise las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

