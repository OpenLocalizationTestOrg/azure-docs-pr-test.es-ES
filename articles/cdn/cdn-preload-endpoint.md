---
title: "carga aaaPre activos en un punto de conexión de red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopre carga almacena en caché el contenido en un punto de conexión de red CDN de Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Carga previa de activos en un punto de conexión de CDN de Azure
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

De forma predeterminada, los recursos primero se almacenan en caché conforme se solicitan. Esto significa que la primera solicitud de cada región de hello puede tardar más tiempo, debido a que los servidores de hello borde no tendrán contenido Hola almacena en caché y deberá tooforward Hola solicitud enviada toohello origen al servidor. La precarga del contenido evita esta latencia de primera visita.

Además tooproviding una mejor experiencia de cliente, Cargando previamente los recursos almacenados en memoria caché también puede reducir el tráfico de red en el servidor de origen de Hola.

> [!NOTE]
> Cargando previamente activos es útil para los eventos de gran tamaño o contenido deja de estar disponible al mismo tiempo tooa gran número de usuarios, como una nueva versión de la película o una actualización de software.
> 
> 

Este tutorial le guiará a través de la precarga de contenido almacenado en la caché en todos los nodos perimetrales de CDN de Azure.

## <a name="walkthrough"></a>Tutorial
1. Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN toohello que contiene el extremo de hello desea toopre carga.  se abre la hoja de perfil de Hola.
2. Haga clic en el punto de conexión de hello en lista de Hola.  se abre la hoja de punto de conexión de Hola.
3. Desde la hoja de punto de conexión de red CDN Hola, haga clic en el botón de carga de Hola.
   
    ![Hoja Punto de conexión de CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    se abre la hoja de la carga de Hola.
   
    ![Hoja Carga de CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Escriba la ruta de acceso completa de Hola de cada recurso que se va tooload (p. ej., `/pictures/kitten.png`) en hello **ruta de acceso** cuadro de texto.
   
   > [!TIP]
   > Más **ruta de acceso** cuadros de texto que aparecerá después de escribir texto tooallow toobuild una lista de varios activos.  Puede eliminar los activos de lista de hello haciendo clic en el botón de puntos suspensivos (...) de Hola.
   > 
   > Las rutas de acceso deben ser una dirección URL relativa que se ajuste a continuación hello [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Carga de un solo archivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Carga de un único archivo con cadena de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Cada recurso debe tener su propia ruta de acceso.  No hay ninguna funcionalidad comodín para la carga previa de recursos.
   > 
   > 
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Haga clic en hello **carga** botón.
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Hay una limitación de 10 solicitudes de carga por minuto por perfil de red CDN. Se admiten 50 rutas por solicitud. Cada ruta de acceso tiene un límite de longitud de 1024 caracteres.
> 
> 

## <a name="see-also"></a>Otras referencias
* [Purgar un punto de conexión de red CDN de Azure](cdn-purge-endpoint.md)
* [Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión](https://msdn.microsoft.com/library/mt634451.aspx)

