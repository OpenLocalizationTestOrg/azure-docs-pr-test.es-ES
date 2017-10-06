---
title: "Administración de API de Azure aaaDeploy services toomultiple Azure regiones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una administración de API de Azure service instancia toomultiple Azure regiones."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Cómo toodeploy una administración de API de Azure service instancia toomultiple Azure regiones
Administración de API admite la implementación de varias regiones que habilita la API publicadores toodistribute un único servicio de administración de API a través de cualquier número de regiones de Azure deseadas. Esto ayuda a reducir la latencia de solicitud que perciben los usuarios de API distribuidos geográficamente y, además, mejora la disponibilidad del servicio en caso de que una región se quede sin conexión. 

Cuando se crea inicialmente un servicio de administración de API, contiene solamente un [unidad] [ unit] y reside en una sola región de Azure, que se designa como Hola región principal. Otras regiones pueden agregarse fácilmente a través de hello Portal de Azure. Un servidor de puerta de enlace de administración de API es región tooeach implementado y el tráfico de llamada será toohello enrutado puerta de enlace más cercano. Si una región se queda sin conexión, el tráfico de hello es toohello redirige automáticamente siguiente más cercano puerta de enlace. 

> [!IMPORTANT]
> Implementación de varias regiones solo está disponible en hello  **[Premium] [ Premium]**  capa.
> 
> 

## <a name="add-region"></a>Implementar un área nueva de administración de API servicio instancia tooa
> [!NOTE]
> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Hola Portal de Azure, navegue toohello **escala y precios** página para la instancia de servicio de administración de API. 

![Pestaña Escala][api-management-scale-service]

toodeploy tooa nueva región, haga clic en **+ Agregar región** de barra de herramientas de Hola.

![Agregar región][api-management-add-region]

Seleccionar ubicación de hello en la lista desplegable de Hola y establecer el número de Hola de unidades con el control deslizante de Hola.

![Especificar unidades][api-management-select-location-units]

Haga clic en **agregar** tooplace su selección en la tabla de ubicaciones de Hola. 

Repita este proceso hasta que haya configurado de todas las ubicaciones y haga clic en **guardar** del proceso de implementación de hello barra de herramientas toostart Hola.

## <a name="remove-region"></a>Eliminación de una instancia de servicio de API Management de una ubicación
Hola Portal de Azure, navegue toohello **escala y precios** página para la instancia de servicio de administración de API. 

![Pestaña Escala][api-management-scale-service]

Para la ubicación de hello le gustaría tooremove abrir menú contextual de hello mediante hello **...**  situado en el extremo derecho de Hola de tabla Hola. Seleccione hello **eliminar** opción.

![Quitar región][api-management-remove-region]

Confirmar eliminación de Hola y haga clic en **guardar** cambios de hello tooapply.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

