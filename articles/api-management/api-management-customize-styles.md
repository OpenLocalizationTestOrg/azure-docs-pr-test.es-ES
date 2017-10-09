---
title: "estilos de aaaCustomize en el portal para desarrolladores de hello en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo utilizarán estilos de hello toomodify de cualquier página del portal para desarrolladores de hello en la administración de API de Azure."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Personalizar un estilo de hello del portal para desarrolladores de hello en la administración de API de Azure
Hay tres portal para desarrolladores de aspectos fundamentales toocustomize hello en administración de API de Azure:

* [Editar contenido de Hola de páginas estáticas y elementos de diseño de página][modify-content-layout]
* [Actualizar estilos de hello utilizados para los elementos de la página a través del portal para desarrolladores de hello] [ customize-styles] (que se explica en esta guía)
* [Modificar plantillas de hello utilizadas para las páginas generadas por el portal de hello] [ portal-templates] (por ejemplo, documentos de API, productos, autenticación de usuario, etcetera)

## <a name="change-headers-styling"></a>Cambiar estilo de hello de elementos de la página

Hello colores, fuentes, tamaños, espaciados y otros elementos relacionados con el estilo de cualquier página de portal de Hola se definen mediante las reglas de estilo. 

Edición de reglas de estilo de hello se realiza de hello **portal para desarrolladores de** al que se va a iniciado sesión como administrador. tooget no existe en primer lugar abra Hola Portal de Azure y haga clic en **portal para desarrolladores de** de barra de herramientas de servicio de saludo de la instancia de la administración de API.

![Portal del publicador][api-management-management-console]

A continuación, haga clic en **portal para desarrolladores de** en hello superior derecha. 

![Enlace del portal para desarrolladores en el portal para desarrolladores de Hola][api-management-pp-dp-link]

barra de herramientas de personalización de tooopen Hola mueva el mouse sobre el icono de personalización de hello (o seleccione la plantilla) y, a continuación, haga clic en "estilos" de la barra de herramientas de Hola.

![Botón de la barra de herramientas de personalización][api-management-customization-toolbar-button]

Hay dos formas principales de la edición de reglas de estilo: puede buscar en la lista de Hola de todas las reglas de estilo de hello utilizado en cualquier parte que se muestra de forma predeterminada y modificar un estilo según sea necesario, o puede elegir **seleccionar un elemento de página de hello** y, a continuación, Haga clic en cualquier lugar en hello página toosee solo Hola estilos para ese elemento.

![Customization toolbar][api-management-customization-toolbar]

Haga clic en hello **seleccionar un elemento de página de hello** opción en este ejemplo.  Ahora los elementos se convierten en resalta cuando se sitúa sobre ellos con hello mouse toosignify estilos de qué elemento se empiece a editar si hace clic en. Hola de movimiento mueva el mouse sobre texto hello en el encabezado de hello (normalmente tiene nombre de la compañía de hello aquí) y, a continuación, haga clic en él. Un conjunto de reglas de estilo con nombre y por categorías aparece en el editor de estilo de hello. Cada regla representa una propiedad de estilo del elemento seleccionado de Hola. Por ejemplo, para el texto de encabezado de hello seleccionada más arriba, tamaño de hello texto hello es en @font-size-h1 mientras Hola nombre de fuente de hello con alternativas está en @headings-font-family.

> Si está familiarizado con [arranque][bootstrap], estas reglas son en realidad [variables LESS] [ LESS variables] dentro de tema de arranque de hello usado por hello portal para desarrolladores.
> 
> 

Vamos a cambiar el color de hello del texto de título de Hola. Seleccione la entrada de Hola Hola  **@headings-color**  campo y el tipo **#000000**. Se trata de código hexadecimal de hello para el color de hello negro. Tal y como lo hace, verá que aparece un indicador de color cuadrado final Hola Hola del cuadro de texto. Si hace clic en este indicador, un selector de color permite toochoose un color.

![Color picker][api-management-customization-toolbar-color-picker]

Son una vista previa de cambios en tiempo real como hacerlos, pero son visibles tooadministrators única. toomake estos cambios se tooeveryone visible, haga clic en hello **publicar** situado en el editor de estilo de hello y confirme los cambios de Hola.

![Publish menu][api-management-customization-toolbar-publish-form]

> Hola toochange reglas de estilo que se aplican tooany otro elemento en la página de hello, seguimiento Hola mismo procedimiento como se hizo para el encabezado de Hola. Haga clic en **seleccionar un elemento de página de hello** desde el editor de estilo de hello, elemento de hello select que le interesen y modificar valores de hello de reglas de estilo de hello muestra en pantalla de bienvenida de inicio.
> 
> 


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo toocustomize contenido de Hola de portal para desarrolladores de páginas mediante [plantillas del portal para desarrolladores](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
