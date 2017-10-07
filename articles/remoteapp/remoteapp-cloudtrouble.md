---
title: "colecciones de nube de RemoteApp aaaTroubleshoot - creación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot RemoteApp en la nube de errores de creación de colección"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Solución de problemas de creación de colecciones en la nube de RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Si tiene problemas para crear una colección en la nube, consulte Hola siguiente información.

## <a name="your-image-is-invalid"></a>La imagen no es válida
Si ve un mensaje como "GoldImageInvalid" cuando se está esperando tooprovision Azure la colección, significa que la imagen de plantilla no cumple con hello [define los requisitos de la imagen](remoteapp-imagereqs.md). Por lo tanto, vaya a leerlos [requisitos](remoteapp-imagereqs.md), corrija la imagen e inténtelo de toocreate volver a la colección.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Errores comunes que se muestra en el portal de administración de Azure de Hola
    DNS server could not be reached
    ProvisioningTimeout

Las colecciones en la nube a menudo presentan errores durante la creación debido a que se usan imágenes personalizadas.  Si ve alguno de Hola por encima de los errores y se usa una imagen personalizada toocreate hello, consulte Hola siguientes cosas:

* Asegúrese de que esa imagen personalizada hello cargado cumple los requisitos de imagen.
* Con mayor frecuencia problema común de hello es que esa imagen hello no estaba correctamente preparada con Sysprep.  
* Comprobar la imagen de hello pueda arrancar dentro de Hyper-V o intente crear una VM de IAAS directamente en su suscripción de Azure con imagen Hola. Si se produce un error en la VM de hello tooboot y no se inicia, a continuación, esto normalmente indica que esa imagen personalizada hello no estaba preparada correctamente.  Compruebe la imagen personalizada de Hola se creó después de hello cómo toocreate una plantilla personalizada de la imagen de RemoteApp

Si está utilizando uno de imágenes de Microsoft de hello incluidas con su suscripción, intente volver a la colección de Hola de toocreate. Si no se soluciona el problema de hello, a continuación, póngase en contacto con soporte técnico de Microsoft.

    PlatformImageTrialModeOnly

Si ve este error normalmente significa que se hayan actualizado tooa pago cuenta pero que está tratando de toouse una imagen de Microsoft proporcionado es válida solo durante el modo de evaluación de hello del servicio de Hola. En este caso, intente toocreate volver a la colección en la nube, pero ser seguro toospecify Hola correcto imagen.

