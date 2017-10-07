---
title: "portal de desarrollador de administración de API aaaCustomize hello mediante plantillas-Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize Hola portal para desarrolladores de administración de API de Azure mediante plantillas."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>¿Cómo toocustomize Hola portal para desarrolladores de administración de API de Azure mediante plantillas

Hay tres portal para desarrolladores de aspectos fundamentales toocustomize hello en administración de API de Azure:

* [Editar contenido de Hola de páginas estáticas y elementos de diseño de página][modify-content-layout]
* [Actualizar estilos de hello utilizados para los elementos de la página a través del portal para desarrolladores de Hola][customize-styles]
* [Modificar plantillas de hello utilizadas para las páginas generadas por el portal de hello] [ portal-templates] (que se explica en esta guía)

Las plantillas son utilizados toocustomize Hola contenido de páginas del portal para desarrolladores generados por el sistema (por ejemplo, documentos de API, productos, autenticación de usuario, etcetera). Usar [DotLiquid](http://dotliquidmarkup.org/) sintaxis y un conjunto proporcionado de recursos de cadena traducida, iconos y controles de la página tienen contenido de gran flexibilidad tooconfigure Hola de páginas de hello como considere oportuno.

## <a name="developer-portal-templates-overview"></a>Información general sobre las plantillas del portal para desarrolladores
Edición de plantillas se realiza de hello **portal para desarrolladores de** al que se va a iniciado sesión como administrador. tooget no existe en primer lugar abra Hola Portal de Azure y haga clic en **portal para desarrolladores de** de barra de herramientas de servicio de saludo de la instancia de la administración de API.

![Portal del publicador][api-management-management-console]

A continuación, haga clic en **portal para desarrolladores de** en hello superior derecha. 

![Menú del portal para desarrolladores][api-management-developer-portal-menu]

tooaccess Hola plantillas del portal para desarrolladores, haga clic en hello personalizar el icono de menú de personalización de hello toodisplay izquierdo hello y haga clic en **plantillas**.

![Plantillas del portal para desarrolladores][api-management-customize-menu]

lista de plantillas de Hello muestra varias categorías de plantillas que tratan sobre las distintas páginas de hello en el portal para desarrolladores de Hola. Cada plantilla es diferente, pero Hola pasos tooedit ellos y publicar los cambios de Hola se Hola igual. tooedit una plantilla, haga clic en nombre de Hola de plantilla de Hola.

![Plantillas del portal para desarrolladores][api-management-templates-menu]

Al hacer clic en una plantilla, se le toohello developer página del portal que se puede personalizar por esa plantilla. En este Hola ejemplo **lista de productos** se muestra la plantilla. Hola **lista de productos** área de pantalla de bienvenida indicado por el rectángulo rojo Hola Hola a controles de la plantilla. 

![Plantilla de lista de productos][api-management-developer-portal-templates-overview]

Algunas plantillas, como hello **perfil de usuario** plantillas, personalizar diferentes partes de hello sintonía. 

![Plantillas de perfil de usuario][api-management-user-profile-templates]

editor de Hola para cada plantilla del portal para desarrolladores tiene dos secciones muestra final Hola de página Hola. lado izquierdo de Hello muestra hello editar panel para la plantilla de Hola y derecha hello muestra el modelo de datos de hello para la plantilla de Hola. 

panel de edición de la plantilla de Hello contiene marcado Hola que controla la apariencia de Hola y el comportamiento de la página correspondiente de hello en el portal para desarrolladores de Hola. marcado de Hello en plantilla hello usa hello [DotLiquid](http://dotliquidmarkup.org/) sintaxis. Un editor popular de DotLiquid es [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Cualquier plantilla de toohello los cambios realizados durante la edición se muestra en tiempo real en el Explorador de hello, pero son los clientes de tooyour no es visible hasta que [guardar](#to-save-a-template) y [publicar](#to-publish-a-template) plantilla Hola.

![Marcado de plantilla][api-management-template]

Hola **datos de la plantilla** panel proporciona una guía toohello datos modelo para entidades de Hola que están disponibles para su uso en una plantilla determinada. Esta guía proporciona mostrando los datos en directo de Hola que actualmente se muestran en el portal para desarrolladores de Hola. Se pueden expandir paneles de plantilla de hello haciendo clic en el rectángulo de hello en la esquina superior derecha de Hola de hello **datos de la plantilla** panel.

![Modelo de datos de plantilla][api-management-template-data]

En el ejemplo anterior de hello hay dos productos que se muestran en el portal para desarrolladores de Hola y que se recuperaron de datos de hello mostrados en hello **datos de la plantilla** panel, como se muestra en el siguiente ejemplo de Hola.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

marcado de Hola Hola **lista de productos** procesos de plantilla Hola salida de datos tooprovide Hola deseado recorriendo en iteración la colección de Hola de información de toodisplay de productos y un vínculo tooeach cada producto individual. Hola Nota `<search-control>` y `<page-control>` elementos de marcado de Hola. Estos controlan la presentación de Hola de hello, búsqueda y controles de página de Hola de paginación. `ProductsStrings|PageTitleProducts`es una referencia de cadena localizada que contiene Hola `h2` texto del encabezado de página de Hola. Para obtener una lista de recursos de cadena, controles de página e iconos disponibles para su uso en plantillas del portal para desarrolladores, consulte la [referencia de plantillas del portal para desarrolladores de API Management](api-management-developer-portal-templates-reference.md).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave una plantilla
toosave una plantilla, haga clic en Guardar en el editor de plantillas de Hola.

![Guardar plantilla][api-management-save-template]

Los cambios se guardaron no están activos en el portal para desarrolladores de hello hasta que se publican.

## <a name="toopublish-a-template"></a>toopublish una plantilla
Las plantillas guardadas se pueden publicar individualmente o todas juntas. toopublish una plantilla individual, haga clic en publicar en el editor de plantillas de Hola.

![Publicar plantilla][api-management-publish-template]

Haga clic en **Sí** tooconfirm y asegúrese de plantilla de hello en vivo en el portal para desarrolladores de Hola.

![Confirmar publicación][api-management-publish-template-confirm]

toopublish actualmente todas las versiones de plantillas se anuló la publicación, haga clic en **publicar** en la lista de plantillas de Hola. Plantillas no publicadas se designan mediante un asterisco después de nombre de la plantilla de Hola. En este ejemplo, Hola **lista de productos** y **producto** plantillas se publican.

![Publicar plantillas][api-management-publish-templates]

Haga clic en **publicar personalizaciones** tooconfirm.

![Confirmar publicación][api-management-publish-customizations]

Las plantillas publicadas recientemente son efectivos inmediatamente en el portal para desarrolladores de Hola.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert una versión anterior de toohello de plantilla
toorevert una versión publicada de plantilla toohello anterior, haga clic en revertir en el editor de plantillas de Hola.

![Revertir plantilla][api-management-revert-template]

Haga clic en **Sí** tooconfirm.

![Confirm][api-management-revert-template-confirm]

Hola previamente versión publicada de una plantilla es viven en el portal para desarrolladores de Hola una vez que la operación de reversión de hello está completa.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore una versión de plantilla toohello predeterminada
Versión de restauración plantillas tootheir predeterminada es un proceso de dos pasos. Deben restaurarse la primera plantillas de hello y, a continuación, se deben publicar versiones Hola restaurado.

toorestore una versión de plantilla único toohello predeterminada haga clic en restaurar en el editor de plantillas de Hola.

![Revertir plantilla][api-management-reset-template]

Haga clic en **Sí** tooconfirm.

![Confirm][api-management-reset-template-confirm]

toorestore versiones predeterminadas de todas las plantillas tootheir, haga clic en ejecutar **Restaurar plantillas predeterminadas** en la lista de plantillas de Hola.

![Restaurar plantillas][api-management-restore-templates]

Hello plantillas restauradas, a continuación, se deben publicar individualmente o a la vez siguiendo los pasos de hello en [toopublish una plantilla de](#to-publish-a-template).

## <a name="next-steps"></a>Pasos siguientes
Para obtener información de referencia sobre plantillas del portal para desarrolladores, recursos de cadena, iconos y controles de página, consulte la [referencia de plantillas del portal para desarrolladores de Administración de API](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







