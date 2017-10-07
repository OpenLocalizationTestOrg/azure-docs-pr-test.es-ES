---
title: aaaGetting a trabajar con la red CDN de Azure | Documentos de Microsoft
description: "Este tema muestra cómo tooenable Hola red de entrega de contenido (CDN) de Azure. Hola tutorial le guía a través de la creación de hello de un nuevo perfil CDN y el punto de conexión."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Introducción a Azure CDN
Este tema le guía a través de la habilitación de la red CDN de Azure mediante la creación de un perfil de red CDN y un punto de conexión nuevo.

> [!IMPORTANT]
> Para un funcionamiento CDN toohow introducción, así como una lista de características, vea hello [información general de la red CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Crear un nuevo perfil de CDN
Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.  Cada perfil contiene uno o más de estos puntos de conexión de CDN.  Puede ser conveniente toouse varios tooorganize perfiles los extremos de red CDN el dominio de internet, las aplicaciones web u otros criterios.

> [!NOTE]
> De forma predeterminada, una sola suscripción de Azure es limitado tooeight perfiles de red CDN. Cada perfil de CDN es puntos de conexión de red CDN tooten limitado.
> 
> Precios de CDN se aplican al nivel de perfil CDN Hola. Si desea toouse una combinación de CDN de Azure los niveles de precios, necesitará varios perfiles de red CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Crear un nuevo extremo de CDN
**toocreate un nuevo extremo CDN**

1. Hola [Portal de Azure](https://portal.azure.com), navegar por el perfil de CDN tooyour.  Puede haber anclarlo toohello panel en el paso anterior de Hola.  Si no es así, se encontrará, haciendo clic en **examinar**, a continuación, **perfiles de red CDN**, y haga clic en el perfil de hello tiene previsto tooadd del extremo que.
   
    aparece la hoja de perfil CDN Hola.
   
    ![Perfil de CDN][cdn-profile-settings]
2. Haga clic en hello **Agregar extremo** botón.
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    Hola **agregar un punto de conexión** aparece hoja.
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.  Este nombre será tooaccess usa los recursos almacenados en caché en el dominio de hello `<endpointname>.azureedge.net`.
4. Hola **tipo de origen** de lista desplegable, seleccione el tipo de origen.  Seleccione **Almacenamiento** para una cuenta de Azure Storage, **Servicio en la nube** para un servicio en la nube de Azure, **Aplic. web** para una aplic. web de Azure, o bien **Origen personalizado** para cualquier otro origen del servidor web públicamente accesible (hospedado en Azure o en otro lugar).
   
    ![Tipo de origen de la red CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. Hola **nombre de host de origen** de lista desplegable, seleccione o escriba el dominio de origen.  Hola desplegable mostrará una lista de todos los orígenes disponibles del tipo hello que especificó en el paso 4.  Si seleccionó *origen personalizado* como su **tipo de origen**, tendrá que escribir en el dominio de Hola de su origen personalizado.
6. Hola **ruta de acceso de origen** texto cuadro, escriba recursos toohello Hola ruta de acceso que desea toocache, o deje en blanco tooallow caché cualquier recurso en el dominio de Hola que especificó en el paso 5.
7. Hola **encabezado de host de origen**, escriba el encabezado de host de hello desea Hola toosend CDN con cada solicitud, o deje Hola predeterminado.
   
   > [!WARNING]
   > Algunos tipos de orígenes, como el almacenamiento de Azure y las aplicaciones Web, requieren dominio hello toomatch de encabezado de host de Hola de origen de Hola. A menos que tenga un origen que requiere un encabezado de host diferente de su dominio, debe dejar el valor predeterminado de Hola.
   > 
   > 
8. Para **protocolo** y **puerto de origen**, especificar Hola protocolos y puertos tooaccess usa los recursos en el origen de Hola.  Se debe seleccionar al menos un protocolo (HTTP o HTTPS).
   
   > [!NOTE]
   > Hola **puerto de origen** solo afecta a qué punto de conexión de puerto hello usa información de tooretrieve de origen de Hola.  Hello propio extremo solo será clientes tooend disponible en hello predeterminado puertos HTTP y HTTPS (80 y 443), independientemente de hello **puerto de origen**.  
   > 
   > **Azure CDN de Akamai** puntos de conexión no permita que el intervalo de puertos TCP completa de Hola para orígenes.  Para obtener una lista de los puertos de origen que no se permiten, consulte [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Puertos de origen permitidos de la red CDN de Azure de Akamai).  
   > 
   > Obtener acceso a la red CDN tiene contenido mediante HTTPS Hola siguiendo las restricciones:
   > 
   > * Debe usar el certificado SSL de hello proporcionado por la red CDN Hola. No se admiten certificados de terceros.
   > * Debe usar el dominio de siempre CDN Hola (`<endpointname>.azureedge.net`) tooaccess contenido HTTPS. Compatibilidad con HTTPS no está disponible para nombres de dominio personalizados (CNAME) ya que la red CDN Hola no admite certificados personalizados en este momento.
   > 
   > 
9. Haga clic en hello **agregar** toocreate botón Hola nuevo punto de conexión.
10. Una vez que se crea el extremo de hello, aparece en una lista de puntos de conexión para el perfil de Hola. vista de lista de Hello muestra hello URL toouse tooaccess almacenado en memoria caché de contenido, así como dominio de origen de Hola.
    
    ![Punto de conexión de CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > punto de conexión de Hello no inmediatamente estará disponible para su uso, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.  Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.  Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.
    > 
    > Los usuarios que intenten nombre de dominio de red CDN Hola de toouse antes de configuración de extremo de hello haya propagado toohello POP recibirá los códigos de respuesta HTTP 404.  Si han pasado varias horas desde que creó el punto de conexión y aún recibe errores 404, consulte [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md)(Solución de problemas de puntos de conexión de redes CDN que devuelven errores 404).
    > 
    > 

## <a name="see-also"></a>Otras referencias
* [Control del comportamiento del almacenamiento en caché de las solicitudes con cadenas de consulta](cdn-query-string.md)
* [¿Cómo tooMap CDN contenido tooa dominio personalizado](cdn-map-content-to-custom-domain.md)
* [Carga previa de activos en un punto de conexión de CDN de Azure](cdn-preload-endpoint.md)
* [Depuración de un punto de conexión de red de entrega de contenido de Azure](cdn-purge-endpoint.md)
* [Solución de problemas de redes CDN que devuelven errores 404](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
