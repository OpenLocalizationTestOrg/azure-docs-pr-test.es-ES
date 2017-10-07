---
title: "aaaManaging memorias caché Redis utilizando hello Azure explorador para IntelliJ | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage su redis de Azure almacena en memoria caché mediante el uso de hello Azure explorador para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a>Administración de cachés de Redis con hello Azure explorador para IntelliJ

Hola Explorador de Azure, que forma parte de hello Azure Toolkit for IntelliJ, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar redis memorias caché en su cuenta de Azure desde dentro de Hola IntelliJ IDE.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Creación de una instancia de Redis Cache mediante IntelliJ

Hola pasos le guiará por hello pasos toocreate una caché en redis mediante Hola Explorador de Azure.

1. Inicie sesión en tooyour cuenta de Azure siguiendo los pasos de Hola Hola [inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ] artículo.

1. Hola **explorador Azure** ventana de herramientas, expanda hello **Azure** nodo, haga clic en **memorias caché Redis**y, a continuación, haga clic en **crear caché en Redis**.

   ![Creación de un menú de Redis Cache][CR01]

1. Cuando Hola **nueva caché en Redis** aparece el cuadro de diálogo, especifique Hola siguientes opciones:

   ![Creación del cuadro de diálogo Nueva caché en Redis][CR02]

   a. **Nombre DNS**: especifica el subdominio DNS de Hola para caché en redis nueva hello, que se anteponen demasiado ". redis.cache.windows .net"; por ejemplo: *wingtiptoys.redis.cache.windows.net*.

   b. **Suscripción**: especifica Hola desea toouse para caché en redis Hola nueva suscripción de Azure.

   c. **Grupo de recursos**: especifica el grupo de recursos de hello para la caché de redis; debe toochoose de hello siguientes opciones:
      * **Crear nuevo**: Especifica que desea toocreate un nuevo grupo de recursos.
      * **Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.

   d. **Ubicación**: especifica la ubicación de Hola donde se crea la memoria caché de redis; por ejemplo, *West US*.

   e. **Nivel de precios**: especifica qué nivel de precios que se usa la memoria caché de redis; esta configuración determina el número de Hola de conexiones de cliente. (Para más información, consulte [Precios de Redis Cache]).

   f. **Puerto sin SSL**: especifica si Redis Cache permite las conexiones sin SSL. De forma predeterminada, se permiten solo las conexiones SSL.

1. Cuando haya especificado toda la configuración de Redis Cache, haga clic en **Aceptar**.

Una vez creada la memoria caché de redis, se mostrará en hello Explorador de Azure.

   ![Redis Cache en Azure Explorer][CR03]

> [!NOTE]
>
> Para obtener más información acerca de cómo configurar Azure redis configuración de la caché, vea [cómo tooconfigure Azure Redis Cache].
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a>Mostrar propiedades de hello de la caché en Redis en IntelliJ

1. Hola Explorador de Azure, haga clic en la memoria caché de redis y haga clic en **mostrar propiedades**.

   ![Azure explorador menú toodisplay propiedades de contexto de una caché de redis][SP01]

1. Hola explorador Azure muestra las propiedades de hello para la caché en redis.

   ![Propiedades de caché en Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Eliminar Redis Cache con IntelliJ

1. Hola Explorador de Azure, haga clic en la memoria caché de redis y haga clic en **eliminar**.

   ![Toodelete de menú contextual de Azure explorador una caché de redis][DE01]

1. Haga clic en **Sí** cuando se le pida toodelete su caché de redis.

   ![Eliminar una instancia de Redis Cache][DE02]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Para obtener más información acerca de las cachés de redis de Azure, opciones de configuración y precios, vea Hola siguientes vínculos:

* [Azure Redis Cache]
* [Documentación de Redis Cache]
* [Precios de Redis Cache]
* [cómo tooconfigure Azure Redis Cache]

<!-- URL List -->

[Precios de Redis Cache]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentación de Redis Cache]: ./redis-cache/index.md
[cómo tooconfigure Azure Redis Cache]: ./redis-cache/cache-configure.md
[inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
