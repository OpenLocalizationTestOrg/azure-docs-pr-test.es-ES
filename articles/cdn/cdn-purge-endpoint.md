---
title: "aaaPurge un punto de conexión de red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopurge todos los almacena en caché contenido desde un punto de conexión de red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Purgar un punto de conexión de red CDN de Azure
## <a name="overview"></a>Información general
Nodos de borde CDN de Azure almacenará en memoria caché activos hasta que expire el período de vida (TTL) del recurso de Hola.  Después de que expire TTL del recurso de hello, cuando un cliente solicita asset Hola desde el nodo del borde de hello, nodo de hello borde recuperará una nueva copia actualizada de solicitud de cliente de hello asset tooserve hello y almacenar Hola de actualización de caché.

toomake de prácticas recomendada de Hello seguro a los usuarios obtengan siempre la copia más reciente de Hola de sus activos es tooversion sus activos para cada actualización y publican como nuevas direcciones URL.  CDN recuperará inmediatamente nuevos activos de Hola Hola siguiente las solicitudes de cliente.  En ocasiones, es recomendable toopurge almacenado en caché contenido de todos los nodos de borde y hacer a todos los tooretrieve nuevos activos actualizados.  Esto podría ser debido a la aplicación web de tooupdates tooyour, o los activos de la actualización de tooquickly que contengan información incorrecta.

> [!TIP]
> Tenga en cuenta que sólo purga borra Hola almacenado en caché contenido en los servidores de borde CDN Hola.  Todas las cachés de nivel inferiores, como servidores proxy y cachés de explorador local, todavía pueden albergar una copia en caché de archivo hello.  Es importante tooremember esto al establecer un archivo período de vida.  Puede forzar una versión más reciente de cliente de nivel inferior toorequest Hola del archivo asignándole un nombre único cada vez que lo actualice o aprovechando las ventajas de [almacenamiento en memoria caché en la cadena de consulta](cdn-query-string.md).  
> 
> 

Este tutorial le guiará a través de purga de los recursos de todos los nodos perimetrales de un punto de conexión.

## <a name="walkthrough"></a>Tutorial
1. Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN toohello que contiene el punto de conexión de hello desea toopurge.
2. Desde la hoja de perfil CDN Hola, haga clic en el botón de purga de Hola.
   
    ![Hoja del perfil de red CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    se abre la hoja de purga de Hola.
   
    ![Hoja de purga de red CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. En hello purgar hoja, seleccione la dirección del servicio Hola desea toopurge de lista desplegable de dirección URL de Hola.
   
    ![Formulario para purgar](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > También puede obtener toohello purga hoja haciendo clic en hello **purgar** botón en la hoja de punto de conexión de red CDN Hola.  En ese caso, Hola **URL** campo se rellenará automáticamente con la dirección de servicio de Hola de ese punto de conexión concreto.
   > 
   > 
4. Seleccione qué activos desea toopurge de hello nodos perimetrales.  Si desea que todos los activos tooclear, haga clic en hello **purgar todo** casilla de verificación.  En caso contrario, ruta de acceso de tipo hello de cada recurso que se va toopurge Hola **ruta de acceso** cuadro de texto. Por debajo de los formatos son compatibles con la ruta de acceso de Hola.
    1. **Purga de dirección URL única**: purga activo individual especificando la dirección URL completa de hello, con o sin la extensión de archivo hello, p. ej.,`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Purga con carácter comodín**: se puede usar el asterisco (\*) como carácter comodín. Purgar todas las carpetas, subcarpetas y archivos en un punto de conexión con `/*` en Hola ruta de acceso o purgar todas las subcarpetas y archivos en una carpeta específica mediante la especificación de la carpeta de hello seguido de `/*`, p. ej.,`/pictures/*`.  Tenga en cuenta que, en estos momentos, la purga de carácter comodín no es compatible con la red CDN de Azure de Akamai. 
    3. **Purga de dominio raíz**: raíz de Hola de purga de punto de conexión de hello con "/" en la ruta de acceso de Hola.
   
   > [!TIP]
   > Las rutas de acceso debe especificarse para purgar y debe ser una dirección URL relativa que se ajusten a siguiente hello [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx). **Purgar todo** y la **purga con carácter comodín** no son compatibles en estos momentos con la **red CDN de Azure de Akamai**.
   > > Purga con una sola URL `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Cadena de consulta `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Purga con carácter comodín `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";` 
   > 
   > Más **ruta de acceso** cuadros de texto que aparecerá después de escribir texto tooallow toobuild una lista de varios activos.  Puede eliminar los activos de lista de hello haciendo clic en el botón de puntos suspensivos (...) de Hola.
   > 
5. Haga clic en hello **purgar** botón.
   
    ![Botón Purgar](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Purgar las solicitudes tardar aproximadamente 2 a 3 minutos tooprocess con **CDN de Azure de Verizon** (Standard y Premium) y aproximadamente 7 minutos con **Azure CDN de Akamai**.  La red CDN de Azure tiene un límite de 50 solicitudes de purga simultáneas en un momento dado. 
> 
> 

## <a name="see-also"></a>Consulte también
* [Carga previa de activos en un punto de conexión de CDN de Azure](cdn-preload-endpoint.md)
* [Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión](https://msdn.microsoft.com/library/mt634451.aspx)

