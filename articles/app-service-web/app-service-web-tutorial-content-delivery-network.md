---
title: un servicio de aplicaciones de Azure CDN tooan aaaAdd | Documentos de Microsoft
description: "Agregue un toocache de servicio de aplicaciones de Azure de red de entrega de contenido (CDN) tooan y entregar los archivos estáticos desde servidores clientes de tooyour cerrar todo Hola a todos."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Agregar un servicio de aplicaciones de Azure tooan de red de entrega de contenido (CDN)

[Red de entrega de contenido (CDN) Azure](../cdn/cdn-overview.md) almacena en caché contenido web estático en el rendimiento máximo de tooprovide situadas estratégicamente para entregar contenido toousers. CDN Hola también reduce la carga del servidor en la aplicación web. Este tutorial se muestra cómo tooadd CDN de Azure tooa [aplicación web en el servicio de aplicación de Azure](app-service-web-overview.md). 

Aquí es página principal de Hola de hello ejemplo sitio HTML estático que va a trabajar con:

![Página de inicio de la aplicación de ejemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Temas que se abordarán:

> [!div class="checklist"]
> * Crear un punto de conexión de CDN.
> * Actualizar los recursos en caché.
> * Versiones de toocontrol almacenado en memoria caché de cadenas de consulta de uso.
> * Usar un dominio personalizado para el extremo de red CDN Hola.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

- [Instalación de Git](https://git-scm.com/)
- [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Crear una aplicación web de Hola

aplicación web de toocreate hello que trabajará con seguimiento hello [inicio rápido HTML estático](app-service-web-get-started-html.md) a través de hello **examinar toohello aplicación** paso.

### <a name="have-a-custom-domain-ready"></a>Tenga listo un dominio personalizado

paso de toocomplete Hola dominio personalizado de este tutorial, necesita tooown un dominio personalizado y tener del registro DNS de acceso tooyour para su proveedor de dominio (por ejemplo, GoDaddy). Por ejemplo, tooadd entradas DNS para `contoso.com` y `www.contoso.com`, debe tener la configuración de DNS de acceso tooconfigure Hola para hello `contoso.com` dominio raíz.

Si ya no tiene un nombre de dominio, considere la posibilidad de siguientes hello [tutorial de dominio de servicio de aplicaciones](custom-dns-web-site-buydomains-web-app.md) toopurchase un dominio con Hola portal de Azure. 

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Abra un explorador y navegue toohello [portal de Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Creación de un perfil y un punto de conexión de CDN

Hola barra de navegación izquierda, seleccione **servicios de aplicaciones**y, a continuación, seleccione aplicación hello que creó en hello [inicio rápido HTML estático](app-service-web-get-started-html.md).

![Seleccione la aplicación de servicio de aplicaciones en portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

Hola **servicio de aplicaciones** página Hola **configuración** sección, seleccione **redes > Configurar CDN de Azure para la aplicación**.

![Seleccione la red CDN en portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

Hola **red de entrega de contenido de Azure** , proporcione hello **nuevo extremo** configuración como se especifica en la tabla de Hola.

![Crear un perfil y punto de conexión en el portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Configuración | Valor sugerido | Descripción |
| ------- | --------------- | ----------- |
| **Perfil de CDN** | myCDNProfile | Seleccione **crear nuevo** toocreate un perfil de CDN. Un perfil de CDN es una colección de puntos de conexión de red CDN Hola mismo nivel de precios. |
| **Plan de tarifa** | Estándar de Akamai | Hola [tarifa](../cdn/cdn-overview.md#azure-cdn-features) especifica el proveedor de Hola y características disponibles. En este tutorial, usamos Akamai estándar. |
| **Nombre del punto de conexión de CDN** | Cualquier nombre que sea único en el dominio de hello azureedge.net | Obtener acceso a los recursos almacenados en caché en el dominio de hello  *\<endpointname >. azureedge.net*.

Seleccione **Crear**.

Azure crea el perfil de Hola y de punto de conexión. nuevo punto de conexión de Hello aparece en hello **extremos** lista Hola sintonía, y cuando se aprovisiona Hola estado **ejecutando**.

![Nuevo punto de conexión en la lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Hola extremo de red CDN de prueba

Si ha seleccionado el plan de tarifa de Verizon, la propagación del punto de conexión suele tardar unos 90 minutos. En Akamai, la propagación tarda unos minutos

aplicación de ejemplo de Hola tiene un `index.html` archivo y *css*, *img*, y *js* carpetas que contienen otros activos estáticos. Hola contenido de las rutas de acceso para todos estos archivos Hola igual al extremo de red CDN Hola. Por ejemplo, redes de hello las siguientes direcciones URL de acceso hello *bootstrap.css* archivo Hola *css* carpeta:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Navegar por un toohello explorador después de la dirección URL:

```
http://<endpointname>.azureedge.net/index.html
```

![Página de inicio de la aplicación de ejemplo servida desde la red CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Vea Hola misma página que se ha ejecutado anteriormente en una aplicación web de Azure. Red CDN de Azure recuperado activos de la aplicación web de hello origen y sirve de punto de conexión de red CDN Hola

tooensure que esta página se almacena en caché en hello CDN, página de actualización de Hola. Dos solicitudes para hello mismo activo a veces son necesarias para hello toocache CDN Hola contenido solicitado.

Para más información acerca de cómo crear perfiles y puntos de conexión de Azure CDN, consulte [Introducción a Azure CDN](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Purgar CDN Hola

CDN Hola actualiza periódicamente los recursos de aplicación web de origen de hello en función de la configuración de hello time-to-live (TTL). TTL predeterminado de Hello es siete días.

En ocasiones tendrá que toorefresh Hola CDN antes de hello caducidad de TTL: por ejemplo, cuando se implementa la aplicación web de toohello contenido actualizado. tootrigger una actualización, puede purgar manualmente los recursos de red CDN Hola. 

En esta sección del tutorial de hello, implementar una aplicación web de toohello de cambio y purgar Hola CDN tootrigger Hola CDN toorefresh su memoria caché.

### <a name="deploy-a-change-toohello-web-app"></a>Implementar una aplicación web de toohello de cambio

Abra hello `index.html` de archivos y agregue "-V2" toohello H1 encabezado, tal y como se muestra en el siguiente ejemplo de Hola: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Confirmar el cambio y lo implementará en la aplicación web de toohello.

```bash
git commit -am "version 2"
git push azure master
```

Una vez completada la implementación, examinar toohello dirección URL de aplicación web y ver Hola cambian.

```
http://<appname>.azurewebsites.net/index.html
```

![V2 en el título de la aplicación web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Examinar toohello CDN dirección URL del extremo para la página principal de Hola y no se ve Hola cambiar porque la versión almacenada en caché de hello en CDN Hola no ha expirado todavía. 

```
http://<endpointname>.azureedge.net/index.html
```

![Sin título V2 en la red CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Purgar Hola CDN en el portal de Hola

tootrigger Hola CDN tooupdate su versión almacenada en caché, purgar CDN Hola.

En hello portal de navegación izquierdo, seleccione **grupos de recursos**y, a continuación, seleccione grupo de recursos de Hola que creó para la aplicación web (myResourceGroup).

![Selección de un grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

En lista de Hola de recursos, seleccione el punto de conexión.

![Selección del punto de conexión](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

En parte superior de Hola de hello **extremo** página, haga clic en **purgar**.

![Seleccionar Purgar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Escriba Hola contenido las rutas de acceso que se va toopurge. Puede pasar un toopurge de ruta de acceso completa del archivo de un archivo individual o un toopurge de segmento de ruta de acceso y actualizar todo el contenido de una carpeta. Puesto que ha cambiado `index.html`, asegúrese de que es una de las rutas de acceso de Hola.

En hello parte inferior de la página de hello, seleccione **purgar**.

![Página Purgar](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Compruebe que Hola que CDN se actualiza

Espere hasta que la solicitud de purga de hello finaliza el procesamiento, normalmente un par de minutos. toosee Hola estado actual, un icono de campana Hola seleccione parte superior de Hola de página de Hola. 

![Notificación de purga](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Examinar dirección URL del extremo CDN de toohello para `index.html`, y ahora verá Hola V2 agregó toohello título en la página de inicio de Hola. Esto muestra que se ha actualizado la caché de la red CDN Hola.

```
http://<endpointname>.azureedge.net/index.html
```

![V2 en el título en la red CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Para más información, consulte [Purgar un punto de conexión de Azure CDN](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Usar el contenido de tooversion de cadenas de consulta

Hola CDN de Azure ofrece Hola siguientes opciones de comportamiento de almacenamiento en caché:

* Pasar por alto las cadenas de consulta
* Omitir el almacenamiento en caché de cadenas de consulta
* Almacenar en caché todas las URL únicas 

Hola primero de ellos es el valor predeterminado de hello, lo que significa que hay solo una versión almacenada en caché de un recurso, independientemente de la cadena de consulta de hello en dirección URL de Hola. 

En esta sección del tutorial de hello, cambiar Hola almacenamiento en caché comportamiento toocache todas las URL únicas.

### <a name="change-hello-cache-behavior"></a>Cambiar el comportamiento de la caché de Hola

En el portal de Azure hello **punto de conexión de red CDN** página, seleccione **caché**.

Seleccione **almacenar en caché todas las URL únicas** de hello **comportamiento almacenamiento en caché de cadena de consulta** lista desplegable.

Seleccione **Guardar**.

![Selección del comportamiento de almacenamiento de cadenas de consulta en caché](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Compruebe que las direcciones URL únicas se almacenan en caché por separado

En un explorador, navegue toohello portada en el extremo de red CDN Hola, pero incluir una cadena de consulta: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

CDN Hola devuelve Hola actual aplicación contenido web, que incluye "V2" en el encabezado de Hola. 

tooensure que esta página se almacena en caché en hello CDN, página de actualización de Hola. 

Abra `index.html` y cambiar "V2" demasiado "V3" e implementar el cambio de Hola. 

```bash
git commit -am "version 3"
git push azure master
```

En un explorador, vaya dirección URL del extremo CDN de toohello con una nueva cadena de consulta como `q=2`. CDN Hola obtiene Hola actual `index.html` de archivos y muestra "V3".  Pero si se desplaza el punto de conexión de red CDN de toohello con hello `q=1` cadena de consulta, vea "V2".

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 en el título en la red CDN, cadena de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 en el título en la red CDN, cadena de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Este resultado muestra que cada cadena de consulta se trata de manera diferente:

* q = 1 se usó antes, por lo que se devuelve contenido almacenado en caché (V2).
* q = 2 es nuevo, por lo que el contenido de aplicación web más reciente Hola se recuperan y se devolverán (V3).

Para más información, consulte [Control del comportamiento del almacenamiento en caché de Azure CDN con cadenas de consulta](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Asignar un punto de conexión de red CDN de tooa de dominio personalizado

Se asignará el extremo de red CDN de tooyour de dominio personalizado mediante la creación de un registro CNAME. Un registro CNAME es una característica DNS que se asigna a un dominio de destino de tooa de dominio de origen. Por ejemplo, podría asignar `cdn.contoso.com` o `static.contoso.com` demasiado`contoso.azureedge.net`.

Si no tiene un dominio personalizado, considere la posibilidad de siguientes hello [tutorial de dominio de servicio de aplicaciones](custom-dns-web-site-buydomains-web-app.md) toopurchase un dominio con Hola portal de Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Buscar Hola hostname toouse con hello CNAME

Hola portal de Azure **extremo** página, asegúrese de que **Introducción** está seleccionado en hello dejado de navegación y, a continuación, seleccione hello **+ dominio personalizado** situado en la parte superior de Hola de página de Hola.

![Seleccionar Agregar dominio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

Hola **agregar un dominio personalizado** página, verá toouse de nombre de host de punto de conexión de hello al crear un registro CNAME. nombre de host de Hola se deriva de las direcciones URL de extremo de red CDN:  **&lt;EndpointName >. azureedge.net**. 

![Página Agregar dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Configurar Hola CNAME con su registrador de dominios

Navegar por el sitio web del registrador de dominios de tooyour y busque la sección hello para la creación de registros DNS. Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.

Busque la sección de Hola para administrar registros CNAME. Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello CNAME, Alias o subdominios.

Crear un registro CNAME que asigne el subdominio elegido (por ejemplo, **estático** o **cdn**) toohello **nombre de host del punto de conexión** se muestra anteriormente en el portal de Hola. 

### <a name="enter-hello-custom-domain-in-azure"></a>Escriba el dominio personalizado de hello en Azure

Devolver toohello **agregar un dominio personalizado** página y escriba su dominio personalizado, incluido el subdominio de hello, en el cuadro de diálogo de Hola. Por ejemplo, escriba: `cdn.contoso.com`.   
   
Azure comprueba que existe el registro CNAME de hello para el nombre de dominio de Hola que ha escrito. Si Hola CNAME es correcto, se valida su dominio personalizado.

Puede tardar tiempo para los servidores de tooname de hello CNAME toopropagate registro de hello Internet. Si el dominio no se valida inmediatamente, espere unos minutos e inténtelo de nuevo.

### <a name="test-hello-custom-domain"></a>Dominio personalizado de prueba Hola

En un explorador, navegue toohello `index.html` archivo utilizando su dominio personalizado (por ejemplo, `cdn.contoso.com/index.html`) tooverify que es el resultado de Hola Hola igual como cuándo pasan directamente demasiado`<endpointname>azureedge.net/index.html`.

![Página de inicio de la aplicación de ejemplo utilizando la dirección URL de dominio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Para obtener más información, consulte [dominio personalizado de CDN de Azure de mapa tooa contenido](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Pasos siguientes

¿Qué ha aprendido?

> [!div class="checklist"]
> * Crear un punto de conexión de CDN.
> * Actualizar los recursos en caché.
> * Versiones de toocontrol almacenado en memoria caché de cadenas de consulta de uso.
> * Usar un dominio personalizado para el extremo de red CDN Hola.

Obtenga información acerca de cómo los artículos toooptimize de rendimiento de red CDN Hola siguientes:

> [!div class="nextstepaction"]
> [Mejora del rendimiento comprimiendo archivos en la red CDN de Azure](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Carga previa de activos en un punto de conexión de CDN de Azure](../cdn/cdn-preload-endpoint.md)
