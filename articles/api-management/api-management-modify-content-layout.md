---
title: "contenido de la página de aaaModify en el portal para desarrolladores de hello en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooedit página contenido en el portal para desarrolladores de hello en la administración de API de Azure."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Modificar el contenido de Hola y el diseño de páginas en el portal para desarrolladores de hello en la administración de API de Azure
Hay tres portal para desarrolladores de aspectos fundamentales toocustomize hello en administración de API de Azure:

* [Editar contenido de Hola de páginas estáticas y elementos de diseño de página] [ modify-content-layout] (que se explica en esta guía)
* [Actualizar estilos de hello utilizados para los elementos de la página a través del portal para desarrolladores de Hola][customize-styles]
* [Modificar plantillas de hello utilizadas para las páginas generadas por el portal de hello] [ portal-templates] (por ejemplo, documentos de API, productos, autenticación de usuario, etcetera)

## <a name="page-structure"></a>Estructura de las páginas del portal para desarrolladores

portal para desarrolladores de Hola se basa en un sistema de administración de contenido. diseño Hola de cada página se compila en función de conjunto de elementos de la página pequeño denominados widgets:

![Estructura de las páginas del portal para desarrolladores][api-management-customization-widget-structure]

Todos los widgets son editables. 
* página individuales de Hello core contenido específico tooeach residen en el widget "Contenido" Hola. Edita una página significa modificar Hola contenido de este widget.
* Todos los elementos de diseño de página se encuentran con widgets restantes Hola. Los cambios realizados widgets toothese aplicará tooall páginas. Estarán tooas que se hace referencia "widgets de diseño".

En la página diaria edición uno normalmente solo modifica widget de contenido de Hola que tendrá contenido diferente para cada página.

## <a name="modify-layout-widget"></a>Modificar el contenido de Hola de un widget de diseño

Se modifica el contenido en el portal para desarrolladores de Hola a través del portal para desarrolladores de Hola que sea accesible desde Hola Portal de Azure. tooreach, haga clic en **portal para desarrolladores de** de barra de herramientas de servicio de saludo de la instancia de la administración de API.

![Portal del publicador][api-management-management-console]

contenido de hello tooedit de ese widget, haga clic en **Widgets** de hello **Portal para desarrolladores de** menú izquierda Hola. Para este ejemplo permite modificar contenido de Hola de widget de encabezado de Hola. Seleccione hello **encabezado** widget de lista Hola.

![Widgets header][api-management-widgets-header]

contenido de Hello del encabezado de hello es editable desde dentro de hello **cuerpo** campo. Cambiar el texto hello como desee y, a continuación, haga clic en **guardar** final Hola de página Hola.

Ahora debe ser el nuevo encabezado de Hola de pueda toosee en todas las páginas en el portal para desarrolladores de Hola.

> portal para desarrolladores de tooopen hello en el portal para desarrolladores de hello, haga clic en **portal para desarrolladores de** en la barra superior Hola.
> 
> 

## <a name="edit-page-contents"></a>Editar contenido de Hola de una página

lista de hello toosee de todas las páginas de contenido existentes, haga clic en **contenido** de hello **portal para desarrolladores de** menú en el portal para desarrolladores de Hola.

![Manage content][api-management-customization-manage-content]

Haga clic en hello **bienvenida** página tooedit lo que se muestra en la portada de Hola de portal para desarrolladores de Hola. Realizar cambios de Hola que desea obtener una vista previa en caso necesario y, a continuación, haga clic en **publicar ahora** toomake les tooeveryone visible.

> página principal de Hello usa un diseño especial que le permite toodisplay una pancarta en la parte superior de Hola. Este encabezado no es editable de hello **contenido** sección. tooedit este banner, haga clic en **Widgets** de hello **portal para desarrolladores de** menú, seleccione **página principal** de hello **capa actual** desplegable lista y, a continuación, abra hello **pancarta** elemento bajo hello **destacadas sección**. contenido de Hola de este widget es editable igual que cualquier otra página.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Actualizar estilos de hello utilizados para los elementos de la página a través del portal para desarrolladores de Hola][customize-styles]
* [Modificar plantillas de hello utilizadas para las páginas generadas por el portal de hello] [ portal-templates] (por ejemplo, documentos de API, productos, autenticación de usuario, etcetera)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
