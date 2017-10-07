---
title: "API del servicio de aplicaciones: ¿qué ha cambiado aaaApp | Documentos de Microsoft"
description: Consulte las novedades de las aplicaciones de API en el Servicio de aplicaciones de Azure.
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>Aplicaciones de API del Servicio de aplicaciones: lo que ha cambiado
En el evento de Connect() hello en noviembre de 2015, una serie de mejoras tooAzure servicio de aplicaciones estaban [anunció](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Estas mejoras incluyen cambios subyacentes tooAPI aplicaciones toobetter se alinean con las aplicaciones Web y móviles, reducir el recuento de concepto y mejorar el rendimiento de la implementación y en tiempo de ejecución. A partir del 30 de noviembre de 2015, nuevas aplicaciones de la API se crea mediante el portal de administración de Azure de Hola o herramientas más recientes de hello reflejarán estos cambios. En este artículo se describe estos cambios, así como el modo tooredeploy existente aplicaciones tootake aprovechar las capacidades de Hola.

## <a name="feature-changes"></a>Cambios de características
Hola características clave de las aplicaciones de API: autenticación, CORS y la API de metadatos: ha movido directamente en el servicio de aplicaciones. Con este cambio, características de hello están disponibles a través de Web, móviles y aplicaciones de API. De hecho, todos los recursos compartidos de tres Hola mismo **Microsoft.Web/sites** el tipo de recurso en el Administrador de recursos. puerta de enlace de aplicaciones de API de Hola ya no es necesario o que ofrece a las aplicaciones de API. Esto también resulta más fácil toouse administración de API de Azure ya que habrá simplemente Hola sola administración de API puerta de enlace.

![Introducción a las aplicaciones de API](./media/app-service-api-whats-changed/api-apps-overview.png)

Un principio clave del diseño con hello actualizar aplicaciones de API es tooenable toobring es la API como, en su idioma preferido.  Si la API ya está implementada como una aplicación Web o aplicación móvil, no es necesario tooredeploy su aplicación tootake aprovechar Hola nuevas características. Si actualmente usa la versión preliminar de Aplicaciones de API, a continuación se detallan las instrucciones de migración.

### <a name="authentication"></a>Autenticación
Hola existente llave en mano aplicaciones de API, servicios o aplicaciones móviles y aplicaciones Web funcionalidades de autenticación se han unificado y están disponibles en una única hoja de autenticación de servicio de aplicaciones de Azure en el portal de administración de Hola. Para una introducción tooauthentication los servicios en el servicio de aplicaciones, consulte [autenticación de servicio de aplicaciones de expansión / autorización](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

En escenarios de API, hay varias funcionalidades nuevas relacionadas:

* **Compatibilidad con el uso de Azure Active Directory directamente**, sin código de cliente con el token de AAD de hello tooexchange para obtener un token de sesión: el cliente puede simplemente incluyen tokens AAD de hello en el encabezado de autorización de hello, según el token de portador toohello especificación. Esto también significa que no se requiere ningún SDK específicos del servicio App en lado de cliente o servidor de Hola. 
* **Acceso al servicio o "Interno"**: si tiene un proceso de demonio o algún otro cliente que necesitan acceso tooAPIs sin una interfaz, puede solicitar un token con una entidad de seguridad de servicio AAD y pasarle tooApp servicio para la autenticación con su aplicación.
* **Diferida autorización**: muchas aplicaciones tienen restricciones de acceso diferentes para las distintas partes de la aplicación hello. Quizás desee algunos toobe de las API disponible públicamente, mientras que otros requieren inicio de sesión. característica de autenticación/autorización de Hello original estaba todo o nada, con todo el sitio Hola necesidad de inicio de sesión. Esta opción sigue existiendo, pero puede o bien permitir que el código de aplicación las decisiones de acceso de toorender después de que el servicio de aplicación ha autenticado el usuario de Hola.

Para obtener más información sobre las nuevas características de autenticación hello, consulte [autenticación y autorización para las aplicaciones de API de servicio de aplicaciones de Azure](app-service-api-authentication.md). Para obtener información acerca de cómo toomigrate aplicaciones de API existentes de aplicaciones de API de hello anteriores modelo toohello nuevo uno, vea [migrar aplicaciones de API existentes](#migrating-existing-api-apps) más adelante en este artículo.

### <a name="cors"></a>CORS
En lugar de una coma **MS_CrossDomainOrigins** aplicación establecer, ahora hay una hoja hello Azure portal de administración de configuración de CORS. Como alternativa, se puede configurar mediante herramientas del Administrador de recursos, como Azure PowerShell, CLI o el [Explorador de recursos](https://resources.azure.com/). Conjunto hello **cors** propiedad hello **Microsoft.Web/sites/config** tipo de recurso para el  **&lt;nombre del sitio&gt;/web** recursos. Por ejemplo:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Metadatos de API
hoja de definición de API de Hello ahora está disponible a través de Web, móviles y aplicaciones de API. En el portal de administración de hello, puede especificar una dirección url relativa o una dirección url absoluta que señala el punto de conexión de tooan esa representación hosts un Swagger 2.0 de la API. También se puede configurar mediante las herramientas del Administrador de recursos. Conjunto hello **apiDefinition** propiedad hello **Microsoft.Web/sites/config** tipo de recurso para el  **&lt;nombre del sitio&gt;/web** recursos. Por ejemplo:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

En este momento, extremo de metadatos de hello necesita toobe públicamente accesible sin autenticación para muchos de los clientes siguen en la cadena (por ejemplo, Visual Studio REST API cliente generación y PowerApps "Agregar API" flujo) de tooconsume lo. Esto significa que si está utilizando la autenticación de servicio de aplicaciones y desea definición de la API tooexpose Hola desde dentro de su propia aplicación, necesitará opción de autenticación de diferidas de hello toouse para que los metadatos de Swagger de hello ruta tooyour están público, se ha descrito anteriormente.

## <a name="management-portal"></a>Portal de administración
Seleccionar **nuevo > Web y móvil > API App** en hello portal va a crear aplicaciones de API que refleja las nuevas capacidades de hello descritas en el artículo Hola. **Examinar &gt; API Apps** mostrará solamente las nuevas aplicaciones de API. Una vez que se examina en una aplicación de API, recursos compartidos de hoja de Hola Hola mismo capacidades como si fuesen Web y aplicaciones móviles y diseño. Hola únicas diferencias son contenido de inicio rápido y el orden de configuración.

Aplicaciones de API existentes (o aplicaciones de API de Marketplace creadas a partir de las aplicaciones lógicas) con hello capacidades de Preview anteriores seguirán estando visibles en el Diseñador de aplicaciones de la lógica de Hola y al examinar todos los recursos de un grupo de recursos.

## <a name="visual-studio"></a>Visual Studio
Mayoría de las aplicaciones Web herramientas funcionará con nuevas aplicaciones de la API ya que comparten Hola subyacente mismo **Microsoft.Web/sites** tipo de recurso. Hola herramientas de Visual Studio de Azure, sin embargo, deben estar actualizado tooversion 2.8.1 o posterior, ya que expone una serie de capacidades específicas tooAPIs. Descargar Hola SDK de hello [página de descargas de Azure](https://azure.microsoft.com/downloads/).

Con racionalización Hola de hello tipos de servicio de aplicaciones, publicar también está unificado en **publicar > servicio de aplicaciones de Microsoft Azure**:

![Publicación de aplicaciones de API](./media/app-service-api-whats-changed/api-apps-publish.png)

más información sobre SDK 2.8.1, anuncio de Hola lectura toolearn [entrada de blog](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Como alternativa, puede importar manualmente Hola publicar el perfil de tooenable de portal de administración de hello publicar. Sin embargo, Cloud Explorer, la generación de código y la creación y selección de aplicaciones de API requerirán el SDK 2.8.1 o superior.

## <a name="migrating-existing-api-apps"></a>Migración de aplicaciones de API existentes
Si la API personalizada es toohello implementado de versión preliminar anterior de las aplicaciones de API, solicitamos migrar toohello nuevo modelo de aplicaciones de API por el 31 de diciembre de 2015. Dado que tanto el modelo de hello antiguos y nuevos se basa en la API de Web hospedadas en el servicio de aplicaciones, se puede reutilizar mayoría Hola de código existente.

### <a name="hosting-and-redeployment"></a>Hospedaje y reimplementación
pasos de Hola para volver a implementar se Hola igual que implementar cualquier tooApp de API Web servicio existente. Pasos:

1. Crear una aplicación de API vacía. Esto puede hacerse en el portal de hello con nuevo > API App, en Visual Studio de publicación o de herramientas del Administrador de recursos. Si usa herramientas de administrador de recursos o plantillas, establecer hello **tipo** valor demasiado**api** en hello **Microsoft.Web/sites** tutoriales rápidos Hola de toohave de tipo de recurso y la configuración de portal de administración de Hello orientado para escenarios de API.
2. Conectarse e implementar su proyecto toohello vacía API aplicación mediante cualquiera de los mecanismos de implementación de hello compatibles con el servicio de aplicación. Lectura [documentación de implementación de servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md) toolearn más. 

### <a name="authentication"></a>Autenticación
Hello compatibilidad con servicios de autenticación de servicio de aplicaciones Hola mismas capacidades que estaban disponibles con el modelo de aplicaciones de API de hello anterior. Si usa tokens de sesión y requieren SDK, use Hola después de SDK de cliente y servidor:

* Cliente: [SDK de cliente móvil de Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Servidor: [Extensión de autenticación de .NET para Aplicaciones móviles de Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Si estaba usando Hola alfa SDK de servicio de aplicaciones en su lugar, estos están en desuso:

* Cliente: [SDK del Servicio de aplicaciones de Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Servidor: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

En particular con Azure Active Directory, sin embargo, no específicos del servicio App es necesario si utilizas token de AAD Hola directamente.

### <a name="internal-access"></a>Acceso interno
modelo de aplicaciones de API de Hello anterior incluye un nivel de acceso interno integrados. Esto requería el uso de hello SDK para firmar las solicitudes. Como se describió anteriormente, el nuevo modelo de aplicaciones de API hello, entidades de servicio AAD pueden utilizarse como alternativa para la autenticación de servicio al servicio sin necesidad de un App específicos del servicio SDK. Puede obtener más información en [Autenticación de entidad de servicio para Aplicaciones de API en el Servicio de aplicaciones de Azure](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Detección
Hola modelo tenía las API para detectar otras aplicaciones de API en tiempo de ejecución en las aplicaciones de API anterior Hola mismo grupo de recursos detrás de Hola misma puerta de enlace. Esto es especialmente útil en las arquitecturas que implementan patrones de microservicio. Aunque esto no se admite directamente, hay varias opciones disponibles:

1. Usar la API del Administrador de recursos de Azure de hello para la detección.
2. Coloque Administración de API de Azure delante de sus API hospedadas por el Servicio de aplicaciones. Administración de API de Azure sirve como fachada y puede proporcionar una URL con orientación externa estable aunque cambie la topología interna.
3. Compile su propia aplicación de API de detección y tienen otras aplicaciones de API de registro con la aplicación de detección de hello en el inicio.
4. Durante la implementación, rellenar configuración de la aplicación hello de todas las aplicaciones de API de hello (y los clientes) con puntos de conexión de Hola de hello otras aplicaciones de API. Esto es viable en las implementaciones de plantilla y, como aplicaciones de API que le ofrecen control de dirección url de Hola.

## <a name="using-api-apps-with-logic-apps"></a>Uso de Aplicaciones de API con Aplicaciones lógicas
nuevo modelo de aplicaciones de API Hola funciona bien con [Logic Apps versión 2015-08-01 del esquema](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Pasos siguientes
toolearn más información, lea los artículos de Hola Hola [sección de documentación de aplicaciones de la API](https://azure.microsoft.com/documentation/services/app-service/api/). Han sido nuevo modelo de Hola de tooreflect actualizada para aplicaciones de API. Además, llegar en foros de Hola para obtener más información o instrucciones sobre la migración:

* [Foro de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

