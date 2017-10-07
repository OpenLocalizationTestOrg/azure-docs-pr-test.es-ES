---
title: "Servicios de multimedia de aaaUpdate después de revertir el almacenamiento de claves de acceso | Documentos de Microsoft"
description: "En este artículo se proporcionan instrucciones sobre cómo tooupdate los servicios multimedia después de revertir el almacenamiento de claves de acceso."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Actualización de Media Services después de revertir las claves de acceso de almacenamiento

Cuando se crea una nueva cuenta de servicios de multimedia de Azure (AMS), también deberá tooselect un almacenamiento de Azure que es la cuenta utiliza toostore su contenido multimedia. Puede agregar tooyour de cuentas de almacenamiento más de una cuenta de servicios multimedia. Este tema se muestra cómo toorotate claves de almacenamiento. También muestra cómo las cuentas de almacenamiento de tooadd tooa cuenta de multimedia. 

acciones de hello tooperform descritas en este tema, debería utilizar [API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) y [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Para obtener más información, consulte [cómo toomanage Azure recursos con PowerShell y Administrador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Información general

Cuando se crea una nueva cuenta de almacenamiento, Azure genera dos claves de acceso de almacenamiento de 512 bits, que son utilizado tooauthenticate acceso a la cuenta de almacenamiento de tooyour. tookeep las conexiones de almacenamiento más seguras, se recomienda tooperiodically volver a generar y rotación la clave de acceso de almacenamiento. Dos claves de acceso (principales y secundarias) aparecen en orden tooenable se toomaintain conexiones toohello cuenta de almacenamiento mediante uno tener acceso a clave mientras regenera Hola otra clave de acceso. Este procedimiento se conoce también como "rotación de claves de acceso".

Servicios multimedia depende de una clave de almacenamiento proporcionada tooit. En concreto, localizadores hello toostream usado o descargan los activos dependen de tecla de acceso de almacenamiento especificada de Hola. Cuando se crea una cuenta de AMS tome una dependencia en la clave de acceso de almacenamiento principal de Hola de forma predeterminada, pero como un usuario puede actualizar la clave de almacenamiento de hello AMS tiene. Debe asegurarse de que los servicios de multimedia toolet saber qué toouse clave siguiendo los pasos descritos en este tema.  

>[!NOTE]
> Si tiene varias cuentas de almacenamiento, realizaría este procedimiento con cada una. orden de Hello en el que Rotar claves de almacenamiento no es fijo. Puede rotar la clave secundaria de hello en primer lugar y, a continuación, Hola principal clave o viceversa.
>
> Antes de ejecutar los pasos descritos en este tema en una cuenta de producción, asegúrese de que tootest ellos en una cuenta de preproducción.
>

## <a name="steps-toorotate-storage-keys"></a>Claves de almacenamiento de toorotate de pasos 
 
 1. Cambio Hola clave cuenta de almacenamiento principal a través del cmdlet de powershell de Hola o [Azure](https://portal.azure.com/) portal.
 2. Llame al cmdlet AzureRmMediaServiceStorageKeys de sincronización con los parámetros adecuados tooforce medios cuenta toopick las claves de cuenta de almacenamiento
 
    Hola de ejemplo siguiente muestra cómo toosync claves toostorage cuentas.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Espere una hora más o menos. Compruebe que están trabajando escenarios de transmisión por secuencias de Hola.
 4. Cambiar la clave secundaria de cuenta de almacenamiento mediante el cmdlet de powershell de Hola o portal de Azure.
 5. Llame a powershell AzureRmMediaServiceStorageKeys de sincronización con los parámetros adecuados tooforce medios cuenta toopick seguridad nuevas claves de cuenta de almacenamiento. 
 6. Espere una hora más o menos. Compruebe que están trabajando escenarios de transmisión por secuencias de Hola.
 
### <a name="a-powershell-cmdlet-example"></a>Un ejemplos de cmdlet de PowerShell 

Hello en el ejemplo siguiente se muestra cómo tooget Hola cuenta de almacenamiento y sincronizarla con cuenta de hello AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Cuentas de almacenamiento de información de pasos tooadd tooyour AMS cuenta

Hello siguiente tema muestra cómo las cuentas de almacenamiento de tooadd tooyour AMS cuenta: [adjuntar varios tooa de cuentas de almacenamiento cuenta de servicios multimedia](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Agradecimientos
Nos gustaría hello tooacknowledge siguientes personas que han contribuido a la creación de este documento: Cenk Dingiloglu, Gada Milán, Seva Titov.
