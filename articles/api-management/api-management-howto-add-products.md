---
title: "aaaHow toocreate y publicar un producto en la administración de API de Azure"
description: "Obtenga información acerca de cómo toocreate y publicar productos en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>¿Cómo toocreate y publicar un producto en la administración de API de Azure
En la administración de API de Azure, un producto contiene una o varias API, así como de los términos de uso hello y cuota de uso. Una vez que se publica un producto, los desarrolladores pueden suscribirse toohello producto y empezar a API del producto de toouse Hola. tema de Hola proporciona una guía toocreating un producto, agregar una API y publicarlo para desarrolladores.

## <a name="create-product"></a>Creación de un producto
Las operaciones se agregan y configuran tooan API en el portal para desarrolladores de Hola. tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **productos** en el menú Hola Hola toodisplay izquierdo Hola **productos** página y haga clic en **agregar producto**.

![Productos][api-management-products]

![New product][api-management-add-new-product]

Escriba un nombre descriptivo para el producto de Hola Hola **nombre** campo y una descripción de producto de Hola Hola **descripción** campo.

Los productos de API Management pueden tener el estado **Abierto** o **Protegido**. Productos protegidos deben estar suscrito toobefore pueden usarse, mientras está abierto productos pueden utilizarse sin una suscripción. Comprobar **requieren suscripción** toocreate un producto protegido que requiere una suscripción. Se trata de una configuración predeterminada de Hola.

Comprobar **requieren la aprobación de suscripción** si desea un tooreview administrador y Aceptar o rechazar suscripción intenta toothis producto. Si Hola casilla está desactivada, los intentos de suscripción será aprobada automáticamente. Para obtener más información sobre las suscripciones, vea [producto de vista suscriptores tooa][View subscribers tooa product].

tooallow developer cuentas toosubscribe producto de toohello varias veces, compruebe hello **permitir múltiples suscripciones** casilla de verificación. Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse solo un producto de toohello sola vez.

![Suscripciones múltiples ilimitadas][api-management-unlimited-multiple-subscriptions]

recuento de hello toolimit de varias suscripciones simultáneas, comprobar hello **limitar el número de suscripciones simultáneas a** casilla de verificación y especifique el límite de la suscripción de Hola. En el siguiente ejemplo de Hola, suscripciones simultáneas son toofour limitado por cuenta de desarrollador.

![Para varias suscripciones][api-management-four-multiple-subscriptions]

Una vez configuradas todas las nuevas opciones de producto, haga clic en **guardar** nuevo producto de toocreate Hola.

![Productos][api-management-products-page]

> De forma predeterminada no están publicados nuevos productos y son visible toohello solo **administradores** grupo.
> 
> 

tooconfigure un producto, haga clic en el nombre de producto de hello en hello **productos** ficha.

## <a name="add-apis"></a>Producto de tooa agregar API
Hola **productos** página contiene cuatro vínculos de configuración: **resumen**, **configuración**, **visibilidad**, y  **Los suscriptores**. Hola **resumen** ficha es donde puede agregar las API y publicar o cancelar la publicación de un producto.

![Resumen][api-management-new-product-summary]

Antes de publicar un producto necesario tooadd una o varias API. toodo, haga clic en **tooproduct agregar API**.

![Add APIs][api-management-add-apis-to-product]

Seleccione Hola deseado API y haga clic en **guardar**.

## <a name="add-description"></a>Producto de agregar información descriptiva tooa
Hola **configuración** pestaña le permite tooprovide información detallada sobre el producto de hello como su propósito, hello las API que proporciona acceso a y otra información útil. contenido de Hola está destinada a los desarrolladores de Hola que llamará a la API de Hola y pueden escribirse en texto sin formato o en formato HTML.

![Product settings][api-management-product-settings]

Comprobar **requieren suscripción** toocreate un producto protegido que requiera un toobe de suscripción se usan o desactive Hola casilla toocreate un producto abierto que se pueda llamar sin una suscripción.

Seleccione **requieren la aprobación de suscripción** si desea toomanually aprobar todas las solicitudes de suscripción de producto. De forma predeterminada, todas las suscripciones de productos se conceden automáticamente.

tooallow developer cuentas toosubscribe producto de toohello varias veces, compruebe hello **permitir múltiples suscripciones** casilla de verificación y, opcionalmente, especifique un límite. Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse solo un producto de toohello sola vez.

Si lo desea, rellene hello **términos de uso** campo donde se describen los términos de Hola de uso de producto de Hola que deben aceptar los suscriptores de producto del pedido toouse Hola.

## <a name="publish-product"></a>Publicación de un producto
Para poder llamar a las API de hello en un producto, se debe publicar el producto de Hola. En hello **resumen** , haga clic para el producto de hello **publicar**y, a continuación, haga clic en **Sí, publicarlo** tooconfirm. toomake privado producto publicados anteriormente, haga clic en **Unpublish**.

![Publish product][api-management-publish-product]

## <a name="make-visible"></a>Realizar un toodevelopers visible del producto
Hola **visibilidad** pestaña le permite toochoose qué roles son toosee capaz de producto de hello en el portal para desarrolladores de Hola y suscriben toohello producto.

![Product visibility][api-management-product-visiblity]

tooenable o deshabilitar visibilidad de un producto para programadores de hello en un grupo, compruebe o desactive Hola casilla situada junto a grupo de hello y, a continuación, haga clic en **guardar**.

> Para obtener más información, consulte [cómo para desarrolladores de toomanage grupos toocreate y usar las cuentas de administración de API de Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Producto de tooa de los suscriptores de vista
Hola **suscriptores** ficha enumera los desarrolladores de Hola que se han suscrito toohello producto. Hello detalles y la configuración para cada programador puede verse haciendo clic en el nombre del desarrollador de Hola. En este ejemplo no los desarrolladores han suscrito aún toohello producto.

![Desarrolladores][api-management-developer-list]

## <a name="next-steps"></a>Pasos siguientes
Una vez Hola deseado las API se agregan y se publica el producto de hello, los desarrolladores pueden suscribirse toohello producto y comenzar toocall Hola API. Para obtener un tutorial que demuestre estos elementos, además de la configuración avanzada del producto, consulte el artículo que versa sobre la [creación y definición de configuraciones de productos avanzadas en Azure API Management][How create and configure advanced product settings in Azure API Management].

Para obtener más información sobre cómo trabajar con productos, vea Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
