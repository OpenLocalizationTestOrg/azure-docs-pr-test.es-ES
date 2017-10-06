---
title: "propiedades de toouse aaaHow en las directivas de administración de API de Azure"
description: "Obtenga información acerca de cómo toouse propiedades en las directivas de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>¿Cómo toouse propiedades en las directivas de administración de API de Azure
Las directivas de administración de API son una capacidad eficaz del sistema de Hola que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración. Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API. Las instrucciones de las directivas se pueden crear con valores de texto literal, expresiones de directiva y propiedades. 

Cada instancia de servicio de administración de API tiene una colección de propiedades de pares clave/valor que las instancias de servicio de toohello global. Estas propiedades pueden ser valores de cadena constante toomanage usados a través de todas las directivas y configuración de la API. Cada propiedad tiene los siguientes atributos de Hola.

| Atributo | Tipo | Description |
| --- | --- | --- |
| Nombre |cadena |nombre de Hola de propiedad de Hola. Puede contener solo letras, dígitos, puntos, guiones o caracteres de subrayado. |
| Valor |cadena |valor de Hola de propiedad de Hola. No puede estar vacío ni contener solo espacios en blanco. |
| Secret |boolean |Determina si el valor de hello es un secreto y debe cifrarse o no. |
| Etiquetas |matriz de cadena |Opcional de etiquetas que cuando se proporciona puede ser la lista de propiedades de hello toofilter usado. |

Propiedades se configuran en el portal para desarrolladores de hello en hello **propiedades** ficha. En el siguiente ejemplo de Hola, se configuran tres propiedades.

![Propiedades][api-management-properties]

Los valores de propiedad pueden contener cadenas literales y [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx). Hello tabla siguiente muestran Hola anterior ejemplo tres propiedades y sus atributos. Hola valo `ExpressionProperty` es una expresión de directiva que devuelve una cadena que contiene Hola fecha y hora actuales. Hola propiedad `ContosoHeaderValue` está marcada como un secreto, por lo que no se muestra su valor.

| Nombre | Valor | Secret | Etiquetas |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse una propiedad
nombre de la propiedad de contexto Hola dentro de un par de llaves doble, toouse una propiedad en una directiva, como `{{ContosoHeader}}`, tal y como se muestra en el siguiente ejemplo de Hola.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

En este ejemplo, `ContosoHeader` se usa como nombre de Hola de un encabezado en un `set-header` directiva, y `ContosoHeaderValue` se utiliza como valor de Hola de ese encabezado. Cuando esta directiva se evalúa durante una solicitud o respuesta toohello administración de API puerta de enlace, `{{ContosoHeader}}` y `{{ContosoHeaderValue}}` se reemplazan con sus respectivos valores de propiedad.

Propiedades que se pueden usar como atributo completa o valores de elemento, como se muestra en el ejemplo anterior de hello, pero también pueden inserta o combina con parte de una expresión de texto literal, como se muestra en el siguiente ejemplo de Hola:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Las propiedades también pueden contener expresiones de directiva. En el siguiente ejemplo de Hola Hola `ExpressionProperty` se utiliza.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Cuando esta directiva se evalúa, se reemplaza `{{ExpressionProperty}}` por su valor: `@(DateTime.Now.ToString())`. Puesto que el valor de hello es una expresión de directiva, Hola expresión se evalúa y directiva de hello continúa con su ejecución.

Puede probar este comando en el portal para desarrolladores de hello mediante una llamada a una operación que tiene una directiva con propiedades en el ámbito. En el siguiente ejemplo de Hola, se llama a una operación con hello dos anterior ejemplo `set-header` directivas con propiedades. Tenga en cuenta que la respuesta hello contiene dos encabezados personalizados que se configuraron mediante directivas con propiedades.

![portal para desarrolladores][api-management-send-results]

