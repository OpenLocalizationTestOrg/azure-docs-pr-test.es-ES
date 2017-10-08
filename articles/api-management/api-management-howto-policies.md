---
title: "aaaPolicies en administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo editar toocreate y configurar las directivas de administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Directivas de Administración de API de Azure
En la administración de API de Azure, las directivas son una capacidad eficaz del sistema de Hola que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración. Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API. Las instrucciones más usadas incluyen la conversión de formato de XML tooJSON y llamar a la cantidad de hello toorestrict de llamadas entrantes de un desarrollador de limitación de velocidad. Existen muchas más directivas desde el principio de Hola.

Vea hello [referencia de directiva] [ Policy Reference] para obtener una lista completa de las instrucciones de directiva y su configuración.

Las directivas se aplican dentro de la puerta de enlace de Hola que se encuentra entre consumidor de la API de Hola y Hola managed API. recibe todas las solicitudes Hello puerta de enlace y normalmente reenvía sin modificaciones toohello subyacente API. Sin embargo puede aplicar una directiva de solicitud entrante de cambios tooboth hello y respuesta saliente.

Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario. Algunas directivas como hello [flujo de Control] [ Control flow] y [Set variable] [ Set variable] directivas basadas en expresiones de directiva. Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].

## <a name="scopes"></a>Cómo tooconfigure directivas
Las directivas se pueden configurar globalmente o en el ámbito de Hola de un [producto][Product], [API] [ API] o [operación] [Operation]. tooconfigure una directiva, navegue toohello editor de directivas en el portal para desarrolladores de Hola.

![Policies menu][policies-menu]

el editor de directivas de Hello consta de tres secciones principales: Hola ámbito (superior), Hola directiva definición de directiva donde las directivas se editan (izquierda) y las instrucciones de hello lista (derecha):

![Policies editor][policies-editor]

toobegin configurar una directiva que primero debe seleccionar ámbito de hello en qué Hola debe aplicarse la directiva. En la captura de pantalla de hello siguiente hello **Starter** producto se selecciona. Tenga en cuenta que este nombre de directiva Hola símbolo cuadrado siguiente toohello indica que ya se aplica una directiva en este nivel.

![Scope][policies-scope]

Puesto que ya se ha aplicado una directiva, configuración de Hola se muestra en la vista de definición de Hola.

![Configuración][policies-configure]

Hola directiva se muestra como de solo lectura en un primer momento. En orden tooedit definición hello, haga clic en hello **Configurar directiva** acción.

![Edit][policies-edit]

definición de la directiva de Hello es un documento XML sencillo que describe una secuencia de instrucciones entrantes y salientes. Hola XML puede modificarse directamente en la ventana de definición de hello. Una lista de instrucciones es siempre toohello derecha y el ámbito actual de instrucciones toohello aplicables están habilitados y resaltados; como se muestra en hello **límite de velocidad de llamar a** instrucción de captura de pantalla de hello anterior.

Al hacer clic en una instrucción habilitada agregará Hola código XML adecuado en la ubicación de Hola de cursor de hello en la vista de definición de Hola. 

> [!NOTE]
> Si no está habilitada la directiva de Hola que desea tooadd, asegúrese de que está en el ámbito correcto de saludo de la directiva. Cada instrucción de la directiva está diseñada para su uso en determinados ámbitos y secciones de la directiva. secciones de la directiva de tooreview hello y ámbitos para una directiva, compruebe hello **uso** sección de la directiva en hello [referencia de directiva][Policy Reference].
> 
> 

Una lista completa de las instrucciones de directiva y sus valores están disponibles en hello [referencia de directiva][Policy Reference].

Por ejemplo, tooadd un nuevo toorestrict de instrucción entrante solicita toospecified las direcciones IP, coloque Hola cursor solo en el contenido de Hola de hello `inbound` Hola de elemento y haga clic en XML **llamador restringir IP** instrucción.

![Restriction policies][policies-restrict]

Esto agregará una toohello de fragmento de código XML `inbound` elemento que se proporciona instrucciones sobre cómo tooconfigure Hola instrucción.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit las solicitudes de entrada y Aceptar sólo aquellos desde una dirección IP de 1.2.3.4 modificar Hola XML como se indica a continuación:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Save][policies-save]

Cuando se complete configuración instrucciones Hola de directiva de hello, haga clic en **guardar** y cambios de hello será puerta de enlace de administración de API toohello propagado inmediatamente.

## <a name="sections"></a>Descripción de la configuración de directivas
Una directiva es una serie de declaraciones que se ejecutan en orden para una solicitud y una respuesta. configuración de Hola se divide adecuadamente en `inbound`, `backend`, `outbound`, y `on-error` secciones tal y como se muestra en la siguiente configuración de Hola.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Si se produce un error durante el procesamiento de Hola de una solicitud, los pasos restantes hello `inbound`, `backend`, o `outbound` secciones se omiten y ejecución saltará instrucciones toohello Hola `on-error` sección. Mediante la colocación de las instrucciones de directiva en hello `on-error` sección podrá revisar error hello mediante hello `context.LastError` propiedad, inspeccionar y personalizar la respuesta de error de hello mediante hello `set-body` directiva y configurar lo que ocurre si se produce un error. Hay códigos de error para conocer los pasos integrados y los errores que pueden producirse durante el procesamiento de Hola de las instrucciones de directiva. Para más información, consulte [Control de errores en las directivas de administración de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Puesto que las directivas se pueden especificar en diferentes niveles (global, producto, api y operación) configuración Hola proporciona una manera para usted toospecify orden de hello en la que se ejecutan las instrucciones de definición de la directiva de hello con la directiva de respeto toohello primario. 

Ámbitos de la directiva se evalúan en hello siguiendo el orden.

1. Ámbito global
2. Ámbito del producto
3. Ámbito de la API
4. Ámbito de la operación

Hello dentro de ellos se evalúen las instrucciones según la selección de ubicación de toohello de hello `base` elemento, si está presente. Directiva global tiene ninguna directiva de elemento primario y el uso de hello `<base>` elemento en el no tiene ningún efecto.

Por ejemplo, si tiene una directiva en el nivel global de hello y una directiva configurada para una API, a continuación, cada vez que se utiliza esa API determinada las dos directivas se aplicará. Administración de API permite orden determinista de las instrucciones de directiva combinada a través del elemento base Hola. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

En hello ejemplo definición de directiva anterior, Hola `cross-domain` ejecutaría instrucción antes de que las directivas de mayor que tomaría a su vez, ir seguido de hello `find-and-replace` directiva. 

directivas de hello toosee en el ámbito actual de hello en el editor de directiva de hello, haga clic en **recalcular directiva en vigor para el ámbito seleccionado**.

## <a name="next-steps"></a>Pasos siguientes
Visualice el siguiente vídeo acerca de expresiones de directivas.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
