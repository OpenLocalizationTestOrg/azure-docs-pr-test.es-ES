---
title: aaaManage streaming extremos con hello portal de Azure | Documentos de Microsoft
description: "Este tema muestra cómo los extremos de streaming con toomanage Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Administrar los extremos de streaming con hello portal de Azure

Este tema muestra cómo toouse Hola extremos de streaming de toomanage de portal de Azure. 

>[!NOTE]
>Realizar seguro hello tooreview [Introducción](media-services-streaming-endpoints-overview.md) tema. 

Para obtener información acerca de cómo tooscale Hola extremo de streaming, vea [esto](media-services-portal-scale-streaming-endpoints.md) tema.

## <a name="start-managing-streaming-endpoints"></a>Inicio de la administración de puntos de conexión de streaming 

Hola toostart administrar extremos de streaming para su cuenta, después.

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** hoja, seleccione **los extremos de Streaming**.
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Solo se le cobrará cuando StreamingEndpoint esté en estado en ejecución.

## <a name="adddelete-a-streaming-endpoint"></a>Adición o eliminación de puntos de conexión de streaming

>[!NOTE]
>no se puede eliminar predeterminado Hola extremo de streaming.

tooadd/delete streaming extremo mediante Hola portal de Azure, Hola siguientes:

1. tooadd un extremo de streaming, haga clic en hello **+ extremo** al principio de Hola de página de Hola. 

    Es recomendable varios extremos de Streaming si tiene previsto toohave CDN diferente o una CDN y el acceso directo.

2. Presione toodelete un extremo de streaming, **eliminar** botón.      
3. Haga clic en hello **iniciar** Hola de toostart botón extremo de streaming.
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Configuración de extremo de Streaming de Hola
Extremo de streaming permite hello tooconfigure propiedades siguientes:

* Control de acceso
* Control de caché
* Directivas de acceso en varios sitios

Para obtener información detallada acerca de estas propiedades, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Puede configurar el extremo de streaming haciendo Hola siguiente:

1. Seleccione Hola desea tooconfigure de extremo de streaming.
2. Haga clic en **Configuración**.

A continuación se muestra una breve descripción de los campos de Hola.

![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Directiva de caché máximo: duración en caché de tooconfigure usado para los activos se sirve a través de este extremo de streaming. Si se establece ningún valor, se utiliza el predeterminado de Hola. valores predeterminados de Hello también pueden definirse directamente en el almacenamiento de Azure. Si la CDN de Azure está habilitada para el extremo de streaming de hello, no debería establecer a Hola caché directiva valor que no requiere herramientas de 600 segundos.  
2. Direcciones IP permitidas: usar direcciones IP de toospecify que se podrá tooconnect toohello publicado extremo de streaming. Si no hay direcciones IP especificadas, cualquier dirección IP sería capaz de tooconnect. Las direcciones IP se pueden especificar como una dirección IP única (por ejemplo, 10.0.0.1), un intervalo de IP que usa una dirección IP y una máscara de subred CIDR (por ejemplo, 10.0.0.1/22) o un intervalo de IP que usa una máscara de subred decimal con puntos; por ejemplo, 10.0.0.1(255.255.255.0).
3. Configuración para la autenticación de encabezado de firma de Akamai: usa toospecify cómo se configura la solicitud de autenticación de encabezado de firma procedentes de servidores Akamai. La expiración está en formato UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Escalado del punto de conexión de streaming premium

Para obtener más información, consulte [este tema](media-services-portal-scale-streaming-endpoints.md) .

## <a id="enable_cdn"></a>Habilitación de la integración de CDN de Azure

Cuando se crea una nueva cuenta, la integración de la red CDN de Azure de punto de conexión de streaming está habilitada de forma predeterminada.

Si posteriormente desea hello toodisable/habilitar CDN, debe ser el extremo de streaming en hello **detenido** estado. Podrían tardar horas de too2 para tooget de integración de CDN de Azure Hola habilitada y para hello cambios toobe active a través de hello todos los POP de CDN. Sin embargo, puede iniciar el punto de conexión y el flujo sin interrupciones transmisión por secuencias de extremo de streaming de hello y una vez completada la integración de hello, flujo de Hola se entregarán de CDN Hola. Durante la Hola aprovisionamiento período su extremo de streaming estará en **a partir de** estado y se puede observar el rendimiento de degredad.

Integración de CDN está habilitada en todos los execpt de centros de datos de Azure de hello China y regiones de Gobierno Federal.

Una vez habilitada, Hola **el Control de acceso**, **nombre de host personalizado** y **autenticación de firma de Akamai** configuración obtiene deshabilitada.
 
> [!IMPORTANT]
> La integración de Azure Media Services con la red CDN de Azure se implementa en la **red CDN de Azure de Verizon** para puntos de conexión de streaming estándar. Los puntos de conexión de streaming premium pueden configurarse con todos los **proveedores y planes de tarifa de la red CDN de Azure**. Para obtener más información acerca de las características de red CDN de Azure, vea hello [información general de la red CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Consideraciones adicionales

* Cuando CDN esté habilitado para un extremo de transmisión por secuencias, los clientes no pueden solicitar contenido directamente desde el origen de Hola. Si necesita el contenido con o sin red CDN Hola tootest de capacidad, puede crear otro extremo de transmisión por secuencias que no está habilitado de CDN.
* La transmisión por secuencias permanece hostname de punto de conexión Hola igual después de habilitar la red CDN. No es necesario toomake cualquier flujo de trabajo de cambios tooyour media services después de habilita la red CDN. Por ejemplo, si el nombre de host de punto de conexión transmisión por secuencias es strasbourg.streaming.mediaservices.windows.net, después de habilitar la red CDN, se utiliza Hola exacta mismo nombre de host.
* Para nuevos extremos de transmisión por secuencias, puede habilitar CDN creando un nuevo punto de conexión; para los extremos de streaming existentes, necesita el punto de conexión de toofirst stop hello y, a continuación, habilitar/deshabilitar Hola CDN.
* El punto de conexión de streaming estándar solo se puede configurar mediante el **proveedor de red CDN estándar de Verizon** con el portal de administración de Azure. Sin embargo, puede habilitar otros proveedores de la red CDN de Azure mediante las API de REST.

## <a name="configure-cdn-profile"></a>Configuración del perfil de la red CDN

Puede configurar el perfil de CDN Hola seleccionando hello **administrar CDN** botón desde la parte superior de Hola.

![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