Si observa hello [seguimiento de API Inspector](api-management-howto-api-inspector.md) para una llamada que incluye dos directivas de ejemplo Hola anterior con propiedades, puede ver dos hello `set-header` directivas con valores de propiedad de hello insertadas, así como la expresión de directiva de Hola evaluación de la propiedad de Hola que contiene la expresión de directiva de Hola.

![Seguimiento de API Inspector][api-management-api-inspector-trace]

Tenga en cuenta que, a pesar de que los valores de propiedad pueden contener expresiones de directiva, no pueden contener otras propiedades. Si el texto que contiene una referencia de propiedad se utiliza para un valor de propiedad, como `Property value text {{MyProperty}}`, que referencia de propiedad no se reemplazan y se van a incluir como parte del valor de propiedad de Hola.

## <a name="toocreate-a-property"></a>toocreate una propiedad
toocreate una propiedad, haga clic en **Agregar propiedad** en hello **propiedades** ficha.

![Agregar propiedad][api-management-properties-add-property-menu]

Los campos **Nombre** y **Valor** son necesarios. Si este valor de propiedad es un secreto, compruebe hello **se trata de un secreto** casilla de verificación. Escriba uno o más toohelp etiquetas opcional con las propiedades de la organización y haga clic en **guardar**.

![Agregar propiedad][api-management-properties-add-property]

Cuando se guarda una nueva propiedad, Hola **propiedades de búsqueda** cuadro de texto se rellena con el nombre de Hola de hello nueva propiedad y se muestra la nueva propiedad de Hola. Borrar todas las propiedades de toodisplay hello **propiedades de búsqueda** cuadro de texto y presione ENTRAR.

![Propiedades][api-management-properties-property-saved]

Para obtener información acerca de cómo crear una propiedad mediante la API de REST de hello, consulte [crear una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>tooedit una propiedad
tooedit una propiedad, haga clic en **editar** lateral Hola propiedad tooedit.

![Editar propiedad][api-management-properties-edit]

Realice los cambios necesarios y haga clic en **Save (Guardar)**. Si cambia el nombre de la propiedad de hello, las directivas que hacen referencia a esa propiedad son nombre nuevo de hello toouse actualizan automáticamente.

![Editar propiedad][api-management-properties-edit-property]

Para obtener información acerca de cómo modificar una propiedad mediante la API de REST de hello, consulte [editar una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>toodelete una propiedad
toodelete una propiedad, haga clic en **eliminar** lateral Hola propiedad toodelete.

![Eliminar propiedad][api-management-properties-delete]

Haga clic en **Sí, eliminarlo** tooconfirm.

![Confirmar eliminación][api-management-delete-confirm]

> [!IMPORTANT]
> Si las directivas hace referencia a la propiedad de hello, no se podrá toosuccessfully eliminarlo hasta que quite la propiedad Hola de todas las directivas que lo usan.
> 
> 

Para obtener información acerca de cómo eliminar una propiedad mediante la API de REST de hello, consulte [eliminar una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>propiedades de toosearch y filtrado
Hola **propiedades** ficha incluye buscar y filtrar toohelp capacidades administrar sus propiedades. lista de propiedades de hello toofilter por nombre de propiedad, escriba un término de búsqueda en hello **propiedades de búsqueda** cuadro de texto. Borrar todas las propiedades de toodisplay hello **propiedades de búsqueda** cuadro de texto y presione ENTRAR.

![Search][api-management-properties-search]

lista de propiedades de hello toofilter por los valores de etiqueta, escriba una o más etiquetas en hello **filtrar por etiquetas** cuadro de texto. Borrar todas las propiedades de toodisplay hello **filtrar por etiquetas** cuadro de texto y presione ENTRAR.

![Filtrar][api-management-properties-filter]

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre cómo trabajar con directivas
  * [Directivas de Administración de API de Azure](api-management-howto-policies.md)
  * [Referencia de directiva](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Policy expressions (Expresiones de directiva)](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Vea un vídeo de introducción.
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

