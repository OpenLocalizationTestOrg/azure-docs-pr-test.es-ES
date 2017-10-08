---
title: "conceptos de información general y la clave de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las API, los productos, los roles, los grupos y otros conceptos clave de Administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>¿Qué es Administración de API?
Administración de API permite a las organizaciones a publicar API tooexternal, socios y potencial de hello toounlock de desarrolladores internos de sus datos y servicios. Las empresas en todas partes se busca tooextend sus operaciones como una plataforma digital, crear nuevos canales, buscar a nuevos clientes e implicarse más con los existentes. Administración de API proporciona Hola core competencias tooensure un programa de API correcta a través de la interacción de desarrollador, información empresarial, análisis, seguridad y protección.

Ver Hola siguiente vídeo para obtener información general de administración de API de Azure y obtenga información acerca de cómo toouse administración de API tooadd muchas características tooyour API, incluido el control de acceso, velocidad limitar, supervisión, el registro de eventos y las respuestas en caché, con el mínimo esfuerzo por su parte.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse administración de API, los administradores crean API. Cada API está formada por una o varias operaciones, y cada API se puede agregar tooone o más productos. toouse una API, los desarrolladores suscriben producto tooa que la contiene y, a continuación, puede llamar a operación Hola de API, las directivas de uso de tooany asunto que pueden estar en vigor.

En este tema se proporciona información general de los conceptos clave de Administración de API.

