---
title: comportamiento de aaaOverride HTTP mediante el motor de reglas de Azure CDN Hola | Documentos de Microsoft
description: "motor de reglas de Hello permite toocustomize cómo se administran las solicitudes HTTP CDN de Azure, como el bloqueo de entrega de Hola de determinados tipos de contenido, definir una directiva de almacenamiento en caché y modificar los encabezados HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Invalidar el comportamiento HTTP mediante el motor de reglas de Azure CDN Hola
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Información general
motor de reglas de Hello permite toocustomize cómo se administran las solicitudes HTTP, por ejemplo, bloqueo de entrega de Hola de determinados tipos de contenido, definir una directiva de almacenamiento en caché y modificar los encabezados HTTP.  Este tutorial mostrará cómo crear una regla que cambiará el comportamiento de los activos de la red CDN de almacenamiento en caché de Hola.  También hay contenido de vídeo en hello "[Vea también](#see-also)" sección.

   > [!TIP] 
   > Para una sintaxis de toohello de referencia de forma detallada, vea [referencia de motor de reglas](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Tutorial
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Haga clic en hello **HTTP grandes** ficha, seguido de **motor de reglas de**.
   
    Se muestran las opciones para una nueva regla.
   
    ![Opciones de nueva regla de CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > orden de Hello en el que se muestran varias reglas afecta a cómo se controlan. Una regla subsiguientes puede invalidar las acciones de hello especificadas por una regla anterior.
   > 
   > 
3. Escriba un nombre en hello **nombre / descripción** cuadro de texto.
4. Identificar el tipo de saludo de solicitudes Hola regla se aplicará a.  De forma predeterminada, Hola **siempre** está seleccionada la condición de coincidencia.  Usará **Siempre** para este tutorial, así pues, deje esa opción seleccionada.
   
   ![Condición de coincidencia de red CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Hay muchos tipos de coincidencia de las condiciones disponibles en la lista desplegable de Hola.  Al hacer clic en hello azul icono informativo toohello izquierda de condición de coincidencia de Hola explicará condición Hola actualmente seleccionado en detalle.
   > 
   >  Para hello lista completa de las expresiones condicionales en detalle, consulte [expresiones condicionales de motor de reglas](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Para hello lista completa de las condiciones de coincidencia de forma detallada, consulte [coincide con condiciones del motor de reglas](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Haga clic en hello  **+**  aparece al lado demasiado**características** tooadd una nueva característica.  En la lista desplegable de Hola Hola izquierda, seleccione **Force interno Max-Age**.  En el cuadro de texto hello que aparece, escriba **300**.  Deje Hola restantes valores predeterminados.
   
   ![Característica de CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Como con las condiciones de coincidencia, haga clic en hello azul icono informativo toohello dejó de hello nueva característica mostrará información sobre esta característica.  En caso de hello de **Force interno Max-Age**, nos estamos reemplazar del recurso de hello **Cache-Control** y **Expires** encabezados toocontrol al nodo del borde CDN Hola actualizará Hola activo a partir de origen de Hola.  Nuestro ejemplo de 300 segundos significa el nodo del borde CDN Hola almacenarán en caché activo de Hola durante 5 minutos antes de actualizar los activos de Hola desde su origen.
   > 
   > Para hello lista completa de características de forma detallada, consulte [detalles de característica de motor de reglas](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Haga clic en hello **agregar** nueva regla de botón toosave Hola.  nueva regla de Hello ahora está en espera de aprobación. Una vez aprobada, estado de hello cambiará de **XML pendiente** demasiado**XML Active**.
   
   > [!IMPORTANT]
   > Cambios de reglas pueden tardar too90 minutos toopropagate a través de la red CDN Hola.
   > 
   > 

## <a name="see-also"></a>Otras referencias
* [Información general de la red CDN de Azure](cdn-overview.md)
* [Referencia del motor de reglas](cdn-rules-engine-reference.md)
* [Condiciones de coincidencia del motor de reglas](cdn-rules-engine-reference-match-conditions.md)
* [Expresiones condicionales del motor de reglas](cdn-rules-engine-reference-conditional-expressions.md)
* [Funciones del motor de reglas](cdn-rules-engine-reference-features.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
* [Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Azure Fridays: Características nuevas y eficaces de la edición Premium de CDN de Azure) (vídeo)