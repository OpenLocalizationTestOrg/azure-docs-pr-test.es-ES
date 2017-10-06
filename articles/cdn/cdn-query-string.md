---
title: "comportamiento de almacenamiento en caché de CDN de Azure con cadenas de consulta aaaControl | Documentos de Microsoft"
description: "Cadena de consulta CDN Azure controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Red CDN premium de Azure de Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Información general
Cadena de consulta controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché.

> [!IMPORTANT]
> productos Standard y Premium CDN Hola proporcionan Hola misma funcionalidad de almacenamiento en caché de cadenas de consulta, pero difiere de la interfaz de usuario de Hola.  Este documento describe la interfaz de Hola de **estándar de red CDN de Azure de Akamai** y **estándar de red CDN de Azure de Verizon**.  Para más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN premium de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de CDN con cadenas de consultas - Premium](cdn-query-string-premium.md).
> 
> 

Hay tres modos disponibles:

* **Pasar por alto las cadenas de consulta**: se trata de modo predeterminado de Hola.  nodo del borde CDN Hola pasará cadena de consulta de Hola de origen de toohello de solicitante de hello en la primera solicitud de Hola y activos de Hola de caché.  Todas las solicitudes posteriores para dicho activo que se atienden desde el nodo del borde de hello hará caso omiso cadena de consulta de hello hasta que expire el activo en caché Hola.
* **Omitir almacenamiento en caché para la dirección URL con cadenas de consulta**: en este modo, las solicitudes con cadenas de consulta no se almacenan en el nodo del borde CDN Hola.  nodo de Hello borde recupera asset Hola directamente desde el origen de hello y pasa toohello solicitante con cada solicitud.
* **Almacenar en caché cada URL única**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.  Por ejemplo, Hola respuesta desde origen Hola para una solicitud de *foo.ashx?q=bar* se almacena en caché en el nodo del borde de Hola y devueltos para las cachés posteriores con esa misma cadena de consulta.  Una solicitud de *foo.ashx?q=somethingelse* podría almacenarse en memoria caché como un recurso independiente con su propio tiempo toolive.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN estándar
1. En la hoja de perfil CDN Hola, haga clic en extremo de red CDN Hola desea toomanage.
   
    ![Puntos de conexión de hoja del perfil de red CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    se abre la hoja de punto de conexión de red CDN Hola.
2. Haga clic en hello **configurar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    se abre la hoja de configuración de red CDN Hola.
3. Seleccione una opción de hello **comportamiento almacenamiento en caché de cadena de consulta** lista desplegable.
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string/cdn-query-string.png)
4. Después de realizar la selección, haga clic en hello **guardar** botón.

> [!IMPORTANT]
> cambios de configuración de Hello no pueden ser inmediatamente visibles, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.  Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.  Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.
> 
> 

