---
title: "aaaProtect su API con administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprotect su API con las cuotas y la limitación de las directivas (limitación de velocidad)."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Protección de su API con límites de frecuencia mediante Azure API Management
Esta guía muestra lo fácil que es tooadd protección para el API de back-end mediante la configuración de directivas de límite y la cuota de la tasa con la administración de API de Azure.

En este tutorial, aprenderá a crear un producto de "Prueba gratuita" API que permite a los desarrolladores toomake too10 llamadas por minuto e instalación tooa máximo de 200 llamadas por semana tooyour API con hello [limitar la tasa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [ Establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) directivas. Podrá publicar API hello y probar la directiva de límite de velocidad de Hola.

Más avanzados limitación escenarios con hello [límite de velocidad por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [cuota por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) directivas, vea [solicitud avanzada limitación con administración de API de Azure](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate un producto
En este paso, creará un producto de evaluación gratuita que no requiere aprobación de suscripción.

> [!NOTE]
> Si ya tiene un producto configurado y desea toouse, para este tutorial, puede saltar a continuación demasiado[configurar directivas de límite y la cuota de tasa de llamadas] [ Configure call rate limit and quota policies] y siga el tutorial de Hola desde ahí con el producto en lugar de producto de evaluación gratuita de Hola.
> 
> 

tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [administrar su primera API de administración de API de Azure] [ Manage your first API in Azure API Management] tutorial.
> 
> 

Haga clic en **productos** en hello **administración de API** menú Hola toodisplay izquierdo Hola **productos** página.

![Add product][api-management-add-product]

Haga clic en **agregar producto** toodisplay hello **Agregar nuevo producto** cuadro de diálogo.

![Agregar nuevo producto][api-management-new-product-window]

Hola **título** , escriba **gratuita**.

Hola **descripción** cuadro, Hola de tipo siguiente texto: **suscriptores van a ser capaz de toorun 10 llamadas por minuto seguridad tooa máximo de 200 llamadas/semana después del cual se deniega el acceso.**

Los productos de API Management pueden estar abiertos o protegidos. Productos protegidos deben ser toobefore suscrito se pueden usar. mientras que los productos abiertos pueden usarse sin suscripción. Asegúrese de que **requieren suscripción** es toocreate seleccionado un producto protegido que requiere una suscripción. Se trata de una configuración predeterminada de Hola.

Si desea que un administrador tooreview y Aceptar o rechazar suscripción intenta toothis producto, seleccione **requieren la aprobación de suscripción**. Si no se selecciona la casilla de verificación de hello, intentos de suscripción será aprobada automáticamente. En este ejemplo, las suscripciones se aprueban automáticamente, por lo que no se active la casilla de Hola.

cuentas de desarrollador tooallow toosubscribe toohello nuevo producto de varias veces, seleccione hello **permitir múltiples suscripciones simultáneas** casilla de verificación. En este tutorial no se usan varias suscripciones simultáneas; por tanto, no active la casilla.

Después de introducen todos los valores, haga clic en **guardar** producto de hello toocreate.

![Product added][api-management-product-added]

De forma predeterminada, los nuevos productos están toousers visible en hello **administradores** grupo. Vamos hello tooadd **a los desarrolladores** grupo. Haga clic en **gratuita**y, a continuación, haga clic en hello **visibilidad** ficha.

> Administración de API, los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos. Productos conceder toogroups de visibilidad, y los desarrolladores pueden ver y suscribirse toohello productos que son grupos de toohello visible en la que pertenecen. Para obtener más información, consulte [cómo toocreate y use los grupos de administración de API de Azure][How toocreate and use groups in Azure API Management].
> 
> 

![Add developers group][api-management-add-developers-group]

Seleccione hello **a los desarrolladores** casilla de verificación y, a continuación, haga clic en **guardar**.

## <a name="add-api"></a>tooadd una API toohello producto
En este paso del tutorial de hello, agregaremos Hola eco API toohello nuevo gratuita producto.

> Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración. Para más información, consulte [Administración de su primera API en Azure API Management][Manage your first API in Azure API Management].
> 
> 

Haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **gratuita** producto de hello tooconfigure.

![Configure product][api-management-configure-product]

Haga clic en **tooproduct agregar API**.

![Agregar API tooproduct][api-management-add-api]

Seleccione **Echo API** (API Eco ) y luego haga clic en **Guardar**.

![Add Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure las directivas de límite y la cuota de tasa de llamadas
Límites de velocidad y las cuotas se configuran en el editor de directiva de Hola. las directivas de Hello dos que se va a agregar en este tutorial son hello [limitar la tasa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) directivas. Estas directivas deben aplicarse en el ámbito del producto de Hola.

Haga clic en **directivas** en hello **administración de API** menú de hello izquierda. Hola **producto** lista, haga clic en **gratuita**.

![Product policy][api-management-product-policy]

Haga clic en **Agregar directiva** tooimport Hola plantilla de directiva y empezar a crear directivas de cuota y el límite de velocidad de Hola.

![Add policy][api-management-add-policy]

Tasa límite y la cuota directivas son entrante, por lo que posición Hola cursor en el elemento de entrada de Hola.

![Policy editor][api-management-policy-editor-inbound]

Desplácese por la lista de directivas de Hola y busque hello **limitar la tasa de llamadas por suscripción** entrada de directiva.

![Policy statements][api-management-limit-policies]

Después de hello cursor se coloca en hello **entrada** elemento de directiva, haga clic en la flecha de hello junto a **limitar la tasa de llamadas por suscripción** tooinsert su plantilla de directiva.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Como puede ver en el fragmento de código de hello, directiva de hello permite establecer límites para el producto Hola API y operaciones. En este tutorial se utilizará no esa capacidad, por lo que elimina hello **api** y **operación** elementos de hello **límite de velocidad** elemento, de forma que solo Hola externa**límite de velocidad** elemento permanece, tal y como se muestra en el siguiente ejemplo de Hola.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

En el producto de evaluación gratuita de hello, velocidad máxima permitida de llamadas de hello es 10 llamadas por minuto, así que escriba **10** como valor de Hola de hello **llamadas** atributo, y **60** para hello **período de renovación** atributo.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

Hola tooconfigure **establecer la cuota de uso por suscripción** directiva, posición el cursor se encuentra justo debajo Hola recién agregado **límite de velocidad** elemento dentro de hello **entrada** elemento y, a continuación, busque y haga clic en hello flecha toohello a la izquierda de **establecer la cuota de uso por suscripción**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Del mismo modo toohello **establecer la cuota de uso por suscripción** directiva, **establecer la cuota de uso por suscripción** directiva permite configurar extremos para en las operaciones y las API del producto de Hola. En este tutorial se utilizará no esa capacidad, por lo que elimina hello **api** y **operación** elementos de hello **cuota** elemento, como se muestra en el siguiente ejemplo de Hola.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Las cuotas pueden basarse en número de Hola de llamadas por intervalo, el ancho de banda o ambos. En este tutorial, no nos estamos limitación en función de ancho de banda, por lo que elimine hello **ancho de banda** atributo.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

En el producto de evaluación gratuita de hello, cuota de hello es 200 llamadas por semana. Especifique **200** como valor de Hola de hello **llamadas** de atributo y, a continuación, especifique **604800** como valor de Hola de hello **período de renovación** atributo.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Los intervalos de directiva se especifican en segundos. intervalo de saludo toocalculate durante una semana, puede multiplicar número Hola de días (7) mediante el número de horas en un día (24) por número de Hola de minutos durante una hora (60) mediante el número de segundos en un minuto (60) Hola Hola: 7 * 24 * 60 * 60 = 604800.
> 
> 

Cuando haya terminado de configurar la directiva de hello, debe coincidir con el siguiente ejemplo de Hola.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Después de hello deseado se configuran las directivas, haga clic en **guardar**.

![Save policy][api-management-policy-save]

## <a name="publish-product"></a> producto de hello toopublish
Ahora que hello hello las API se agregan y se configuran las directivas de hello, producto Hola debe publicarse para que los desarrolladores pueden usar. Haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **gratuita** producto de hello tooconfigure.

![Configure product][api-management-configure-product]

Haga clic en **publicar**y, a continuación, haga clic en **Sí, publicarlo** tooconfirm.

![Publish product][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe un producto de toohello de cuenta de desarrollador
Ahora se publica ese producto hello, es tooand toobe disponibles suscrito la usan los programadores.

> Los administradores de una instancia de la administración de API son producto tooevery automáticamente suscrito. En este paso del tutorial, se suscribirá uno de producto de evaluación gratuita de hello desarrollador sin privilegios de administrador cuentas toohello. Si la cuenta de desarrollador forma parte del rol de administradores de hello, después, puede seguir este paso, incluso si ya está suscrito.
> 
> 

Haga clic en **usuarios** en hello **administración de API** menú Hola izquierda y, a continuación, haga clic en nombre de saludo de la cuenta de desarrollador. En este ejemplo, estamos utilizando hello **Clayton Gragg** cuenta de desarrollador.

![Configure developer][api-management-configure-developer]

Haga clic en **Agregar suscripción**.

![Agregar suscripción][api-management-add-subscription-menu]

Seleccione **Evaluación gratuita** y, después, haga clic en **Suscribirse**.

![Agregar suscripción][api-management-add-subscription]

> [!NOTE]
> En este tutorial, varias suscripciones simultáneas no están habilitadas para el producto de evaluación gratuita de Hola. Si se hubieran, sería tooname solicitadas Hola suscripción, como se muestra en el siguiente ejemplo de Hola.
> 
> 

![Agregar suscripción][api-management-add-subscription-multiple]

Después de hacer clic **suscribir**, producto Hola aparece en hello **suscripción** lista para el usuario de Hola.

![Subscription added][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall un límite de velocidad de Hola de operación y prueba
Ahora que hello producto de evaluación gratuita se configura y se publica, podemos llamar a algunas operaciones y probar la directiva de límite de velocidad de Hola.
Portal para desarrolladores de conmutador toohello haciendo clic en **portal para desarrolladores de** en el menú de hello superior derecha.

![portal para desarrolladores][api-management-developer-portal-menu]

Haga clic en **API** en Hola menú superior y, a continuación, haga clic en **API de eco**.

![portal para desarrolladores][api-management-developer-portal-api-menu]

Haga clic en **GET Resource** (Recurso GET) y, después, en **Pruébelo**.

![Open console][api-management-open-console]

Mantener valores de parámetro de predeterminado de hello y, a continuación, seleccione la clave de suscripción para el producto de evaluación gratuita de Hola.

![Subscription key][api-management-select-key]

> [!NOTE]
> Si tiene varias suscripciones, ser seguro de clave de Hola de tooselect para **gratuita**, o más directivas de Hola que se configuraron en pasos anteriores hello no estará en vigor.
> 
> 

Haga clic en **enviar**y, a continuación, ver la respuesta de Hola. Hola Nota **estado de respuesta** de **200 Aceptar**.

![Operation results][api-management-http-get-results]

Haga clic en **enviar** a una velocidad mayor que la directiva de límite de velocidad de Hola de 10 llamadas por minuto. Después de que se supera la directiva de límite de velocidad de hello, el estado de respuesta **429 demasiado muchas solicitudes** se devuelve.

![Operation results][api-management-http-get-429]

Hola **contenido de la respuesta** indica Hola restantes intervalo antes de reintentos se realice correctamente.

Cuando la directiva de límite de velocidad de Hola de 10 llamadas por minuto está habilitada, las llamadas subsiguientes se producirá un error hasta que hayan transcurrido 60 segundos de hello primer de producto de toohello de hello 10 llamadas correctas antes de que se ha superado el límite de velocidad de Hola. En este ejemplo, hello restantes intervalo es 54 segundos.

## <a name="next-steps"></a>Pasos siguientes
* Vea una demostración de establecer límites de velocidad y las cuotas en hello después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
