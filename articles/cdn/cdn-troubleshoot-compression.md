---
title: "compresión de archivo aaaTroubleshooting en la red CDN de Azure | Documentos de Microsoft"
description: "Solucione los problemas con la compresión de archivos de la red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Solución de problemas de compresión de archivos de red CDN
Este artículo le ayudará a solucionar los problemas con la [compresión de archivos de red CDN](cdn-improve-performance.md).

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.

## <a name="symptom"></a>Síntoma
Está habilitada la compresión para el punto de conexión, pero se devuelven archivos sin comprimir.

> [!TIP]
> toocheck si se devuelven los archivos comprimidos, necesita toouse una herramienta como [Fiddler](http://www.telerik.com/fiddler) o el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Encabezados de respuesta de comprobación Hola HTTP devuelvan con la red CDN en caché contenidos.  Si hay un encabezado denominado `Content-Encoding` con un valor de **gzip**, **bzip2**, o **deflate**, el contenido se comprime.
> 
> ![Encabezado content-encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Causa
Hay varias causas posibles, por nombrar algunas:

* Hola solicitado no es elegible para la compresión de contenido.
* La compresión no está habilitada para hello solicita el tipo de archivo.
* solicitud HTTP de Hello no incluía un encabezado que solicita un tipo de compresión válidos.

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas
> [!TIP]
> Al igual que con la implementación de nuevos puntos de conexión, los cambios de configuración de red CDN tienen algunos toopropagate tiempo a través de la red de Hola.  Normalmente, los cambios se aplican en un plazo de 90 minutos.  Si se trata de hello primera vez que se ha establecido la compresión para el punto de conexión, considere la posibilidad de 1 y 2 horas toobe seguro de los valores de compresión de hello propagaron toohello POP en espera. 
> 
> 

### <a name="verify-hello-request"></a>Comprobar la solicitud Hola
En primer lugar, debemos hacer una comprobación rápida en la solicitud de saludo.  Puede usar el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello las solicitudes realizadas.

* Compruebe la solicitud de saludo se enviaran a dirección URL del extremo de tooyour, `<endpointname>.azureedge.net`y no su origen.
* Compruebe la solicitud de hello contiene un **Accept-Encoding** hello y encabezado el valor de ese encabezado contiene **gzip**, **deflate**, o **bzip2** .

> [!NOTE]
> Los perfiles de la **red CDN de Azure de Akamai** solo admiten la codificación **gzip**.
> 
> 

![Encabezados de solicitud de red CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Comprobar la configuración de compresión (perfil de red CDN estándar)
> [!NOTE]
> Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN estándar de Azure de Verizon** o de **red CDN estándar de Azure de Akamai**. 
> 
> 

Navegar por el extremo de tooyour en hello [portal de Azure](https://portal.azure.com) y haga clic en hello **configurar** botón.

* Compruebe que la compresión está habilitada.
* Compruebe el tipo MIME que Hola Hola contenido toobe comprimido está incluido en lista de Hola de formatos comprimidos.

![Configuración de compresión de red CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Comprobar la configuración de compresión (perfil de red CDN Premium)
> [!NOTE]
> Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN Premium de Azure de Verizon** .
> 
> 

Navegar por el extremo de tooyour en hello [portal de Azure](https://portal.azure.com) y haga clic en hello **administrar** botón.  se abrirá el portal complementario de Hola.  Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.  Haga clic en **Compresión**. 

* Compruebe que la compresión está habilitada.
* Comprobar hello **tipos de archivo** lista contiene una lista separada por comas (sin espacios) de los tipos MIME.
* Compruebe el tipo MIME que Hola Hola contenido toobe comprimido está incluido en lista de Hola de formatos comprimidos.

![Configuración de compresión de red CDN Premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Compruebe que se almacena en caché el contenido de Hola
> [!NOTE]
> Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).
> 
> 

Con herramientas de desarrollo de su explorador, compruebe el archivo hello tooensure encabezados de respuesta de Hola se almacena en caché en la región de Hola donde se solicita.

* Comprobar hello **Server** encabezado de respuesta.  encabezado de Hello debe tener formato de hello **plataforma (Id. de servidor/POP)**, tal como se muestra en el siguiente ejemplo de Hola.
* Comprobar hello **X caché** encabezado de respuesta.  debe leer el encabezado de Hello **ACIERTOS**.  

![Encabezados de respuesta de red CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Compruebe el archivo hello cumple los requisitos de tamaño de Hola
> [!NOTE]
> Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).
> 
> 

toobe apta para la compresión, un archivo debe cumplir Hola según los requisitos de tamaño:

* Mayor que 128 bytes.
* Menor que 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Compruebe la solicitud de hello en el servidor de origen de hello para un **a través de** encabezado
Hola **a través de** encabezado HTTP indica el servidor de web toohello que Hola solicitud se pasa por un servidor proxy.  Servidores web de Microsoft IIS de forma predeterminada no comprimen las respuestas cuando la solicitud de hello contiene un **a través de** encabezado.  toooverride este comportamiento, realizar Hola siguientes:

* **IIS 6**: [establecer HcNoCompressionForProxies = "FALSE" en Propiedades de la Metabase de IIS de Hola](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 y hasta**: [establecer **noCompressionForHttp10** y **noCompressionForProxies** tooFalse en configuración del servidor hello](http://www.iis.net/configreference/system.webserver/httpcompression)