> [!NOTE]
> Para obtener más información, vea hello [administración de API basada en la nube: aprovechamiento de Hola de API de Power](http://j.mp/ms-apim-whitepaper) PDF notas del producto. Estas notas del producto introductorias sobre la administración de API por CITO Research cubren: 
> 
> * Desafíos y requisitos comunes de API
> * Desacoplamiento de API y presentación de fachadas
> * Puesta en marcha de los desarrolladores rápidamente
> * Protección de acceso
> * Análisis y métricas
> * Obtención de control e información con una plataforma de administración de API
> * Uso de soluciones de nube frente a locales
> * Administración de API de Azure
> 
> 

## <a name="apis"></a>API y operaciones
Las API son foundation Hola de una instancia de servicio de administración de API. Cada API representa un conjunto de operaciones disponibles toodevelopers. Cada API contiene un servicio back-end de toohello de referencia que implementa la API de Hola y sus operaciones asignan operaciones toohello implementadas por el servicio de back-end de Hola. Las operaciones de Administración de API son altamente configurables, con control sobre asignación de direcciones URL, parámetros de consulta y ruta de acceso, contenidos de solicitudes y respuestas y almacenamiento en caché de respuestas de operaciones. El límite de velocidad, cuotas y las directivas de restricción de IP también se pueden implementar en el nivel de operación individual u Hola API.

Para obtener más información, consulte [cómo toocreate API] [ How toocreate APIs] y [cómo tooadd operaciones tooan API][How tooadd operations tooan API].

## <a name="products"></a> Productos
Los productos son cómo API son toodevelopers apareció. Los productos en Administración de API tienen una o varias API y se configuran con un título, una descripción y términos de uso. Los productos pueden ser de tipo **Abierto** o **Protegido**. Productos protegidos deben estar suscrito toobefore pueden usarse, mientras está abierto productos pueden utilizarse sin una suscripción. Cuando un producto está preparado para que lo usen los desarrolladores, se puede publicar. Una vez publicado, puede verse (y en hello suscrito caso de productos protegidos) por los desarrolladores. Aprobación de la suscripción se configura en el nivel de producto de Hola y puede requerir aprobación del administrador o ser aprobada automáticamente.

Los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos. Productos conceder toogroups de visibilidad, y los desarrolladores pueden ver y suscribirse toohello productos que son grupos de toohello visible en la que pertenecen. 

Para obtener más información, consulte [cómo toocreate y publicar un producto] [ How toocreate and publish a product] y Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"></a> Grupos
Los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos. Administración de API tiene Hola los grupos de sistema inmutables siguientes.

* **Administradores** : los administradores de la suscripción de Azure son miembros de este grupo. Los administradores administran las instancias de servicio de administración de API, crear Hola API, operaciones y productos que se usan los programadores.
* **Desarrolladores** : los usuarios del portal para desarrolladores autenticados se incluyen en este grupo. Los desarrolladores son clientes de Hola que compilan aplicaciones mediante las API. Los programadores se conceden portal para desarrolladores de acceso toohello y creación aplicaciones que llaman a operaciones de Hola de una API.
* **Los invitados** -sin autenticar usuarios del portal para desarrolladores, como clientes potenciales visitar el portal para desarrolladores de Hola de una caída de la instancia de administración de API en este grupo. Se pueden conceder cierto acceso de solo lectura, como la capacidad de hello tooview API, pero no llamarlos.

En grupos de sistema de toothese de suma, los administradores pueden crear grupos personalizados o [aprovechar grupos externos en inquilinos de Azure Active Directory asociados](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Grupos personalizados y externos pueden usarse junto con grupos del sistema para conceder a los desarrolladores visibilidad y tener acceso a los productos tooAPI. Por ejemplo, podría crear un grupo personalizado para desarrolladores afiliados a una determinada organización de socios y permitan tener acceso toohello las API de un producto que contiene solo las API relevantes. Un usuario puede ser miembro de más de un grupo.

Para obtener más información, consulte [cómo toocreate y usar grupos][How toocreate and use groups].

## <a name="developers"></a> Desarrolladores
Los desarrolladores representan las cuentas de usuario de hello en una instancia de servicio de administración de API. Los desarrolladores pueden crearse o invitación toojoin por los administradores, o puede registrarse de hello [portal para desarrolladores de][Developer portal]. Cada desarrollador es un miembro de uno o varios grupos y puede ser suscribirse toohello productos que conceda a grupos de toothose de visibilidad.

Cuando los desarrolladores suscriben tooa producto se les conceden clave principal y secundaria de hello para el producto de Hola. Esta clave se usa cuando se realizan llamadas a las API del producto de Hola.

Para obtener más información, consulte [cómo toocreate o invitar a los desarrolladores] [ How toocreate or invite developers] y [cómo tooassociate los grupos con los desarrolladores][How tooassociate groups with developers].

## <a name="policies"></a> Directivas
Las directivas son una capacidad eficaz de administración de API que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración. Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API. Las instrucciones más usadas incluyen la conversión de formato de velocidad de tooJSON y llame al método XML y limitar toorestrict Hola cantidad de llamadas entrantes de un desarrollador y muchas otras directivas están disponibles.

Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario. Algunas directivas como hello [flujo de Control](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) y [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) directivas basadas en expresiones de directiva. Para obtener más información, consulte [directivas avanzadas](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx), y Hola inspección después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Para obtener una lista completa de las directivas de API Management, consulte [Referencia de la directiva][Policy reference]. Para más información acerca del uso y la configuración de directivas, consulte [Directivas de API Management][API Management policies]. Para ver un tutorial sobre la creación de un producto con directivas de cuota y límite de tasas, consulte [Creación y definición de configuraciones de productos avanzadas][How create and configure advanced product settings]. Para obtener una demostración, vea Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"></a> Portal para desarrolladores
portal para desarrolladores de Hello es donde los desarrolladores pueden obtener información acerca de las operaciones de API, la vista y la llamada y suscribirse tooproducts. Clientes potenciales pueden visitar el portal para desarrolladores de hello, ver las API y operaciones e inscribirse. dirección URL de Hola para su portal para desarrolladores se encuentra en el panel Hola Hola Portal clásico de Azure para la instancia de servicio de administración de API.

Puede personalizar Hola apariencia y funcionamiento de su portal para desarrolladores agregando contenido personalizado, personalizar los estilos y agregar la personalización de marca.

## <a name="api-management-and-hello-api-economy"></a>Economía de API de administración de API y Hola
toolearn más información acerca de la administración de API, Hola inspección después de presentación de la conferencia de hello Microsoft Ignite 2015.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




