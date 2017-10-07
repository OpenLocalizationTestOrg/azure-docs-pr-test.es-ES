---
title: "comportamiento de almacenamiento en caché de CDN de Azure con cadenas de consulta - Premium aaaControl | Documentos de Microsoft"
description: "Cadena de consulta CDN Azure controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta: Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Red CDN premium de Azure de Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Información general
Cadena de consulta controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché.

> [!IMPORTANT]
> productos Standard y Premium CDN Hola proporcionan Hola misma funcionalidad de almacenamiento en caché de cadenas de consulta, pero difiere de la interfaz de usuario de Hola.  Este documento describe la interfaz de Hola de **Premium de CDN de Azure de Verizon**.  Para obtener más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN estándar de Azure de Akamai** y la **red CDN estándar de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de red CDN con cadenas de consultas](cdn-query-string.md).
> 
> 

Hay tres modos disponibles:

* **caché estándar**: se trata de modo predeterminado de Hola.  nodo del borde CDN Hola pasará cadena de consulta de Hola de origen de toohello de solicitante de hello en la primera solicitud de Hola y activos de Hola de caché.  Todas las solicitudes posteriores para dicho activo que se atienden desde el nodo del borde de hello hará caso omiso cadena de consulta de hello hasta que expire el activo en caché Hola.
* **sin caché**: en este modo, las solicitudes con cadenas de consulta no se almacenan en el nodo del borde CDN Hola.  nodo de Hello borde recupera asset Hola directamente desde el origen de hello y pasa toohello solicitante con cada solicitud.
* **unique-cache**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.  Por ejemplo, Hola respuesta desde origen Hola para una solicitud de *foo.ashx?q=bar* se almacena en caché en el nodo del borde de Hola y devueltos para las cachés posteriores con esa misma cadena de consulta.  Una solicitud de *foo.ashx?q=somethingelse* podría almacenarse en memoria caché como un recurso independiente con su propio tiempo toolive.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN premium
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.  Haga clic en **Almacenamiento en caché de cadenas de consultas**.
   
    Aparecen las opciones del almacenamiento en caché de cadenas de consultas.
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. Después de realizar la selección, haga clic en hello **actualización** botón.

> [!IMPORTANT]
> cambios de configuración de Hello no pueden ser inmediatamente visibles, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.  Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.
> 
> 

